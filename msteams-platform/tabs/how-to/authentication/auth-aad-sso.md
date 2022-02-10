---
title: タブのシングル サインオンのサポート
description: シングル サインオン (SSO) について説明します
ms.topic: how-to
ms.localizationpriority: high
keywords: teams authentication SSO Microsoft Azure Active Directory (Azure AD) single sign-on api
ms.openlocfilehash: 24b9465e8400660fb0f271d20e3922679c43663e
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518101"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>タブのシングル サインオン (SSO) のサポート

ユーザーは職場、学校から Microsoft Teams にサインインしているか、Office 365、Outlook の Microsoft アカウントにサインインしているので、それを利用してシングル サインオンを許可すると、Teams タブまたはタスク モジュールを承認することができるようになります。 一度サインインすれば、サインインが自動的に行われるので、別のデバイスでもう一度サインインする必要はありません。 また、アクセス トークンは、パフォーマンスと読み込み時間を改善するために指定されています。

> [!NOTE]
> **SSO をサポートする Teams モバイル クライアントのバージョン**  
>
> ✔Teams for Android (1416/1.0.0.2020073101 以降)
>
> ✔Teams for iOS (_バージョン_: 2.0.18 以降)  
> 
> ✔Teams JavaScript SDK (_バージョン_: 1.10 以降)。SSO が会議のサイド パネルで機能するようになります。 
>
> Teams を最適なパフォーマンスでご利用いただくために、最新バージョンの iOS および Android を使用してください。

> [!NOTE]
> **クイックスタート**  
>
> タブ SSO を使い始める最も簡単なパスは、Microsoft Visual Studio Code 用 Teams ツールキット内にあります。 詳細については、「[Teams ツールキットやタブ用 Visual Studio Code を使用したシングル サインオン](../../../toolkit/visual-studio-code-tab-sso.md)」をご覧ください。

## <a name="how-sso-works-at-runtime"></a>実行時の SSO の動作のしくみ

次の画像は、SSO プロセスの動作のしくみを示しています。

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. タブでは、JavaScript 呼び出しが `getAuthToken()`に対してなされます。 `getAuthToken()` は Teams にタブ アプリケーションのアクセス トークンを取得するように指示します。
2. 現在のユーザーが初めてタブ アプリケーションを使用していて、同意が必要になる場合は、同意を要求する要求プロンプトが表示されます。 または、2 要素認証などのステップアップ認証を要求する要求プロンプトが表示されます。
3. Teams は、現在のユーザーのMicrosoft Azure Active Directory (Microsoft Azure Active Directory (Azure AD)) エンドポイントからタブ アクセス トークンを要求します。
4. Microsoft Azure Active Directory (Microsoft Azure Active Directory (Azure AD)) は、Teams アプリケーションにタブ アクセス トークンを送信します。
5. `getAuthToken()` の呼び出しによって返される結果オブジェクトの一部として、Teams ではタブにタブ アクセス トークン を送信します。
6. トークンは JavaScript を使用してタブ アプリケーションで解析され、ユーザーのメール アドレスなどの必要な情報を抽出します。

