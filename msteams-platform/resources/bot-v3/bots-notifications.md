---
title: ボット イベントの処理
description: Microsoft Teams のボットでイベントを処理する方法について説明します。
keywords: teams ボット イベント
ms.date: 05/20/2019
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 5a7f7971d7f58af315222933f1c1f192868a4171
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020640"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="15b7f-104">Microsoft Teams でのボット イベントの処理</span><span class="sxs-lookup"><span data-stu-id="15b7f-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="15b7f-105">Microsoft Teams は、ボットがアクティブなスコープで発生する変更やイベントに関する通知をボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="15b7f-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="15b7f-106">これらのイベントを使用して、次のようなサービス ロジックをトリガーできます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="15b7f-107">ボットをチームに追加するときにウェルカム メッセージをトリガーする</span><span class="sxs-lookup"><span data-stu-id="15b7f-107">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="15b7f-108">ボットがグループ チャットに追加された場合のグループ情報のクエリとキャッシュ</span><span class="sxs-lookup"><span data-stu-id="15b7f-108">Query and cache group information when the bot is added to a group chat</span></span>
* <span data-ttu-id="15b7f-109">チーム メンバーシップまたはチャネル情報に関するキャッシュ情報を更新する</span><span class="sxs-lookup"><span data-stu-id="15b7f-109">Update cached information on team membership or channel information</span></span>
* <span data-ttu-id="15b7f-110">ボットが削除された場合、チームのキャッシュされた情報を削除する</span><span class="sxs-lookup"><span data-stu-id="15b7f-110">Remove cached information for a team if the bot is removed</span></span>
* <span data-ttu-id="15b7f-111">ボット メッセージがユーザーに気に入らされた場合</span><span class="sxs-lookup"><span data-stu-id="15b7f-111">When a bot message is liked by a user</span></span>

<span data-ttu-id="15b7f-112">各ボット イベントは、オブジェクト `Activity` 内の情報を定義 `messageType` するオブジェクトとして送信されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="15b7f-113">種類のメッセージについては、「 `message` メッセージの [送受信」を参照してください](~/resources/bot-v3/bot-conversations/bots-conversations.md)。</span><span class="sxs-lookup"><span data-stu-id="15b7f-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="15b7f-114">Teams イベントとグループ イベント (通常は型からトリガーされる) には、オブジェクトの一部として渡される Teams イベント情報が追加されるため、イベント ハンドラーは Teams のペイロードと追加のイベント固有のメタデータを照会する `conversationUpdate` `channelData` `channelData` `eventType` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="15b7f-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="15b7f-115">次の表に、ボットが受け取ってアクションを実行できるイベントの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="15b7f-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="15b7f-116">種類</span><span class="sxs-lookup"><span data-stu-id="15b7f-116">Type</span></span>|<span data-ttu-id="15b7f-117">Payload オブジェクト</span><span class="sxs-lookup"><span data-stu-id="15b7f-117">Payload object</span></span>|<span data-ttu-id="15b7f-118">Teams eventType</span><span class="sxs-lookup"><span data-stu-id="15b7f-118">Teams eventType</span></span> |<span data-ttu-id="15b7f-119">説明</span><span class="sxs-lookup"><span data-stu-id="15b7f-119">Description</span></span>|<span data-ttu-id="15b7f-120">範囲</span><span class="sxs-lookup"><span data-stu-id="15b7f-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="15b7f-121">チームに追加されたメンバー</span><span class="sxs-lookup"><span data-stu-id="15b7f-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="15b7f-122">すべての</span><span class="sxs-lookup"><span data-stu-id="15b7f-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="15b7f-123">メンバーがチームから削除された</span><span class="sxs-lookup"><span data-stu-id="15b7f-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="15b7f-124">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="15b7f-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="15b7f-125">チャネルが作成されました</span><span class="sxs-lookup"><span data-stu-id="15b7f-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="15b7f-126">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="15b7f-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="15b7f-127">チャネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="15b7f-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="15b7f-128">ボット メッセージへの反応</span><span class="sxs-lookup"><span data-stu-id="15b7f-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="15b7f-129">すべての</span><span class="sxs-lookup"><span data-stu-id="15b7f-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="15b7f-130">ボット メッセージから削除された反応</span><span class="sxs-lookup"><span data-stu-id="15b7f-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="15b7f-131">すべての</span><span class="sxs-lookup"><span data-stu-id="15b7f-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="15b7f-132">チーム メンバーまたはボットの追加</span><span class="sxs-lookup"><span data-stu-id="15b7f-132">Team member or bot addition</span></span>

