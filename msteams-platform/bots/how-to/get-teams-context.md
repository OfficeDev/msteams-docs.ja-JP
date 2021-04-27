---
title: ボットの Teams 固有のコンテキストを取得する
author: laujan
description: 会話の名簿、詳細、チャネル リストなど、ボットの Microsoft Team の特定のコンテキストを取得する方法。
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 2e0178c5fd1ebca85d6e6c2cb6f3591f36a648fb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020015"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="7b020-103">ボットの Teams 固有のコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="7b020-103">Get Teams specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="7b020-104">ボットは、インストールされているチームまたはチャットに関する追加のコンテキスト データにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="7b020-104">A bot can access additional context data about a team or chat where it is installed.</span></span> <span data-ttu-id="7b020-105">この情報は、ボットの機能を強化し、よりカスタマイズされたエクスペリエンスを提供するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetch-the-roster-or-user-profile"></a><span data-ttu-id="7b020-106">名簿またはユーザー プロファイルを取得する</span><span class="sxs-lookup"><span data-stu-id="7b020-106">Fetch the roster or user profile</span></span>

<span data-ttu-id="7b020-107">ボットは、Teams ユーザー ID や Azure Active Directory (AAD) 情報 (名前や objectId など) を含む、メンバーのリストとその基本的なユーザー プロファイルを照会できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-107">Your bot can query for the list of members and their basic user profiles, including Teams user IDs and Azure Active Directory (AAD) information, such as name and objectId.</span></span> <span data-ttu-id="7b020-108">この情報を使用して、ユーザー ID を関連付けできます。</span><span class="sxs-lookup"><span data-stu-id="7b020-108">You can use this information to correlate user identities.</span></span> <span data-ttu-id="7b020-109">たとえば、ユーザーが AAD 資格情報を使用してタブにログインしたかどうかを確認するには、チームのメンバーです。</span><span class="sxs-lookup"><span data-stu-id="7b020-109">For example, to check whether a user logged into a tab through AAD credentials, is a member of the team.</span></span> <span data-ttu-id="7b020-110">会話メンバーを取得する場合、最小または最大のページ サイズは実装によって異なります。</span><span class="sxs-lookup"><span data-stu-id="7b020-110">For get conversation members, minimum or maximum page size depends on the implementation.</span></span> <span data-ttu-id="7b020-111">50 未満のページ サイズは 50 として扱い、500 より大きい場合は 500 に制限されます。</span><span class="sxs-lookup"><span data-stu-id="7b020-111">Page size less than 50, are treated as 50, and greater than 500, are capped at 500.</span></span> <span data-ttu-id="7b020-112">ページ以外のバージョンを使用する場合でも、大規模なチームではこのバージョンは使用できません。</span><span class="sxs-lookup"><span data-stu-id="7b020-112">Even if you use the non-paged version, it is unreliable in large teams and must not be used.</span></span> <span data-ttu-id="7b020-113">詳細については、「チームまたはチャット メンバーをフェッチする Teams Bot API への変更 [」を参照してください](~/resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="7b020-113">For more information, see [changes to Teams Bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="7b020-114">次のサンプル コードでは、ページ化されたエンドポイントを使用して、名簿をフェッチします。</span><span class="sxs-lookup"><span data-stu-id="7b020-114">The following sample code uses the paged endpoint for fetching the roster:</span></span>

# <a name="c"></a>[<span data-ttu-id="7b020-115">C#</span><span class="sxs-lookup"><span data-stu-id="7b020-115">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="7b020-116">TypeScript</span><span class="sxs-lookup"><span data-stu-id="7b020-116">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="7b020-117">Python</span><span class="sxs-lookup"><span data-stu-id="7b020-117">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="7b020-118">JSON</span><span class="sxs-lookup"><span data-stu-id="7b020-118">JSON</span></span>](#tab/json)

