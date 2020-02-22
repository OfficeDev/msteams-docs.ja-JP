---
title: 事前メッセージ
description: Bot が Microsoft Teams で会話を開始できることについて説明します。
keywords: teams シナリオの予防的なメッセージング会話 bot
ms.openlocfilehash: 2f644820da33acc885a7972b13a1f61c167d6d8f
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228067"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="cd49d-104">Bot のための事前のメッセージング</span><span class="sxs-lookup"><span data-stu-id="cd49d-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="cd49d-105">"予防的なメッセージ" とは、bot が会話を開始するために送信するメッセージです。</span><span class="sxs-lookup"><span data-stu-id="cd49d-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="cd49d-106">次のようなさまざまな理由により、ボットで会話を開始することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="cd49d-107">個人ボット会話のウェルカムメッセージ</span><span class="sxs-lookup"><span data-stu-id="cd49d-107">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="cd49d-108">投票応答</span><span class="sxs-lookup"><span data-stu-id="cd49d-108">Poll responses</span></span>
* <span data-ttu-id="cd49d-109">外部イベント通知</span><span class="sxs-lookup"><span data-stu-id="cd49d-109">External event notifications</span></span>

<span data-ttu-id="cd49d-110">メッセージを送信して新しい会話スレッドを開始する方法は、既存の会話に対してメッセージを送信することとは異なります。 bot が新しい会話を開始すると、メッセージを投稿する既存の会話はありません。</span><span class="sxs-lookup"><span data-stu-id="cd49d-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="cd49d-111">事前メッセージを送信するには、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="cd49d-112">発言対象を決定する</span><span class="sxs-lookup"><span data-stu-id="cd49d-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="cd49d-113">ユーザーの一意の Id とテナント Id を取得する</span><span class="sxs-lookup"><span data-stu-id="cd49d-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="cd49d-114">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="cd49d-114">Send the message</span></span>](#examples)

<span data-ttu-id="cd49d-115">事前メッセージを作成するときは`MicrosoftAppCredentials.TrustServiceUrl`、を呼び出してサービス URL を作成して`ConnectorClient`から、メッセージの送信に使用するを作成する**必要があり**ます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="cd49d-116">そうしないと、アプリは応答を`401: Unauthorized`受信します。</span><span class="sxs-lookup"><span data-stu-id="cd49d-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="cd49d-117">[以下のサンプルを](#net-example-from-this-sample)参照してください。</span><span class="sxs-lookup"><span data-stu-id="cd49d-117">See [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="cd49d-118">事前メッセージのベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="cd49d-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="cd49d-119">事前にメッセージをユーザーに送信することは、ユーザーとの通信に非常に効果的な方法となります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="cd49d-120">ただし、このメッセージは完全に表示されないことがわかります。また、ウェルカムメッセージがアプリを初めて操作したときには、このメッセージが完全に非表示になっているように見えます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="cd49d-121">そのため、この機能を多用しない (ユーザーにスパムを行わない) こと、および伝達の理由を理解するのに十分な情報を提供することが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="cd49d-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="cd49d-122">予防的なメッセージは、通常、ウェルカムメッセージまたは通知の2つのカテゴリに分類されます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="cd49d-123">ウェルカムメッセージ</span><span class="sxs-lookup"><span data-stu-id="cd49d-123">Welcome messages</span></span>

<span data-ttu-id="cd49d-124">事前メッセージを使用して、ユーザーにウェルカムメッセージを送信する場合は、メッセージを受信する多くのユーザーが受信する理由についてのコンテキストがないことに注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="cd49d-125">これは、アプリを初めて使用したときにも使用されます。最初の印象を得ることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="cd49d-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="cd49d-126">推奨されるウェルカムメッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="cd49d-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="cd49d-127">**なぜこのメッセージを受信するのですか。**</span><span class="sxs-lookup"><span data-stu-id="cd49d-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="cd49d-128">ユーザーがメッセージを受信する理由を明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="cd49d-129">Bot がチャネルにインストールされていて、すべてのユーザーにウェルカムメッセージを送信した場合は、インストールされているチャネルと、インストールされている可能性のあるチャネルを知らせます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="cd49d-130">**何を提供するか。**</span><span class="sxs-lookup"><span data-stu-id="cd49d-130">**What do you offer.**</span></span> <span data-ttu-id="cd49d-131">アプリでできること</span><span class="sxs-lookup"><span data-stu-id="cd49d-131">What can they do with your app?</span></span> <span data-ttu-id="cd49d-132">どのような値にすることができますか。</span><span class="sxs-lookup"><span data-stu-id="cd49d-132">What value can you bring to them?</span></span>
* <span data-ttu-id="cd49d-133">**次の手順を実行します。**</span><span class="sxs-lookup"><span data-stu-id="cd49d-133">**What should they do next.**</span></span> <span data-ttu-id="cd49d-134">コマンドを試したり、何らかの方法でアプリを操作したりするように招待します。</span><span class="sxs-lookup"><span data-stu-id="cd49d-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="cd49d-135">通知メッセージ</span><span class="sxs-lookup"><span data-stu-id="cd49d-135">Notification messages</span></span>