<span data-ttu-id="15b7f-133">イベントは、追加されたチームのメンバーシップ更新に関する情報を受信すると、ボット [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) に送信されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="15b7f-134">また、ボットが特定の個人の会話に初めて追加されたときにも更新を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="15b7f-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="15b7f-135">ユーザー情報 ( ) はボットに対して一意であり、サービスで将来使用するためにキャッシュできます (特定のユーザーにメッセージを送信するなど `Id` )。</span><span class="sxs-lookup"><span data-stu-id="15b7f-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="15b7f-136">チームに追加されたボットまたはユーザー</span><span class="sxs-lookup"><span data-stu-id="15b7f-136">Bot or user added to a team</span></span>

<span data-ttu-id="15b7f-137">ペイロード内のオブジェクトを含むイベントは、ボットがチームに追加された場合、またはボットが追加されたチームに新しいユーザーが追加された場合 `conversationUpdate` `membersAdded` に送信されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="15b7f-138">Microsoft Teams もオブジェクト `eventType.teamMemberAdded` に追加 `channelData` します。</span><span class="sxs-lookup"><span data-stu-id="15b7f-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="15b7f-139">このイベントはどちらの場合も送信されますので、オブジェクトを解析して、追加がユーザーかボット自体かを `membersAdded` 判断する必要があります。</span><span class="sxs-lookup"><span data-stu-id="15b7f-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="15b7f-140">後者の場合、ベスト プラクティスは、ユーザーが[](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams)ボットが提供する機能をユーザーが理解できるよう、チャネルにウェルカム メッセージを送信する方法です。</span><span class="sxs-lookup"><span data-stu-id="15b7f-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="15b7f-141">コード例: ボットが追加されたメンバーであるかどうかを確認する</span><span class="sxs-lookup"><span data-stu-id="15b7f-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="15b7f-142">.NET</span><span class="sxs-lookup"><span data-stu-id="15b7f-142">.NET</span></span>

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

##### <a name="nodejs"></a><span data-ttu-id="15b7f-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="15b7f-143">Node.js</span></span>

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

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="15b7f-144">スキーマの例: ボットがチームに追加されました</span><span class="sxs-lookup"><span data-stu-id="15b7f-144">Schema example: Bot added to team</span></span>

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a><span data-ttu-id="15b7f-145">会議に追加されたユーザー</span><span class="sxs-lookup"><span data-stu-id="15b7f-145">User Added to a meeting</span></span>

<span data-ttu-id="15b7f-146">ペイロード `conversationUpdate` 内のオブジェクトを含むイベントは、ユーザーがプライベートスケジュールされた会議に追加 `membersAdded` された場合に送信されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-146">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when a user is added to a private scheduled meeting.</span></span> <span data-ttu-id="15b7f-147">匿名ユーザーが会議に参加した場合でも、イベントの詳細が送信されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-147">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="15b7f-148">匿名ユーザーが会議に追加される場合、membersAdded ペイロード オブジェクトにはフィールド `aadObjectId` はありません。</span><span class="sxs-lookup"><span data-stu-id="15b7f-148">When an anonymous user is added to a meeting, membersAdded payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="15b7f-149">匿名ユーザーが会議に追加された場合、匿名ユーザーが別の発表者によって追加された場合でも、ペイロード内のオブジェクトは常に会議開催者の `from` ID を持つ。</span><span class="sxs-lookup"><span data-stu-id="15b7f-149">When an anonymous user is added to a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was added by another presenter.</span></span>

#### <a name="schema-example-user-added-to-meeting"></a><span data-ttu-id="15b7f-150">スキーマの例: 会議に追加されたユーザー</span><span class="sxs-lookup"><span data-stu-id="15b7f-150">Schema example: User added to meeting</span></span>

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="15b7f-151">個人用コンテキスト用に追加されたボットのみ</span><span class="sxs-lookup"><span data-stu-id="15b7f-151">Bot added for personal context only</span></span>

