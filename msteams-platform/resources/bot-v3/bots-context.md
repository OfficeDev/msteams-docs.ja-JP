---
title: Microsoft Teamsボットのコンテキストを取得する
description: Microsoft Teamsでボットのコンテキストを取得する方法について説明します。
keywords: チームボットコンテキスト
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: cda2e24816330964342b097f52bb955c8846c54a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566489"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Microsoft Teamsボットのコンテキストを取得する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットは、チームやチャットに関するその他のコンテキスト (ユーザー プロファイルなど) にアクセスできます。 この情報を使用して、ボットの機能を強化し、よりパーソナライズされたエクスペリエンスを提供できます。

> [!NOTE]
>
> * Microsoft Teams固有のボット API は、ボット ビルダー SDK の拡張機能を通じてアクセスするのが最善です。
> * C# または .NET の場合は、NuGet パッケージをダウンロード[Teams。](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)
> * Node.js開発では、Teams機能のボット ビルダーが Bot [Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6 に組み込まれています。

## <a name="fetch-the-team-roster"></a>チーム名簿を取得する

ボットは、チーム メンバーとその基本プロファイルのリストを照会できます。 基本プロファイルには、名前やオブジェクト ID などのTeamsユーザー ID および Azure Active Directory (AAD) 情報が含まれます。 この情報を使用して、ユーザー ID を関連付けることができます。 たとえば、AAD 資格情報を使用してタブにログインしたユーザーがチーム メンバーであるかどうかを確認します。

### <a name="rest-api-example"></a>REST API の例

[`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)に値をエンドポイントとして使用して、GET 要求を直接発行 `serviceUrl` します。

は `teamId` 、 `channeldata` 次のシナリオでボットが受け取るアクティビティ ペイロードのオブジェクトにあります。

* チーム コンテキストでユーザーがボットにメッセージを送信したり、ボットと対話したりする場合。 詳細については、「 [メッセージの受信](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)」を参照してください。
* 新しいユーザーまたはボットがチームに追加された場合。 詳細については、「 [チームに追加されたボットまたはユーザー」を](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)参照してください。

> [!NOTE]
>
>* API を呼び出すときは、必ずチーム ID を使用してください。
>* `serviceUrl`値は安定する傾向がありますが、変化する可能性があります。 新しいメッセージが到着したら、ボットは保存された値を確認する必要があります `serviceUrl` 。

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

を呼び出 `GetConversationMembersAsync` `Team.Id` して、ユーザー ID のリストを返します。

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

### <a name="nodejs-or-typescript-example"></a>Node.jsまたはタイプスクリプトの例

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>個人チャットまたはグループ チャットでユーザー プロファイルまたは名簿を取得する

任意のパーソナルチャットの API 呼び出しを行って、ボットとチャットしているユーザーのプロファイル情報を取得できます。

API 呼び出し、SDK メソッド、および応答オブジェクトは、チームの一覧を取得する場合と同じです。 唯一の違いは、代 `conversationId` わりにを渡すことです `teamId` 。

## <a name="fetch-the-list-of-channels-in-a-team"></a>チーム内のチャネルのリストを取得する

ボットはチーム内のチャネルのリストを照会できます。

> [!NOTE]
>
>* `null`ローカリゼーションを許可するために、デフォルトの General チャネルの名前が返されます。
>* 一般チャネルのチャネル ID は、常にチーム ID と一致します。

### <a name="rest-api-example"></a>REST API の例

`/teams/{teamId}/conversations/`に値をエンドポイントとして使用して、GET 要求を直接発行 `serviceUrl` します。

唯一のソース `teamId` は、チームコンテキストからのメッセージです。 メッセージは、ユーザーからのメッセージか、チームに追加されたときにボットが受信するメッセージのいずれかです。 詳細については、「 [チームに追加されたボットまたはユーザー」を](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)参照してください。

> [!NOTE]
> `serviceUrl`値は安定する傾向がありますが、変化する可能性があります。 新しいメッセージが到着したら、ボットは保存された値を確認する必要があります `serviceUrl` 。

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

次の例では `FetchChannelList` [、.NET 用の Bot Builder SDK のTeams拡張](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)からの呼び出しを使用します。

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js例

次の例では `fetchChannelList` [、Node.jsの Bot Builder SDK のTeams拡張](https://www.npmjs.com/package/botbuilder-teams)からの呼び出しを使用します。

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

ボットのアクティビティ内で clientInfo を取得できます。 clientInfo には、次のプロパティが含まれています。

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

### <a name="c-example"></a>C# の例

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a>関連項目

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)