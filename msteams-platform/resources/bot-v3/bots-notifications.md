---
title: ボット イベントの処理
description: Microsoft Teamsのボットでイベントを処理する方法について説明します。
keywords: チームボットイベント
ms.date: 05/20/2019
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: da624ea0e92e193f4ad7f334d958349d542dd6e0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566468"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="37a14-104">Microsoft Teamsでボット イベントを処理する</span><span class="sxs-lookup"><span data-stu-id="37a14-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="37a14-105">Microsoft Teamsは、ボットがアクティブなスコープで発生する変更やイベントに関する通知をボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="37a14-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="37a14-106">これらのイベントを使用して、次のようなサービス ロジックをトリガーできます。</span><span class="sxs-lookup"><span data-stu-id="37a14-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="37a14-107">ボットがチームに追加されたときにウェルカムメッセージをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="37a14-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="37a14-108">ボットがグループ チャットに追加されたときに、グループ情報をクエリおよびキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="37a14-108">Query and cache group information when the bot is added to a group chat.</span></span>
* <span data-ttu-id="37a14-109">チーム メンバーシップまたはチャネル情報に関するキャッシュ情報を更新します。</span><span class="sxs-lookup"><span data-stu-id="37a14-109">Update cached information on team membership or channel information.</span></span>
* <span data-ttu-id="37a14-110">ボットが削除された場合、チームのキャッシュ情報を削除します。</span><span class="sxs-lookup"><span data-stu-id="37a14-110">Remove cached information for a team if the bot is removed.</span></span>
* <span data-ttu-id="37a14-111">ボット メッセージがユーザーに気に入られたとき。</span><span class="sxs-lookup"><span data-stu-id="37a14-111">When a bot message is liked by a user.</span></span>

