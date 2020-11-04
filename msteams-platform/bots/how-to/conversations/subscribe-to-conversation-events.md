---
title: 会話イベントにサブスクライブする
author: WashingtonKayaker
description: Microsoft Teams bot からの会話イベントを購読する方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d6a385d4608239029a943c0a1365cfcb56b21b6b
ms.sourcegitcommit: df9448681d2a81f1029aad5a5e1989cd438d1ae0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "48877037"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="7a96c-103">会話イベントにサブスクライブする</span><span class="sxs-lookup"><span data-stu-id="7a96c-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="7a96c-104">Microsoft Teams はボットがアクティブな範囲で発生するイベントの通知をボットに送ります。</span><span class="sxs-lookup"><span data-stu-id="7a96c-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="7a96c-105">コードでこれらのイベントをキャプチャして、次のようなアクションを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="7a96c-106">Bot がチームに追加されたときに開始メッセージをトリガーする</span><span class="sxs-lookup"><span data-stu-id="7a96c-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="7a96c-107">新しいチームメンバーが追加または削除されたときに、開始メッセージをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="7a96c-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="7a96c-108">チャネルの作成、名前変更、または削除時に通知をトリガーする</span><span class="sxs-lookup"><span data-stu-id="7a96c-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="7a96c-109">Bot メッセージがユーザーによって好評になった場合</span><span class="sxs-lookup"><span data-stu-id="7a96c-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="7a96c-110">会話の更新イベント</span><span class="sxs-lookup"><span data-stu-id="7a96c-110">Conversation update events</span></span>

