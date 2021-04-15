---
title: Teams での Azure Bot Service の認証の使用
description: Azure Bot Service OAuthCard と、それが認証に使用される方法について説明します。
ms.topic: conceptual
keywords: teams 認証 OAuthCard OAuth カード Azure Bot Service
ms.openlocfilehash: 6e609daba1374f4e971e1634810d3b217ce55371
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696676"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="ed86d-104">Teams での Azure Bot Service の認証の使用</span><span class="sxs-lookup"><span data-stu-id="ed86d-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="ed86d-105">Azure Bot Service の OAuthCard がない場合、ボットに認証を実装する方法は複雑です。</span><span class="sxs-lookup"><span data-stu-id="ed86d-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="ed86d-106">Web エクスペリエンスの構築、外部 OAuth プロバイダーとの統合、トークン管理、および認証フローを安全に完了するための適切なサーバー間 API 呼び出しの処理が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="ed86d-107">これにより、"マジック ナンバー" の入力が必要な不格好なエクスペリエンスが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="ed86d-108">Azure Bot Service の OAuthCard を使用すると、Teams ボットがユーザーにサインインし、外部データ プロバイダーにアクセスしやすくなります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="ed86d-109">既に認証を実装済みで、より簡単なものに切り替える場合も、ボット サービスに初めて認証を追加する場合でも、OAuthCard を使用すると、簡単に行えます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="ed86d-110">[認証][](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)の他のトピックでは、OAuthCard を使用せずに認証を記述します。そのため、Teams での認証を深く理解する場合や、OAuthCard を使用できない状況がある場合は、引き続きこれらのトピックを参照できます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="ed86d-111">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="ed86d-111">Support for the OAuthCard</span></span>

<span data-ttu-id="ed86d-112">現在、OAuthCard を使用できる場所にはいくつかの制限があります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="ed86d-113">これには、次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-113">These include:</span></span>

