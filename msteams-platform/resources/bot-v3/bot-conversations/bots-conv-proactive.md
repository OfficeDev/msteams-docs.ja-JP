---
title: プロアクティブ メッセージ
description: ボットが Microsoft Teams で会話を開始できる方法について説明する
ms.topic: conceptual
localization_priority: Normal
keywords: Teams シナリオのプロアクティブ メッセージング会話ボット
ms.openlocfilehash: a13c565c8abe8c78fe6402d76796381b6a837393
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019791"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="f21d3-104">ボットのプロアクティブ メッセージング</span><span class="sxs-lookup"><span data-stu-id="f21d3-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="f21d3-105">プロアクティブ メッセージとは、ボットが会話を開始するために送信するメッセージです。</span><span class="sxs-lookup"><span data-stu-id="f21d3-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="f21d3-106">ボットに会話を開始させる理由として、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="f21d3-107">個人向けの会話におけるボットのウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="f21d3-107">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="f21d3-108">投票の回答</span><span class="sxs-lookup"><span data-stu-id="f21d3-108">Poll responses</span></span>
* <span data-ttu-id="f21d3-109">外部イベントの通知</span><span class="sxs-lookup"><span data-stu-id="f21d3-109">External event notifications</span></span>

<span data-ttu-id="f21d3-110">新しい会話スレッドを開始するメッセージの送信は、既存の会話に応答してメッセージを送信する場合とは異なります。ボットが新しい会話を開始すると、メッセージを投稿する既存の会話はありません。</span><span class="sxs-lookup"><span data-stu-id="f21d3-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="f21d3-111">プロアクティブ メッセージを送信するには、次の必要があります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="f21d3-112">何を言うのかを決める</span><span class="sxs-lookup"><span data-stu-id="f21d3-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="f21d3-113">ユーザーの一意の ID とテナント ID を取得する</span><span class="sxs-lookup"><span data-stu-id="f21d3-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="f21d3-114">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="f21d3-114">Send the message</span></span>](#examples)

<span data-ttu-id="f21d3-115">プロアクティブ メッセージを作成する場合は、メッセージの送信に使用するメッセージを作成する前に、サービス URL を呼び出して渡 `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` す必要があります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="f21d3-116">応答しない場合、アプリは応答を受信 `401: Unauthorized` します。</span><span class="sxs-lookup"><span data-stu-id="f21d3-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="f21d3-117">以下 [のサンプルを参照してください](#net-example-from-this-sample)。</span><span class="sxs-lookup"><span data-stu-id="f21d3-117">See [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="f21d3-118">プロアクティブ メッセージングのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="f21d3-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="f21d3-119">ユーザーにプロアクティブ メッセージを送信すると、ユーザーと通信する非常に効果的な方法になります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="f21d3-120">ただし、このメッセージの観点から見ると、このメッセージは完全にプロンプトされていないものに見え、ウェルカム メッセージの場合はアプリを初めて操作します。</span><span class="sxs-lookup"><span data-stu-id="f21d3-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="f21d3-121">そのため、この機能を使用する (ユーザーに迷惑メールを送信しない) ので、メッセージが送信される理由を理解するのに十分な情報を提供することが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="f21d3-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="f21d3-122">プロアクティブ メッセージは、一般にウェルカム メッセージと通知の 2 つのカテゴリに分類されます。</span><span class="sxs-lookup"><span data-stu-id="f21d3-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="f21d3-123">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="f21d3-123">Welcome messages</span></span>

