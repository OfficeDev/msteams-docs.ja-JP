---
title: タブのシングル サインオンのサポート
description: シングル サインオン (SSO) について説明します。
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams 認証 SSO AADシングル サインオン API
ms.openlocfilehash: 3e941e905f2c75825c502f67f49bb4cec5e601fa
ms.sourcegitcommit: 696b0f86cd32f20d4d4201e4c415e31f6c103a77
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2021
ms.locfileid: "61323290"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>タブのシングル サインオン (SSO) のサポート

ユーザーは、Office 365、Outlook である仕事、学校、または Microsoft アカウントを通じて Microsoft Teams にサインインし、デスクトップまたはモバイル クライアントでシングル サインオンを許可して Teams タブまたはタスク モジュールを承認できます。 ユーザーが一度サインインした場合、自動的にサインインしている別のデバイスでもう一度サインインする必要はありません。 また、アクセス トークンは、パフォーマンスと読み込み時間を改善するために指定されています。

> [!NOTE]
> **Teams SSO をサポートするモバイル クライアント バージョン**  
>
> ✔Teams (1416/1.0.0.2020073101 以降)
>
> ✔Teams iOS のバージョン (_バージョン_: 2.0.18 以降)  
> 
> ✔Teamsサイド _パネルで_ SSO が機能する JavaScript SDK (バージョン : 1.10 以降) を使用します。 
>
> 最新のバージョンの iOS Teams Android を使用して、アプリのエクスペリエンスを向上します。

