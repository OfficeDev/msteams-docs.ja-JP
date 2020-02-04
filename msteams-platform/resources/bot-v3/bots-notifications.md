---
title: Bot イベントを処理する
description: Microsoft Teams でボットのイベントを処理する方法について説明します。
keywords: teams の bot イベント
ms.date: 05/20/2019
ms.openlocfilehash: 06da5e6b0668e86012d87af3184493cdeb70aecd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674927"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="ed22f-104">Microsoft Teams で bot イベントを処理する</span><span class="sxs-lookup"><span data-stu-id="ed22f-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="ed22f-105">Microsoft Teams は、bot がアクティブである範囲で発生した変更やイベントについて、bot に通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="ed22f-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="ed22f-106">これらのイベントを使用して、次のようなサービスロジックをトリガーできます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="ed22f-107">Bot がチームに追加されたときに開始メッセージをトリガーする</span><span class="sxs-lookup"><span data-stu-id="ed22f-107">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="ed22f-108">Bot がグループチャットに追加されたときに、グループ情報を照会およびキャッシュする</span><span class="sxs-lookup"><span data-stu-id="ed22f-108">Query and cache group information when the bot is added to a group chat</span></span>
* <span data-ttu-id="ed22f-109">チームメンバーシップまたはチャネル情報のキャッシュされた情報を更新する</span><span class="sxs-lookup"><span data-stu-id="ed22f-109">Update cached information on team membership or channel information</span></span>
* <span data-ttu-id="ed22f-110">Bot が削除された場合にチームのキャッシュされた情報を削除する</span><span class="sxs-lookup"><span data-stu-id="ed22f-110">Remove cached information for a team if the bot is removed</span></span>
* <span data-ttu-id="ed22f-111">Bot メッセージがユーザーによって好評になった場合</span><span class="sxs-lookup"><span data-stu-id="ed22f-111">When a bot message is liked by a user</span></span>

