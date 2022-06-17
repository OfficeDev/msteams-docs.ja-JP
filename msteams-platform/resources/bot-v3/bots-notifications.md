---
title: ボット イベントを処理する
description: このモジュールでは、Microsoft Teams、Teamsメンバーまたはボットの追加、チーム メンバーまたはボットの削除などのボット内のイベントを処理する方法について説明します
ms.date: 05/20/2019
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 30ccb4ee8810154e2b36311d15217205de87b413
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142760"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Microsoft Teams でボット イベントを処理する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams は、ボットがアクティブなスコープで発生する変更やイベントに関する通知をボットに送信します。 これらのイベントを使用して、次のようなサービス ロジックをトリガーできます。

* ボットがチームに追加されたときに、ウェルカム メッセージをトリガーする。
* ボットがグループ チャットに追加されたときに、グループ情報をクエリおよびキャッシュする。
* チーム メンバーシップまたはチャネル情報に関するキャッシュされた情報を更新する。
* ボットが削除された場合は、キャッシュされたチームの情報を削除する。
* ボット メッセージがユーザーによって "いいね!" された場合。

各ボット イベントは `Activity` オブジェクトとして送信されます。このオブジェクトに含まれる情報は `messageType` で定義されます。 `message` の種類のメッセージについては、[メッセージの送受信](~/resources/bot-v3/bot-conversations/bots-conversations.md)に関する記事を参照してください。

Teamsイベントとグループ イベントは、型から`conversationUpdate`トリガーされ、より多くのTeamsイベント情報がオブジェクトの`channelData`一部として渡されるため、イベント ハンドラーは、Teams`eventType`とより多くのイベント固有のメタデータのペイロードに対してクエリを実行`channelData`する必要があります。

次の表に、ボットが受信してアクションを実行できるイベントの一覧を示します。

