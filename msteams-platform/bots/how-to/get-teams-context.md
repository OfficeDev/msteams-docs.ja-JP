---
title: ボットTeams特定のコンテキストを取得する
author: surbhigupta
description: 会話名簿、単一メンバー、またはチームの詳細、チャネル リスト、コード サンプルなど、ボットの Microsoft Team の特定のコンテキストを取得する方法。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
keywords: ボット コンテキスト名簿ユーザー プロファイル チャネル リスト
ms.openlocfilehash: 69f4f81720fc24acfbfb6ae5b0769e37511bd7b7
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518570"
---
# <a name="get-teams-specific-context-for-your-bot"></a>ボットTeams特定のコンテキストを取得する

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

ボットは、インストールされているチームまたはチャットに関する追加のコンテキスト データにアクセスできます。 この情報は、ボットの機能を強化し、よりカスタマイズされたエクスペリエンスを提供するために使用できます。

## <a name="fetch-the-roster-or-user-profile"></a>名簿またはユーザー プロファイルを取得する

ボットは、Teams ユーザー ID や Microsoft Azure Active Directory (Azure AD) 情報 (名前や objectId など) を含む、メンバーのリストとその基本的なユーザー プロファイルを照会できます。 この情報を使用して、ユーザー ID を関連付けできます。 たとえば、ユーザーが (Microsoft Azure Active Directory) Azure AD資格情報を使用してタブにログインしたかどうかを確認するには、チームのメンバーです。 会話メンバーを取得する場合、最小または最大のページ サイズは実装によって異なります。 50 未満のページ サイズは 50 として扱い、500 より大きい場合は 500 に制限されます。 ページ以外のバージョンを使用する場合でも、大規模なチームではこのバージョンは使用できません。 詳細については、「チームまたはチャット [メンバーをフェッチTeamsボット API に対する変更」を参照してください](~/resources/team-chat-member-api-changes.md)。

次のサンプル コードでは、ページ化されたエンドポイントを使用して、名簿をフェッチします。

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[JSON](#tab/json)

エンドポイントとして値を使用して、 `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`GET 要求を直接 `serviceUrl` 発行できます。 値は安定 `serviceUrl` していますが、変更できます。 新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl`。 応答ペイロードは、ユーザーが正規ユーザーか匿名ユーザーかも示します。

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

名簿またはユーザー プロファイルを取得した後、1 つのメンバーの詳細を取得できます。 現在、チャットまたはチームの 1 `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` 人または複数のメンバーの情報を取得するには、Microsoft Teamsまたは TypeScript API の C#ボット API を使用します。

## <a name="get-single-member-details"></a>単一のメンバーの詳細を取得する

特定のユーザーの詳細は、ユーザー ID、UP Microsoft Azure Active Directory N、または Teams (Azure AD) オブジェクト ID を使用して取得できます。

次のサンプル コードは、単一のメンバーの詳細を取得するために使用されます。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = await TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[JSON](#tab/json)

エンドポイントとして値を使用して、 `/v3/conversations/{conversationId}/members/{userId}`GET 要求を直接 `serviceUrl` 発行できます。 値は安定 `serviceUrl` していますが、変更できます。 新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl`。 これは、通常のユーザーと匿名ユーザーに使用できます。

通常のユーザーの応答サンプルを次に示します。

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

匿名ユーザーの応答サンプルを次に示します。

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

1 人のメンバーの詳細を取得した後、チームの詳細を取得できます。 現時点では、チームの情報を取得するには、Microsoft Teamsまたは `TeamsInfo.GetMemberDetailsAsync` TypeScript のC#ボット `TeamsInfo.getTeamDetails` API を使用します。

## <a name="get-teams-details"></a>チームの詳細を取得する

チームにインストールすると、ボットは、そのチームに関するメタデータ (グループ ID を含むMicrosoft Azure Active DirectoryクエリAzure ADできます。

チームの詳細を取得するには、次のサンプル コードを使用します。

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

エンドポイントとして値を使用して、 `/v3/teams/{teamId}`GET 要求を直接 `serviceUrl` 発行できます。 値は安定 `serviceUrl` していますが、変更できます。 新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl`。

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

チームの詳細を取得した後、チーム内のチャネルの一覧を取得できます。 現時点では、チーム内の`TeamsInfo.GetTeamChannelsAsync``TeamsInfo.getTeamChannels`チャネルの一覧の情報を取得するには、Microsoft Teamsまたは TypeScript API 用C#ボット API を使用します。

## <a name="get-the-list-of-channels-in-a-team"></a>チーム内のチャネルの一覧を取得する

ボットは、チーム内のチャネルの一覧を照会できます。

> [!NOTE]
> * ローカライズを許可するために、既定の一般チャネル `null` の名前が返されます。
> * General チャネルのチャネル ID は、常にチーム ID と一致します。

チーム内のチャネルの一覧を取得するには、次のサンプル コードを使用します。

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

エンドポイントとして値を使用して、 `/v3/teams/{teamId}/conversations`GET 要求を直接 `serviceUrl` 発行できます。 値は安定 `serviceUrl` していますが、変更できます。 新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl`。

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

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ボットを介してファイルを送受信する](~/bots/how-to/bots-filesv4.md)
