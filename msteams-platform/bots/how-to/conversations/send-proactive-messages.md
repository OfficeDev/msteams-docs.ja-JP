---
title: プロアクティブ メッセージを送信する
author: clearab
description: Microsoft Teams bot で予防的なメッセージを送信する方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6e387dcf0e73124d57996a56c835f5a99fc6f1c6
ms.sourcegitcommit: b822584b643e003d12d2e9b5b02a0534b2d57d71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "44704461"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="4cc51-103">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="4cc51-103">Send proactive messages</span></span>

> [!Note]
> <span data-ttu-id="4cc51-104">この記事のコードサンプルでは、v3 Bot フレームワーク SDK および v3 Teams Bot SDK 拡張機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="4cc51-104">The code samples in this article make use of the v3 Bot Framework SDK, and v3 Teams Bot Builder SDK extensions.</span></span> <span data-ttu-id="4cc51-105">概念上、SDK の v4 バージョンを使用している場合、この情報は適用されますが、コードは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-105">Conceptually, the information applies when using the v4 versions of the SDK, but the code is slightly different.</span></span>

<span data-ttu-id="4cc51-106">"予防的なメッセージ" とは、bot が会話を開始するために送信するメッセージです。</span><span class="sxs-lookup"><span data-stu-id="4cc51-106">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="4cc51-107">ボットに会話を開始させる理由として、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-107">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="4cc51-108">個人向けの会話におけるボットのウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="4cc51-108">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="4cc51-109">投票の回答</span><span class="sxs-lookup"><span data-stu-id="4cc51-109">Poll responses</span></span>
* <span data-ttu-id="4cc51-110">外部イベントの通知</span><span class="sxs-lookup"><span data-stu-id="4cc51-110">External event notifications</span></span>

<span data-ttu-id="4cc51-111">メッセージを送信して新しい会話スレッドを開始する方法は、既存の会話に対してメッセージを送信することとは異なります。 bot が新しい会話を開始すると、メッセージを投稿する既存の会話はありません。</span><span class="sxs-lookup"><span data-stu-id="4cc51-111">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="4cc51-112">事前メッセージを送信するには、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-112">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="4cc51-113">発言対象を決定する</span><span class="sxs-lookup"><span data-stu-id="4cc51-113">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="4cc51-114">ユーザーの一意の Id とテナント Id を取得する</span><span class="sxs-lookup"><span data-stu-id="4cc51-114">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="4cc51-115">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="4cc51-115">Send the message</span></span>](#examples)

<span data-ttu-id="4cc51-116">事前メッセージを作成する**must**ときは、を呼び出し `MicrosoftAppCredentials.TrustServiceUrl` てサービス URL を作成してから、 [`ConnectorClient`](/azure/bot-service/dotnet/bot-builder-dotnet-connector) メッセージの送信に使用するを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-116">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the [`ConnectorClient`](/azure/bot-service/dotnet/bot-builder-dotnet-connector) you will use to send the message.</span></span> <span data-ttu-id="4cc51-117">そうしないと、アプリは応答を受信 `401: Unauthorized` します。</span><span class="sxs-lookup"><span data-stu-id="4cc51-117">If you do not, your app will receive a `401: Unauthorized` response.</span></span>

