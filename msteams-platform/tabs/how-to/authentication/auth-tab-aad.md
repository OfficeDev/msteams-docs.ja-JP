---
title: Azure Active Directory を使用したタブの認証
description: Teams での認証とタブでの認証の使い方について説明します。
keywords: Teams 認証タブ AAD
ms.openlocfilehash: f6df2dbf84583488ddc0c57798d423b6288af16d
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777932"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a><span data-ttu-id="5ca99-104">Microsoft Teams タブでユーザーを認証する</span><span class="sxs-lookup"><span data-stu-id="5ca99-104">Authenticate a user in a Microsoft Teams tab</span></span>

> [!Note]
> <span data-ttu-id="5ca99-105">モバイル クライアントのタブで認証を機能するには、Teams JavaScript SDK のバージョン 1.4.1 以降を使用している必要があります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-105">For authentication to work for your tab on mobile clients, you need to ensure you're using version 1.4.1 or later of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="5ca99-106">Teams アプリ内で使用するサービスは多数あるので、それらのサービスのほとんどで、サービスにアクセスするには認証と承認が必要です。</span><span class="sxs-lookup"><span data-stu-id="5ca99-106">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="5ca99-107">サービスには、Facebook、Twitter、もちろん Teams が含まれます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-107">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="5ca99-108">Teams のユーザーは、Microsoft Graph を使用して Azure Active Directory (Azure AD) に保存されているユーザー プロファイル情報を持っています。この記事では、Azure AD を使用してこの情報にアクセスする認証に重点を置きます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-108">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph and this article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="5ca99-109">OAuth 2.0 は、Azure AD他の多くのサービス プロバイダーで使用される認証のオープン標準です。</span><span class="sxs-lookup"><span data-stu-id="5ca99-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="5ca99-110">OAuth 2.0 について理解するには、Teams および Azure AD で認証を操作する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="5ca99-111">次の例では、OAuth 2.0 の暗黙的な付与フローを使用して、最終的に Azure AD および Microsoft Graph からユーザーのプロファイル情報を読み取るという目標を達成しています。</span><span class="sxs-lookup"><span data-stu-id="5ca99-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="5ca99-112">この記事のコードは、Teams サンプル アプリ [の Microsoft Teams タブ認証サンプル (ノード) から提供されています](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)。</span><span class="sxs-lookup"><span data-stu-id="5ca99-112">The code in this article comes from the Teams sample app [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span> <span data-ttu-id="5ca99-113">Microsoft Graph のアクセス トークンを要求し、Azure Graph から現在のユーザーの基本的なプロファイル情報を表示する静的タブAD。</span><span class="sxs-lookup"><span data-stu-id="5ca99-113">It contains a static tab that requests an access token for Microsoft Graph and shows the current user's basic profile information from Azure AD.</span></span>