> [!NOTE]
> `getAuthToken()` は、メール、プロファイル、offline_access、OpenId など、ユーザー レベルの API の限定された組み合わせに同意する場合にのみ有効です。 `User.Read` や `Mail.Read` など、それ以上の Graph スコープには使用されません。 推奨される回避策については、「[Graph のアクセス許可を持つアクセス トークンを取得する](#get-an-access-token-with-graph-permissions)」をご覧ください。

SSO API は、Web コンテンツを埋め込む [タスク モジュール](../../../task-modules-and-cards/what-are-task-modules.md) でも機能します。

## <a name="develop-an-sso-microsoft-teams-tab"></a>SSO Microsoft Teams のタブを開発する

このセクションでは、SSO を使用する Teams のタブの作成に関連するタスクについて説明します。 これらのタスクは、言語とフレームワークに依存していません。

### <a name="1-create-your-microsoft-azure-active-directory-azure-ad-application"></a>1. Microsoft Azure Active Directory (Azure AD) アプリケーションを作成する

> [!NOTE]
> 知っておかなければならない重要な制限事項がいくつかあります。
>
> * メール、プロファイル、offline_access、OpenId など、ユーザー レベルの Graph API のアクセス許可のみがサポートされます。 `User.Read` や `Mail.Read` などの他の Graph スコープにアクセスしなければならない場合は、「[Graph のアクセス許可を持つアクセス トークンを取得する](#get-an-access-token-with-graph-permissions)」を参照してください。
> * アプリケーションのドメイン名が Microsoft Azure Active Directory (Azure AD) アプリケーションに登録した時のドメイン名と同じであることが重要です。
> * 現在、アプリごとの複数のドメインはサポートされていません。
> * ユーザーは、`accessTokenAcceptedVersion` を新しいアプリケーションの `2` に設定する必要があります。

**Microsoft Azure Active Directory (Azure AD) ポータルからアプリを登録するには**

1. 新しいアプリケーションを [Microsoft Azure Active Directory (Azure AD) アプリ登録](https://go.microsoft.com/fwlink/?linkid=2083908) ポータルに登録します。
1. **[新規登録]** を選択します。 **[アプリケーション登録]** ページが表示されます。
1. **[アプリケーション登録]** ページで、次の値を入力します。
    1. アプリの **[名前]** を入力します。
    2. **[サポートされているアカウントの種類]** を選択し、[単一テナント] または [マルチテナント アカウントの種類] を選択します。 ¹
    * **[リダイレクト URI]** を空のままにします。
    3. **[登録]** を選択します。
1. 概要ページで、**[アプリケーション (クライアント) ID]** をコピーして保存します。 後で Teams アプリケーション マニフェストを更新する際に必要になります。
1. [**管理**] で [**API の公開**] を選択します。

    > [!NOTE]
    > ボットとタブを使用してアプリをビルドしている場合は、アプリケーション ID URI と `api://fully-qualified-domain-name.com/botid-{YourBotId}` に入力します。

1. **[設定]** リンクを選択して、`api://{AppID}` の形式でアプリケーション ID URIを生成します。 ダブル スラッシュと GUID の間に完全修飾ドメイン名 (末尾にスラッシュ "/" を付けて) を挿入します。 ID 全体の形式は `api://fully-qualified-domain-name.com/{AppID}` である必要があります。 ² たとえば、`api://subdomain.example.com/00000000-0000-0000-0000-000000000000`。 完全修飾ドメイン名は、アプリを提供する人間が判読できるドメイン名です。 ngrok などのトンネリング サービスを使用している場合は、ngrok サブドメインが変更される度にこの値を更新する必要があります。
1. **[スコープの追加]** を選択します。 開いたパネルで、**access_as_user** と **スコープ名** に入力します。
1. **[同意できるユーザー]** ボックスに、**管理者とユーザー** と入力します。
1. 管理者とユーザーの同意プロンプトを構成するためのボックスに、`access_as_user` スコープに適した値を使用して詳細を入力します。
    * **管理者の同意タイトル:** チームはユーザーのプロフィールにアクセスできます。
    * **管理者の同意説明:** チームは、現在のユーザーとしてアプリの Web API を呼び出すことができます。
    * **ユーザーの同意タイトル**: チームは、ユーザーのプロフィールにアクセスしてユーザーに代わって要求を行うことができます。
    * **ユーザーの同意の説明:** チームは、ユーザーと同じ権限でこのアプリの API を呼び出すことができます。
1. **[状態]** が **[有効]** に設定されていることを確認してください。
1. **[スコープの追加]** を選択して、詳細を保存します。 テキスト フィールドの下に表示される **[スコープ名]** のドメイン部分は、前の手順で設定された **[アプリケーション ID URI]** と自動的に一致し、最後に `/access_as_user` が追加されます`api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`。
1. **[承認済みのクライアント アプリケーション]** セクションで、アプリの Web アプリケーションに対して承認するアプリケーションを特定します。 **[クライアント アプリケーションの追加]** を選択します。 次の各クライアント ID を入力し、前の手順で作成した承認スコープを選択します。
    * Teams モバイル アプリケーションまたはデスクトップ アプリケーション用 `1fec8e78-bce4-4aaf-ab1b-5451cc387264`。
    * Teams Web アプリケーション用 `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`。
1. **[API アクセス許可]** に移動します。 **[アクセス許可の追加]** > **[Microsoft Graph]** > **[委任されたアクセス許可]** の順に選択してから、Graph API で以下のアクセス許可を追加します。
    * User.Read が既定で有効になっています
    * メール
    * offline_access
    * OpenId
    * profile

1. **[認証]** に移動します。

    > [!IMPORTANT]
    > アプリに IT 管理者の同意が付与されていない場合、ユーザーはアプリを初めて使用する際に同意する必要があります。

    リダイレクト URI を入力するには:
    * **[プラットフォームの追加]** を選択します。
    * **[Web]** を選びます。
    * アプリの **[リダイレクト URI]** を入力します。 この URI は、手順 5 で入力したのと同じ完全修飾ドメイン名です。 認証応答が送信される場合には API ルートも続きます。 Teams のサンプルのいずれかをフォローしている場合、URI は `https://subdomain.example.com/auth-end` です。 詳細については、「[OAuth 2.0 承認コード フロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow)」を参照してください。

    > [!NOTE]
    > タブ SSO には暗黙的な付与は必要ありません。

おめでとうございます! 登録の前提条件を完了し、タブ SSO アプリを続行できるようになりました。

> [!NOTE]
>
> * ¹ Microsoft Azure Active Directory (Azure AD) アプリが Teams で認証要求を行うのと同じテナントに登録されている場合には、ユーザーが同意を求められることはなく、アクセス トークンがすぐに付与されます。 ユーザーは、Microsoft Azure Active Directory (Azure AD) アプリが別のテナントに登録されている場合にのみ、これらのアクセス許可に同意します。
> * ² カスタム ドメインが Microsoft Azure Active Directory (Azure AD) に追加されていない場合は、ホスト名が既に所有されているドメインに基づいていなければならないというエラーが表示されます。 カスタム ドメインを Microsoft Azure Active Directory (Azure AD) に追加して登録するには、「[カスタム ドメイン名を Microsoft Azure Active Directory (Azure AD) に追加する](/azure/active-directory/fundamentals/add-custom-domain)」手順に従い、手順 5 を繰り返します。 Office 365 テナンシーで管理者資格情報を使用してサインインしていない場合にも、このエラーが表示されることがあります。
> * Azure AD では、返されたアクセス トークンでユーザー プリンシパル名 (UPN) を受け取っていない場合は、それを Microsoft Azure Active Directory (Azure AD) で [[オプションの要求](/azure/active-directory/develop/active-directory-optional-claims)] に追加することができます。

### <a name="2-update-your-teams-application-manifest"></a>2. Teams アプリケーション マニフェストを更新する

次のコードを使用して、Teams マニフェストに新しいプロパティを追加します。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** は、次の要素の親です。

> [!div class="checklist"]
> * **id** - アプリケーションのクライアント ID。 これは、アプリケーションを Microsoft Azure Active Directory (Azure AD) に登録する際に取得したアプリケーション ID です。
>* **resource** - アプリケーションのドメインとサブドメイン。 これは、手順 6 で `scope` を作成するときに登録したのと同じ URI (`api://` プロトコルを含む) です。 リソースに `access_as_user` パスを含めることはできません。 この URI のドメイン部分は、Teams アプリケーション マニフェストの URL で使用されている任意のサブドメインを含むドメインと一致している必要があります。

> [!NOTE]
>
>* Microsoft Azure Active Directory (Azure AD) アプリのリソースは、通常、そのサイト URL と appID のルートです (例: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`)。 この値は、ユーザーの要求が同じドメインから送信されているのを確認するのにも使用されます。 タブの `contentURL` でリソース プロパティと同じドメインが使用されていることを確認します。
>* `webApplicationInfo` フィールドを実装するには、マニフェスト バージョン 1.5 以上を使用する必要があります。

### <a name="3-get-an-access-token-from-your-client-side-code"></a>3. クライアント側コードからアクセス トークンを取得する

次の認証 API を使用します。

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

`getAuthToken` を呼び出し、ユーザー レベルのアクセス許可にユーザーの同意が必要な場合は、同意を付与するためのダイアログがユーザーに表示されます。

成功コールバックでアクセス トークンを受信した後、アクセス トークンをデコードして、そのトークンのクレームを表示します。 必要に応じて、[jwt.ms](https://jwt.ms/) など、手動でツールにアクセス トークンをコピーして貼り付けます。 返されたアクセス トークンで UPN を受け取っていない場合は、Microsoft Azure Active Directory (Azure AD) で [[オプションの要求](/azure/active-directory/develop/active-directory-optional-claims)] として追加します。 詳細については、「[アクセス トークン](/azure/active-directory/develop/access-tokens)」を参照してください。

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-snippets"></a>コード スニペット

次のコードは、MSAL ライブラリを使用してアクセス トークンを取得するための on-behalf-of flow の例を示しています。

### <a name="c"></a>[C#](#tab/dotnet)

```csharp

IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(<"Client id">)
                                                .WithClientSecret(<"Client secret">)
                                                .WithAuthority($"https://login.microsoftonline.com/<"Tenant id">")
                                                .Build();
 
            try
            {
                var idToken = <"Client side token">;
                UserAssertion assert = new UserAssertion(idToken);
                List<string> scopes = new List<string>();
                scopes.Add("https://graph.microsoft.com/User.Read");
                var responseToken = await app.AcquireTokenOnBehalfOf(scopes, assert).ExecuteAsync();
                return responseToken.AccessToken.ToString();
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
        }
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Exchange cliend side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenand id" >
    var token = < "Client side token" >
    var scopes = ["https://graph.microsoft.com/User.Read"];

        // Creating MSAL client
        const msalClient = new msal.ConfidentialClientApplication({
            auth: {
                clientId: < "Client ID" >,
                clientSecret: < "Client Secret" >
      }
        });

        var oboPromise = new Promise((resolve, reject) => {
            msalClient.acquireTokenOnBehalfOf({
                authority: `https://login.microsoftonline.com/${tid}`,
                oboAssertion: token,
                scopes: scopes,
                skipCache: true
            }).then(result => {
                console.log("Token is: " + result.accessToken);
            }).catch(error => {
                reject({ "error": error.errorCode });
            });
        });
```
---

## <a name="code-sample"></a>コード サンプル

|**サンプルの名前**|**説明**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| タブ SSO |タブ Microsoft Azure Active Directory (Azure AD) SSO 用 Microsoft Teams サンプル アプリ| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)、 </br>[Teams ツールキット](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>既知の制限

### <a name="get-an-access-token-with-graph-permissions"></a>Graph のアクセス許可を持つアクセス トークンを取得する

SSO の現在の実装では、ユーザー レベルのアクセス許可に対する同意のみを付与します。このアクセス許可は、Graph の呼び出しには使用できません。 Graph の呼び出しに必要なアクセス許可 (スコープ) を取得するには、SSO ソリューションでカスタム Web サービスを実装して、Teams JavaScript SDK から受け取ったトークンを必要なスコープを含むトークンと交換する必要があります。 これは、Microsoft Azure Active Directory (Azure AD) の[代理フロー](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)を使用して行われます。

### <a name="tenant-admin-consent"></a>テナント管理者の同意

テナント管理者として組織に代わって同意する簡単な方法は、`https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>` を参照することです。

#### <a name="ask-for-consent-using-the-auth-api"></a>認証 API を使用して同意を求める

Graph のスコープを取得するもう 1 つの方法は、既存の [Web ベースの Microsoft Azure Active Directory (Azure AD) 認証方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page) を使用して同意ダイアログを表示する方法です。 この方法では、Microsoft Azure Active Directory (Azure AD) 同意ダイアログ ボックスをポップアップ表示します。

**認証 API を使用してその他の同意を求めるには**

1. `getAuthToken()` を使用して取得したトークンは、他の Graph API にアクセスするのに Microsoft Azure Active Directory (Azure AD) [代理フロー](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)を使用してサーバー側で交換しなければなりません。 この交換には v2 Graph エンドポイントを使用するようにしてください。
2. 交換が失敗した場合、Microsoft Azure Active Directory (Azure AD) は無効な許可例外を返します。 通常、2 つのエラー メッセージ (`invalid_grant` または `interaction_required`) のいずれかです。
3. 交換が失敗すると、同意を求める必要があります。 ユーザーに他の同意を求めるユーザー インターフェイス (UI) をいくつか表示します。 この UI には、[Microsoft Azure Active Directory (Azure AD) 認証 API](~/concepts/authentication/auth-silent-aad.md) を使用してMicrosoft Azure Active Directory (Azure AD) 同意ダイアログ ボックスをトリガーするボタンが含まれているはずです。
4. Microsoft Azure Active Directory (Azure AD) にさらなる同意を求める場合は、Microsoft Azure Active Directory (Azure AD) に対するお客様の [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) に `prompt=consent` を含める必要があります。そうされない場合、Microsoft Azure Active Directory (Azure AD) から他のスコープは要求されません。
    * `?scope={scopes}` の代わりに
    * この `?prompt=consent&scope={scopes}` を使用する
    * `{scopes}` に Mail.Read や User.Read など、ユーザーに求めるすべてのスコープが含まれていることを確認します。
5. ユーザーにその他のアクセス許可が付与されたら、代理のフローのを再試行して、これらの他の API へのアクセスを取得します。

### <a name="non-microsoft-azure-active-directory-azure-ad-authentication"></a>Microsoft Azure Active Directory (Azure AD) 以外の認証

上記の認証ソリューションは、ID プロバイダーとして Microsoft Azure Active Directory (Azure AD) をサポートするアプリとサービスに対してのみ機能します。 Microsoft Azure Active Directory (Azure AD) ベースのサービス以外を使用して認証するアプリでは、引き続きポップアップ ベースの [Web 認証フロー](~/concepts/authentication.md)を使用する必要があります。

> [!NOTE]
> SSO は、Microsoft Azure Active Directory (Azure AD) B2C テナント内の顧客所有のアプリでサポートされています。

## <a name="step-by-step-guides"></a>ステップ バイ ステップのガイド

* [ステップ バイ ステップのガイド](../../../sbs-tabs-and-messaging-extensions-with-sso.yml) に従って、タブとメッセージング拡張機能を認証します。
* [ステップ バイ ステップのガイド](../../../sbs-tab-with-adaptive-cards.yml) に従って、アダプティブ カード付きタブを作成します。

## <a name="see-also"></a>関連項目
[シングル サインオンと Teams ボット](../../../sbs-bots-with-sso.yml)
