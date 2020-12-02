---
title: Bot のチーム固有のコンテキストを取得する
author: laujan
description: 会話名簿、details、channel list を含む、bot の Microsoft チーム固有のコンテキストを取得する方法。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 7f3b2fbea33f64659dcd5d9d39bb95e2d953dbea
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552473"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="5bc51-103">Bot のチーム固有のコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="5bc51-103">Get Team's specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="5bc51-104">Bot は、にインストールされているチームまたはチャットに関する追加のコンテキストデータにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-104">A bot can access additional context data about a team or chat it is installed in.</span></span> <span data-ttu-id="5bc51-105">この情報は、ボットの機能を強化し、よりパーソナライズされた環境を提供するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetching-the-roster-or-user-profile"></a><span data-ttu-id="5bc51-106">名簿またはユーザープロファイルを取得する</span><span class="sxs-lookup"><span data-stu-id="5bc51-106">Fetching the roster or user profile</span></span>

<span data-ttu-id="5bc51-107">Bot は、メンバーの一覧とその基本プロファイルを照会できます。これには、Teams のユーザー Id や Azure Active Directory (Azure AD) (name、objectId など) の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-107">Your bot can query for the list of members and their basic profiles, including Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="5bc51-108">この情報を使用して、ユーザー id (たとえば、Azure AD 資格情報を介してタブにログインしたユーザー) がチームのメンバーであるかどうかを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-108">You can use this information to correlate user identities, e.g., to check whether a user, logged into a tab through Azure AD credentials, is a member of the team.</span></span> <span data-ttu-id="5bc51-109">次のサンプルコードでは、名簿を取得するためにページエンドポイントを使用しています。</span><span class="sxs-lookup"><span data-stu-id="5bc51-109">The sample code below uses the paged endpoint for retrieving the roster.</span></span> <span data-ttu-id="5bc51-110">会話メンバーを取得する場合、ページサイズの最小値または最大値は、実装によって異なります。</span><span class="sxs-lookup"><span data-stu-id="5bc51-110">For get conversation members, minimum or maximum page size depends on the implementation.</span></span> <span data-ttu-id="5bc51-111">ページサイズが50未満で、50として扱われ、ページサイズが500を超えると、500には上限があります。</span><span class="sxs-lookup"><span data-stu-id="5bc51-111">Page size less than 50, are treated as 50, and page size greater than 500, are capped at 500.</span></span> <span data-ttu-id="5bc51-112">非ページバージョンを引き続き使用する場合もありますが、大規模なチームでは信頼性が低く、使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="5bc51-112">Although you may still use the non-paged version, it will be unreliable in large teams and should not be used.</span></span> <span data-ttu-id="5bc51-113">追加情報については、「 [Teams Bot api に対するチーム/チャットメンバーを取得するための変更点」を](~/resources/team-chat-member-api-changes.md)*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="5bc51-113">*See* [Changes to Teams Bot APIs for Fetching Team/Chat Members](~/resources/team-chat-member-api-changes.md) for additional information.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5bc51-114">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5bc51-114">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="5bc51-115">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5bc51-115">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="5bc51-116">Python</span><span class="sxs-lookup"><span data-stu-id="5bc51-116">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="5bc51-117">JSON</span><span class="sxs-lookup"><span data-stu-id="5bc51-117">JSON</span></span>](#tab/json)

<span data-ttu-id="5bc51-118">`/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-118">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="5bc51-119">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-119">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="5bc51-120">新しいメッセージが到着すると、bot はに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-120">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="5bc51-121">応答ペイロードは、ユーザーが通常のユーザーであるか匿名であるかも示します。</span><span class="sxs-lookup"><span data-stu-id="5bc51-121">The response payload will also indicate if the user is a regular or anonymous user.</span></span>

```http
GET /v3/conversations/19:meeting_N2QzYTA3YmItYmMwOC00OTJmLThkYzMtZWMzZGU0NGIyZGI0@thread.v2/pagedmembers?pageSize=100&continuationToken=asdfasdfalkdsjfalksjdf

