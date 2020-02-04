---
title: チャネルとグループの会話
author: clearab
description: チャネルまたはグループのチャットで bot 宛てのメッセージを送信、受信、処理する方法について説明します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ada2839ba41e4004b5f48449f4e057830dd841b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675025"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="e5b9a-103">Microsoft Teams bot によるチャネルおよびグループチャットの会話</span><span class="sxs-lookup"><span data-stu-id="e5b9a-103">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="e5b9a-104">Bot に`teams` or `groupchat`スコープを追加することで、チームまたはグループのチャットにインストールできるようになります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="e5b9a-105">これにより、会話のすべてのメンバーが bot と対話することができます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="e5b9a-106">インストールされた後は、会話メンバーのリストと同様に会話に関するメタデータにアクセスできます。また、チームの詳細と、そのチームに関する詳細なチャネルリストがインストールされている場合。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="e5b9a-107">グループまたはチャネル内のボットは、メッセージが記載されている場合にのみメッセージを受信します ("@botname")、会話に送信された他のメッセージは受信しません。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-107">Bots in a group or channel only receive messages when they are mentioned ("@botname"), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="e5b9a-108">Bot は直接 @mentioned する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="e5b9a-109">チームまたはチャネルが言及されたとき、またはユーザーが bot からメッセージに返信したときに @mentioning せずに、そのメッセージが bot に表示されることはありません。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-considerations"></a><span data-ttu-id="e5b9a-110">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="e5b9a-110">Design considerations</span></span>

<span data-ttu-id="e5b9a-111">Bot は、グループまたはチャネル内のすべてのメンバーについて適切かつ関連性のある情報を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-111">A bot should provide information that is both appropriate and relevant to all members in a group or channel.</span></span> <span data-ttu-id="e5b9a-112">この会話は、グループまたはチャネルの一部であるすべてのユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-112">Conversations with it are visible to everyone that is a part of the group or channel.</span></span> <span data-ttu-id="e5b9a-113">適切に設計された bot は、すべてのユーザーに値を追加することができますが、1対1の会話でより適切な情報を誤って共有することはありません。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-113">A well designed bot can add value to all users while not inadvertently sharing information that is more appropriate in a one-to-one conversation.</span></span> <span data-ttu-id="e5b9a-114">ダイアログのようなマルチターン会話は回避する必要があります。代わりに、カードやタスクモジュールを使用して情報を収集します。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-114">Multi-turn conversations like dialogs should be avoided - use cards and/or task modules to collect information instead.</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="e5b9a-115">新しい会話スレッドを作成する</span><span class="sxs-lookup"><span data-stu-id="e5b9a-115">Creating new conversation threads</span></span>

<span data-ttu-id="e5b9a-116">Bot がチームにインストールされている場合、既存のスレッドに返信するのではなく、新しい会話スレッドを作成する必要が生じることがあります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-116">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="e5b9a-117">これは、[事前メッセージ](~/bots/how-to/conversations/send-proactive-messages.md)の形式です。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-117">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with--mentions"></a><span data-ttu-id="e5b9a-118">@ メンションの使用</span><span class="sxs-lookup"><span data-stu-id="e5b9a-118">Working with @ Mentions</span></span>

<span data-ttu-id="e5b9a-119">グループまたはチャネルから bot へのすべてのメッセージには、メッセージテキストに独自の名前を持つ @mention が含まれているため、メッセージ解析でそのことを確実に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-119">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="e5b9a-120">Bot は、メッセージに記載されている他のユーザーを取得し、そのユーザーが送信するメッセージにメンションを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-120">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="e5b9a-121">メッセージテキストからメンションを除去する</span><span class="sxs-lookup"><span data-stu-id="e5b9a-121">Stripping mentions from message text</span></span>

<span data-ttu-id="e5b9a-122">Bot が受信するメッセージのテキストから @mentions を削除する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-122">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="e5b9a-123">メンションの取得</span><span class="sxs-lookup"><span data-stu-id="e5b9a-123">Retrieving mentions</span></span>

<span data-ttu-id="e5b9a-124">メンションは、 `entities`ペイロードのオブジェクトに返され、ユーザーの一意の ID と、通常はユーザーの名前の両方が含まれます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-124">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="e5b9a-125">メッセージのテキストには、同様`<at>@John Smith<at>`の説明も含まれます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-125">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="e5b9a-126">ただし、ユーザーに関する情報を取得するために、メッセージ内のテキストに依存しないようにしてください。メッセージを送信するユーザーが変更を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-126">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="e5b9a-127">代わりに、 `entities`オブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-127">Instead, use the `entities` object.</span></span>