|種類|ペイロード オブジェクト|Teams eventType |説明|範囲|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[チームへのメンバーの追加](#team-member-or-bot-addition)| すべて |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[チームからのメンバーの削除](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [チームの名前の変更](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [チャネルの作成](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [チャネルの名前の変更](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [チャネルの削除](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [ボット メッセージへのリアクション](#reactions)| すべて |
| `messageReaction` |`reactionsRemoved`|| [ボット メッセージからのリアクションの削除](#reactions)| すべて |

## <a name="team-member-or-bot-addition"></a>チーム メンバーまたはボットの追加

[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) イベントは、ボットが追加されているチームのメンバーシップの更新に関する情報を受信したときにボットに送信されます。 また、ボットが特定の個人の会話に初めて追加されたときにも更新を受け取ります。 ユーザー情報 (`Id`) はボットに対して一意であり、特定のユーザーにメッセージを送信するなど、サービスが今後使用するためにキャッシュできます。

### <a name="bot-or-user-added-to-a-team"></a>チームへのボットまたはユーザーの追加

ペイロード内の `membersAdded` オブジェクトを含む `conversationUpdate` イベントは、ボットがチームに追加されるか、ボットが既に追加されているチームに新しいユーザーが追加されたときに送信されます。 Microsoft Teams では `channelData` オブジェクトに `eventType.teamMemberAdded` も追加されます。

このイベントはどちらの場合も送信されるため、追加されたのがユーザーかボット自体かを判断するには、`membersAdded` オブジェクトを解析する必要があります。 後者の場合、ユーザーがボットによって提供される機能を理解できるように、[ウェルカム メッセージ](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams)をチャネルに送信することがベスト プラクティスです。

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>コード例: ボットが追加されたメンバーだったかどうかの確認

##### <a name="net"></a>.NET

```csharp
    for (int i = 0; i < sourceMessage.MembersAdded.Count; i++)
    {
        if (sourceMessage.MembersAdded[i].Id == sourceMessage.Recipient.Id)
        {
            addedBot = true;
            break;
        }
    }
```

##### <a name="nodejs"></a>Node.js

```javascript
const builder = require('botbuilder');

var c = new builder.ChatConnector({appId: BOT_APP_ID, appPassword: .BOT_SECRET});
var bot = new builder.UniversalBot(c);

bot.on('conversationUpdate', (msg) => {
    var members = msg.membersAdded;
    // Loop through all members that were just added to the team
    for (var i = 0; i < members.length; i++) {

        // See if the member added was our bot
        if (members[i].id.includes(BOT_APP_ID)) {
            var botmessage = new builder.Message()
                .address(msg.address)
                .text('Hello World!');

            bot.send(botmessage, function(err) {});
        }
    }
});
```

#### <a name="schema-example-bot-added-to-team"></a>スキーマ例: チームへのボットの追加

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a>会議へのユーザーの追加

ペイロード内の `membersAdded` オブジェクトを含む `conversationUpdate` イベントは、ユーザーがスケジュールされたプライベート会議に追加されたときに送信されます。 匿名ユーザーがこの会議に参加した場合でも、イベントの詳細が送信されます。

> [!NOTE]
>
>* 匿名ユーザーが会議に追加される場合、membersAdded ペイロード オブジェクトには `aadObjectId` フィールドがありません。
>* 匿名ユーザーが会議に追加される場合、そのペイロード内の `from` オブジェクトには常に会議の開催者の ID が指定されます。これは、その匿名ユーザーが別の発表者によって追加された場合でも同じです。

#### <a name="schema-example-user-added-to-meeting"></a>スキーマ例: 会議へのユーザーの追加

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a>個人用コンテキスト専用のボットの追加

ユーザーが個人用チャットのためにボットを直接追加すると、ボットは `membersAdded` を含む `conversationUpdate` を受け取ります。 この場合、ボットが受け取るペイロードに `channelData.team` オブジェクトは含まれません。 スコープに応じてボットで異なる[ウェルカム メッセージ](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations)を提供する必要がある場合は、これをフィルターとして使用する必要があります。

> [!NOTE]
> 個人スコープのボットの場合、ボットが削除されて再度追加された場合でも、ボットは `conversationUpdate` イベントを複数回受け取ります。 開発とテストでは、ボットを完全にリセットできるヘルパー関数を追加すると便利な場合があります。 これを実装する方法の詳細については、[Node.js の例](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts)や [C# の例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238)を参照してください。

#### <a name="schema-example-bot-added-to-personal-context"></a>スキーマ例: 個人用コンテキストへのボットの追加

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
    "aadObjectId": "***"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "***"
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

## <a name="team-member-or-bot-removed"></a>チーム メンバーまたはボットの削除

ペイロード内の `membersRemoved` オブジェクトを含む `conversationUpdate` イベントは、ボットがチームから削除されるか、ボットが追加されているチームからユーザーが削除されたときに送信されます。 Microsoft Teams では `channelData` オブジェクトに `eventType.teamMemberRemoved` も追加されます。 `membersAdded` オブジェクトと同様に、削除されたユーザーを判断するには、ボットのアプリ ID の `membersRemoved` オブジェクトを解析する必要があります。

### <a name="schema-example-team-member-removed"></a>スキーマ例: チーム メンバーの削除

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

### <a name="user-removed-from-a-meeting"></a>会議からのユーザーの削除

ペイロード内の `membersRemoved` オブジェクトを含む `conversationUpdate` イベントは、ユーザーがスケジュールされたプライベート会議から削除されたときに送信されます。 匿名ユーザーがこの会議に参加した場合でも、イベントの詳細が送信されます。

> [!NOTE]
>
>* 匿名ユーザーが会議から削除される場合、membersRemoved ペイロード オブジェクトには `aadObjectId` フィールドがありません。
>* 匿名ユーザーが会議から削除される場合、そのペイロード内の `from` オブジェクトには常に会議の開催者の ID が指定されます。これは、その匿名ユーザーが別の発表者によって削除された場合でも同じです。

#### <a name="schema-example-user-removed-from-meeting"></a>スキーマ例: 会議からのユーザーの削除

```
{   
      "membersRemoved": 
        {  
          "id": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"   
        }   
      ],   
      "type": "conversationUpdate",   
      "timestamp": "2020-09-29T21:15:08.6391139Z",   
      "id": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",   
      "channelId": "msteams",   
      "serviceUrl": "https://canary.botapi.skype.com/amer/",   
      "from": {   
        "id": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",   
        "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"   
      },   
      "conversation": {    
        "isGroup": true,   
        "tenantId": "e15762ef-a8d8-416b-871c-25516354f1fe",   
        "id": "19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"   
      },   
      "recipient": {   
        "id": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",   
        "name": "EchoBot1_Rename"   
      },   
      "channelData": {   
        "tenant": {   
          "id": "e15762ef-a8d8-416b-871c-25516354f1fe"   
        },   
        "source": null,   
        "meeting": {   
          "id": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="   
        }   
      }   
}
```

## <a name="team-name-updates"></a>チーム名の更新

> [!NOTE]
> すべてのチーム名に対してクエリを実行する機能はなく、チーム名は他のイベントのペイロードでは返されません。

ボットが含まれているチームの名前が変更されると、そのボットは通知を受け取ります。 ボットは、`channelData` オブジェクト内に `eventType.teamRenamed` を含む `conversationUpdate` イベントを受信します。 ボットはチームの一部としてのみ存在し、追加されたスコープ外の可視性がないため、チームの作成または削除に関する通知はありません。

### <a name="schema-example-team-renamed"></a>スキーマ例: チームの名前の変更

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

## <a name="channel-updates"></a>チャネルの更新

ボットが追加されているチームでチャネルが作成、名前変更、または削除されると、そのボットは通知を受け取ります。 ここでも、`conversationUpdate` イベントが受信され、Teams 固有のイベント識別子が `channelData.eventType` オブジェクトの一部として送信されます。このチャネル データの `channel.id` はチャネルの GUID であり、`channel.name` にはチャネル名自体が含まれます。

チャネル イベントは次のとおりです。

* **channelCreated**&emsp;ユーザーがチームに新しいチャネルを追加する。
* **channelRenamed**&emsp;ユーザーが既存のチャネルの名前を変更する。
* **channelDeleted**&emsp;ユーザーがチャネルを削除する。

### <a name="full-schema-example-channelcreated"></a>完全なスキーマ例: channelCreated

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>スキーマの抜粋: channelRenamed の場合の channelData

```json
⋮
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
⋮
```

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>スキーマの抜粋: channelDeleted の場合の channelData

```json
⋮
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
⋮
```

## <a name="reactions"></a>リアクション

イベントは `messageReaction` 、ユーザーがメッセージに対する反応を追加または削除したときに送信されます。これは、もともとボットによって送信されました。 `replyToId` には、その特定のメッセージの ID が含まれます。

### <a name="schema-example-a-user-likes-a-message"></a>スキーマ例: ユーザーがメッセージに "いいね!" する

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
    "replyToId": "1575667808184"
}
```

### <a name="schema-example-a-user-un-likes-a-message"></a>スキーマ例: ユーザーがメッセージの "いいね!" を解除する

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
    "replyToId": "1575667808184"
}
```
