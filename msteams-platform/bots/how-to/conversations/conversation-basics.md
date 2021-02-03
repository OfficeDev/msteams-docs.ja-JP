---
title: 会話の基本
author: clearab
description: Microsoft Teams ボットと会話する方法
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6f7e7a4d1be08126c96dff07ddbc3e1156700a90
ms.sourcegitcommit: 94ad961ecd002805b4e0424601d1c0ec191ff376
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "50075694"
---
# <a name="conversation-basics"></a><span data-ttu-id="9e6c4-103">会話の基本</span><span class="sxs-lookup"><span data-stu-id="9e6c4-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="9e6c4-104">会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="9e6c4-105">Teams には、次の 3 種類の会話 (スコープとも呼ばれる) があります。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-105">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="9e6c4-106">`teams` チャネル会話とも呼ばれる、チャネルのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-106">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="9e6c4-107">`personal` ボットと 1 人のユーザーの会話。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-107">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="9e6c4-108">`groupChat` ボットと 2 人以上のユーザーの間でチャットします。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-108">`groupChat` Chat between a bot and two or more users.</span></span> <span data-ttu-id="9e6c4-109">また、会議チャットでボットを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-109">Also enables your bot in meeting chats.</span></span>

<span data-ttu-id="9e6c4-110">ボットの動作は、関連する会話の種類によって少し異なります。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="9e6c4-111">チャネルとグループ チャットの会話のボットでは、ユーザーがボットを @メンションしてチャネルで呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-111">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="9e6c4-112">1 対 1 の会話のボットには@ メンションは必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-112">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="9e6c4-113">ユーザーによって送信されたすべてのメッセージがボットにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-113">All messages sent by the user will be routed to your bot.</span></span>

