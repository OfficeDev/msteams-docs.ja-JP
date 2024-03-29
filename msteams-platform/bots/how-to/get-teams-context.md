---
title: Teams の特定のコンテキストをボット用に取得する
author: surbhigupta
description: ボットの Teams 固有のコンテキストを取得し、ユーザー プロファイルを取得し、チームの詳細で単一メンバー、チームのチャネルの一覧を取得します。 新しいチャネル スレッドの作成に関するサンプル。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: 1958d45bf4fac927c32b628ea8aebc4c1c03ad46
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789990"
---
# <a name="get-teams-specific-context-for-your-bot"></a>Teams の特定のコンテキストをボット用に取得する

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

ボットは、インストールされているチームまたはチャットに関する追加のコンテキスト データにアクセスできます。 この情報は、ボットの機能を強化し、よりパーソナライズされたエクスペリエンスを提供するために使用できます。

## <a name="fetch-the-roster-or-user-profile"></a>名簿またはユーザー プロファイルをフェッチする

ボットは、メンバーとその基本的なユーザー プロファイルの一覧 (Teams ユーザー ID、名前や objectId などの Microsoft Azure Active Directory (Azure AD) 情報を含む) を照会できます。 この情報を使用して、ユーザー ID を関連付けることができます。 たとえば、ユーザーが Azure AD 資格情報を使用してタブにログインしているかどうかを確認するには、チームのメンバーです。 会話メンバーを取得する場合、最小または最大ページ サイズは実装によって異なります。 ページ サイズが 50 未満の場合は 50 として扱われ、500 を超える場合は 500 に制限されます。 ページ化されていないバージョンを使用している場合でも、大規模なチームでは信頼性が低いため、使用しないでください。 詳細については、「[チームまたはチャット メンバーをフェッチするための Teams ボット API に対する変更](~/resources/team-chat-member-api-changes.md)」を参照してください。

次のサンプル コードは、ページ化されたエンドポイントを使用して名簿を取得します。

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
                var pagedMembers = await TeamsInfo.getPagedMembers(turnContext, 100, continuationToken);
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

`serviceUrl` の値をエンドポイントとして使用して、`/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` で GET 要求を直接発行できます。 `serviceUrl` の値は安定していますが、変化する可能性があります。 新しいメッセージが届いたら、ボットは格納されている `serviceUrl` の値を確認する必要があります。 応答ペイロードは、ユーザーが通常のユーザーであるか匿名のユーザーであるかも示します。

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

名簿またはユーザー プロファイルをフェッチすると、単一のメンバーの詳細を取得できます。 現在、チャットまたはチームの 1 人以上のメンバーの情報を取得するには、Microsoft Teams ボット API `TeamsInfo.GetMembersAsync` (C# の場合) または `TeamsInfo.getMembers` (TypeScript API の場合) を使用します。

## <a name="get-single-member-details"></a>単一のメンバーの詳細を取得する

Teams のユーザー ID、UPN、または Azure AD オブジェクト ID を使用して、特定のユーザーの詳細を取得することもできます。

次のサンプル コードは、単一メンバーの詳細を取得するために使用されます。

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
        this.onMessage(async (turnContext, next) => {
            const member = await TeamsInfo.getMember(turnContext, encodeURI('someone@somecompany.com'));

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

`serviceUrl` の値をエンドポイントとして使用して、`/v3/conversations/{conversationId}/members/{userId}` で GET 要求を直接発行できます。 `serviceUrl` の値は安定していますが、変化する可能性があります。 新しいメッセージが届いたら、ボットは格納されている `serviceUrl` の値を確認する必要があります。 これは、通常のユーザーと匿名ユーザーに使用できます。

以下は、通常のユーザーの応答サンプルです。

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

以下は、匿名ユーザーの応答サンプルです。

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

単一のメンバーの詳細を取得した後、チームの詳細を取得できます。 現在、チームの情報を取得するには、Teams ボット API `TeamsInfo.GetMemberDetailsAsync` (C# の場合) または `TeamsInfo.getTeamDetails` (TypeScript の場合) を使用します。

## <a name="get-teams-details"></a>チームの詳細を取得する

チームにインストールすると、ボットは Azure AD グループ ID を含むそのチームに関するメタデータをクエリできます。

次のサンプル コードは、チームの詳細を取得するために使用されます。

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

`serviceUrl` の値をエンドポイントとして使用して、`/v3/teams/{teamId}` で GET 要求を直接発行できます。 `serviceUrl` の値は安定していますが、変化する可能性があります。 新しいメッセージが届いたら、ボットは格納されている `serviceUrl` の値を確認する必要があります。

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

チームの詳細を取得したら、チーム内のチャネルのリストを取得できます。 現在、チーム内のチャネルのリストの情報を取得するには、Teams ボット API `TeamsInfo.GetTeamChannelsAsync` (C# の場合) または `TeamsInfo.getTeamChannels` (TypeScript API の場合) を使用します。

## <a name="get-the-list-of-channels-in-a-team"></a>チーム内のチャネルの一覧を取得します。

ボットは、チーム内のチャネルのリストをクエリできます。

> [!NOTE]
>
> * ローカリゼーションを可能にするために、既定の一般チャネルの名前が `null` として返されます。
> * 一般チャネルのチャネル ID は、常にチーム ID と一致します。

次のサンプル コードは、チーム内のチャネルのリストを取得するために使用されます。

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

`serviceUrl` の値をエンドポイントとして使用して、`/v3/teams/{teamId}/conversations` で GET 要求を直接発行できます。 `serviceUrl` の値は安定していますが、変化する可能性があります。 新しいメッセージが届いたら、ボットは格納されている `serviceUrl` の値を確認する必要があります。

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
> [ボットを介してファイルを送受信する方法](~/bots/how-to/bots-filesv4.md)

## <a name="see-also"></a>関連項目

* [アプリをローカライズする](../../concepts/build-and-test/apps-localization.md)
* [ユーザー、グループ、チーム、または Outlook 連絡先のプロフィール写真を取得する](/graph/api/profilephoto-get)
