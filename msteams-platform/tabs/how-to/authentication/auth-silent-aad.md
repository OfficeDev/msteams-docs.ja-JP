---
title: サイレント認証
description: サイレント認証について説明します
ms.topic: conceptual
keywords: teams 認証 SSO サイレント AAD
ms.openlocfilehash: db8409cd4a6edface6d5dc3b3de6698852eaaa24
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449229"
---
# <a name="silent-authentication"></a><span data-ttu-id="51b78-104">サイレント認証</span><span class="sxs-lookup"><span data-stu-id="51b78-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="51b78-105">モバイル クライアントでタブで認証を機能するには、少なくとも 1.4.1 バージョンの Teams JavaScript SDK を使用してください。</span><span class="sxs-lookup"><span data-stu-id="51b78-105">For authentication to work for your tab on mobile clients, ensure you are using at least 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="51b78-106">Azure Active Directory (AAD) でのサイレント認証では、ユーザーがサインイン資格情報を入力する回数を最小限に抑え、認証トークンをサイレント 更新します。</span><span class="sxs-lookup"><span data-stu-id="51b78-106">Silent authentication in Azure Active Directory (AAD) minimizes the number of times a user enters their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="51b78-107">シングル サインオンの真のサポートについては、SSO のドキュメント [を参照してください](~/tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="51b78-107">For true single sign-on support, see [SSO documentation](~/tabs/how-to/authentication/auth-aad-sso.md).</span></span>

<span data-ttu-id="51b78-108">コードを完全にクライアント側に保持する場合は [、JavaScript](/azure/active-directory/develop/active-directory-authentication-libraries) の AAD 認証ライブラリを使用して、AAD アクセス トークンをサイレント モードで取得できます。</span><span class="sxs-lookup"><span data-stu-id="51b78-108">If you want to keep your code completely client-side, you can use the [AAD authentication library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to get an AAD access token silently.</span></span> <span data-ttu-id="51b78-109">ユーザーが最近サインインした場合、ポップアップ ダイアログ ボックスは表示されます。</span><span class="sxs-lookup"><span data-stu-id="51b78-109">If the user has signed in recently, they never see a popup dialog box.</span></span>

<span data-ttu-id="51b78-110">このライブラリADAL.js AngularJS アプリケーション用に最適化されているにもかかわらず、純粋な JavaScript シングル ページ アプリケーションでも動作します。</span><span class="sxs-lookup"><span data-stu-id="51b78-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="51b78-111">現在、サイレント認証はタブでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="51b78-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="51b78-112">ボットからサインインしても機能しません。</span><span class="sxs-lookup"><span data-stu-id="51b78-112">It does not work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="51b78-113">サイレント認証の仕組み</span><span class="sxs-lookup"><span data-stu-id="51b78-113">How silent authentication works</span></span>

<span data-ttu-id="51b78-114">このADAL.jsは、OAuth 2.0 暗黙的な付与フロー用の非表示の iframe を作成します。</span><span class="sxs-lookup"><span data-stu-id="51b78-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow.</span></span> <span data-ttu-id="51b78-115">ただし、ライブラリは 、サインイン ページを表示AD表示しないので、 `prompt=none` 指定します。</span><span class="sxs-lookup"><span data-stu-id="51b78-115">But the library specifies `prompt=none`, so Azure AD never shows the sign in page.</span></span> <span data-ttu-id="51b78-116">ユーザーがサインインまたはアプリケーションへのアクセス許可を必要とするためにユーザーの操作が必要な場合、AAD はアプリに報告するエラーADAL.jsすぐに返します。</span><span class="sxs-lookup"><span data-stu-id="51b78-116">If user interaction is required because the user needs to sign in or grant access to the application, AAD immediately returns an error that ADAL.js reports to your app.</span></span> <span data-ttu-id="51b78-117">この時点で、アプリは必要に応じてサインイン ボタンを表示できます。</span><span class="sxs-lookup"><span data-stu-id="51b78-117">At this point your app can show a sign in button if required.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="51b78-118">サイレント認証を実行する方法</span><span class="sxs-lookup"><span data-stu-id="51b78-118">How to do silent authentication</span></span>

<span data-ttu-id="51b78-119">この記事のコードは、Teams 認証サンプル ノードである [Teams サンプル アプリから提供されます](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)。</span><span class="sxs-lookup"><span data-stu-id="51b78-119">The code in this article comes from the Teams sample app that is [Teams authentication sample node](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="51b78-120">ADAL を含め、構成する</span><span class="sxs-lookup"><span data-stu-id="51b78-120">include and configure ADAL</span></span>

<span data-ttu-id="51b78-121">タブ ページに ADAL.jsライブラリを含め、クライアント ID とリダイレクト URL を使用して ADAL を構成します。</span><span class="sxs-lookup"><span data-stu-id="51b78-121">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="51b78-122">ユーザー コンテキストの取得</span><span class="sxs-lookup"><span data-stu-id="51b78-122">Get the user context</span></span>

<span data-ttu-id="51b78-123">タブのコンテンツ ページで、現在のユーザーのサインイン ヒントを取得 `microsoftTeams.getContext()` するために呼び出します。</span><span class="sxs-lookup"><span data-stu-id="51b78-123">In the tab's content page, call `microsoftTeams.getContext()` to get a sign in hint for the current user.</span></span> <span data-ttu-id="51b78-124">これは、AAD の呼び出しで loginHint として使用されます。</span><span class="sxs-lookup"><span data-stu-id="51b78-124">This is used as a loginHint in the call to AAD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="51b78-125">認証</span><span class="sxs-lookup"><span data-stu-id="51b78-125">Authenticate</span></span>

<span data-ttu-id="51b78-126">ADAL にユーザー用にキャッシュされた未発行のトークンがある場合は、トークンを使用します。</span><span class="sxs-lookup"><span data-stu-id="51b78-126">If ADAL has an unexpired token cached for the user, use the token.</span></span> <span data-ttu-id="51b78-127">または、呼び出してトークンをサイレント モードで取得します `acquireToken(resource, callback)` 。</span><span class="sxs-lookup"><span data-stu-id="51b78-127">Alternately, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="51b78-128">ADAL.jsトークンを使用してコールバック関数を呼び出したり、認証に失敗した場合にエラーが発生したりします。</span><span class="sxs-lookup"><span data-stu-id="51b78-128">ADAL.js will call your callback function with the requested token, or give an error if authentication fails.</span></span>

<span data-ttu-id="51b78-129">コールバック関数でエラーが発生した場合は、サインイン ボタンを表示し、明示的なサインインに戻します。</span><span class="sxs-lookup"><span data-stu-id="51b78-129">If you get an error in the callback function, show a sign in button and fall back to an explicit sign in.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="51b78-130">戻り値を処理する</span><span class="sxs-lookup"><span data-stu-id="51b78-130">Process the return value</span></span>

<span data-ttu-id="51b78-131">ADAL.jsコールバック ページで呼び出すことによって、AAD からの `AuthenticationContext.handleWindowCallback(hash)` 結果を解析します。</span><span class="sxs-lookup"><span data-stu-id="51b78-131">ADAL.js parses the result from AAD by calling `AuthenticationContext.handleWindowCallback(hash)` in the sign in callback page.</span></span>

<span data-ttu-id="51b78-132">有効なユーザーを持ち、電話をかけられているか、メイン タブのコンテンツ ページ `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` に状態を報告してください。</span><span class="sxs-lookup"><span data-stu-id="51b78-132">Check that you have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report the status to your main tab content page.</span></span>

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
