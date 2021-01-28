---
title: サイレント認証
description: サイレント認証について説明します。
ms.topic: conceptual
keywords: Teams 認証 SSO サイレント AAD
ms.openlocfilehash: e55e415aba08fdedf4409abf39115838c3a5faf0
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014097"
---
# <a name="silent-authentication"></a>サイレント認証

> [!NOTE]
> モバイル クライアントのタブで認証を機能するには、Teams JavaScript SDK の 1.4.1 バージョン以上を使用している必要があります。

Azure Active Directory (Azure AD) でのサイレント認証は、ユーザーがログイン資格情報を入力する必要がある回数を最小限に抑えるために、認証トークンをサイレント 更新します。 (シングル サインオンの真のサポートについては [、SSO ドキュメントを参照してください](~/tabs/how-to/authentication/auth-aad-sso.md))

コードを完全にクライアント側に維持する場合は [、JavaScript](/azure/active-directory/develop/active-directory-authentication-libraries) 用 Azure Active Directory 認証ライブラリを使用して、Azure AD アクセス トークンをサイレント モードで取得することができます。 つまり、ユーザーが最近サインインした場合、ポップアップ ダイアログが表示される可能性は一度も発生しない可能性があります。

このライブラリADAL.js AngularJS アプリケーション用に最適化されているにもかかわらず、純粋な JavaScript シングルページ アプリケーションでも動作します。

> [!NOTE]
> 現在、サイレント認証はタブでのみ機能します。 ボットからサインインする場合、まだ機能しません。

## <a name="how-silent-authentication-works"></a>サイレント認証のしくみ

このADAL.jsライブラリは、OAuth 2.0 の暗黙的な付与フロー用に非表示の iframe を作成しますが、Azure AD がログイン ページを表示しなけれなすように指定 `prompt=none` します。 ユーザーがログインまたはアプリケーションへのアクセスを許可する必要があるという理由でユーザーの操作が必要な場合、Azure AD は直ちにエラーを返し、ADAL.jsがアプリに報告します。 この時点で、必要に応じてアプリにログイン ボタンを表示できます。

## <a name="how-to-do-silent-authentication"></a>サイレント認証を実行する方法

この記事のコードは、Teams サンプル アプリ [の Microsoft Teams 認証サンプル (ノード) から提供されています](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)。

### <a name="include-and-configure-adal"></a>ADAL を含め、構成する

タブ ページにADAL.jsライブラリを含め、クライアント ID とリダイレクト URL を使用して ADAL を構成します。

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // ADAL.js configuration
    let config = {
        clientId: "YOUR_APP_ID_HERE",
        // redirectUri must be in the list of redirect URLs for the Azure AD app
        redirectUri: window.location.origin + "/tab-auth/silent-end",
        cacheLocation: "localStorage",
        navigateToLoginRequestUrl: false,
    };
</script>
```

### <a name="get-the-user-context"></a>ユーザー コンテキストを取得する

タブのコンテンツ ページで、現在のユーザー `microsoftTeams.getContext()` のログイン ヒントを取得するために呼び出します。 これは、Azure login_hint への呼び出しで、AD。

```javascript
// Set up extra query parameters for ADAL
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a>認証

ユーザーに対して ADAL に有効期限が設定されていないトークンがキャッシュされている場合は、そのトークンを使用します。 それ以外の場合は、呼び出してトークンをサイレント モードで取得します `acquireToken(resource, callback)` 。 ADAL.js要求されたトークンを使用してコールバック関数を呼び出します。認証に失敗した場合はエラーが発生します。

コールバック関数でエラーが発生した場合は、ログイン ボタンを表示し、明示的なログインにフォール バックします。

```javascript
let authContext = new AuthenticationContext(config); // from the ADAL.js library
// See if there's a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which ADAL.js returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure ADAL gave us an id token
        if (tokenType !== authContext.CONSTANTS.ID_TOKEN) {
            token = authContext.getCachedToken(config.clientId);
        }
        showProfileInformation(idToken);
    } else {
        console.log("Renewal failed: " + err);
        // Failed to get the token silently; show the login button
        showLoginButton();
        // You could attempt to launch the login popup here, but in browsers this could be blocked by
        // a popup blocker, in which case the login attempt will fail with the reason FailedToOpenWindow.
    }
});
```

### <a name="process-the-return-value"></a>戻り値を処理する

Azure ADAL.js結果の解析は、ログイン コールバック ページAD呼び出して `AuthenticationContext.handleWindowCallback(hash)` 行います。

有効なユーザーがいて、電話をかけられているか、メイン タブのコンテンツ ページにステータス `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` を報告します。

```javascript
if (authContext.isCallback(window.location.hash)) {
    authContext.handleWindowCallback(window.location.hash);
    if (window.parent === window) {
        if (authContext.getCachedUser()) {
            microsoftTeams.authentication.notifySuccess();
        } else {
            microsoftTeams.authentication.notifyFailure(authContext.getLoginError());
        }
    }
}
```
