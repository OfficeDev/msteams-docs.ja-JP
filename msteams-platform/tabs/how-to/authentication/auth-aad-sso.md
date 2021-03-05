---
title: タブのシングル サインオンのサポート
description: シングル サインオン (SSO) について説明します。
ms.topic: how-to
keywords: teams 認証 SSO AAD シングル サインオン API
ms.openlocfilehash: 7b8406473b8356b9c26948641b49f7e1239e697a
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449263"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>タブのシングル サインオン (SSO) のサポート

ユーザーは、自分の仕事、学校、または Microsoft アカウント (Office 365、Outlook など) を介して Microsoft Teams にサインインします。 これを利用するには、シングル サインオンでデスクトップまたはモバイル クライアントで Microsoft Teams タブ (またはタスク モジュール) を承認できます。 したがって、ユーザーがアプリの使用に同意した場合、別のデバイスでもう一度同意する必要はありません。自動的にサインインします。 さらに、パフォーマンスと読み込み時間を向上させるためにアクセス トークンをプリフェッチします。

> [!NOTE]
> **SSO をサポートする Teams モバイル クライアントのバージョン**  
>
> ✔Teams for Android (1416/1.0.0.2020073101 以降)
>
> ✔Teams for iOS (_バージョン_: 2.0.18 以降)  
>
> Teams で最高のエクスペリエンスを得る場合は、最新バージョンの iOS と Android を使用してください。

