---
title: ボットの会話内のメッセージ
description: ボットと会話する方法Microsoft Teamsします。
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 5b23e3b2548e3d0eab98fae73d37316063fe60c1
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058601"
---
# <a name="messages-in-bot-conversations"></a><span data-ttu-id="87a56-103">ボットの会話内のメッセージ</span><span class="sxs-lookup"><span data-stu-id="87a56-103">Messages in bot conversations</span></span>

<span data-ttu-id="87a56-104">会話内の各メッセージは、 `Activity` 型のオブジェクトです `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="87a56-104">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="87a56-105">ユーザーがメッセージを送信すると、Teamsボットにメッセージが投稿されます。</span><span class="sxs-lookup"><span data-stu-id="87a56-105">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="87a56-106">Teamsボットのメッセージング エンドポイントに JSON オブジェクトを送信します。</span><span class="sxs-lookup"><span data-stu-id="87a56-106">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="87a56-107">ボットはメッセージを調べて、その種類を特定し、それに応じて応答します。</span><span class="sxs-lookup"><span data-stu-id="87a56-107">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="87a56-108">基本的な会話は、単一の REST API である Bot Framework コネクタを介して処理されます。</span><span class="sxs-lookup"><span data-stu-id="87a56-108">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="87a56-109">この API を使用すると、ボットは他のチャネルTeams通信できます。</span><span class="sxs-lookup"><span data-stu-id="87a56-109">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="87a56-110">ボット ビルダー SDK には、次の機能があります。</span><span class="sxs-lookup"><span data-stu-id="87a56-110">The Bot Builder SDK provides the following features:</span></span>

* <span data-ttu-id="87a56-111">Bot Framework コネクタに簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="87a56-111">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="87a56-112">会話のフローと状態を管理するための追加機能。</span><span class="sxs-lookup"><span data-stu-id="87a56-112">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="87a56-113">自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法。</span><span class="sxs-lookup"><span data-stu-id="87a56-113">Simple ways to incorporate cognitive services, such as natural language processing (NLP).</span></span>

<span data-ttu-id="87a56-114">ボットはプロパティを使用Teamsメッセージを受信し、ユーザーに単一または複数のメッセージ `Text` 応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="87a56-114">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="87a56-115">メッセージを受信する</span><span class="sxs-lookup"><span data-stu-id="87a56-115">Receive a message</span></span>

<span data-ttu-id="87a56-116">テキスト メッセージを受信するには、`Activity` オブジェクトの `Text` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="87a56-116">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="87a56-117">ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `Activity` を使用して、1 つのメッセージ要求を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="87a56-117">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="87a56-118">次のコードは、メッセージを受信する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="87a56-118">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="87a56-119">C#</span><span class="sxs-lookup"><span data-stu-id="87a56-119">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="87a56-120">TypeScript</span><span class="sxs-lookup"><span data-stu-id="87a56-120">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="87a56-121">Python</span><span class="sxs-lookup"><span data-stu-id="87a56-121">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="87a56-122">JSON</span><span class="sxs-lookup"><span data-stu-id="87a56-122">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="87a56-123">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="87a56-123">Send a message</span></span>

<span data-ttu-id="87a56-124">テキスト メッセージを送信するには、送信する文字列をアクティビティとして指定します。</span><span class="sxs-lookup"><span data-stu-id="87a56-124">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="87a56-125">ボットのアクティビティ ハンドラーで、turn context オブジェクトのメソッドを使用して 1 つの `SendActivityAsync` メッセージ応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="87a56-125">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="87a56-126">オブジェクトのメソッドを使用して `SendActivitiesAsync` 、複数の応答を一度に送信します。</span><span class="sxs-lookup"><span data-stu-id="87a56-126">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span>

<span data-ttu-id="87a56-127">次のコードは、ユーザーが会話に追加された場合にメッセージを送信する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="87a56-127">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

# <a name="c"></a>[<span data-ttu-id="87a56-128">C#</span><span class="sxs-lookup"><span data-stu-id="87a56-128">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="87a56-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="87a56-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="87a56-130">Python</span><span class="sxs-lookup"><span data-stu-id="87a56-130">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="87a56-131">JSON</span><span class="sxs-lookup"><span data-stu-id="87a56-131">JSON</span></span>](#tab/json)

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
> <span data-ttu-id="87a56-132">メッセージの分割は、テキスト メッセージと添付ファイルが同じアクティビティ ペイロードで送信される場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="87a56-132">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="87a56-133">このアクティビティは、テキスト メッセージMicrosoft Teams添付ファイルを持つ別のアクティビティに分割されます。</span><span class="sxs-lookup"><span data-stu-id="87a56-133">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="87a56-134">アクティビティが分割されている間、メッセージ ID は応答で受信されません。これは、メッセージを事前に更新または [削除するために使用](~/bots/how-to/update-and-delete-bot-messages.md) されます。</span><span class="sxs-lookup"><span data-stu-id="87a56-134">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="87a56-135">メッセージの分割に応じてではなく、個別のアクティビティを送信する方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="87a56-135">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="87a56-136">ユーザーとボットの間で送信されるメッセージには、メッセージ内の内部チャネル データが含まれます。</span><span class="sxs-lookup"><span data-stu-id="87a56-136">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="87a56-137">このデータを使用すると、ボットはチャネルで適切に通信できます。</span><span class="sxs-lookup"><span data-stu-id="87a56-137">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="87a56-138">ボット ビルダー SDK を使用すると、メッセージ構造を変更できます。</span><span class="sxs-lookup"><span data-stu-id="87a56-138">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="87a56-139">Teamsチャネル データ</span><span class="sxs-lookup"><span data-stu-id="87a56-139">Teams channel data</span></span>

<span data-ttu-id="87a56-140">この `channelData` オブジェクトには、Teams固有の情報が含まれているので、チームとチャネルの ID の決定的なソースです。</span><span class="sxs-lookup"><span data-stu-id="87a56-140">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="87a56-141">必要に応じて、これらの ID をローカル ストレージのキーとしてキャッシュして使用できます。</span><span class="sxs-lookup"><span data-stu-id="87a56-141">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="87a56-142">`TeamsActivityHandler`SDK では、オブジェクトから重要な情報を取り出して、簡単 `channelData` にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="87a56-142">The `TeamsActivityHandler` in the SDK pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="87a56-143">ただし、オブジェクトから元のデータにいつでもアクセス `turnContext` できます。</span><span class="sxs-lookup"><span data-stu-id="87a56-143">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="87a56-144">オブジェクトは、チャネルの外部で行なうので、個人的な会話の `channelData` メッセージには含まれません。</span><span class="sxs-lookup"><span data-stu-id="87a56-144">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="87a56-145">ボットに `channelData` 送信されるアクティビティの一般的なオブジェクトには、次の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="87a56-145">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="87a56-146">`eventType`: Teams変更イベントの場合にのみ渡されるイベント[の種類を指定します](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="87a56-146">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="87a56-147">`tenant.id`: Azure Active Directoryで渡されるテナント ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="87a56-147">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="87a56-148">`team`: チャネル コンテキストでのみ渡されます。個人チャットでは渡されない。</span><span class="sxs-lookup"><span data-stu-id="87a56-148">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="87a56-149">`id`: チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="87a56-149">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="87a56-150">`name`: チーム名の変更イベントの場合にのみ渡された [チームの名前](~/bots/how-to/conversations/subscribe-to-conversation-events.md)です。</span><span class="sxs-lookup"><span data-stu-id="87a56-150">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="87a56-151">`channel`: ボットが言及されている場合、またはボットが追加されたチームのチャネル内のイベントに対して、チャネル コンテキストでのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="87a56-151">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="87a56-152">`id`: チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="87a56-152">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="87a56-153">`name`: チャネル変更イベントの場合にのみ渡 [されるチャネル名](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="87a56-153">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="87a56-154">`channelData.teamsTeamId`: 非推奨です。</span><span class="sxs-lookup"><span data-stu-id="87a56-154">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="87a56-155">このプロパティは、下位互換性のためにのみ含まれます。</span><span class="sxs-lookup"><span data-stu-id="87a56-155">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="87a56-156">`channelData.teamsChannelId`: 非推奨です。</span><span class="sxs-lookup"><span data-stu-id="87a56-156">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="87a56-157">このプロパティは、下位互換性のためにのみ含まれます。</span><span class="sxs-lookup"><span data-stu-id="87a56-157">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-or-channelcreated-event"></a><span data-ttu-id="87a56-158">channelData オブジェクトまたは channelCreated イベントの例</span><span class="sxs-lookup"><span data-stu-id="87a56-158">Example channelData object or channelCreated event</span></span>

<span data-ttu-id="87a56-159">次のコードは、channelData オブジェクトの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="87a56-159">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="87a56-160">ボットから受信またはボットに送信されるメッセージには、さまざまな種類のメッセージ コンテンツを含めできます。</span><span class="sxs-lookup"><span data-stu-id="87a56-160">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="87a56-161">メッセージの内容</span><span class="sxs-lookup"><span data-stu-id="87a56-161">Message content</span></span>

| <span data-ttu-id="87a56-162">Format</span><span class="sxs-lookup"><span data-stu-id="87a56-162">Format</span></span>    | <span data-ttu-id="87a56-163">ユーザーからボットへ</span><span class="sxs-lookup"><span data-stu-id="87a56-163">From user to bot</span></span> | <span data-ttu-id="87a56-164">ボットからユーザーへ</span><span class="sxs-lookup"><span data-stu-id="87a56-164">From bot to user</span></span> | <span data-ttu-id="87a56-165">Notes</span><span class="sxs-lookup"><span data-stu-id="87a56-165">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="87a56-166">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="87a56-166">Rich text</span></span> | <span data-ttu-id="87a56-167">✔</span><span class="sxs-lookup"><span data-stu-id="87a56-167">✔</span></span>                | <span data-ttu-id="87a56-168">✔</span><span class="sxs-lookup"><span data-stu-id="87a56-168">✔</span></span>                | <span data-ttu-id="87a56-169">ボットはリッチ テキスト、画像、カードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="87a56-169">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="87a56-170">ユーザーは、リッチ テキストと画像をボットに送信できます。</span><span class="sxs-lookup"><span data-stu-id="87a56-170">Users can send rich text and pictures to your bot.</span></span>                                                                                        |
| <span data-ttu-id="87a56-171">ピクチャ</span><span class="sxs-lookup"><span data-stu-id="87a56-171">Pictures</span></span>  | <span data-ttu-id="87a56-172">✔</span><span class="sxs-lookup"><span data-stu-id="87a56-172">✔</span></span>                | <span data-ttu-id="87a56-173">✔</span><span class="sxs-lookup"><span data-stu-id="87a56-173">✔</span></span>                | <span data-ttu-id="87a56-174">最大 1024 × 1024 および 1 MB (PNG、JPEG、または GIF 形式)。</span><span class="sxs-lookup"><span data-stu-id="87a56-174">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="87a56-175">アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="87a56-175">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="87a56-176">カード</span><span class="sxs-lookup"><span data-stu-id="87a56-176">Cards</span></span>     | <span data-ttu-id="87a56-177">✖</span><span class="sxs-lookup"><span data-stu-id="87a56-177">✖</span></span>                | <span data-ttu-id="87a56-178">✔</span><span class="sxs-lookup"><span data-stu-id="87a56-178">✔</span></span>                | <span data-ttu-id="87a56-179">サポートされているカード[についてはTeamsカード](~/task-modules-and-cards/cards/cards-reference.md)リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="87a56-179">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="87a56-180">絵文字</span><span class="sxs-lookup"><span data-stu-id="87a56-180">Emojis</span></span>    | <span data-ttu-id="87a56-181">✖</span><span class="sxs-lookup"><span data-stu-id="87a56-181">✖</span></span>                | <span data-ttu-id="87a56-182">✔</span><span class="sxs-lookup"><span data-stu-id="87a56-182">✔</span></span>                | <span data-ttu-id="87a56-183">Teams、顔にニヤリと笑う U+1F600 など、UTF-16 による絵文字がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="87a56-183">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="87a56-184">プロパティを使用してメッセージに通知を追加 `Notification.Alert` することもできます。</span><span class="sxs-lookup"><span data-stu-id="87a56-184">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="87a56-185">メッセージへの通知</span><span class="sxs-lookup"><span data-stu-id="87a56-185">Notifications to your message</span></span>

<span data-ttu-id="87a56-186">通知は、新しいタスク、メンション、コメントについてユーザーに通知します。</span><span class="sxs-lookup"><span data-stu-id="87a56-186">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="87a56-187">これらのアラートは、ユーザーが作業している情報や、アクティビティ フィードに通知を挿入して表示する必要があるものに関連しています。</span><span class="sxs-lookup"><span data-stu-id="87a56-187">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="87a56-188">ボット メッセージから通知をトリガーするには、objects プロパティを `TeamsChannelData` true `Notification.Alert` に設定 *します*。</span><span class="sxs-lookup"><span data-stu-id="87a56-188">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to *true*.</span></span> <span data-ttu-id="87a56-189">通知が発生するかどうかは、個々のユーザーの設定によって異Teams、これらの設定を上書きすることはできません。</span><span class="sxs-lookup"><span data-stu-id="87a56-189">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="87a56-190">通知の種類は、バナー、またはバナーとメールの両方です。</span><span class="sxs-lookup"><span data-stu-id="87a56-190">The notification type is either a banner, or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="87a56-191">[ **概要] フィールド** には、ユーザーからのテキストがフィードに通知メッセージとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="87a56-191">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="87a56-192">次のコードは、メッセージに通知を追加する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="87a56-192">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="87a56-193">C#</span><span class="sxs-lookup"><span data-stu-id="87a56-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="87a56-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="87a56-194">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="87a56-195">Python</span><span class="sxs-lookup"><span data-stu-id="87a56-195">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="87a56-196">JSON</span><span class="sxs-lookup"><span data-stu-id="87a56-196">JSON</span></span>](#tab/json)

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

<span data-ttu-id="87a56-197">メッセージを強化するために、画像をそのメッセージの添付ファイルとして含めることができます。</span><span class="sxs-lookup"><span data-stu-id="87a56-197">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="87a56-198">ピクチャ メッセージ</span><span class="sxs-lookup"><span data-stu-id="87a56-198">Picture messages</span></span>

<span data-ttu-id="87a56-199">画像は、メッセージに添付ファイルを追加して送信されます。</span><span class="sxs-lookup"><span data-stu-id="87a56-199">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="87a56-200">添付ファイルの詳細については [、Bot Framework のドキュメントを参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。</span><span class="sxs-lookup"><span data-stu-id="87a56-200">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="87a56-201">画像は、PNG、JPEG、または GIF 形式× 1024、1024、1 MB までです。</span><span class="sxs-lookup"><span data-stu-id="87a56-201">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="87a56-202">アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="87a56-202">Animated GIF is not supported.</span></span>

<span data-ttu-id="87a56-203">XML を使用して各イメージの高さと幅を指定します。</span><span class="sxs-lookup"><span data-stu-id="87a56-203">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="87a56-204">markdown では、イメージ サイズの既定値は 256 ×256 です。</span><span class="sxs-lookup"><span data-stu-id="87a56-204">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="87a56-205">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="87a56-205">For example:</span></span>

* <span data-ttu-id="87a56-206">使用: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .</span><span class="sxs-lookup"><span data-stu-id="87a56-206">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="87a56-207">使用 `![Duck on a rock](http://aka.ms/Fo983c)` しない:</span><span class="sxs-lookup"><span data-stu-id="87a56-207">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="87a56-208">会話型ボットには、ビジネス ワークフローを簡素化するアダプティブ カードを含めできます。</span><span class="sxs-lookup"><span data-stu-id="87a56-208">A conversational bot can include Adaptive Cards that simplify business workflows.</span></span> <span data-ttu-id="87a56-209">アダプティブ カードは、豊富なカスタマイズ可能なテキスト、音声、画像、ボタン、および入力フィールドを提供します。</span><span class="sxs-lookup"><span data-stu-id="87a56-209">Adaptive Cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="87a56-210">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="87a56-210">Adaptive Cards</span></span>

<span data-ttu-id="87a56-211">アダプティブ カードはボットで作成し、Teams、Web サイトなど、複数のアプリに表示できます。</span><span class="sxs-lookup"><span data-stu-id="87a56-211">Adaptive Cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="87a56-212">詳細については、「アダプティブ カード」 [を参照してください](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)。</span><span class="sxs-lookup"><span data-stu-id="87a56-212">For more information, see [Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="87a56-213">次のコードは、単純なアダプティブ カードを送信する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="87a56-213">The following code shows an example of sending a simple Adaptive Card:</span></span>

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

<span data-ttu-id="87a56-214">ボット内のカードとカードの詳細については、カードのドキュメント [を参照してください](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="87a56-214">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="87a56-215">状態コードの応答</span><span class="sxs-lookup"><span data-stu-id="87a56-215">Status code responses</span></span>

<span data-ttu-id="87a56-216">状態コードとエラー コードとメッセージ値を次に示します。</span><span class="sxs-lookup"><span data-stu-id="87a56-216">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="87a56-217">状態コード</span><span class="sxs-lookup"><span data-stu-id="87a56-217">Status code</span></span> | <span data-ttu-id="87a56-218">エラー コードとメッセージ値</span><span class="sxs-lookup"><span data-stu-id="87a56-218">Error code and message values</span></span> | <span data-ttu-id="87a56-219">説明</span><span class="sxs-lookup"><span data-stu-id="87a56-219">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="87a56-220">403</span><span class="sxs-lookup"><span data-stu-id="87a56-220">403</span></span> | <span data-ttu-id="87a56-221">**コード**: `ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="87a56-221">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="87a56-222">**メッセージ**: ユーザーがボットとの会話をブロックしました。</span><span class="sxs-lookup"><span data-stu-id="87a56-222">**Message**: User blocked the conversation with the bot.</span></span> | <span data-ttu-id="87a56-223">ユーザーは、モデレート設定を使用して、1:1 チャットまたはチャネルでボットをブロックしました。</span><span class="sxs-lookup"><span data-stu-id="87a56-223">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="87a56-224">403</span><span class="sxs-lookup"><span data-stu-id="87a56-224">403</span></span> | <span data-ttu-id="87a56-225">**コード**: `BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="87a56-225">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="87a56-226">**メッセージ**: ボットは会話名簿の一部ではありません。</span><span class="sxs-lookup"><span data-stu-id="87a56-226">**Message**: The bot is not part of the conversation roster.</span></span> | <span data-ttu-id="87a56-227">ボットは会話の一部ではありません。</span><span class="sxs-lookup"><span data-stu-id="87a56-227">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="87a56-228">403</span><span class="sxs-lookup"><span data-stu-id="87a56-228">403</span></span> | <span data-ttu-id="87a56-229">**コード**: `BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="87a56-229">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="87a56-230">**メッセージ**: テナント管理者は、このボットを無効にしました。</span><span class="sxs-lookup"><span data-stu-id="87a56-230">**Message**: The tenant admin disabled this bot.</span></span> | <span data-ttu-id="87a56-231">テナントがボットをブロックしました。</span><span class="sxs-lookup"><span data-stu-id="87a56-231">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="87a56-232">401</span><span class="sxs-lookup"><span data-stu-id="87a56-232">401</span></span> | <span data-ttu-id="87a56-233">**コード**: `BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="87a56-233">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="87a56-234">**メッセージ**: このボットの登録が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="87a56-234">**Message**: No registration found for this bot.</span></span> | <span data-ttu-id="87a56-235">このボットの登録が見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="87a56-235">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="87a56-236">412</span><span class="sxs-lookup"><span data-stu-id="87a56-236">412</span></span> | <span data-ttu-id="87a56-237">**コード**: `PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="87a56-237">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="87a56-238">**メッセージ**: 事前条件に失敗しました。もう一度お試しください。</span><span class="sxs-lookup"><span data-stu-id="87a56-238">**Message**: Precondition failed, please try again.</span></span> | <span data-ttu-id="87a56-239">同じ会話に対する複数の同時操作が原因で、依存関係の 1 つでプレコンディションが失敗しました。</span><span class="sxs-lookup"><span data-stu-id="87a56-239">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="87a56-240">404</span><span class="sxs-lookup"><span data-stu-id="87a56-240">404</span></span> | <span data-ttu-id="87a56-241">**コード**: `ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="87a56-241">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="87a56-242">**メッセージ**: 会話が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="87a56-242">**Message**: Conversation not found.</span></span> | <span data-ttu-id="87a56-243">会話が見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="87a56-243">The conversation was not found.</span></span> |
| <span data-ttu-id="87a56-244">413</span><span class="sxs-lookup"><span data-stu-id="87a56-244">413</span></span> | <span data-ttu-id="87a56-245">**コード**: `MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="87a56-245">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="87a56-246">**メッセージ**: メッセージ サイズが大きすぎます。</span><span class="sxs-lookup"><span data-stu-id="87a56-246">**Message**: Message size too large.</span></span> | <span data-ttu-id="87a56-247">受信要求のサイズが大きすぎました。</span><span class="sxs-lookup"><span data-stu-id="87a56-247">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="87a56-248">429</span><span class="sxs-lookup"><span data-stu-id="87a56-248">429</span></span> | <span data-ttu-id="87a56-249">**コード**: `Throttled`</span><span class="sxs-lookup"><span data-stu-id="87a56-249">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="87a56-250">**メッセージ**: 要求が多すぎます。</span><span class="sxs-lookup"><span data-stu-id="87a56-250">**Message**: Too many requests.</span></span> <span data-ttu-id="87a56-251">後で再試行する場合も返します。</span><span class="sxs-lookup"><span data-stu-id="87a56-251">Also returns when to retry after.</span></span> | <span data-ttu-id="87a56-252">ボットから送信された要求が多すぎます。</span><span class="sxs-lookup"><span data-stu-id="87a56-252">Too many requests were sent by the bot.</span></span> <span data-ttu-id="87a56-253">詳細については、「レート制限 [」を参照してください](~/bots/how-to/rate-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="87a56-253">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

## <a name="code-sample"></a><span data-ttu-id="87a56-254">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="87a56-254">Code sample</span></span>

|<span data-ttu-id="87a56-255">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="87a56-255">Sample name</span></span> | <span data-ttu-id="87a56-256">説明</span><span class="sxs-lookup"><span data-stu-id="87a56-256">Description</span></span> | <span data-ttu-id="87a56-257">.NETCore</span><span class="sxs-lookup"><span data-stu-id="87a56-257">.NETCore</span></span> | <span data-ttu-id="87a56-258">Node.js</span><span class="sxs-lookup"><span data-stu-id="87a56-258">Node.js</span></span> | <span data-ttu-id="87a56-259">Python</span><span class="sxs-lookup"><span data-stu-id="87a56-259">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="87a56-260">Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="87a56-260">Teams conversation bot</span></span> | <span data-ttu-id="87a56-261">メッセージングおよび会話イベントの処理。</span><span class="sxs-lookup"><span data-stu-id="87a56-261">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="87a56-262">View</span><span class="sxs-lookup"><span data-stu-id="87a56-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="87a56-263">View</span><span class="sxs-lookup"><span data-stu-id="87a56-263">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="87a56-264">View</span><span class="sxs-lookup"><span data-stu-id="87a56-264">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="87a56-265">関連項目</span><span class="sxs-lookup"><span data-stu-id="87a56-265">See also</span></span>

- [<span data-ttu-id="87a56-266">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="87a56-266">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)

- [<span data-ttu-id="87a56-267">会話イベントにサブスクライブする</span><span class="sxs-lookup"><span data-stu-id="87a56-267">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="87a56-268">次の手順</span><span class="sxs-lookup"><span data-stu-id="87a56-268">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="87a56-269">ボット コマンド メニュー</span><span class="sxs-lookup"><span data-stu-id="87a56-269">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)
