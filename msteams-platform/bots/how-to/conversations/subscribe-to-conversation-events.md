---
title: 会話イベントにサブスクライブする
author: WashingtonKayaker
description: Microsoft Teams ボットから会話イベントをサブスクライブする方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: bc4ae36d8cffe5b19ee778a71e1c7b1c00c5e88c
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634503"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="8168b-103">会話イベントにサブスクライブする</span><span class="sxs-lookup"><span data-stu-id="8168b-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="8168b-104">Microsoft Teams はボットがアクティブな範囲で発生するイベントの通知をボットに送ります。</span><span class="sxs-lookup"><span data-stu-id="8168b-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="8168b-105">コードでこれらのイベントをキャプチャして、次のようなアクションを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="8168b-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="8168b-106">ボットをチームに追加するときにウェルカム メッセージをトリガーする</span><span class="sxs-lookup"><span data-stu-id="8168b-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="8168b-107">新しいチーム メンバーが追加または削除されると、ウェルカム メッセージをトリガーする</span><span class="sxs-lookup"><span data-stu-id="8168b-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="8168b-108">チャネルの作成、名前の変更、または削除時に通知をトリガーする</span><span class="sxs-lookup"><span data-stu-id="8168b-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="8168b-109">ボット メッセージがユーザーに気に入らされた場合</span><span class="sxs-lookup"><span data-stu-id="8168b-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="8168b-110">会話の更新イベント</span><span class="sxs-lookup"><span data-stu-id="8168b-110">Conversation update events</span></span>

> [!Important]
> <span data-ttu-id="8168b-111">新しいイベントはいつでも追加できます。ボットは受信を開始します。</span><span class="sxs-lookup"><span data-stu-id="8168b-111">New events can be added at any time, and your bot will begin to receive them.</span></span>
> <span data-ttu-id="8168b-112">予期しないイベントを受け取る可能性を設計する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8168b-112">You must design for the possibility of receiving unexpected events.</span></span>
> <span data-ttu-id="8168b-113">Bot Framework SDK を使用している場合、ボットは処理を選択しないイベントに対して自動的 `200 - OK` に応答します。</span><span class="sxs-lookup"><span data-stu-id="8168b-113">If you are using the Bot Framework SDK, your bot will automatically respond with a `200 - OK` to any events you do not choose to handle.</span></span>