<span data-ttu-id="7b020-119">エンドポイントとして値を使用して、GET 要求を `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` 直接 `serviceUrl` 発行できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-119">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="7b020-120">値は安定 `serviceUrl` していますが、変更できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-120">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="7b020-121">新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="7b020-121">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="7b020-122">応答ペイロードは、ユーザーが正規ユーザーか匿名ユーザーかも示します。</span><span class="sxs-lookup"><span data-stu-id="7b020-122">The response payload also indicates if the user is a regular or anonymous user.</span></span>

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

<span data-ttu-id="7b020-123">名簿またはユーザー プロファイルを取得した後、1 つのメンバーの詳細を取得できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-123">After you fetch the roster or user profile, you can get details of a single member.</span></span> <span data-ttu-id="7b020-124">現在、チャットまたはチームの 1 人または複数のメンバーの情報を取得するには、Microsoft Teams ボット API を使用して、C#または TypeScript API 用に `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` 使用します。</span><span class="sxs-lookup"><span data-stu-id="7b020-124">Currently, to retrieve information for one or more members of a chat or team, use the Microsoft Teams bot APIs `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript APIs.</span></span>

## <a name="get-single-member-details"></a><span data-ttu-id="7b020-125">単一のメンバーの詳細を取得する</span><span class="sxs-lookup"><span data-stu-id="7b020-125">Get single member details</span></span>

<span data-ttu-id="7b020-126">Teams ユーザー ID、UPN、または AAD オブジェクト ID を使用して、特定のユーザーの詳細を取得できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-126">You can also retrieve the details of a particular user using their Teams user ID, UPN, or AAD Object ID.</span></span>

<span data-ttu-id="7b020-127">次のサンプル コードは、単一のメンバーの詳細を取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="7b020-127">The following sample code is used to get single member details:</span></span>

# <a name="c"></a>[<span data-ttu-id="7b020-128">C#</span><span class="sxs-lookup"><span data-stu-id="7b020-128">C#</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="7b020-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="7b020-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="7b020-130">Python</span><span class="sxs-lookup"><span data-stu-id="7b020-130">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="7b020-131">JSON</span><span class="sxs-lookup"><span data-stu-id="7b020-131">JSON</span></span>](#tab/json)

<span data-ttu-id="7b020-132">エンドポイントとして値を使用して、GET 要求を `/v3/conversations/{conversationId}/members/{userId}` 直接 `serviceUrl` 発行できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-132">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="7b020-133">値は安定 `serviceUrl` していますが、変更できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-133">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="7b020-134">新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="7b020-134">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="7b020-135">これは、通常のユーザーと匿名ユーザーに使用できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-135">This can be used for regular users and anonymous users.</span></span>

<span data-ttu-id="7b020-136">通常のユーザーの応答サンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="7b020-136">The following is the response sample for regular user:</span></span>

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

<span data-ttu-id="7b020-137">匿名ユーザーの応答サンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="7b020-137">The following is the response sample for anonymous user:</span></span>

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

<span data-ttu-id="7b020-138">1 人のメンバーの詳細を取得した後、チームの詳細を取得できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-138">After you get details of a single member, you can get details of the team.</span></span> <span data-ttu-id="7b020-139">現時点では、チームの情報を取得するには、Microsoft Teams ボット API を使用して、C#または `TeamsInfo.GetMemberDetailsAsync` `TeamsInfo.getTeamDetails` TypeScript 用に使用します。</span><span class="sxs-lookup"><span data-stu-id="7b020-139">Currently, to retrieve information for a team, use the Microsoft Teams bot APIs `TeamsInfo.GetMemberDetailsAsync` for C# or `TeamsInfo.getTeamDetails` for TypeScript.</span></span>

## <a name="get-teams-details"></a><span data-ttu-id="7b020-140">チームの詳細を取得する</span><span class="sxs-lookup"><span data-stu-id="7b020-140">Get team's details</span></span>

<span data-ttu-id="7b020-141">チームにインストールすると、ボットは AAD グループ ID を含むそのチームに関するメタデータを照会できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-141">When installed in a team, your bot can query for metadata about that team including the AAD group ID.</span></span>

