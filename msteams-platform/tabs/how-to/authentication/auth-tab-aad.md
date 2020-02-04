---
title: Azure Active Directory を使用したタブの認証
description: Teams での認証と、それらをタブで使用する方法について説明します。
keywords: teams の認証タブ AAD
ms.openlocfilehash: 760fce99a51dc722905035bade6db008072ee0b4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674878"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a><span data-ttu-id="97a36-104">Microsoft Teams タブでユーザーを認証する</span><span class="sxs-lookup"><span data-stu-id="97a36-104">Authenticate a user in a Microsoft Teams tab</span></span>

> [!Note]
> <span data-ttu-id="97a36-105">モバイルクライアントのタブで認証を行うには、Teams JavaScript SDK のバージョン1.4.1 以降を使用していることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97a36-105">For authentication to work for your tab on mobile clients, you need to ensure you're using version 1.4.1 or later of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="97a36-106">Teams アプリ内で使用する必要があるサービスは多数ありますが、これらのサービスのほとんどは、サービスへのアクセスを取得するために認証と承認を必要とします。</span><span class="sxs-lookup"><span data-stu-id="97a36-106">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="97a36-107">サービスには、Facebook、Twitter、およびコースチームが含まれます。</span><span class="sxs-lookup"><span data-stu-id="97a36-107">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="97a36-108">Teams のユーザーは、Microsoft Graph を使用して Azure Active Directory (Azure AD) に保存されたユーザープロファイル情報を持っています。この記事では、Azure AD を使用した認証に重点を置いて、この情報にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="97a36-108">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph and this article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="97a36-109">OAuth 2.0 は、Azure AD とその他の多くのサービスプロバイダーによって使用される、オープンスタンダードの認証です。</span><span class="sxs-lookup"><span data-stu-id="97a36-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="97a36-110">OAuth 2.0 については、Teams および Azure AD で認証を処理するための前提条件となります。</span><span class="sxs-lookup"><span data-stu-id="97a36-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="97a36-111">次の例では、最終的に Azure AD と Microsoft Graph からユーザーのプロファイル情報を読み取るという目標を持つ OAuth 2.0 暗黙的な付与フローを使用します。</span><span class="sxs-lookup"><span data-stu-id="97a36-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="97a36-112">この記事のコードは、Teams サンプルアプリの[Microsoft teams タブ認証のサンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)から取得されます。</span><span class="sxs-lookup"><span data-stu-id="97a36-112">The code in this article comes from the Teams sample app [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span> <span data-ttu-id="97a36-113">このプロパティには、Microsoft Graph のアクセストークンを要求する静的なタブが含まれており、Azure AD からの現在のユーザーの基本プロファイル情報を示しています。</span><span class="sxs-lookup"><span data-stu-id="97a36-113">It contains a static tab that requests an access token for Microsoft Graph and shows the current user's basic profile information from Azure AD.</span></span>

<span data-ttu-id="97a36-114">タブの認証フローの一般的な概要については、「[タブでの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="97a36-114">For a general overview of authentication flow for tabs see the topic [Authentication flow in tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="97a36-115">タブ内の認証フローは、ボットの認証フローと若干異なります。</span><span class="sxs-lookup"><span data-stu-id="97a36-115">Authentication flow in tabs differs slightly from authentication flow in bots.</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="97a36-116">Id プロバイダーを構成する</span><span class="sxs-lookup"><span data-stu-id="97a36-116">Configuring identity providers</span></span>

<span data-ttu-id="97a36-117">Azure Active Directory を id プロバイダーとして使用する場合は、「 [id プロバイダー](~/concepts/authentication/configure-identity-provider.md)を構成する」の「OAuth 2.0 コールバック URL を構成する」の詳細な手順については、このトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="97a36-117">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="97a36-118">認証フローの開始</span><span class="sxs-lookup"><span data-stu-id="97a36-118">Initiate authentication flow</span></span>

<span data-ttu-id="97a36-119">認証フローは、ユーザーの操作によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="97a36-119">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="97a36-120">これにより、ブラウザーのポップアップブロックがトリガーされ、ユーザーが混乱する可能性があるので、自動的に認証ポップアップを開かないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="97a36-120">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

<span data-ttu-id="97a36-121">ユーザーが必要なときにサインインできるように、構成ページまたはコンテンツページにボタンを追加します。</span><span class="sxs-lookup"><span data-stu-id="97a36-121">Add a button to your configuration or content page to enable the user to sign in when needed.</span></span> <span data-ttu-id="97a36-122">この操作は、[タブの[構成](~/tabs/how-to/create-tab-pages/configuration-page.md)] ページまたは任意の[コンテンツ](~/tabs/how-to/create-tab-pages/content-page.md)ページで行うことができます。</span><span class="sxs-lookup"><span data-stu-id="97a36-122">This can be done in the tab [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) page or any [content](~/tabs/how-to/create-tab-pages/content-page.md) page.</span></span>

<span data-ttu-id="97a36-123">多くの id プロバイダーと同様に Azure AD は、そのコンテンツを iframe に配置することを許可しません。</span><span class="sxs-lookup"><span data-stu-id="97a36-123">Azure AD, like most identity providers, does not allow its content to be placed in an iframe.</span></span> <span data-ttu-id="97a36-124">これは、id プロバイダーをホストするポップアップページを追加する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="97a36-124">This means that you will need to add a pop-up page to host the identity provider.</span></span> <span data-ttu-id="97a36-125">このページの例を次に`/tab-auth/simple-start`示します。</span><span class="sxs-lookup"><span data-stu-id="97a36-125">In the following example this page is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="97a36-126">ボタンが`microsoftTeams.authenticate()`選択されているときに、Microsoft TEAMS クライアント SDK の関数を使用してこのページを起動します。</span><span class="sxs-lookup"><span data-stu-id="97a36-126">Use the `microsoftTeams.authenticate()` function of the Microsoft Teams client SDK to launch this page when your button is selected.</span></span>

```javascript
microsoftTeams.authentication.authenticate({
    url: window.location.origin + "/tab-auth/simple-start",
    width: 600,
    height: 535,
    successCallback: function (result) {
        getUserProfile(result.accessToken);
    },
    failureCallback: function (reason) {
        handleAuthError(reason);
    }
});
```

### <a name="notes"></a><span data-ttu-id="97a36-127">メモ</span><span class="sxs-lookup"><span data-stu-id="97a36-127">Notes</span></span>

* <span data-ttu-id="97a36-128">渡される URL `microsoftTeams.authentication.authenticate()`は、認証フローの開始ページです。</span><span class="sxs-lookup"><span data-stu-id="97a36-128">The URL you pass to `microsoftTeams.authentication.authenticate()` is the start page of the authentication flow.</span></span> <span data-ttu-id="97a36-129">この例では`/tab-auth/simple-start`、です。</span><span class="sxs-lookup"><span data-stu-id="97a36-129">In this example that is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="97a36-130">これは、 [AZURE AD アプリケーション登録ポータル](https://apps.dev.microsoft.com)に登録した内容と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97a36-130">This should match what you registered in the [Azure AD Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

* <span data-ttu-id="97a36-131">認証フローは、ドメイン上のページで開始する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97a36-131">Authentication flow must start on a page that's on your domain.</span></span> <span data-ttu-id="97a36-132">このドメインは、マニフェストの[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)セクションにも記載されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="97a36-132">This domain should also be listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="97a36-133">失敗すると、空のポップアップが発生します。</span><span class="sxs-lookup"><span data-stu-id="97a36-133">Failure to do so will result in an empty pop-up.</span></span>

* <span data-ttu-id="97a36-134">使用`microsoftTeams.authentication.authenticate()`できない場合は、サインインプロセスの終了時にポップアップが閉じられない問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="97a36-134">Failing to use `microsoftTeams.authentication.authenticate()` will cause a problem with the popup not closing at the end of the sign in process.</span></span>

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a><span data-ttu-id="97a36-135">ポップアップページから [認証] ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="97a36-135">Navigate to the authorization page from your popup page</span></span>

<span data-ttu-id="97a36-136">ポップアップページ (`/tab-auth/simple-start`) が表示されると、次のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="97a36-136">When your popup page (`/tab-auth/simple-start`) is displayed the following code is run.</span></span> <span data-ttu-id="97a36-137">このページの主な目的は、ユーザーがサインインできるように、id プロバイダーにリダイレクトすることです。</span><span class="sxs-lookup"><span data-stu-id="97a36-137">The main goal of this page is to redirect to your identity provider so the user can sign in.</span></span> <span data-ttu-id="97a36-138">このリダイレクトは、HTTP 302 を使用してサーバー側で実行でき`window.location.assign()`ますが、この場合は、の呼び出しを使用してクライアント側で行われます。</span><span class="sxs-lookup"><span data-stu-id="97a36-138">This redirection could be done on the server side using HTTP 302, but in this case it is done on the client side using with a call to `window.location.assign()`.</span></span> <span data-ttu-id="97a36-139">これは、 `microsoftTeams.getContext()` Azure AD に渡すことができるヒント情報を取得するためにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="97a36-139">This also allows `microsoftTeams.getContext()` to be used to retrieve hinting information which can be passed to Azure AD.</span></span>

```javascript
microsoftTeams.getContext(function (context) {
    // Generate random state string and store it, so we can verify it in the callback
    let state = _guid(); // _guid() is a helper function in the sample
    localStorage.setItem("simple.state", state);
    localStorage.removeItem("simple.error");
    // Go to the Azure AD authorization endpoint
    let queryParams = {
        client_id: "YOUR_APP_ID_HERE",
        response_type: "id_token token",
        response_mode: "fragment",
        resource: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab-auth/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
         // is used as hinting information
        login_hint: context.loginHint,
    };

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

<span data-ttu-id="97a36-140">ユーザーが認証を完了すると、ユーザーは、アプリで指定されたコールバックページ`/tab-auth/simple-end`にリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="97a36-140">After the user completes authorization, the user is redirected to the callback page you specified for your app at `/tab-auth/simple-end`.</span></span>

### <a name="notes"></a><span data-ttu-id="97a36-141">メモ</span><span class="sxs-lookup"><span data-stu-id="97a36-141">Notes</span></span>

* <span data-ttu-id="97a36-142">認証要求および Url の作成方法については、「 [get user context information](~/tabs/how-to/access-teams-context.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="97a36-142">See [get user context information](~/tabs/how-to/access-teams-context.md) for help building authentication requests and URLs.</span></span> <span data-ttu-id="97a36-143">たとえば、ユーザーのログイン名を Azure AD サインインの`login_hint`値として使用できます。これは、ユーザーがより少ない値を入力する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="97a36-143">For example, you can use the user's login name as the `login_hint` value for Azure AD sign-in, which means the user might need to type less.</span></span> <span data-ttu-id="97a36-144">攻撃者が悪意のあるブラウザーにページを読み込み、必要な情報を提供する可能性があるため、このコンテキストを id の証明として直接使用することはできないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="97a36-144">Remember that you should not use this context directly as proof of identity since an attacker could load your page in a malicious browser and provide it with any information they want.</span></span>
* <span data-ttu-id="97a36-145">Tab コンテキストはユーザーに関して有用な情報を提供しますが、この情報を使用してユーザーがタブのコンテンツ URL への URL パラメーターとして`microsoftTeams.getContext()`取得するか、Microsoft TEAMS クライアント SDK の関数を呼び出すかを認証しません。</span><span class="sxs-lookup"><span data-stu-id="97a36-145">Although the tab context provides useful information regarding the user, don't use this information to authenticate the user whether you get it as URL parameters to your tab content URL or by calling the `microsoftTeams.getContext()` function in the Microsoft Teams client SDK.</span></span> <span data-ttu-id="97a36-146">悪意のあるアクターは、独自のパラメーターを使用してタブコンテンツ URL を呼び出すことができ、Microsoft Teams を偽装している web ページは、タブコンテンツ URL `getContext()`を iframe に読み込み、そのデータを関数に返すことができました。</span><span class="sxs-lookup"><span data-stu-id="97a36-146">A malicious actor could invoke your tab content URL with its own parameters, and a web page impersonating Microsoft Teams could load your tab content URL in an iframe and return its own data to the `getContext()` function.</span></span> <span data-ttu-id="97a36-147">Tab コンテキストの id 関連情報は単にヒントとして扱い、使用する前に検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97a36-147">You should treat the identity-related information in the tab context simply as hints and validate them before use.</span></span>
* <span data-ttu-id="97a36-148">この`state`パラメーターは、コールバック URI を呼び出すサービスが、呼び出したサービスであることを確認するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="97a36-148">The `state` parameter is used to confirm that the service calling the callback URI is the service you called.</span></span> <span data-ttu-id="97a36-149">コールバック`state`内のパラメーターが、呼び出し中に送信したパラメーターと一致しない場合は、戻り呼び出しは検証されず、終了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97a36-149">If the `state` parameter in the callback does not match the parameter you sent during the call the return call is not verified and should be terminated.</span></span>
* <span data-ttu-id="97a36-150">アプリの manifest.xml ファイルの`validDomains`リストに id プロバイダーのドメインを含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="97a36-150">It is not necessary to include the identity provider's domain in the `validDomains` list in the app's manifest.json file.</span></span>

## <a name="the-callback-page"></a><span data-ttu-id="97a36-151">コールバックページ</span><span class="sxs-lookup"><span data-stu-id="97a36-151">The callback page</span></span>

<span data-ttu-id="97a36-152">最後のセクションでは、azure AD authorization service を呼び出して、ユーザーとアプリの情報を渡して、Azure AD がユーザーに独自のモノリシックな認証環境を提供できるようにしました。</span><span class="sxs-lookup"><span data-stu-id="97a36-152">In the last section you called the Azure AD authorization service and passed in user and app information so that Azure AD could present the user with its own monolithic authorization experience.</span></span> <span data-ttu-id="97a36-153">アプリには、この操作での動作を制御する機能はありません。</span><span class="sxs-lookup"><span data-stu-id="97a36-153">Your app has no control over what happens in this experience.</span></span> <span data-ttu-id="97a36-154">提供されたコールバックページが Azure AD によって呼び出されたときに`/tab-auth/simple-end`返されることがわかっています ()。</span><span class="sxs-lookup"><span data-stu-id="97a36-154">All it knows is what is returned when Azure AD calls the  callback page that you provided (`/tab-auth/simple-end`).</span></span>

<span data-ttu-id="97a36-155">このページでは、Azure AD によって返された情報と、または`microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()`の呼び出しに基づいて、成功または失敗を特定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97a36-155">In this page you need to determine success or failure based on the information returned by Azure AD and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()`.</span></span> <span data-ttu-id="97a36-156">ログインに成功すると、サービスリソースにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="97a36-156">If the login was successful you will have access to service resources.</span></span>

````javascript
// Split the key-value pairs passed from Azure AD
// getHashParameters is a helper function that parses the arguments sent
// to the callback URL by Azure AD after the authorization call
let hashParams = getHashParameters();
if (hashParams["error"]) {
    // Authentication/authorization failed
    microsoftTeams.authentication.notifyFailure(hashParams["error"]);
} else if (hashParams["access_token"]) {
    // Get the stored state parameter and compare with incoming state
    // This validates that the data is coming from Azure AD
    let expectedState = localStorage.getItem("simple.state");
    if (expectedState !== hashParams["state"]) {
        // State does not match, report error
        microsoftTeams.authentication.notifyFailure("StateDoesNotMatch");
    } else {
        // Success: return token information to the tab
        microsoftTeams.authentication.notifySuccess({
            idToken: hashParams["id_token"],
            accessToken: hashParams["access_token"],
            tokenType: hashParams["token_type"],
            expiresIn: hashParams["expires_in"]
        })
    }
} else {
    // Unexpected condition: hash does not contain error or access_token parameter
    microsoftTeams.authentication.notifyFailure("UnexpectedFailure");
}
````

<span data-ttu-id="97a36-157">このコードで`window.location.hash`は、 `getHashParameters()`ヘルパー関数を使用して Azure AD から受信したキーと値のペアを解析します。</span><span class="sxs-lookup"><span data-stu-id="97a36-157">This code parses the key-value pairs received from Azure AD in `window.location.hash` using the `getHashParameters()` helper function.</span></span> <span data-ttu-id="97a36-158">が`access_token`で、その`state`値が認証フローの開始時に指定されたものと同じである場合は、呼び出し`notifySuccess()`によってタブへのアクセストークンが返されます。それ以外の場合は、 `notifyFailure()`でエラーが報告されます。</span><span class="sxs-lookup"><span data-stu-id="97a36-158">If it finds an `access_token`, and the `state` value is the same as the one provided at the start of the authentication flow, it returns the access token to the tab by calling `notifySuccess()`; otherwise it reports an error with `notifyFailure()`.</span></span>

### <a name="notes"></a><span data-ttu-id="97a36-159">メモ</span><span class="sxs-lookup"><span data-stu-id="97a36-159">Notes</span></span>

<span data-ttu-id="97a36-160">`NotifyFailure()`には、次のような定義済みエラーの理由があります。</span><span class="sxs-lookup"><span data-stu-id="97a36-160">`NotifyFailure()` has the following predefined failure reasons:</span></span>

* <span data-ttu-id="97a36-161">`CancelledByUser`ユーザーが認証フローを完了する前にポップアップウィンドウを閉じました。</span><span class="sxs-lookup"><span data-stu-id="97a36-161">`CancelledByUser` the user closed the popup window before completing the authentication flow.</span></span>
* <span data-ttu-id="97a36-162">`FailedToOpenWindow`ポップアップウィンドウを開くことができませんでした。</span><span class="sxs-lookup"><span data-stu-id="97a36-162">`FailedToOpenWindow` the popup window could not be opened.</span></span> <span data-ttu-id="97a36-163">ブラウザーで Microsoft Teams を実行している場合、これは通常、ポップアップブロックによってウィンドウがブロックされたことを意味します。</span><span class="sxs-lookup"><span data-stu-id="97a36-163">When running Microsoft Teams in a browser, this typically means that the window was blocked by a popup blocker.</span></span>

<span data-ttu-id="97a36-164">成功した場合は、ページを更新または再読み込みして、現在認証されているユーザーに関連するコンテンツを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="97a36-164">If successful, you can refresh or reload the page and show content relevant to the now-authenticated user.</span></span> <span data-ttu-id="97a36-165">認証が失敗した場合は、エラーメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="97a36-165">If authentication fails, display an error message.</span></span>

<span data-ttu-id="97a36-166">アプリは、自分のセッション cookie を設定して、ユーザーが現在のデバイスのタブに戻ったときにもう一度サインインしないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="97a36-166">Your app can set its own session cookie so that the user need not sign in again when they return to your tab on the current device.</span></span>

> [!NOTE]
> <span data-ttu-id="97a36-167">Chrome 80 (初期2020でリリースが予定されています)。新しい cookie 値を紹介し、既定で cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="97a36-167">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="97a36-168">既定のブラウザーの動作に依存するのではなく、cookie に対して使用する目的を設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="97a36-168">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="97a36-169">[SameSite cookie 属性 (2020 update)](../../../resources/samesite-cookie-update.md)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="97a36-169">*See* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md).</span></span>

<span data-ttu-id="97a36-170">シングルサインオン (SSO) の詳細については、「[サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="97a36-170">For more information on Single Sign-On (SSO) see the article [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span></span>

## <a name="samples"></a><span data-ttu-id="97a36-171">サンプル</span><span class="sxs-lookup"><span data-stu-id="97a36-171">Samples</span></span>

<span data-ttu-id="97a36-172">Azure AD を使用したタブ認証プロセスを示すサンプルコードについては、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="97a36-172">For sample code showing the tab authentication process using Azure AD see:</span></span>

* [<span data-ttu-id="97a36-173">Microsoft Teams タブ認証のサンプル (ノード)</span><span class="sxs-lookup"><span data-stu-id="97a36-173">Microsoft Teams tab authentication sample (Node)</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
