---
title: ボットのコンテキストをMicrosoft Teamsする
description: ボットのコンテキストを取得する方法について説明Microsoft Teams
keywords: teams ボットのコンテキスト
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: 154a276c65987955cfe20e5b7ce4ed2e8973cbfd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020661"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>ボットのコンテキストをMicrosoft Teamsする

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットは、チームまたはチャットに関する追加のコンテキスト (ユーザー プロファイルなど) にアクセスできます。 この情報は、ボットの機能を強化し、よりパーソナライズされたエクスペリエンスを提供するために使用できます。

> [!NOTE]
>
> * Microsoft Teams固有のボット API は、ボット ビルダー SDK の拡張機能を通じて最適にアクセスできます。
> * Microsoft.bot.Connector.C#または .NET については[、Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)してください。
> * 開発Node.js、ボット フレームワーク SDK v4.6 Teams機能の[ボット ビルダーが](https://github.com/microsoft/botframework-sdk)組み込まれています。

## <a name="fetch-the-team-roster"></a>チーム名簿を取得する

ボットは、チーム メンバーとその基本的なプロファイルの一覧を照会できます。 基本的なプロファイルには、Teams ID、Azure Active Directory ID などの AAD (AAD) 情報が含まれます。 この情報を使用して、ユーザー ID を関連付けできます。 たとえば、AAD 資格情報を使用してタブにログインしたユーザーがチーム メンバーである場合に確認します。

### <a name="rest-api-example"></a>REST API の例

値をエンドポイントとして使用して、GET 要求 [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) `serviceUrl` を直接発行します。

ボットが受け取るアクティビティ ペイロードのオブジェクトは、次の `teamId` `channeldata` シナリオで確認できます。

* ユーザーがチーム コンテキストでボットにメッセージを送信または操作する場合。 詳細については、「メッセージの受信 [」を参照してください](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)。
* 新しいユーザーまたはボットがチームに追加された場合。 詳細については、「チームに [追加されたボットまたはユーザー」を参照してください](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)。

> [!NOTE]
>
>* API を呼び出す場合は、必ずチーム ID を使用してください。
>* 値 `serviceUrl` は安定している傾向がありますが、変更される可能性があります。 新しいメッセージが届いた場合、ボットは保存されている値を確認する必要 `serviceUrl` があります。

```json
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members

Response body
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
```

### <a name="net-example"></a>.NET の例

ユーザー `GetConversationMembersAsync` ID `Team.Id` の一覧を取得するために using を呼び出します。

```csharp
// Fetch the members in the current conversation
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));
var teamId = context.Activity.GetChannelData<TeamsChannelData>().Team.Id;
var members = await connector.Conversations.GetConversationMembersAsync(teamId);

// Concatenate information about all members into a string
var sb = new StringBuilder();
foreach (var member in members.AsTeamsChannelAccounts())
{
    sb.AppendFormat(
        "GivenName = {0}, TeamsMemberId = {1}",
        member.Name, member.Id);

    sb.AppendLine();
}

// Post the member info back into the conversation
await context.PostAsync($"People in this conversation: {sb.ToString()}");
```

### <a name="nodejs-or-typescript-example"></a>Node.jsまたは TypeScript の例

```typescript

[...]
import * as builder from "botbuilder";
[...]

var teamId = session.message.sourceEvent.team.id;
connector.fetchMembers(
  (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is some error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

また [、「Bot Framework のサンプル」を参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>個人チャットまたはグループ チャットでユーザー プロファイルまたは名簿を取得する

任意の個人チャットの API 呼び出しを行って、ボットとチャットしているユーザーのプロファイル情報を取得できます。

API 呼び出し、SDK メソッド、および応答オブジェクトは、チーム名簿のフェッチと同じです。 唯一の違いは `conversationId` 、. `teamId`

## <a name="fetch-the-list-of-channels-in-a-team"></a>チーム内のチャネルの一覧を取得する

ボットは、チーム内のチャネルの一覧を照会できます。

> [!NOTE]
>
>* ローカライズを許可するために、既定の一般チャネル `null` の名前が返されます。
>* General チャネルのチャネル ID は、常にチーム ID と一致します。

### <a name="rest-api-example"></a>REST API の例

値をエンドポイントとして使用して、GET 要求 `/teams/{teamId}/conversations/` `serviceUrl` を直接発行します。

唯一のソース `teamId` は、チーム コンテキストからのメッセージです。 メッセージは、ユーザーからのメッセージか、ボットがチームに追加するときに受信するメッセージのいずれかです。 詳細については、「チームに [追加されたボットまたはユーザー」を参照してください](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。

> [!NOTE]
> 値 `serviceUrl` は安定している傾向がありますが、変更される可能性があります。 新しいメッセージが届いた場合、ボットは保存されている値を確認する必要 `serviceUrl` があります。

```json
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

#### <a name="net-example"></a>.NET の例

次の例では、ボット ビルダー SDK for .NET Teams拡張機能からの呼び `FetchChannelList` [出しを使用します](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)。

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js例

次の例では、ボット ビルダー SDK Teams `fetchChannelList` [拡張機能からの呼び出しを使用Node.js。 ](https://www.npmjs.com/package/botbuilder-teams)

```javascript
var teamId = session.message.sourceEvent.team.id;
connector.fetchChannelList(
  (session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is an error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

## <a name="get-clientinfo-in-your-bot-context"></a>ボット コンテキストで clientInfo を取得する

ボットのアクティビティ内で clientInfo をフェッチできます。 clientInfo には、次のプロパティが含まれます。

* Locale
* 国
* プラットフォーム
* タイムゾーン

### <a name="json-example"></a>JSON の例

```json
[
    {
        "type": "clientInfo",
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "Asia/Calcutta"
    }
]
```

### <a name="c-example"></a>C#例

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```
