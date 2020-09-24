---
title: Bot のチーム固有のコンテキストを取得する
author: clearab
description: 会話名簿、details、channel list を含む、bot の Microsoft チーム固有のコンテキストを取得する方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 55f93a914cdb0f92885ff535424cd823072184aa
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237799"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="9360f-103">Bot のチーム固有のコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="9360f-103">Get Team's specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="9360f-104">Bot は、にインストールされているチームまたはチャットに関する追加のコンテキストデータにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="9360f-104">A bot can access additional context data about a team or chat it is installed in.</span></span> <span data-ttu-id="9360f-105">この情報は、ボットの機能を強化し、よりパーソナライズされた環境を提供するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="9360f-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetching-the-roster-or-user-profile"></a><span data-ttu-id="9360f-106">名簿またはユーザープロファイルを取得する</span><span class="sxs-lookup"><span data-stu-id="9360f-106">Fetching the roster or user profile</span></span>

<span data-ttu-id="9360f-107">Bot は、メンバーの一覧とその基本プロファイルを照会できます。これには、Teams のユーザー Id や Azure Active Directory (Azure AD) (name、objectId など) の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="9360f-107">Your bot can query for the list of members and their basic profiles, including Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="9360f-108">この情報を使用して、ユーザー id (たとえば、Azure AD 資格情報を介してタブにログインしたユーザー) がチームのメンバーであるかどうかを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="9360f-108">You can use this information to correlate user identities, e.g., to check whether a user, logged into a tab through Azure AD credentials, is a member of the team.</span></span> <span data-ttu-id="9360f-109">次のサンプルコードでは、名簿を取得するためにページエンドポイントを使用しています。</span><span class="sxs-lookup"><span data-stu-id="9360f-109">The sample code below uses the paged endpoint for retrieving the roster.</span></span> <span data-ttu-id="9360f-110">非ページバージョンを引き続き使用する場合もありますが、大規模なチームでは信頼性が低く、使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="9360f-110">Although you may still use the non-paged version, it will be unreliable in large teams and should not be used.</span></span> <span data-ttu-id="9360f-111">詳細については、 [この記事](~/resources/team-chat-member-api-changes.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9360f-111">See [this article](~/resources/team-chat-member-api-changes.md) for additional information.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9360f-112">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9360f-112">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var members = new List<TeamsChannelAccount>();
        string continuationToken = null;

        do
        {
            var currentPage = await TeamsInfo.GetPagedMembersAsync(turnContext, 100, continuationToken, cancellationToken);
            continuationToken = currentPage.ContinuationToken;
            members.AddRange(currentPage.Members);
         }
         while (continuationToken != null);
     }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="9360f-113">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9360f-113">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            var continuationToken;
            var members = [];

            do {
                var pagedMembers = await TeamsInfo.getPagedMembers(context, 100, continuationToken);
                continuationToken = pagedMembers.continuationToken;
                members.push(...pagedMembers.members);
            }
            while(continuationToken !== undefined)

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="9360f-114">Python</span><span class="sxs-lookup"><span data-stu-id="9360f-114">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="9360f-115">JSON</span><span class="sxs-lookup"><span data-stu-id="9360f-115">JSON</span></span>](#tab/json)

<span data-ttu-id="9360f-116">`/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="9360f-116">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="9360f-117">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="9360f-117">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="9360f-118">新しいメッセージが到着すると、bot はに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="9360f-118">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/pagedmembers?pageSize=100&continuationToken=asdfasdfalkdsjfalksjdf

Response body
{
    "continuationToken": "asdfqwerueiqpiewr",
    "members":
        [{
            "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
            "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
            "givenName": "Larry",
            "surname": "Brown",
            "email": "Larry.Brown@fabrikam.com",
            "userPrincipalName": "labrown@fabrikam.com"
        }, {
            "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
            "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
            "givenName": "John",
            "surname": "Patterson",
            "email": "johnp@fabrikam.com",
            "userPrincipalName": "johnp@fabrikam.com"
        }, {
            "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
            "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
            "givenName": "Rick",
            "surname": "Stevens",
            "email": "Rick.Stevens@fabrikam.com",
            "userPrincipalName": "rstevens@fabrikam.com"
        }]
}
```

* * *

## <a name="get-single-member-details"></a><span data-ttu-id="9360f-119">単一メンバーの詳細を取得する</span><span class="sxs-lookup"><span data-stu-id="9360f-119">Get single member details</span></span>

<span data-ttu-id="9360f-120">Teams のユーザー Id、UPN、または AAD オブジェクト Id を使用して、特定のユーザーの詳細を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="9360f-120">You can also retrieve the details of a particular user using their Teams user Id, UPN, or AAD Object Id.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9360f-121">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9360f-121">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="9360f-122">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9360f-122">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        const member = await TeamsInfo.getMember(context, encodeURI('someone@somecompany.com'));

        // By calling next() you ensure that the next BotHandler is run.
        await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="9360f-123">Python</span><span class="sxs-lookup"><span data-stu-id="9360f-123">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="9360f-124">JSON</span><span class="sxs-lookup"><span data-stu-id="9360f-124">JSON</span></span>](#tab/json)

<span data-ttu-id="9360f-125">`/v3/conversations/{conversationId}/members/{userId}`エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="9360f-125">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="9360f-126">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="9360f-126">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="9360f-127">新しいメッセージが到着すると、bot はに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="9360f-127">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/labrown@fabrikam.com"

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}
```

* * *

## <a name="get-teams-details"></a><span data-ttu-id="9360f-128">チームの詳細を取得する</span><span class="sxs-lookup"><span data-stu-id="9360f-128">Get team's details</span></span>

<span data-ttu-id="9360f-129">Bot がチームにインストールされている場合は、そのチームに関するメタデータのクエリを実行できます (Azure AD groupId を含む)。</span><span class="sxs-lookup"><span data-stu-id="9360f-129">When installed in a team, your bot can query for metadata about that team including the Azure AD groupId.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9360f-130">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9360f-130">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        TeamDetails teamDetails = await TeamsInfo.GetTeamDetailsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);
        if (teamDetails != null) {
            await turnContext.SendActivityAsync($"The groupId is: {teamDetails.AadGroupId}");
        }
        else {
            await turnContext.SendActivityAsync($"Message did not come from a channel in a team.");
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="9360f-131">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9360f-131">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const teamDetails = await TeamsInfo.getTeamDetails(turnContext);
            if (teamDetails) {
                await turnContext.sendActivity(`The group ID is: ${teamDetails.aadGroupId}`);
            } else {
                await turnContext.sendActivity('This message did not come from a channel in a team.');
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="9360f-132">Python</span><span class="sxs-lookup"><span data-stu-id="9360f-132">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="9360f-133">JSON</span><span class="sxs-lookup"><span data-stu-id="9360f-133">JSON</span></span>](#tab/json)

<span data-ttu-id="9360f-134">`/v3/teams/{teamId}`エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="9360f-134">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="9360f-135">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="9360f-135">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="9360f-136">新しいメッセージが到着すると、bot はに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="9360f-136">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/teams/19:ja0cu120i1jod12j@skype.net

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "The Team Name",
    "aadGroupId": "02ce3874-dd86-41ba-bddc-013f34019978"
}
```