<span data-ttu-id="8168b-114">会話にボットが追加されたとき、他のメンバーが会話に追加または会話から削除されたとき、会話のメタデータが変更されたときに、ボットは `conversationUpdate` イベントを受信します。</span><span class="sxs-lookup"><span data-stu-id="8168b-114">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="8168b-115">`conversationUpdate` イベントは、ボットが追加されているチームのメンバーシップの更新に関する情報を受信したときにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-115">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="8168b-116">また、ボットが特定の個人の会話に初めて追加されたときにも更新を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="8168b-116">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="8168b-117">次の表に、Teams の会話更新イベントの一覧と、詳細へのリンクを示します。</span><span class="sxs-lookup"><span data-stu-id="8168b-117">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="8168b-118">アクションの実行</span><span class="sxs-lookup"><span data-stu-id="8168b-118">Action Taken</span></span>        | <span data-ttu-id="8168b-119">EventType</span><span class="sxs-lookup"><span data-stu-id="8168b-119">EventType</span></span>         | <span data-ttu-id="8168b-120">呼び出されるメソッド</span><span class="sxs-lookup"><span data-stu-id="8168b-120">Method Called</span></span>              | <span data-ttu-id="8168b-121">説明</span><span class="sxs-lookup"><span data-stu-id="8168b-121">Description</span></span>                | <span data-ttu-id="8168b-122">範囲</span><span class="sxs-lookup"><span data-stu-id="8168b-122">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="8168b-123">作成されたチャネル</span><span class="sxs-lookup"><span data-stu-id="8168b-123">channel created</span></span>     | <span data-ttu-id="8168b-124">channelCreated</span><span class="sxs-lookup"><span data-stu-id="8168b-124">channelCreated</span></span>    | <span data-ttu-id="8168b-125">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-125">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="8168b-126">チャネルが作成されました</span><span class="sxs-lookup"><span data-stu-id="8168b-126">A channel was created</span></span>](#channel-created) | <span data-ttu-id="8168b-127">チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-127">Team</span></span> |
| <span data-ttu-id="8168b-128">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="8168b-128">channel renamed</span></span>     | <span data-ttu-id="8168b-129">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="8168b-129">channelRenamed</span></span>    | <span data-ttu-id="8168b-130">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-130">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="8168b-131">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="8168b-131">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="8168b-132">チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-132">Team</span></span> |
| <span data-ttu-id="8168b-133">チャネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="8168b-133">channel deleted</span></span>     | <span data-ttu-id="8168b-134">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="8168b-134">channelDeleted</span></span>    | <span data-ttu-id="8168b-135">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-135">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="8168b-136">チャネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="8168b-136">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="8168b-137">チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-137">Team</span></span> |
| <span data-ttu-id="8168b-138">チャネルの復元</span><span class="sxs-lookup"><span data-stu-id="8168b-138">channel restored</span></span>    | <span data-ttu-id="8168b-139">channelRestored</span><span class="sxs-lookup"><span data-stu-id="8168b-139">channelRestored</span></span>    | <span data-ttu-id="8168b-140">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-140">OnTeamsChannelRestoredAsync</span></span> | [<span data-ttu-id="8168b-141">チャネルが復元された</span><span class="sxs-lookup"><span data-stu-id="8168b-141">A channel was restored</span></span>](#channel-deleted) | <span data-ttu-id="8168b-142">チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-142">Team</span></span> |
| <span data-ttu-id="8168b-143">追加されたメンバー</span><span class="sxs-lookup"><span data-stu-id="8168b-143">members added</span></span>   | <span data-ttu-id="8168b-144">membersAdded</span><span class="sxs-lookup"><span data-stu-id="8168b-144">membersAdded</span></span>   | <span data-ttu-id="8168b-145">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-145">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="8168b-146">追加されたメンバー</span><span class="sxs-lookup"><span data-stu-id="8168b-146">A member added</span></span>](#team-members-added)   | <span data-ttu-id="8168b-147">すべて</span><span class="sxs-lookup"><span data-stu-id="8168b-147">All</span></span> |
| <span data-ttu-id="8168b-148">メンバーが削除されました</span><span class="sxs-lookup"><span data-stu-id="8168b-148">members removed</span></span> | <span data-ttu-id="8168b-149">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="8168b-149">membersRemoved</span></span> | <span data-ttu-id="8168b-150">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-150">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="8168b-151">メンバーが削除されました</span><span class="sxs-lookup"><span data-stu-id="8168b-151">A member was removed</span></span>](#team-members-removed) | <span data-ttu-id="8168b-152">groupChat & チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-152">groupChat & team</span></span> |
| <span data-ttu-id="8168b-153">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="8168b-153">team renamed</span></span>        | <span data-ttu-id="8168b-154">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="8168b-154">teamRenamed</span></span>       | <span data-ttu-id="8168b-155">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-155">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="8168b-156">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="8168b-156">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="8168b-157">チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-157">Team</span></span> |
| <span data-ttu-id="8168b-158">チームが削除されました</span><span class="sxs-lookup"><span data-stu-id="8168b-158">team deleted</span></span>        | <span data-ttu-id="8168b-159">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="8168b-159">teamDeleted</span></span>       | <span data-ttu-id="8168b-160">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-160">OnTeamsTeamDeletedAsync</span></span>    | [<span data-ttu-id="8168b-161">チームが削除されました</span><span class="sxs-lookup"><span data-stu-id="8168b-161">A Team was deleted</span></span>](#team-deleted)       | <span data-ttu-id="8168b-162">チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-162">Team</span></span> |
| <span data-ttu-id="8168b-163">チームのアーカイブ</span><span class="sxs-lookup"><span data-stu-id="8168b-163">team archived</span></span>        | <span data-ttu-id="8168b-164">teamArchived</span><span class="sxs-lookup"><span data-stu-id="8168b-164">teamArchived</span></span>       | <span data-ttu-id="8168b-165">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-165">OnTeamsTeamArchivedAsync</span></span>    | [<span data-ttu-id="8168b-166">チームがアーカイブされた</span><span class="sxs-lookup"><span data-stu-id="8168b-166">A Team was archived</span></span>](#team-archived)       | <span data-ttu-id="8168b-167">チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-167">Team</span></span> |
| <span data-ttu-id="8168b-168">team unarchived</span><span class="sxs-lookup"><span data-stu-id="8168b-168">team unarchived</span></span>        | <span data-ttu-id="8168b-169">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="8168b-169">teamUnarchived</span></span>       | <span data-ttu-id="8168b-170">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-170">OnTeamsTeamUnarchivedAsync</span></span>    | [<span data-ttu-id="8168b-171">チームがアーカイブされていない</span><span class="sxs-lookup"><span data-stu-id="8168b-171">A Team was unarchived</span></span>](#team-unarchived)       | <span data-ttu-id="8168b-172">チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-172">Team</span></span> |
| <span data-ttu-id="8168b-173">チームの復元</span><span class="sxs-lookup"><span data-stu-id="8168b-173">team restored</span></span>        | <span data-ttu-id="8168b-174">teamRestored</span><span class="sxs-lookup"><span data-stu-id="8168b-174">teamRestored</span></span>      | <span data-ttu-id="8168b-175">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="8168b-175">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="8168b-176">チームが復元されました</span><span class="sxs-lookup"><span data-stu-id="8168b-176">A Team was restored</span></span>](#team-restored)       | <span data-ttu-id="8168b-177">チーム</span><span class="sxs-lookup"><span data-stu-id="8168b-177">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="8168b-178">作成されたチャネル</span><span class="sxs-lookup"><span data-stu-id="8168b-178">Channel created</span></span>

<span data-ttu-id="8168b-179">作成されたチャネル イベントは、ボットがインストールされているチームで新しいチャネルが作成されるたびにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-179">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-180">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-181">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-181">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-182">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-182">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-183">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-183">Python</span></span>](#tab/python)

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

### <a name="channel-renamed"></a><span data-ttu-id="8168b-184">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="8168b-184">Channel renamed</span></span>

<span data-ttu-id="8168b-185">チャネルの名前が変更されたイベントは、ボットがインストールされているチームでチャネルの名前が変更されるたびにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-185">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-186">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-186">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-187">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-187">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-188">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-189">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-189">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="8168b-190">チャネル削除済み</span><span class="sxs-lookup"><span data-stu-id="8168b-190">Channel Deleted</span></span>

<span data-ttu-id="8168b-191">チャネル削除イベントは、ボットがインストールされているチームでチャネルが削除されるたびにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-191">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-193">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-194">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-194">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-195">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-195">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="8168b-196">チャネルの復元</span><span class="sxs-lookup"><span data-stu-id="8168b-196">Channel restored</span></span>

<span data-ttu-id="8168b-197">以前に削除されたチャネルが、ボットが既にインストールされているチームで復元されるたびに、チャネル復元イベントがボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-197">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team that your bot is already installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-198">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-199">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-199">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-200">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-200">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-201">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-201">Python</span></span>](#tab/python)

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

### <a name="team-members-added"></a><span data-ttu-id="8168b-202">チーム メンバーの追加</span><span class="sxs-lookup"><span data-stu-id="8168b-202">Team members added</span></span>

<span data-ttu-id="8168b-203">イベントは、会話に初めて追加され、ボットがインストールされているチームまたはグループ チャットに新しいユーザーが追加される度にボット `teamMemberAdded` に送信されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-203">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="8168b-204">ユーザー情報 (ID) はボットに対して一意であり、サービスが将来使用するためにキャッシュできます (特定のユーザーにメッセージを送信するなど)。</span><span class="sxs-lookup"><span data-stu-id="8168b-204">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-205">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-205">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-206">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-206">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-207">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-207">JSON</span></span>](#tab/json)

<span data-ttu-id="8168b-208">これは、ボットがチームに追加された場合にボットが受信 **するメッセージです**。</span><span class="sxs-lookup"><span data-stu-id="8168b-208">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="8168b-209">これは、ボットが 1 対 1 のチャットに \* を追加するときにボットが *受信するメッセージです*。</span><span class="sxs-lookup"><span data-stu-id="8168b-209">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="8168b-210">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-210">Python</span></span>](#tab/python)

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

### <a name="team-members-removed"></a><span data-ttu-id="8168b-211">チーム メンバーが削除されました</span><span class="sxs-lookup"><span data-stu-id="8168b-211">Team members removed</span></span>

<span data-ttu-id="8168b-212">イベントは、チームから削除され、ボットがメンバーであるチームからユーザーが削除される度にボット `teamMemberRemoved` に送信されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-212">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="8168b-213">削除された新しいメンバーがボット自体かユーザーかは、 のオブジェクトを見て `Activity` 判断できます `turnContext` 。</span><span class="sxs-lookup"><span data-stu-id="8168b-213">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="8168b-214">オブジェクトのフィールドがオブジェクトのフィールドと同じ場合、削除されたメンバーはボット、それ以外の場合はユーザー `Id` `MembersRemoved` `Id` `Recipient` です。</span><span class="sxs-lookup"><span data-stu-id="8168b-214">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise, it is a user.</span></span>  <span data-ttu-id="8168b-215">ボットは通常、 `Id` 次の値を使用します。 `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="8168b-215">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="8168b-216">ユーザーがテナントから完全に削除されると、 `membersRemoved conversationUpdate` イベントがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="8168b-216">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-217">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-217">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-218">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-218">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-219">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-219">JSON</span></span>](#tab/json)

<span data-ttu-id="8168b-220">次のペイロード例のオブジェクトは、グループ チャットではなくチームにメンバーを追加するか、新しい 1 対 1 の会話を `channelData` 開始します。</span><span class="sxs-lookup"><span data-stu-id="8168b-220">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="8168b-221">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-221">Python</span></span>](#tab/python)

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

### <a name="team-renamed"></a><span data-ttu-id="8168b-222">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="8168b-222">Team renamed</span></span>

<span data-ttu-id="8168b-223">ボットが含むチームの名前が変更された場合、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-223">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="8168b-224">オブジェクトで `conversationUpdate` イベントを `eventType.teamRenamed` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="8168b-224">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-225">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-225">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-226">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-226">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-227">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-227">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-228">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-228">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-deleted"></a><span data-ttu-id="8168b-229">チームが削除されました</span><span class="sxs-lookup"><span data-stu-id="8168b-229">Team deleted</span></span>

<span data-ttu-id="8168b-230">ボットが含むチームが削除された場合、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-230">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="8168b-231">オブジェクトで `conversationUpdate` イベントを `eventType.teamDeleted` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="8168b-231">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-232">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-232">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-233">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-233">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-234">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-234">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-235">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-235">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="8168b-236">チームの復元</span><span class="sxs-lookup"><span data-stu-id="8168b-236">Team restored</span></span>

<span data-ttu-id="8168b-237">チームが削除から復元された場合、ボットは通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="8168b-237">The bot receives a notification when the team is restored from deletion.</span></span> <span data-ttu-id="8168b-238">ボットは、オブジェクト `conversationUpdate` 内でイベント `eventType.teamrestored` を受信 `channelData` します。</span><span class="sxs-lookup"><span data-stu-id="8168b-238">The bot receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-239">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-239">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-240">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-240">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-241">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-241">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-242">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-242">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="8168b-243">チームのアーカイブ</span><span class="sxs-lookup"><span data-stu-id="8168b-243">Team archived</span></span>

<span data-ttu-id="8168b-244">ボットは、インストールされているチームがアーカイブされる際に通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="8168b-244">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="8168b-245">オブジェクトで `conversationUpdate` イベントを `eventType.teamarchived` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="8168b-245">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-246">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-246">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-247">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-247">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-248">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-248">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-249">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-249">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *


### <a name="team-unarchived"></a><span data-ttu-id="8168b-250">チームのアーカイブ解除</span><span class="sxs-lookup"><span data-stu-id="8168b-250">Team unarchived</span></span>

<span data-ttu-id="8168b-251">ボットがインストールされているチームがアーカイブ解除された場合、ボットは通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="8168b-251">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="8168b-252">オブジェクトで `conversationUpdate` イベントを `eventType.teamUnarchived` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="8168b-252">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-253">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-253">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-254">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-254">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-255">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-255">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-256">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-256">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="8168b-257">メッセージの反応イベント</span><span class="sxs-lookup"><span data-stu-id="8168b-257">Message reaction events</span></span>

<span data-ttu-id="8168b-258">ユーザーがボットから送信されたメッセージに対する反応を追加または削除すると、イベント `messageReaction` が送信されます。</span><span class="sxs-lookup"><span data-stu-id="8168b-258">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="8168b-259">には `replyToId` 、特定のメッセージの ID が含まれているし、テキスト形式での反応 `Type` の種類です。</span><span class="sxs-lookup"><span data-stu-id="8168b-259">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="8168b-260">反応の種類には、"怒っている"、"ハート"、"笑い"、"like"、"Sad"、"驚いた"が含まれます。</span><span class="sxs-lookup"><span data-stu-id="8168b-260">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="8168b-261">このイベントには元のメッセージの内容が含まれているので、メッセージに対する処理の反応がボットにとって重要な場合は、メッセージを送信するときにメッセージを保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8168b-261">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="8168b-262">EventType</span><span class="sxs-lookup"><span data-stu-id="8168b-262">EventType</span></span>       | <span data-ttu-id="8168b-263">Payload オブジェクト</span><span class="sxs-lookup"><span data-stu-id="8168b-263">Payload object</span></span>   | <span data-ttu-id="8168b-264">説明</span><span class="sxs-lookup"><span data-stu-id="8168b-264">Description</span></span>                                                             | <span data-ttu-id="8168b-265">範囲</span><span class="sxs-lookup"><span data-stu-id="8168b-265">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="8168b-266">messageReaction</span><span class="sxs-lookup"><span data-stu-id="8168b-266">messageReaction</span></span> | <span data-ttu-id="8168b-267">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="8168b-267">reactionsAdded</span></span>   | [<span data-ttu-id="8168b-268">ボット メッセージへの反応</span><span class="sxs-lookup"><span data-stu-id="8168b-268">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="8168b-269">すべて</span><span class="sxs-lookup"><span data-stu-id="8168b-269">All</span></span>   |
| <span data-ttu-id="8168b-270">messageReaction</span><span class="sxs-lookup"><span data-stu-id="8168b-270">messageReaction</span></span> | <span data-ttu-id="8168b-271">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="8168b-271">reactionsRemoved</span></span> | [<span data-ttu-id="8168b-272">ボット メッセージから削除された反応</span><span class="sxs-lookup"><span data-stu-id="8168b-272">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="8168b-273">すべて</span><span class="sxs-lookup"><span data-stu-id="8168b-273">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="8168b-274">ボット メッセージへの反応</span><span class="sxs-lookup"><span data-stu-id="8168b-274">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-275">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-275">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-276">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-276">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-277">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-277">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-278">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-278">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="8168b-279">ボット メッセージから削除されたリアクション</span><span class="sxs-lookup"><span data-stu-id="8168b-279">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8168b-280">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8168b-280">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8168b-281">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8168b-281">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="8168b-282">JSON</span><span class="sxs-lookup"><span data-stu-id="8168b-282">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8168b-283">Python</span><span class="sxs-lookup"><span data-stu-id="8168b-283">Python</span></span>](#tab/python)

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

## <a name="samples"></a><span data-ttu-id="8168b-284">サンプル</span><span class="sxs-lookup"><span data-stu-id="8168b-284">Samples</span></span>

<span data-ttu-id="8168b-285">ボットの会話イベントを示すサンプル コードについては、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8168b-285">For sample code showing the bots conversation events, see:</span></span>

[<span data-ttu-id="8168b-286">Microsoft Teams ボットの会話イベントのサンプル</span><span class="sxs-lookup"><span data-stu-id="8168b-286">Microsoft Teams bots conversation events sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)



