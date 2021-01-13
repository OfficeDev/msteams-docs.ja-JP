---
title: ボットとのチャネル会話とグループ会話
author: clearab
description: チャネルまたはグループ チャットでボットのメッセージを送信、受信、処理する方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8a9a58208fff5cc2fe376fcb9932bad6ac2bf36f
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797842"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="a8e24-103">Microsoft Teams ボットとのチャネルとグループ チャットの会話</span><span class="sxs-lookup"><span data-stu-id="a8e24-103">Channel and group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="a8e24-104">ボットに `teams` スコープを追加することで、チームチャットまたはグループ チャットにインストール `groupchat` できます。</span><span class="sxs-lookup"><span data-stu-id="a8e24-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="a8e24-105">これにより、会話のすべてのメンバーがボットと対話できるようになります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="a8e24-106">インストールされたボットは、会話メンバーのリストなど、会話に関するメタデータにもアクセスできるようになります。チームにインストールされた場合、そのチームに関する詳細とチャネルの完全な一覧にアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="a8e24-107">グループまたはチャネル内のボットは、メッセージが記載されている場合 (@botname) にのみメッセージを受信します。会話に送信された他のメッセージは受信しません。</span><span class="sxs-lookup"><span data-stu-id="a8e24-107">Bots in a group or channel only receive messages when they are mentioned (@botname), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="a8e24-108">ボットは直接 @メンションされる必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="a8e24-109">チームまたはチャネルが言及されている場合や、ボットからのメッセージに返信したユーザーがメッセージに応答しない場合、ボットはメッセージ@mentioningされません。</span><span class="sxs-lookup"><span data-stu-id="a8e24-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="a8e24-110">デザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="a8e24-110">Design guidelines</span></span>

