---
title: タブのシングル サインオンのサポート
description: シングル サインオン (SSO) について説明します。
keywords: Teams 認証 SSO AAD シングル サインオン API
ms.openlocfilehash: 3eff1cd1d73573c8eaade63580516f432fe082a1
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731987"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>タブのシングル サインオン (SSO) のサポート

ユーザーは、自分の仕事、学校、または Microsoft アカウント (Office 365、Outlook など) を介して Microsoft Teams にサインインします。 これを利用するには、シングル サインオンを使用して、デスクトップまたはモバイル クライアントで Microsoft Teams タブ (またはタスク モジュール) を承認できます。 したがって、ユーザーがアプリの使用に同意した場合、別のデバイスでもう一度同意する必要はありません。ユーザーは自動的にサインインします。 さらに、アクセス トークンをプリフェッチして、パフォーマンスと読み込み時間を向上させます。

>[!NOTE]
> **SSO をサポートする Teams モバイル クライアントのバージョン**  
>
> ✔Teams for Android (1416/1.0.0.2020073101 以降)
>
> ✔ iOS 用のチーム (_バージョン_: 2.0.18 以降)  
>
> Teams で最高のエクスペリエンスを得る場合は、最新バージョンの iOS と Android を使用してください。

>[!NOTE]
> **クイックスタート**  
>
> タブ SSO の使用を開始する最も簡単な方法は、Microsoft Teams Toolkit for Visual Studio です。 [詳細情報](../../../toolkit/visual-studio-code-tab-sso.md)


## <a name="how-sso-works-at-runtime"></a>実行時の SSO の動作のしくみ

次の図は、SSO プロセスのしくみを示しています。

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. タブでは、JavaScript 呼び出しが実行されます `getAuthToken()` 。 これにより、タブ アプリケーションの認証トークンを取得する必要があります。
2. 現在のユーザーが初めてタブ アプリケーションを使用する場合は、同意を求める要求プロンプト (同意が必要な場合) またはステップ アップ認証 (2 要素認証など) の処理を求めるプロンプトが表示されます。
3. Teams は、現在のユーザーの Azure AD エンドポイントにタブ アプリケーション トークンを要求します。
4. Azure AD Teams アプリケーションにタブ アプリケーション トークンを送信します。
5. Teams は、呼び出しによって返される結果オブジェクトの一部としてタブ にタブ アプリケーション トークンを送信 `getAuthToken()` します。
6. トークンは、JavaScript を使用してタブ アプリケーションで解析され、ユーザーの電子メール アドレスなどの必要な情報を抽出します。

