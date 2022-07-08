---
title: タブの SSO を有効にするためのコード構成
description: タブの SSO を有効にするためのコード構成について説明します
ms.topic: how-to
ms.localizationpriority: high
keywords: Teams 認証タブ Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: 466da3cbd879ed2546adcad87f6f55620d54256d
ms.sourcegitcommit: 07f41abbeb1572a306a789485953c5588d65051e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2022
ms.locfileid: "66658938"
---
# <a name="add-code-to-enable-sso"></a>SSO を有効にするコードを追加する

SSO を有効にするコードを追加する前に、Azure AD にアプリを登録していることを確認します。

> [!div class="nextstepaction"]
> [Azure AD に登録](tab-sso-register-aad.md)

Azure AD からアクセス トークンを取得するには、タブ アプリのクライアント側コードを構成する必要があります。 アクセス トークンは、タブ アプリの代わりに発行されます。 タブ アプリに追加の Microsoft Graph アクセス許可が必要な場合は、アクセス トークンをサーバー側に渡し、Microsoft Graph トークンと交換する必要があります。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-config-code.png" alt-text="アクセス トークンを処理するためのコードを構成する":::

このセクションでは、次の手順について説明します。

- [クライアント側のコードを追加する](#add-client-side-code)
- [アクセス トークンをサーバー側のコードに渡す](#pass-the-access-token-to-server-side-code)
- [アクセス トークンを検証する](#validate-the-access-token)

## <a name="add-client-side-code"></a>クライアント側のコードを追加する

現在のアプリ ユーザーのアプリ アクセスを取得するには、クライアント側のコードがアクセス トークンを取得するために Teams を呼び出す必要があります。 `getAuthToken()` を使用して検証プロセスを開始するために、クライアント側のコードを更新する必要があります。

<br>
<details>
<summary>getAuthToken() に関する詳細情報</summary>
<br>
`getAuthToken()` は、Microsoft Teams JavaScript SDK のメソッドです。 アプリに代わって発行される Azure AD アクセス トークンを要求します。 有効期限が切れていない場合は、トークンをキャッシュから取得します。 有効期限が切れている場合は、新しいアクセス トークンを取得するために Azure AD に要求が送信されます。

 詳細については、[getAuthToken](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true) を参照してください。
</details>

### <a name="when-to-call-getauthtoken"></a>getAccessToken を呼び出す場合

現在のアプリ ユーザーにアクセス トークンが必要な場合に `getAuthToken()` を使用します。

| アクセス トークンが必要な場合... | getAuthToken() を呼び出します... |
| --- | --- |
| アプリ ユーザーがアプリにアクセスする場合 | 内側の `microsoftTeams.initialize()`から。 |
| アプリの特定の機能を使用するには | アプリ ユーザーがサインインを必要とするアクションを実行した場合。 |

### <a name="add-code-for-getauthtoken"></a>getAuthToken のコードを追加する

JavaScript コード スニペットをタブ アプリに追加するには、次の手順を実行します。

- `getAuthToken()` を呼び出します。
- アクセス トークンを解析するか、それをサーバー側コードに渡します。

次のコード スニペットに、`getAuthToken()` の呼び出しの例を示します。

```javascript
microsoftTeams.initialize();
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Error getting token: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

`getAuthToken()` の呼び出しを、このトークンが必要とされる場所でアクションを開始するすべての関数とハンドラーに追加できます。

<br>
<details>
<summary>クライアント側のコードの例を次に示します。</summary>

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png" alt-text="クライアント コードを構成する" lightbox="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png":::

</details>

Teams は、アクセス トークンを受け取るとキャッシュされ、必要に応じて再利用されます。 このトークンは、Azure AD への別の呼び出しを行うことなく、有効期限が切れるまで、`getAuthToken()` が呼び出されるたびに使用できます。

> [!IMPORTANT]
> アクセス トークンのセキュリティのベスト プラクティスは以下のとおりです。
>
> - アクセス トークンが必要な場合は、常に `getAuthToken()` を呼び出します。
> - Teams によってアクセス トークンがキャッシュされます。 キャッシュしたり、アプリのコードに格納したりしないでください。

### <a name="consent-dialog-for-getting-access-token"></a>アクセス トークンを取得するための同意ダイアログ

`getAuthToken()` を呼び出し、ユーザー レベルのアクセス許可に対してアプリ ユーザーの同意が必要な場合は、現在サインインしているアプリ ユーザーに Azure AD ダイアログが表示されます。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tabs-sso-prompt.png" alt-text="タブ シングル サインオン ダイアログ プロンプト":::

表示される同意ダイアログは、Azure AD で定義された open-id スコープ用です。 アプリ ユーザーは同意を 1 回だけ行う必要があります。 同意した後、アプリ ユーザーは、付与されたアクセス許可とスコープ用のタブ アプリにアクセスして使用できます。

> [!IMPORTANT]
> 同意ダイアログが不要なシナリオ:
>
> - テナント管理者がテナントに代わって同意した場合、アプリ ユーザーに同意を求めるメッセージを表示する必要はありません。 つまり、アプリ ユーザーは同意ダイアログを表示することなく、アプリにシームレスにアクセスできます。
> - Azure AD アプリが Teams で認証要求を行うのと同じテナントに登録されている場合には、アプリ ユーザーが同意を求められることはなく、アクセス トークンがすぐ付与されます。 アプリ ユーザーは、Azure AD アプリが別のテナントに登録されている場合にのみ、これらのアクセス許可に同意します。

エラーが発生した場合は、「[Teams での SSO 認証のトラブルシューティング](tab-sso-troubleshooting.md)」を参照してください。

### <a name="use-the-access-token-as-an-identity-token"></a>アクセス トークンを ID トークンとして使用する

タブ アプリに返されるトークンは、アクセス トークン と ID トークンの両方です。 タブ アプリは、トークンを アクセス トークンとして使用して、サーバー側の API に対して認証された HTTPS 要求を行うことができます。

`getAuthToken()` から返されたアクセス トークンは、トークンの次の要求を使用してアプリ ユーザーの ID を確立するために使用できます。

- `name`: ユーザーの表示名。
- `preferred_username`: アプリ ユーザーの電子メール アドレス。
- `oid` - アプリ ユーザーの ID を表す GUID。
- `tid` - アプリ ユーザーがサインインしているテナントを表す GUID。

Teams は、ユーザーの設定など、アプリ ユーザーの ID に関連付けられたこの情報をキャッシュできます。

> [!NOTE]
> システム内のユーザーを表す一意の ID を作成する必要がある場合は、「[クレームを使用してユーザーを確実に識別する](/azure/active-directory/develop/id-tokens#using-claims-to-reliably-identify-a-user-subject-and-object-id)」を参照してください。

## <a name="pass-the-access-token-to-server-side-code"></a>アクセス トークンをサーバー側のコードに渡す

サーバー上の Web API にアクセスする必要がある場合は、アクセス トークンをサーバー側のコードに渡す必要があります。 Web API では、アクセス トークンをデコードして、そのトークンの要求を表示する必要があります。

> [!NOTE]
> Azure AD では、返されたアクセス トークンでユーザー プリンシパル名 (UPN) を受け取らない場合、それを[オプションの要求](/azure/active-directory/develop/active-directory-optional-claims)に追加します。
> 詳細については、「[アクセス トークン](/azure/active-directory/develop/access-tokens)」を参照してください。

`getAuthToken()` のコールバックに成功して受け取ったアクセス トークンは、(認証されたアプリ ユーザー用の) Web API へのアクセスを提供します。 サーバー側のコードは、必要に応じてトークンを解析して [ID 情報](#use-the-access-token-as-an-identity-token)を取得することもできます。

Microsoft Graph データを取得するためにアクセス トークンを渡す必要がある場合は、「[Microsoft Graph のアクセス許可を持つタブ アプリを拡張する](tab-sso-graph-api.md)」を参照してください。

### <a name="code-for-passing-access-token-to-server-side"></a>アクセス トークンをサーバー側に渡すためのコード

次のコードは、アクセス トークンをサーバー側に渡す例を示しています。 トークンは、サーバー側の Web API に要求を送信するときに `Authorization` ヘッダーに渡されます。 この例では JSON データを送信し、`POST` メソッドを使用します。 サーバーに書き込まない場合は、`GET` はアクセス トークンを送信するのに十分です。

```javascript
$.ajax({
    type: "POST",
    url: "/api/DoSomething",
    headers: {
        "Authorization": "Bearer " + accessToken
    },
    data: { /* some JSON payload */ },
    contentType: "application/json; charset=utf-8"
}).done(function (data) {
    // Handle success
}).fail(function (error) {
    // Handle error
}).always(function () {
    // Cleanup
});
```

### <a name="validate-the-access-token"></a>アクセス トークンを検証する

サーバー上の Web API は、アクセス トークンがクライアントから送信された場合、それをデコード詩、検証する必要があります。 このトークンは、JSON Web トークン (JWT) です。そのため、この検証は最も標準的な OAuth でのトークンの検証とまったく同様に動作します。 Web API では、アクセス トークンをデコードする必要があります。 必要に応じて、jwt.ms など、手動でツールにアクセス トークンをコピーして貼り付けます。

JWT の検証を処理できるライブラリが複数入手可能です。 基本的な検証には、次のものが含まれます。

- トークンが整形式であることを確認する
- トークンが意図した証明機関から発行されたことを確認する
- トークンが Web API をターゲットにしていることを確認する

トークンの検証時には、次のガイドラインに注意してください。

- 有効な SSO トークンは、Azure AD によって発行されます。 トークン内の `iss` クレームは、この値で始まっている必要があります。
- トークンの `aud1` パラメーターは、Azure AD アプリ登録中に生成されるアプリ ID に設定されます。
- トークンの `scp` パラメーターは `access_as_user` に設定します。

#### <a name="example-access-token"></a>アクセス トークンの例

アクセス トークンの標準的なデコードされたペイロードを次に示します。

```javascript
{
    aud: "2c3caa80-93f9-425e-8b85-0745f50c0d24",
    iss: "https://login.microsoftonline.com/fec4f964-8bc9-4fac-b972-1c1da35adbcd/v2.0",
    iat: 1521143967,
    nbf: 1521143967,
    exp: 1521147867,
    aio: "ATQAy/8GAAAA0agfnU4DTJUlEqGLisMtBk5q6z+6DB+sgiRjB/Ni73q83y0B86yBHU/WFJnlMQJ8",
    azp: "e4590ed6-62b3-5102-beff-bad2292ab01c",
    azpacr: "0",
    e_exp: 262800,
    name: "Mila Nikolova",
    oid: "6467882c-fdfd-4354-a1ed-4e13f064be25",
    preferred_username: "milan@contoso.com",
    scp: "access_as_user",
    sub: "XkjgWjdmaZ-_xDmhgN1BMP2vL2YOfeVxfPT_o8GRWaw",
    tid: "fec4f964-8bc9-4fac-b972-1c1da35adbcd",
    uti: "MICAQyhrH02ov54bCtIDAA",
    ver: "2.0"
}
```

## <a name="code-samples"></a>コード サンプル

| サンプルの名前 | 説明 | C#/.NET| Node.js |
|---------------|---------------|------|--------------|
| タブ SSO |Azure AD SSO タブのための Microsoft Teams サンプル アプリ| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)、 </br>[Teams ツールキット](../../../toolkit/visual-studio-code-tab-sso.md)|
| タブ、ボット、メッセージ拡張機能 (ME) SSO | このサンプルは、タブ、ボット、および ME の SSO (検索、アクション、linkunfurl) を示しています。 |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Teams アプリ マニフェストを更新し、アプリをプレビューする](tab-sso-manifest.md)

## <a name="see-also"></a>関連項目

- [jwt.ms](https://jwt.ms/)
- [アクティブ ディレクトリの省略可能な要求](/azure/active-directory/develop/active-directory-optional-claims)
- [アクセス トークン](/azure/active-directory/develop/access-tokens)
- [Microsoft Authentication Library (MSAL) の概要](/azure/active-directory/develop/msal-overview)
- [Microsoft ID プラットフォームの ID トークン](/azure/active-directory/develop/id-tokens)
- [Microsoft ID プラットフォームのアクセス トークン](/azure/active-directory/develop/access-tokens#validating-tokens)