> [!Tip]
> <span data-ttu-id="4cc51-118">For .NET クライアントのセットアップの詳細については、「 `ConnectorClient` [Send and receive アクティビティ](/azure/bot-service/dotnet/bot-builder-dotnet-connector#create-a-connector-client)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4cc51-118">For more details on setting up the `ConnectorClient` for .NET clients, see the [Send and receive activities](/azure/bot-service/dotnet/bot-builder-dotnet-connector#create-a-connector-client) topic</span></span>
>
> <span data-ttu-id="4cc51-119">予防的なメッセージを送信するためのその他の例については、「Azure Bot Service [.net](/azure/bot-service/dotnet/bot-builder-dotnet-proactive-messages) 」および[Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-proactive-messages)のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4cc51-119">More examples for sending proactive messages can be found in the Azure Bot Service [.NET](/azure/bot-service/dotnet/bot-builder-dotnet-proactive-messages) and [Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-proactive-messages) documentation</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="4cc51-120">事前メッセージのベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="4cc51-120">Best practices for proactive messaging</span></span>

<span data-ttu-id="4cc51-121">事前にメッセージをユーザーに送信することは、ユーザーとの通信に非常に効果的な方法となります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-121">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="4cc51-122">ただし、このメッセージは完全に表示されないことがわかります。また、ウェルカムメッセージがアプリを初めて操作したときには、このメッセージが完全に非表示になっているように見えます。</span><span class="sxs-lookup"><span data-stu-id="4cc51-122">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="4cc51-123">そのため、この機能を多用しない (ユーザーにスパムを行わない) こと、および伝達の理由を理解するのに十分な情報を提供することが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="4cc51-123">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="4cc51-124">プロアクティブ メッセージは、一般にウェルカム メッセージと通知の 2 つのカテゴリに分類されます。</span><span class="sxs-lookup"><span data-stu-id="4cc51-124">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="4cc51-125">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="4cc51-125">Welcome messages</span></span>

<span data-ttu-id="4cc51-126">事前メッセージを使用して、ユーザーにウェルカムメッセージを送信する場合は、メッセージを受信する多くのユーザーが受信する理由についてのコンテキストがないことに注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-126">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="4cc51-127">これは、アプリを初めて使用したときにも使用されます。最初の印象を得ることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4cc51-127">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="4cc51-128">推奨されるウェルカムメッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="4cc51-128">The best welcome messages will include:</span></span>

* <span data-ttu-id="4cc51-129">**なぜこのメッセージを受信するのですか。**</span><span class="sxs-lookup"><span data-stu-id="4cc51-129">**Why are they receiving this message.**</span></span> <span data-ttu-id="4cc51-130">ユーザーがメッセージを受信する理由を明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-130">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="4cc51-131">Bot がチャネルにインストールされていて、すべてのユーザーにウェルカムメッセージを送信した場合は、インストールされているチャネルと、インストールされている可能性のあるチャネルを知らせます。</span><span class="sxs-lookup"><span data-stu-id="4cc51-131">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="4cc51-132">**何を提供するか。**</span><span class="sxs-lookup"><span data-stu-id="4cc51-132">**What do you offer.**</span></span> <span data-ttu-id="4cc51-133">アプリでできること</span><span class="sxs-lookup"><span data-stu-id="4cc51-133">What can they do with your app?</span></span> <span data-ttu-id="4cc51-134">どのような値にすることができますか。</span><span class="sxs-lookup"><span data-stu-id="4cc51-134">What value can you bring to them?</span></span>
* <span data-ttu-id="4cc51-135">**次の手順を実行します。**</span><span class="sxs-lookup"><span data-stu-id="4cc51-135">**What should they do next.**</span></span> <span data-ttu-id="4cc51-136">コマンドを試したり、何らかの方法でアプリを操作したりするように招待します。</span><span class="sxs-lookup"><span data-stu-id="4cc51-136">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="4cc51-137">通知メッセージ</span><span class="sxs-lookup"><span data-stu-id="4cc51-137">Notification messages</span></span>

<span data-ttu-id="4cc51-138">事前メッセージを使用して通知を送信する場合は、ユーザーが通知に基づいて一般的な操作を実行するための明確なパスを持っていることを確認し、通知が発生した理由を明確に理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-138">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="4cc51-139">適切な通知メッセージには、通常次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="4cc51-139">Good notification messages will generally include:</span></span>

* <span data-ttu-id="4cc51-140">**どうしたのですか。**</span><span class="sxs-lookup"><span data-stu-id="4cc51-140">**What happened.**</span></span> <span data-ttu-id="4cc51-141">通知を発生させた理由を明確に示します。</span><span class="sxs-lookup"><span data-stu-id="4cc51-141">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="4cc51-142">**何が起こったのか。**</span><span class="sxs-lookup"><span data-stu-id="4cc51-142">**What it happened to.**</span></span> <span data-ttu-id="4cc51-143">通知を発生させるためにアイテムまたはアイテムが更新されたことを明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-143">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="4cc51-144">**だれがやったか。**</span><span class="sxs-lookup"><span data-stu-id="4cc51-144">**Who did it.**</span></span> <span data-ttu-id="4cc51-145">通知が送信された原因となった操作を行ったユーザー。</span><span class="sxs-lookup"><span data-stu-id="4cc51-145">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="4cc51-146">**そのためにできること。**</span><span class="sxs-lookup"><span data-stu-id="4cc51-146">**What they can do about it.**</span></span> <span data-ttu-id="4cc51-147">ユーザーが通知に基づいて操作を簡単に実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="4cc51-147">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="4cc51-148">**どのようにオプトアウトできるか。** ユーザーが追加の通知をオプトアウトするためのパスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-148">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="4cc51-149">必要なユーザー情報を取得する</span><span class="sxs-lookup"><span data-stu-id="4cc51-149">Obtain necessary user information</span></span>

<span data-ttu-id="4cc51-150">Bot は、ユーザーの*一意の id*とテナント id を取得することによって、個々の Microsoft Teams ユーザーとの新しい会話を作成でき*ます。*</span><span class="sxs-lookup"><span data-stu-id="4cc51-150">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="4cc51-151">これらの値は、次のいずれかの方法を使用して取得できます。</span><span class="sxs-lookup"><span data-stu-id="4cc51-151">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="4cc51-152">アプリがインストールされているチャネルから[チーム名簿を取得](../get-teams-context.md#fetching-the-roster-or-user-profile)します。</span><span class="sxs-lookup"><span data-stu-id="4cc51-152">By [fetching the team roster](../get-teams-context.md#fetching-the-roster-or-user-profile) from a channel your app is installed in.</span></span>
* <span data-ttu-id="4cc51-153">ユーザーが[チャネル内の bot と対話](./channel-and-group-conversations.md)するときにキャッシュする。</span><span class="sxs-lookup"><span data-stu-id="4cc51-153">By caching them when a user [interacts with your bot in a channel](./channel-and-group-conversations.md).</span></span>
* <span data-ttu-id="4cc51-154">ユーザーが[チャネル会話で @mentioned](./channel-and-group-conversations.md#retrieving-mentions)すると、bot はの一部になります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-154">When a users is [@mentioned in a channel conversation](./channel-and-group-conversations.md#retrieving-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="4cc51-155">アプリが個人スコープにインストールされたときにイベントを[受け取っ `conversationUpdate` ](./subscribe-to-conversation-events.md#team-members-added)たときにキャッシュするか、新しいメンバーをチャネルまたはグループのチャットに追加します。</span><span class="sxs-lookup"><span data-stu-id="4cc51-155">By caching them when you [receive the `conversationUpdate`](./subscribe-to-conversation-events.md#team-members-added) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="4cc51-156">Graph を使用してアプリを事前にインストールする</span><span class="sxs-lookup"><span data-stu-id="4cc51-156">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="4cc51-157">Graph を使用してアプリを事前にインストールするのは、現在ベータ版です。</span><span class="sxs-lookup"><span data-stu-id="4cc51-157">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="4cc51-158">場合によっては、既にインストールされていない、またはアプリと対話していないメッセージユーザーを予防的に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-158">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="4cc51-159">たとえば、[会社の communicator](~/samples/app-templates.md#company-communicator)を使用して組織全体にメッセージを送信するとします。</span><span class="sxs-lookup"><span data-stu-id="4cc51-159">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="4cc51-160">このシナリオでは、Graph API を使用して、ユーザー用のアプリを事前にインストールし、 `conversationUpdate` インストール時にアプリが受け取るイベントから必要な値をキャッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="4cc51-160">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="4cc51-161">組織のアプリカタログまたは Teams アプリストアにあるアプリのみをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="4cc51-161">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="4cc51-162">詳細については、グラフのドキュメントの「[ユーザー用アプリのインストール](/graph/teams-proactive-messaging)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4cc51-162">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="4cc51-163">[.Net に](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)は、サンプルもあります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-163">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="4cc51-164">例</span><span class="sxs-lookup"><span data-stu-id="4cc51-164">Examples</span></span>

<span data-ttu-id="4cc51-165">REST API を使用して新しい会話を作成する前に、必ず事前認証を行い、ベアラートークンを用意してください。</span><span class="sxs-lookup"><span data-stu-id="4cc51-165">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span> <span data-ttu-id="4cc51-166">`members.id`下のオブジェクトのフィールドは、ボットとユーザーの組み合わせに固有のものです。</span><span class="sxs-lookup"><span data-stu-id="4cc51-166">The `members.id` field in the object below is unique to the combination of your bot and a user.</span></span> <span data-ttu-id="4cc51-167">上記以外の方法では、他の方法で取得することはできません。</span><span class="sxs-lookup"><span data-stu-id="4cc51-167">You cannot obtain it via any other method than those outlined above.</span></span>

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

<span data-ttu-id="4cc51-168">ユーザー ID とテナント ID を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cc51-168">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="4cc51-169">呼び出しが成功すると、API は次の応答オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="4cc51-169">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="4cc51-170">この ID は、パーソナルチャットの一意の会話 ID です。</span><span class="sxs-lookup"><span data-stu-id="4cc51-170">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="4cc51-171">この値を保存して、後でユーザーとの対話のために再利用してください。</span><span class="sxs-lookup"><span data-stu-id="4cc51-171">Please store this value and reuse it for future interactions with the user.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="4cc51-172">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="4cc51-172">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="4cc51-173">この例では、 [Microsoft の Bot](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="4cc51-173">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span> <span data-ttu-id="4cc51-174">この例で `client` は、は、 `ConnectorClient` [送受信アクティビティ](/azure/bot-service/dotnet/bot-builder-dotnet-connector)の説明に従って既に作成され、認証されているインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="4cc51-174">In this example, `client` is a `ConnectorClient` instance that has already been created and authenticated as described in [Send and receive activities](/azure/bot-service/dotnet/bot-builder-dotnet-connector)</span></span>

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

# <a name="javascript"></a>[<span data-ttu-id="4cc51-175">JavaScript</span><span class="sxs-lookup"><span data-stu-id="4cc51-175">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="4cc51-176">[Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください*。</span><span class="sxs-lookup"><span data-stu-id="4cc51-176">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

# <a name="python"></a>[<span data-ttu-id="4cc51-177">Python</span><span class="sxs-lookup"><span data-stu-id="4cc51-177">Python</span></span>](#tab/python)

```python
async def _send_proactive_message():
  for conversation_reference in CONVERSATION_REFERENCES.values():
    return await ADAPTER.continue_conversation(APP_ID, conversation_reference,
      lambda turn_context: turn_context.send_activity("proactive hello")
    )

```

---

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="4cc51-178">チャネル会話の作成</span><span class="sxs-lookup"><span data-stu-id="4cc51-178">Creating a channel conversation</span></span>

<span data-ttu-id="4cc51-179">チームが追加したボットは、チャネルに投稿して新しい返信チェーンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="4cc51-179">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="4cc51-180">Node.js Teams SDK を使用している場合は、を使用して、 `startReplyChain()` 適切なアクティビティ id と会話 id を持つ完全に入力されたアドレスを提供します。C# を使用している場合は、次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4cc51-180">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="4cc51-181">または、REST API を使用して、POST 要求を resource に発行することもでき [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ます。</span><span class="sxs-lookup"><span data-stu-id="4cc51-181">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="4cc51-182">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="4cc51-182">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="4cc51-183">[このサンプル](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)のコードスニペットは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="4cc51-183">The following code snippet is from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs).</span></span>

```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```

# <a name="javascript"></a>[<span data-ttu-id="4cc51-184">JavaScript</span><span class="sxs-lookup"><span data-stu-id="4cc51-184">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="4cc51-185">次のコードスニペットは[teamsConversationBot.js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js)からのものです。</span><span class="sxs-lookup"><span data-stu-id="4cc51-185">The following code snippet is from [teamsConversationBot.js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js).</span></span>

[!code-javascript[messageAllMembersAsync](~/../botbuilder-samples/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js?range=115-134&highlight=13-15)]

# <a name="python"></a>[<span data-ttu-id="4cc51-186">Python</span><span class="sxs-lookup"><span data-stu-id="4cc51-186">Python</span></span>](#tab/python)

[!code-python[message-all-members](~/../botbuilder-samples/samples/python/57.teams-conversation-bot/bots/teams_conversation_bot.py?range=101-135)]

---
