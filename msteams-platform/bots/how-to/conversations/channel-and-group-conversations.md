---
title: ボットとのチャネルとグループの会話
author: clearab
description: チャネルまたはグループ チャットでボットのメッセージを送信、受信、および処理する方法。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: ef5cf8464fa0e93d5ea3840003a2b0c04a4a5ef5
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631000"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a><span data-ttu-id="b7f6b-103">ボットとのチャネルチャットとグループ チャットの会話</span><span class="sxs-lookup"><span data-stu-id="b7f6b-103">Channel and group chat conversations with a bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="b7f6b-104">チームまたはグループ チャットMicrosoft Teamsボットをインストールするには、ボットに `teams` または `groupchat` スコープを追加します。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-104">To install the Microsoft Teams bot in a team or group chat, add the `teams` or `groupchat` scope to your bot.</span></span> <span data-ttu-id="b7f6b-105">これにより、会話のすべてのメンバーがボットと対話できるようになります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="b7f6b-106">ボットをインストールすると、会話に関するメタデータ (会話メンバーの一覧など) にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-106">After the bot is installed, it has access to metadata about the conversation, such as the list of conversation members.</span></span> <span data-ttu-id="b7f6b-107">また、チームにインストールすると、ボットは、そのチームに関する詳細とチャネルの完全なリストにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-107">Also, when it is installed in a team, the bot has access to details about that team and the full list of channels.</span></span>

<span data-ttu-id="b7f6b-108">グループまたはチャネル内のボットは、グループまたはチャネルに関する情報が記載されている場合にのみ@botname。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-108">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="b7f6b-109">会話に送信された他のメッセージは受信しません。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-109">They do not receive any other messages sent to the conversation.</span></span> <span data-ttu-id="b7f6b-110">ボットは直接 @メンションされる必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-110">The bot must be @mentioned directly.</span></span> <span data-ttu-id="b7f6b-111">チームまたはチャネルが言及された場合、またはボットからメッセージに返信しても、ボットはメッセージを受信@mentioningされません。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-111">Your bot does not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

