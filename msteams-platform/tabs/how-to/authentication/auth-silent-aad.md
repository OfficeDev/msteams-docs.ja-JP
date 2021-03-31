---
title: サイレント認証
description: サイレント認証について説明します
ms.topic: conceptual
keywords: teams 認証 SSO サイレント AAD
ms.openlocfilehash: 7a68c532cadf181b15c16d6bc4d4ab861d5c9922
ms.sourcegitcommit: 2bf651dfbaf5dbab6d466788f668e7a6c5d69c36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2021
ms.locfileid: "51421609"
---
# <a name="silent-authentication"></a><span data-ttu-id="a630a-104">サイレント認証</span><span class="sxs-lookup"><span data-stu-id="a630a-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="a630a-105">モバイル クライアントでタブで認証を機能するには、少なくとも 1.4.1 バージョンの Teams JavaScript SDK を使用してください。</span><span class="sxs-lookup"><span data-stu-id="a630a-105">For authentication to work for your tab on mobile clients, ensure you are using at least 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="a630a-106">Azure Active Directory (AAD) でのサイレント認証では、ユーザーがサインイン資格情報を入力する回数を最小限に抑え、認証トークンをサイレント 更新します。</span><span class="sxs-lookup"><span data-stu-id="a630a-106">Silent authentication in Azure Active Directory (AAD) minimizes the number of times a user enters their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="a630a-107">シングル サインオンの真のサポートについては、SSO のドキュメント [を参照してください](~/tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="a630a-107">For true single sign-on support, see [SSO documentation](~/tabs/how-to/authentication/auth-aad-sso.md).</span></span>

