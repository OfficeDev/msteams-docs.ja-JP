---
title: Microsoft Teams ボットのコンテキストを取得する
description: このモジュールでは、Microsoft Teams でボットのコンテキストを取得し、個人チャットまたはグループ チャットでチーム名簿とユーザー プロファイルまたは名簿を取得する方法について説明します
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: fd43d9c4b3a3e4702b9bbd4955e58c0fc86caddf
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780927"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Microsoft Teams ボットのコンテキストを取得する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットは、チームまたはチャットに関する追加のコンテキスト (ユーザー プロファイルなど) にアクセスできます。 この情報は、ボットの機能を強化し、よりパーソナライズされたエクスペリエンスを提供するために使用できます。

> [!NOTE]
>
> * Microsoft Teams 固有のボット API には、Bot Builder SDK 用の拡張機能からアクセスするのが最適です。
> * C# または .NET の場合は、 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをダウンロードします。
> * Node.js開発では、Bot Framework SDK v4.6 に [Bot](https://github.com/microsoft/botframework-sdk) Builder for Teams 機能が組み込まれています。

## <a name="fetch-the-team-roster"></a>チーム名簿を取得する

ボットは、チーム メンバーとその基本的なプロファイルの一覧に対してクエリを実行できます。 基本的なプロファイルには、Teams ユーザー ID とMicrosoft Azure Active Directory (Azure AD) 情報 (名前やオブジェクト ID など) が含まれます。 この情報を使用して、ユーザー ID を関連付けることができます。 たとえば、Microsoft Azure Active Directory (Azure AD) 資格情報を使用してタブにログインしたユーザーがチーム メンバーであるかどうかを確認します。

### <a name="rest-api-example"></a>REST API の例

エンドポイントとして値を使用して、GET 要求 [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)を `serviceUrl` 直接発行します。

このオブジェクトは `teamId` 、次のシナリオで `channeldata` ボットが受け取るアクティビティ ペイロードのオブジェクトにあります。

* ユーザーがチーム コンテキストでボットにメッセージを送信したり、ボットと対話したりする場合。 詳細については、「 [メッセージの受信」を](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)参照してください。
* 新しいユーザーまたはボットがチームに追加されたとき。 詳細については、 [チームに追加されたボットまたはユーザーを](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)参照してください。

> [!NOTE]
>
>* API を呼び出すときは、常にチーム ID を使用してください。
>* 値は `serviceUrl` 安定する傾向がありますが、変更される可能性があります。 新しいメッセージが届いたら、ボットは格納されている `serviceUrl` 値を確認する必要があります。

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

ユーザー ID の一覧を返すために使用する`Team.Id`呼び出し`GetConversationMembersAsync`。
get `userRole` プロパティの呼び出し`GetConversationMembersAsync`は、ユーザーとして値を返します。

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>個人チャットまたはグループ チャットでユーザー プロファイルまたは名簿を取得する

任意のパーソナル チャットの API 呼び出しを行って、ボットとチャットしているユーザーのプロファイル情報を取得できます。

API 呼び出し、SDK メソッド、および応答オブジェクトは、チーム名簿のフェッチと同じです。 唯一の違いは、.`conversationId` `teamId`

## <a name="fetch-the-list-of-channels-in-a-team"></a>チーム内のチャネルの一覧を取得する

ボットは、チーム内のチャネルのリストをクエリできます。

> [!NOTE]
>
>* ローカリゼーションを可能にするために、既定の一般チャネルの名前が `null` として返されます。
>* 一般チャネルのチャネル ID は、常にチーム ID と一致します。

### <a name="rest-api-example"></a>REST API の例

エンドポイントとして値を使用して、GET 要求 `/teams/{teamId}/conversations/`を `serviceUrl` 直接発行します。

唯一の `teamId` ソースは、チーム コンテキストからのメッセージです。 メッセージは、ユーザーからのメッセージか、ボットがチームに追加されたときに受け取るメッセージです。 詳細については、 [チームに追加されたボットまたはユーザーを](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)参照してください。

> [!NOTE]
> 値は `serviceUrl` 安定する傾向がありますが、変更される可能性があります。 新しいメッセージが届いたら、ボットは格納されている `serviceUrl` 値を確認する必要があります。

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

次の例では、`FetchChannelList`[Bot Builder SDK for .NET の Teams 拡張機能](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)からの呼び出しを使用します。

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js の例

次の例では、[Bot Builder SDK for Node.jsの Teams 拡張機能](https://www.npmjs.com/package/botbuilder-teams)からの呼び出しを使用`fetchChannelList`します。

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

ボットのアクティビティ内で clientInfo をフェッチできます。 clientInfo には、次のプロパティが含まれています。

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

[Bot Framework サンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
