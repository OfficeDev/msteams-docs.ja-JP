---
title: 会話イベントにサブスクライブする
author: WashingtonKayaker
description: Microsoft Teams ボットから会話イベントをサブスクライブする方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 17d13d51ab26aba60defb962dd425c1aed5b4133
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911962"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="e39ae-103">会話イベントにサブスクライブする</span><span class="sxs-lookup"><span data-stu-id="e39ae-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="e39ae-104">Microsoft Teams はボットがアクティブな範囲で発生するイベントの通知をボットに送ります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="e39ae-105">コードでこれらのイベントをキャプチャして、次のようなアクションを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="e39ae-106">ボットがチームに追加されるとウェルカム メッセージをトリガーする</span><span class="sxs-lookup"><span data-stu-id="e39ae-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="e39ae-107">新しいチーム メンバーが追加または削除されると、ウェルカム メッセージをトリガーする</span><span class="sxs-lookup"><span data-stu-id="e39ae-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="e39ae-108">チャネルの作成、名前の変更、または削除時に通知をトリガーする</span><span class="sxs-lookup"><span data-stu-id="e39ae-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="e39ae-109">ボット メッセージがユーザーに 「いいね!」と付けらた場合</span><span class="sxs-lookup"><span data-stu-id="e39ae-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="e39ae-110">会話の更新イベント</span><span class="sxs-lookup"><span data-stu-id="e39ae-110">Conversation update events</span></span>

> [!Important]
> <span data-ttu-id="e39ae-111">新しいイベントはいつでも追加できます。ボットはそれらを受信し始めるでしょう。</span><span class="sxs-lookup"><span data-stu-id="e39ae-111">New events can be added at any time, and your bot will begin to receive them.</span></span>
> <span data-ttu-id="e39ae-112">予期しないイベントが発生する可能性を設計する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-112">You must design for the possibility of receiving unexpected events.</span></span>
> <span data-ttu-id="e39ae-113">Bot Framework SDK を使用している場合、ボットは処理を選択しないイベントに自動的 `200 - OK` に応答します。</span><span class="sxs-lookup"><span data-stu-id="e39ae-113">If you are using the Bot Framework SDK, your bot will automatically respond with a `200 - OK` to any events you do not choose to handle.</span></span>

