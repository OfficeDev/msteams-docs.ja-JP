---
title: Microsoft Teams ボットのコンテキストを取得する
description: Microsoft Teams でボットのコンテキストを取得する方法について説明します。
keywords: チーム ボットのコンテキスト
ms.date: 05/20/2019
ms.openlocfilehash: 1465e6624b4eaadd73e2d4d9cf87fccedc002e52
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231553"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Microsoft Teams ボットのコンテキストを取得する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットは、ユーザー プロファイルなど、チームまたはチャットに関する追加のコンテキストにアクセスできます。 この情報は、ボットの機能を強化し、よりカスタマイズされたエクスペリエンスを提供するために使用できます。

> [!NOTE]
>
> * Microsoft Teams 固有のボット API は、Bot Builder SDK の拡張機能を通じて最適にアクセスできます。
> * C# または .NET の場合は [、Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをダウンロードします。
> * 開発Node.js、Teams のボット ビルダー機能は [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6 に組み込まれています。

## <a name="fetch-the-team-roster"></a>チーム名簿を取得する

ボットは、チーム メンバーのリストとその基本的なプロファイルを照会できます。 基本的なプロファイルには、Teams ユーザー ID と、名前やオブジェクト ID などの Azure Active Directory (AAD) 情報が含まれます。 この情報を使用して、ユーザー ID を関連付けできます。 たとえば、AAD 資格情報を使用してタブにログインしたユーザーがチーム メンバーである場合を確認します。

### <a name="rest-api-example"></a>REST API の例

値をエンドポイントとして使用して、GET [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) `serviceUrl` 要求を直接発行します。

次 `teamId` のシナリオでは、ボットが受け取るアクティビティ ペイロード `channeldata` のオブジェクト内で確認できます。

* ユーザーがチーム コンテキストでボットにメッセージを送信または操作する場合。 詳細については、「メッセージの受信 [」を参照してください](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)。
* 新しいユーザーまたはボットがチームに追加された場合。 詳細については、チームに [追加されたボットまたはユーザーを参照してください](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)。

> [!NOTE]
>
>* API を呼び出す場合は、常にチーム ID を使用します。
>* 値 `serviceUrl` は安定する傾向がありますが、変更される可能性があります。 新しいメッセージが到着したら、ボットは保存された値を確認する必要 `serviceUrl` があります。

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

ユーザー `GetConversationMembersAsync` ID `Team.Id` の一覧を返す呼び出し

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

また [、Bot Framework のサンプルも参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>個人チャットまたはグループ チャットでユーザー プロファイルまたは名簿を取得する

任意の個人チャットの API 呼び出しを行って、ボットとチャットしているユーザーのプロファイル情報を取得できます。

API 呼び出し、SDK メソッド、および応答オブジェクトは、チーム名簿の取得と同じです。 唯一の違いは、 `conversationId` `teamId` .

## <a name="fetch-the-list-of-channels-in-a-team"></a>チーム内のチャネルの一覧を取得する

ボットは、チーム内のチャネルの一覧を照会できます。

> [!NOTE]
>
>* ローカライズを許可するために、既定の全般チャネル `null` の名前が返されます。
>* 一般チャネルのチャネル ID は、常にチーム ID と一致します。

### <a name="rest-api-example"></a>REST API の例

値をエンドポイントとして使用して、GET `/teams/{teamId}/conversations/` `serviceUrl` 要求を直接発行します。

唯一のソース `teamId` は、チーム コンテキストからのメッセージです。 メッセージは、ユーザーからのメッセージか、ボットがチームに追加された際に受信するメッセージのいずれかです。 詳細については、チームに [追加されたボットまたはユーザーを参照してください](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。

> [!NOTE]
> 値 `serviceUrl` は安定する傾向がありますが、変更される可能性があります。 新しいメッセージが到着したら、ボットは保存された値を確認する必要 `serviceUrl` があります。

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

次の例では、.NET 用 Bot Builder SDK の Teams 拡張機能からの呼び `FetchChannelList` [出しを使用します](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)。

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js例

次の例では、Bot Builder SDK for Node.jsの Teams 拡張機能からの呼び出 `fetchChannelList` [しを使用します ](https://www.npmjs.com/package/botbuilder-teams)。

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

### <a name="c-example"></a>C# の例

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```