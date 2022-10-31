---
title: Microsoft Graph のアクセス許可を使用してタブ アプリを拡張する
description: シングル サインオン (SSO) を有効にするために、Microsoft Graph で追加のアクセス許可とスコープを構成します。
ms.topic: how-to
ms.localizationpriority: high
keywords: Teams 認証タブ Microsoft Azure Active Directory (Azure AD) Graph API 委任されたアクセス許可アクセス トークン スコープ
ms.openlocfilehash: 11620e10ed736ce9fe88e3bb755acfbabfec3f47
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791721"
---
# <a name="extend-tab-app-with-microsoft-graph-permissions-and-scope"></a>Microsoft Graph のアクセス許可とスコープを使用してタブ アプリを拡張する

Microsoft Graph を使用してタブ アプリを拡張し、ユーザーに追加のアクセス許可 (アプリ ユーザー プロファイルの表示、メールの読み取りなど) を許可できます。 アプリは、アプリ ユーザーの同意に基づいてアクセス トークンを取得するために、特定のアクセス許可スコープを依頼する必要があります。

Graph スコープでは、`User.Read` や `Mail.Read` など、アプリが Teams ユーザーのアカウントにアクセスする方法を指定できます。 承認要求でスコープを指定する必要があります。

このセクションでは、次に示す操作について説明します。