<span data-ttu-id="e39ae-114">会話にボットが追加されたとき、他のメンバーが会話に追加または会話から削除されたとき、会話のメタデータが変更されたときに、ボットは `conversationUpdate` イベントを受信します。</span><span class="sxs-lookup"><span data-stu-id="e39ae-114">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="e39ae-115">`conversationUpdate` イベントは、ボットが追加されているチームのメンバーシップの更新に関する情報を受信したときにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-115">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="e39ae-116">また、ボットが特定の個人の会話に初めて追加されたときにも更新を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-116">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="e39ae-117">次の表に、Teams の会話更新イベントの一覧と、詳細へのリンクを示します。</span><span class="sxs-lookup"><span data-stu-id="e39ae-117">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="e39ae-118">実行されたアクション</span><span class="sxs-lookup"><span data-stu-id="e39ae-118">Action Taken</span></span>        | <span data-ttu-id="e39ae-119">EventType</span><span class="sxs-lookup"><span data-stu-id="e39ae-119">EventType</span></span>         | <span data-ttu-id="e39ae-120">呼び出されるメソッド</span><span class="sxs-lookup"><span data-stu-id="e39ae-120">Method Called</span></span>              | <span data-ttu-id="e39ae-121">説明</span><span class="sxs-lookup"><span data-stu-id="e39ae-121">Description</span></span>                | <span data-ttu-id="e39ae-122">範囲</span><span class="sxs-lookup"><span data-stu-id="e39ae-122">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="e39ae-123">チャネルが作成されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-123">channel created</span></span>     | <span data-ttu-id="e39ae-124">channelCreated</span><span class="sxs-lookup"><span data-stu-id="e39ae-124">channelCreated</span></span>    | <span data-ttu-id="e39ae-125">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="e39ae-125">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="e39ae-126">チャネルが作成されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-126">A channel was created</span></span>](#channel-created) | <span data-ttu-id="e39ae-127">チーム</span><span class="sxs-lookup"><span data-stu-id="e39ae-127">Team</span></span> |
| <span data-ttu-id="e39ae-128">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-128">channel renamed</span></span>     | <span data-ttu-id="e39ae-129">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="e39ae-129">channelRenamed</span></span>    | <span data-ttu-id="e39ae-130">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="e39ae-130">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="e39ae-131">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-131">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="e39ae-132">チーム</span><span class="sxs-lookup"><span data-stu-id="e39ae-132">Team</span></span> |
| <span data-ttu-id="e39ae-133">チャネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-133">channel deleted</span></span>     | <span data-ttu-id="e39ae-134">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="e39ae-134">channelDeleted</span></span>    | <span data-ttu-id="e39ae-135">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="e39ae-135">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="e39ae-136">チャネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-136">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="e39ae-137">チーム</span><span class="sxs-lookup"><span data-stu-id="e39ae-137">Team</span></span> |
| <span data-ttu-id="e39ae-138">チャネルの復元</span><span class="sxs-lookup"><span data-stu-id="e39ae-138">channel restored</span></span>    | <span data-ttu-id="e39ae-139">channelRestored</span><span class="sxs-lookup"><span data-stu-id="e39ae-139">channelRestored</span></span>    | <span data-ttu-id="e39ae-140">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="e39ae-140">OnTeamsChannelRestoredAsync</span></span> | [<span data-ttu-id="e39ae-141">チャネルが復元されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-141">A channel was restored</span></span>](#channel-deleted) | <span data-ttu-id="e39ae-142">チーム</span><span class="sxs-lookup"><span data-stu-id="e39ae-142">Team</span></span> |
| <span data-ttu-id="e39ae-143">追加されたメンバー</span><span class="sxs-lookup"><span data-stu-id="e39ae-143">members added</span></span>   | <span data-ttu-id="e39ae-144">membersAdded</span><span class="sxs-lookup"><span data-stu-id="e39ae-144">membersAdded</span></span>   | <span data-ttu-id="e39ae-145">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="e39ae-145">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="e39ae-146">追加されたメンバー</span><span class="sxs-lookup"><span data-stu-id="e39ae-146">A member added</span></span>](#team-members-added)   | <span data-ttu-id="e39ae-147">すべて</span><span class="sxs-lookup"><span data-stu-id="e39ae-147">All</span></span> |
| <span data-ttu-id="e39ae-148">メンバーの削除</span><span class="sxs-lookup"><span data-stu-id="e39ae-148">members removed</span></span> | <span data-ttu-id="e39ae-149">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="e39ae-149">membersRemoved</span></span> | <span data-ttu-id="e39ae-150">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="e39ae-150">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="e39ae-151">メンバーが削除されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-151">A member was removed</span></span>](#team-members-removed) | <span data-ttu-id="e39ae-152">groupChat & team</span><span class="sxs-lookup"><span data-stu-id="e39ae-152">groupChat & team</span></span> |
| <span data-ttu-id="e39ae-153">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-153">team renamed</span></span>        | <span data-ttu-id="e39ae-154">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="e39ae-154">teamRenamed</span></span>       | <span data-ttu-id="e39ae-155">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="e39ae-155">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="e39ae-156">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-156">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="e39ae-157">チーム</span><span class="sxs-lookup"><span data-stu-id="e39ae-157">Team</span></span> |
| <span data-ttu-id="e39ae-158">チームのアーカイブ</span><span class="sxs-lookup"><span data-stu-id="e39ae-158">team archived</span></span>        | <span data-ttu-id="e39ae-159">teamArchived</span><span class="sxs-lookup"><span data-stu-id="e39ae-159">teamArchived</span></span>       | <span data-ttu-id="e39ae-160">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="e39ae-160">OnTeamsTeamArchivedAsync</span></span>    | [<span data-ttu-id="e39ae-161">チームがアーカイブされました</span><span class="sxs-lookup"><span data-stu-id="e39ae-161">A Team was archived</span></span>](#team-archived)       | <span data-ttu-id="e39ae-162">チーム</span><span class="sxs-lookup"><span data-stu-id="e39ae-162">Team</span></span> |
| <span data-ttu-id="e39ae-163">チームの復元</span><span class="sxs-lookup"><span data-stu-id="e39ae-163">team restored</span></span>        | <span data-ttu-id="e39ae-164">teamRestored</span><span class="sxs-lookup"><span data-stu-id="e39ae-164">teamRestored</span></span>      | <span data-ttu-id="e39ae-165">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="e39ae-165">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="e39ae-166">チームの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-166">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="e39ae-167">チーム</span><span class="sxs-lookup"><span data-stu-id="e39ae-167">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="e39ae-168">チャネルの作成</span><span class="sxs-lookup"><span data-stu-id="e39ae-168">Channel created</span></span>

<span data-ttu-id="e39ae-169">チャネル作成イベントは、ボットがインストールされているチームで新しいチャネルが作成されるたびにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-169">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-170">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-170">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-171">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-171">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-172">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-172">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e39ae-173">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-173">Python</span></span>](#tab/python)

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

### <a name="channel-renamed"></a><span data-ttu-id="e39ae-174">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="e39ae-174">Channel renamed</span></span>

<span data-ttu-id="e39ae-175">チャネル名が変更されたイベントは、ボットがインストールされているチームでチャネルの名前が変更されるたびにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-175">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-176">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-176">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-177">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-177">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-178">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-178">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e39ae-179">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-179">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="e39ae-180">Channel Deleted</span><span class="sxs-lookup"><span data-stu-id="e39ae-180">Channel Deleted</span></span>

<span data-ttu-id="e39ae-181">チャネル削除イベントは、ボットがインストールされているチームでチャネルが削除されるたびにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-181">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-182">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-182">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-183">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-183">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-184">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-184">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e39ae-185">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-185">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="e39ae-186">チャネルの復元</span><span class="sxs-lookup"><span data-stu-id="e39ae-186">Channel restored</span></span>

<span data-ttu-id="e39ae-187">以前に削除されたチャネルが、ボットが既にインストールされているチームで復元されるたびに、チャネル復元イベントがボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-187">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team that your bot is already installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-188">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-188">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-189">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-189">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-190">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-190">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e39ae-191">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-191">Python</span></span>](#tab/python)

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

### <a name="team-members-added"></a><span data-ttu-id="e39ae-192">チーム メンバーの追加</span><span class="sxs-lookup"><span data-stu-id="e39ae-192">Team members added</span></span>

<span data-ttu-id="e39ae-193">イベントは、初めて会話に追加された場合や、ボットがインストールされているチームまたはグループ チャットに新しいユーザーが追加されるたび、ボットに送信 `teamMemberAdded` されます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-193">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="e39ae-194">ユーザー情報 (ID) はボットに対して一意であり、サービスが将来使用するためにキャッシュできます (特定のユーザーへのメッセージの送信など)。</span><span class="sxs-lookup"><span data-stu-id="e39ae-194">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-195">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-195">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-196">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-196">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-197">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-197">JSON</span></span>](#tab/json)

<span data-ttu-id="e39ae-198">これは、ボットがチームに追加された場合にボットが受信 **するメッセージです**。</span><span class="sxs-lookup"><span data-stu-id="e39ae-198">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="e39ae-199">これは、ボットが 1 対 1 のチャットに \* を追加するときにボットが受信 *するメッセージです*。</span><span class="sxs-lookup"><span data-stu-id="e39ae-199">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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
    "aadObjectId": "**_"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "_*_"
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

# <a name="python"></a>[<span data-ttu-id="e39ae-200">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-200">Python</span></span>](#tab/python)

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

<span data-ttu-id="e39ae-201">_ \* \*</span><span class="sxs-lookup"><span data-stu-id="e39ae-201">_ \* \*</span></span>

### <a name="team-members-removed"></a><span data-ttu-id="e39ae-202">チーム メンバーの削除</span><span class="sxs-lookup"><span data-stu-id="e39ae-202">Team members removed</span></span>

<span data-ttu-id="e39ae-203">イベントがチームから削除され、ボットがメンバーであるチームからユーザーが削除されるたび、ボット `teamMemberRemoved` に送信されます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-203">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="e39ae-204">削除された新しいメンバーがボット自体かユーザーかは、次のオブジェクトを見て `Activity` 確認できます `turnContext` 。</span><span class="sxs-lookup"><span data-stu-id="e39ae-204">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="e39ae-205">オブジェクトのフィールドがオブジェクトのフィールドと同じ場合、削除されたメンバーはボット、それ以外の場合はユーザー `Id` `MembersRemoved` `Id` `Recipient` です。</span><span class="sxs-lookup"><span data-stu-id="e39ae-205">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise, it is a user.</span></span>  <span data-ttu-id="e39ae-206">通常、ボットは `Id` 次の条件を使用します。 `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="e39ae-206">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="e39ae-207">ユーザーがテナントから完全に削除されると、 `membersRemoved conversationUpdate` イベントがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-207">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-208">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-208">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-209">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-209">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-210">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-210">JSON</span></span>](#tab/json)

<span data-ttu-id="e39ae-211">次のペイロード例のオブジェクトは、グループ チャットではなくチームにメンバーを追加するか、新しい 1 対 1 の会話を開始します `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="e39ae-211">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="e39ae-212">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-212">Python</span></span>](#tab/python)

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

### <a name="team-renamed"></a><span data-ttu-id="e39ae-213">チームの名前の変更</span><span class="sxs-lookup"><span data-stu-id="e39ae-213">Team renamed</span></span>

<span data-ttu-id="e39ae-214">ボットは、チームの名前が変更された際に通知されます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-214">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="e39ae-215">オブジェクト内で `conversationUpdate` イベントを `eventType.teamRenamed` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-215">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-216">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-216">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-217">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-217">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-218">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-218">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e39ae-219">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-219">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="e39ae-220">チームのアーカイブ</span><span class="sxs-lookup"><span data-stu-id="e39ae-220">Team archived</span></span>

<span data-ttu-id="e39ae-221">ボットは、インストールされているチームがアーカイブされる際に通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-221">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="e39ae-222">オブジェクト内で `conversationUpdate` イベントを `eventType.teamarchived` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-222">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-223">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-223">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-224">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-224">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-225">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-225">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e39ae-226">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-226">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="e39ae-227">チームの復元</span><span class="sxs-lookup"><span data-stu-id="e39ae-227">Team restored</span></span>

<span data-ttu-id="e39ae-228">ボットは、インストールされているチームが復元された際に通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-228">The bot receives a notification when the team it is installed in is restored.</span></span> <span data-ttu-id="e39ae-229">オブジェクト内で `conversationUpdate` イベントを `eventType.teamrestored` 受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-229">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-230">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-230">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-231">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-231">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-232">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-232">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e39ae-233">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-233">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="e39ae-234">メッセージリアクション イベント</span><span class="sxs-lookup"><span data-stu-id="e39ae-234">Message reaction events</span></span>

<span data-ttu-id="e39ae-235">このイベントは、ボットによって送信されたメッセージに対するリアクションをユーザーが追加 `messageReaction` または削除すると送信されます。</span><span class="sxs-lookup"><span data-stu-id="e39ae-235">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="e39ae-236">特定 `replyToId` のメッセージの ID を含み、テキスト形式でのリアクション `Type` の種類です。</span><span class="sxs-lookup"><span data-stu-id="e39ae-236">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="e39ae-237">反応の種類には、"a立"、"heart"、"子"、"like"、"Sad"、"surprised" があります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-237">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="e39ae-238">このイベントには元のメッセージの内容が含まれているのではないので、メッセージに対する反応の処理がボットにとって重要な場合は、メッセージを送信するときにメッセージを保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e39ae-238">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="e39ae-239">EventType</span><span class="sxs-lookup"><span data-stu-id="e39ae-239">EventType</span></span>       | <span data-ttu-id="e39ae-240">Payload オブジェクト</span><span class="sxs-lookup"><span data-stu-id="e39ae-240">Payload object</span></span>   | <span data-ttu-id="e39ae-241">説明</span><span class="sxs-lookup"><span data-stu-id="e39ae-241">Description</span></span>                                                             | <span data-ttu-id="e39ae-242">範囲</span><span class="sxs-lookup"><span data-stu-id="e39ae-242">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="e39ae-243">messageReaction</span><span class="sxs-lookup"><span data-stu-id="e39ae-243">messageReaction</span></span> | <span data-ttu-id="e39ae-244">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="e39ae-244">reactionsAdded</span></span>   | [<span data-ttu-id="e39ae-245">ボット メッセージへの反応</span><span class="sxs-lookup"><span data-stu-id="e39ae-245">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="e39ae-246">すべて</span><span class="sxs-lookup"><span data-stu-id="e39ae-246">All</span></span>   |
| <span data-ttu-id="e39ae-247">messageReaction</span><span class="sxs-lookup"><span data-stu-id="e39ae-247">messageReaction</span></span> | <span data-ttu-id="e39ae-248">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="e39ae-248">reactionsRemoved</span></span> | [<span data-ttu-id="e39ae-249">ボット メッセージから削除されたリアクション</span><span class="sxs-lookup"><span data-stu-id="e39ae-249">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="e39ae-250">すべて</span><span class="sxs-lookup"><span data-stu-id="e39ae-250">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="e39ae-251">ボット メッセージに対する反応</span><span class="sxs-lookup"><span data-stu-id="e39ae-251">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-252">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-252">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-253">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-253">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-254">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-254">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e39ae-255">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-255">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="e39ae-256">ボット メッセージから削除されたリアクション</span><span class="sxs-lookup"><span data-stu-id="e39ae-256">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e39ae-257">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e39ae-257">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e39ae-258">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e39ae-258">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e39ae-259">JSON</span><span class="sxs-lookup"><span data-stu-id="e39ae-259">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e39ae-260">Python</span><span class="sxs-lookup"><span data-stu-id="e39ae-260">Python</span></span>](#tab/python)

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

## <a name="samples"></a><span data-ttu-id="e39ae-261">サンプル</span><span class="sxs-lookup"><span data-stu-id="e39ae-261">Samples</span></span>
<span data-ttu-id="e39ae-262">ボットの会話イベントを示すサンプル コードについては、次を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e39ae-262">For sample code showing the bots conversation events, see:</span></span>

[<span data-ttu-id="e39ae-263">Microsoft Teams ボット会話イベントのサンプル</span><span class="sxs-lookup"><span data-stu-id="e39ae-263">Microsoft Teams bots conversation events sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)



