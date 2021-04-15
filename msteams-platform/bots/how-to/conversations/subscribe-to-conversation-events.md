---
title: 会話イベント
author: WashingtonKayaker
description: Microsoft Teams ボットからの会話イベントを処理する方法。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: af06dba58b3784a03dbcbbc627fa38fce681eeb8
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696347"
---
# <a name="conversation-events-in-your-teams-bot"></a><span data-ttu-id="14d85-103">Teams ボットの会話イベント</span><span class="sxs-lookup"><span data-stu-id="14d85-103">Conversation events in your Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="14d85-104">Microsoft Teams 用の会話型ボットを構築する場合は、会話イベントを処理できます。</span><span class="sxs-lookup"><span data-stu-id="14d85-104">When building your conversational bots for Microsoft Teams, you can work with conversation events.</span></span> <span data-ttu-id="14d85-105">Teams は、ボットがアクティブなスコープで発生する会話イベントの通知をボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="14d85-105">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="14d85-106">これらのイベントをコードでキャプチャし、次のアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="14d85-106">You can capture these events in your code and take the following actions:</span></span>

* <span data-ttu-id="14d85-107">ボットがチームに追加されると、ウェルカム メッセージをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="14d85-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="14d85-108">新しいチーム メンバーが追加または削除されると、ウェルカム メッセージをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="14d85-108">Trigger a welcome message when a new team member is added or removed.</span></span>
* <span data-ttu-id="14d85-109">チャネルの作成、名前の変更、または削除時に通知をトリガーします。</span><span class="sxs-lookup"><span data-stu-id="14d85-109">Trigger a notification when a channel is created, renamed, or deleted.</span></span>
* <span data-ttu-id="14d85-110">ボット メッセージがユーザーに気に入った場合。</span><span class="sxs-lookup"><span data-stu-id="14d85-110">When a bot message is liked by a user.</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="14d85-111">会話の更新イベント</span><span class="sxs-lookup"><span data-stu-id="14d85-111">Conversation update events</span></span>

<span data-ttu-id="14d85-112">会話の更新イベントを使用して、通知の向上とボットの効果的なアクションを提供できます。</span><span class="sxs-lookup"><span data-stu-id="14d85-112">You can use conversation update events to provide better notifications and more effective bot actions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="14d85-113">いつでも新しいイベントを追加し、ボットがイベントの受信を開始できます。</span><span class="sxs-lookup"><span data-stu-id="14d85-113">You can add new events any time and your bot begins to receive them.</span></span>
> * <span data-ttu-id="14d85-114">予期しないイベントを受け取るボットを設計する必要があります。</span><span class="sxs-lookup"><span data-stu-id="14d85-114">You must design your bot to receive unexpected events.</span></span>
> * <span data-ttu-id="14d85-115">ボット フレームワーク SDK を使用している場合、ボットは処理しないイベントに対して自動的 `200 - OK` に応答します。</span><span class="sxs-lookup"><span data-stu-id="14d85-115">If you are using the Bot Framework SDK, your bot automatically responds with a `200 - OK` to any events you choose not to handle.</span></span>

<span data-ttu-id="14d85-116">ボットは、次 `conversationUpdate` のいずれかの場合にイベントを受信します。</span><span class="sxs-lookup"><span data-stu-id="14d85-116">A bot receives a `conversationUpdate` event in either of the following cases:</span></span>

* <span data-ttu-id="14d85-117">ボットが会話に追加された場合。</span><span class="sxs-lookup"><span data-stu-id="14d85-117">When bot has been added to a conversation.</span></span>
* <span data-ttu-id="14d85-118">他のメンバーは会話に追加または削除されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-118">Other members are added to or removed from a conversation.</span></span>
* <span data-ttu-id="14d85-119">会話のメタデータが変更されました。</span><span class="sxs-lookup"><span data-stu-id="14d85-119">Conversation metadata has changed.</span></span>

<span data-ttu-id="14d85-120">`conversationUpdate` イベントは、ボットが追加されているチームのメンバーシップの更新に関する情報を受信したときにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-120">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="14d85-121">また、個人の会話用に初めて追加された更新プログラムも受け取ります。</span><span class="sxs-lookup"><span data-stu-id="14d85-121">It also receives an update when it has been added for the first time for personal conversations.</span></span>

