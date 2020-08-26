---
title: シングル サインオン
description: シングルサインオン (SSO) について説明します。
keywords: teams 認証 SSO AAD シングルサインオン api
ms.openlocfilehash: 503d5ff9779224d922ab0d45c6e2a3b33d7e0de7
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874857"
---
# <a name="single-sign-on-sso"></a>シングルサインオン (SSO)

ユーザーは、職場、学校、または Microsoft アカウント (Office 365、Outlook など) 経由で Microsoft Teams にサインインします。 この機能を利用すると、シングルサインオンで、デスクトップまたはモバイルクライアントの Microsoft Teams タブ (またはタスクモジュール) を承認できるようになります。 そのため、ユーザーがアプリを使用することに同意場合は、別のデバイスで再び同意する必要はありません。自動的にサインインされます。 また、アクセストークンをプリフェッチして、パフォーマンスと負荷の時間を短縮します。

>[!NOTE]
> **SSO をサポートする Teams モバイルクライアントバージョン**  
>
> Android 用の✔ Teams (1416/1.0.0.2020073101 以降)
>
> ✔ Teams for iOS (_バージョン_: 2.0.18 以降)  
>
> Teams でのベストな利便性を実現するため、iOS と Android の最新バージョンをご利用ください。

## <a name="how-sso-works-at-runtime"></a>実行時の SSO の動作のしくみ

次の図は、SSO プロセスのしくみを示しています。

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. タブで、に対して JavaScript 呼び出しが行われ `getAuthToken()` ます。 これにより、チームはタブアプリケーションの認証トークンを取得するように指示されます。
2. 現在のユーザーが初めてタブアプリケーションを使用していた場合は、同意を求めるメッセージが表示されます (同意が必要な場合)。または、ステップアップ認証 (2 要素認証など) を処理するための要求があります。
3. Teams は、現在のユーザーの Azure AD エンドポイントからタブアプリケーショントークンを要求します。
4. Azure AD は、タブアプリケーショントークンを Teams アプリケーションに送信します。
5. チームは、呼び出しによって返される result オブジェクトの一部として、タブにタブアプリケーショントークンを送信し `getAuthToken()` ます。
6. このトークンは、JavaScript を使用してタブアプリケーションで解析され、ユーザーの電子メールアドレスなど、必要な情報を抽出します。

