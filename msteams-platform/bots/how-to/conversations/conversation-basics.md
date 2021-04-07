---
title: 会話の基本
description: Microsoft Teams ボットと会話する方法について説明します。
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 193a93dbf775389383e0385207fa4112440bffe5
ms.sourcegitcommit: 82bda0599ba2676ab9348c2f4284f73c7dad0838
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596675"
---
# <a name="conversation-basics"></a><span data-ttu-id="82b14-103">会話の基本</span><span class="sxs-lookup"><span data-stu-id="82b14-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="82b14-104">会話とは、Microsoft Teams ボットと 1 人または複数のユーザーの間で送信される一連のメッセージです。</span><span class="sxs-lookup"><span data-stu-id="82b14-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="82b14-105">Teams には、スコープとも呼ばれる 3 種類の会話があります。</span><span class="sxs-lookup"><span data-stu-id="82b14-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="82b14-106">会話の種類</span><span class="sxs-lookup"><span data-stu-id="82b14-106">Conversation type</span></span> | <span data-ttu-id="82b14-107">説明</span><span class="sxs-lookup"><span data-stu-id="82b14-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="82b14-108">この会話の種類は、チャネルのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="82b14-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="82b14-109">この会話の種類には、ボットと 1 人のユーザーとの会話が含まれます。</span><span class="sxs-lookup"><span data-stu-id="82b14-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="82b14-110">この会話の種類には、ボットと 2 人以上のユーザーの間のチャットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="82b14-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="82b14-111">また、会議チャットでボットを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="82b14-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="82b14-112">ボットの動作は、関連する会話に応じて異なります。</span><span class="sxs-lookup"><span data-stu-id="82b14-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="82b14-113">チャネルチャットとグループ チャット会話のボットでは、チャネルでボットを呼び出す場合は、ユーザーがボットに @メンションする必要があります。</span><span class="sxs-lookup"><span data-stu-id="82b14-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="82b14-114">1 対 1 の会話のボットでは@メンションは必要ない。</span><span class="sxs-lookup"><span data-stu-id="82b14-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="82b14-115">ユーザーが送信したメッセージはすべてボットにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="82b14-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="82b14-116">ボットが特定の会話またはスコープで動作するには、アプリ マニフェストのそのスコープにサポートを [追加します](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="82b14-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="messages-in-bot-conversations"></a><span data-ttu-id="82b14-117">ボットの会話内のメッセージ</span><span class="sxs-lookup"><span data-stu-id="82b14-117">Messages in bot conversations</span></span>