<span data-ttu-id="15b7f-152">ボットは、ユーザーが `conversationUpdate` 個人用 `membersAdded` チャットに直接追加すると、そのメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="15b7f-152">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="15b7f-153">この場合、ボットが受け取るペイロードにはオブジェクトが含 `channelData.team` まれます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-153">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="15b7f-154">スコープに応じてボットが別のウェルカム メッセージを提供する場合は、これを [フィルターとして使用](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) する必要があります。</span><span class="sxs-lookup"><span data-stu-id="15b7f-154">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="15b7f-155">個人用スコープボットの場合、ボットが削除され、再追加された場合でも、ボットはイベントを複数回 `conversationUpdate` 受信します。</span><span class="sxs-lookup"><span data-stu-id="15b7f-155">For personal scoped bots, your bot will  receive the `conversationUpdate` event multiple times, even if the bot is removed and re-added.</span></span> <span data-ttu-id="15b7f-156">開発とテストでは、ボットを完全にリセットできるヘルパー関数を追加すると便利です。</span><span class="sxs-lookup"><span data-stu-id="15b7f-156">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="15b7f-157">この実装 [Node.js詳細については](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) 、Node.js [C#例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) または例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="15b7f-157">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="15b7f-158">スキーマの例: 個人用コンテキストにボットを追加する</span><span class="sxs-lookup"><span data-stu-id="15b7f-158">Schema example: bot added to personal context</span></span>

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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="15b7f-159">チーム メンバーまたはボットが削除されました</span><span class="sxs-lookup"><span data-stu-id="15b7f-159">Team member or bot removed</span></span>

<span data-ttu-id="15b7f-160">ペイロード内のオブジェクトを含むイベントは、ボットがチームから削除されたか、ボットが追加されたチームからユーザーが削除されると `conversationUpdate` `membersRemoved` 送信されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-160">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="15b7f-161">Microsoft Teams もオブジェクト `eventType.teamMemberRemoved` に追加 `channelData` します。</span><span class="sxs-lookup"><span data-stu-id="15b7f-161">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="15b7f-162">オブジェクトと同様に、ボットのアプリ ID のオブジェクトを解析して、削除された `membersAdded` `membersRemoved` ユーザーを特定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="15b7f-162">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="15b7f-163">スキーマの例: チーム メンバーが削除されました</span><span class="sxs-lookup"><span data-stu-id="15b7f-163">Schema example: Team member removed</span></span>

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

### <a name="user-removed-from-a-meeting"></a><span data-ttu-id="15b7f-164">会議から削除されたユーザー</span><span class="sxs-lookup"><span data-stu-id="15b7f-164">User removed from a meeting</span></span>

<span data-ttu-id="15b7f-165">ペイロード内のオブジェクトを含むイベントは、ユーザーがプライベートスケジュールされた会議から削除 `conversationUpdate` `membersRemoved` されると送信されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-165">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when a user is removed from a private scheduled meeting.</span></span> <span data-ttu-id="15b7f-166">匿名ユーザーが会議に参加した場合でも、イベントの詳細が送信されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-166">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="15b7f-167">匿名ユーザーが会議から削除されると、membersRemoved ペイロード オブジェクトにはフィールド `aadObjectId` はありません。</span><span class="sxs-lookup"><span data-stu-id="15b7f-167">When an anonymous user is removed from a meeting, membersRemoved payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="15b7f-168">匿名ユーザーが会議から削除されると、匿名ユーザーが別の発表者によって削除された場合でも、ペイロード内のオブジェクトは常に会議開催者の `from` ID を持つ。</span><span class="sxs-lookup"><span data-stu-id="15b7f-168">When an anonymous user is removed from a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was removed by another presenter.</span></span>

#### <a name="schema-example-user-removed-from-meeting"></a><span data-ttu-id="15b7f-169">スキーマの例: 会議から削除されたユーザー</span><span class="sxs-lookup"><span data-stu-id="15b7f-169">Schema example: User removed from meeting</span></span>

```
{   
      "membersRemoved": 
        {  
          "id": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"   
        }   
      ],   
      "type": "conversationUpdate",   
      "timestamp": "2020-09-29T21:15:08.6391139Z",   
      "id": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",   
      "channelId": "msteams",   
      "serviceUrl": "https://canary.botapi.skype.com/amer/",   
      "from": {   
        "id": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",   
        "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"   
      },   
      "conversation": {    
        "isGroup": true,   
        "tenantId": "e15762ef-a8d8-416b-871c-25516354f1fe",   
        "id": "19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"   
      },   
      "recipient": {   
        "id": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",   
        "name": "EchoBot1_Rename"   
      },   
      "channelData": {   
        "tenant": {   
          "id": "e15762ef-a8d8-416b-871c-25516354f1fe"   
        },   
        "source": null,   
        "meeting": {   
          "id": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="   
        }   
      }   
}
```