Response body
{
   "continuationToken":"asdfqwerueiqpiewr",
   "members":[
      {
         "id":"29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
         "name":"Anon1 (Guest)",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"anonymous"
      },
      {
         "id":"29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
         "objectId":"76b0b09f-d410-48fd-993e-84da521a597b",
         "givenName":"John",
         "surname":"Patterson",
         "email":"johnp@fabrikam.com",
         "userPrincipalName":"johnp@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      },
      {
         "id":"29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
         "objectId":"6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
         "givenName":"Rick",
         "surname":"Stevens",
         "email":"Rick.Stevens@fabrikam.com",
         "userPrincipalName":"rstevens@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      }
   ]
}
```

* * *

## <a name="get-single-member-details"></a><span data-ttu-id="5bc51-122">単一メンバーの詳細を取得する</span><span class="sxs-lookup"><span data-stu-id="5bc51-122">Get single member details</span></span>

<span data-ttu-id="5bc51-123">Teams のユーザー Id、UPN、または AAD オブジェクト Id を使用して、特定のユーザーの詳細を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-123">You can also retrieve the details of a particular user using their Teams user Id, UPN, or AAD Object Id.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5bc51-124">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5bc51-124">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="5bc51-125">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5bc51-125">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="5bc51-126">Python</span><span class="sxs-lookup"><span data-stu-id="5bc51-126">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="5bc51-127">JSON</span><span class="sxs-lookup"><span data-stu-id="5bc51-127">JSON</span></span>](#tab/json)

<span data-ttu-id="5bc51-128">`/v3/conversations/{conversationId}/members/{userId}`エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-128">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="5bc51-129">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-129">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="5bc51-130">新しいメッセージが到着すると、bot はに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-130">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="5bc51-131">これは、regualr ユーザーおよび匿名ユーザーに使用できます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-131">This can be used for regualr users and anonymous users.</span></span>

<span data-ttu-id="5bc51-132">通常のユーザーに対する応答のサンプルを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="5bc51-132">Below is a response sample for regular user</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"user"
}
```

<span data-ttu-id="5bc51-133">匿名ユーザーに対する応答の例</span><span class="sxs-lookup"><span data-stu-id="5bc51-133">Below is response for anonymous user</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/<anonymous user id>"

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"anonymous"
}
```

* * *

## <a name="get-teams-details"></a><span data-ttu-id="5bc51-134">チームの詳細を取得する</span><span class="sxs-lookup"><span data-stu-id="5bc51-134">Get team's details</span></span>

<span data-ttu-id="5bc51-135">Bot がチームにインストールされている場合は、そのチームに関するメタデータのクエリを実行できます (Azure AD groupId を含む)。</span><span class="sxs-lookup"><span data-stu-id="5bc51-135">When installed in a team, your bot can query for metadata about that team including the Azure AD groupId.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5bc51-136">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5bc51-136">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="5bc51-137">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5bc51-137">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="5bc51-138">Python</span><span class="sxs-lookup"><span data-stu-id="5bc51-138">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="5bc51-139">JSON</span><span class="sxs-lookup"><span data-stu-id="5bc51-139">JSON</span></span>](#tab/json)

<span data-ttu-id="5bc51-140">`/v3/teams/{teamId}`エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-140">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="5bc51-141">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-141">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="5bc51-142">新しいメッセージが到着すると、bot はに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-142">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

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

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="5bc51-143">チーム内のチャネルの一覧を取得する</span><span class="sxs-lookup"><span data-stu-id="5bc51-143">Get the list of channels in a team</span></span>

<span data-ttu-id="5bc51-144">Bot は、チーム内のチャネルの一覧を照会できます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-144">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="5bc51-145">既定の一般的なチャネルの名前は、 `null` ローカリゼーションを許可するためにとして返されます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-145">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="5bc51-146">一般チャネルのチャネル ID は、常にチーム ID と一致します。</span><span class="sxs-lookup"><span data-stu-id="5bc51-146">The channel ID for the General channel always matches the team ID.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5bc51-147">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5bc51-147">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="5bc51-148">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5bc51-148">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="5bc51-149">Python</span><span class="sxs-lookup"><span data-stu-id="5bc51-149">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="5bc51-150">JSON</span><span class="sxs-lookup"><span data-stu-id="5bc51-150">JSON</span></span>](#tab/json)

<span data-ttu-id="5bc51-151">`/v3/teams/{teamId}/conversations`エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-151">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="5bc51-152">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-152">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="5bc51-153">新しいメッセージが到着すると、bot はに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="5bc51-153">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

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