<span data-ttu-id="82b14-118">会話内の各メッセージは、 `Activity` 型のオブジェクトです `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="82b14-118">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="82b14-119">ユーザーがメッセージを送信すると、Teams はボットにメッセージを投稿します。</span><span class="sxs-lookup"><span data-stu-id="82b14-119">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="82b14-120">Teams は JSON オブジェクトをボットのメッセージング エンドポイントに送信します。</span><span class="sxs-lookup"><span data-stu-id="82b14-120">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="82b14-121">ボットはメッセージを調べて、その種類を特定し、それに応じて応答します。</span><span class="sxs-lookup"><span data-stu-id="82b14-121">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="82b14-122">基本的な会話は、単一の REST API である Bot Framework コネクタを介して処理されます。</span><span class="sxs-lookup"><span data-stu-id="82b14-122">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="82b14-123">この API を使用すると、ボットは Teams や他のチャネルと通信できます。</span><span class="sxs-lookup"><span data-stu-id="82b14-123">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="82b14-124">ボット ビルダー SDK には、次の機能があります。</span><span class="sxs-lookup"><span data-stu-id="82b14-124">The Bot Builder SDK provides the following:</span></span>

* <span data-ttu-id="82b14-125">Bot Framework コネクタに簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="82b14-125">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="82b14-126">会話のフローと状態を管理するための追加機能。</span><span class="sxs-lookup"><span data-stu-id="82b14-126">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="82b14-127">自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法。</span><span class="sxs-lookup"><span data-stu-id="82b14-127">Simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

<span data-ttu-id="82b14-128">ボットは、このプロパティを使用して Teams からメッセージを受信し、ユーザーに単一または複数 `Text` のメッセージ応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="82b14-128">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="82b14-129">メッセージを受信する</span><span class="sxs-lookup"><span data-stu-id="82b14-129">Receive a message</span></span>

<span data-ttu-id="82b14-130">テキスト メッセージを受信するには、`Activity` オブジェクトの `Text` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="82b14-130">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="82b14-131">ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `Activity` を使用して、1 つのメッセージ要求を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="82b14-131">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="82b14-132">次のコードは、メッセージを受信する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="82b14-132">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="82b14-133">C#</span><span class="sxs-lookup"><span data-stu-id="82b14-133">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="82b14-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="82b14-134">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="82b14-135">Python</span><span class="sxs-lookup"><span data-stu-id="82b14-135">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="82b14-136">JSON</span><span class="sxs-lookup"><span data-stu-id="82b14-136">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="82b14-137">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="82b14-137">Send a message</span></span>

<span data-ttu-id="82b14-138">テキスト メッセージを送信するには、送信する文字列をアクティビティとして指定します。</span><span class="sxs-lookup"><span data-stu-id="82b14-138">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="82b14-139">ボットのアクティビティ ハンドラーで、turn context オブジェクトのメソッドを使用して 1 つの `SendActivityAsync` メッセージ応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="82b14-139">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="82b14-140">オブジェクトのメソッドを使用して `SendActivitiesAsync` 、複数の応答を一度に送信します。</span><span class="sxs-lookup"><span data-stu-id="82b14-140">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="82b14-141">次のコードは、ユーザーが会話に追加された場合にメッセージを送信する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="82b14-141">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

<span data-ttu-id="82b14-142">次のコードは、メッセージを送信する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="82b14-142">The following code shows an example of sending a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="82b14-143">C#</span><span class="sxs-lookup"><span data-stu-id="82b14-143">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="82b14-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="82b14-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="82b14-145">Python</span><span class="sxs-lookup"><span data-stu-id="82b14-145">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="82b14-146">JSON</span><span class="sxs-lookup"><span data-stu-id="82b14-146">JSON</span></span>](#tab/json)

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
> <span data-ttu-id="82b14-147">メッセージの分割は、テキスト メッセージと添付ファイルが同じアクティビティ ペイロードで送信される場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="82b14-147">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="82b14-148">このアクティビティは、Microsoft Teams によって個別のアクティビティに分割され、1 つはテキスト メッセージだけで、もう 1 つは添付ファイルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="82b14-148">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="82b14-149">アクティビティが分割されている間、メッセージ ID は応答で受信されません。これは、メッセージを事前に更新または [削除するために使用](~/bots/how-to/update-and-delete-bot-messages.md) されます。</span><span class="sxs-lookup"><span data-stu-id="82b14-149">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="82b14-150">メッセージの分割に応じてではなく、個別のアクティビティを送信する方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="82b14-150">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="82b14-151">ユーザーとボットの間で送信されるメッセージには、メッセージ内の内部チャネル データが含まれます。</span><span class="sxs-lookup"><span data-stu-id="82b14-151">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="82b14-152">このデータを使用すると、ボットはチャネルで適切に通信できます。</span><span class="sxs-lookup"><span data-stu-id="82b14-152">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="82b14-153">ボット ビルダー SDK を使用すると、メッセージ構造を変更できます。</span><span class="sxs-lookup"><span data-stu-id="82b14-153">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="82b14-154">Teams チャネル データ</span><span class="sxs-lookup"><span data-stu-id="82b14-154">Teams channel data</span></span>

<span data-ttu-id="82b14-155">オブジェクト `channelData` には Teams 固有の情報が含まれているので、チームとチャネルの ID の決定的なソースです。</span><span class="sxs-lookup"><span data-stu-id="82b14-155">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="82b14-156">必要に応じて、これらの ID をローカル ストレージのキーとしてキャッシュして使用できます。</span><span class="sxs-lookup"><span data-stu-id="82b14-156">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="82b14-157">SDK では、通常、オブジェクトから重要な情報を引き出して、簡単 `TeamsActivityHandler` `channelData` にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="82b14-157">The `TeamsActivityHandler` in the SDK typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="82b14-158">ただし、オブジェクトから元のデータにいつでもアクセス `turnContext` できます。</span><span class="sxs-lookup"><span data-stu-id="82b14-158">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="82b14-159">オブジェクトは、チャネルの外部で行なうので、個人的な会話の `channelData` メッセージには含まれません。</span><span class="sxs-lookup"><span data-stu-id="82b14-159">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="82b14-160">ボットに `channelData` 送信されるアクティビティの一般的なオブジェクトには、次の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="82b14-160">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="82b14-161">`eventType`: チャネル変更イベントの場合にのみ渡される Teams イベント [の種類](~/bots/how-to/conversations/subscribe-to-conversation-events.md)です。</span><span class="sxs-lookup"><span data-stu-id="82b14-161">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="82b14-162">`tenant.id`: すべてのコンテキストで渡された Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="82b14-162">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="82b14-163">`team`: チャネル コンテキストでのみ渡されます。個人チャットでは渡されない。</span><span class="sxs-lookup"><span data-stu-id="82b14-163">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="82b14-164">`id`: チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="82b14-164">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="82b14-165">`name`: チーム名の変更イベントの場合にのみ渡された [チームの名前](~/bots/how-to/conversations/subscribe-to-conversation-events.md)です。</span><span class="sxs-lookup"><span data-stu-id="82b14-165">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="82b14-166">`channel`: ボットが言及されている場合、またはボットが追加されたチームのチャネル内のイベントに対して、チャネル コンテキストでのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="82b14-166">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="82b14-167">`id`: チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="82b14-167">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="82b14-168">`name`: チャネル変更イベントの場合にのみ渡 [されるチャネル名](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="82b14-168">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="82b14-169">`channelData.teamsTeamId`: 非推奨です。</span><span class="sxs-lookup"><span data-stu-id="82b14-169">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="82b14-170">このプロパティは、下位互換性のためにのみ含まれます。</span><span class="sxs-lookup"><span data-stu-id="82b14-170">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="82b14-171">`channelData.teamsChannelId`: 非推奨です。</span><span class="sxs-lookup"><span data-stu-id="82b14-171">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="82b14-172">このプロパティは、下位互換性のためにのみ含まれます。</span><span class="sxs-lookup"><span data-stu-id="82b14-172">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="82b14-173">channelData オブジェクトの例 (channelCreated イベント)</span><span class="sxs-lookup"><span data-stu-id="82b14-173">Example channelData object (channelCreated event)</span></span>

<span data-ttu-id="82b14-174">次のコードは、channelData オブジェクトの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="82b14-174">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="82b14-175">ボットから受信またはボットに送信されるメッセージには、さまざまな種類のメッセージ コンテンツを含めできます。</span><span class="sxs-lookup"><span data-stu-id="82b14-175">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="82b14-176">メッセージの内容</span><span class="sxs-lookup"><span data-stu-id="82b14-176">Message content</span></span>

<span data-ttu-id="82b14-177">ボットはリッチ テキスト、画像、カードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="82b14-177">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="82b14-178">ユーザーは、リッチ テキストと画像をボットに送信できます。</span><span class="sxs-lookup"><span data-stu-id="82b14-178">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="82b14-179">フォーマット</span><span class="sxs-lookup"><span data-stu-id="82b14-179">Format</span></span>    | <span data-ttu-id="82b14-180">ユーザーからボットへ</span><span class="sxs-lookup"><span data-stu-id="82b14-180">From user to bot</span></span> | <span data-ttu-id="82b14-181">ボットからユーザーへ</span><span class="sxs-lookup"><span data-stu-id="82b14-181">From bot to user</span></span> | <span data-ttu-id="82b14-182">メモ</span><span class="sxs-lookup"><span data-stu-id="82b14-182">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="82b14-183">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="82b14-183">Rich text</span></span> | <span data-ttu-id="82b14-184">✔</span><span class="sxs-lookup"><span data-stu-id="82b14-184">✔</span></span>                | <span data-ttu-id="82b14-185">✔</span><span class="sxs-lookup"><span data-stu-id="82b14-185">✔</span></span>                |                                                                                         |
| <span data-ttu-id="82b14-186">ピクチャ</span><span class="sxs-lookup"><span data-stu-id="82b14-186">Pictures</span></span>  | <span data-ttu-id="82b14-187">✔</span><span class="sxs-lookup"><span data-stu-id="82b14-187">✔</span></span>                | <span data-ttu-id="82b14-188">✔</span><span class="sxs-lookup"><span data-stu-id="82b14-188">✔</span></span>                | <span data-ttu-id="82b14-189">最大 1024 × 1024 および 1 MB (PNG、JPEG、または GIF 形式)。</span><span class="sxs-lookup"><span data-stu-id="82b14-189">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="82b14-190">アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="82b14-190">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="82b14-191">カード</span><span class="sxs-lookup"><span data-stu-id="82b14-191">Cards</span></span>     | <span data-ttu-id="82b14-192">✖</span><span class="sxs-lookup"><span data-stu-id="82b14-192">✖</span></span>                | <span data-ttu-id="82b14-193">✔</span><span class="sxs-lookup"><span data-stu-id="82b14-193">✔</span></span>                | <span data-ttu-id="82b14-194">サポートされているカード [については、「Teams カード](~/task-modules-and-cards/cards/cards-reference.md) リファレンス」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="82b14-194">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="82b14-195">絵文字</span><span class="sxs-lookup"><span data-stu-id="82b14-195">Emojis</span></span>    | <span data-ttu-id="82b14-196">✖</span><span class="sxs-lookup"><span data-stu-id="82b14-196">✖</span></span>                | <span data-ttu-id="82b14-197">✔</span><span class="sxs-lookup"><span data-stu-id="82b14-197">✔</span></span>                | <span data-ttu-id="82b14-198">Teams は現在、顔にニヤリと笑う U+1F600 など、UTF-16 による絵文字をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="82b14-198">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="82b14-199">プロパティを使用してメッセージに通知を追加 `Notification.Alert` することもできます。</span><span class="sxs-lookup"><span data-stu-id="82b14-199">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="82b14-200">メッセージへの通知</span><span class="sxs-lookup"><span data-stu-id="82b14-200">Notifications to your message</span></span>

<span data-ttu-id="82b14-201">通知は、新しいタスク、メンション、コメントについてユーザーに通知します。</span><span class="sxs-lookup"><span data-stu-id="82b14-201">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="82b14-202">これらのアラートは、ユーザーが作業している情報や、アクティビティ フィードに通知を挿入して表示する必要があるものに関連しています。</span><span class="sxs-lookup"><span data-stu-id="82b14-202">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="82b14-203">ボット メッセージから通知をトリガーするには、objects プロパティを `TeamsChannelData` true `Notification.Alert` に設定します。</span><span class="sxs-lookup"><span data-stu-id="82b14-203">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="82b14-204">通知が発生するかどうかは、個々のユーザーの Teams 設定によって異なります。これらの設定を上書きすることはできません。</span><span class="sxs-lookup"><span data-stu-id="82b14-204">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="82b14-205">通知の種類は、バナーまたはバナーとメールの両方です。</span><span class="sxs-lookup"><span data-stu-id="82b14-205">The notification type is either a banner or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="82b14-206">[ **概要] フィールド** には、ユーザーからのテキストがフィードに通知メッセージとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="82b14-206">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="82b14-207">次のコードは、メッセージに通知を追加する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="82b14-207">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="82b14-208">C#</span><span class="sxs-lookup"><span data-stu-id="82b14-208">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="82b14-209">TypeScript</span><span class="sxs-lookup"><span data-stu-id="82b14-209">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="82b14-210">Python</span><span class="sxs-lookup"><span data-stu-id="82b14-210">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="82b14-211">JSON</span><span class="sxs-lookup"><span data-stu-id="82b14-211">JSON</span></span>](#tab/json)

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

<span data-ttu-id="82b14-212">メッセージを強化するために、画像をそのメッセージの添付ファイルとして含めることができます。</span><span class="sxs-lookup"><span data-stu-id="82b14-212">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="82b14-213">ピクチャ メッセージ</span><span class="sxs-lookup"><span data-stu-id="82b14-213">Picture messages</span></span>

<span data-ttu-id="82b14-214">画像は、メッセージに添付ファイルを追加して送信されます。</span><span class="sxs-lookup"><span data-stu-id="82b14-214">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="82b14-215">添付ファイルの詳細については [、Bot Framework のドキュメントを参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。</span><span class="sxs-lookup"><span data-stu-id="82b14-215">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="82b14-216">画像は、PNG、JPEG、または GIF 形式× 1024、1024、1 MB までです。</span><span class="sxs-lookup"><span data-stu-id="82b14-216">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="82b14-217">アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="82b14-217">Animated GIF is not supported.</span></span>

<span data-ttu-id="82b14-218">XML を使用して各イメージの高さと幅を指定します。</span><span class="sxs-lookup"><span data-stu-id="82b14-218">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="82b14-219">markdown では、イメージ サイズの既定値は 256 ×256 です。</span><span class="sxs-lookup"><span data-stu-id="82b14-219">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="82b14-220">例:</span><span class="sxs-lookup"><span data-stu-id="82b14-220">For example:</span></span>

* <span data-ttu-id="82b14-221">使用: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .</span><span class="sxs-lookup"><span data-stu-id="82b14-221">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="82b14-222">使用 `![Duck on a rock](http://aka.ms/Fo983c)` しない:</span><span class="sxs-lookup"><span data-stu-id="82b14-222">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="82b14-223">会話型ボットには、ビジネス ワークフローを簡素化するアダプティブ カードを含めできます。</span><span class="sxs-lookup"><span data-stu-id="82b14-223">A conversational bot can include adaptive cards that simplify business workflows.</span></span> <span data-ttu-id="82b14-224">アダプティブ カードは、豊富なカスタマイズ可能なテキスト、音声、画像、ボタン、および入力フィールドを提供します。</span><span class="sxs-lookup"><span data-stu-id="82b14-224">Adaptive cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="82b14-225">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="82b14-225">Adaptive cards</span></span>

<span data-ttu-id="82b14-226">アダプティブ カードはボットで作成し、Teams、Web サイトなどの複数のアプリに表示できます。</span><span class="sxs-lookup"><span data-stu-id="82b14-226">Adaptive cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="82b14-227">詳細については、「アダプティブ カード [」を参照してください](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)。</span><span class="sxs-lookup"><span data-stu-id="82b14-227">For more information, see [adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="82b14-228">次のコードは、単純なアダプティブ カードを送信する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="82b14-228">The following code shows an example of sending a simple adaptive card:</span></span>

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

<span data-ttu-id="82b14-229">ボット内のカードとカードの詳細については、カードのドキュメント [を参照してください](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="82b14-229">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="82b14-230">次のセクションでは、ボット API から生成されたエラーに対する状態コードの応答を示します。</span><span class="sxs-lookup"><span data-stu-id="82b14-230">The next section provides status code responses for errors generated from Bot APIs.</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="82b14-231">状態コードの応答</span><span class="sxs-lookup"><span data-stu-id="82b14-231">Status code responses</span></span>

<span data-ttu-id="82b14-232">状態コードとエラー コードとメッセージ値を次に示します。</span><span class="sxs-lookup"><span data-stu-id="82b14-232">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="82b14-233">状態コード</span><span class="sxs-lookup"><span data-stu-id="82b14-233">Status code</span></span> | <span data-ttu-id="82b14-234">エラー コードとメッセージ値</span><span class="sxs-lookup"><span data-stu-id="82b14-234">Error code and message values</span></span> | <span data-ttu-id="82b14-235">説明</span><span class="sxs-lookup"><span data-stu-id="82b14-235">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="82b14-236">403</span><span class="sxs-lookup"><span data-stu-id="82b14-236">403</span></span> | <span data-ttu-id="82b14-237">**コード**: `ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="82b14-237">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="82b14-238">**メッセージ**: "ユーザーがボットとの会話をブロックしました。</span><span class="sxs-lookup"><span data-stu-id="82b14-238">**Message**: "User blocked the conversation with the bot."</span></span> | <span data-ttu-id="82b14-239">ユーザーは、モデレート設定を使用して、1:1 チャットまたはチャネルでボットをブロックしました。</span><span class="sxs-lookup"><span data-stu-id="82b14-239">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="82b14-240">403</span><span class="sxs-lookup"><span data-stu-id="82b14-240">403</span></span> | <span data-ttu-id="82b14-241">**コード**: `BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="82b14-241">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="82b14-242">**メッセージ**: "ボットは会話名簿の一部ではありません。</span><span class="sxs-lookup"><span data-stu-id="82b14-242">**Message**: "The bot is not part of the conversation roster."</span></span> | <span data-ttu-id="82b14-243">ボットは会話の一部ではありません。</span><span class="sxs-lookup"><span data-stu-id="82b14-243">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="82b14-244">403</span><span class="sxs-lookup"><span data-stu-id="82b14-244">403</span></span> | <span data-ttu-id="82b14-245">**コード**: `BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="82b14-245">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="82b14-246">**メッセージ**: "テナント管理者は、このボットを無効にしました。</span><span class="sxs-lookup"><span data-stu-id="82b14-246">**Message**: "The tenant admin disabled this bot."</span></span> | <span data-ttu-id="82b14-247">テナントがボットをブロックしました。</span><span class="sxs-lookup"><span data-stu-id="82b14-247">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="82b14-248">401</span><span class="sxs-lookup"><span data-stu-id="82b14-248">401</span></span> | <span data-ttu-id="82b14-249">**コード**: `BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="82b14-249">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="82b14-250">**メッセージ**: "このボットの登録が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="82b14-250">**Message**: “No registration found for this bot.”</span></span> | <span data-ttu-id="82b14-251">このボットの登録が見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="82b14-251">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="82b14-252">412</span><span class="sxs-lookup"><span data-stu-id="82b14-252">412</span></span> | <span data-ttu-id="82b14-253">**コード**: `PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="82b14-253">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="82b14-254">**メッセージ**: "Precondition が失敗しました。もう一度お試しください。</span><span class="sxs-lookup"><span data-stu-id="82b14-254">**Message**: “Precondition failed, please try again.”</span></span> | <span data-ttu-id="82b14-255">同じ会話に対する複数の同時操作が原因で、依存関係の 1 つでプレコンディションが失敗しました。</span><span class="sxs-lookup"><span data-stu-id="82b14-255">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="82b14-256">404</span><span class="sxs-lookup"><span data-stu-id="82b14-256">404</span></span> | <span data-ttu-id="82b14-257">**コード**: `ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="82b14-257">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="82b14-258">**メッセージ**: "会話が見つかりません"</span><span class="sxs-lookup"><span data-stu-id="82b14-258">**Message**: “Conversation not found.”</span></span> | <span data-ttu-id="82b14-259">会話が見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="82b14-259">The conversation was not found.</span></span> |
| <span data-ttu-id="82b14-260">413</span><span class="sxs-lookup"><span data-stu-id="82b14-260">413</span></span> | <span data-ttu-id="82b14-261">**コード**: `MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="82b14-261">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="82b14-262">**メッセージ**: "メッセージ サイズが大きすぎます。</span><span class="sxs-lookup"><span data-stu-id="82b14-262">**Message**: “Message size too large.”</span></span> | <span data-ttu-id="82b14-263">受信要求のサイズが大きすぎました。</span><span class="sxs-lookup"><span data-stu-id="82b14-263">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="82b14-264">429</span><span class="sxs-lookup"><span data-stu-id="82b14-264">429</span></span> | <span data-ttu-id="82b14-265">**コード**: `Throttled`</span><span class="sxs-lookup"><span data-stu-id="82b14-265">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="82b14-266">**メッセージ**: "要求が多すぎます。</span><span class="sxs-lookup"><span data-stu-id="82b14-266">**Message**: “Too many requests.”</span></span> <span data-ttu-id="82b14-267">後で再試行する場合も返します。</span><span class="sxs-lookup"><span data-stu-id="82b14-267">Also returns when to retry after.</span></span> | <span data-ttu-id="82b14-268">ボットから送信された要求が多すぎます。</span><span class="sxs-lookup"><span data-stu-id="82b14-268">Too many requests were sent by the bot.</span></span> <span data-ttu-id="82b14-269">詳細については、「レート制限 [」を参照してください](~/bots/how-to/rate-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="82b14-269">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

<span data-ttu-id="82b14-270">次のセクションでは、基本的な会話フローを Teams アプリケーションに組み込む簡単なコード サンプルを示します。</span><span class="sxs-lookup"><span data-stu-id="82b14-270">The next section illustrates a simple code sample that incorporates basic conversational flow into a Teams application.</span></span>

## <a name="code-sample"></a><span data-ttu-id="82b14-271">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="82b14-271">Code sample</span></span>

<span data-ttu-id="82b14-272">Teams 会話ボットのコード サンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="82b14-272">Following are the code samples for Teams conversation bot:</span></span>

|<span data-ttu-id="82b14-273">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="82b14-273">Sample name</span></span> | <span data-ttu-id="82b14-274">説明</span><span class="sxs-lookup"><span data-stu-id="82b14-274">Description</span></span> | <span data-ttu-id="82b14-275">.NETCore</span><span class="sxs-lookup"><span data-stu-id="82b14-275">.NETCore</span></span> | <span data-ttu-id="82b14-276">Node.js</span><span class="sxs-lookup"><span data-stu-id="82b14-276">Node.js</span></span> | <span data-ttu-id="82b14-277">Python</span><span class="sxs-lookup"><span data-stu-id="82b14-277">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="82b14-278">Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="82b14-278">Teams conversation bot</span></span> | <span data-ttu-id="82b14-279">メッセージングおよび会話イベントの処理。</span><span class="sxs-lookup"><span data-stu-id="82b14-279">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="82b14-280">View</span><span class="sxs-lookup"><span data-stu-id="82b14-280">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="82b14-281">View</span><span class="sxs-lookup"><span data-stu-id="82b14-281">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="82b14-282">View</span><span class="sxs-lookup"><span data-stu-id="82b14-282">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="82b14-283">関連項目</span><span class="sxs-lookup"><span data-stu-id="82b14-283">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82b14-284">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="82b14-284">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="82b14-285">会話イベントにサブスクライブする</span><span class="sxs-lookup"><span data-stu-id="82b14-285">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="82b14-286">次の手順</span><span class="sxs-lookup"><span data-stu-id="82b14-286">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82b14-287">ボット コマンド メニュー</span><span class="sxs-lookup"><span data-stu-id="82b14-287">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)