<span data-ttu-id="9e6c4-114">特定のスコープでボットを有効にするには、そのスコープをアプリ マニフェストに [追加します](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-114">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="9e6c4-115">アクティビティ</span><span class="sxs-lookup"><span data-stu-id="9e6c4-115">Activities</span></span>

<span data-ttu-id="9e6c4-116">各メッセージは `messageType: message` 型の `Activity` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-116">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="9e6c4-117">ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-117">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="9e6c4-118">ボットがメッセージを調べて種類を特定し、それに応じて応答します。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-118">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="9e6c4-119">基本的な会話は、ボットが Teams や他のチャネルと通信するための単一の REST API である Bot Framework Connector を通じて処理されます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-119">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="9e6c4-120">Bot Builder SDK は、この API への簡単なアクセス、会話のフローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-120">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="9e6c4-121">メッセージを受信する</span><span class="sxs-lookup"><span data-stu-id="9e6c4-121">Receive a message</span></span>

<span data-ttu-id="9e6c4-122">テキスト メッセージを受信するには、`Activity` オブジェクトの `Text` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-122">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="9e6c4-123">ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `Activity` を使用して、1 つのメッセージ要求を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-123">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="9e6c4-124">次のコードは例を示しています。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-124">The code below shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9e6c4-125">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9e6c4-125">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="9e6c4-126">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9e6c4-126">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="9e6c4-127">Python</span><span class="sxs-lookup"><span data-stu-id="9e6c4-127">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="9e6c4-128">JSON</span><span class="sxs-lookup"><span data-stu-id="9e6c4-128">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="9e6c4-129">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="9e6c4-129">Send a message</span></span>

<span data-ttu-id="9e6c4-130">テキスト メッセージを送信するには、送信する文字列をアクティビティとして指定します。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-130">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="9e6c4-131">ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `SendActivityAsync` メソッドを使用して、1 つのメッセージ応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-131">In the bot's activity handlers, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="9e6c4-132">オブジェクトのメソッドを使用して、一 `SendActivitiesAsync` 度に複数の応答を送信できます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-132">You can also use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="9e6c4-133">次のコードは、誰かが会話に追加されたときにメッセージを送信する例を示しています</span><span class="sxs-lookup"><span data-stu-id="9e6c4-133">The code below shows an example of sending a message when someone is added to a conversation</span></span>  

# <a name="cnet"></a>[<span data-ttu-id="9e6c4-134">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9e6c4-134">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="9e6c4-135">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9e6c4-135">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="9e6c4-136">Python</span><span class="sxs-lookup"><span data-stu-id="9e6c4-136">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="9e6c4-137">JSON</span><span class="sxs-lookup"><span data-stu-id="9e6c4-137">JSON</span></span>](#tab/json)

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

## <a name="teams-channel-data"></a><span data-ttu-id="9e6c4-138">Teams チャネル データ</span><span class="sxs-lookup"><span data-stu-id="9e6c4-138">Teams channel data</span></span>

<span data-ttu-id="9e6c4-139">オブジェクトには Teams 固有の情報が含まれているので、チームとチャネルの ID の確定的 `channelData` なソースです。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-139">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="9e6c4-140">ローカル ストレージのキーとしてこれらの ID をキャッシュして使用する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-140">You may need to cache and use these ids as keys for local storage.</span></span> <span data-ttu-id="9e6c4-141">SDK では通常、オブジェクトから重要な情報を取り出してアクセスしやすくしますが、いつでもオブジェクトの元の情報に `TeamsActivityHandler` `channelData` アクセス `turnContext` できます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-141">The `TeamsActivityHandler` in the SDK will typically pull out important information from the `channelData` object to make it more easily accessible, however you can always access the original information from the `turnContext` object.</span></span>

<span data-ttu-id="9e6c4-142">オブジェクトはチャネルの外部で行うので、個人の会話の `channelData` メッセージには含まれません。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-142">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="9e6c4-143">ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-143">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="9e6c4-144">`eventType` Teams イベントの種類:チャネル変更イベントの場合 [にのみ渡されます。](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="9e6c4-144">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="9e6c4-145">`tenant.id` Azure Active Directory テナント ID;すべてのコンテキストで渡される</span><span class="sxs-lookup"><span data-stu-id="9e6c4-145">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="9e6c4-146">`team` チャネル コンテキストでのみ渡されます。個人用チャットでは渡されます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-146">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="9e6c4-147">`id` チャネルの GUID</span><span class="sxs-lookup"><span data-stu-id="9e6c4-147">`id` GUID for the channel</span></span>
  * <span data-ttu-id="9e6c4-148">`name` チームの名前。チームの名前変更イベントの場合 [にのみ渡されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="9e6c4-148">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="9e6c4-149">`channel` ボットが言及されている場合、またはボットが追加されたチームのチャネルのイベントに対して、チャネル コンテキストでのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-149">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="9e6c4-150">`id` チャネルの GUID</span><span class="sxs-lookup"><span data-stu-id="9e6c4-150">`id` GUID for the channel</span></span>
  * <span data-ttu-id="9e6c4-151">`name` チャネル名チャネル変更イベントの場合 [にのみ渡されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-151">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="9e6c4-152">`channelData.teamsTeamId` 非推奨。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-152">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="9e6c4-153">このプロパティは、下位互換性のためにのみ含まれています。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-153">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="9e6c4-154">`channelData.teamsChannelId` 非推奨。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-154">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="9e6c4-155">このプロパティは、下位互換性のためにのみ含まれています。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-155">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="9e6c4-156">channelData オブジェクトの例 (channelCreated イベント)</span><span class="sxs-lookup"><span data-stu-id="9e6c4-156">Example channelData object (channelCreated event)</span></span>

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

## <a name="message-content"></a><span data-ttu-id="9e6c4-157">メッセージの内容</span><span class="sxs-lookup"><span data-stu-id="9e6c4-157">Message content</span></span>

<span data-ttu-id="9e6c4-158">ボットは、リッチ テキスト、画像、カードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-158">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="9e6c4-159">ユーザーは、リッチ テキストと画像をボットに送信できます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-159">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="9e6c4-160">フォーマット</span><span class="sxs-lookup"><span data-stu-id="9e6c4-160">Format</span></span>    | <span data-ttu-id="9e6c4-161">ユーザーからボットへ</span><span class="sxs-lookup"><span data-stu-id="9e6c4-161">From user to bot</span></span> | <span data-ttu-id="9e6c4-162">ボットからユーザーへ</span><span class="sxs-lookup"><span data-stu-id="9e6c4-162">From bot to user</span></span> | <span data-ttu-id="9e6c4-163">Notes</span><span class="sxs-lookup"><span data-stu-id="9e6c4-163">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="9e6c4-164">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="9e6c4-164">Rich text</span></span> | <span data-ttu-id="9e6c4-165">✔</span><span class="sxs-lookup"><span data-stu-id="9e6c4-165">✔</span></span>                | <span data-ttu-id="9e6c4-166">✔</span><span class="sxs-lookup"><span data-stu-id="9e6c4-166">✔</span></span>                |                                                                                         |
| <span data-ttu-id="9e6c4-167">ピクチャ</span><span class="sxs-lookup"><span data-stu-id="9e6c4-167">Pictures</span></span>  | <span data-ttu-id="9e6c4-168">✔</span><span class="sxs-lookup"><span data-stu-id="9e6c4-168">✔</span></span>                | <span data-ttu-id="9e6c4-169">✔</span><span class="sxs-lookup"><span data-stu-id="9e6c4-169">✔</span></span>                | <span data-ttu-id="9e6c4-170">最大 1024×1024 および 1 MB (PNG、JPEG、または GIF 形式)。アニメーション GIF はサポートされていません</span><span class="sxs-lookup"><span data-stu-id="9e6c4-170">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="9e6c4-171">カード</span><span class="sxs-lookup"><span data-stu-id="9e6c4-171">Cards</span></span>     | <span data-ttu-id="9e6c4-172">✖</span><span class="sxs-lookup"><span data-stu-id="9e6c4-172">✖</span></span>                | <span data-ttu-id="9e6c4-173">✔</span><span class="sxs-lookup"><span data-stu-id="9e6c4-173">✔</span></span>                | <span data-ttu-id="9e6c4-174">サポートされている [カードについては、「Teams カード リファレンス](~/task-modules-and-cards/cards/cards-reference.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-174">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="9e6c4-175">Emojis</span><span class="sxs-lookup"><span data-stu-id="9e6c4-175">Emojis</span></span>    | <span data-ttu-id="9e6c4-176">✖</span><span class="sxs-lookup"><span data-stu-id="9e6c4-176">✖</span></span>                | <span data-ttu-id="9e6c4-177">✔</span><span class="sxs-lookup"><span data-stu-id="9e6c4-177">✔</span></span>                | <span data-ttu-id="9e6c4-178">Teams は現在 UTF-16 を介して絵文字をサポートしています (顔のくびくびくをする U+1F600 など)</span><span class="sxs-lookup"><span data-stu-id="9e6c4-178">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="9e6c4-179">メッセージへの通知の追加</span><span class="sxs-lookup"><span data-stu-id="9e6c4-179">Adding notifications to your message</span></span>

<span data-ttu-id="9e6c4-180">通知は、作業している作業に関連する新しいタスク、メンション、コメント、またはアクティビティ フィードに通知を挿入して確認する必要があるタスク、メンション、コメントについてユーザーに警告します。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span></span> <span data-ttu-id="9e6c4-181">objects プロパティを true に設定することで、ボット メッセージからトリガーする `TeamsChannelData` `Notification.Alert` 通知を設定できます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-181">You can set notifications to trigger from your bot message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="9e6c4-182">通知が発生するかどうかは、最終的には個々のユーザーの Teams 設定に依存し、これらの設定をプログラムで上書きすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-182">Whether or not a notification is raised will ultimately depend on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="9e6c4-183">通知の種類は、バナー、またはバナーとメールの両方です。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-183">The type of notification will be either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9e6c4-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9e6c4-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="9e6c4-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9e6c4-185">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="9e6c4-186">Python</span><span class="sxs-lookup"><span data-stu-id="9e6c4-186">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="9e6c4-187">JSON</span><span class="sxs-lookup"><span data-stu-id="9e6c4-187">JSON</span></span>](#tab/json)

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

## <a name="picture-messages"></a><span data-ttu-id="9e6c4-188">画像メッセージ</span><span class="sxs-lookup"><span data-stu-id="9e6c4-188">Picture messages</span></span>

<span data-ttu-id="9e6c4-189">画像は、メッセージに添付ファイルを追加することで送信されます。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-189">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="9e6c4-190">添付ファイルの詳細については、Bot Framework のドキュメント [を参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-190">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="9e6c4-191">画像は、PNG、JPEG、GIF 形式で最大 1024×1024 および 1 MB です。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-191">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="9e6c4-192">XML を使用して各イメージの高さと幅を指定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-192">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="9e6c4-193">Markdown を使用する場合、画像サイズの既定値は 256×256 です。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-193">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="9e6c4-194">例:</span><span class="sxs-lookup"><span data-stu-id="9e6c4-194">For example:</span></span>

* <span data-ttu-id="9e6c4-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="9e6c4-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="9e6c4-196">使用しない - `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="9e6c4-196">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="code-sample"></a><span data-ttu-id="9e6c4-197">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="9e6c4-197">Code sample</span></span>
|<span data-ttu-id="9e6c4-198">**サンプルの名前**</span><span class="sxs-lookup"><span data-stu-id="9e6c4-198">**Sample name**</span></span> | <span data-ttu-id="9e6c4-199">**説明**</span><span class="sxs-lookup"><span data-stu-id="9e6c4-199">**Description**</span></span> | <span data-ttu-id="9e6c4-200">**.NETCore**</span><span class="sxs-lookup"><span data-stu-id="9e6c4-200">**.NETCore**</span></span> | <span data-ttu-id="9e6c4-201">**Javascript**</span><span class="sxs-lookup"><span data-stu-id="9e6c4-201">**Javascript**</span></span> | <span data-ttu-id="9e6c4-202">**Python**</span><span class="sxs-lookup"><span data-stu-id="9e6c4-202">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="9e6c4-203">Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="9e6c4-203">Teams Conversation Bot</span></span> | <span data-ttu-id="9e6c4-204">メッセージングと会話イベントの処理。</span><span class="sxs-lookup"><span data-stu-id="9e6c4-204">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="9e6c4-205">View</span><span class="sxs-lookup"><span data-stu-id="9e6c4-205">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="9e6c4-206">View</span><span class="sxs-lookup"><span data-stu-id="9e6c4-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="9e6c4-207">View</span><span class="sxs-lookup"><span data-stu-id="9e6c4-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="9e6c4-208">次の手順</span><span class="sxs-lookup"><span data-stu-id="9e6c4-208">Next steps</span></span>

* [<span data-ttu-id="9e6c4-209">プロアクティブ メッセージの送信</span><span class="sxs-lookup"><span data-stu-id="9e6c4-209">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="9e6c4-210">会話イベントにサブスクライブする</span><span class="sxs-lookup"><span data-stu-id="9e6c4-210">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
