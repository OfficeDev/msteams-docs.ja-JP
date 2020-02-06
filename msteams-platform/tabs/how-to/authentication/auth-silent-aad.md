---
title: サイレント認証
description: サイレント認証について説明します。
keywords: teams 認証 SSO サイレント AAD
ms.openlocfilehash: b8a5b8cb9328635f5730ca089da29140d0a17ac4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674638"
---
# <a name="silent-authentication"></a><span data-ttu-id="9a61b-104">サイレント認証</span><span class="sxs-lookup"><span data-stu-id="9a61b-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="9a61b-105">モバイルクライアントのタブで認証が機能するには、少なくとも、Teams バージョンの Teams SDK を使用していることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9a61b-105">For authentication to work for your tab on mobile clients, you need to ensure you're using at least the 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="9a61b-106">Azure Active Directory (Azure AD) でのサイレント認証は、ユーザーが認証トークンを自動的に更新することによってログイン資格情報を入力する回数を最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="9a61b-106">Silent authentication in Azure Active Directory (Azure AD) minimizes the number of times a user needs to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="9a61b-107">(真のシングルサインオンがサポートされるように、 [SSO に関するドキュメント](~/tabs/how-to/authentication/auth-aad-sso.md)をご覧ください)</span><span class="sxs-lookup"><span data-stu-id="9a61b-107">(For true single sign-on support, view our [SSO Documentation](~/tabs/how-to/authentication/auth-aad-sso.md))</span></span>

<span data-ttu-id="9a61b-108">コードを完全にクライアント側に保持する場合は、JavaScript の[Azure Active Directory 認証ライブラリ](/azure/active-directory/develop/active-directory-authentication-libraries)を使用して、azure AD アクセストークンの取得を暗黙的に試行することができます。</span><span class="sxs-lookup"><span data-stu-id="9a61b-108">If you want to keep your code completely client-side, you can use the [Azure Active Directory Authentication Library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to attempt to acquire an Azure AD access token silently.</span></span> <span data-ttu-id="9a61b-109">これは、ユーザーが最近サインインしたときに、ポップアップダイアログが表示されない可能性があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-109">This means that the user may never see a popup dialog if they have signed in recently.</span></span>

<span data-ttu-id="9a61b-110">ADAL ライブラリは AngularJS アプリケーション用に最適化されていますが、純粋な JavaScript シングルページアプリケーションでも動作します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="9a61b-111">現時点では、サイレント認証はタブに対してのみ有効です。</span><span class="sxs-lookup"><span data-stu-id="9a61b-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="9a61b-112">Bot からサインインするときには機能しません。</span><span class="sxs-lookup"><span data-stu-id="9a61b-112">It does not yet work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="9a61b-113">サイレント認証のしくみ</span><span class="sxs-lookup"><span data-stu-id="9a61b-113">How silent authentication works</span></span>

<span data-ttu-id="9a61b-114">ADAL ライブラリは、OAuth 2.0 の暗黙的な付与フロー用の非表示の iframe を作成`prompt=none`しますが、Azure AD がログインページを表示しないように指定します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow, but it specifies `prompt=none` so that Azure AD never shows the login page.</span></span> <span data-ttu-id="9a61b-115">ユーザーがログインする必要があるか、アプリケーションへのアクセスを許可する必要があるために、ユーザーの操作が必要な場合、Azure AD は、その後、ADAL がアプリケーションにレポートするエラーを返します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-115">If user interaction is required because the user needs to log in or grant access to the application, Azure AD will immediately return an error that ADAL.js then reports to your app.</span></span> <span data-ttu-id="9a61b-116">この時点で、アプリは必要に応じてログインボタンを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="9a61b-116">At this point your app can show a login button if needed.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="9a61b-117">サイレント認証を行う方法</span><span class="sxs-lookup"><span data-stu-id="9a61b-117">How to do silent authentication</span></span>

<span data-ttu-id="9a61b-118">この記事のコードは Teams サンプルアプリの[Microsoft Teams 認証サンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)から取得されます。</span><span class="sxs-lookup"><span data-stu-id="9a61b-118">The code in this article comes from the Teams sample app [Microsoft Teams Authentication Sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="9a61b-119">ADAL を含めるおよび構成する</span><span class="sxs-lookup"><span data-stu-id="9a61b-119">include and configure ADAL</span></span>

<span data-ttu-id="9a61b-120">タブページに ADAL ライブラリを含め、クライアント ID とリダイレクト URL を使用して ADAL を構成します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-120">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="9a61b-121">ユーザーコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="9a61b-121">Get the user context</span></span>

<span data-ttu-id="9a61b-122">タブの [コンテンツ] ページで、 `microsoftTeams.getContext()`現在のユーザーのログインヒントを取得するためにを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-122">In the tab's content page, call `microsoftTeams.getContext()` to get a login hint for the current user.</span></span> <span data-ttu-id="9a61b-123">これは、Azure AD への呼び出しで login_hint として使用されます。</span><span class="sxs-lookup"><span data-stu-id="9a61b-123">This will be used as a login_hint in the call to Azure AD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="9a61b-124">認証</span><span class="sxs-lookup"><span data-stu-id="9a61b-124">Authenticate</span></span>

<span data-ttu-id="9a61b-125">ADAL にユーザーの切れトークンがキャッシュされている場合は、そのトークンを使用します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-125">If ADAL has an unexpired token cached for the user, use that.</span></span> <span data-ttu-id="9a61b-126">それ以外の場合は、を呼び出し`acquireToken(resource, callback)`てトークンをサイレントに取得します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-126">Otherwise, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="9a61b-127">ADAL は、要求されたトークンを使用してコールバック関数を呼び出します。認証が失敗した場合はエラーになります。</span><span class="sxs-lookup"><span data-stu-id="9a61b-127">ADAL.js will call your callback function with the requested token, or an error if authentication fails.</span></span>

<span data-ttu-id="9a61b-128">コールバック関数でエラーが発生した場合は、ログインボタンを表示し、明示的なログインに戻します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-128">If you get an error in the callback function, show a login button and fall back to an explicit login.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="9a61b-129">戻り値を処理する</span><span class="sxs-lookup"><span data-stu-id="9a61b-129">Process the return value</span></span>

<span data-ttu-id="9a61b-130">ADAL がログインコールバックページで呼び出し`AuthenticationContext.handleWindowCallback(hash)`て、Azure AD からの結果を解析できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9a61b-130">Let ADAL.js take care of parsing the result from Azure AD by calling `AuthenticationContext.handleWindowCallback(hash)` in the login callback page.</span></span>

<span data-ttu-id="9a61b-131">有効なユーザーが存在することを確認`microsoftTeams.authentication.notifySuccess()`し`microsoftTeams.authentication.notifyFailure()` 、その状態をメインタブのコンテンツページに報告するために呼び出します。</span><span class="sxs-lookup"><span data-stu-id="9a61b-131">Check that we have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report status back to your main tab content page.</span></span>

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