<span data-ttu-id="5ca99-114">タブの認証フローの概要については、タブの「認証フロー」 [を参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="5ca99-114">For a general overview of authentication flow for tabs see the topic [Authentication flow in tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="5ca99-115">タブの認証フローは、ボットの認証フローとは若干異なります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-115">Authentication flow in tabs differs slightly from authentication flow in bots.</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="5ca99-116">ID プロバイダーの構成</span><span class="sxs-lookup"><span data-stu-id="5ca99-116">Configuring identity providers</span></span>

<span data-ttu-id="5ca99-117">Azure Active Directory を [ID](~/concepts/authentication/configure-identity-provider.md) プロバイダーとして使用する場合の OAuth 2.0 コールバック リダイレクト URL の構成に関する詳細な手順については、「ID プロバイダーを構成する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5ca99-117">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="5ca99-118">認証フローを開始する</span><span class="sxs-lookup"><span data-stu-id="5ca99-118">Initiate authentication flow</span></span>

<span data-ttu-id="5ca99-119">認証フローは、ユーザーの操作によってトリガーされる必要があります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-119">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="5ca99-120">認証ポップアップは、ブラウザーのポップアップ ブロックをトリガーし、ユーザーを混乱させる可能性が高いので、自動的に開かれません。</span><span class="sxs-lookup"><span data-stu-id="5ca99-120">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

<span data-ttu-id="5ca99-121">必要に応じてユーザーがサインインできるボタンを構成ページまたはコンテンツ ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="5ca99-121">Add a button to your configuration or content page to enable the user to sign in when needed.</span></span> <span data-ttu-id="5ca99-122">これは、タブ構成ページまたは [任意のコンテンツ](~/tabs/how-to/create-tab-pages/configuration-page.md) ページで [行](~/tabs/how-to/create-tab-pages/content-page.md) えます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-122">This can be done in the tab [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) page or any [content](~/tabs/how-to/create-tab-pages/content-page.md) page.</span></span>

<span data-ttu-id="5ca99-123">Azure AD、ほとんどの ID プロバイダーと同様に、そのコンテンツを iframe に配置する機能は許可されています。</span><span class="sxs-lookup"><span data-stu-id="5ca99-123">Azure AD, like most identity providers, does not allow its content to be placed in an iframe.</span></span> <span data-ttu-id="5ca99-124">つまり、ID プロバイダーをホストするためにポップアップ ページを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-124">This means that you will need to add a pop-up page to host the identity provider.</span></span> <span data-ttu-id="5ca99-125">次の例では、このページは `/tab-auth/simple-start` 次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5ca99-125">In the following example this page is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="5ca99-126">Microsoft `microsoftTeams.authenticate()` Teams クライアント SDK の機能を使用して、ボタンが選択されているときにこのページを起動します。</span><span class="sxs-lookup"><span data-stu-id="5ca99-126">Use the `microsoftTeams.authenticate()` function of the Microsoft Teams client SDK to launch this page when your button is selected.</span></span>

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

### <a name="notes"></a><span data-ttu-id="5ca99-127">Notes</span><span class="sxs-lookup"><span data-stu-id="5ca99-127">Notes</span></span>

* <span data-ttu-id="5ca99-128">渡す URL `microsoftTeams.authentication.authenticate()` は、認証フローの開始ページです。</span><span class="sxs-lookup"><span data-stu-id="5ca99-128">The URL you pass to `microsoftTeams.authentication.authenticate()` is the start page of the authentication flow.</span></span> <span data-ttu-id="5ca99-129">この例では、 `/tab-auth/simple-start` .</span><span class="sxs-lookup"><span data-stu-id="5ca99-129">In this example that is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="5ca99-130">これは、Azure AD [アプリケーション登録ポータルに登録したデータと一致する必要があります](https://apps.dev.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="5ca99-130">This should match what you registered in the [Azure AD Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

* <span data-ttu-id="5ca99-131">認証フローは、ドメイン上のページから開始する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-131">Authentication flow must start on a page that's on your domain.</span></span> <span data-ttu-id="5ca99-132">このドメインは、マニフェストのセクション [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) にも一覧表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-132">This domain should also be listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="5ca99-133">そうしない場合は、空のポップアップが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-133">Failure to do so will result in an empty pop-up.</span></span>

* <span data-ttu-id="5ca99-134">使用に失敗すると、サインイン プロセスの最後にポップアップが閉じない問題 `microsoftTeams.authentication.authenticate()` が発生します。</span><span class="sxs-lookup"><span data-stu-id="5ca99-134">Failing to use `microsoftTeams.authentication.authenticate()` will cause a problem with the popup not closing at the end of the sign in process.</span></span>

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a><span data-ttu-id="5ca99-135">ポップアップ ページから承認ページに移動する</span><span class="sxs-lookup"><span data-stu-id="5ca99-135">Navigate to the authorization page from your popup page</span></span>

<span data-ttu-id="5ca99-136">ポップアップ ページ ( ) が表示 `/tab-auth/simple-start` される場合は、次のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-136">When your popup page (`/tab-auth/simple-start`) is displayed the following code is run.</span></span> <span data-ttu-id="5ca99-137">このページの主な目的は、ユーザーがサインインできるよう ID プロバイダーにリダイレクトする方法です。</span><span class="sxs-lookup"><span data-stu-id="5ca99-137">The main goal of this page is to redirect to your identity provider so the user can sign in.</span></span> <span data-ttu-id="5ca99-138">このリダイレクトは、HTTP 302 を使用してサーバー側で実行できますが、この場合は、クライアント側で呼び出しを使用して行われます `window.location.assign()` 。</span><span class="sxs-lookup"><span data-stu-id="5ca99-138">This redirection could be done on the server side using HTTP 302, but in this case it is done on the client side using with a call to `window.location.assign()`.</span></span> <span data-ttu-id="5ca99-139">これにより、Azure アプリに渡されるヒント情報を取得 `microsoftTeams.getContext()` AD。</span><span class="sxs-lookup"><span data-stu-id="5ca99-139">This also allows `microsoftTeams.getContext()` to be used to retrieve hinting information which can be passed to Azure AD.</span></span>

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
        scope: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab-auth/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
         // is used as hinting information
        login_hint: context.loginHint,
    };

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/v2.0/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

<span data-ttu-id="5ca99-140">ユーザーが承認を完了すると、ユーザーはアプリに対して指定したコールバック ページにリダイレクトされます `/tab-auth/simple-end` 。</span><span class="sxs-lookup"><span data-stu-id="5ca99-140">After the user completes authorization, the user is redirected to the callback page you specified for your app at `/tab-auth/simple-end`.</span></span>

### <a name="notes"></a><span data-ttu-id="5ca99-141">Notes</span><span class="sxs-lookup"><span data-stu-id="5ca99-141">Notes</span></span>

* <span data-ttu-id="5ca99-142">認証 [要求と URL の構築に](~/tabs/how-to/access-teams-context.md) 関するヘルプについては、ユーザー コンテキスト情報の取得に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5ca99-142">See [get user context information](~/tabs/how-to/access-teams-context.md) for help building authentication requests and URLs.</span></span> <span data-ttu-id="5ca99-143">たとえば、Azure AD サインインの値としてユーザーのログイン名を使用できます。これは、ユーザーが入力する必要が少ない可能性があることを `login_hint` 意味します。</span><span class="sxs-lookup"><span data-stu-id="5ca99-143">For example, you can use the user's login name as the `login_hint` value for Azure AD sign-in, which means the user might need to type less.</span></span> <span data-ttu-id="5ca99-144">攻撃者が悪意のあるブラウザーにページを読み込み、必要な情報をページに提供する可能性があります。そのため、このコンテキストを ID の証明として直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="5ca99-144">Remember that you should not use this context directly as proof of identity since an attacker could load your page in a malicious browser and provide it with any information they want.</span></span>
* <span data-ttu-id="5ca99-145">タブ コンテキストはユーザーに関する有用な情報を提供しますが、タブ コンテンツの URL への URL パラメーターとして取得するか、Microsoft Teams クライアント SDK の関数を呼び出す場合でも、この情報を使用してユーザーを認証しません。 `microsoftTeams.getContext()`</span><span class="sxs-lookup"><span data-stu-id="5ca99-145">Although the tab context provides useful information regarding the user, don't use this information to authenticate the user whether you get it as URL parameters to your tab content URL or by calling the `microsoftTeams.getContext()` function in the Microsoft Teams client SDK.</span></span> <span data-ttu-id="5ca99-146">悪意のあるアクターが独自のパラメーターを使用してタブ コンテンツの URL を呼び出す可能性があります。また、Microsoft Teams を偽装する Web ページが iframe にタブ コンテンツ URL を読み込み、独自のデータを関数に返す可能性があります。 `getContext()`</span><span class="sxs-lookup"><span data-stu-id="5ca99-146">A malicious actor could invoke your tab content URL with its own parameters, and a web page impersonating Microsoft Teams could load your tab content URL in an iframe and return its own data to the `getContext()` function.</span></span> <span data-ttu-id="5ca99-147">タブ コンテキストでは、ID 関連の情報をヒントとして扱い、使用する前に検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-147">You should treat the identity-related information in the tab context simply as hints and validate them before use.</span></span>
* <span data-ttu-id="5ca99-148">この `state` パラメーターは、コールバック URI を呼び出すサービスが呼び出したサービスを確認するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-148">The `state` parameter is used to confirm that the service calling the callback URI is the service you called.</span></span> <span data-ttu-id="5ca99-149">コールバックのパラメーターが呼び出し中に送信したパラメーターと一致しない場合、戻り値の呼び出しは検証されないので、 `state` 終了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-149">If the `state` parameter in the callback does not match the parameter you sent during the call the return call is not verified and should be terminated.</span></span>
* <span data-ttu-id="5ca99-150">ID プロバイダーのドメインをアプリの on ファイルの一覧に含 `validDomains` manifest.js必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5ca99-150">It is not necessary to include the identity provider's domain in the `validDomains` list in the app's manifest.json file.</span></span>

## <a name="the-callback-page"></a><span data-ttu-id="5ca99-151">コールバック ページ</span><span class="sxs-lookup"><span data-stu-id="5ca99-151">The callback page</span></span>

<span data-ttu-id="5ca99-152">最後のセクションでは、Azure AD 認証サービスを呼び出し、Azure AD が独自のモノリシックな承認エクスペリエンスをユーザーに提供できるよう、ユーザーとアプリの情報を渡しました。</span><span class="sxs-lookup"><span data-stu-id="5ca99-152">In the last section you called the Azure AD authorization service and passed in user and app information so that Azure AD could present the user with its own monolithic authorization experience.</span></span> <span data-ttu-id="5ca99-153">アプリは、このエクスペリエンスで何が起こるかを制御する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5ca99-153">Your app has no control over what happens in this experience.</span></span> <span data-ttu-id="5ca99-154">Azure ADが指定したコールバック ページ () を呼び出す場合に返されるのは、そのことを知っているだけです `/tab-auth/simple-end` 。</span><span class="sxs-lookup"><span data-stu-id="5ca99-154">All it knows is what is returned when Azure AD calls the  callback page that you provided (`/tab-auth/simple-end`).</span></span>

<span data-ttu-id="5ca99-155">このページでは、Azure が返す情報に基づいて、成功または失敗を判断する必要があります。AD呼び出し `microsoftTeams.authentication.notifySuccess()` または `microsoftTeams.authentication.notifyFailure()` .</span><span class="sxs-lookup"><span data-stu-id="5ca99-155">In this page you need to determine success or failure based on the information returned by Azure AD and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()`.</span></span> <span data-ttu-id="5ca99-156">ログインが成功した場合は、サービス リソースにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-156">If the login was successful you will have access to service resources.</span></span>

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

<span data-ttu-id="5ca99-157">このコードは、ヘルパー関数を使用して Azure ADキーと値のペア `window.location.hash` を `getHashParameters()` 解析します。</span><span class="sxs-lookup"><span data-stu-id="5ca99-157">This code parses the key-value pairs received from Azure AD in `window.location.hash` using the `getHashParameters()` helper function.</span></span> <span data-ttu-id="5ca99-158">認証フローの開始時点で指定した値と同じ値が見つからなければ、アクセス トークンを呼び出してタブに返します。それ以外の場合は、エラーを報告 `access_token` `state` `notifySuccess()` します `notifyFailure()` 。</span><span class="sxs-lookup"><span data-stu-id="5ca99-158">If it finds an `access_token`, and the `state` value is the same as the one provided at the start of the authentication flow, it returns the access token to the tab by calling `notifySuccess()`; otherwise it reports an error with `notifyFailure()`.</span></span>

### <a name="notes"></a><span data-ttu-id="5ca99-159">Notes</span><span class="sxs-lookup"><span data-stu-id="5ca99-159">Notes</span></span>

<span data-ttu-id="5ca99-160">`NotifyFailure()` には、次の定義済みのエラーの理由があります。</span><span class="sxs-lookup"><span data-stu-id="5ca99-160">`NotifyFailure()` has the following predefined failure reasons:</span></span>

* <span data-ttu-id="5ca99-161">`CancelledByUser` ユーザーが認証フローを完了する前にポップアップ ウィンドウを閉じた。</span><span class="sxs-lookup"><span data-stu-id="5ca99-161">`CancelledByUser` the user closed the popup window before completing the authentication flow.</span></span>
* <span data-ttu-id="5ca99-162">`FailedToOpenWindow` ポップアップ ウィンドウを開く必要がありました。</span><span class="sxs-lookup"><span data-stu-id="5ca99-162">`FailedToOpenWindow` the popup window could not be opened.</span></span> <span data-ttu-id="5ca99-163">ブラウザーで Microsoft Teams を実行する場合、これは通常、ウィンドウがポップアップ ブロックによってブロックされた状態を意味します。</span><span class="sxs-lookup"><span data-stu-id="5ca99-163">When running Microsoft Teams in a browser, this typically means that the window was blocked by a popup blocker.</span></span>

<span data-ttu-id="5ca99-164">成功した場合は、ページを更新または再読み込みし、現在認証されたユーザーに関連するコンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-164">If successful, you can refresh or reload the page and show content relevant to the now-authenticated user.</span></span> <span data-ttu-id="5ca99-165">認証に失敗した場合は、エラー メッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="5ca99-165">If authentication fails, display an error message.</span></span>

<span data-ttu-id="5ca99-166">アプリでは、ユーザーが現在のデバイスのタブに戻る際にもう一度サインインする必要が生じないので、独自のセッション Cookie を設定できます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-166">Your app can set its own session cookie so that the user need not sign in again when they return to your tab on the current device.</span></span>

> [!NOTE]
> <span data-ttu-id="5ca99-167">Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="5ca99-167">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="5ca99-168">既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5ca99-168">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="5ca99-169">「[SameSite Cookie 属性 (2020 更新プログラム)](../../../resources/samesite-cookie-update.md)」を *参照してください*。</span><span class="sxs-lookup"><span data-stu-id="5ca99-169">*See* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md).</span></span>

>[!NOTE]
><span data-ttu-id="5ca99-170">Microsoft Teams 無料ユーザーとゲスト ユーザーの適切なトークンを取得するには、アプリでテナント固有のエンドポイント https://login.microsoftonline.com/ **{tenantId} を使用することが重要です**。</span><span class="sxs-lookup"><span data-stu-id="5ca99-170">To get the correct token for Microsoft Teams Free and guest users, it is important that the apps use tenant specific endpoint https://login.microsoftonline.com/**{tenantId}**.</span></span> <span data-ttu-id="5ca99-171">bot メッセージまたはタブ コンテキストから tenantId を取得できます。</span><span class="sxs-lookup"><span data-stu-id="5ca99-171">You can get tenantId from the bot message or tab context.</span></span> <span data-ttu-id="5ca99-172">アプリが使用されている場合、ユーザーは正しくないトークンを取得し、現在サインインしているテナントではなく https://login.microsoftonline.com/common 、"ホーム" テナントにログオンします。</span><span class="sxs-lookup"><span data-stu-id="5ca99-172">If the apps use https://login.microsoftonline.com/common, the users will get incorrect tokens and will log on to the "home" tenant instead of the tenant that they are currently signed into.</span></span>

<span data-ttu-id="5ca99-173">シングル 認証 (SSO) の詳細Sign-Onサイレント認証の記事 [を参照してください](~/tabs/how-to/authentication/auth-silent-AAD.md)。</span><span class="sxs-lookup"><span data-stu-id="5ca99-173">For more information on Single Sign-On (SSO) see the article [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span></span>

## <a name="samples"></a><span data-ttu-id="5ca99-174">サンプル</span><span class="sxs-lookup"><span data-stu-id="5ca99-174">Samples</span></span>

<span data-ttu-id="5ca99-175">Azure 認証を使用したタブ認証プロセスを示すサンプル コードAD参照してください。</span><span class="sxs-lookup"><span data-stu-id="5ca99-175">For sample code showing the tab authentication process using Azure AD see:</span></span>

* [<span data-ttu-id="5ca99-176">Microsoft Teams タブ認証のサンプル (ノード)</span><span class="sxs-lookup"><span data-stu-id="5ca99-176">Microsoft Teams tab authentication sample (Node)</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