<span data-ttu-id="ed22f-112">各 bot イベントは、オブジェクトに`Activity`含まれて`messageType`いる情報を定義するオブジェクトとして送信されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="ed22f-113">受信メッセージの種類`message`については、「[メッセージの送受信](~/resources/bot-v3/bot-conversations/bots-conversations.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed22f-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="ed22f-114">通常、チームおよびグループイベントは、通常`conversationUpdate`は型から呼び出され、追加の teams イベント情報が`channelData`オブジェクトの一部として渡されるため、 `channelData`イベントハンドラーは teams `eventType`および追加のイベント固有のメタデータのペイロードを照会する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed22f-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="ed22f-115">次の表に、ボットが受信してアクションを実行できるイベントを示します。</span><span class="sxs-lookup"><span data-stu-id="ed22f-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="ed22f-116">型</span><span class="sxs-lookup"><span data-stu-id="ed22f-116">Type</span></span>|<span data-ttu-id="ed22f-117">ペイロードオブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed22f-117">Payload object</span></span>|<span data-ttu-id="ed22f-118">Teams の eventType</span><span class="sxs-lookup"><span data-stu-id="ed22f-118">Teams eventType</span></span> |<span data-ttu-id="ed22f-119">説明</span><span class="sxs-lookup"><span data-stu-id="ed22f-119">Description</span></span>|<span data-ttu-id="ed22f-120">範囲</span><span class="sxs-lookup"><span data-stu-id="ed22f-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="ed22f-121">チームに追加されたメンバー</span><span class="sxs-lookup"><span data-stu-id="ed22f-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="ed22f-122">すべての</span><span class="sxs-lookup"><span data-stu-id="ed22f-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="ed22f-123">メンバーがチームから削除されました</span><span class="sxs-lookup"><span data-stu-id="ed22f-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="ed22f-124">チームの名前変更</span><span class="sxs-lookup"><span data-stu-id="ed22f-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="ed22f-125">チャネルが作成されました</span><span class="sxs-lookup"><span data-stu-id="ed22f-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="ed22f-126">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="ed22f-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="ed22f-127">チャネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="ed22f-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="ed22f-128">Bot メッセージへの反応</span><span class="sxs-lookup"><span data-stu-id="ed22f-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="ed22f-129">すべての</span><span class="sxs-lookup"><span data-stu-id="ed22f-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="ed22f-130">Bot メッセージからの反力の削除</span><span class="sxs-lookup"><span data-stu-id="ed22f-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="ed22f-131">すべての</span><span class="sxs-lookup"><span data-stu-id="ed22f-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="ed22f-132">チームメンバーまたはボットの追加</span><span class="sxs-lookup"><span data-stu-id="ed22f-132">Team member or bot addition</span></span>

<span data-ttu-id="ed22f-133">[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate)イベントは、追加されたチームのメンバーシップ更新に関する情報を受け取ったときに bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="ed22f-134">また、個人的な会話に初めて追加されたときに、更新プログラムを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="ed22f-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="ed22f-135">ユーザー情報 (`Id`) は bot に対して一意であることに注意してください。また、サービス (特定のユーザーへのメッセージの送信など) で将来使用するためにキャッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="ed22f-136">チームに追加された Bot またはユーザー</span><span class="sxs-lookup"><span data-stu-id="ed22f-136">Bot or user added to a team</span></span>

<span data-ttu-id="ed22f-137">ユーザー `conversationUpdate`がチームに`membersAdded` bot が追加されるか、または bot が追加されたチームに新しいユーザーが追加されると、ペイロード内のオブジェクトを持つイベントが送信されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="ed22f-138">Microsoft Teams でも`eventType.teamMemberAdded`オブジェクトが`channelData`追加されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="ed22f-139">このイベントは両方の場合で送信されるため、 `membersAdded`オブジェクトを解析して、追加がユーザーか bot 自体かを判断する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed22f-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="ed22f-140">後者の場合は、ユーザーが bot が提供する機能を理解できるように、[開始メッセージ](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams)をチャネルに送信することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ed22f-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="ed22f-141">コード例: bot が追加されたメンバーであるかどうかを確認する</span><span class="sxs-lookup"><span data-stu-id="ed22f-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="ed22f-142">.NET</span><span class="sxs-lookup"><span data-stu-id="ed22f-142">.NET</span></span>

```csharp
    for (int i = 0; i < sourceMessage.MembersAdded.Count; i++)
    {
        if (sourceMessage.MembersAdded[i].Id == sourceMessage.Recipient.Id)
        {
            addedBot = true;
            break;
        }
    }
```

##### <a name="nodejs"></a><span data-ttu-id="ed22f-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="ed22f-143">Node.js</span></span>

```javascript
const builder = require('botbuilder');

var c = new builder.ChatConnector({appId: BOT_APP_ID, appPassword: .BOT_SECRET});
var bot = new builder.UniversalBot(c);

bot.on('conversationUpdate', (msg) => {
    var members = msg.membersAdded;
    // Loop through all members that were just added to the team
    for (var i = 0; i < members.length; i++) {

        // See if the member added was our bot
        if (members[i].id.includes(BOT_APP_ID)) {
            var botmessage = new builder.Message()
                .address(msg.address)
                .text('Hello World!');

            bot.send(botmessage, function(err) {});
        }
    }
});
```

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="ed22f-144">スキーマの例: チームに追加された Bot</span><span class="sxs-lookup"><span data-stu-id="ed22f-144">Schema example: Bot added to team</span></span>

```json
{
    "membersAdded": [
        {
            "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:38:35.312Z",
    "localTimestamp": "2017-02-23T12:38:35.312-07:00",
    "id": "f:5f85c2ad",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="ed22f-145">個人コンテキストのみに追加された Bot</span><span class="sxs-lookup"><span data-stu-id="ed22f-145">Bot added for personal context only</span></span>

<span data-ttu-id="ed22f-146">Bot は、ユーザー `conversationUpdate`が`membersAdded`個人チャット用に直接追加したを使用してを受信します。</span><span class="sxs-lookup"><span data-stu-id="ed22f-146">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="ed22f-147">この場合、ボットが受け取るペイロードには`channelData.team`オブジェクトが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="ed22f-147">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="ed22f-148">この範囲に応じて、bot が異なる[ウェルカムメッセージ](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations)を提供するようにする場合に備えて、これをフィルターとして使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed22f-148">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="ed22f-149">個人のスコープのボットの場合、bot が削除さ`conversationUpdate`れて再度追加されても、そのイベントは1回だけ受信されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-149">For personal scoped bots, your bot will only ever receive the `conversationUpdate` event a single time, even if the bot is removed and re-added.</span></span> <span data-ttu-id="ed22f-150">開発およびテストの場合は、ボットを完全にリセットできるヘルパー関数を追加すると便利です。</span><span class="sxs-lookup"><span data-stu-id="ed22f-150">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="ed22f-151">これを実装する詳細については、「 [node.js の例](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts)」または「 [C# の例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed22f-151">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="ed22f-152">スキーマの例: 個人コンテキストに追加された bot</span><span class="sxs-lookup"><span data-stu-id="ed22f-152">Schema example: bot added to personal context</span></span>

```json
{
  "membersAdded": [{
      "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
    },
    {
      "id": "29:<userID>",
      "aadObjectId": "***"
    }
  ],
  "type": "conversationUpdate",
  "timestamp": "2019-04-23T10:17:44.349Z",
  "id": "f:5f85c2ad",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:<USERID>",
    "aadObjectId": "***"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "***"
  },
  "recipient": {
    "id": "28:<BOT ID>",
    "name": "<BOT NAME>"
  },
  "channelData": {
    "tenant": {
      "id": "<TENANT ID>"
    }
  }
}
```

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="ed22f-153">チームメンバーまたは bot が削除されました</span><span class="sxs-lookup"><span data-stu-id="ed22f-153">Team member or bot removed</span></span>

<span data-ttu-id="ed22f-154">ユーザー `conversationUpdate`がチームから`membersRemoved` bot を削除したとき、または bot が追加されたチームからユーザーが削除されたときに、ペイロード内のオブジェクトを含むイベントが送信されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-154">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="ed22f-155">Microsoft Teams でも`eventType.teamMemberRemoved`オブジェクトが`channelData`追加されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-155">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="ed22f-156">`membersAdded`オブジェクトと同様に、Bot のアプリ ID `membersRemoved`のオブジェクトを解析して、削除されたユーザーを特定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed22f-156">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="ed22f-157">スキーマの例: チームメンバーが削除されました</span><span class="sxs-lookup"><span data-stu-id="ed22f-157">Schema example: Team member removed</span></span>

```json
{
    "membersRemoved": [
        {
            "id": "29:1_LCi5Up14pAy65yZuaJzG1uIT7ujYhjjSTsUNqjORsZHjLHKiQIBJa4cX2XsAsRoaY7va2w6ZymA9-1VtSY_g"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:37:06.96Z",
    "localTimestamp": "2017-02-23T12:37:06.96-07:00",
    "id": "f:d8a6a4aa",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient":
    {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberRemoved",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="team-name-updates"></a><span data-ttu-id="ed22f-158">チーム名の更新</span><span class="sxs-lookup"><span data-stu-id="ed22f-158">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="ed22f-159">すべてのチーム名を照会する機能はありません。また、他のイベントからのペイロードではチーム名が返されません。</span><span class="sxs-lookup"><span data-stu-id="ed22f-159">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="ed22f-160">自分のチームの名前が変更されると、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-160">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="ed22f-161">オブジェクト内で`conversationUpdate` `eventType.teamRenamed`イベントを受け取り`channelData`ます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-161">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="ed22f-162">Bot は teams の一部としてのみ存在し、追加された範囲外には表示されないので、チーム作成または削除の通知はありません。</span><span class="sxs-lookup"><span data-stu-id="ed22f-162">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="ed22f-163">スキーマの例: チームの名前変更</span><span class="sxs-lookup"><span data-stu-id="ed22f-163">Schema example: Team renamed</span></span>

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "New Team Name"
        },
        "eventType": "teamRenamed",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="channel-updates"></a><span data-ttu-id="ed22f-164">チャネルの更新</span><span class="sxs-lookup"><span data-stu-id="ed22f-164">Channel updates</span></span>

<span data-ttu-id="ed22f-165">Bot が追加されたチームでチャネルが作成、名前変更、または削除されると、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-165">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="ed22f-166">`conversationUpdate`イベントが受信され、チーム固有のイベント識別子が`channelData.eventType`オブジェクトの一部として送信されます。ここで、チャネル`channel.id`データはチャネルの GUID で、チャネル名自体が`channel.name`含まれます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-166">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="ed22f-167">チャネルイベントは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ed22f-167">The channel events are as follows:</span></span>

* <span data-ttu-id="ed22f-168">**channelcreated**&emsp;ユーザーが新しいチャネルをチームに追加する</span><span class="sxs-lookup"><span data-stu-id="ed22f-168">**channelCreated**&emsp;A user adds a new channel to the team</span></span>
* <span data-ttu-id="ed22f-169">**channelrenamed 変更**&emsp;されたユーザーが既存のチャネルの名前を変更する</span><span class="sxs-lookup"><span data-stu-id="ed22f-169">**channelRenamed**&emsp;A user renames an existing channel</span></span>
* <span data-ttu-id="ed22f-170">**channeldeleted**&emsp;ユーザーがチャネルを削除しました</span><span class="sxs-lookup"><span data-stu-id="ed22f-170">**channelDeleted**&emsp;A user removes a channel</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="ed22f-171">完全なスキーマの例: channelCreated</span><span class="sxs-lookup"><span data-stu-id="ed22f-171">Full schema example: channelCreated</span></span>

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelCreated",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="ed22f-172">スキーマの抜粋: channelData が名前変更されました</span><span class="sxs-lookup"><span data-stu-id="ed22f-172">Schema excerpt: channelData for channelRenamed</span></span>

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelRenamed",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="ed22f-173">スキーマの抜粋: チャネルが削除された channelData</span><span class="sxs-lookup"><span data-stu-id="ed22f-173">Schema excerpt: channelData for channelDeleted</span></span>

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelDeleted",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

## <a name="reactions"></a><span data-ttu-id="ed22f-174">感想</span><span class="sxs-lookup"><span data-stu-id="ed22f-174">Reactions</span></span>

<span data-ttu-id="ed22f-175">この`messageReaction`イベントは、ユーザーが最初に bot によって送信されたメッセージに対して、自分の反応を追加または削除したときに送信されます。</span><span class="sxs-lookup"><span data-stu-id="ed22f-175">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="ed22f-176">`replyToId`特定のメッセージの ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="ed22f-176">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="ed22f-177">スキーマの例: ユーザーがメッセージを好む</span><span class="sxs-lookup"><span data-stu-id="ed22f-177">Schema example: A user likes a message</span></span>

```json
{
    "reactionsAdded": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="ed22f-178">スキーマの例: ユーザーがメッセージの表示を取り消す</span><span class="sxs-lookup"><span data-stu-id="ed22f-178">Schema example: A user un-likes a message</span></span>

```json
{
    "reactionsRemoved": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```