<span data-ttu-id="37a14-112">各 bot イベントは、 `Activity` オブジェクト内の `messageType` 情報を定義するオブジェクトとして送信されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="37a14-113">種類のメッセージについては `message` 、「 [メッセージの送受信」](~/resources/bot-v3/bot-conversations/bots-conversations.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="37a14-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="37a14-114">通常は型からトリガーされるTeams イベントとグループ イベント `conversationUpdate` には、オブジェクトの一部として追加のTeamsイベント情報が渡 `channelData` されるため、イベント ハンドラーは `channelData` 、Teams `eventType` と追加のイベント固有のメタデータのペイロードを照会する必要があります。</span><span class="sxs-lookup"><span data-stu-id="37a14-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="37a14-115">次の表に、ボットが受信してアクションを実行できるイベントを示します。</span><span class="sxs-lookup"><span data-stu-id="37a14-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="37a14-116">型</span><span class="sxs-lookup"><span data-stu-id="37a14-116">Type</span></span>|<span data-ttu-id="37a14-117">ペイロード オブジェクト</span><span class="sxs-lookup"><span data-stu-id="37a14-117">Payload object</span></span>|<span data-ttu-id="37a14-118">Teamsイベントタイプ</span><span class="sxs-lookup"><span data-stu-id="37a14-118">Teams eventType</span></span> |<span data-ttu-id="37a14-119">説明</span><span class="sxs-lookup"><span data-stu-id="37a14-119">Description</span></span>|<span data-ttu-id="37a14-120">範囲</span><span class="sxs-lookup"><span data-stu-id="37a14-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="37a14-121">チームに追加されたメンバー</span><span class="sxs-lookup"><span data-stu-id="37a14-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="37a14-122">すべての</span><span class="sxs-lookup"><span data-stu-id="37a14-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="37a14-123">メンバーがチームから削除されました</span><span class="sxs-lookup"><span data-stu-id="37a14-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="37a14-124">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="37a14-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="37a14-125">チャネルが作成されました</span><span class="sxs-lookup"><span data-stu-id="37a14-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="37a14-126">チャンネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="37a14-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="37a14-127">チャンネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="37a14-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="37a14-128">ボット メッセージへの反応</span><span class="sxs-lookup"><span data-stu-id="37a14-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="37a14-129">すべての</span><span class="sxs-lookup"><span data-stu-id="37a14-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="37a14-130">ボット メッセージから削除された反応</span><span class="sxs-lookup"><span data-stu-id="37a14-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="37a14-131">すべての</span><span class="sxs-lookup"><span data-stu-id="37a14-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="37a14-132">チーム メンバーまたはボットの追加</span><span class="sxs-lookup"><span data-stu-id="37a14-132">Team member or bot addition</span></span>

<span data-ttu-id="37a14-133">[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true)イベントは、追加されたチームのメンバーシップ更新に関する情報を受け取ると、ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="37a14-134">また、ボットが特定の個人の会話に初めて追加されたときにも更新を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="37a14-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="37a14-135">ユーザー情報 ( `Id` ) は、ボットに固有のもので、特定のユーザーにメッセージを送信するなど、サービスでの今後の使用のためにキャッシュできます。</span><span class="sxs-lookup"><span data-stu-id="37a14-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service, such as, sending a message to a specific user.</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="37a14-136">チームに追加されたボットまたはユーザー</span><span class="sxs-lookup"><span data-stu-id="37a14-136">Bot or user added to a team</span></span>

<span data-ttu-id="37a14-137">`conversationUpdate`ペイロード内のオブジェクトを含むイベント `membersAdded` は、ボットがチームに追加されるか、ボットが追加されたチームに新しいユーザーが追加されたときに送信されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="37a14-138">Microsoft Teamsも `eventType.teamMemberAdded` オブジェクトに追加 `channelData` します。</span><span class="sxs-lookup"><span data-stu-id="37a14-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="37a14-139">このイベントはどちらの場合も送信されるため、オブジェクトを解析 `membersAdded` して、追加がユーザーかボット自体かを判断する必要があります。</span><span class="sxs-lookup"><span data-stu-id="37a14-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="37a14-140">後者の場合、ユーザーがボットに提供する機能を理解できるように [、チャネルにウェルカム メッセージ](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) を送信することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="37a14-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="37a14-141">コード例: ボットが追加されたメンバーかどうかを確認する</span><span class="sxs-lookup"><span data-stu-id="37a14-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="37a14-142">.NET</span><span class="sxs-lookup"><span data-stu-id="37a14-142">.NET</span></span>

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

##### <a name="nodejs"></a><span data-ttu-id="37a14-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="37a14-143">Node.js</span></span>

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

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="37a14-144">スキーマの例: ボットがチームに追加されました</span><span class="sxs-lookup"><span data-stu-id="37a14-144">Schema example: Bot added to team</span></span>

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

### <a name="user-added-to-a-meeting"></a><span data-ttu-id="37a14-145">ユーザーが会議に追加されました</span><span class="sxs-lookup"><span data-stu-id="37a14-145">User Added to a meeting</span></span>

<span data-ttu-id="37a14-146">`conversationUpdate`ペイロード内のオブジェクトを含むイベント `membersAdded` は、ユーザーが非公開のスケジュールされた会議に追加されたときに送信されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-146">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when a user is added to a private scheduled meeting.</span></span> <span data-ttu-id="37a14-147">匿名ユーザーが会議に参加した場合でも、イベントの詳細が送信されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-147">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="37a14-148">匿名ユーザーが会議に追加されると、メンバー追加ペイロード オブジェクトには `aadObjectId` フィールドがありません。</span><span class="sxs-lookup"><span data-stu-id="37a14-148">When an anonymous user is added to a meeting, membersAdded payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="37a14-149">匿名ユーザーが会議に追加されると、 `from` 別の発表者によって匿名ユーザーが追加された場合でも、ペイロード内のオブジェクトには常に会議の開催者の ID が割り当てられています。</span><span class="sxs-lookup"><span data-stu-id="37a14-149">When an anonymous user is added to a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was added by another presenter.</span></span>

#### <a name="schema-example-user-added-to-meeting"></a><span data-ttu-id="37a14-150">スキーマの例: ユーザーが会議に追加されました</span><span class="sxs-lookup"><span data-stu-id="37a14-150">Schema example: User added to meeting</span></span>

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

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="37a14-151">ボットは、個人的なコンテキストのためだけに追加されました</span><span class="sxs-lookup"><span data-stu-id="37a14-151">Bot added for personal context only</span></span>

<span data-ttu-id="37a14-152">ボットは、 `conversationUpdate` `membersAdded` ユーザーが個人チャット用に直接追加したときに、 で の を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="37a14-152">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="37a14-153">この場合、ボットが受け取るペイロードにはオブジェクトが含まれていません `channelData.team` 。</span><span class="sxs-lookup"><span data-stu-id="37a14-153">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="37a14-154">スコープに応じて異なる [ウェルカム メッセージ](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) をボットが提供する場合に備えて、これをフィルターとして使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="37a14-154">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="37a14-155">パーソナル スコープのボットの場合、ボットが `conversationUpdate` 削除されて再び追加された場合でも、ボットはイベントを複数回受信します。</span><span class="sxs-lookup"><span data-stu-id="37a14-155">For personal scoped bots, your bot will  receive the `conversationUpdate` event multiple times, even if the bot is removed and re-added.</span></span> <span data-ttu-id="37a14-156">開発とテストのために、ボットを完全にリセットできるヘルパー関数を追加すると便利です。</span><span class="sxs-lookup"><span data-stu-id="37a14-156">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="37a14-157">この実装の詳細については [ 、Node.js例](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) または [C# の例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="37a14-157">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="37a14-158">スキーマの例: ボットが個人コンテキストに追加されました</span><span class="sxs-lookup"><span data-stu-id="37a14-158">Schema example: bot added to personal context</span></span>

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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="37a14-159">チーム メンバーまたはボットを削除しました</span><span class="sxs-lookup"><span data-stu-id="37a14-159">Team member or bot removed</span></span>

<span data-ttu-id="37a14-160">`conversationUpdate`ペイロード内のオブジェクトを含むイベント `membersRemoved` は、ボットがチームから削除された場合、またはボットが追加されたチームからユーザーが削除されたときに送信されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-160">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="37a14-161">Microsoft Teamsも `eventType.teamMemberRemoved` オブジェクトに追加 `channelData` します。</span><span class="sxs-lookup"><span data-stu-id="37a14-161">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="37a14-162">オブジェクトと同様に `membersAdded` 、ボットの `membersRemoved` App ID のオブジェクトを解析して、誰が削除されたかを判断する必要があります。</span><span class="sxs-lookup"><span data-stu-id="37a14-162">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="37a14-163">スキーマの例: チーム メンバーが削除されました</span><span class="sxs-lookup"><span data-stu-id="37a14-163">Schema example: Team member removed</span></span>

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

### <a name="user-removed-from-a-meeting"></a><span data-ttu-id="37a14-164">ユーザーが会議から削除されました</span><span class="sxs-lookup"><span data-stu-id="37a14-164">User removed from a meeting</span></span>

<span data-ttu-id="37a14-165">`conversationUpdate`ペイロード内のオブジェクトを含むイベント `membersRemoved` は、ユーザーが非公開のスケジュールされた会議から削除されたときに送信されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-165">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when a user is removed from a private scheduled meeting.</span></span> <span data-ttu-id="37a14-166">匿名ユーザーが会議に参加した場合でも、イベントの詳細が送信されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-166">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="37a14-167">匿名ユーザーが会議から削除されると、メンバー削除されたペイロード オブジェクトにはフィールドがありません `aadObjectId` 。</span><span class="sxs-lookup"><span data-stu-id="37a14-167">When an anonymous user is removed from a meeting, membersRemoved payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="37a14-168">匿名ユーザーが会議から削除されると、 `from` 別の発表者によって匿名ユーザーが削除された場合でも、ペイロード内のオブジェクトには常に会議の開催者の ID が割り当てられています。</span><span class="sxs-lookup"><span data-stu-id="37a14-168">When an anonymous user is removed from a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was removed by another presenter.</span></span>

#### <a name="schema-example-user-removed-from-meeting"></a><span data-ttu-id="37a14-169">スキーマの例: ユーザーが会議から削除されました</span><span class="sxs-lookup"><span data-stu-id="37a14-169">Schema example: User removed from meeting</span></span>

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

## <a name="team-name-updates"></a><span data-ttu-id="37a14-170">チーム名の更新</span><span class="sxs-lookup"><span data-stu-id="37a14-170">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="37a14-171">すべてのチーム名を照会する機能はなく、チーム名は他のイベントのペイロードで返されません。</span><span class="sxs-lookup"><span data-stu-id="37a14-171">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="37a14-172">ボットが参加しているチームの名前が変更されると、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-172">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="37a14-173">`conversationUpdate`オブジェクト内のイベントを受け取 `eventType.teamRenamed` `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="37a14-173">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="37a14-174">ボットはチームの一部としてしか存在しないため、追加されたスコープ外の可視性がないため、チームの作成または削除に関する通知はありません。</span><span class="sxs-lookup"><span data-stu-id="37a14-174">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="37a14-175">スキーマの例: チーム名変更</span><span class="sxs-lookup"><span data-stu-id="37a14-175">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="37a14-176">チャンネルの更新</span><span class="sxs-lookup"><span data-stu-id="37a14-176">Channel updates</span></span>

<span data-ttu-id="37a14-177">ボットは、追加されたチームでチャネルが作成、名前変更、または削除されたときに通知されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-177">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="37a14-178">イベント `conversationUpdate` が受信され、Teams固有のイベント識別子がオブジェクトの一部として送信 `channelData.eventType` `channel.id` されます `channel.name` 。</span><span class="sxs-lookup"><span data-stu-id="37a14-178">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="37a14-179">チャネル イベントは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="37a14-179">The channel events are as follows:</span></span>

* <span data-ttu-id="37a14-180">**チャンネル作成** &emsp;ユーザーがチームに新しいチャネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="37a14-180">**channelCreated**&emsp;A user adds a new channel to the team.</span></span>
* <span data-ttu-id="37a14-181">**チャンネル名前変更** &emsp;ユーザーが既存のチャネルの名前を変更した場合。</span><span class="sxs-lookup"><span data-stu-id="37a14-181">**channelRenamed**&emsp;A user renames an existing channel.</span></span>
* <span data-ttu-id="37a14-182">**チャンネル削除済み** &emsp;ユーザーがチャネルを削除した場合。</span><span class="sxs-lookup"><span data-stu-id="37a14-182">**channelDeleted**&emsp;A user removes a channel.</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="37a14-183">完全なスキーマの例: チャネル作成</span><span class="sxs-lookup"><span data-stu-id="37a14-183">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="37a14-184">スキーマの抜粋: チャンネルデータを名前を変更</span><span class="sxs-lookup"><span data-stu-id="37a14-184">Schema excerpt: channelData for channelRenamed</span></span>

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="37a14-185">スキーマの抜粋: チャンネルデータ削除</span><span class="sxs-lookup"><span data-stu-id="37a14-185">Schema excerpt: channelData for channelDeleted</span></span>

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

## <a name="reactions"></a><span data-ttu-id="37a14-186">反応</span><span class="sxs-lookup"><span data-stu-id="37a14-186">Reactions</span></span>

<span data-ttu-id="37a14-187">`messageReaction`イベントは、ユーザーが最初にボットから送信されたメッセージに対する反応を追加または削除したときに送信されます。</span><span class="sxs-lookup"><span data-stu-id="37a14-187">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="37a14-188">`replyToId` には、特定のメッセージの ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="37a14-188">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="37a14-189">スキーマの例: ユーザーがメッセージを気に入る</span><span class="sxs-lookup"><span data-stu-id="37a14-189">Schema example: A user likes a message</span></span>

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

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="37a14-190">スキーマの例: ユーザーがメッセージを非アクティブにする</span><span class="sxs-lookup"><span data-stu-id="37a14-190">Schema example: A user un-likes a message</span></span>

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