- [Azure AD における API アクセス許可の構成](#configure-api-permissions-in-azure-ad)
- [さまざまなプラットフォームの認証の構成](#configure-authentication-for-different-platforms)
- [MS Graph 向けアクセス トークンの取得](#acquire-access-token-for-ms-graph)

## <a name="configure-api-permissions-in-azure-ad"></a>Azure AD における API アクセス許可の構成

アプリ向け Azure AD で追加の Graph スコープを構成できます。 これらは委任されたアクセス許可であり、サインイン アクセスを必要とするアプリによって使用されます。 サインインしているアプリ ユーザーまたは管理者は、それらに同意する必要があります。 Microsoft Graph を呼び出すときに、サインインしているユーザーに代わってタブ アプリで同意できます。

### <a name="to-configure-api-permissions"></a>API のアクセス許可を構成するには

1. [Azure portal](https://ms.portal.azure.com/) で登録したアプリを開きます。

2. 左側のウィンドウで **[管理]** > **[API のアクセス許可]** の順に選択します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/api-permission-menu.png" alt-text="[アプリのアクセス許可] メニュー オプション。":::

    **[API のアクセス許可]** ページが表示されます。

3. **[アクセス許可を追加する]** を選択して、Microsoft Graph API アクセス許可を追加します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-permission.png" alt-text="[アプリのアクセス許可] ページ。":::

    **[要求 API のアクセス許可]** ページが表示されます。

4. **[Microsoft Graph]** を選択します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/request-api-permission.png" alt-text="[API アクセス許可の要求] ページ。":::

    Graph アクセス許可のオプションが表示されます。

5. **[委任されたアクセス許可]** を選択して、アクセス許可の一覧を表示します。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/delegated-permission.png" alt-text="委任されたアクセス許可。":::

6. アプリに関連するアクセス許可を選択し、**[アクセス許可を追加する]** を選択します。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-permission.png" alt-text="[アクセス許可] を選択します。":::

    検索ボックスにアクセス許可名を入力して検索することもできます。

    アクセス許可が更新されたことを示すメッセージがブラウザーに表示されます。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/updated-permission-msg.png" alt-text="アクセス許可更新済みのメッセージ。":::

    追加されたアクセス許可は、**[API アクセス許可]** ページに表示されます。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configured-permissions.png" alt-text="API のアクセス許可が構成されます。":::

    Microsoft Graph のアクセス許可を使用してアプリを構成しました。

## <a name="configure-authentication-for-different-platforms"></a>さまざまなプラットフォーム向け認証を構成する

アプリをターゲットにするプラットフォームまたはデバイスによっては、リダイレクト URI、特定の認証設定、プラットフォーム固有の詳細など、追加の構成が必要になる場合があります。

> [!NOTE]
>
> - タブ アプリに IT 管理者の同意が付与されていない場合、アプリ ユーザーは異なるプラットフォームでアプリを初めて使用する際に同意する必要があります。
> - タブ アプリで SSO が有効になっている場合、暗黙的な許可は必須ではありません。

URL が一意である限り、複数のプラットフォームの認証を構成することができます。

### <a name="to-configure-authentication-for-a-platform"></a>プラットフォームの認証を構成するには

1. [Azure portal](https://ms.portal.azure.com/) で登録したアプリを開きます。

1. 左側のウィンドウで、**[管理]** > **[認証]** の順に選択します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-platform.png" alt-text="プラットフォームの認証":::

    **[プラットフォームの構成]** ページが表示されます。

1. **[プラットフォームの追加]** を選択します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-platform.png" alt-text="プラットフォームの追加":::

    **[プラットフォームの構成]** ページが表示されます。

1. タブ アプリ用に構成するプラットフォームを選択します。 プラットフォームの種類は、Web または SPA から選択できます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configure-platform.png" alt-text="Web プラットフォームを選択する":::

    特定のプラットフォームの種類に対して複数のプラットフォームを構成できます。 リダイレクト URI が、構成するすべてのプラットフォームで一意であることを確認します。

    構成 Web ページが表示されます。

    > [!NOTE]
    > 構成は、選択したプラットフォームによって異なります。

1. プラットフォームの構成の詳細を入力します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-web-platform.png" alt-text="Web プラットフォームを構成する":::

    1. リダイレクト URI を入力します。 URI は一意である必要があります。
    2. フロント チャネルのログアウト URL を入力します。
    3. アプリに対して Azure AD に送信するトークンを選択します。

1. **[構成]** を選択します。

    プラットフォームが構成され、**[プラットフォームの構成]** ページに表示されます。

## <a name="acquire-access-token-for-ms-graph"></a>MS Graph 向けアクセス トークンの取得

Microsoft Graph のアクセス トークンを取得する必要があります。 これを行うには、Azure AD OBO フローを使用します。

SSO の現在の実装では、ユーザー レベルのアクセス許可に対する同意のみを付与します。このアクセス許可は、Graph の呼び出しには使用できません。 Graph の呼び出しに必要なアクセス許可 (スコープ) を取得するには、SSO アプリでカスタム Web サービスを実装して、Teams JavaScript SDK から受け取ったトークンを必要なスコープを含むトークンと交換する必要があります。 Microsoft Authentication Library (MSAL) を使用して、クライアント側からトークンを取得できます。

Azure AD で Graph のアクセス許可を構成したら、次の手順を実行します。

- [クライアント側コードを構成して MSAL を使用するアクセス トークンを取得する](#configure-code-to-fetch-access-token-using-msal)
- [アクセス トークンをサーバー側のコードに渡す](#pass-the-access-token-to-server-side-code)

### <a name="configure-code-to-fetch-access-token-using-msal"></a>コードを構成して MSAL を使用するアクセス トークンを取得する

次のコードは、MSAL ライブラリを使用するアクセス トークンを取得するための OBO フローの例を示しています。

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

```Node.js

// Exchange client Id side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenant id" >
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

### <a name="pass-the-access-token-to-server-side-code"></a>アクセス トークンをサーバー側のコードに渡す

Microsoft Graph データにアクセスする必要がある場合は、サーバー側のコードで次の操作を行う必要があります。

1. アクセス トークンを検証する。 詳細については、[アクセス トークンの検証](tab-sso-code.md#validate-the-access-token)に関するページを参照してください。
1. Microsoft ID プラットフォームを呼び出して、OAuth 2.0 OBO フローを開始します。これには、アクセス トークン、ユーザーに関するメタデータ、およびタブ アプリの資格情報 (ID とクライアント シークレット) を含めます。 Microsoft ID プラットフォームは、Microsoft Graph へのアクセスに使用できる新しいアクセス トークンを返します。
1. 新しいトークンを使用して Microsoft Graph からデータを取得します。
1. MSAL.NET でトークン キャッシュシリアル化を使用して、必要に応じて複数の新しいアクセス トークンをキャッシュします。

> [!IMPORTANT]
> セキュリティのベスト プラクティスとして、常にサーバー側のコードを使用して、Microsoft Graph 呼び出し、またはアクセス トークンを渡す必要があるその他の呼び出しを行います。 クライアントから Microsoft Graph への直接呼び出しを有効にするために、クライアントに OBO トークンを返しません。 これにより、トークンが傍受またはリークされないように保護できます。

## <a name="known-limitations"></a>既知の制限

テナント管理者の同意: [テナント管理者として組織に代わって同意する](/azure/active-directory/manage-apps/consent-and-permissions-overview#admin-consent)簡単な方法は、[管理者から同意](/azure/active-directory/manage-apps/grant-admin-consent)を得ることです。

認証 API を使用するその他の同意を依頼できます。 Graph のスコープを取得できるもう 1 つの方法は、既存の[サードパーティの OAuth プロバイダー認証](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page)を使用して同意ダイアログを表示する方法です。 この方法には、Azure AD 同意ダイアログ ボックスのポップアップが含まれます。

<details>
<summary>認証 API を使用してその他の同意を求めるには、次の手順を実行します。</summary>

1. `getAuthToken()` を使用して取得されたトークンでは、他の Graph API にアクセスするのに Azure AD [代理フロー](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) を使用してサーバー側で交換を行う必要があります。 この交換には v2 Graph エンドポイントを使用するようにしてください。
2. 交換が失敗した場合、Azure AD で使用できない付与例外が返されます。 通常、`invalid_grant` または `interaction_required` の 2 つのエラー メッセージのいずれかに応答します。
3. 交換が失敗すると、同意を求める必要があります。 ユーザー インターフェイス (UI) を使用して、アプリ ユーザーに他の同意を付与するように求めます。 この UI には、[サイレント認証](~/concepts/authentication/auth-silent-aad.md)を使用して Azure AD 同意ダイアログをトリガーするボタンを含める必要があります。
4. Azure AD にその他の同意を求める場合は、`prompt=consent` Azure AD への [クエリ文字列パラメーター](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) を含める必要があります。それ以外の場合、Azure AD では他のスコープを要求できなくなります。
    - `?scope={scopes}` の代わりに、 `?prompt=consent&scope={scopes}` を使用します。
    - `{scopes}` に `Mail.Read` や `User.Read` など、ユーザーに求めるすべてのスコープが含まれていることを確認します。

    タブ アプリの増分同意を処理するには、「 [増分と動的なユーザーの同意](/azure/active-directory/develop/v2-permissions-and-consent)」を参照してください。
5. ユーザーにその他のアクセス許可が付与されたら、OBO フローを再試行して、これらの他の API へのアクセスを取得します。
    </details>

## <a name="see-also"></a>関連項目

- [OAuth 2.0 On-Behalf-Of フロー](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
- [MS Graph へのアクセス権を取得する](/graph/auth-v2-user)
- [MSAL.NET でのトークン キャッシュのシリアル化](/azure/active-directory/develop/msal-net-token-cache-serialization?tabs=aspnet)
- [Microsoft Teams MSAL2 プロバイダー](/graph/toolkit/providers/teams-msal2)