<span data-ttu-id="e5b9a-128">メッセージ内のすべてのメンションを取得するに`GetMentions`は、オブジェクトの`Mention`配列を返す Bot ビルダー SDK の関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-128">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="e5b9a-129">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e5b9a-129">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="e5b9a-130">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="e5b9a-130">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="e5b9a-131">JSON</span><span class="sxs-lookup"><span data-stu-id="e5b9a-131">JSON</span></span>](#tab/json)

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

# <a name="pythontabpython"></a>[<span data-ttu-id="e5b9a-132">Python</span><span class="sxs-lookup"><span data-stu-id="e5b9a-132">Python</span></span>](#tab/python)

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

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="e5b9a-133">メッセージにメンションを追加する</span><span class="sxs-lookup"><span data-stu-id="e5b9a-133">Adding mentions to your messages</span></span>

<span data-ttu-id="e5b9a-134">Bot は、チャネルに投稿されたメッセージに他のユーザーを伝えます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-134">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="e5b9a-135">これを行うには、メッセージで次の操作を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-135">To do this, your message must do the following:</span></span>

<span data-ttu-id="e5b9a-136">オブジェクト`Mention`には、次の2つのプロパティを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-136">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="e5b9a-137">メッセージテキストに<at>@username</at>を含める</span><span class="sxs-lookup"><span data-stu-id="e5b9a-137">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="e5b9a-138">エンティティのコレクション内に、メンションオブジェクトを含めます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-138">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="e5b9a-139">Bot フレームワーク SDK は、ヘルパーメソッドとオブジェクトを提供して、メンションを簡単に作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-139">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="e5b9a-140">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e5b9a-140">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="e5b9a-141">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="e5b9a-141">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="e5b9a-142">JSON</span><span class="sxs-lookup"><span data-stu-id="e5b9a-142">JSON</span></span>](#tab/json)

<span data-ttu-id="e5b9a-143">配列内のオブジェクトのフィールドは、 `text`メッセージ\*\* `text`フィールドの一部に正確に一致している必要があります。 `entities`</span><span class="sxs-lookup"><span data-stu-id="e5b9a-143">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="e5b9a-144">そうでない場合、メンションは無視されます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-144">If it does not, the mention will be ignored.</span></span>

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

# <a name="pythontabpython"></a>[<span data-ttu-id="e5b9a-145">Python</span><span class="sxs-lookup"><span data-stu-id="e5b9a-145">Python</span></span>](#tab/python)

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

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="e5b9a-146">インストール時にメッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="e5b9a-146">Sending a message on installation</span></span>

<span data-ttu-id="e5b9a-147">Bot がグループまたはチームに最初に追加されたときに、それを紹介するメッセージを送信すると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-147">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="e5b9a-148">このメッセージには、bot の機能の簡単な説明とその使用方法が記載されています。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-148">The message should provide a brief description of the bot’s features, and how to use them.</span></span> <span data-ttu-id="e5b9a-149">`conversationUpdate`イベントをイベントにサブスクライブするには`teamMemberAdded` 、eventType を使用します。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-149">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="e5b9a-150">新しいチームメンバーが追加されたときにイベントが送信されるため、追加された新しいメンバーが bot であるかどうかを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-150">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="e5b9a-151">詳細については、「[新しいチームメンバーへのウェルカムメッセージの送信](~/bots/how-to/conversations/send-proactive-messages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-151">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="e5b9a-152">Bot が追加されたときに、チームの各メンバーに個人メッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-152">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="e5b9a-153">これを行うには、チーム名簿を取得して、各ユーザーに直接メッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-153">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="e5b9a-154">次の状況では、メッセージを送信することはお勧めしません。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-154">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="e5b9a-155">チームは大規模です (ただし、100メンバーよりも大きいなど)。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-155">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="e5b9a-156">Bot が "spammy" と表示されている可能性があります。これを追加したユーザーは、ウェルカムメッセージが表示されるすべてのユーザーに bot の価値提案を明確に伝えない限り、苦情を受けることがあります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-156">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="e5b9a-157">Bot は、最初にグループまたはチャネルで言及されます (チームに最初に追加されるものではありません)。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-157">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="e5b9a-158">グループまたはチャネルの名前が変更された</span><span class="sxs-lookup"><span data-stu-id="e5b9a-158">A group or channel is renamed</span></span>
* <span data-ttu-id="e5b9a-159">チームメンバーがグループまたはチャネルに追加される</span><span class="sxs-lookup"><span data-stu-id="e5b9a-159">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="e5b9a-160">詳細情報</span><span class="sxs-lookup"><span data-stu-id="e5b9a-160">Learn more</span></span>

<span data-ttu-id="e5b9a-161">Bot は、インストールされているグループチャットまたはチームに関する追加情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-161">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="e5b9a-162">Bot で利用できるその他の Api については、「 [teams コンテキストを取得](~/bots/how-to/get-teams-context.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-162">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="e5b9a-163">Bot がサブスクライブして応答できる追加のイベントもあります。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-163">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="e5b9a-164">詳細については、「[会話イベントを購読](~/bots/how-to/conversations/subscribe-to-conversation-events.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e5b9a-164">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