<span data-ttu-id="a8e24-111">チャネルとチャットで [ボットの会話を設計する方法を参照してください](~/bots/design/bots.md)。</span><span class="sxs-lookup"><span data-stu-id="a8e24-111">See how to [design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="a8e24-112">新しい会話スレッドの作成</span><span class="sxs-lookup"><span data-stu-id="a8e24-112">Creating new conversation threads</span></span>

<span data-ttu-id="a8e24-113">ボットがチームにインストールされている場合、既存の会話スレッドに返信するのではなく、新しい会話スレッドを作成する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-113">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="a8e24-114">これはプロアクティブ メッセージング [の 1 つの形式です](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="a8e24-114">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with-mentions"></a><span data-ttu-id="a8e24-115">メンションの操作</span><span class="sxs-lookup"><span data-stu-id="a8e24-115">Working with mentions</span></span>

<span data-ttu-id="a8e24-116">グループやチャネルからボットに送信されるすべてのメッセージには、メッセージのテキストにボット自身の名前の付いた @メンションが含まれているため、メッセージ解析でメンションが確実に処理されるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-116">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="a8e24-117">ボットは、メッセージ内でメンションされている他のユーザーを取得したり、ボットが送信するすべてのメッセージにメンションを追加したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a8e24-117">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="a8e24-118">メッセージ テキストからメンションを削除する</span><span class="sxs-lookup"><span data-stu-id="a8e24-118">Stripping mentions from message text</span></span>

<span data-ttu-id="a8e24-119">ボットが受け取ったメッセージのテキストから @メンションを取り除く必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-119">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="a8e24-120">メンションの取得</span><span class="sxs-lookup"><span data-stu-id="a8e24-120">Retrieving mentions</span></span>

<span data-ttu-id="a8e24-121">メンションはペイロード内のオブジェクトで返され、ユーザーの一意の ID と、ほとんどの場合、メンションされたユーザーの名前の両方 `entities` が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a8e24-121">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="a8e24-122">メッセージのテキストには、`<at>@John Smith<at>` のようなメンションも含まれます。</span><span class="sxs-lookup"><span data-stu-id="a8e24-122">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="a8e24-123">ただし、メッセージ内のテキストを使用してユーザーに関する情報を取得する必要があります。メッセージを送信したユーザーがメッセージを変更する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-123">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="a8e24-124">代わりに、オブジェクトを使用 `entities` します。</span><span class="sxs-lookup"><span data-stu-id="a8e24-124">Instead, use the `entities` object.</span></span>

<span data-ttu-id="a8e24-125">オブジェクトの配列を返す Bot Builder SDK の関数を呼び出すことによって、メッセージ内のすべてのメンション `GetMentions` を取得 `Mention` できます。</span><span class="sxs-lookup"><span data-stu-id="a8e24-125">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="a8e24-126">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="a8e24-126">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    Mention[] mentions = turnContext.Activity.GetMentions();
    if(mentions != null)
    {
        ChannelAccount firstMention = mentions[0].Mentioned;
        await turnContext.SendActivityAsync($"Hello {firstMention.Name}");
    }
    else
    {
        await turnContext.SendActivityAsync("Aw, no one was mentioned.");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="a8e24-127">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="a8e24-127">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mentions = TurnContext.getMentions(turnContext.activity);
    if (mentions){
        const firstMention = mentions[0].mentioned;
        await turnContext.sendActivity(`Hello ${firstMention.name}.`);
    } else {
        await turnContext.sendActivity(`Aw, no one was mentioned.`);
    }

    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="a8e24-128">JSON</span><span class="sxs-lookup"><span data-stu-id="a8e24-128">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[<span data-ttu-id="a8e24-129">Python</span><span class="sxs-lookup"><span data-stu-id="a8e24-129">Python</span></span>](#tab/python)

```python
@staticmethod
def get_mentions(activity: Activity) -> List[Mention]:
    result: List[Mention] = []
    if activity.entities is not None:
        for entity in activity.entities:
            if entity.type.lower() == "mention":
                    result.append(entity)
     return result
```

* * *

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="a8e24-130">メッセージへのメンションの追加</span><span class="sxs-lookup"><span data-stu-id="a8e24-130">Adding mentions to your messages</span></span>

<span data-ttu-id="a8e24-131">ボットは、チャネルに投稿されたメッセージで他のユーザーをメンションできます。</span><span class="sxs-lookup"><span data-stu-id="a8e24-131">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="a8e24-132">これを行うには、メッセージで次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-132">To do this, your message must do the following:</span></span>

<span data-ttu-id="a8e24-133">この `Mention` オブジェクトには、次の 2 つのプロパティを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-133">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="a8e24-134">メッセージ <at>@username</at> にメッセージを含める</span><span class="sxs-lookup"><span data-stu-id="a8e24-134">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="a8e24-135">entities コレクション内に mention オブジェクトを含める</span><span class="sxs-lookup"><span data-stu-id="a8e24-135">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="a8e24-136">Bot Framework SDK には、メンションを簡単に構築するためのヘルパー メソッドとオブジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a8e24-136">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="a8e24-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="a8e24-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="a8e24-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="a8e24-138">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="a8e24-139">JSON</span><span class="sxs-lookup"><span data-stu-id="a8e24-139">JSON</span></span>](#tab/json)

<span data-ttu-id="a8e24-140">配列 `text` 内のオブジェクトのフィールド `entities` は、メッセージ *フィールドの一* 部と完全に一致している必要 `text` があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-140">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="a8e24-141">指定しない場合、メンションは無視されます。</span><span class="sxs-lookup"><span data-stu-id="a8e24-141">If it does not, the mention will be ignored.</span></span>

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[<span data-ttu-id="a8e24-142">Python</span><span class="sxs-lookup"><span data-stu-id="a8e24-142">Python</span></span>](#tab/python)

```python
async def _mention_activity(self, turn_context: TurnContext):
        mention = Mention(
            mentioned=turn_context.activity.from_property,
            text=f"<at>{turn_context.activity.from_property.name}</at>",
            type="mention"
        )

        reply_activity = MessageFactory.text(f"Hello {mention.text}")
        reply_activity.entities = [Mention().deserialize(mention.serialize())]
        await turn_context.send_activity(reply_activity)
```

* * *

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="a8e24-143">インストール時にメッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="a8e24-143">Sending a message on installation</span></span>

<span data-ttu-id="a8e24-144">ボットが最初にグループまたはチームに追加された場合、ボットを紹介するメッセージを送信すると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-144">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="a8e24-145">メッセージには、ボットの機能の簡単な説明と、その使い方が記載されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-145">The message should provide a brief description of the bot's features, and how to use them.</span></span> <span data-ttu-id="a8e24-146">eventType を使用して `conversationUpdate` イベントをサブスクライブ `teamMemberAdded` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-146">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="a8e24-147">イベントは新しいチーム メンバーが追加された際に送信されます。このイベントは、追加された新しいメンバーがボットかどうかを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-147">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="a8e24-148">詳細 [については、「新しいチーム メンバーへのウェルカム メッセージ](~/bots/how-to/conversations/send-proactive-messages.md) の送信」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a8e24-148">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="a8e24-149">ボットを追加するときに、チームの各メンバーに個人用メッセージを送信する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-149">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="a8e24-150">これを行うには、チーム名簿を取得し、各ユーザーに直接メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="a8e24-150">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="a8e24-151">次の状況では、メッセージを送信する方法は推奨されません。</span><span class="sxs-lookup"><span data-stu-id="a8e24-151">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="a8e24-152">チームは大規模です (明らかに主観的ですが、たとえば 100 人を超えるメンバー)。</span><span class="sxs-lookup"><span data-stu-id="a8e24-152">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="a8e24-153">ボットは "spammy" と見なされ、ボットを追加したユーザーは、ウェルカム メッセージを見たすべてのユーザーにボットの価値提案を明確に伝えられない限り、苦情を受け取る可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a8e24-153">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="a8e24-154">ボットは最初にグループまたはチャネルで言及されます (最初にチームに追加されるのとは比較して)</span><span class="sxs-lookup"><span data-stu-id="a8e24-154">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="a8e24-155">グループまたはチャネルの名前が変更される</span><span class="sxs-lookup"><span data-stu-id="a8e24-155">A group or channel is renamed</span></span>
* <span data-ttu-id="a8e24-156">チーム メンバーがグループまたはチャネルに追加される</span><span class="sxs-lookup"><span data-stu-id="a8e24-156">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="a8e24-157">詳細情報</span><span class="sxs-lookup"><span data-stu-id="a8e24-157">Learn more</span></span>

<span data-ttu-id="a8e24-158">ボットは、インストールされているグループ チャットまたはチームに関する追加情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a8e24-158">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="a8e24-159">ボット [で利用できる追加の](~/bots/how-to/get-teams-context.md) API については、チームのコンテキストの取得に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a8e24-159">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="a8e24-160">ボットがサブスクライブして応答できる追加のイベントも用意されています。</span><span class="sxs-lookup"><span data-stu-id="a8e24-160">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="a8e24-161">その [方法については、会話イベントのサブスクライブ](~/bots/how-to/conversations/subscribe-to-conversation-events.md) に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a8e24-161">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
