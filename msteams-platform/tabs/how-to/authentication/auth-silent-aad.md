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
# <a name="silent-authentication"></a><span data-ttu-id="50f8a-104">サイレント認証</span><span class="sxs-lookup"><span data-stu-id="50f8a-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="50f8a-105">モバイル クライアントのタブで認証を機能するには、Teams JavaScript SDK の 1.4.1 バージョン以上を使用している必要があります。</span><span class="sxs-lookup"><span data-stu-id="50f8a-105">For authentication to work for your tab on mobile clients, you need to ensure you're using at least the 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="50f8a-106">Azure Active Directory (Azure AD) でのサイレント認証は、ユーザーがログイン資格情報を入力する必要がある回数を最小限に抑えるために、認証トークンをサイレント 更新します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-106">Silent authentication in Azure Active Directory (Azure AD) minimizes the number of times a user needs to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="50f8a-107">(シングル サインオンの真のサポートについては [、SSO ドキュメントを参照してください](~/tabs/how-to/authentication/auth-aad-sso.md))</span><span class="sxs-lookup"><span data-stu-id="50f8a-107">(For true single sign-on support, view our [SSO Documentation](~/tabs/how-to/authentication/auth-aad-sso.md))</span></span>

<span data-ttu-id="50f8a-108">コードを完全にクライアント側に維持する場合は [、JavaScript](/azure/active-directory/develop/active-directory-authentication-libraries) 用 Azure Active Directory 認証ライブラリを使用して、Azure AD アクセス トークンをサイレント モードで取得することができます。</span><span class="sxs-lookup"><span data-stu-id="50f8a-108">If you want to keep your code completely client-side, you can use the [Azure Active Directory Authentication Library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to attempt to acquire an Azure AD access token silently.</span></span> <span data-ttu-id="50f8a-109">つまり、ユーザーが最近サインインした場合、ポップアップ ダイアログが表示される可能性は一度も発生しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="50f8a-109">This means that the user may never see a popup dialog if they have signed in recently.</span></span>

<span data-ttu-id="50f8a-110">このライブラリADAL.js AngularJS アプリケーション用に最適化されているにもかかわらず、純粋な JavaScript シングルページ アプリケーションでも動作します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="50f8a-111">現在、サイレント認証はタブでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="50f8a-112">ボットからサインインする場合、まだ機能しません。</span><span class="sxs-lookup"><span data-stu-id="50f8a-112">It does not yet work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="50f8a-113">サイレント認証のしくみ</span><span class="sxs-lookup"><span data-stu-id="50f8a-113">How silent authentication works</span></span>

<span data-ttu-id="50f8a-114">このADAL.jsライブラリは、OAuth 2.0 の暗黙的な付与フロー用に非表示の iframe を作成しますが、Azure AD がログイン ページを表示しなけれなすように指定 `prompt=none` します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow, but it specifies `prompt=none` so that Azure AD never shows the login page.</span></span> <span data-ttu-id="50f8a-115">ユーザーがログインまたはアプリケーションへのアクセスを許可する必要があるという理由でユーザーの操作が必要な場合、Azure AD は直ちにエラーを返し、ADAL.jsがアプリに報告します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-115">If user interaction is required because the user needs to log in or grant access to the application, Azure AD will immediately return an error that ADAL.js then reports to your app.</span></span> <span data-ttu-id="50f8a-116">この時点で、必要に応じてアプリにログイン ボタンを表示できます。</span><span class="sxs-lookup"><span data-stu-id="50f8a-116">At this point your app can show a login button if needed.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="50f8a-117">サイレント認証を実行する方法</span><span class="sxs-lookup"><span data-stu-id="50f8a-117">How to do silent authentication</span></span>

<span data-ttu-id="50f8a-118">この記事のコードは、Teams サンプル アプリ [の Microsoft Teams 認証サンプル (ノード) から提供されています](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)。</span><span class="sxs-lookup"><span data-stu-id="50f8a-118">The code in this article comes from the Teams sample app [Microsoft Teams Authentication Sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="50f8a-119">ADAL を含め、構成する</span><span class="sxs-lookup"><span data-stu-id="50f8a-119">include and configure ADAL</span></span>

<span data-ttu-id="50f8a-120">タブ ページにADAL.jsライブラリを含め、クライアント ID とリダイレクト URL を使用して ADAL を構成します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-120">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="50f8a-121">ユーザー コンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="50f8a-121">Get the user context</span></span>

<span data-ttu-id="50f8a-122">タブのコンテンツ ページで、現在のユーザー `microsoftTeams.getContext()` のログイン ヒントを取得するために呼び出します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-122">In the tab's content page, call `microsoftTeams.getContext()` to get a login hint for the current user.</span></span> <span data-ttu-id="50f8a-123">これは、Azure login_hint への呼び出しで、AD。</span><span class="sxs-lookup"><span data-stu-id="50f8a-123">This will be used as a login_hint in the call to Azure AD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="50f8a-124">認証</span><span class="sxs-lookup"><span data-stu-id="50f8a-124">Authenticate</span></span>

<span data-ttu-id="50f8a-125">ユーザーに対して ADAL に有効期限が設定されていないトークンがキャッシュされている場合は、そのトークンを使用します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-125">If ADAL has an unexpired token cached for the user, use that.</span></span> <span data-ttu-id="50f8a-126">それ以外の場合は、呼び出してトークンをサイレント モードで取得します `acquireToken(resource, callback)` 。</span><span class="sxs-lookup"><span data-stu-id="50f8a-126">Otherwise, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="50f8a-127">ADAL.js要求されたトークンを使用してコールバック関数を呼び出します。認証に失敗した場合はエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-127">ADAL.js will call your callback function with the requested token, or an error if authentication fails.</span></span>

<span data-ttu-id="50f8a-128">コールバック関数でエラーが発生した場合は、ログイン ボタンを表示し、明示的なログインにフォール バックします。</span><span class="sxs-lookup"><span data-stu-id="50f8a-128">If you get an error in the callback function, show a login button and fall back to an explicit login.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="50f8a-129">戻り値を処理する</span><span class="sxs-lookup"><span data-stu-id="50f8a-129">Process the return value</span></span>

<span data-ttu-id="50f8a-130">Azure ADAL.js結果の解析は、ログイン コールバック ページAD呼び出して `AuthenticationContext.handleWindowCallback(hash)` 行います。</span><span class="sxs-lookup"><span data-stu-id="50f8a-130">Let ADAL.js take care of parsing the result from Azure AD by calling `AuthenticationContext.handleWindowCallback(hash)` in the login callback page.</span></span>

<span data-ttu-id="50f8a-131">有効なユーザーがいて、電話をかけられているか、メイン タブのコンテンツ ページにステータス `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` を報告します。</span><span class="sxs-lookup"><span data-stu-id="50f8a-131">Check that we have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report status back to your main tab content page.</span></span>

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
