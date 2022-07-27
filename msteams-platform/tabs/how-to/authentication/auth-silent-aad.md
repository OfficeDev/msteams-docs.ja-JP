---
title: サイレント認証
description: このモジュールでは、サイレント認証、シングル サインオン、Azure AD をタブに対して実行する方法と動作方法について説明します
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 7df394bf43bd004e0a430b011ad5aad9c23d6983
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035311"
---
# <a name="use-silent-authentication-in-azure-ad"></a>Azure AD でサイレント認証を使用する

> [!IMPORTANT]
> セキュリティ修正プログラムを含む Active Directory Authentication Library (ADAL) の Microsoft サポートと開発は、 **2022 年 6 月 30** 日に終了します。 引き続きサポートを受けるには、Microsoft Authentication Library (MSAL) を使用するようにアプリケーションを更新します。 [Microsoft Authentication Library (MSAL) へのアプリケーションの移行に関するページを](/azure/active-directory/develop/msal-migration)参照してください。

> [!NOTE]
> モバイル クライアントのタブで認証を機能させるには、Teams JavaScript SDK バージョン 1.4.1 以降を使用していることを確認します。

Azure AD のサイレント認証では、認証トークンをサイレント に更新することで、ユーザーが資格情報を入力する回数が最小限に抑えられます。 シングル サインオンの真のサポートについては、 [SSO のドキュメントを参照してください](~/tabs/how-to/authentication/tab-sso-overview.md)。

コード クライアント側を維持するには、[JavaScript 用の Azure AD 認証ライブラリ](/azure/active-directory/develop/active-directory-authentication-libraries)を使用して、Microsoft Azure Active Directory (Azure AD) アクセス トークンをサイレント モードで取得します。 ユーザーが最近サインインした場合、ポップアップ ダイアログ ボックスは表示されません。

Active Directory 認証ライブラリは AngularJS アプリケーション用に最適化されていますが、JavaScript シングルページ アプリケーション (SPA) でも動作します。

> [!NOTE]
> 現時点では、サイレント認証はタブでのみ機能します。 ボットからサインインする場合は機能しません。

## <a name="how-silent-authentication-works"></a>サイレント認証のしくみ

Active Directory 認証ライブラリでは、OAuth 2.0 の暗黙的な許可フロー用に非表示の iframe が作成されます。 ただし、このライブラリでは `prompt=none`、Azure AD にサインイン ページが表示されないように指定されています。 ユーザーがサインインするか、アプリケーションへのアクセスを許可する必要がある場合は、ユーザー操作が必要になる場合があります。 ユーザー操作が必要な場合は、ライブラリがアプリに報告するエラーが Azure AD によって返されます。 必要に応じて、アプリにサインイン オプションを表示できるようになりました。

## <a name="how-to-do-silent-authentication"></a>サイレント認証を行う方法

この記事のコードは、Teams [認証サンプル ノードである Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs) サンプル アプリからのものです。

[Azure AD を使用してサイレントでシンプルな認証構成可能タブを開始](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) し、指示に従ってローカル コンピューターでサンプルを実行します。

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

### <a name="get-the-user-context"></a>ユーザー コンテキストを取得する

タブのコンテンツ ページで、現在のユーザーのサインイン ヒントを取得するために呼び出 `microsoftTeams.getContext()` します。 このヒントは、Azure AD の呼び出しで使用 `loginHint` されます。

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

Active Directory 認証ライブラリに、ユーザーの有効期限が切れていないトークンがキャッシュされている場合は、そのトークンを使用します。 または、サイレント モードでトークンを受信するように呼び出 `acquireToken(resource, callback)` します。 ライブラリは、要求されたトークンを使用してコールバック関数を呼び出すか、認証が失敗した場合にエラーを生成します。

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

Active Directory 認証ライブラリは、サインイン コールバック ページで呼び出 `AuthenticationContext.handleWindowCallback(hash)` すことによって、Azure AD の結果を解析します。

有効なユーザーが存在することを確認し、呼び出 `microsoftTeams.authentication.notifySuccess()` すか `microsoftTeams.authentication.notifyFailure()` 、メイン タブのコンテンツ ページに状態を報告します。

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

### <a name="handle-the-sign-out-flow"></a>サインアウト フローを処理する

Azure AD 認証でサインアウト フローを処理するには、次のコードを使用します。

> [!NOTE]
> Teams タブまたはボットからログアウトすると、現在のセッションがクリアされます。

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>関連項目

* [Azure AD を使用するように ID プロバイダーを構成する](../../../concepts/authentication/configure-identity-provider.md)
* [Microsoft 認証ライブラリ (MSAL) について知る](/azure/active-directory/develop/msal-overview)
