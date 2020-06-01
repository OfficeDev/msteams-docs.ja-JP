---
title: シングル サインオン
description: シングルサインオン (SSO) について説明します。
keywords: teams 認証 SSO AAD
ms.openlocfilehash: 8f9d94346aad7c096e4310f80b6cda73856afc8c
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455514"
---
# <a name="single-sign-on"></a>シングル サインオン

> [!NOTE]
> 現在、"シングルサインオン" API は_開発者向けプレビュー_でのみサポートされています。

ユーザーが職場または学校 (Office 365) アカウントを使用して Microsoft Teams にサインインし、シングルサインオン (SSO) を使用して Microsoft Teams タブにユーザーを承認することで、この機能を利用できるようになります。これは、ユーザーがデスクトップでアプリを使用することを同意する場合、モバイルで再び同意する必要がなく、自動的にログインされることを意味します。 

## <a name="how-sso-works-at-runtime"></a>実行時の SSO の動作のしくみ

次の図は、SSO プロセスのしくみを示しています。

<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. タブで、JavaScript は getAuthToken () を呼び出します。 これにより、Teams アプリケーションに対して、タブアプリケーションへの認証トークンを取得するように指示します。
2. 現在のユーザーが初めてタブアプリケーションを使用していた場合は、同意を求めるメッセージが表示されます (同意が必要な場合)。または、手順アップ認証 (2 要素認証など) の処理を求められます。
3. Microsoft Teams アプリケーションは、現在のユーザーの Azure AD v2.0 エンドポイントからタブアプリケーショントークンを要求します。
4. Azure AD は、タブアプリケーショントークンを Teams アプリケーションに送信します。
5. Microsoft Teams アプリケーションは、getAuthToken () 呼び出しによって返される result オブジェクトの一部として、タブにタブアプリケーショントークンを送信します。
6. タブアプリケーションの JavaScript は、トークンを解析し、ユーザーの電子メールアドレスなど、必要な情報を抽出できます。
    * 注: このトークンは、限られたレベルのユーザーレベルの Api (例: 電子メール、プロファイルなど) に対してのみ有効であり、その他のグラフスコープ (同意など) では使用できません。 追加のグラフスコープが必要な場合の回避策については、このドキュメントの最後にあるセクションを参照してください。

## <a name="develop-an-sso-microsoft-teams-tab"></a>SSO Microsoft Teams タブを開発する

このセクションでは、SSO を使用する Microsoft Teams タブの作成に関連するタスクについて説明します。 ここでは、これらのタスクについて、言語とフレームワークに依存しない方法で説明しています。

### <a name="1-create-your-aad-application-in-azure"></a>1. Azure で AAD アプリケーションを作成する

Azure AD v2.0 エンドポイントの登録ポータルでアプリケーションを登録します。 このプロセスには、次に示すタスクを含めて 5 分から 10 分の時間がかかります。

* AAD アプリケーション ID を取得する
* AAD エンドポイント (およびオプションで Microsoft Graph) に対してアプリケーションに必要なアクセス許可を指定します。 
* アプリケーションに信頼するように Microsoft Teams デスクトップ、web、モバイルアプリケーションに付与する
* 既定のスコープ名を使用して、アプリに対して Microsoft Teams アプリケーションを事前認証し `access_as_user` ます。

> [!NOTE]
> 注意すべき重要な制限がいくつかあります。
>
> * ユーザーレベルの Graph API アクセス許可 (電子メール、プロファイル、offline_access、openid など) のみがサポートしています。 他のグラフスコープにアクセスする必要がある場合は、このドキュメントの最後にある「推奨される回避策」をお読みください。
> * アプリケーションのドメイン名が Azure AD アプリケーションに登録されていることが重要です。 これは、Teams で認証トークンを要求するときにアプリケーションが実行するドメイン名と同じである必要があります。また、Teams のマニフェストでリソースのプロパティを指定するときにも、次のセクションの詳細について説明します。
> * 現在、アプリごとに複数のドメインをサポートしていません
> * また、このドメインが一般的すぎるためにドメインを使用するアプリケーションをサポートしておらず、 `azurewebsites.net` セキュリティリスクになる可能性もあります。

