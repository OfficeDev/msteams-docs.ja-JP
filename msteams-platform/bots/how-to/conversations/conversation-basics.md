---
title: 会話の基本
description: Microsoft Teams ボットと会話する方法について説明します。
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 4eba22e9b29f5378dc03480ba5f6ba421f816eb3
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449508"
---
# <a name="conversation-basics"></a><span data-ttu-id="262c6-103">会話の基本</span><span class="sxs-lookup"><span data-stu-id="262c6-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="262c6-104">会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。</span><span class="sxs-lookup"><span data-stu-id="262c6-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="262c6-105">Teams には、スコープとも呼ばれる 3 種類の会話があります。</span><span class="sxs-lookup"><span data-stu-id="262c6-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="262c6-106">会話の種類</span><span class="sxs-lookup"><span data-stu-id="262c6-106">Conversation type</span></span> | <span data-ttu-id="262c6-107">説明</span><span class="sxs-lookup"><span data-stu-id="262c6-107">Description</span></span> |
| ------- | ----------- |
|  `teams` | <span data-ttu-id="262c6-108">チャネル会話とも呼ばれる、チャネルのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="262c6-108">Also called channel conversations, visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="262c6-109">ボットと 1 人のユーザーの会話。</span><span class="sxs-lookup"><span data-stu-id="262c6-109">Conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="262c6-110">ボットと 2 人以上のユーザーとのチャット。</span><span class="sxs-lookup"><span data-stu-id="262c6-110">Chat between a bot and two or more users.</span></span> <span data-ttu-id="262c6-111">また、会議チャットでボットを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="262c6-111">Also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="262c6-112">ボットの動作は、関係する会話の種類に応じて少し異なります。</span><span class="sxs-lookup"><span data-stu-id="262c6-112">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="262c6-113">チャネルチャットとグループ チャット会話のボットでは、チャネルでボットを呼び出す場合は、ユーザーがボットに @メンションする必要があります。</span><span class="sxs-lookup"><span data-stu-id="262c6-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="262c6-114">1 対 1 の会話のボットでは@メンションは必要ない。</span><span class="sxs-lookup"><span data-stu-id="262c6-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="262c6-115">ユーザーが送信したメッセージはすべてボットにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="262c6-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="262c6-116">特定のスコープでボットを有効にするには、そのスコープをアプリ マニフェスト [に追加します](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="262c6-116">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="262c6-117">アクティビティ</span><span class="sxs-lookup"><span data-stu-id="262c6-117">Activities</span></span>

<span data-ttu-id="262c6-118">各メッセージは `messageType: message` 型の `Activity` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="262c6-118">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="262c6-119">ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。</span><span class="sxs-lookup"><span data-stu-id="262c6-119">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="262c6-120">ボットはメッセージを調べて、その種類を特定し、それに応じて応答します。</span><span class="sxs-lookup"><span data-stu-id="262c6-120">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="262c6-121">基本的な会話は、単一の REST API である Bot Framework Connector を介して処理されます。</span><span class="sxs-lookup"><span data-stu-id="262c6-121">Basic conversations are handled through the Bot Framework Connector, a single REST API.</span></span> <span data-ttu-id="262c6-122">この API を使用すると、ボットは Teams や他のチャネルと通信できます。</span><span class="sxs-lookup"><span data-stu-id="262c6-122">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="262c6-123">ボット ビルダー SDK は、この API への簡単なアクセス、会話のフローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="262c6-123">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="262c6-124">メッセージを受信する</span><span class="sxs-lookup"><span data-stu-id="262c6-124">Receive a message</span></span>

<span data-ttu-id="262c6-125">テキスト メッセージを受信するには、`Activity` オブジェクトの `Text` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="262c6-125">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="262c6-126">ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `Activity` を使用して、1 つのメッセージ要求を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="262c6-126">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="262c6-127">次のコードは一例です。</span><span class="sxs-lookup"><span data-stu-id="262c6-127">The following code shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="262c6-128">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="262c6-128">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="262c6-129">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="262c6-129">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# <a name="python"></a>[<span data-ttu-id="262c6-130">Python</span><span class="sxs-lookup"><span data-stu-id="262c6-130">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="262c6-131">JSON</span><span class="sxs-lookup"><span data-stu-id="262c6-131">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="send-a-message"></a><span data-ttu-id="262c6-132">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="262c6-132">Send a message</span></span>