> [!NOTE]
> は、 `getAuthToken()` 同意に対してのみ、ユーザーレベルの api の制限付きセット (電子メール、プロファイル、offline_access および OpenId) に対してのみ有効です `User.Read` 。また、またはなどの Microsoft Graph スコープでは使用できません `Mail.Read` 。 [追加のグラフスコープ](#apps-that-require-additional-microsoft-graph-scopes)が必要な場合の回避策については、このドキュメントの最後にあるセクションを参照してください。

SSO API は、web コンテンツを埋め込む [タスクモジュール](../../../task-modules-and-cards/what-are-task-modules.md) でも動作します。

## <a name="develop-an-sso-microsoft-teams-tab"></a>SSO Microsoft Teams タブを開発する

このセクションでは、SSO を使用する Teams タブの作成に関連するタスクについて説明します。 これらのタスクについては、言語とフレームワークに依存しません。

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a>1. Azure Active Directory (Azure AD) アプリケーションを作成する

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a>[AZURE AD ポータル](https://azure.microsoft.com/features/azure-portal/)でのアプリケーションの登録の概要:

1. [AZURE AD アプリケーション ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)を取得します。
2. Azure AD エンドポイントと、必要に応じて Microsoft Graph に対してアプリケーションに必要なアクセス許可を指定します。
3. Teams デスクトップ、web、モバイルアプリケーションに[アクセス許可を付与](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)します。
4. 事前承認する [ **スコープの追加** ] ボタンを選択し、表示されるパネルで、 `access_as_user` **範囲名**としてを入力します。

> [!NOTE]
> 注意すべき重要な制限がいくつかあります。
>
> * ユーザーレベルの Microsoft Graph API アクセス許可 (電子メール、プロファイル、offline_access、OpenId) のみがサポートしています。 他の Microsoft Graph スコープ (やなど) へのアクセスが必要な場合は `User.Read` `Mail.Read` 、このドキュメントの最後にある [推奨回避策](#apps-that-require-additional-microsoft-graph-scopes) を参照してください。
> * アプリケーションのドメイン名が Azure AD アプリケーションに登録したドメイン名と同じであることが重要です。
> * 現在、アプリごとに複数のドメインをサポートしていません。
> * `azurewebsites.net`ドメインは一般的すぎるため、セキュリティ上のリスクがある場合があるため、ドメインを使用するアプリケーションはサポートされていません。 しかし、この制限を排除することを積極的に目指しています。

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a>Azure Active Directory ポータルを使用してアプリを詳細に登録する:

1. 新しいアプリケーションを [Azure Active Directory –アプリ登録](https://go.microsoft.com/fwlink/?linkid=2083908) ポータルに登録します。
2. [ **新規登録** ] を選択し、[ *アプリケーションの登録] ページ*で、次の値を設定します。
    * **名前**をアプリ名に設定します。
    * **サポートされているアカウントの種類**(任意のアカウントの種類が機能する) を選択します。
    * **[リダイレクト URI]** を空のままにします。
    * **[登録]** を選択します。
3. [概要] ページで、 **アプリケーション (クライアント) ID**をコピーして保存します。 Teams アプリケーションマニフェストを更新するときには、後で必要になります。
4. [**管理**] で [**API の公開**] を選択します。 
5. [ **設定** ] リンクを選択して、アプリケーション ID URI をの形式で生成し `api://{AppID}` ます。 二重スラッシュと GUID の間に、完全修飾ドメイン名 (末尾にスラッシュ "/" を付加したもの) を挿入します。 ID 全体の形式は次のようにする必要があります: `api://fully-qualified-domain-name.com/{AppID}` ²
    * ex: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。
    
    完全修飾ドメイン名は、アプリが提供される人間が読むことができるドメイン名です。 Ngrok などのトンネリングサービスを使用している場合は、ngrok サブドメインが変更されるたびにこの値を更新する必要があります。 
6. **[Scope の追加]** ボタンをクリックします。 開いたパネルで、**[スコープ名]** として `access_as_user` を入力します。
7. **同意できるユーザー**を設定するには`Admins and users`
8. [管理者] と [ユーザーの同意] プロンプトを構成するためのフィールドに、範囲に適した値を入力し `access_as_user` ます。
    * **管理者の同意のタイトル:** Teams は、ユーザーのプロファイルにアクセスできます。
    * **管理者の同意の説明**: Teams は、現在のユーザーとしてアプリの web api を呼び出すことができます。
    * **ユーザーの同意のタイトル**: Teams はユーザープロファイルにアクセスし、ユーザーに代わって要求を行うことができます。
    * **ユーザーの同意の説明:** Teams が、ユーザーと同じ権限でこのアプリの Api を呼び出せるようにします。
9. **状態**が**有効**に設定されていることを確認する
10. [ **スコープの追加** ] ボタンを選択して保存します。 
    * テキストフィールドのすぐ下に表示される **スコープ名** のドメイン部分は、前の手順で設定した **アプリケーション ID** URI を `/access_as_user` 次の末尾に追加して自動的に一致する必要があります。
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. [承認された **クライアントアプリケーション** ] セクションで、アプリの web アプリケーションに対して承認するアプリケーションを特定します。 [ *クライアントアプリケーションの追加*] を選択します。 次の各クライアント Id を入力し、前の手順で作成した承認済みスコープを選択します。
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams モバイル/デスクトップアプリケーション)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams web アプリケーション)
12. [ **API アクセス許可**に移動します。 [*アクセス許可を追加する*  >  *Microsoft Graph*の委任された  >  *アクセス許可*] を選択し、次のアクセス許可を追加します。
    * User. 読み取り (既定では有効)
    * メール
    * offline_access
    * OpenId
    * profile

13. [**認証**に移動します。

    アプリに管理者の同意が与えられていない場合、ユーザーはアプリを初めて使用するときに同意を得る必要があります。

    リダイレクト URI を設定します。
    * [ **プラットフォームの追加**] を選択します。
    * [ **Web**] を選択します。
    * アプリの **リダイレクト URI** を入力します。 これは、暗黙的な付与フローが成功した場合にユーザーをリダイレクトするページになります。 これは、手順5で入力したのと同じ完全修飾ドメイン名となり、認証応答を送信する API ルートが続きます。 Teams のサンプルのいずれかをフォローしている場合は、次のようになります。 `https://subdomain.example.com/auth-end`

    次に、以下のチェックボックスをオンにして暗黙的な付与を有効にします。  
    ✔ ID トークン  
    ✔アクセストークン  
    
おめでとうございます! Prerequsities アプリの登録を完了し、タブ SSO アプリを続行します。     

> [!NOTE]
>
> * * Teams で認証要求を行うのと _同じ_ テナントに Azure AD アプリが登録されている場合は、ユーザーに同意を求められず、アクセストークンがすぐに付与されます。 ユーザーは、Azure AD アプリが別のテナントに登録されている場合にのみ、これらのアクセス許可に同意する必要があります。
> * ²ドメインが既に所有されていて所有者であることを示すエラーが表示された場合は、「 [クイックスタート: カスタムドメイン名を Azure Active Directory に追加](/azure/active-directory/fundamentals/add-custom-domain) してドメインを登録する」の手順に従って、上記の手順5を繰り返します。 (このエラーは、Office 365 テナントの管理者の資格情報を使用してサインインしていない場合にも発生する可能性があります)。
> * 返されたアクセストークンで UPN (ユーザープリンシパル名) を受信していない場合は、Azure AD に [オプションの要求](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) として追加できます。

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. Microsoft Teams アプリケーションマニフェストを更新する

Microsoft Teams のマニフェストに新しいプロパティを追加します。

* **Webapplicationinfo** -次の要素の親。

> [!div class="checklist"]
> * **id** -アプリケーションのクライアント id。 これは、アプリケーションを Azure AD に登録する際に取得したアプリケーション ID です。
>* **resource** -アプリケーションのドメインとサブドメイン。 これは、 `api://` 上記の手順6でを作成するときに登録したものと同じ URI (プロトコルを含む) です `scope` 。 リソースにパスを含めることはでき `access_as_user` ません。 この URI のドメイン部分は、Teams アプリケーションマニフェストの Url で使用されるすべてのサブドメインを含むドメインと一致する必要があります。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* AAD アプリのリソースは、通常、そのサイト URL と appID のルートになります (例: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` )。 また、この値を使用して、要求が同じドメインから送信されるようにします。 そのため、の `contentURL` タブのがリソースプロパティと同じドメインを使用していることを確認してください。
>* フィールドを実装するには、マニフェストバージョン1.5 以降を使用する必要があり `webApplicationInfo` ます。

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

成功のコールバックでアクセストークンを受信したら、アクセストークンをデコードして、そのトークンに関連付けられているクレームを表示することができます。 (オプションで、アクセストークンを [JWT.io](https://jwt.io/) などのツールに手動でコピー/貼り付けて、そのコンテンツを検査することもできます)。 返されたアクセストークンで UPN (ユーザープリンシパル名) を受信していない場合は、Azure AD に [オプションの要求](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) として追加できます。

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="sample-code"></a>サンプル コード

サンプルアプリケーションを参照してください。 [Msteams TAB SSO サンプル-Nodejs](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs)

この README では、開発環境をセットアップする方法と、Azure AD でアプリケーションを構成する方法について説明しています。 また、このサンプルが [「アプリ構造」セクション](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure) でどのように構造化されているかについては、コードベースの理解に役立つ情報もあります。

## <a name="known-limitations"></a>既知の制限

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a>追加の Microsoft Graph スコープが必要なアプリ

現在の SSO の実装では、ユーザーレベルのアクセス許可 (電子メール、プロファイル、offline_access、OpenId) に対してのみ同意が付与されます。他の Api (ユーザーによる読み取りまたはメールなど) に対しては使用できません。 アプリにさらに Microsoft Graph のスコープが必要な場合は、次のいくつかの回避策を参照してください。

#### <a name="tenant-admin-consent"></a>テナント管理者の同意

最も簡単な方法は、テナント管理者に組織の代わりに事前の同意を得ることです。 これは、ユーザーがこれらのスコープに同意する必要がなく、Azure AD の送信 [フロー](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)を使用してトークンサーバー側を自由に交換できることを意味します。 この回避策は内部の基幹業務アプリケーションには適していますが、テナント管理者の承認を利用できない可能性があるサードパーティの開発者には十分ではない可能性があります。

組織の代わりに (テナント管理者として) 同意を簡単に参照するには、次のようにします。

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Auth API を使用して追加の同意を求める

追加の Microsoft Graph スコープを取得するためのもう1つの方法は、既存の [web ベースの AZURE ad 認証方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) を使用して、azure ad 同意ダイアログをポップアップするという同意ダイアログを表示することです。 注目すべき追加事項がいくつかあります。

1. を使用して取得したトークンは、その `getAuthToken()` 他の Microsoft Graph api にアクセスするために、AZURE AD [の代理送信フロー](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) を使用して、サーバー側を交換する必要があります。
    * この exchange では、v2 Microsoft Graph エンドポイントを使用してください。
2. Exchange に障害が発生した場合、Azure AD は無効な付与の例外を返します。 通常、次の2つのエラーメッセージのいずれかがあります。 `invalid_grant``interaction_required`
3. Exchange に障害が発生した場合は、追加の同意を求める必要があります。 ユーザーに追加の同意を付与するように求める UI を表示することをお勧めします。 この UI には、azure [ad 認証 API](~/concepts/authentication/auth-silent-aad.md)を使用して azure ad 同意ダイアログをトリガーするボタンが含まれている必要があります。
4. Azure ad から追加の同意を求める場合は、azure ad `prompt=consent` に [クエリ文字列-パラメーター](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) を含める必要があります。それ以外の場合、azure ad は追加のスコープを要求しません。
    * 代わりに： `?scope={scopes}`
    * 使用するもの: `?prompt=consent&scope={scopes}`
    * ユーザーに対して要求しているすべてのスコープが含まれていることを確認してください `{scopes}` (例: Mail. read または user. read)。
5. ユーザーが追加のアクセス許可を付与した後、代理送信を再試行して、追加の Api へのアクセス権を取得します。

### <a name="non-azure-ad-authentication"></a>非 Azure AD 認証

前述の認証ソリューションは、id プロバイダーとして Azure AD をサポートするアプリとサービスに対してのみ機能します。 非 Azure AD ベースのサービスを使用して認証するアプリケーションは、ポップアップベースの [web 認証フロー](~/concepts/authentication.md)を引き続き使用する必要があります。