#### <a name="steps"></a>手順

1. 新しいアプリケーションを[Azure Active Directory に登録する–アプリ登録](https://go.microsoft.com/fwlink/?linkid=2083908)ポータル
2. [新しい登録] を選択します。 [アプリケーションの登録] ページで、次のように値を設定します。
    * **名前**をアプリ名に設定します。
    * **任意の組織ディレクトリおよび個人の Microsoft アカウントのアカウント**に**サポートされているアカウントの種類**を設定する
    * **リダイレクト URI**を空のままにする
    * [**登録**] を選択する
3. [概要] ページで、**アプリケーション (クライアント) ID**をコピーして保存します。 Teams アプリケーションマニフェストを更新するときには、後で必要になります。
4. **[管理]** の下の **[API の公開]** を選択します。 [**設定**] リンクを選択して、アプリケーション ID URI をの形式で生成し `api://{AppID}` ます。 二重スラッシュと GUID の間に、完全修飾ドメイン名 (末尾にスラッシュ "/" を付加したもの) を挿入します。 ID 全体の形式は次のようになります。`api://fully-qualified-domain-name.com/{AppID}`
    * ex: `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7` 。

> [!NOTE]
> ドメインを所有しているにもかかわらず、そのドメインが既に所有されているというエラーが表示される場合は、「[クイック スタート: カスタム ドメイン名を Azure Active Directory に追加する](/azure/active-directory/fundamentals/add-custom-domain)」の手順に従って登録し、この手順を繰り返します。 このエラーは、Office 365 テナントの管理者の資格情報を使用してサインインしていない場合にも発生します。

5. **[Scope の追加]** ボタンをクリックします。 開いたパネルで、**[スコープ名]** として `access_as_user` を入力します。
6. 同意できるユーザーを設定する管理者とユーザーに対して
7. [管理者] と [ユーザーの同意] の入力を構成するためのフィールドに、範囲に適した値を入力し `access_as_user` ます。 提案:
    * **管理者の同意のタイトル:** Teams はユーザーのプロファイルにアクセスできます
    * **管理者の同意の説明**: Teams は、現在のユーザーとしてアプリの web api を呼び出すことができます。
    * **ユーザーの同意のタイトル**: Teams はユーザープロファイルにアクセスして、自分の代わりに要求を行うことができます。
    * **ユーザーの同意の説明:** Teams が同じ権限でこのアプリの Api を呼び出せるようにします。
8. **状態**が**有効**に設定されていることを確認する
9. [**範囲の追加**] を選択します。
    * 注: テキストフィールドのすぐ下に表示される**スコープ名**のドメイン部分は、末尾に追加された、前の手順で設定した**アプリケーション ID** URI に自動的に一致する必要があります。 `/access_as_user` 次に例を示します。 
        * `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7/access_as_user`
10. [承認された**クライアントアプリケーション**] セクションで、アプリの web アプリケーションに承認するアプリケーションを特定します。 次の各 Id を入力する必要があります。
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`(Teams モバイル/デスクトップアプリケーション)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`(Teams web アプリケーション)
11. [ **API アクセス許可**] に移動し、次のアクセス許可を追加していることを確認してください。
    * User. 読み取り (既定では有効)
    * メール
    * offline_access
    * openid
    * profile

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. Microsoft Teams アプリケーションマニフェストを更新する

Microsoft Teams のマニフェストに新しいプロパティを追加します。

* **WebApplicationInfo** - 次の要素の親。
* **Id** -アプリケーションのクライアント id。 これは、アプリケーションを Azure AD 1.0 エンドポイントに登録する際に取得するアプリケーション ID です。
* **Resource** -アプリケーションのドメインとサブドメイン。 これは、 `api://` AAD にアプリを登録するときに使用したものと同じ URI (プロトコルを含む) です。 この URI のドメイン部分は、Teams アプリケーションマニフェストのセクションの Url で使用されているすべてのサブドメインを含むドメインと一致する必要があります。

```json
"webApplicationInfo": {
  "id": "<application_GUID here>",
  "resource": "<web_API resource here>"
}
```

注:

* AAD アプリのリソースは、通常、そのサイトの URL と appID (例) のルートにすぎ `api://subdomain.example.com/6789/c6c1f32b-5e55-4997-881a-753cc1d563b7` ません。 また、この値を使用して、要求が同じドメインから送信されるようにします。 Therefor `contentURL` タブのがリソースプロパティと同じドメインを使用していることを確認してください。
* これらのフィールドを使用するには、マニフェストバージョン1.5 またはそれ以降を使用する必要があります。
* 範囲はマニフェストではサポートされていません。代わりに、Azure portal の API 権限セクションで指定する必要があります。

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. クライアント側のコードから認証トークンを取得する

認証 API は次のようになります。

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); },
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