> [!NOTE]
> The is only valid for consenting to a `getAuthToken()` limited set of user-level APIs — email, profile, offline_access and OpenId — and not for further Microsoft Graph scopes such as or `User.Read` `Mail.Read` . 追加の Graph スコープが必要な場合に推奨される回避策については、このドキュメントの最後にあるセクション [を参照してください](#apps-that-require-additional-microsoft-graph-scopes)。

SSO API は、Web コンテンツを埋め [込むタスク モジュール](../../../task-modules-and-cards/what-are-task-modules.md) でも機能します。

## <a name="develop-an-sso-microsoft-teams-tab"></a>SSO Microsoft Teams タブを開発する

このセクションでは、SSO を使用する Teams タブの作成に関連するタスクについて説明します。 ここでは、これらのタスクについて、言語とフレームワークに依存しないタスクについて説明します。

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a>1. Azure Active Directory (Azure AD) アプリケーションを作成する

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a>Azure AD[ポータルでのアプリケーションの登録の](https://azure.microsoft.com/features/azure-portal/) 概要:

1. Azure AD [アプリケーション ID を取得します](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。
2. アプリケーションが Azure AD エンドポイントと、必要に応じて Microsoft Graph に必要なアクセス許可を指定します。
3. Teams[のデスクトップ、Web、](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)およびモバイル アプリケーションのアクセス許可を付与します。
4. [範囲の追加] ボタンを選択して Teams を事前承認し、開くパネルで、スコープ `access_as_user` 名として **入力します**。

> [!NOTE]
> 次の重要な制限に注意する必要があります。
>
> * ユーザー レベルの Microsoft Graph API のアクセス許可 (メール、プロファイル、offline_access、OpenId など) のみをサポートしています。 他の Microsoft Graph スコープ (またはなど) にアクセスする必要がある場合は、このドキュメントの最後にある推奨 `User.Read` `Mail.Read` される回避策を参照してください。 [](#apps-that-require-additional-microsoft-graph-scopes)
> * アプリケーションのドメイン名は、Azure AD アプリケーションに登録したドメイン名と同じ名前にすることが重要です。
> * 現在、アプリごとに複数のドメインはサポートされていません。
> * ドメインが一般的すぎるため、セキュリティ上のリスクが生じ得るアプリケーション `azurewebsites.net` はサポートされていません。 ただし、この制限を積極的に削除する必要があります。

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a>Azure Active Directory ポータルを使用してアプリを登録する方法について詳細に説明します。

1. Azure Active Directory アプリ登録ポータルに [新しいアプリケーションを登録](https://go.microsoft.com/fwlink/?linkid=2083908) します。
2. [ **新しい登録] を** 選択し、[アプリケーションの *登録] ページで* 次の値を設定します。
    * アプリ **名に** 名前を設定します。
    * サポートされている **アカウントの種類を選択** する (任意のアカウントの種類が機能します) ¹
    * **[リダイレクト URI]** を空のままにします。
    * **[登録]** を選択します。
3. 概要ページで、アプリケーション **(クライアント) ID をコピーして保存します**。 後で Teams アプリケーション マニフェストを更新するときに必要になります。
4. [**管理**] で [**API の公開**] を選択します。 
5. [Set] リンク **を** 選択して、アプリケーション ID URI を次の形式で生成します `api://{AppID}` 。 二重スラッシュと GUID の間に完全修飾ドメイン名 (末尾にスラッシュ "/" を付加) を挿入します。 ID 全体は次の形式である `api://fully-qualified-domain-name.com/{AppID}` 必要があります。
    * 例: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` .
    
    完全修飾ドメイン名は、アプリが提供される人間が読み取り可能なドメイン名です。 ngrok などのトンネリング サービスを使用している場合は、ngrok サブドメインが変更されるたびにこの値を更新する必要があります。 
6. **[Scope の追加]** ボタンをクリックします。 開いたパネルで、**[スコープ名]** として `access_as_user` を入力します。
7. 同意 **できるユーザーを設定** する `Admins and users`
8. 管理者とユーザーの同意のプロンプトを構成するためのフィールドに、範囲に適した値を入力 `access_as_user` します。
    * **管理者の同意のタイトル:** Teams はユーザーのプロファイルにアクセスできます。
    * **管理者の同意の説明**: Teams がアプリの Web API を現在のユーザーとして呼び出すのを許可します。
    * **ユーザーの同意のタイトル**: Teams はユーザー プロファイルにアクセスし、ユーザーに代わって要求を行うことができます。
    * **ユーザーの同意の説明:** Teams がユーザーと同じ権限でこのアプリの API を呼び出すのを有効にする。
9. [状態 **] が [有効** ] **に設定されている**
10. [範囲の **追加] ボタンを** 選択して保存する 
    * テキスト フィールドの下に **表示されるスコープ** 名のドメイン部分は、前の手順で設定したアプリケーション **ID** URI と自動的に一致し、末尾に追加 `/access_as_user` されます。
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. [ **承認済みクライアント アプリケーション** ] セクションで、アプリの Web アプリケーションに対して承認するアプリケーションを特定します。 [クライアント *アプリケーションの追加] を選択します*。 次の各クライアント ID を入力し、前の手順で作成した承認済みスコープを選択します。
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams モバイル/デスクトップ アプリケーション)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams Web アプリケーション)
12. API の **アクセス許可に移動します**。 [Microsoft Graph *委任されたアクセス* 許可のアクセス許可の追加] を選択し、Microsoft Graph API から次のアクセス  >    >  許可を追加します。
    * User.Read (既定で有効)
    * メール
    * offline_access
    * OpenId
    * profile

13. [認証] に **移動します**

    アプリに IT 管理者の同意が与えされていない場合、ユーザーは初めてアプリを使用する場合に同意する必要があります。

    リダイレクト URI を設定します。
    * [プラットフォーム **の追加] を選択します**。
    * Web を **選択します**。
    * アプリの **リダイレクト URI** を入力します。 これは、暗黙的な許可フローが成功するとユーザーがリダイレクトされるページです。 これは、手順 5 で入力した完全修飾ドメイン名と、認証応答を送信する API ルートと同じ名前です。 Teams のサンプルを実行している場合は、次のようになります。 `https://subdomain.example.com/auth-end`

    次に、次のボックスをオンにして、暗黙的な許可を有効にします。  
    ✔ ID トークン  
    ✔ アクセス トークン  
    
おめでとうございます! タブ SSO アプリを続行するには、アプリ登録の前提条件が完了しています。     

> [!NOTE]
>
> * ¹ Azure AD アプリが Teams で認証要求を行っているのと同じテナントに登録されている場合、ユーザーは同意を求められなく、アクセス トークンがすぐ付与されます。 ユーザーがこれらのアクセス許可に同意する必要があるのは、Azure ADアプリが別のテナントに登録されている場合のみです。
> * ドメインが既に所有され、自分が所有者であることを示すエラーが表示された場合は、「クイック スタート [: Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) にカスタム ドメイン名を追加してドメインを登録し、上記の手順 5 を繰り返します。 (このエラーは、Office 365 テナンシーで管理者の資格情報でサインインしていない場合にも発生します)。
> * 返されたアクセス トークンで UPN (ユーザー プリンシパル名) を受信していない場合は、Azure AD[](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)でオプションのクレームとして追加できます。

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. Microsoft Teams アプリケーション マニフェストを更新する

Microsoft Teams マニフェストに新しいプロパティを追加します。

* **WebApplicationInfo** - 次の要素の親。

> [!div class="checklist"]
> * **id** - アプリケーションのクライアント ID。 これは、Azure AD にアプリケーションを登録する一環として取得したアプリケーション ID です。
>* **resource** - アプリケーションのドメインとサブドメイン。 これは、上記の手順 6 で作成するときに登録した URI (プロトコルを含む `api://` ) `scope` と同じです。 リソースにパスを `access_as_user` 含めてはならない。 この URI のドメイン部分は、Teams アプリケーション マニフェストの URL で使用される任意のサブドメインを含むドメインと一致する必要があります。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* AAD アプリのリソースは、通常、サイト URL のルートと appID (例: ) です `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。 また、この値を使用して、要求が同じドメインから送信されるのを確認します。 したがって、タブのドメインがリソース プロパティと同 `contentURL` じドメインを使用する必要があります。
>* フィールドを実装するには、マニフェスト バージョン 1.5 以上を使用する必要 `webApplicationInfo` があります。

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. クライアント側コードから認証トークンを取得する

認証 API は次のように表示されます。

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

(ユーザー レベルのアクセス許可に対して) 呼び出しを行い、追加のユーザーの同意が必要な場合は、追加の同意を許可するダイアログがユーザーに `getAuthToken` 表示されます。 

成功コールバックでアクセス トークンを受信したら、アクセス トークンをデコードして、そのトークンに関連付けられているクレームを表示できます。 (必要に応じて、アクセス トークンを手動でコピー/貼り付け[](https://jwt.io/)(コンテンツを検査するJWT.ioツールなど) に貼り付けます。 返されたアクセス トークンで UPN (ユーザー プリンシパル名) を受信していない場合は、Azure AD[](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)でオプションのクレームとして追加できます。

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="sample-code"></a>サンプル コード

サンプル アプリケーションにアクセスする: [MSTeams PnP SSO サンプル](https://github.com/pnp/teams-dev-samples/tree/master/samples/tab-sso)

README では、開発環境をセットアップする方法と、Azure AD でアプリケーションを構成する方法について説明します。 また、コードベースを理解するのに役立つ、アプリの構造に関[](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure)するセクションで、サンプルがどのように構成されているのかについて詳しい情報を確認することもできます。

## <a name="known-limitations"></a>既知の制限事項

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a>追加の Microsoft Graph スコープが必要なアプリ

SSO の現在の実装では、他の API (User.Read や Mail.Read など) ではなく、ユーザー レベルのアクセス許可 (電子メール、プロファイル、offline_access、OpenId) に対する同意のみを付与します。 アプリにさらに Microsoft Graph スコープが必要な場合は、いくつかの有効な回避策を次に示します。

#### <a name="tenant-admin-consent"></a>テナント管理者の同意

最も簡単な方法は、テナント管理者に組織の代わりに事前同意を得る方法です。 つまり、ユーザーはこれらのスコープに同意する必要がならないので、Azure AD の代理フローを使用してトークン サーバー側を自由に交換 [できます](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。 この回避策は、内部の業務アプリケーションでは許容されますが、テナント管理者の承認に依存できないサードパーティの開発者には十分ではない可能性があります。

(テナント管理者として) 組織の代わりに同意する簡単な方法は、次にアクセスする方法です。

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Auth API を使用して追加の同意を求める

追加の Microsoft Graph スコープを取得するためのもう 1 つのアプローチは、既存の Web ベースの [Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) 認証アプローチを使用して同意ダイアログを表示する方法です。この認証方法では、Azure AD 同意ダイアログが表示されます。 いくつかの追加機能があります。

1. 取得するトークンは、追加の Microsoft Graph API にアクセスするために `getAuthToken()` 、Azure AD [on-behalf-of フロー](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) を使用してサーバー側で交換する必要があります。
    * この交換には必ず v2 Microsoft Graph エンドポイントを使用してください。
2. Exchange が失敗した場合、Azure AD無効な付与例外が返されます。 通常、次の 2 つのエラー メッセージの 1 `invalid_grant` つがあります。 `interaction_required`
3. 交換が失敗した場合は、追加の同意を求める必要があります。 ユーザーに追加の同意を求める UI を表示することをお勧めします。 この UI には、Azure 認証 API を使用して Azure AD同意ダイアログ [をトリガーするAD含める必要があります](~/concepts/authentication/auth-silent-aad.md)。
4. Azure AD から追加の同意を求める場合は、Azure AD へのクエリ文字列パラメーターに含める必要があります。それ以外の場合 `prompt=consent` 、Azure AD[](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)は追加のスコープを求めしません。
    * 代わりに： `?scope={scopes}`
    * 次のコマンドを使用します。 `?prompt=consent&scope={scopes}`
    * ユーザーに確認を求めるすべてのスコープ `{scopes}` (Mail.Read や User.Read など) を含める必要があります。
5. ユーザーが追加のアクセス許可を付与したら、代理フローを再試行して、これらの追加の API にアクセスします。

### <a name="non-azure-ad-authentication"></a>Azure 以外のAD認証

上記の認証ソリューションは、AZURE 認証をサポートするアプリとサービスADプロバイダーとしてのみ機能します。 Azure ベース以外のサービスを使用してADするアプリは、ポップアップ ベースの Web 認証フローを引き続き [使用する必要があります](~/concepts/authentication.md)。