* <span data-ttu-id="ed86d-114">カードはゲスト アクセスでは [機能しません](/MicrosoftTeams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="ed86d-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="ed86d-115">Microsoft Teams 無料では [動作しません](https://products.office.com/microsoft-teams/free)</span><span class="sxs-lookup"><span data-stu-id="ed86d-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="ed86d-116">ボット認証にのみ使用できます</span><span class="sxs-lookup"><span data-stu-id="ed86d-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="ed86d-117">Azure Bot Service に登録されているボットでのみ [機能します。](https://azure.microsoft.com/services/bot-service/)</span><span class="sxs-lookup"><span data-stu-id="ed86d-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="ed86d-118">Azure Bot Service は認証を行う上でどのように役立ちますか?</span><span class="sxs-lookup"><span data-stu-id="ed86d-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="ed86d-119">OAuthCard を使用した完全なドキュメントについては、「Azure Bot Service 経由でボットに認証を追加する [」を参照してください](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="ed86d-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="ed86d-120">このトピックは Azure Bot Framework のドキュメント セットに含まれていますが、Teams に固有のトピックではありません。</span><span class="sxs-lookup"><span data-stu-id="ed86d-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="ed86d-121">次のセクションでは、Teams で OAuthCard を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ed86d-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="ed86d-122">Teams 開発者の主な利点</span><span class="sxs-lookup"><span data-stu-id="ed86d-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="ed86d-123">OAuthCard は、次の方法で認証に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="ed86d-124">アウトオブボックスの Web ベース認証フローを提供します。外部ログイン エクスペリエンスに移動したり、リダイレクトを提供したりするために、Web ページを作成してホストする必要がなくなりました。</span><span class="sxs-lookup"><span data-stu-id="ed86d-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="ed86d-125">エンド ユーザーはシームレスです。Teams 内で完全なサインイン エクスペリエンスを完了します。</span><span class="sxs-lookup"><span data-stu-id="ed86d-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="ed86d-126">簡単なトークン管理が含まれています。トークン ストレージ システムを実装する必要がなくなりました。代わりに、Bot Service はトークンキャッシュを処理し、これらのトークンをフェッチするための安全なメカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="ed86d-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="ed86d-127">完全な SDK でサポートされています。ボット サービスから簡単に統合して使用できます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="ed86d-128">Azure AD/MSA、Facebook、Google など、多くの一般的な OAuth プロバイダーをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ed86d-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="ed86d-129">自分のソリューションをいつ実装する必要がありますか?</span><span class="sxs-lookup"><span data-stu-id="ed86d-129">When should I implement my own solution?</span></span>

<span data-ttu-id="ed86d-130">アクセス トークンは機密情報であるため、外部サービスに保存する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="ed86d-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="ed86d-131">この場合も、Teams 認証の他のトピックで説明するように、独自のトークン管理システムとログイン エクスペリエンスを [Teams](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) 内に実装することができます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="ed86d-132">Teams での OAuthCard の使用を開始する</span><span class="sxs-lookup"><span data-stu-id="ed86d-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="ed86d-133">このガイドでは、Bot Framework v3 SDK を使用しています。</span><span class="sxs-lookup"><span data-stu-id="ed86d-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="ed86d-134">v4 実装は、こちらを参照 [してください](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="ed86d-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span> <span data-ttu-id="ed86d-135">それ以外の場合は [サインイン] ボタンが認証ウィンドウを開かないので、マニフェストを作成し、セクションに token.botframework.com を含める `validDomains` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="ed86d-136">App [Studio を使用して](~/concepts/build-and-test/app-studio-overview.md) マニフェストを生成します。</span><span class="sxs-lookup"><span data-stu-id="ed86d-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="ed86d-137">まず、外部認証プロバイダーをセットアップするように Azure ボット サービスを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="ed86d-138">詳細な [手順については、「ID プロバイダーの構成](~/concepts/authentication/configure-identity-provider.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed86d-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="ed86d-139">Azure Bot Service を使用して認証を有効にするには、コードに次の追加を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="ed86d-140">Teams token.botframework.com ボット サービスのログイン ページが埋め込まれるため、アプリ マニフェストのセクションにアプリ マニフェストを `validDomains` 含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="ed86d-141">ボットが認証されたリソースにアクセスする必要がある場合は常に、ボット サービスからトークンをフェッチします。</span><span class="sxs-lookup"><span data-stu-id="ed86d-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="ed86d-142">トークンが使用できない場合は、OAuthCard を含むメッセージを外部サービスへのログインを要求するユーザーに送信します。</span><span class="sxs-lookup"><span data-stu-id="ed86d-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="ed86d-143">ログイン完了アクティビティを処理します。</span><span class="sxs-lookup"><span data-stu-id="ed86d-143">Handle the login completion activity.</span></span> <span data-ttu-id="ed86d-144">これにより、認証要求とトークンがボットと現在対話しているユーザーに関連付けられる。</span><span class="sxs-lookup"><span data-stu-id="ed86d-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="ed86d-145">外部 REST API の呼び出しなど、ボットが認証されたアクションを実行する必要がある場合は常にトークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="ed86d-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="ed86d-146">ダイアログ コードで、次のスニペット (C#) を追加する必要があります。これは、既存のアクセス トークンをチェックします。</span><span class="sxs-lookup"><span data-stu-id="ed86d-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

```CSharp
// First ask Bot Service if it already has a token for this user
var token = await context.GetUserTokenAsync(ConnectionName).ConfigureAwait(false);
if (token != null)
{
    // use the token to do exciting things!
}
else
{
    // If Bot Service does not have a token, send an OAuth card to sign in 
    await SendOAuthCardAsync(context, (Activity)context.Activity);
}
```

<span data-ttu-id="ed86d-147">アクセス トークンが存在しない場合、コードは OAuthCard を含むメッセージをユーザーに送信します。</span><span class="sxs-lookup"><span data-stu-id="ed86d-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="ed86d-148">ログイン完了アクティビティを処理するには、この Invoke を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

```CSharp
if (activity.Name == "signin/verifyState")
{
  // We do this so that we can pass handling to the right logic in the dialog. You can
  // set this to be whatever string you want.
  activity.Text = "loginComplete";
  await Conversation.SendAsync(activity, () => new Dialogs.RootDialog());

  return Request.CreateResponse(HttpStatusCode.OK);
}
```

<span data-ttu-id="ed86d-149">ダイアログ コードで、ボット認証サービスからトークンを取得できます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

```CSharp
if (text.Contains("loginComplete"))
  {
    // Handle login completion event.
    JObject ctx = activity.Value as JObject;

    if (ctx != null)
    {
      string code = ctx["state"].ToString();

      var oauthClient = activity.GetOAuthClient();
      var token = await oauthClient.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, magicCode: code).ConfigureAwait(false);
      if (token != null)
      {
        // Make whatever API calls here you want
        await context.PostAsync($"Success! You are now signed in.");
      }
    }
  // Need to respond to the Invoke.
  return;
}
```

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="ed86d-150">メッセージング拡張機能での OAuthCard の使用</span><span class="sxs-lookup"><span data-stu-id="ed86d-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="ed86d-151">Azure Bot Service を使用して、サードパーティ プロバイダーをメッセージング拡張機能に接続することもできます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="ed86d-152">フローはボットと同じですが、OAuthCard を返す代わりに、サービスはログイン プロンプトを返します。</span><span class="sxs-lookup"><span data-stu-id="ed86d-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="ed86d-153">次のスニペット (C#) は、ログイン応答を作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="ed86d-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

```CSharp
var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName).ConfigureAwait(false);

if (token == null)
{
  // Send the login response with the auth link.
  string link = await client.OAuthApi.GetSignInLinkAsync(activity, ConnectionName);

  response = new ComposeExtensionResponse()
  {
    ComposeExtension = new ComposeExtensionResult()
  };
  response.ComposeExtension.Type = "auth";
  response.ComposeExtension.SuggestedActions = new ComposeExtensionSuggestedAction()
  {
    Actions = new List<CardAction>()
      {
        new CardAction(ActionTypes.OpenUrl, title: "Sign into this app", value: link)
      }
    };
  return response;
}
```

<span data-ttu-id="ed86d-154">上記の例では、プロパティに対して直接呼び出し `GetSignInLinkAsync` を行う必要 `client.OAuthApi` があります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="ed86d-155">ユーザーがログイン シーケンスを正常に完了すると、サービスは元のユーザー クエリを含む別の Invoke 要求と、"マジック コード" を含む状態パラメーター文字列を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="ed86d-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="ed86d-156">これで、ユーザー ID と接続名と共に、この文字列を使用してトークンをフェッチできます。</span><span class="sxs-lookup"><span data-stu-id="ed86d-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

```CSharp
var query = activity.GetComposeExtensionQueryData();
JObject data = activity.Value as JObject;

var client = activity.GetOAuthClient();

// Check if the request comes with login state
if (data != null && data["state"] != null)
{
  var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, data["state"].ToString());

  // Do stuff with the token here.

}
```