<span data-ttu-id="7b020-142">チームの詳細を取得するには、次のサンプル コードを使用します。</span><span class="sxs-lookup"><span data-stu-id="7b020-142">The following sample code is used to get team's details:</span></span>

# <a name="c"></a>[<span data-ttu-id="7b020-143">C#</span><span class="sxs-lookup"><span data-stu-id="7b020-143">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="7b020-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="7b020-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="7b020-145">Python</span><span class="sxs-lookup"><span data-stu-id="7b020-145">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="7b020-146">JSON</span><span class="sxs-lookup"><span data-stu-id="7b020-146">JSON</span></span>](#tab/json)

<span data-ttu-id="7b020-147">エンドポイントとして値を使用して、GET 要求を `/v3/teams/{teamId}` 直接 `serviceUrl` 発行できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-147">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="7b020-148">値は安定 `serviceUrl` していますが、変更できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-148">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="7b020-149">新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="7b020-149">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

<span data-ttu-id="7b020-150">チームの詳細を取得した後、チーム内のチャネルの一覧を取得できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-150">After you get details of the team, you can get the list of channels in a team.</span></span> <span data-ttu-id="7b020-151">現時点では、チーム内のチャネルの一覧の情報を取得するには、Microsoft Teams ボット API を使用して、C#または `TeamsInfo.GetTeamChannelsAsync` `TeamsInfo.getTeamChannels` TypeScript API に使用します。</span><span class="sxs-lookup"><span data-stu-id="7b020-151">Currently, to retrieve information for a list of channels in a team, use the Microsoft Teams bot APIs `TeamsInfo.GetTeamChannelsAsync` for C# or `TeamsInfo.getTeamChannels` for TypeScript APIs.</span></span>

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="7b020-152">チーム内のチャネルの一覧を取得する</span><span class="sxs-lookup"><span data-stu-id="7b020-152">Get the list of channels in a team</span></span>

<span data-ttu-id="7b020-153">ボットは、チーム内のチャネルの一覧を照会できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-153">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
> * <span data-ttu-id="7b020-154">ローカライズを許可するために、既定の一般チャネル `null` の名前が返されます。</span><span class="sxs-lookup"><span data-stu-id="7b020-154">The name of the default General channel is returned as `null` to allow for localization.</span></span>
> * <span data-ttu-id="7b020-155">General チャネルのチャネル ID は、常にチーム ID と一致します。</span><span class="sxs-lookup"><span data-stu-id="7b020-155">The channel ID for the General channel always matches the team ID.</span></span>

<span data-ttu-id="7b020-156">チーム内のチャネルの一覧を取得するには、次のサンプル コードを使用します。</span><span class="sxs-lookup"><span data-stu-id="7b020-156">The following sample code is used to get the list of channels in a team:</span></span>

# <a name="c"></a>[<span data-ttu-id="7b020-157">C#</span><span class="sxs-lookup"><span data-stu-id="7b020-157">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="7b020-158">TypeScript</span><span class="sxs-lookup"><span data-stu-id="7b020-158">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="7b020-159">Python</span><span class="sxs-lookup"><span data-stu-id="7b020-159">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="7b020-160">JSON</span><span class="sxs-lookup"><span data-stu-id="7b020-160">JSON</span></span>](#tab/json)

<span data-ttu-id="7b020-161">エンドポイントとして値を使用して、GET 要求を `/v3/teams/{teamId}/conversations` 直接 `serviceUrl` 発行できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-161">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="7b020-162">値は安定 `serviceUrl` していますが、変更できます。</span><span class="sxs-lookup"><span data-stu-id="7b020-162">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="7b020-163">新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="7b020-163">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

## <a name="next-step"></a><span data-ttu-id="7b020-164">次の手順</span><span class="sxs-lookup"><span data-stu-id="7b020-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7b020-165">ボットを介してファイルを送受信する</span><span class="sxs-lookup"><span data-stu-id="7b020-165">Send and receive files through the bot</span></span>](~/bots/how-to/bots-filesv4.md)