> [!NOTE]
> **クイックスタート**  
>
> タブ SSO の使用を開始する最も簡単なパスは、Microsoft Teams ToolkitコードVisual Studioです。 [詳細情報](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>実行時の SSO の動作のしくみ

次の図は、SSO プロセスの動作を示しています。

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. タブで、 に JavaScript 呼び出しが行います `getAuthToken()` 。 これにより、タブ アプリケーションの認証トークンを取得する必要があります。
2. 現在のユーザーが初めてタブ アプリケーションを使用した場合は、同意を求める要求プロンプト (同意が必要な場合) や、ステップ アップ認証 (2 要素認証など) を処理する要求プロンプトが表示されます。
3. Teams は、現在のユーザーの Azure ADアプリケーション トークンを要求します。
4. Azure AD、タブ アプリケーション トークンを Teams アプリケーションに送信します。
5. Teams は、呼び出しによって返される結果オブジェクトの一部としてタブ アプリケーション トークンをタブに送信 `getAuthToken()` します。
6. トークンは、JavaScript を介してタブ アプリケーションで解析され、ユーザーの電子メール アドレスなどの必要な情報を抽出します。

> [!NOTE]
> これは `getAuthToken()` 、電子メール、プロファイル、offline_access、OpenId など、ユーザー レベルの API の制限されたセットに同意する場合にのみ有効であり、それ以上の Microsoft Graph スコープでは有効ではありません `User.Read` `Mail.Read` 。 追加の Graph スコープが必要な場合の回避策については、このドキュメントの最後のセクション [を参照してください](#apps-that-require-additional-microsoft-graph-scopes)。

SSO API は、Web コンテンツを埋 [め込むタスク モジュール](../../../task-modules-and-cards/what-are-task-modules.md) でも機能します。

## <a name="develop-an-sso-microsoft-teams-tab"></a>[SSO Microsoft Teams] タブの開発

このセクションでは、SSO を使用する Teams タブの作成に関連するタスクについて説明します。 これらのタスクについては、言語とフレームワークに依存しないタスクについて説明します。

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a>1. Azure Active Directory (Azure Active Directory AD) アプリケーションを作成する

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a>Azure ADポータル[の概要にアプリケーションを登録](https://azure.microsoft.com/features/azure-portal/) します。

1. Azure の [アプリケーション ID AD取得します](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。
2. Azure のエンドポイントおよび必要に応じて、アプリケーションAD Microsoft Graph に必要なアクセス許可を指定します。
3. [Teams デスクトップ、Web、](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) およびモバイル アプリケーションのアクセス許可を付与します。
4. [スコープの追加] ボタンを選択して Teams を事前承認し、開くパネルで [スコープ `access_as_user` 名] と **入力します**。

> [!NOTE]
> 注意する必要がある重要な制限は次のとおりです。
>
> * Microsoft Graph API のユーザー レベルのアクセス許可 、つまり、電子メール、プロファイル、Offline_access OpenId のみをサポートします。 他の Microsoft Graph スコープ (またはなど) にアクセスする必要がある場合は、このドキュメントの最後にある推奨 `User.Read` `Mail.Read` される回避策を参照してください。 [](#apps-that-require-additional-microsoft-graph-scopes)
> * アプリケーションのドメイン名は、Azure アプリケーションに登録したドメイン名と同ADです。
> * 現在、アプリごとに複数のドメインはサポートされていません。
> * ドメインを使用するアプリケーションは、一般的すぎるため、セキュリティ 上のリスクが発生する可能性があるため `azurewebsites.net` 、サポートされていません。 ただし、この制限を積極的に削除する必要があります。

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a>Azure Active Directory ポータルを通じてアプリを詳細に登録する:

1. Azure Active Directory - アプリ登録ポータルに [新しいアプリケーションを登録](https://go.microsoft.com/fwlink/?linkid=2083908) します。
2. [ **新規登録] を** 選択し、[ *アプリケーションの登録] ページで*、次の値を設定します。
    * アプリ **名に** 名前を設定します。
    * サポートされている **アカウントの種類を選択** する (任意のアカウントの種類が機能します) ¹
    * **[リダイレクト URI]** を空のままにします。
    * **[登録]** を選択します。
3. [概要] ページで、アプリケーション **(クライアント) ID をコピーして保存します**。 Teams アプリケーション マニフェストを更新する場合は、後で必要になります。
4. [**管理**] で [**API の公開**] を選択します。 
5. [設定 **] リンクを** 選択して、 の形式でアプリケーション ID URI を生成します `api://{AppID}` 。 2 つのスラッシュと GUID の間に完全修飾ドメイン名 (末尾にスラッシュ "/" が付加された) を挿入します。 ID 全体の形式は `api://fully-qualified-domain-name.com/{AppID}` ² である必要があります。
    * ex: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` .
    
    完全修飾ドメイン名は、アプリが提供される人間が読み取り可能なドメイン名です。 ngrok などのトンネリング サービスを使用している場合は、ngrok サブドメインが変更されるたびにこの値を更新する必要があります。 
6. **[Scope の追加]** ボタンをクリックします。 開いたパネルで、**[スコープ名]** として `access_as_user` を入力します。
7. 同意 **できるユーザーを設定** する `Admins and users`
8. 管理者とユーザーの同意のプロンプトを構成するためのフィールドに、スコープに適した値を入力 `access_as_user` します。
    * **管理者の同意タイトル:** Teams は、ユーザーのプロファイルにアクセスできます。
    * **管理者の同意の説明**: Teams がアプリの Web API を現在のユーザーとして呼び出します。
    * **ユーザーの同意タイトル**: Teams はユーザー プロファイルにアクセスし、ユーザーの代わりに要求を行うことができます。
    * **ユーザーの同意の説明:** Teams がユーザーと同じ権限でこのアプリの API を呼び出すのを有効にする。
9. State が **[有効]** に設定 **されている**
10. [スコープの **追加] ボタンを** 選択して保存する 
    * テキスト フィールドの下に **表示されるスコープ** 名のドメイン 部分は、前の手順で設定した **アプリケーション ID** URI と自動的に一致し、末尾に追加 `/access_as_user` されます。
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. [承認済 **みクライアント アプリケーション** ] セクションで、アプリの Web アプリケーションに対して承認するアプリケーションを特定します。 [クライアント *アプリケーションの追加] を選択します*。 次の各クライアント ID を入力し、前の手順で作成した承認済みスコープを選択します。
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams モバイル/デスクトップ アプリケーション)
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams Web アプリケーション)
12. **[API のアクセス許可] に移動します**。 [Microsoft Graph *委任された* アクセス許可の追加] を選択し、Microsoft Graph API から次の  >    >  アクセス許可を追加します。
    * User.Read (既定で有効)
    * メール
    * offline_access
    * OpenId
    * profile

13. [認証] に **移動する**

    アプリに IT 管理者の同意が与えされていない場合、ユーザーはアプリを初めて使用する場合に同意する必要があります。

    リダイレクト URI を設定します。
    * [プラットフォーム **の追加] を選択します**。
    * **[Web] を選択します**。
    * アプリの **リダイレクト URI** を入力します。 これは、成功した暗黙的な付与フローがユーザーをリダイレクトするページです。 これは、手順 5 で入力した完全修飾ドメイン名と、認証応答を送信する API ルートと同じです。 Teams のサンプルに従う場合は、次のようになります。 `https://subdomain.example.com/auth-end`

    次に、次のボックスをチェックして暗黙的な付与を有効にします。  
    ✔ ID トークン  
    ✔ アクセス トークン  
    
おめでとうございます。 タブ SSO アプリを続行するためのアプリ登録の前提条件が完了しました。     

> [!NOTE]
>
> * ¹ Azure AD アプリが Teams で認証要求を行うのと同じテナントに登録されている場合、ユーザーは同意を求められなく、アクセス トークンがすぐ付与されます。 ユーザーがこれらのアクセス許可に同意する必要があるのは、Azure ADが別のテナントに登録されている場合のみです。
> * ² ドメインが既に所有され、所有者であることを示すエラーが表示される場合は、「クイック スタート: [カスタム](/azure/active-directory/fundamentals/add-custom-domain) ドメイン名を Azure Active Directory に追加してドメインを登録する」の手順に従い、上記の手順 5 を繰り返します。 (このエラーは、365 テナントの管理者資格情報でサインインしていないOffice発生する可能性があります)。
> * 返されるアクセス トークンで UPN (ユーザー プリンシパル名) を受信していない場合は、Azure AD[](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)でオプションのクレームとして追加できます。

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. Microsoft Teams アプリケーション マニフェストを更新する

Microsoft Teams マニフェストに新しいプロパティを追加します。

* **WebApplicationInfo** - 次の要素の親。

> [!div class="checklist"]
> * **id** - アプリケーションのクライアント ID。 これは、Azure アプリケーションへのアプリケーションの登録の一環として取得したアプリケーション ID AD。
>* **resource** - アプリケーションのドメインとサブドメイン。 これは、上記の手順 6 で作成するときに登録したのと同じ URI (プロトコルを含む `api://` ) `scope` です。 リソースにパスを `access_as_user` 含めてはいけない。 この URI のドメイン部分は、Teams アプリケーション マニフェストの URL で使用されるサブドメインを含むドメインと一致する必要があります。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* AAD アプリのリソースは、通常、サイト URL のルートと appID (たとえば) です `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。 また、この値を使用して、要求が同じドメインから送信されるのを確認します。 したがって、タブのリソース `contentURL` プロパティと同じドメインが使用されます。
>* フィールドを実装するには、マニフェスト バージョン 1.5 以上を使用する必要 `webApplicationInfo` があります。

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. クライアント側コードから認証トークンを取得する

認証 API の外観を次に示します。

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

(ユーザー レベルのアクセス許可に対して) 追加のユーザーの同意が必要な場合は、ユーザーに追加の同意を与えるダイアログがユーザーに `getAuthToken` 表示されます。 

成功コールバックでアクセス トークンを受信した後、アクセス トークンをデコードして、そのトークンに関連付けられているクレームを表示できます。 必要に応じて、アクセス トークンを手動でコピーしてツールに貼り付[](https://jwt.ms/)けます (コンテンツをjwt.msなど)。 返されるアクセス トークンでユーザー プリンシパル名 (UPN) を受け取らない場合は、Azure [](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) AD でオプションのクレームとして追加できます。

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>コード サンプル

|**サンプル名**|**説明**|**C#**|**TypeScript**|
|---------------|---------------|------|--------------|
| タブ SSO |Microsoft Teams のタブ用サンプル アプリ Azure AD SSO| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)、 </br>[Teams Toolkit](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>既知の制限事項

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a>追加の Microsoft Graph スコープが必要なアプリ

SSO の現在の実装では、他の API (User.Read や Mail.Read など) ではなく、ユーザー レベルのアクセス許可 (電子メール、プロファイル、offline_access、OpenId) に対する同意のみを付与します。 アプリでさらに Microsoft Graph スコープが必要な場合は、次の回避策を有効にしてください。

#### <a name="tenant-admin-consent"></a>テナント管理者の同意

最も簡単な方法は、組織の代わりにテナント管理者に事前同意を得る方法です。 つまり、ユーザーはこれらのスコープに同意する必要が生じ、Azure AD の代理フローを使用してトークン サーバー側を自由に交換 [できます](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。 この回避策は、社内の業務用アプリケーションでは受け入れ可能ですが、テナント管理者の承認に依存できない可能性があるサードパーティの開発者には十分ではない可能性があります。

組織に代わって (テナント管理者として) 同意する簡単な方法は、次のページにアクセスします。

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>Auth API を使用して追加の同意を求める

追加の Microsoft Graph スコープを取得するもう 1 つの方法は、Azure AD 同意ダイアログをポップアップする既存の Web ベースの [Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) 認証アプローチを使用して同意ダイアログを表示する方法です。 いくつかの注意が必要な追加があります。

1. これらの追加の Microsoft Graph API にアクセスするには、Azure AD の代理フローを使用してサーバー側で交換する必要があります `getAuthToken()` 。 [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
    * この交換には必ず v2 Microsoft Graph エンドポイントを使用してください
2. Exchange が失敗した場合、Azure AD無効な付与例外が返されます。 通常、次の 2 つのエラー メッセージの 1 `invalid_grant` つがあります。 `interaction_required`
3. 交換が失敗した場合は、追加の同意を求める必要があります。 ユーザーに追加の同意を求める UI を表示することをお勧めします。 この UI には、Azure 認証 API を使用して Azure AD同意ダイアログをトリガーするAD [含める必要があります](~/concepts/authentication/auth-silent-aad.md)。
4. Azure AD から追加の同意を求める場合は、クエリ文字列パラメーターを Azure AD に含める必要があります。それ以外の場合 `prompt=consent` 、Azure AD[](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)は追加のスコープを求めしません。
    * 代わりに： `?scope={scopes}`
    * これを使用します。 `?prompt=consent&scope={scopes}`
    * ユーザーに求 `{scopes}` めるすべてのスコープ (Mail.Read や User.Read など) が含まれる必要があります。
5. ユーザーが追加のアクセス許可を付与したら、これらの追加 API へのアクセスを取得するために、フローの代理を再試行します。

### <a name="non-azure-ad-authentication"></a>Azure 以外のAD認証

上記の認証ソリューションは、Azure サービスをサポートするアプリとサービスAD ID プロバイダーとしてのみ機能します。 Azure ベース以外のサービスを使用して認証ADするアプリは、ポップアップ ベースの Web 認証フローを引き続 [き使用する必要があります](~/concepts/authentication.md)。

> [!NOTE] 
> SSO は、Azure および B2C テナント内のADサポートされています。