<span data-ttu-id="f21d3-124">プロアクティブ メッセージングを使用してユーザーにウェルカム メッセージを送信する場合は、メッセージを受信するほとんどのユーザーに対して、メッセージを受信する理由に関するコンテキストが提供されません。</span><span class="sxs-lookup"><span data-stu-id="f21d3-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="f21d3-125">また、アプリを操作したのも初めてです。良い第一印象を作り出す機会です。</span><span class="sxs-lookup"><span data-stu-id="f21d3-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="f21d3-126">最適なウェルカム メッセージには、次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f21d3-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="f21d3-127">**なぜこのメッセージを受け取るのですか。**</span><span class="sxs-lookup"><span data-stu-id="f21d3-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="f21d3-128">ユーザーがメッセージを受信する理由は非常に明確である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="f21d3-129">あなたのボットがチャネルにインストールされていて、すべてのユーザーにウェルカム メッセージを送信した場合は、どのチャネルにインストールされ、誰がインストールしたのかを通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="f21d3-130">**提示する内容。**</span><span class="sxs-lookup"><span data-stu-id="f21d3-130">**What do you offer.**</span></span> <span data-ttu-id="f21d3-131">ユーザーはあなたのアプリで何ができるのでしょうか?</span><span class="sxs-lookup"><span data-stu-id="f21d3-131">What can they do with your app?</span></span> <span data-ttu-id="f21d3-132">ユーザーはどのような価値を得られるのでしょうか?</span><span class="sxs-lookup"><span data-stu-id="f21d3-132">What value can you bring to them?</span></span>
* <span data-ttu-id="f21d3-133">**ユーザーが次にするべきこと。**</span><span class="sxs-lookup"><span data-stu-id="f21d3-133">**What should they do next.**</span></span> <span data-ttu-id="f21d3-134">コマンドを試すように招待したり、何らかの方法でアプリと対話したりします。</span><span class="sxs-lookup"><span data-stu-id="f21d3-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="f21d3-135">通知メッセージ</span><span class="sxs-lookup"><span data-stu-id="f21d3-135">Notification messages</span></span>

<span data-ttu-id="f21d3-136">プロアクティブ メッセージングを使用して通知を送信する場合は、ユーザーが通知に基づいて一般的なアクションを実行する明確なパスを持ち、通知が発生した理由を明確に理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="f21d3-137">良好な通知メッセージには、通常、次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f21d3-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="f21d3-138">**何が起こったのですか。**</span><span class="sxs-lookup"><span data-stu-id="f21d3-138">**What happened.**</span></span> <span data-ttu-id="f21d3-139">何が原因で通知が発生したのかを明確に示しています。</span><span class="sxs-lookup"><span data-stu-id="f21d3-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="f21d3-140">**何が起こったのか。**</span><span class="sxs-lookup"><span data-stu-id="f21d3-140">**What it happened to.**</span></span> <span data-ttu-id="f21d3-141">通知を発生するために更新されたアイテム/物を明確にしてください。</span><span class="sxs-lookup"><span data-stu-id="f21d3-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="f21d3-142">**誰がやったか。**</span><span class="sxs-lookup"><span data-stu-id="f21d3-142">**Who did it.**</span></span> <span data-ttu-id="f21d3-143">通知の送信を引き起こしたアクションを実行したユーザー。</span><span class="sxs-lookup"><span data-stu-id="f21d3-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="f21d3-144">**彼らが何を行うのか。**</span><span class="sxs-lookup"><span data-stu-id="f21d3-144">**What they can do about it.**</span></span> <span data-ttu-id="f21d3-145">ユーザーが通知に基づいてアクションを取ることを容易にします。</span><span class="sxs-lookup"><span data-stu-id="f21d3-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="f21d3-146">**オプトアウトする方法。** ユーザーが追加の通知をオプトアウトするパスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="f21d3-147">必要なユーザー情報を取得する</span><span class="sxs-lookup"><span data-stu-id="f21d3-147">Obtain necessary user information</span></span>