> [!NOTE]
> **クイックスタート**  
>
> タブ SSO を使い始める最も簡単なパスは、TeamsツールキットVisual Studio Code。 詳細については、「SSO with [Teamsツールキット」および「Visual Studio Code」を参照してください。](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>実行時の SSO の動作のしくみ

次の図は、SSO プロセスの動作を示しています。

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. タブでは、JavaScript 呼び出しが `getAuthToken()`に対してなされます。 `getAuthToken()`タブ Teamsアクセス トークンを取得する必要があります。
2. 現在のユーザーが初めてタブ アプリケーションを使用している場合、同意が必要な場合は、同意を求める要求プロンプトが表示されます。 または、2 要素認証などのステップアップ認証を処理する要求プロンプトがあります。
3. Teamsユーザーの Azure Active Directory (AAD) エンドポイントからタブ アクセス トークンを要求します。
4. AADアプリケーションにタブ アクセス トークンをTeamsします。
5. Teamsによって返される結果オブジェクトの一部としてタブ アクセス トークンをタブに送信 `getAuthToken()` します。
6. トークンは JavaScript を使用してタブ アプリケーションで解析され、ユーザーのメール アドレスなどの必要な情報を抽出します。

> [!NOTE]
> これは、電子メール、プロファイル、offline_access、および OpenId であるユーザー レベル API `getAuthToken()` の制限されたセットに同意する場合にのみ有効です。 または など、他のスコープGraphには使用 `User.Read` されません `Mail.Read` 。 推奨される回避策については、「アクセス トークンを[取得する」を](#get-an-access-token-with-graph-permissions)参照Graphしてください。

SSO API は、Web コンテンツを [埋め込むタスク](../../../task-modules-and-cards/what-are-task-modules.md) モジュールでも機能します。

## <a name="develop-an-sso-microsoft-teams-tab"></a>[SSO] タブMicrosoft Teamsする

このセクションでは、SSO を使用する [Teams] タブの作成に関連するタスクについて説明します。 これらのタスクは言語とフレームワークに依存しないタスクです。

### <a name="1-create-your-aad-application"></a>1. アプリケーションをAADする

> [!NOTE]
> 以下の重要な制限を知る必要があります。
>
> * API のアクセス許可Graphユーザー レベルのアクセス許可 (電子メール、プロファイル、offline_access OpenId) だけがサポートされます。 その他のスコープ (Graphなど) にアクセスする必要がある場合は、「アクセス トークンを取得する」を参照Graph `User.Read` `Mail.Read` [してください](#get-an-access-token-with-graph-permissions)。
> * アプリケーションのドメイン名は、アプリケーションに登録したドメイン名と同AADです。
> * 現在、アプリごとに複数のドメインはサポートされていません。
> * ユーザーは、新しい `accessTokenAcceptedVersion` アプリケーション `2` に対して設定する必要があります。

**アプリをポータルから登録するにはAADする**

1. 新しいアプリケーションをアプリ登録[ポータルAAD登録](https://go.microsoft.com/fwlink/?linkid=2083908)します。
1. [新規 **登録] を選択します**。 [ **アプリケーションの登録] ページ** が表示されます。
1. [アプリケーションの **登録] ページで** 、次の値を入力します。
    1. アプリの **[名前]** を入力します。
    2. [サポートされている **アカウントの種類] を選択し、[** 単一テナント] または [マルチテナント アカウントの種類] を選択します。 ¹
    * **[リダイレクト URI]** を空のままにします。
    3. **[登録]** を選択します。
1. [概要] ページで、アプリケーション **(クライアント) ID をコピーして保存します**。 アプリケーション マニフェストを更新する際には、後でTeams必要があります。
1. [**管理**] で [**API の公開**] を選択します。

    > [!NOTE]
    > ボットとタブを使用してアプリを作成する場合は、アプリケーション ID URI を次のように入力します `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。

1. [設定 **] リンクを** 選択して、 の形式でアプリケーション ID URI を生成します `api://{AppID}` 。 2 つのスラッシュと GUID の間に、末尾にスラッシュ "/" が付加された完全修飾ドメイン名を挿入します。 ID 全体に . の形式が必要です `api://fully-qualified-domain-name.com/{AppID}` 。 ² たとえば `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 、 . 完全修飾ドメイン名は、アプリが提供される人間が読み取り可能なドメイン名です。 ngrok などのトンネリング サービスを使用している場合は、ngrok サブドメインが変更されるたびにこの値を更新する必要があります。
1. **[スコープの追加]** を選択します。 開くパネルで、[スコープ名] **access_as_user** を **入力します**。
1. [同意 **できるWho] ボックスに、「****管理者とユーザー」と入力します**。
1. スコープに適した値を使用して管理者とユーザーの同意のプロンプトを構成するための詳細をボックスに入力 `access_as_user` します。
    * **管理者の同意タイトル:** チームはユーザーのプロフィールにアクセスできます。
    * **管理者の同意の** 説明: Teamsアプリの Web API を現在のユーザーとして呼び出す場合があります。
    * **ユーザーの同意タイトル**: Teamsにアクセスして、ユーザーに代わって要求を行うことができます。
    * **ユーザーの同意の説明: Teams** と同じ権限でこのアプリの API を呼び出す場合があります。
1. **[状態]** が **[有効]** に設定されていることを確認してください。
1. [スコープ **の追加] を** 選択して詳細を保存します。 テキスト フィールドの下に表示 **されるスコープ** 名のドメイン 部分は、前の手順で設定した **アプリケーション ID** URI と自動的に一致し、末尾に追加 `/access_as_user` する必要があります `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user` 。
1. [承認済 **みクライアント アプリケーション** ] セクションで、アプリの Web アプリケーションに対して承認するアプリケーションを特定します。 [クライアント **アプリケーションの追加] を選択します**。 次の各クライアント ID を入力し、前の手順で作成した承認済みスコープを選択します。
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`モバイルTeamsデスクトップ アプリケーションの場合。
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`web アプリケーションTeamsの場合。
1. **[API のアクセス許可] に移動します**。 [**アクセス許可を**  >  **追加する] Graph** 委任されたアクセス許可を選択し、次のアクセス許可を API から  >  Graphします。
    * User.Read は既定で有効になっています
    * メール
    * offline_access
    * OpenId
    * profile

1. [認証] **に移動します**。

    > [!IMPORTANT]
    > アプリに IT 管理者の同意が与えされていない場合、ユーザーはアプリを初めて使用する場合に同意する必要があります。

    リダイレクト URI を入力するには、次のコマンドを使用します。
    * [プラットフォーム **の追加] を選択します**。
    * **[Web] を選択します**。
    * アプリの **リダイレクト URI** を入力します。 この URI は、手順 5 で入力したのと同じ完全修飾ドメイン名です。 また、認証応答が送信される API ルートも続きます。 次のサンプルを実行している場合Teams URI はです `https://subdomain.example.com/auth-end` 。 詳細については [、「OAuth 2.0 承認コード フロー」を参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

    > [!NOTE]
    > タブ SSO には暗黙的な付与は必要ありません。

おめでとうございます。 タブ SSO アプリを続行するには、アプリ登録の前提条件が完了しました。

> [!NOTE]
>
> * ¹ AAD アプリが Teams で認証要求を行うのと同じテナントに登録されている場合、ユーザーは同意を求めれなく、アクセス トークンがすぐ付与されます。 ユーザーは、アプリが別のテナントにAAD場合にのみ、これらのアクセス許可に同意します。
> * ² カスタム ドメインが AAD に追加されていない場合は、ホスト名が既に所有されているドメインに基づいていなければならないというエラーが表示されます。 カスタム ドメインを AADして登録するには、カスタム ドメイン名を[](/azure/active-directory/fundamentals/add-custom-domain)追加して AAD手順に従い、手順 5 を繰り返します。 このエラーは、テナントの管理者資格情報でサインインしていない場合Office 365できます。
> * 返されるアクセス トークンでユーザー プリンシパル名 (UPN) を受け取らない場合は、そのユーザー[](/azure/active-directory/develop/active-directory-optional-claims)プリンシパル名をオプションのクレームとして追加AAD。

### <a name="2-update-your-teams-application-manifest"></a>2. アプリケーション マニフェストTeams更新する

次のコードを使用して、新しいプロパティをマニフェストにTeamsします。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** は、次の要素の親です。

> [!div class="checklist"]
> * **id** - アプリケーションのクライアント ID。 これは、アプリケーションをアプリケーションに登録する一部として取得したアプリケーション ID Azure AD。
>* **resource** - アプリケーションのドメインとサブドメイン。 これは、手順 6 で作成するときに登録したのと同じ URI (プロトコルを含む `api://` ) `scope` です。 リソースにパスを `access_as_user` 含めなけれ。 この URI のドメイン部分は、アプリケーション マニフェストの URL で使用されるサブドメインを含むドメインTeams必要があります。

> [!NOTE]
>
>* アプリのリソースはAADサイト URL のルートであり、appID (など) です `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。 この値は、要求が同じドメインから送信されるのを確認するためにも使用されます。 タブの `contentURL` リソース プロパティと同じドメインが使用されます。
>* フィールドを実装するには、マニフェスト バージョン 1.5 以上を使用する必要 `webApplicationInfo` があります。

### <a name="3-get-an-access-token-from-your-client-side-code"></a>3. クライアント側コードからアクセス トークンを取得する

次の認証 API を使用します。

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

ユーザー レベルのアクセス許可を呼び出し、ユーザーの同意が必要な場合は、同意を許可する `getAuthToken` ダイアログがユーザーに表示されます。

成功コールバックでアクセス トークンを受信した後、アクセス トークンをデコードして、そのトークンのクレームを表示します。 必要に応じて、アクセス トークンを手動でコピーしてツールに貼り付[jwt.ms。](https://jwt.ms/) 返されるアクセス トークンで UPN を受け取らない場合は、その UPN をオプションのクレームとして追加AAD。 [](/azure/active-directory/develop/active-directory-optional-claims) 詳細については、「アクセス トークン [」を参照してください](/azure/active-directory/develop/access-tokens)。

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>コード サンプル

|**サンプルの名前**|**説明**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| タブ SSO |Microsoft Teams SSO のタブのサンプル Azure ADアプリ| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)、 </br>[Teams Toolkit](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>既知の制限

### <a name="get-an-access-token-with-graph-permissions"></a>アクセス許可を使用してアクセス トークンGraphする

SSO の現在の実装では、ユーザー レベルのアクセス許可に対する同意のみを付与します。このアクセス許可は、ユーザーの呼び出しGraphできません。 Graph 呼び出しに必要なアクセス許可 (スコープ) を取得するには、SSO ソリューションがカスタム Web サービスを実装して、Teams JavaScript SDK から取得したトークンを必要なスコープを含むトークンと交換する必要があります。 これは、AADの代理フロー[を使用して実行されます](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。

#### <a name="tenant-admin-consent"></a>テナント管理者の同意

テナント管理者として組織に代わって同意する簡単な方法は、 を参照する方法です `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>` 。

#### <a name="ask-for-consent-using-the-auth-api"></a>Auth API を使用して同意を求める

スコープを使用Graphもう 1 つの方法は、既存の Web ベースの認証方法を使用して同意ダイアログ[をAzure ADです](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page)。 この方法では、同意ダイアログ ボックスAzure AD表示されます。

**Auth API を使用して追加の同意を求めるには**

1. 他の API へのアクセスを取得するには、フロー AADを使用して取得したトークンをサーバー側 `getAuthToken()` Graph必要があります。 [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) この交換に v2 Graphエンドポイントを使用してください。
2. Exchange が失敗した場合、AAD無効な付与例外が返されます。 通常、2 つのエラー メッセージの 1 つ、 `invalid_grant` または `interaction_required` .
3. 交換が失敗した場合は、同意を求める必要があります。 ユーザーに他の同意を許可するユーザー インターフェイス (UI) を表示します。 この UI には、認証 API を使用してAAD同意ダイアログ ボックスをトリガーする[ボタンAAD必要があります](~/concepts/authentication/auth-silent-aad.md)。
4. AAD からより多くの同意を求める場合は、AAD にクエリ文字列パラメーターを含める必要があります。それ以外の場合、AAD は他のスコープを求めずに行います `prompt=consent` 。 [](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)
    * 代わりに `?scope={scopes}`
    * これを使用する `?prompt=consent&scope={scopes}`
    * メール.Read や User.Read など、ユーザーに求めるすべてのスコープ `{scopes}` が含まれるか確認します。
5. ユーザーにより多くのアクセス許可が付与された後、これらの他の API へのアクセスを取得するために、フローの代理を再試行します。

### <a name="non-aad-authentication"></a>非認証AAD認証

上記の認証ソリューションは、ID プロバイダーとして認証をサポートするアプリAADにのみ機能します。 非ユーザー ベースのサービスを使用して認証AADするアプリは、ポップアップ ベースの Web 認証フローを引き続[き使用する必要があります](~/concepts/authentication.md)。

> [!NOTE]
> SSO は、B2C テナント内の顧客所有AADサポートされます。
