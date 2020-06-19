---
title: サイレント認証
description: サイレント認証について説明します。
keywords: teams 認証 SSO サイレント AAD
ms.openlocfilehash: b8a5b8cb9328635f5730ca089da29140d0a17ac4
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801220"
---
# <a name="silent-authentication"></a>サイレント認証

> [!NOTE]
> モバイルクライアントのタブで認証が機能するには、少なくとも、Teams バージョンの Teams SDK を使用していることを確認する必要があります。

Azure Active Directory (Azure AD) でのサイレント認証は、ユーザーが認証トークンを自動的に更新することによってログイン資格情報を入力する回数を最小限に抑えます。 (真のシングルサインオンがサポートされるように、 [SSO に関するドキュメント](~/tabs/how-to/authentication/auth-aad-sso.md)をご覧ください)

コードを完全にクライアント側に保持する場合は、JavaScript の[Azure Active Directory 認証ライブラリ](/azure/active-directory/develop/active-directory-authentication-libraries)を使用して、azure AD アクセストークンの取得を暗黙的に試行することができます。 これは、ユーザーが最近サインインしたときに、ポップアップダイアログが表示されない可能性があることを意味します。

ADAL.js ライブラリは AngularJS アプリケーション用に最適化されていますが、純粋な JavaScript シングルページアプリケーションでも動作します。

> [!NOTE]
> 現時点では、サイレント認証はタブに対してのみ有効です。 Bot からサインインするときには機能しません。

## <a name="how-silent-authentication-works"></a>サイレント認証のしくみ

ADAL.js ライブラリは、OAuth 2.0 の暗黙的な付与フロー用の非表示の iframe を作成しますが、 `prompt=none` AZURE AD がログインページを表示しないように指定します。 ユーザーがログインするか、アプリケーションへのアクセス権を付与する必要があるため、ユーザーの操作が必要な場合、Azure AD はすぐに、アプリにレポート ADAL.js れるエラーを返します。 この時点で、アプリは必要に応じてログインボタンを表示することができます。

## <a name="how-to-do-silent-authentication"></a>サイレント認証を行う方法

この記事のコードは Teams サンプルアプリの[Microsoft Teams 認証サンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)から取得されます。

### <a name="include-and-configure-adal"></a>ADAL を含めるおよび構成する

タブページに ADAL.js ライブラリを含め、クライアント ID とリダイレクト URL を使用して ADAL を構成します。

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

### <a name="get-the-user-context"></a>ユーザーコンテキストを取得する

タブの [コンテンツ] ページで、 `microsoftTeams.getContext()` 現在のユーザーのログインヒントを取得するためにを呼び出します。 これは、Azure AD への呼び出しで login_hint として使用されます。

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

ADAL にユーザーの切れトークンがキャッシュされている場合は、そのトークンを使用します。 それ以外の場合は、を呼び出してトークンをサイレントに取得し `acquireToken(resource, callback)` ます。 ADAL.js は、要求されたトークンを使用してコールバック関数を呼び出します。認証が失敗した場合はエラーになります。

コールバック関数でエラーが発生した場合は、ログインボタンを表示し、明示的なログインに戻します。

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

`AuthenticationContext.handleWindowCallback(hash)`[ログインコールバック] ページで呼び出して、AZURE AD からの結果を解析することを ADAL.js に任せます。

有効なユーザーが存在することを確認し、その `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` 状態をメインタブのコンテンツページに報告するために呼び出します。

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