* * *

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="9360f-137">チーム内のチャネルの一覧を取得する</span><span class="sxs-lookup"><span data-stu-id="9360f-137">Get the list of channels in a team</span></span>

<span data-ttu-id="9360f-138">Bot は、チーム内のチャネルの一覧を照会できます。</span><span class="sxs-lookup"><span data-stu-id="9360f-138">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="9360f-139">既定の一般的なチャネルの名前は、 `null` ローカリゼーションを許可するためにとして返されます。</span><span class="sxs-lookup"><span data-stu-id="9360f-139">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="9360f-140">一般チャネルのチャネル ID は、常にチーム ID と一致します。</span><span class="sxs-lookup"><span data-stu-id="9360f-140">The channel ID for the General channel always matches the team ID.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9360f-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9360f-141">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        IEnumerable<ChannelInfo> channels = await TeamsInfo.GetTeamChannelsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);

        await turnContext.SendActivityAsync($"The channel count is: {channels.Count()}");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="9360f-142">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9360f-142">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const channels = await TeamsInfo.getTeamChannels(turnContext);

            await turnContext.sendActivity(`The channel count is: ${channels.length}`);

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="9360f-143">Python</span><span class="sxs-lookup"><span data-stu-id="9360f-143">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="9360f-144">JSON</span><span class="sxs-lookup"><span data-stu-id="9360f-144">JSON</span></span>](#tab/json)

<span data-ttu-id="9360f-145">`/v3/teams/{teamId}/conversations`エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="9360f-145">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="9360f-146">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="9360f-146">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="9360f-147">新しいメッセージが到着すると、bot はに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="9360f-147">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/teams/19%3A033451497ea84fcc83d17ed7fb08a1b6%40thread.skype/conversations

Response body
{
    "conversations": [{
        "id": "19:033451497ea84fcc83d17ed7fb08a1b6@thread.skype",
        "name": null
    }, {
        "id": "19:cc25e4aae50746ecbb11473bba24c70a@thread.skype",
        "name": "Materials"
    }, {
        "id": "19:b7b84cba410c406ba671dbbf5e0a3519@thread.skype",
        "name": "Design"
    }, {
        "id": "19:fc5db2aed489454e8f8c06829ed6c986@thread.skype",
        "name": "Marketing"
    }]
}
```

* * *

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