<span data-ttu-id="cd49d-136">事前メッセージを使用して通知を送信する場合は、ユーザーが通知に基づいて一般的な操作を実行するための明確なパスを持っていることを確認し、通知が発生した理由を明確に理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="cd49d-137">適切な通知メッセージには、通常次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="cd49d-138">**どうしたのですか。**</span><span class="sxs-lookup"><span data-stu-id="cd49d-138">**What happened.**</span></span> <span data-ttu-id="cd49d-139">通知を発生させた理由を明確に示します。</span><span class="sxs-lookup"><span data-stu-id="cd49d-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="cd49d-140">**何が起こったのか。**</span><span class="sxs-lookup"><span data-stu-id="cd49d-140">**What it happened to.**</span></span> <span data-ttu-id="cd49d-141">通知を発生させるためにアイテムまたはアイテムが更新されたことを明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="cd49d-142">**だれがやったか。**</span><span class="sxs-lookup"><span data-stu-id="cd49d-142">**Who did it.**</span></span> <span data-ttu-id="cd49d-143">通知が送信された原因となった操作を行ったユーザー。</span><span class="sxs-lookup"><span data-stu-id="cd49d-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="cd49d-144">**そのためにできること。**</span><span class="sxs-lookup"><span data-stu-id="cd49d-144">**What they can do about it.**</span></span> <span data-ttu-id="cd49d-145">ユーザーが通知に基づいて操作を簡単に実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="cd49d-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="cd49d-146">**どのようにオプトアウトできるか。** ユーザーが追加の通知をオプトアウトするためのパスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="cd49d-147">必要なユーザー情報を取得する</span><span class="sxs-lookup"><span data-stu-id="cd49d-147">Obtain necessary user information</span></span>

<span data-ttu-id="cd49d-148">Bot は、ユーザーの*一意の id*とテナント id を取得することによって、個々の Microsoft Teams ユーザーとの新しい会話を作成でき*ます。*</span><span class="sxs-lookup"><span data-stu-id="cd49d-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user’s *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="cd49d-149">これらの値は、次のいずれかの方法を使用して取得できます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="cd49d-150">アプリがインストールされているチャネルから[チーム名簿を取得](~/resources/bot-v3/bots-context.md#fetching-the-team-roster)します。</span><span class="sxs-lookup"><span data-stu-id="cd49d-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="cd49d-151">ユーザーが[チャネル内の bot と対話](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)するときにキャッシュする。</span><span class="sxs-lookup"><span data-stu-id="cd49d-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="cd49d-152">ユーザーが[チャネル会話で @mentioned](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)すると、bot はの一部になります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="cd49d-153">アプリが個人スコープにインストールされたときにイベントを[受け取っ`conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)たときにキャッシュするか、新しいメンバーをチャネルまたはグループのチャットに追加します。</span><span class="sxs-lookup"><span data-stu-id="cd49d-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="cd49d-154">Graph を使用してアプリを事前にインストールする</span><span class="sxs-lookup"><span data-stu-id="cd49d-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="cd49d-155">Graph を使用してアプリを事前にインストールするのは、現在ベータ版です。</span><span class="sxs-lookup"><span data-stu-id="cd49d-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="cd49d-156">場合によっては、既にインストールされていない、またはアプリと対話していないメッセージユーザーを予防的に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="cd49d-157">たとえば、[会社の communicator](~/samples/app-templates.md#company-communicator)を使用して組織全体にメッセージを送信するとします。</span><span class="sxs-lookup"><span data-stu-id="cd49d-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="cd49d-158">このシナリオでは、Graph API を使用して、ユーザー用のアプリを事前にインストールし、インストール時に`conversationUpdate`アプリが受け取るイベントから必要な値をキャッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="cd49d-159">組織のアプリカタログまたは Teams アプリストアにあるアプリのみをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="cd49d-160">詳細については、グラフのドキュメントの「[ユーザー用アプリのインストール](/graph/teams-proactive-messaging)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cd49d-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="cd49d-161">[.Net に](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)は、サンプルもあります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="cd49d-162">例</span><span class="sxs-lookup"><span data-stu-id="cd49d-162">Examples</span></span>

<span data-ttu-id="cd49d-163">REST API を使用して新しい会話を作成する前に、必ず事前認証を行い、ベアラートークンを用意してください。</span><span class="sxs-lookup"><span data-stu-id="cd49d-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="cd49d-164">ユーザー ID とテナント ID を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd49d-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="cd49d-165">呼び出しが成功すると、API は次の応答オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="cd49d-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="cd49d-166">この ID は、パーソナルチャットの一意の会話 ID です。</span><span class="sxs-lookup"><span data-stu-id="cd49d-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="cd49d-167">この値を保存して、後でユーザーとの対話のために再利用してください。</span><span class="sxs-lookup"><span data-stu-id="cd49d-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="cd49d-168">.NET の使用</span><span class="sxs-lookup"><span data-stu-id="cd49d-168">Using .NET</span></span>

<span data-ttu-id="cd49d-169">この例では、 [Microsoft の Bot](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="cd49d-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

### <a name="using-nodejs"></a><span data-ttu-id="cd49d-170">Node.js の使用</span><span class="sxs-lookup"><span data-stu-id="cd49d-170">Using Node.js</span></span>

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

<span data-ttu-id="cd49d-171">[Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください*。</span><span class="sxs-lookup"><span data-stu-id="cd49d-171">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="cd49d-172">チャネル会話の作成</span><span class="sxs-lookup"><span data-stu-id="cd49d-172">Creating a channel conversation</span></span>

<span data-ttu-id="cd49d-173">チームが追加した bot は、チャネルに投稿して新しい返信チェーンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-173">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="cd49d-174">Node.js Teams SDK を使用している場合は、を`startReplyChain()`使用して、適切なアクティビティ id と会話 id を持つ完全に入力されたアドレスを付与します。C# を使用している場合は、次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cd49d-174">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="cd49d-175">または、REST API を使用して、POST 要求を resource [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation)に発行することもできます。</span><span class="sxs-lookup"><span data-stu-id="cd49d-175">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="cd49d-176">.NET の例 ([このサンプル](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)から)</span><span class="sxs-lookup"><span data-stu-id="cd49d-176">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

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
