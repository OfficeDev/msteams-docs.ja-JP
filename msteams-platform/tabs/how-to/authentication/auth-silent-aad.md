---
title: サイレント認証
description: サイレント認証、シングル サインオン、タブのAzure AD説明します。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams 認証 SSO サイレント Azure ADタブ
ms.openlocfilehash: e59b7ff30a0659b670796c56b97eda437f907739
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821571"
---
# <a name="silent-authentication"></a>サイレント認証

> [!IMPORTANT]
> セキュリティ修正プログラムを含む Active Directory 認証ライブラリ (ADAL) の Microsoft サポートと開発は **、2022 年 6 月 30** 日に終了します。 Microsoft 認証ライブラリ (MSAL) を使用してサポートを引き続き受け取るアプリケーションを更新します。 「 [アプリケーションを Microsoft 認証ライブラリ (MSAL)に移行する」を参照してください](/azure/active-directory/develop/msal-migration)。

> [!NOTE]
> モバイル クライアントでタブで認証を機能するには、JavaScript SDK バージョン 1.4.1 以降Teamsを使用してください。

サイレント認証はAzure ADトークンをサイレント 更新することで、ユーザーが資格情報を入力する回数を最小限に抑える必要があります。 シングル サインオンの真のサポートについては、SSO のドキュメント [を参照してください](~/tabs/how-to/authentication/auth-aad-sso.md)。

コードクライアント側を保持するには、JavaScript Azure AD[](/azure/active-directory/develop/active-directory-authentication-libraries)認証ライブラリを使用して、Microsoft Azure Active Directory (Azure AD) アクセス トークンをサイレント モードで取得します。 ユーザーが最近サインインした場合、ポップアップ ダイアログ ボックスは表示されない。

Active Directory 認証ライブラリは AngularJS アプリケーション用に最適化されています。JavaScript シングル ページ アプリケーション (SPA) でも機能します。

> [!NOTE]
> 現在、サイレント認証はタブでのみ機能します。 ボットからサインインしても機能しません。

## <a name="how-silent-authentication-works"></a>サイレント認証の仕組み

Active Directory 認証ライブラリは、OAuth 2.0 暗黙的な付与フロー用の非表示の iframe を作成します。 ただし、ライブラリは 、`prompt=none`サインイン Azure ADページを表示しないので、指定します。 ユーザーがサインインするか、アプリケーションへのアクセスを許可する必要がある場合は、ユーザーの操作が必要になる場合があります。 ユーザーの操作が必要な場合Azure AD、ライブラリがアプリに報告するエラーが返されます。 必要に応じて、アプリにサインイン オプションを表示できます。

## <a name="how-to-do-silent-authentication"></a>サイレント認証を実行する方法

この記事のコードは、認証サンプル ノードTeamsサンプル アプリTeams[から来ます](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)。

[[サイレント認証] タブと](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) [簡易認証構成可能] Azure ADを開始し、指示に従ってローカル コンピューターでサンプルを実行します。

### <a name="include-and-configure-active-directory-authentication-library"></a>Active Directory 認証ライブラリを含め、構成する

Active Directory 認証ライブラリをタブ ページに含め、クライアント ID とリダイレクト URL を使用してライブラリを構成します。

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // Active Directory Authentication Library configuration
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

タブのコンテンツ ページで、現在 `microsoftTeams.getContext()` のユーザーのサインイン ヒントを取得するために呼び出します。 ヒントは、ユーザーに対する`loginHint`呼び出しで使用Azure AD。

```javascript
// Set up extra query parameters for Active Directory Authentication Library
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a>認証

Active Directory 認証ライブラリに、ユーザー用にキャッシュされた未発行のトークンがある場合は、トークンを使用します。 または、トークンをサイレント `acquireToken(resource, callback)` 受信する呼び出しを行います。 ライブラリは、要求されたトークンを使用してコールバック関数を呼び出したり、認証に失敗した場合にエラーを生成します。

コールバック関数でエラーが発生した場合は、明示的なサインイン オプションを表示して使用します。

```javascript
let authContext = new AuthenticationContext(config); // from Active Directory Authentication Library
// See if there is a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which Active Directory Authentication Library returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure Active Directory Authentication Library gave us an ID token
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

Active Directory 認証ライブラリは、サインイン コールバック ページAzure AD呼`AuthenticationContext.handleWindowCallback(hash)`び出すことによって、ユーザーからの結果を解析します。

有効なユーザーを持ち、電話をか`microsoftTeams.authentication.notifySuccess()``microsoftTeams.authentication.notifyFailure()`けられているか、メイン タブのコンテンツ ページに状態を報告してください。

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

### <a name="handle-the-sign-out-flow"></a>サインアウト フローの処理

次のコードを使用して、認証のサインアウト フローをAzure ADします。

> [!NOTE]
> タブまたはボットからTeamsすると、現在のセッションがクリアされます。

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>関連項目

* [ID プロバイダーが ID プロバイダーを使用Azure AD](../../../concepts/authentication/configure-identity-provider.md)
* [Microsoft 認証ライブラリ (MSAL) について](/azure/active-directory/develop/msal-overview)