<span data-ttu-id="262c6-133">テキスト メッセージを送信するには、送信する文字列をアクティビティとして指定します。</span><span class="sxs-lookup"><span data-stu-id="262c6-133">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="262c6-134">ボットのアクティビティ ハンドラーで、turn context オブジェクトのメソッドを使用して 1 つの `SendActivityAsync` メッセージ応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="262c6-134">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="262c6-135">オブジェクトのメソッドを使用して `SendActivitiesAsync` 、複数の応答を一度に送信します。</span><span class="sxs-lookup"><span data-stu-id="262c6-135">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="262c6-136">次のコードは、誰かが会話に追加されたときにメッセージを送信する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="262c6-136">The following code shows an example of sending a message when someone is added to a conversation.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="262c6-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="262c6-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="262c6-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="262c6-138">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity('Hello and welcome!');
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="262c6-139">Python</span><span class="sxs-lookup"><span data-stu-id="262c6-139">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="262c6-140">JSON</span><span class="sxs-lookup"><span data-stu-id="262c6-140">JSON</span></span>](#tab/json)

```json
{
    "text": "hi",
    "textFormat": "plain",
    "type": "message",
    "timestamp": "2019-10-31T20:57:27.2347285Z",
    "localTimestamp": "2019-10-31T13:57:27.2347285-07:00",
    "id": "1572555447214",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1Xv-kvy4dKirR0rZfSF_kAVUzotoT1SXuEzkC9XGkuZng8YBw8qyu5uh4128fQRjlGgvEiRLx-0XP4KYMwcgdZw",
        "name": "Jane Doe",
        "aadObjectId": "df486eae-88fd-42a5-b45e-c581588186db"
    },
    "conversation": {
        "conversationType": "personal",
        "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "id": "a:1oAmWTVBBe9E0JrpGxauqNyx4CCE_iQf2ZuWon9D42722Fon3wYIpbhgbRChE3wgVS1Gwl9zS1pZy4FSu6-x1vGEq5KBQK-EbBgyPyeP_C-lbLBY3vxnGk9m9D_282jbg"
    },
    "recipient": {
        "id": "28:5baea8d1-d4ea-43a1-b101-882f4c8d9cb4",
        "name": "Imported Bot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Windows",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

> [!NOTE]
> <span data-ttu-id="262c6-141">メッセージの分割は、テキスト メッセージと添付ファイルが同じアクティビティ ペイロードで送信される場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="262c6-141">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="262c6-142">このアクティビティは、Microsoft Teams によって個別のアクティビティに分割され、1 つのアクティビティはテキスト メッセージだけで、もう 1 つは添付ファイルを持つアクティビティに分割されます。</span><span class="sxs-lookup"><span data-stu-id="262c6-142">This activity is split into separate activities by Microsoft Teams, one activity with just a text message and the other with an attachment.</span></span> <span data-ttu-id="262c6-143">アクティビティが分割されている間、メッセージ ID は応答で受信されません。これは、メッセージを事前に更新または [削除するために使用](~/bots/how-to/update-and-delete-bot-messages.md) されます。</span><span class="sxs-lookup"><span data-stu-id="262c6-143">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="262c6-144">メッセージの分割に応じてではなく、個別のアクティビティを送信する方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="262c6-144">It is recommended to send separate activities instead of depending on message splitting.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="262c6-145">Teams チャネル データ</span><span class="sxs-lookup"><span data-stu-id="262c6-145">Teams channel data</span></span>

<span data-ttu-id="262c6-146">オブジェクト `channelData` には Teams 固有の情報が含まれているので、チームとチャネルの ID の決定的なソースです。</span><span class="sxs-lookup"><span data-stu-id="262c6-146">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="262c6-147">これらの ID をローカル ストレージのキーとしてキャッシュして使用する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="262c6-147">You may need to cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="262c6-148">SDK では、通常、オブジェクトから重要な情報を引き出して、簡単 `TeamsActivityHandler` `channelData` にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="262c6-148">The `TeamsActivityHandler` in the SDK, typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="262c6-149">ただし、オブジェクトから元のデータにいつでもアクセス `turnContext` できます。</span><span class="sxs-lookup"><span data-stu-id="262c6-149">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="262c6-150">オブジェクトは、チャネルの外部で行なうので、個人の会話のメッセージ `channelData` には含まれません。</span><span class="sxs-lookup"><span data-stu-id="262c6-150">The `channelData` object is not included in messages in personal conversations, as these take place outside of any channel.</span></span>

<span data-ttu-id="262c6-151">ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="262c6-151">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="262c6-152">`eventType` Teams イベントの種類。チャネル変更イベントの場合 [にのみ渡されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="262c6-152">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="262c6-153">`tenant.id` すべてのコンテキストで渡される Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="262c6-153">`tenant.id` Azure Active Directory tenant ID, passed in all contexts.</span></span>
* <span data-ttu-id="262c6-154">`team` 個人チャットではなく、チャネル コンテキストでのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="262c6-154">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="262c6-155">`id` チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="262c6-155">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="262c6-156">`name` チームの名前。チームの名前変更イベントの場合 [にのみ渡されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="262c6-156">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="262c6-157">`channel` ボットが言及されている場合、またはボットが追加されたチームのチャネル内のイベントに対して、チャネル コンテキストでのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="262c6-157">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="262c6-158">`id` チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="262c6-158">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="262c6-159">`name` チャネル名。チャネル変更イベントの場合 [にのみ渡されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="262c6-159">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="262c6-160">`channelData.teamsTeamId` 非推奨です。</span><span class="sxs-lookup"><span data-stu-id="262c6-160">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="262c6-161">このプロパティは、下位互換性の場合にのみ含まれます。</span><span class="sxs-lookup"><span data-stu-id="262c6-161">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="262c6-162">`channelData.teamsChannelId` 非推奨です。</span><span class="sxs-lookup"><span data-stu-id="262c6-162">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="262c6-163">このプロパティは、下位互換性の場合にのみ含まれます。</span><span class="sxs-lookup"><span data-stu-id="262c6-163">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="262c6-164">channelData オブジェクトの例 (channelCreated イベント)</span><span class="sxs-lookup"><span data-stu-id="262c6-164">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

## <a name="message-content"></a><span data-ttu-id="262c6-165">メッセージの内容</span><span class="sxs-lookup"><span data-stu-id="262c6-165">Message content</span></span>

<span data-ttu-id="262c6-166">ボットはリッチ テキスト、画像、カードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="262c6-166">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="262c6-167">ユーザーは、リッチ テキストと画像をボットに送信できます。</span><span class="sxs-lookup"><span data-stu-id="262c6-167">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="262c6-168">フォーマット</span><span class="sxs-lookup"><span data-stu-id="262c6-168">Format</span></span>    | <span data-ttu-id="262c6-169">ユーザーからボットへ</span><span class="sxs-lookup"><span data-stu-id="262c6-169">From user to bot</span></span> | <span data-ttu-id="262c6-170">ボットからユーザーへ</span><span class="sxs-lookup"><span data-stu-id="262c6-170">From bot to user</span></span> | <span data-ttu-id="262c6-171">備考</span><span class="sxs-lookup"><span data-stu-id="262c6-171">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="262c6-172">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="262c6-172">Rich text</span></span> | <span data-ttu-id="262c6-173">✔</span><span class="sxs-lookup"><span data-stu-id="262c6-173">✔</span></span>                | <span data-ttu-id="262c6-174">✔</span><span class="sxs-lookup"><span data-stu-id="262c6-174">✔</span></span>                |                                                                                         |
| <span data-ttu-id="262c6-175">ピクチャ</span><span class="sxs-lookup"><span data-stu-id="262c6-175">Pictures</span></span>  | <span data-ttu-id="262c6-176">✔</span><span class="sxs-lookup"><span data-stu-id="262c6-176">✔</span></span>                | <span data-ttu-id="262c6-177">✔</span><span class="sxs-lookup"><span data-stu-id="262c6-177">✔</span></span>                | <span data-ttu-id="262c6-178">最大 1024× 1024 および 1 MB (PNG、JPEG、または GIF 形式)。アニメーション GIF はサポートされていません</span><span class="sxs-lookup"><span data-stu-id="262c6-178">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="262c6-179">カード</span><span class="sxs-lookup"><span data-stu-id="262c6-179">Cards</span></span>     | <span data-ttu-id="262c6-180">✖</span><span class="sxs-lookup"><span data-stu-id="262c6-180">✖</span></span>                | <span data-ttu-id="262c6-181">✔</span><span class="sxs-lookup"><span data-stu-id="262c6-181">✔</span></span>                | <span data-ttu-id="262c6-182">サポートされている [カードについては、「Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="262c6-182">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="262c6-183">絵文字</span><span class="sxs-lookup"><span data-stu-id="262c6-183">Emojis</span></span>    | <span data-ttu-id="262c6-184">✖</span><span class="sxs-lookup"><span data-stu-id="262c6-184">✖</span></span>                | <span data-ttu-id="262c6-185">✔</span><span class="sxs-lookup"><span data-stu-id="262c6-185">✔</span></span>                | <span data-ttu-id="262c6-186">Teams は現在、UTF-16 を使用して絵文字をサポートしています (顔にニヤリする場合は U+1F600 など)</span><span class="sxs-lookup"><span data-stu-id="262c6-186">Teams currently supports emojis through UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="262c6-187">メッセージへの通知の追加</span><span class="sxs-lookup"><span data-stu-id="262c6-187">Adding notifications to your message</span></span>

<span data-ttu-id="262c6-188">通知は、ユーザーのアクティビティ フィードに通知を挿入することで、ユーザーが取り組み、または確認する必要がある作業に関連する新しいタスク、メンション、コメントについてユーザーに通知します。</span><span class="sxs-lookup"><span data-stu-id="262c6-188">Notifications alert users about new tasks, mentions, and comments related to what they are working on or need to look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="262c6-189">objects プロパティを true に設定することで、ボット メッセージからトリガーする `TeamsChannelData` `Notification.Alert` 通知を設定できます。</span><span class="sxs-lookup"><span data-stu-id="262c6-189">You can set notifications to trigger from your bot-message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="262c6-190">通知が最終的に発生するかどうかは、個々のユーザーの Teams 設定によって異なります。これらの設定をプログラムで上書きすることはできません。</span><span class="sxs-lookup"><span data-stu-id="262c6-190">Whether or not a notification is raised ultimately depends on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="262c6-191">通知の種類は、バナー、またはバナーとメールの両方です。</span><span class="sxs-lookup"><span data-stu-id="262c6-191">The type of notification is either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="262c6-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="262c6-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="262c6-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="262c6-193">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="262c6-194">Python</span><span class="sxs-lookup"><span data-stu-id="262c6-194">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="262c6-195">JSON</span><span class="sxs-lookup"><span data-stu-id="262c6-195">JSON</span></span>](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

## <a name="picture-messages"></a><span data-ttu-id="262c6-196">ピクチャ メッセージ</span><span class="sxs-lookup"><span data-stu-id="262c6-196">Picture messages</span></span>

<span data-ttu-id="262c6-197">画像は、メッセージに添付ファイルを追加して送信されます。</span><span class="sxs-lookup"><span data-stu-id="262c6-197">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="262c6-198">添付ファイルの詳細については、Bot Framework のドキュメント [を参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。</span><span class="sxs-lookup"><span data-stu-id="262c6-198">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="262c6-199">画像は、PNG、JPEG、または GIF 形式× 1024、1024、1 MB までです。</span><span class="sxs-lookup"><span data-stu-id="262c6-199">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="262c6-200">アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="262c6-200">Animated GIF is not supported.</span></span>

<span data-ttu-id="262c6-201">XML を使用して、各イメージの高さと幅を常に指定します。</span><span class="sxs-lookup"><span data-stu-id="262c6-201">Always specify the height and width of each image by using XML.</span></span> <span data-ttu-id="262c6-202">Markdown では、イメージ サイズの既定値は 256 ×256 です。</span><span class="sxs-lookup"><span data-stu-id="262c6-202">In Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="262c6-203">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="262c6-203">For example:</span></span>

* <span data-ttu-id="262c6-204">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="262c6-204">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="262c6-205">使用しない - `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="262c6-205">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="262c6-206">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="262c6-206">Adaptive cards</span></span>

<span data-ttu-id="262c6-207">次のコードを使用して、単純なアダプティブ カードを送信します。</span><span class="sxs-lookup"><span data-stu-id="262c6-207">Use the following code to send a simple adaptive card:</span></span>

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

<span data-ttu-id="262c6-208">ボット内のカードとカードの詳細については、カードのドキュメント [を参照してください](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="262c6-208">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="262c6-209">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="262c6-209">Code sample</span></span>

|<span data-ttu-id="262c6-210">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="262c6-210">**Sample name**</span></span> | <span data-ttu-id="262c6-211">**説明**</span><span class="sxs-lookup"><span data-stu-id="262c6-211">**Description**</span></span> | <span data-ttu-id="262c6-212">**.NETCore**</span><span class="sxs-lookup"><span data-stu-id="262c6-212">**.NETCore**</span></span> | <span data-ttu-id="262c6-213">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="262c6-213">**JavaScript**</span></span> | <span data-ttu-id="262c6-214">**Python**</span><span class="sxs-lookup"><span data-stu-id="262c6-214">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="262c6-215">Teams の会話ボット</span><span class="sxs-lookup"><span data-stu-id="262c6-215">Teams Conversation Bot</span></span> | <span data-ttu-id="262c6-216">メッセージングおよび会話イベントの処理。</span><span class="sxs-lookup"><span data-stu-id="262c6-216">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="262c6-217">View</span><span class="sxs-lookup"><span data-stu-id="262c6-217">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="262c6-218">View</span><span class="sxs-lookup"><span data-stu-id="262c6-218">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="262c6-219">View</span><span class="sxs-lookup"><span data-stu-id="262c6-219">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="262c6-220">次の手順</span><span class="sxs-lookup"><span data-stu-id="262c6-220">Next steps</span></span>

* [<span data-ttu-id="262c6-221">プロアクティブ メッセージの送信</span><span class="sxs-lookup"><span data-stu-id="262c6-221">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="262c6-222">会話イベントにサブスクライブする</span><span class="sxs-lookup"><span data-stu-id="262c6-222">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