<span data-ttu-id="f21d3-148">ボットは、ユーザーの一意の *ID* とテナント ID を取得することで、個々の Microsoft Teams ユーザーとの新しい会話 *を作成できます。*</span><span class="sxs-lookup"><span data-stu-id="f21d3-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="f21d3-149">これらの値は、次のいずれかの方法で取得できます。</span><span class="sxs-lookup"><span data-stu-id="f21d3-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="f21d3-150">アプリ [がインストールされているチャネル](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) からチーム名簿を取得します。</span><span class="sxs-lookup"><span data-stu-id="f21d3-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="f21d3-151">ユーザーがチャネルでボットとやり取りするときにキャッシュ [します](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="f21d3-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="f21d3-152">ユーザーがチャネル会話 [@mentioned、](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) ボットは一部です。</span><span class="sxs-lookup"><span data-stu-id="f21d3-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="f21d3-153">アプリが個人用スコープにインストール[ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)されている場合、または新しいメンバーがチャネルまたはグループ チャットに追加された場合に、それらをキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="f21d3-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="f21d3-154">Graph を使用してアプリをプロアクティブにインストール</span><span class="sxs-lookup"><span data-stu-id="f21d3-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="f21d3-155">Graph を使用してアプリを積極的にインストールする方法は、現在ベータ版です。</span><span class="sxs-lookup"><span data-stu-id="f21d3-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="f21d3-156">場合によっては、以前にアプリをインストールしていない、またはアプリと対話していないユーザーにプロアクティブにメッセージを送る必要があるかもしれません。</span><span class="sxs-lookup"><span data-stu-id="f21d3-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="f21d3-157">たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。</span><span class="sxs-lookup"><span data-stu-id="f21d3-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="f21d3-158">このシナリオでは、Graph API を使用してユーザー向けアプリをプロアクティブにインストールし、インストール時にアプリが受け取るイベントから必要な値を `conversationUpdate` キャッシュできます。</span><span class="sxs-lookup"><span data-stu-id="f21d3-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="f21d3-159">組織のアプリ カタログまたは Teams アプリ ストア内のアプリのみをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="f21d3-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="f21d3-160">詳細については [、Graph のドキュメントの](/graph/teams-proactive-messaging) 「ユーザー向けアプリのインストール」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f21d3-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="f21d3-161">.NET にも [サンプルがあります](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。</span><span class="sxs-lookup"><span data-stu-id="f21d3-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="f21d3-162">例</span><span class="sxs-lookup"><span data-stu-id="f21d3-162">Examples</span></span>

<span data-ttu-id="f21d3-163">REST API を使用して新しい会話を作成する前に、ベアラー トークンを認証して持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="f21d3-164">ユーザー ID とテナント ID を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f21d3-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="f21d3-165">呼び出しに成功した場合、API は以下の応答オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="f21d3-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="f21d3-166">この ID は、個人チャットの一意の会話 ID です。</span><span class="sxs-lookup"><span data-stu-id="f21d3-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="f21d3-167">この値を保存し、ユーザーとの将来のやり取りのために再利用してください。</span><span class="sxs-lookup"><span data-stu-id="f21d3-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="f21d3-168">.NET の使用</span><span class="sxs-lookup"><span data-stu-id="f21d3-168">Using .NET</span></span>

<span data-ttu-id="f21d3-169">この例では [、Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="f21d3-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

### <a name="using-nodejs"></a><span data-ttu-id="f21d3-170">ユーザー設定Node.js</span><span class="sxs-lookup"><span data-stu-id="f21d3-170">Using Node.js</span></span>

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

<span data-ttu-id="f21d3-171">*「Bot* [Framework のサンプル」も参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="f21d3-171">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="f21d3-172">チャネル会話の作成</span><span class="sxs-lookup"><span data-stu-id="f21d3-172">Creating a channel conversation</span></span>

<span data-ttu-id="f21d3-173">チームが追加したボットは、チャネルに投稿して新しい返信チェーンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f21d3-173">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="f21d3-174">Teams SDK の Node.js使用している場合は、正しいアクティビティ ID と会話 ID を持つ完全に入力されたアドレス `startReplyChain()` を使用します。このツールを使用しているC#、以下の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f21d3-174">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="f21d3-175">または、REST API を使用して、リソースに POST 要求を発行 [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) することもできます。</span><span class="sxs-lookup"><span data-stu-id="f21d3-175">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="f21d3-176">.NET の例 (この [サンプルから](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span><span class="sxs-lookup"><span data-stu-id="f21d3-176">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

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
