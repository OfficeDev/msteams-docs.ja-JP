---
title: Teams での認証に Azure Bot サービスを使用する
description: Azure ボット Service OAuthCard について、および認証にどのように使用するかについて説明します。
keywords: teams 認証 OAuthCard OAuth card Azure Bot サービス
ms.openlocfilehash: 0397c45b39470d97c1158b2681462038de618a39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674931"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="dfe4d-104">Teams での認証に Azure Bot サービスを使用する</span><span class="sxs-lookup"><span data-stu-id="dfe4d-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="dfe4d-105">Azure Bot サービスの OAuthCard を使用していない場合は、ボットに認証を実装するのは複雑です。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="dfe4d-106">これは、web 環境の構築、外部 OAuth プロバイダーとの統合、トークン管理、および適切なサーバー間 API 呼び出しを処理して認証フローを安全に完了することを含む、完全なスタックの課題です。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="dfe4d-107">これにより、clunky エクスペリエンスで "magic numbers" の入力が必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="dfe4d-108">Azure Bot サービスの OAuthCard を使用すると、Teams でユーザーにサインインして外部データプロバイダーにアクセスすることが容易になります。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="dfe4d-109">既に認証を実装していて、より単純なものに切り替える必要がある場合、または初めて bot サービスに認証を追加する場合は、OAuthCard を使用すると簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="dfe4d-110">[認証](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)の他のトピックでは、oauthcard を使用しない認証について説明しているため、Teams での認証をより深く理解したい場合や、oauthcard を使用できないような状況がある場合は、これらのトピックを参照することもできます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="dfe4d-111">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="dfe4d-111">Support for the OAuthCard</span></span>

<span data-ttu-id="dfe4d-112">現時点では、OAuthCard の使用にはいくつかの制限があります。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="dfe4d-113">これには、次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-113">These include:</span></span>

* <span data-ttu-id="dfe4d-114">カードは[ゲストアクセス](/MicrosoftTeams/guest-access)では機能しません</span><span class="sxs-lookup"><span data-stu-id="dfe4d-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="dfe4d-115">[Microsoft Teams の無料](https://products.office.com/microsoft-teams/free)では機能しません</span><span class="sxs-lookup"><span data-stu-id="dfe4d-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="dfe4d-116">Bot 認証にのみ使用できます</span><span class="sxs-lookup"><span data-stu-id="dfe4d-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="dfe4d-117">[Azure Bot サービス](https://azure.microsoft.com/services/bot-service/)に登録されている bot に対してのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="dfe4d-118">Azure Bot サービスはどのように認証を行いますか?</span><span class="sxs-lookup"><span data-stu-id="dfe4d-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="dfe4d-119">OAuthCard を使用した完全なドキュメントについては、「 [Azure Bot サービスによる bot への認証の追加](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="dfe4d-120">このトピックは Azure Bot フレームワークドキュメントセットに含まれており、Teams に固有ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="dfe4d-121">次のセクションでは、Teams での OAuthCard の使用方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="dfe4d-122">Teams 開発者の主な利点</span><span class="sxs-lookup"><span data-stu-id="dfe4d-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="dfe4d-123">OAuthCard は、以下の方法で認証に役立てることができます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="dfe4d-124">すぐに使用できる web ベースの認証フローを提供します。 web ページを作成してホストして、外部ログインのエクスペリエンスに直接アクセスしたり、リダイレクトを提供したりする必要がなくなりました。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="dfe4d-125">エンドユーザーにとってシームレスである: Teams 内の完全なサインイン機能を完全に完了します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="dfe4d-126">簡単なトークン管理が含まれています。トークンストレージシステムを実装する必要がなくなりました。その代わりに、ボットサービスはトークンのキャッシュを処理し、それらのトークンをフェッチするための安全なメカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="dfe4d-127">は、完全な Sdk でサポートされています。ボットサービスの統合と使用が容易です。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="dfe4d-128">Azure AD/MSA、Facebook、Google などの一般的な OAuth プロバイダーに対して、すぐにサポートが提供されます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="dfe4d-129">どのような場合に独自のソリューションを実装する必要がありますか。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-129">When should I implement my own solution?</span></span>

<span data-ttu-id="dfe4d-130">アクセストークンは機密情報なので、外部サービスに格納したくない場合があります。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="dfe4d-131">この場合は、teams の[認証](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)に関する他のトピックで説明されているように、チーム内で独自のトークン管理システムとログインの処理を実装してもかまいません。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="dfe4d-132">Teams での OAuthCard の概要</span><span class="sxs-lookup"><span data-stu-id="dfe4d-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="dfe4d-133">このガイドでは、Bot Framework v3 SDK を使用しています。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="dfe4d-134">V4 の実装については、[こちら](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp).</span></span> <span data-ttu-id="dfe4d-135">それ以外の場合は、[サインイン] ボタンをクリックし`validDomains`ても認証ウィンドウが表示されないため、マニフェストを作成して token.botframework.com をセクションに含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="dfe4d-136">[アプリ Studio](~/concepts/build-and-test/app-studio-overview.md)を使用して、マニフェストを生成します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="dfe4d-137">最初に、外部認証プロバイダをセットアップするために Azure bot サービスを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="dfe4d-138">詳細な手順については、「 [id プロバイダーの構成](~/concepts/authentication/configure-identity-provider.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="dfe4d-139">Azure Bot サービスを使用して認証を有効にするには、コードにこれらを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="dfe4d-140">Teams が Bot サービス`validDomains`のログインページを埋め込むため、アプリマニフェストのセクションに token.botframework.com を含めます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="dfe4d-141">Bot が認証済みリソースにアクセスする必要がある場合は、ボットサービスからトークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="dfe4d-142">トークンを使用できない場合は、外部サービスへのログインを要求しているユーザーに OAuthCard というメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="dfe4d-143">ログイン完了アクティビティを処理します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-143">Handle the login completion activity.</span></span> <span data-ttu-id="dfe4d-144">これにより、認証要求とトークンが、現在 bot と対話しているユーザーに関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="dfe4d-145">Bot が認証済みアクション (外部 REST Api の呼び出しなど) を実行する必要があるときに、トークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="dfe4d-146">ダイアログコードでは、次のスニペット (C#) を追加する必要があります。これは、既存のアクセストークンがあるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

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

<span data-ttu-id="dfe4d-147">アクセストークンが存在しない場合、コードは OAuthCard を含むメッセージをユーザーに送信します。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="dfe4d-148">ログイン完了アクティビティを処理するには、次の呼び出しを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

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

<span data-ttu-id="dfe4d-149">ダイアログコードで、Bot 認証サービスからトークンを取得できます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

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

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="dfe4d-150">メッセージング拡張機能での OAuthCard の使用</span><span class="sxs-lookup"><span data-stu-id="dfe4d-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="dfe4d-151">Azure Bot サービスを使用して、メッセージング拡張機能にサードパーティのプロバイダーを接続することもできます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="dfe4d-152">このフローは bot と同じですが、OAuthCard を返すのではなく、サービスからログインプロンプトが返されます。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="dfe4d-153">次のスニペット (C#) は、ログイン応答を策定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

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

<span data-ttu-id="dfe4d-154">上記の例では、 `GetSignInLinkAsync` `client.OAuthApi`プロパティに対して直接呼び出しを行う必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="dfe4d-155">ユーザーがログインシーケンスを正常に完了すると、サービスは、元のユーザークエリを含む別の呼び出し要求と、"マジック code" を含む状態パラメーター文字列を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="dfe4d-156">この文字列を使用してトークンを、ユーザー ID と接続名とともにフェッチできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="dfe4d-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

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