<span data-ttu-id="a630a-108">コードを完全にクライアント側に保持する場合は [、JavaScript](/azure/active-directory/develop/active-directory-authentication-libraries) の AAD 認証ライブラリを使用して、AAD アクセス トークンをサイレント モードで取得できます。</span><span class="sxs-lookup"><span data-stu-id="a630a-108">If you want to keep your code completely client-side, you can use the [AAD authentication library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to get an AAD access token silently.</span></span> <span data-ttu-id="a630a-109">ユーザーが最近サインインした場合、ポップアップ ダイアログ ボックスは表示されます。</span><span class="sxs-lookup"><span data-stu-id="a630a-109">If the user has signed in recently, they never see a popup dialog box.</span></span>

<span data-ttu-id="a630a-110">このライブラリADAL.js AngularJS アプリケーション用に最適化されているにもかかわらず、純粋な JavaScript シングル ページ アプリケーションでも動作します。</span><span class="sxs-lookup"><span data-stu-id="a630a-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="a630a-111">現在、サイレント認証はタブでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="a630a-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="a630a-112">ボットからサインインしても機能しません。</span><span class="sxs-lookup"><span data-stu-id="a630a-112">It does not work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="a630a-113">サイレント認証の仕組み</span><span class="sxs-lookup"><span data-stu-id="a630a-113">How silent authentication works</span></span>

<span data-ttu-id="a630a-114">このADAL.jsは、OAuth 2.0 暗黙的な付与フロー用の非表示の iframe を作成します。</span><span class="sxs-lookup"><span data-stu-id="a630a-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow.</span></span> <span data-ttu-id="a630a-115">ただし、ライブラリは 、サインイン ページを表示AD表示しないので、 `prompt=none` 指定します。</span><span class="sxs-lookup"><span data-stu-id="a630a-115">But the library specifies `prompt=none`, so Azure AD never shows the sign in page.</span></span> <span data-ttu-id="a630a-116">ユーザーがサインインまたはアプリケーションへのアクセス許可を必要とするためにユーザーの操作が必要な場合、AAD はアプリに報告するエラーADAL.jsすぐに返します。</span><span class="sxs-lookup"><span data-stu-id="a630a-116">If user interaction is required because the user needs to sign in or grant access to the application, AAD immediately returns an error that ADAL.js reports to your app.</span></span> <span data-ttu-id="a630a-117">この時点で、アプリは必要に応じてサインイン ボタンを表示できます。</span><span class="sxs-lookup"><span data-stu-id="a630a-117">At this point your app can show a sign in button if required.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="a630a-118">サイレント認証を実行する方法</span><span class="sxs-lookup"><span data-stu-id="a630a-118">How to do silent authentication</span></span>

<span data-ttu-id="a630a-119">この記事のコードは、Teams 認証サンプル ノードである [Teams サンプル アプリから提供されます](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)。</span><span class="sxs-lookup"><span data-stu-id="a630a-119">The code in this article comes from the Teams sample app that is [Teams authentication sample node](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).</span></span>

<span data-ttu-id="a630a-120">[AAD を使用してサイレント認証と簡単な認証構成可能](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) タブを開始し、指示に従ってローカル コンピューターでサンプルを実行します。</span><span class="sxs-lookup"><span data-stu-id="a630a-120">[Initiate silent and simple authentication configurable tab using AAD](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) and follow the instructions to run the sample on your local machine.</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="a630a-121">ADAL を含めるおよび構成する</span><span class="sxs-lookup"><span data-stu-id="a630a-121">Include and configure ADAL</span></span>

<span data-ttu-id="a630a-122">タブ ページに ADAL.jsライブラリを含め、クライアント ID とリダイレクト URL を使用して ADAL を構成します。</span><span class="sxs-lookup"><span data-stu-id="a630a-122">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="a630a-123">ユーザー コンテキストの取得</span><span class="sxs-lookup"><span data-stu-id="a630a-123">Get the user context</span></span>

<span data-ttu-id="a630a-124">タブのコンテンツ ページで、現在のユーザーのサインイン ヒントを取得 `microsoftTeams.getContext()` するために呼び出します。</span><span class="sxs-lookup"><span data-stu-id="a630a-124">In the tab's content page, call `microsoftTeams.getContext()` to get a sign in hint for the current user.</span></span> <span data-ttu-id="a630a-125">これは、AAD の呼び出しで loginHint として使用されます。</span><span class="sxs-lookup"><span data-stu-id="a630a-125">This is used as a loginHint in the call to AAD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="a630a-126">認証</span><span class="sxs-lookup"><span data-stu-id="a630a-126">Authenticate</span></span>

<span data-ttu-id="a630a-127">有効期限が切れていないユーザーのトークンが ADAL にキャッシュされている場合は、そのトークンを使用します。</span><span class="sxs-lookup"><span data-stu-id="a630a-127">If ADAL has a token cached for the user that has not expired, use that token.</span></span> <span data-ttu-id="a630a-128">または、呼び出してトークンをサイレント モードで取得します `acquireToken(resource, callback)` 。</span><span class="sxs-lookup"><span data-stu-id="a630a-128">Alternately, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="a630a-129">ADAL.js要求されたトークンでコールバック関数を呼び出したり、認証に失敗した場合にエラーが発生したりします。</span><span class="sxs-lookup"><span data-stu-id="a630a-129">ADAL.js calls the callback function with the requested token, or gives an error if authentication fails.</span></span>

<span data-ttu-id="a630a-130">コールバック関数でエラーが発生した場合は、サインイン ボタンを表示し、明示的なサインインに戻します。</span><span class="sxs-lookup"><span data-stu-id="a630a-130">If you get an error in the callback function, show a sign in button and fall back to an explicit sign in.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="a630a-131">戻り値を処理する</span><span class="sxs-lookup"><span data-stu-id="a630a-131">Process the return value</span></span>

<span data-ttu-id="a630a-132">ADAL.jsコールバック ページで呼び出すことによって、AAD からの `AuthenticationContext.handleWindowCallback(hash)` 結果を解析します。</span><span class="sxs-lookup"><span data-stu-id="a630a-132">ADAL.js parses the result from AAD by calling `AuthenticationContext.handleWindowCallback(hash)` in the sign in callback page.</span></span>

<span data-ttu-id="a630a-133">有効なユーザーを持ち、電話をかけられているか、メイン タブのコンテンツ ページ `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` に状態を報告してください。</span><span class="sxs-lookup"><span data-stu-id="a630a-133">Check that you have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report the status to your main tab content page.</span></span>

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

### <a name="handle-sign-out-flow"></a><span data-ttu-id="a630a-134">サインアウト フローの処理</span><span class="sxs-lookup"><span data-stu-id="a630a-134">Handle sign out flow</span></span>

<span data-ttu-id="a630a-135">AAD Auth のサインアウト フローを処理するには、次のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="a630a-135">Use the following code to handle sign out flow in AAD Auth:</span></span>

> [!NOTE]
> <span data-ttu-id="a630a-136">Teams タブまたはボットのログアウトが完了すると、現在のセッションもクリアされます。</span><span class="sxs-lookup"><span data-stu-id="a630a-136">While logout for Teams tab or bot is done, the current session is also cleared.</span></span>

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```