<span data-ttu-id="14d85-122">次の表に、Teams の会話更新イベントの一覧と詳細を示します。</span><span class="sxs-lookup"><span data-stu-id="14d85-122">The following table shows a list of Teams conversation update events with more details:</span></span>

| <span data-ttu-id="14d85-123">実行されたアクション</span><span class="sxs-lookup"><span data-stu-id="14d85-123">Action taken</span></span>        | <span data-ttu-id="14d85-124">EventType</span><span class="sxs-lookup"><span data-stu-id="14d85-124">EventType</span></span>         | <span data-ttu-id="14d85-125">呼び出されるメソッド</span><span class="sxs-lookup"><span data-stu-id="14d85-125">Method called</span></span>              | <span data-ttu-id="14d85-126">説明</span><span class="sxs-lookup"><span data-stu-id="14d85-126">Description</span></span>                | <span data-ttu-id="14d85-127">範囲</span><span class="sxs-lookup"><span data-stu-id="14d85-127">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="14d85-128">作成されたチャネル</span><span class="sxs-lookup"><span data-stu-id="14d85-128">Channel created</span></span>     | <span data-ttu-id="14d85-129">channelCreated</span><span class="sxs-lookup"><span data-stu-id="14d85-129">channelCreated</span></span>    | <span data-ttu-id="14d85-130">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-130">OnTeamsChannelCreatedAsync</span></span> | <span data-ttu-id="14d85-131">[チャネルが作成されます](#channel-created)。</span><span class="sxs-lookup"><span data-stu-id="14d85-131">[A channel is created](#channel-created).</span></span> | <span data-ttu-id="14d85-132">チーム</span><span class="sxs-lookup"><span data-stu-id="14d85-132">Team</span></span> |
| <span data-ttu-id="14d85-133">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="14d85-133">Channel renamed</span></span>     | <span data-ttu-id="14d85-134">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="14d85-134">channelRenamed</span></span>    | <span data-ttu-id="14d85-135">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-135">OnTeamsChannelRenamedAsync</span></span> | <span data-ttu-id="14d85-136">[チャネルの名前が変更されます](#channel-renamed)。</span><span class="sxs-lookup"><span data-stu-id="14d85-136">[A channel is renamed](#channel-renamed).</span></span> | <span data-ttu-id="14d85-137">チーム</span><span class="sxs-lookup"><span data-stu-id="14d85-137">Team</span></span> |
| <span data-ttu-id="14d85-138">チャネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="14d85-138">Channel deleted</span></span>     | <span data-ttu-id="14d85-139">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="14d85-139">channelDeleted</span></span>    | <span data-ttu-id="14d85-140">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-140">OnTeamsChannelDeletedAsync</span></span> | <span data-ttu-id="14d85-141">[チャネルが削除されます](#channel-deleted)。</span><span class="sxs-lookup"><span data-stu-id="14d85-141">[A channel is deleted](#channel-deleted).</span></span> | <span data-ttu-id="14d85-142">チーム</span><span class="sxs-lookup"><span data-stu-id="14d85-142">Team</span></span> |
| <span data-ttu-id="14d85-143">チャネルの復元</span><span class="sxs-lookup"><span data-stu-id="14d85-143">Channel restored</span></span>    | <span data-ttu-id="14d85-144">channelRestored</span><span class="sxs-lookup"><span data-stu-id="14d85-144">channelRestored</span></span>    | <span data-ttu-id="14d85-145">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-145">OnTeamsChannelRestoredAsync</span></span> | <span data-ttu-id="14d85-146">[チャネルが復元されます](#channel-deleted)。</span><span class="sxs-lookup"><span data-stu-id="14d85-146">[A channel is restored](#channel-deleted).</span></span> | <span data-ttu-id="14d85-147">チーム</span><span class="sxs-lookup"><span data-stu-id="14d85-147">Team</span></span> |
| <span data-ttu-id="14d85-148">追加されたメンバー</span><span class="sxs-lookup"><span data-stu-id="14d85-148">Members added</span></span>   | <span data-ttu-id="14d85-149">membersAdded</span><span class="sxs-lookup"><span data-stu-id="14d85-149">membersAdded</span></span>   | <span data-ttu-id="14d85-150">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-150">OnTeamsMembersAddedAsync</span></span>   | <span data-ttu-id="14d85-151">[メンバーが追加されます](#team-members-added)。</span><span class="sxs-lookup"><span data-stu-id="14d85-151">[A member is added](#team-members-added).</span></span> | <span data-ttu-id="14d85-152">すべて</span><span class="sxs-lookup"><span data-stu-id="14d85-152">All</span></span> |
| <span data-ttu-id="14d85-153">削除されたメンバー</span><span class="sxs-lookup"><span data-stu-id="14d85-153">Members removed</span></span> | <span data-ttu-id="14d85-154">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="14d85-154">membersRemoved</span></span> | <span data-ttu-id="14d85-155">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-155">OnTeamsMembersRemovedAsync</span></span> | <span data-ttu-id="14d85-156">[メンバーが削除されます](#team-members-removed)。</span><span class="sxs-lookup"><span data-stu-id="14d85-156">[A member is removed](#team-members-removed).</span></span> | <span data-ttu-id="14d85-157">groupChat とチーム</span><span class="sxs-lookup"><span data-stu-id="14d85-157">groupChat and team</span></span> |
| <span data-ttu-id="14d85-158">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="14d85-158">Team renamed</span></span>        | <span data-ttu-id="14d85-159">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="14d85-159">teamRenamed</span></span>       | <span data-ttu-id="14d85-160">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-160">OnTeamsTeamRenamedAsync</span></span>    | <span data-ttu-id="14d85-161">[チームの名前が変更されました](#team-renamed)。</span><span class="sxs-lookup"><span data-stu-id="14d85-161">[A team is renamed](#team-renamed).</span></span>       | <span data-ttu-id="14d85-162">チーム</span><span class="sxs-lookup"><span data-stu-id="14d85-162">Team</span></span> |
| <span data-ttu-id="14d85-163">チームが削除されました</span><span class="sxs-lookup"><span data-stu-id="14d85-163">Team deleted</span></span>        | <span data-ttu-id="14d85-164">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="14d85-164">teamDeleted</span></span>       | <span data-ttu-id="14d85-165">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-165">OnTeamsTeamDeletedAsync</span></span>    | <span data-ttu-id="14d85-166">[チームが削除されます](#team-deleted)。</span><span class="sxs-lookup"><span data-stu-id="14d85-166">[A team is deleted](#team-deleted).</span></span>       | <span data-ttu-id="14d85-167">チーム</span><span class="sxs-lookup"><span data-stu-id="14d85-167">Team</span></span> |
| <span data-ttu-id="14d85-168">チームのアーカイブ</span><span class="sxs-lookup"><span data-stu-id="14d85-168">Team archived</span></span>        | <span data-ttu-id="14d85-169">teamArchived</span><span class="sxs-lookup"><span data-stu-id="14d85-169">teamArchived</span></span>       | <span data-ttu-id="14d85-170">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-170">OnTeamsTeamArchivedAsync</span></span>    | <span data-ttu-id="14d85-171">[チームがアーカイブされます](#team-archived)。</span><span class="sxs-lookup"><span data-stu-id="14d85-171">[A team is archived](#team-archived).</span></span>       | <span data-ttu-id="14d85-172">チーム</span><span class="sxs-lookup"><span data-stu-id="14d85-172">Team</span></span> |
| <span data-ttu-id="14d85-173">チームのアーカイブ解除</span><span class="sxs-lookup"><span data-stu-id="14d85-173">Team unarchived</span></span>        | <span data-ttu-id="14d85-174">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="14d85-174">teamUnarchived</span></span>       | <span data-ttu-id="14d85-175">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-175">OnTeamsTeamUnarchivedAsync</span></span>    | <span data-ttu-id="14d85-176">[チームはアーカイブ解除されます](#team-unarchived)。</span><span class="sxs-lookup"><span data-stu-id="14d85-176">[A team is unarchived](#team-unarchived).</span></span>       | <span data-ttu-id="14d85-177">チーム</span><span class="sxs-lookup"><span data-stu-id="14d85-177">Team</span></span> |
| <span data-ttu-id="14d85-178">チームの復元</span><span class="sxs-lookup"><span data-stu-id="14d85-178">Team restored</span></span>        | <span data-ttu-id="14d85-179">teamRestored</span><span class="sxs-lookup"><span data-stu-id="14d85-179">teamRestored</span></span>      | <span data-ttu-id="14d85-180">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="14d85-180">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="14d85-181">チームが復元される</span><span class="sxs-lookup"><span data-stu-id="14d85-181">A team is restored</span></span>](#team-restored)       | <span data-ttu-id="14d85-182">チーム</span><span class="sxs-lookup"><span data-stu-id="14d85-182">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="14d85-183">作成されたチャネル</span><span class="sxs-lookup"><span data-stu-id="14d85-183">Channel created</span></span>

<span data-ttu-id="14d85-184">作成されたチャネル イベントは、ボットがインストールされているチームで新しいチャネルが作成されるたびにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-184">The channel created event is sent to your bot whenever a new channel is created in a team where your bot is installed.</span></span>

<span data-ttu-id="14d85-185">次のコードは、チャネル作成イベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-185">The following code shows an example of channel created event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-186">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-186">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-187">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-187">TypeScript</span></span>](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelCreatedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Created', `${channelInfo.name} is the Channel created`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="14d85-188">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="14d85-189">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-189">Python</span></span>](#tab/python)

```python
async def on_teams_channel_created(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="channel-renamed"></a><span data-ttu-id="14d85-190">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="14d85-190">Channel renamed</span></span>

<span data-ttu-id="14d85-191">チャネルの名前が変更されたイベントは、ボットがインストールされているチームでチャネルの名前が変更されるたびにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-191">The channel renamed event is sent to your bot whenever a channel is renamed in a team where your bot is installed.</span></span>

<span data-ttu-id="14d85-192">次のコードは、チャネルの名前が変更されたイベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-192">The following code shows an example of channel renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-193">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-194">TypeScript</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRenamedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Renamed', `${channelInfo.name} is the new Channel name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
```

# <a name="json"></a>[<span data-ttu-id="14d85-195">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-195">JSON</span></span>](#tab/json)

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
}
```

# <a name="python"></a>[<span data-ttu-id="14d85-196">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-196">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="14d85-197">チャネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="14d85-197">Channel deleted</span></span>

<span data-ttu-id="14d85-198">チャネル削除イベントは、ボットがインストールされているチームでチャネルが削除されるたびにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-198">The channel deleted event is sent to your bot whenever a channel is deleted in a team where your bot is installed.</span></span>

<span data-ttu-id="14d85-199">次のコードは、チャネル削除イベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-199">The following code shows an example of channel deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-200">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-200">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-201">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-201">TypeScript</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelDeletedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Deleted', `${channelInfo.name} is the Channel deleted`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="14d85-202">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-202">JSON</span></span>](#tab/json)

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
}
```

# <a name="python"></a>[<span data-ttu-id="14d85-203">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-203">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="14d85-204">チャネルの復元</span><span class="sxs-lookup"><span data-stu-id="14d85-204">Channel restored</span></span>

<span data-ttu-id="14d85-205">以前に削除されたチャネルがボットが既にインストールされているチームで復元されるたびに、チャネル復元イベントがボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-205">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team where your bot is already installed.</span></span>

<span data-ttu-id="14d85-206">次のコードは、チャネル復元イベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-206">The following code shows an example of channel restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-207">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-207">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-208">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-208">TypeScript</span></span>](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRestoredEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Restored', `${channelInfo.name} is the Channel restored`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="14d85-209">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-209">JSON</span></span>](#tab/json)

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
        "eventType": "channelRestored",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="14d85-210">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-210">Python</span></span>](#tab/python)

```python
async def on_teams_channel_restored(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The restored channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="team-members-added"></a><span data-ttu-id="14d85-211">チーム メンバーの追加</span><span class="sxs-lookup"><span data-stu-id="14d85-211">Team members added</span></span>

<span data-ttu-id="14d85-212">イベント `teamMemberAdded` が初めて会話に追加された場合、イベントはボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-212">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation.</span></span> <span data-ttu-id="14d85-213">イベントは、ボットがインストールされているチームまたはグループ チャットに新しいユーザーが追加される度にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-213">The event is sent to your bot every time a new user is added to a team or group chat where your bot is installed.</span></span> <span data-ttu-id="14d85-214">ID であるユーザー情報はボットに対して一意であり、特定のユーザーにメッセージを送信するなどのサービスで将来使用するためにキャッシュできます。</span><span class="sxs-lookup"><span data-stu-id="14d85-214">The user information that is ID is unique for your bot and can be cached for future use by your service, such as sending a message to a specific user.</span></span>

<span data-ttu-id="14d85-215">次のコードは、チーム メンバーがイベントを追加した例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-215">The following code shows an example of team members added event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-216">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-216">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded , TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in teamsMembersAdded)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // Send a message to introduce the bot to the team
            var heroCard = new HeroCard(text: $"The {member.Name} bot has joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-217">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-217">TypeScript</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersAddedEvent(async (membersAdded: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
                let newMembers: string = '';
                console.log(JSON.stringify(membersAdded));
                membersAdded.forEach((account) => {
                    newMembers += account.id + ' ';
                });
                const name = !teamInfo ? 'not in team' : teamInfo.name;
                const card = CardFactory.heroCard('Account Added', `${newMembers} joined ${name}.`);
                const message = MessageFactory.attachment(card);
                await turnContext.sendActivity(message);
                await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="14d85-218">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-218">JSON</span></span>](#tab/json)

<span data-ttu-id="14d85-219">これは、ボットがチームに追加された場合にボットが受信するメッセージです。</span><span class="sxs-lookup"><span data-stu-id="14d85-219">This is the message your bot receives when the bot is added to a team.</span></span>

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

<span data-ttu-id="14d85-220">これは、ボットが 1 対 1 のチャットに追加された場合にボットが受信するメッセージです。</span><span class="sxs-lookup"><span data-stu-id="14d85-220">This is the message your bot receives when the bot is added to a one-to-one chat.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="14d85-221">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-221">Python</span></span>](#tab/python)

```python
async def on_teams_members_added(
    self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(
            MessageFactory.text(f"Welcome your new team member {member.id}")
        )
    return
```

* * *

### <a name="team-members-removed"></a><span data-ttu-id="14d85-222">チーム メンバーが削除されました</span><span class="sxs-lookup"><span data-stu-id="14d85-222">Team members removed</span></span>

<span data-ttu-id="14d85-223">イベント `teamMemberRemoved` は、チームから削除された場合にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-223">The `teamMemberRemoved` event is sent to your bot if it is removed from a team.</span></span> <span data-ttu-id="14d85-224">イベントは、ボットがメンバーであるチームからユーザーが削除される度にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-224">The event is sent to your bot every time any user is removed from a team where your bot is a member.</span></span> <span data-ttu-id="14d85-225">削除された新しいメンバーがボット自体またはユーザーかどうかを確認するには、 `Activity` のオブジェクトを確認します `turnContext` 。</span><span class="sxs-lookup"><span data-stu-id="14d85-225">To determine if the new member removed was the bot itself or a user, check the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="14d85-226">オブジェクトのフィールドがオブジェクトのフィールドと同じ場合、削除されたメンバーはボット、それ以外の場合は `Id` `MembersRemoved` `Id` `Recipient` ユーザーです。</span><span class="sxs-lookup"><span data-stu-id="14d85-226">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, else it is a user.</span></span> <span data-ttu-id="14d85-227">ボットの一般的 `Id` な設定はです `28:<MicrosoftAppId>` 。</span><span class="sxs-lookup"><span data-stu-id="14d85-227">The bot's `Id` generally is `28:<MicrosoftAppId>`.</span></span>

> [!NOTE]
> <span data-ttu-id="14d85-228">ユーザーがテナントから完全に削除されると、 `membersRemoved conversationUpdate` イベントがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="14d85-228">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

<span data-ttu-id="14d85-229">次のコードは、チーム メンバーが削除したイベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-229">The following code shows an example of team members removed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-230">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-230">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersRemovedAsync(IList<ChannelAccount> membersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersRemoved)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // The bot was removed
            // You should clear any cached data you have for this team
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} was removed from {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-231">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-231">TypeScript</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersRemovedEvent(async (membersRemoved: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            let removedMembers: string = '';
            console.log(JSON.stringify(membersRemoved));
            membersRemoved.forEach((account) => {
                removedMembers += account.id + ' ';
            });
            const name = !teamInfo ? 'not in team' : teamInfo.name;
            const card = CardFactory.heroCard('Account Removed', `${removedMembers} removed from ${teamInfo.name}.`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="14d85-232">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-232">JSON</span></span>](#tab/json)

<span data-ttu-id="14d85-233">次のペイロード例のオブジェクトは、グループ チャットではなくチームにメンバーを追加するか、新しい 1 対 1 の会話を `channelData` 開始します。</span><span class="sxs-lookup"><span data-stu-id="14d85-233">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="14d85-234">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-234">Python</span></span>](#tab/python)

```python
async def on_teams_members_removed(
    self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_removed:
        await turn_context.send_activity(
            MessageFactory.text(f"Say goodbye to {member.id}")
        )
    return
```

* * *

### <a name="team-renamed"></a><span data-ttu-id="14d85-235">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="14d85-235">Team renamed</span></span>

<span data-ttu-id="14d85-236">ボットが含むチームの名前が変更された場合、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-236">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="14d85-237">オブジェクトで `conversationUpdate` イベントを `eventType.teamRenamed` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="14d85-237">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

<span data-ttu-id="14d85-238">次のコードは、チーム名が変更されたイベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-238">The following code shows an example of team renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-239">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-239">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-240">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-240">TypeScript</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamRenamedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team Renamed', `${teamInfo.name} is the new Team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="14d85-241">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-241">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="14d85-242">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-242">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-deleted"></a><span data-ttu-id="14d85-243">チームが削除されました</span><span class="sxs-lookup"><span data-stu-id="14d85-243">Team deleted</span></span>

<span data-ttu-id="14d85-244">ボットが含むチームが削除された場合、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-244">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="14d85-245">オブジェクトで `conversationUpdate` イベントを `eventType.teamDeleted` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="14d85-245">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

<span data-ttu-id="14d85-246">次のコードは、チームが削除したイベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-246">The following code shows an example of team deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-247">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-247">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-248">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-248">TypeScript</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamDeletedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            //handle delete event
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="14d85-249">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-249">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamDeleted",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="14d85-250">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-250">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="14d85-251">チームの復元</span><span class="sxs-lookup"><span data-stu-id="14d85-251">Team restored</span></span>

<span data-ttu-id="14d85-252">削除後にチームが復元された場合、ボットは通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="14d85-252">The bot receives a notification when a team is restored after being deleted.</span></span> <span data-ttu-id="14d85-253">オブジェクトで `conversationUpdate` イベントを `eventType.teamrestored` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="14d85-253">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

<span data-ttu-id="14d85-254">次のコードは、チームが復元したイベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-254">The following code shows an example of team restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-255">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-255">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-256">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-256">TypeScript</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamrestoredEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team restored', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="14d85-257">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-257">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamrestored",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="14d85-258">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-258">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="14d85-259">チームのアーカイブ</span><span class="sxs-lookup"><span data-stu-id="14d85-259">Team archived</span></span>

<span data-ttu-id="14d85-260">ボットは、インストールされているチームがアーカイブされる際に通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="14d85-260">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="14d85-261">オブジェクトで `conversationUpdate` イベントを `eventType.teamarchived` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="14d85-261">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

<span data-ttu-id="14d85-262">次のコードは、チーム アーカイブ イベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-262">The following code shows an example of team archived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-263">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-263">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-264">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-264">TypeScript</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamArchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="14d85-265">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-265">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamArchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="14d85-266">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-266">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *


### <a name="team-unarchived"></a><span data-ttu-id="14d85-267">チームのアーカイブ解除</span><span class="sxs-lookup"><span data-stu-id="14d85-267">Team unarchived</span></span>

<span data-ttu-id="14d85-268">ボットがインストールされているチームがアーカイブ解除された場合、ボットは通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="14d85-268">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="14d85-269">オブジェクトで `conversationUpdate` イベントを `eventType.teamUnarchived` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="14d85-269">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

<span data-ttu-id="14d85-270">次のコードは、チームのアーカイブ解除イベントの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-270">The following code shows an example of team unarchived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-271">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-271">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-272">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-272">TypeScript</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamUnarchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="14d85-273">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-273">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamUnarchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="14d85-274">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-274">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

<span data-ttu-id="14d85-275">会話の更新イベントを処理したので、メッセージに対するさまざまな反応に対して発生するメッセージの反応イベントを理解できます。</span><span class="sxs-lookup"><span data-stu-id="14d85-275">Now that you have worked with the conversation update events, you can understand the message reaction events that occur for different reactions to a message.</span></span>

## <a name="message-reaction-events"></a><span data-ttu-id="14d85-276">メッセージの反応イベント</span><span class="sxs-lookup"><span data-stu-id="14d85-276">Message reaction events</span></span>

<span data-ttu-id="14d85-277">ユーザーがボットから送信されたメッセージに対する反応を追加または削除すると、イベント `messageReaction` が送信されます。</span><span class="sxs-lookup"><span data-stu-id="14d85-277">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="14d85-278">メッセージ `replyToId` の ID を含み、テキスト形式 `Type` の反応の種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="14d85-278">The `replyToId` contains the ID of the message, and the `Type` is the type of reaction in text format.</span></span> <span data-ttu-id="14d85-279">反応の種類には、怒り、心、笑い、例えば、悲しい、驚くなどです。</span><span class="sxs-lookup"><span data-stu-id="14d85-279">The types of reactions include angry, heart, laugh, like, sad, and surprised.</span></span> <span data-ttu-id="14d85-280">このイベントには、元のメッセージの内容は含めされません。</span><span class="sxs-lookup"><span data-stu-id="14d85-280">This event does not contain the contents of the original message.</span></span> <span data-ttu-id="14d85-281">メッセージに対する処理の反応がボットにとって重要な場合は、メッセージを送信するときにメッセージを保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="14d85-281">If processing reactions to your messages is important for your bot, you must store the messages when you send them.</span></span> <span data-ttu-id="14d85-282">次の表に、イベントの種類とペイロード オブジェクトの詳細を示します。</span><span class="sxs-lookup"><span data-stu-id="14d85-282">The following table provides more information about the event type and payload objects:</span></span>

| <span data-ttu-id="14d85-283">EventType</span><span class="sxs-lookup"><span data-stu-id="14d85-283">EventType</span></span>       | <span data-ttu-id="14d85-284">Payload オブジェクト</span><span class="sxs-lookup"><span data-stu-id="14d85-284">Payload object</span></span>   | <span data-ttu-id="14d85-285">説明</span><span class="sxs-lookup"><span data-stu-id="14d85-285">Description</span></span>                                                             | <span data-ttu-id="14d85-286">範囲</span><span class="sxs-lookup"><span data-stu-id="14d85-286">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="14d85-287">messageReaction</span><span class="sxs-lookup"><span data-stu-id="14d85-287">messageReaction</span></span> | <span data-ttu-id="14d85-288">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="14d85-288">reactionsAdded</span></span>   | [<span data-ttu-id="14d85-289">ボット メッセージへの反応</span><span class="sxs-lookup"><span data-stu-id="14d85-289">Reactions to a bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="14d85-290">すべて</span><span class="sxs-lookup"><span data-stu-id="14d85-290">All</span></span>   |
| <span data-ttu-id="14d85-291">messageReaction</span><span class="sxs-lookup"><span data-stu-id="14d85-291">messageReaction</span></span> | <span data-ttu-id="14d85-292">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="14d85-292">reactionsRemoved</span></span> | [<span data-ttu-id="14d85-293">ボット メッセージから削除されたリアクション</span><span class="sxs-lookup"><span data-stu-id="14d85-293">Reactions removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="14d85-294">すべて</span><span class="sxs-lookup"><span data-stu-id="14d85-294">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="14d85-295">ボット メッセージへの反応</span><span class="sxs-lookup"><span data-stu-id="14d85-295">Reactions to a bot message</span></span>

<span data-ttu-id="14d85-296">次のコードは、ボット メッセージに対する反応の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-296">The following code shows an example of reactions to a bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-297">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-297">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnReactionsAddedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You reacted with '{reaction.Type}' to the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-298">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-298">TypeScript</span></span>](#tab/typescript)

<!-- Verify -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsAdded(async (context, next) => {
           const reactionsAdded = context.activity.reactionsAdded;
            if (reactionsAdded && reactionsAdded.length > 0) {
                for (let i = 0; i < reactionsAdded.length; i++) {
                    const reaction = reactionsAdded[i];
                    const newReaction = `You reacted with '${reaction.type}' to the following message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="14d85-299">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-299">JSON</span></span>](#tab/json)

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
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[<span data-ttu-id="14d85-300">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-300">Python</span></span>](#tab/python)

```python
async def on_reactions_added(
    self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
    for reaction in message_reactions:
        activity = await self._log.find(turn_context.activity.reply_to_id)
        if not activity:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"Activity {turn_context.activity.reply_to_id} not found in log",
            )
        else:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"You added '{reaction.type}' regarding '{activity.text}'",
            )
    return
```

* * *

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="14d85-301">ボット メッセージから削除されたリアクション</span><span class="sxs-lookup"><span data-stu-id="14d85-301">Reactions removed from bot message</span></span>

<span data-ttu-id="14d85-302">次のコードは、ボット メッセージから削除された反応の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="14d85-302">The following code shows an example of reactions removed from bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="14d85-303">C#</span><span class="sxs-lookup"><span data-stu-id="14d85-303">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnReactionsRemovedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You removed the reaction '{reaction.Type}' from the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="14d85-304">TypeScript</span><span class="sxs-lookup"><span data-stu-id="14d85-304">TypeScript</span></span>](#tab/typescript)

<!-- Verify -->

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsRemoved(async(context,next)=>{
            const reactionsRemoved = context.activity.reactionsRemoved;
            if (reactionsRemoved && reactionsRemoved.length > 0) {
                for (let i = 0; i < reactionsRemoved.length; i++) {
                    const reaction = reactionsRemoved[i];
                    const newReaction = `You removed the reaction '${reaction.type}' from the message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="14d85-305">JSON</span><span class="sxs-lookup"><span data-stu-id="14d85-305">JSON</span></span>](#tab/json)

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
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[<span data-ttu-id="14d85-306">Python</span><span class="sxs-lookup"><span data-stu-id="14d85-306">Python</span></span>](#tab/python)

```python
async def on_reactions_removed(
    self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
    for reaction in message_reactions:
        activity = await self._log.find(turn_context.activity.reply_to_id)
        if not activity:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"Activity {turn_context.activity.reply_to_id} not found in log",
            )
        else:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"You removed '{reaction.type}' regarding '{activity.text}'",
            )
    return
```

* * *

## <a name="code-sample"></a><span data-ttu-id="14d85-307">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="14d85-307">Code sample</span></span>

<span data-ttu-id="14d85-308">次の表に、ボットの会話イベントを Teams アプリケーションに組み込む簡単なコード サンプルを示します。</span><span class="sxs-lookup"><span data-stu-id="14d85-308">The following table provides a simple code sample that incorporates bots conversation events into a Teams application:</span></span>

| <span data-ttu-id="14d85-309">サンプル</span><span class="sxs-lookup"><span data-stu-id="14d85-309">Sample</span></span> | <span data-ttu-id="14d85-310">説明</span><span class="sxs-lookup"><span data-stu-id="14d85-310">Description</span></span> | <span data-ttu-id="14d85-311">.NET Core</span><span class="sxs-lookup"><span data-stu-id="14d85-311">.NET Core</span></span> |
|--------|------------- |---|
| <span data-ttu-id="14d85-312">Teams ボットの会話イベントのサンプル</span><span class="sxs-lookup"><span data-stu-id="14d85-312">Teams bots conversation events sample</span></span> | <span data-ttu-id="14d85-313">Teams のボット フレームワーク v4 会話ボットのサンプル。</span><span class="sxs-lookup"><span data-stu-id="14d85-313">Bot Framework v4 conversation bot sample for Teams.</span></span> | [<span data-ttu-id="14d85-314">View</span><span class="sxs-lookup"><span data-stu-id="14d85-314">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|

## <a name="next-step"></a><span data-ttu-id="14d85-315">次の手順</span><span class="sxs-lookup"><span data-stu-id="14d85-315">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="14d85-316">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="14d85-316">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