> [!NOTE]
> <span data-ttu-id="b7f6b-112">この機能は現在、パブリック開発者 [プレビューでのみ利用](../../../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-112">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>
>
> <span data-ttu-id="b7f6b-113">リソース固有の同意 (RSC) を使用して、ボットは、インストールされているチーム内のすべてのチャネル メッセージを受信@mentioned。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-113">Using resource-specific consent (RSC), bots can receive all channel messages in teams that it is installed in without being @mentioned.</span></span> <span data-ttu-id="b7f6b-114">詳細については [、「RSC を使用してすべてのチャネル メッセージを受信する」を参照してください](channel-messages-with-rsc.md)。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-114">For more information, see [receive all channel messages with RSC](channel-messages-with-rsc.md).</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="b7f6b-115">デザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="b7f6b-115">Design guidelines</span></span>

<span data-ttu-id="b7f6b-116">個人用チャットとは異なり、グループ チャットやチャネルでは、ボットが簡単な概要を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-116">Unlike personal chats, in group chats and channels, your bot must provide a quick introduction.</span></span> <span data-ttu-id="b7f6b-117">これらのボットの設計ガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-117">You must follow these and more bot design guidelines.</span></span> <span data-ttu-id="b7f6b-118">ボットを設計する方法の詳細については、「Teamsチャットでボットの会話を設計する方法[」を参照してください](~/bots/design/bots.md)。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-118">For more information on how to design bots in Teams, see [how to design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

<span data-ttu-id="b7f6b-119">これで、新しい会話スレッドを作成し、チャネル内の異なる会話を簡単に管理できます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-119">Now, you can create new conversation threads and easily manage different conversations in channels.</span></span>

## <a name="create-new-conversation-threads"></a><span data-ttu-id="b7f6b-120">新しいスレッドの作成</span><span class="sxs-lookup"><span data-stu-id="b7f6b-120">Create new conversation threads</span></span>

<span data-ttu-id="b7f6b-121">ボットがチームにインストールされている場合は、既存のスレッドに返信するのではなく、新しいスレッドを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-121">When your bot is installed in a team, you must create a new conversation thread rather than reply to an existing one.</span></span> <span data-ttu-id="b7f6b-122">2 つの会話を区別することは困難な場合があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-122">At times it is difficult to differentiate between two conversations.</span></span> <span data-ttu-id="b7f6b-123">スレッド化された会話の場合は、チャネルでさまざまな会話を整理して管理する方が簡単です。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-123">If the conversation is threaded, it is easier to organize and manage different conversations in channels.</span></span> <span data-ttu-id="b7f6b-124">これは、プロアクティブ メッセージング [の形式です](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-124">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="b7f6b-125">次に、オブジェクトを使用してメンションを取得し、オブジェクトを使用して `entities` メッセージにメンションを追加 `Mention` できます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-125">Next, you can retrieve mentions using the `entities` object and add mentions to your messages using the `Mention` object.</span></span>

## <a name="work-with-mentions"></a><span data-ttu-id="b7f6b-126">メンションを使用する</span><span class="sxs-lookup"><span data-stu-id="b7f6b-126">Work with mentions</span></span>

<span data-ttu-id="b7f6b-127">グループまたはチャネルからボットに送信されるメッセージには、@mentionに名前が含まれているメッセージが含まれる。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-127">Every message to your bot from a group or channel contains an @mention with its name in the message text.</span></span> <span data-ttu-id="b7f6b-128">ボットは、メッセージに記載されている他のユーザーを取得し、送信するメッセージにメンションを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-128">Your bot can also retrieve other users mentioned in a message and add mentions to any messages it sends.</span></span>

<span data-ttu-id="b7f6b-129">また、ボットが受信したメッセージ@mentionsコンテンツから削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-129">You must also strip out the @mentions from the content of the message your bot receives.</span></span>

### <a name="retrieve-mentions"></a><span data-ttu-id="b7f6b-130">メンションの取得</span><span class="sxs-lookup"><span data-stu-id="b7f6b-130">Retrieve mentions</span></span>

<span data-ttu-id="b7f6b-131">メンションはペイロード内のオブジェクトに返され、ユーザーの一意の ID と、指定したユーザーの `entities` 名前の両方が含まれます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-131">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and the name of the user mentioned.</span></span> <span data-ttu-id="b7f6b-132">メッセージのテキストには、次のようなメンションも含まれます `<at>@John Smith<at>` 。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-132">The text of the message also includes the mention, such as `<at>@John Smith<at>`.</span></span> <span data-ttu-id="b7f6b-133">ただし、メッセージ内のテキストを使用して、ユーザーに関する情報を取得しない。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-133">However, do not rely on the text in the message to retrieve any information about the user.</span></span> <span data-ttu-id="b7f6b-134">メッセージを送信するユーザーがメッセージを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-134">It is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="b7f6b-135">したがって、オブジェクトを使用 `entities` します。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-135">Therefore, use the `entities` object.</span></span>

<span data-ttu-id="b7f6b-136">メッセージ内のすべてのメンションを取得するには、Bot Builder SDK で関数を呼び出し、オブジェクトの `GetMentions` 配列を返 `Mention` します。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-136">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK, which returns an array of `Mention` objects.</span></span>

<span data-ttu-id="b7f6b-137">次のコードは、メンションを取得する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-137">The following code shows an example of retrieving mentions:</span></span>

# <a name="c"></a>[<span data-ttu-id="b7f6b-138">C#</span><span class="sxs-lookup"><span data-stu-id="b7f6b-138">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="b7f6b-139">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b7f6b-139">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="b7f6b-140">JSON</span><span class="sxs-lookup"><span data-stu-id="b7f6b-140">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="b7f6b-141">Python</span><span class="sxs-lookup"><span data-stu-id="b7f6b-141">Python</span></span>](#tab/python)

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

### <a name="add-mentions-to-your-messages"></a><span data-ttu-id="b7f6b-142">メッセージにメンションを追加する</span><span class="sxs-lookup"><span data-stu-id="b7f6b-142">Add mentions to your messages</span></span>

<span data-ttu-id="b7f6b-143">ボットは、チャネルに投稿されたメッセージで他のユーザーに言及できます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-143">Your bot can mention other users in messages posted into channels.</span></span>

<span data-ttu-id="b7f6b-144">オブジェクト `Mention` には、次の 2 つのプロパティを使用して設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-144">The `Mention` object has two properties that you must set using the following:</span></span>

* <span data-ttu-id="b7f6b-145">メッセージ <at>の@username</at> にデータを含める。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-145">Include <at>@username</at> in the message text.</span></span>
* <span data-ttu-id="b7f6b-146">エンティティ コレクション内にメンション オブジェクトを含める。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-146">Include the mention object inside the entities collection.</span></span>

<span data-ttu-id="b7f6b-147">Bot Framework SDK には、メンションを作成するヘルパー メソッドとオブジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-147">The Bot Framework SDK provides helper methods and objects to create mentions.</span></span>

<span data-ttu-id="b7f6b-148">次のコードは、メッセージにメンションを追加する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-148">The following code shows an example of adding mentions to your messages:</span></span>

# <a name="c"></a>[<span data-ttu-id="b7f6b-149">C#</span><span class="sxs-lookup"><span data-stu-id="b7f6b-149">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="b7f6b-150">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b7f6b-150">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="b7f6b-151">JSON</span><span class="sxs-lookup"><span data-stu-id="b7f6b-151">JSON</span></span>](#tab/json)

<span data-ttu-id="b7f6b-152">配列 `text` 内のオブジェクトのフィールドは、メッセージ `entities` フィールドの一部と一致している必要 `text` があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-152">The `text` field in the object in the `entities` array must match a portion of the message `text` field.</span></span> <span data-ttu-id="b7f6b-153">指定しない場合、メンションは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-153">If it does not, the mention is ignored.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="b7f6b-154">Python</span><span class="sxs-lookup"><span data-stu-id="b7f6b-154">Python</span></span>](#tab/python)

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

<span data-ttu-id="b7f6b-155">これで、ボットが最初にインストールまたはグループまたはチームに追加された場合に、概要メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-155">Now you can send an introduction message when your bot is first installed or added to a group or team.</span></span>

## <a name="send-a-message-on-installation"></a><span data-ttu-id="b7f6b-156">インストール時にメッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="b7f6b-156">Send a message on installation</span></span>

<span data-ttu-id="b7f6b-157">ボットが最初にグループまたはチームに追加された場合は、紹介メッセージを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-157">When your bot is first added to the group or team, an introduction message must be sent.</span></span> <span data-ttu-id="b7f6b-158">メッセージには、ボットの機能とボットの機能の使い方について簡単に説明する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-158">The message must provide a brief description of the bot's features and how to use them.</span></span> <span data-ttu-id="b7f6b-159">eventType を使用して `conversationUpdate` イベントをサブスクライブする `teamMemberAdded` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-159">You must subscribe to the `conversationUpdate` event with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="b7f6b-160">イベントは、新しいチーム メンバーが追加された場合に送信されます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-160">The event is sent when any new team member is added.</span></span> <span data-ttu-id="b7f6b-161">追加された新しいメンバーがボットか確認します。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-161">Check if the new member added is the bot.</span></span> <span data-ttu-id="b7f6b-162">詳細については、「ウェルカム [メッセージを新しいチーム メンバーに送信する」を参照してください](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-162">For more information, see [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="b7f6b-163">ボットが追加された場合、各チーム メンバーに個人メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-163">Send a personal message to each team member when the bot is added.</span></span> <span data-ttu-id="b7f6b-164">これを行うには、チーム名簿を取得し、各ユーザーに直接メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-164">To do this, get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="b7f6b-165">次の場合は、メッセージを送信しない。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-165">Do not send a message in the following cases:</span></span>

* <span data-ttu-id="b7f6b-166">チームは大きい (たとえば、100 人を超えるメンバー) です。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-166">The team is large, for example, larger than 100 members.</span></span> <span data-ttu-id="b7f6b-167">ボットはスパムと見なされ、追加したユーザーは苦情を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-167">Your bot can be seen as spam and the person who added it can get complaints.</span></span> <span data-ttu-id="b7f6b-168">ウェルカム メッセージを見たすべてのユーザーに、ボットの価値提案を明確に伝える必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-168">You must clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="b7f6b-169">ボットは、最初にチームに追加されるのではなく、グループまたはチャネルで最初に言及されます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-169">Your bot is first mentioned in a group or channel instead of being first added to a team.</span></span>
* <span data-ttu-id="b7f6b-170">グループまたはチャネルの名前が変更されます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-170">A group or channel is renamed.</span></span>
* <span data-ttu-id="b7f6b-171">チーム メンバーがグループまたはチャネルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="b7f6b-171">A team member is added to a group or channel.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a><span data-ttu-id="b7f6b-172">関連項目</span><span class="sxs-lookup"><span data-stu-id="b7f6b-172">See also</span></span>

[<span data-ttu-id="b7f6b-173">コンテキストTeams取得</span><span class="sxs-lookup"><span data-stu-id="b7f6b-173">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)

## <a name="next-step"></a><span data-ttu-id="b7f6b-174">次の手順</span><span class="sxs-lookup"><span data-stu-id="b7f6b-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b7f6b-175">会話イベントにサブスクライブする</span><span class="sxs-lookup"><span data-stu-id="b7f6b-175">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