`getAuthToken`を呼び出して、ユーザーレベルの権限に対してユーザーの同意を追加する必要がある場合は、追加の同意を付与するためのダイアログがユーザーに表示されます。 

<img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>

## <a name="demo-code"></a>デモコード

ここでは、「test application [Task Meow](https://github.com/ydogandjiev/taskmeow) 」を参照し、SSO マニフェストを使用して、およびファイルをチェックアウトし、 `teams.auth.service.js` `sso.auth.service.js` 認証ワークフローの処理方法を確認できます。

## <a name="known-limitations"></a>既知の制限

### <a name="apps-that-require-additional-graph-scopes"></a>追加のグラフスコープが必要なアプリ

現在の SSO の実装では、ユーザーレベルのアクセス許可 (電子メール、プロファイル、offline_access、openid) に対する同意のみが付与されますが、その他の Api (メールなど) については同意しません。 アプリにさらにグラフスコープが必要な場合は、これを有効にするための回避策がいくつかあります。

#### <a name="tenant-admin-consent"></a>テナント管理者の同意

最も簡単な方法は、テナント管理者が組織の代わりに事前同意を得ることです。 これは、ユーザーがこれらのスコープに同意する必要がないことを意味します。これにより、AAD の送信[フロー](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)を使用してトークンサーバー側を自由に交換できるようになります。 内部の基幹業務アプリケーションではこの回避策は許容されますが、テナント管理者の承認を利用できない可能性がある Isv にとっては十分ではない場合があります。

組織の代わりに (テナント管理者として) 同意を簡単に参照するには、次のようにします。

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Auth API を使用して追加の同意を求める

追加のグラフスコープを取得するためのもう1つの方法は、既存[の web ベースの aad 認証方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)を使用して、aad 同意ダイアログをポップアップするという同意ダイアログを表示することです。 注目すべき追加事項がいくつかあります。

1. GetAuthToken を使用して取得したトークンは、その追加の Graph Api へのアクセスを取得するために、[代理送信フロー](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)を使用してサーバー側を交換する必要があります。
    * 必ず、この exchange の v2 Graph エンドポイントを使用してください。
2. Exchange に障害が発生した場合、AAD は無効な付与の例外を返します。 通常、次の2つのエラーメッセージのいずれかがあります。 `ConsentRequired``InteractionRequired`
3. Exchange に障害が発生した場合は、追加の同意を求める必要があります。 ユーザーに追加の同意を付与するように求める UI を表示することをお勧めします。 この UI には、 [aad 認証 API](~/concepts/authentication/auth-silent-aad.md)を使用して aad 同意ダイアログをトリガーするボタンが含まれている必要があります。
4. AAD から追加の同意を求めている場合は、aad `prompt=consent` に[クエリ文字列-パラメーター](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)を含める必要があります。それ以外の場合、aad は追加のスコープを要求しません。
    * 代わりに：`?scope={scopes}`
    * 使用するもの:`?prompt=consent&scope={scopes}`
    * ユーザーに対して要求しているすべてのスコープが含まれていることを確認してください `{scopes}` (例: Mail. read または user. read)。
5. ユーザーが追加のアクセス許可を付与した後、代理送信を再試行して、追加の Api へのアクセス権を取得します。

### <a name="non-aad-authentication"></a>非 AAD 認証

前述の認証ソリューションは、id プロバイダーとして Azure AD をサポートするアプリとサービスに対してのみ機能します。 AAD 以外のサービスを使用して認証するアプリは、ポップアップベースの[web 認証フロー](~/concepts/authentication.md)を引き続き使用する必要があります。
