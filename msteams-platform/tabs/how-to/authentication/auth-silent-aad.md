---
title: サイレント認証
description: サイレント認証について説明します
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams 認証 SSO サイレント AAD
ms.openlocfilehash: 02078775ef3349ae5bb35e999e0f65587ab943d1
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156092"
---
# <a name="silent-authentication"></a>サイレント認証

> [!NOTE]
> モバイル クライアントでタブで認証を機能するには、JavaScript SDK の 1.4.1 以上のバージョンを使用Teamsしてください。

Azure Active Directory (AAD) のサイレント認証では、ユーザーがサインイン資格情報を入力する回数を最小限に抑え、認証トークンをサイレント 更新します。 シングル サインオンの真のサポートについては、SSO のドキュメント [を参照してください](~/tabs/how-to/authentication/auth-aad-sso.md)。

コードを完全にクライアント側に保持する場合は [、JavaScript](/azure/active-directory/develop/active-directory-authentication-libraries) の AAD 認証ライブラリを使用して、AAD アクセス トークンをサイレント モードで取得できます。 ユーザーが最近サインインした場合、ポップアップ ダイアログ ボックスは表示されます。

このライブラリADAL.js AngularJS アプリケーション用に最適化されているにもかかわらず、純粋な JavaScript シングル ページ アプリケーションでも動作します。

> [!NOTE]
> 現在、サイレント認証はタブでのみ機能します。 ボットからサインインしても機能しません。

## <a name="how-silent-authentication-works"></a>サイレント認証の仕組み

このADAL.jsは、OAuth 2.0 暗黙的な付与フロー用の非表示の iframe を作成します。 ただし、ライブラリは 、サインイン ページを表示AD表示しないので、 `prompt=none` 指定します。 ユーザーがサインインまたはアプリケーションへのアクセス許可を必要とするためにユーザーの操作が必要な場合、AAD はアプリに報告するエラーADAL.jsすぐに返します。 この時点で、アプリは必要に応じてサインイン ボタンを表示できます。

## <a name="how-to-do-silent-authentication"></a>サイレント認証を実行する方法

この記事のコードは、認証サンプル ノードTeamsサンプル アプリTeams[から来ます](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)。

[AAD を使用してサイレント認証と簡単な認証構成可能](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) タブを開始し、指示に従ってローカル コンピューターでサンプルを実行します。

### <a name="include-and-configure-adal"></a>ADAL を含めるおよび構成する

タブ ページに ADAL.jsライブラリを含め、クライアント ID とリダイレクト URL を使用して ADAL を構成します。

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

### <a name="get-the-user-context"></a>ユーザー コンテキストの取得

タブのコンテンツ ページで、現在のユーザーのサインイン ヒントを取得 `microsoftTeams.getContext()` するために呼び出します。 これは、AAD の呼び出しで loginHint として使用されます。

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

有効期限が切れていないユーザーのトークンが ADAL にキャッシュされている場合は、そのトークンを使用します。 または、呼び出してトークンをサイレント モードで取得します `acquireToken(resource, callback)` 。 ADAL.js要求されたトークンでコールバック関数を呼び出したり、認証に失敗した場合にエラーが発生したりします。

コールバック関数でエラーが発生した場合は、サインイン ボタンを表示し、明示的なサインインに戻します。

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

ADAL.jsコールバック ページで呼び出すことによって、AAD からの `AuthenticationContext.handleWindowCallback(hash)` 結果を解析します。

有効なユーザーを持ち、電話をかけられているか、メイン タブのコンテンツ ページ `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` に状態を報告してください。

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

### <a name="handle-sign-out-flow"></a>サインアウト フローの処理

AAD Auth のサインアウト フローを処理するには、次のコードを使用します。

> [!NOTE]
> タブまたはボットTeamsログアウトが完了すると、現在のセッションもクリアされます。

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```