<span data-ttu-id="7a96c-111">会話にボットが追加されたとき、他のメンバーが会話に追加または会話から削除されたとき、会話のメタデータが変更されたときに、ボットは `conversationUpdate` イベントを受信します。</span><span class="sxs-lookup"><span data-stu-id="7a96c-111">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="7a96c-112">`conversationUpdate` イベントは、ボットが追加されているチームのメンバーシップの更新に関する情報を受信したときにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-112">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="7a96c-113">また、ボットが特定の個人の会話に初めて追加されたときにも更新を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="7a96c-113">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="7a96c-114">次の表に、チームの会話の更新イベントの一覧と、詳細情報へのリンクを示します。</span><span class="sxs-lookup"><span data-stu-id="7a96c-114">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="7a96c-115">実行されたアクション</span><span class="sxs-lookup"><span data-stu-id="7a96c-115">Action Taken</span></span>        | <span data-ttu-id="7a96c-116">EventType</span><span class="sxs-lookup"><span data-stu-id="7a96c-116">EventType</span></span>         | <span data-ttu-id="7a96c-117">メソッドの呼び出し先</span><span class="sxs-lookup"><span data-stu-id="7a96c-117">Method Called</span></span>              | <span data-ttu-id="7a96c-118">説明</span><span class="sxs-lookup"><span data-stu-id="7a96c-118">Description</span></span>                | <span data-ttu-id="7a96c-119">範囲</span><span class="sxs-lookup"><span data-stu-id="7a96c-119">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="7a96c-120">チャネルの作成</span><span class="sxs-lookup"><span data-stu-id="7a96c-120">channel created</span></span>     | <span data-ttu-id="7a96c-121">channelCreated</span><span class="sxs-lookup"><span data-stu-id="7a96c-121">channelCreated</span></span>    | <span data-ttu-id="7a96c-122">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="7a96c-122">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="7a96c-123">チャネルが作成されました</span><span class="sxs-lookup"><span data-stu-id="7a96c-123">A channel was created</span></span>](#channel-created) | <span data-ttu-id="7a96c-124">チーム</span><span class="sxs-lookup"><span data-stu-id="7a96c-124">Team</span></span> |
| <span data-ttu-id="7a96c-125">チャネル名の変更</span><span class="sxs-lookup"><span data-stu-id="7a96c-125">channel renamed</span></span>     | <span data-ttu-id="7a96c-126">channelRenamed 名前変更</span><span class="sxs-lookup"><span data-stu-id="7a96c-126">channelRenamed</span></span>    | <span data-ttu-id="7a96c-127">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="7a96c-127">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="7a96c-128">チャネルの名前が変更されました</span><span class="sxs-lookup"><span data-stu-id="7a96c-128">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="7a96c-129">チーム</span><span class="sxs-lookup"><span data-stu-id="7a96c-129">Team</span></span> |
| <span data-ttu-id="7a96c-130">チャネルの削除</span><span class="sxs-lookup"><span data-stu-id="7a96c-130">channel deleted</span></span>     | <span data-ttu-id="7a96c-131">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="7a96c-131">channelDeleted</span></span>    | <span data-ttu-id="7a96c-132">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="7a96c-132">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="7a96c-133">チャネルが削除されました</span><span class="sxs-lookup"><span data-stu-id="7a96c-133">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="7a96c-134">チーム</span><span class="sxs-lookup"><span data-stu-id="7a96c-134">Team</span></span> |
| <span data-ttu-id="7a96c-135">チームメンバーの追加</span><span class="sxs-lookup"><span data-stu-id="7a96c-135">team members added</span></span>   | <span data-ttu-id="7a96c-136">teamMemberAdded 済み</span><span class="sxs-lookup"><span data-stu-id="7a96c-136">teamMemberAdded</span></span>   | <span data-ttu-id="7a96c-137">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="7a96c-137">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="7a96c-138">チームに追加されたメンバー</span><span class="sxs-lookup"><span data-stu-id="7a96c-138">A Member added to team</span></span>](#team-members-added)   | <span data-ttu-id="7a96c-139">すべて</span><span class="sxs-lookup"><span data-stu-id="7a96c-139">All</span></span> |
| <span data-ttu-id="7a96c-140">チームメンバーの削除</span><span class="sxs-lookup"><span data-stu-id="7a96c-140">team members removed</span></span> | <span data-ttu-id="7a96c-141">teamMemberRemoved 済み</span><span class="sxs-lookup"><span data-stu-id="7a96c-141">teamMemberRemoved</span></span> | <span data-ttu-id="7a96c-142">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="7a96c-142">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="7a96c-143">メンバーがチームから削除されました</span><span class="sxs-lookup"><span data-stu-id="7a96c-143">A Member was removed from team</span></span>](#team-members-removed) | <span data-ttu-id="7a96c-144">groupChat & チーム</span><span class="sxs-lookup"><span data-stu-id="7a96c-144">groupChat & team</span></span> |
| <span data-ttu-id="7a96c-145">チームの名前変更</span><span class="sxs-lookup"><span data-stu-id="7a96c-145">team renamed</span></span>        | <span data-ttu-id="7a96c-146">teamRenamed 名前変更</span><span class="sxs-lookup"><span data-stu-id="7a96c-146">teamRenamed</span></span>       | <span data-ttu-id="7a96c-147">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="7a96c-147">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="7a96c-148">チームの名前が変更された</span><span class="sxs-lookup"><span data-stu-id="7a96c-148">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="7a96c-149">チーム</span><span class="sxs-lookup"><span data-stu-id="7a96c-149">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="7a96c-150">チャネルの作成</span><span class="sxs-lookup"><span data-stu-id="7a96c-150">Channel created</span></span>

<span data-ttu-id="7a96c-151">Bot がインストールされているチームに新しいチャネルが作成されるたびに、チャネル作成イベントが bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-151">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a96c-152">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a96c-152">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a96c-153">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a96c-153">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="7a96c-154">JSON</span><span class="sxs-lookup"><span data-stu-id="7a96c-154">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="7a96c-155">Python</span><span class="sxs-lookup"><span data-stu-id="7a96c-155">Python</span></span>](#tab/python)

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

### <a name="channel-renamed"></a><span data-ttu-id="7a96c-156">チャネル名の変更</span><span class="sxs-lookup"><span data-stu-id="7a96c-156">Channel renamed</span></span>

<span data-ttu-id="7a96c-157">「Bot がインストールされているチームでチャネルの名前が変更されるたびに、チャネルの名前が変更されたイベントが bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-157">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a96c-158">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a96c-158">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a96c-159">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a96c-159">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="7a96c-160">JSON</span><span class="sxs-lookup"><span data-stu-id="7a96c-160">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="7a96c-161">Python</span><span class="sxs-lookup"><span data-stu-id="7a96c-161">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="7a96c-162">チャネルの削除</span><span class="sxs-lookup"><span data-stu-id="7a96c-162">Channel Deleted</span></span>

<span data-ttu-id="7a96c-163">Bot がインストールされているチームでチャネルが削除されるたびに、チャネル削除イベントが bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-163">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a96c-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a96c-164">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a96c-165">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a96c-165">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="7a96c-166">JSON</span><span class="sxs-lookup"><span data-stu-id="7a96c-166">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="7a96c-167">Python</span><span class="sxs-lookup"><span data-stu-id="7a96c-167">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="team-members-added"></a><span data-ttu-id="7a96c-168">チームメンバーの追加</span><span class="sxs-lookup"><span data-stu-id="7a96c-168">Team members added</span></span>

<span data-ttu-id="7a96c-169">このイベントは、ユーザーが初めて会話に追加されたときに、bot がインストールされて `teamMemberAdded` いるチームまたはグループのチャットに新しいユーザーが追加されるたびに、bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-169">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="7a96c-170">ユーザー情報 (ID) は bot に対して一意であり、サービスが今後使用するためにキャッシュすることができます (たとえば、特定のユーザーにメッセージを送信するなど)。</span><span class="sxs-lookup"><span data-stu-id="7a96c-170">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a96c-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a96c-171">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<ChannelAccount> membersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersAdded)
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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a96c-172">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a96c-172">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="7a96c-173">JSON</span><span class="sxs-lookup"><span data-stu-id="7a96c-173">JSON</span></span>](#tab/json)

<span data-ttu-id="7a96c-174">これは、ボットが **チームに** 追加されたときに bot が受け取るメッセージです。</span><span class="sxs-lookup"><span data-stu-id="7a96c-174">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="7a96c-175">これは、ボットが *1 対1のチャットに* 追加された場合に、ボットが受け取るメッセージです。</span><span class="sxs-lookup"><span data-stu-id="7a96c-175">This is the message your bot will receive when the bot is added \* *to a one-to-one chat*.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="7a96c-176">Python</span><span class="sxs-lookup"><span data-stu-id="7a96c-176">Python</span></span>](#tab/python)

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

<span data-ttu-id="7a96c-177">_ \* \*</span><span class="sxs-lookup"><span data-stu-id="7a96c-177">_ \* \*</span></span>

### <a name="team-members-removed"></a><span data-ttu-id="7a96c-178">チームメンバーの削除</span><span class="sxs-lookup"><span data-stu-id="7a96c-178">Team members removed</span></span>

<span data-ttu-id="7a96c-179">`teamMemberRemoved`このイベントは、チームから削除され、bot がメンバーになっているチームからユーザーが削除されるたびに、bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-179">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="7a96c-180">が削除された新しいメンバーが bot 自体またはユーザーであったかどうかを調べるには、のオブジェクトを参照して `Activity` `turnContext` ください。</span><span class="sxs-lookup"><span data-stu-id="7a96c-180">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="7a96c-181">オブジェクトの `Id` フィールド `MembersRemoved` がオブジェクトのフィールドと同じ場合は、削除された `Id` `Recipient` メンバーが bot になります。それ以外の場合は、ユーザーになります。</span><span class="sxs-lookup"><span data-stu-id="7a96c-181">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise it is a user.</span></span>  <span data-ttu-id="7a96c-182">Bot は `Id` 通常、次のようになります。 `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="7a96c-182">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="7a96c-183">ユーザーがテナントから完全に削除されると、 `membersRemoved conversationUpdate` イベントがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-183">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a96c-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a96c-184">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a96c-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a96c-185">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="7a96c-186">JSON</span><span class="sxs-lookup"><span data-stu-id="7a96c-186">JSON</span></span>](#tab/json)

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


# <a name="python"></a>[<span data-ttu-id="7a96c-187">Python</span><span class="sxs-lookup"><span data-stu-id="7a96c-187">Python</span></span>](#tab/python)

```python
async def on_teams_members_removed(
    self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_removed:
        await turn_context.send_activity(
            MessageFactory.text(f"Say goodbye to your team member {member.id}")
        )
    return
```

* * *

### <a name="team-renamed"></a><span data-ttu-id="7a96c-188">チームの名前変更</span><span class="sxs-lookup"><span data-stu-id="7a96c-188">Team renamed</span></span>

<span data-ttu-id="7a96c-189">自分のチームの名前が変更されると、ボットに通知されます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-189">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="7a96c-190">`conversationUpdate` `eventType.teamRenamed` オブジェクト内でイベントを受け取り `channelData` ます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-190">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a96c-191">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a96c-191">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a96c-192">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a96c-192">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="7a96c-193">JSON</span><span class="sxs-lookup"><span data-stu-id="7a96c-193">JSON</span></span>](#tab/json)

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


# <a name="python"></a>[<span data-ttu-id="7a96c-194">Python</span><span class="sxs-lookup"><span data-stu-id="7a96c-194">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="7a96c-195">メッセージ反反応イベント</span><span class="sxs-lookup"><span data-stu-id="7a96c-195">Message reaction events</span></span>

<span data-ttu-id="7a96c-196">`messageReaction`ユーザーが bot によって送信されたメッセージに対して反力を追加または削除すると、イベントが送信されます。</span><span class="sxs-lookup"><span data-stu-id="7a96c-196">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="7a96c-197">には `replyToId` 特定のメッセージの ID が含まれており、は `Type` テキスト形式での応答の種類です。</span><span class="sxs-lookup"><span data-stu-id="7a96c-197">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="7a96c-198">反応の種類には、"怒っている"、"ハート"、"laugh"、"like"、"悲しい"、"驚いた" などがあります。</span><span class="sxs-lookup"><span data-stu-id="7a96c-198">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="7a96c-199">このイベントには元のメッセージの内容が含まれていないため、メッセージに対する反応の処理が bot にとって重要である場合は、メッセージを送信するときに格納する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7a96c-199">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="7a96c-200">EventType</span><span class="sxs-lookup"><span data-stu-id="7a96c-200">EventType</span></span>       | <span data-ttu-id="7a96c-201">ペイロードオブジェクト</span><span class="sxs-lookup"><span data-stu-id="7a96c-201">Payload object</span></span>   | <span data-ttu-id="7a96c-202">説明</span><span class="sxs-lookup"><span data-stu-id="7a96c-202">Description</span></span>                                                             | <span data-ttu-id="7a96c-203">範囲</span><span class="sxs-lookup"><span data-stu-id="7a96c-203">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="7a96c-204">messageReaction</span><span class="sxs-lookup"><span data-stu-id="7a96c-204">messageReaction</span></span> | <span data-ttu-id="7a96c-205">再アクションの追加</span><span class="sxs-lookup"><span data-stu-id="7a96c-205">reactionsAdded</span></span>   | [<span data-ttu-id="7a96c-206">Bot メッセージへの反応</span><span class="sxs-lookup"><span data-stu-id="7a96c-206">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="7a96c-207">すべて</span><span class="sxs-lookup"><span data-stu-id="7a96c-207">All</span></span>   |
| <span data-ttu-id="7a96c-208">messageReaction</span><span class="sxs-lookup"><span data-stu-id="7a96c-208">messageReaction</span></span> | <span data-ttu-id="7a96c-209">再アクションの削除</span><span class="sxs-lookup"><span data-stu-id="7a96c-209">reactionsRemoved</span></span> | [<span data-ttu-id="7a96c-210">Bot メッセージからの反力の削除</span><span class="sxs-lookup"><span data-stu-id="7a96c-210">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="7a96c-211">すべて</span><span class="sxs-lookup"><span data-stu-id="7a96c-211">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="7a96c-212">Bot メッセージに対する反応</span><span class="sxs-lookup"><span data-stu-id="7a96c-212">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a96c-213">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a96c-213">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a96c-214">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a96c-214">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="7a96c-215">JSON</span><span class="sxs-lookup"><span data-stu-id="7a96c-215">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="7a96c-216">Python</span><span class="sxs-lookup"><span data-stu-id="7a96c-216">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="7a96c-217">Bot メッセージから削除された反応</span><span class="sxs-lookup"><span data-stu-id="7a96c-217">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a96c-218">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a96c-218">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a96c-219">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a96c-219">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="7a96c-220">JSON</span><span class="sxs-lookup"><span data-stu-id="7a96c-220">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="7a96c-221">Python</span><span class="sxs-lookup"><span data-stu-id="7a96c-221">Python</span></span>](#tab/python)

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