## <a name="team-name-updates"></a><span data-ttu-id="15b7f-170">チーム名の更新</span><span class="sxs-lookup"><span data-stu-id="15b7f-170">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="15b7f-171">すべてのチーム名を照会する機能はありません。また、他のイベントからのペイロードではチーム名は返されません。</span><span class="sxs-lookup"><span data-stu-id="15b7f-171">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="15b7f-172">ボットが含むチームの名前が変更された場合、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-172">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="15b7f-173">オブジェクトで `conversationUpdate` イベントを `eventType.teamRenamed` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="15b7f-173">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="15b7f-174">ボットはチームの一部としてのみ存在し、追加されたスコープ外の可視性を持たないので、チームの作成または削除に関する通知はありません。</span><span class="sxs-lookup"><span data-stu-id="15b7f-174">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="15b7f-175">スキーマの例: チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="15b7f-175">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="15b7f-176">チャネルの更新</span><span class="sxs-lookup"><span data-stu-id="15b7f-176">Channel updates</span></span>

<span data-ttu-id="15b7f-177">チャネルが追加されたチームでチャネルが作成、名前変更、または削除されると、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-177">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="15b7f-178">繰り返しますが、イベントが受信され、Teams 固有のイベント識別子がオブジェクトの一部として送信され、チャネル データはチャネルの GUID であり、チャネル名自体が `conversationUpdate` `channelData.eventType`  `channel.id` `channel.name` 含まれる。</span><span class="sxs-lookup"><span data-stu-id="15b7f-178">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="15b7f-179">チャネル イベントは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="15b7f-179">The channel events are as follows:</span></span>

* <span data-ttu-id="15b7f-180">**channelCreated** &emsp;ユーザーがチームに新しいチャネルを追加する</span><span class="sxs-lookup"><span data-stu-id="15b7f-180">**channelCreated**&emsp;A user adds a new channel to the team</span></span>
* <span data-ttu-id="15b7f-181">**channelRenamed** &emsp;ユーザーが既存のチャネルの名前を変更する</span><span class="sxs-lookup"><span data-stu-id="15b7f-181">**channelRenamed**&emsp;A user renames an existing channel</span></span>
* <span data-ttu-id="15b7f-182">**channelDeleted** &emsp;ユーザーがチャネルを削除する</span><span class="sxs-lookup"><span data-stu-id="15b7f-182">**channelDeleted**&emsp;A user removes a channel</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="15b7f-183">完全なスキーマの例: channelCreated</span><span class="sxs-lookup"><span data-stu-id="15b7f-183">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="15b7f-184">スキーマの抜粋: channelData for channelRenamed</span><span class="sxs-lookup"><span data-stu-id="15b7f-184">Schema excerpt: channelData for channelRenamed</span></span>

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="15b7f-185">スキーマの抜粋: channelData for channelDeleted</span><span class="sxs-lookup"><span data-stu-id="15b7f-185">Schema excerpt: channelData for channelDeleted</span></span>

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

## <a name="reactions"></a><span data-ttu-id="15b7f-186">リアクション</span><span class="sxs-lookup"><span data-stu-id="15b7f-186">Reactions</span></span>

<span data-ttu-id="15b7f-187">イベントは、ユーザーがボットから送信されたメッセージに対する反応を追加または削除 `messageReaction` すると送信されます。</span><span class="sxs-lookup"><span data-stu-id="15b7f-187">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="15b7f-188">`replyToId` には、特定のメッセージの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="15b7f-188">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="15b7f-189">スキーマの例: ユーザーがメッセージを気に入る</span><span class="sxs-lookup"><span data-stu-id="15b7f-189">Schema example: A user likes a message</span></span>

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

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="15b7f-190">スキーマの例: ユーザーがメッセージを好きにしない</span><span class="sxs-lookup"><span data-stu-id="15b7f-190">Schema example: A user un-likes a message</span></span>

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
