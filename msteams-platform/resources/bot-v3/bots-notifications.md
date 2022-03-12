---
title: ボット イベントの処理
description: ボットでイベントを処理する方法について説明Microsoft Teams
keywords: teams ボット イベント
ms.date: 05/20/2019
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 89d5bd3d1fb13961822cbb261bf25b5ca40ead34
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452733"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>ボット イベントを処理するMicrosoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams、ボットがアクティブなスコープで発生する変更やイベントに関する通知をボットに送信します。 これらのイベントを使用して、次のようなサービス ロジックをトリガーできます。

* ボットがチームに追加されると、ウェルカム メッセージをトリガーします。
* ボットがグループ チャットに追加された場合に、グループ情報をクエリしてキャッシュします。
* チーム メンバーシップまたはチャネル情報に関するキャッシュ情報を更新します。
* ボットが削除された場合は、チームのキャッシュされた情報を削除します。
* ボット メッセージがユーザーに気に入った場合。

各ボット イベントは、オブジェクト内の`Activity``messageType`情報を定義するオブジェクトとして送信されます。 種類のメッセージについては、「メッセージ `message`の [送受信」を参照してください](~/resources/bot-v3/bot-conversations/bots-conversations.md)。

`conversationUpdate` Teamsイベントとグループ イベント (通常は型からトリガーされる) には、オブジェクトの一部として渡される追加の Teams `channelData` `channelData` イベント情報が含まれます。そのため、イベント ハンドラーは Teams `eventType` および追加のイベント固有のメタデータのペイロードを照会する必要があります。

次の表に、ボットが受け取ってアクションを実行できるイベントの一覧を示します。

|型|Payload オブジェクト|Teams eventType |説明|範囲|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[チームに追加されたメンバー](#team-member-or-bot-addition)| すべての |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[メンバーがチームから削除された](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [チームの名前が変更されました](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [チャネルが作成されました](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [チャネルの名前が変更されました](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [チャネルが削除されました](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [ボット メッセージへの反応](#reactions)| すべての |
| `messageReaction` |`reactionsRemoved`|| [ボット メッセージから削除された反応](#reactions)| すべての |

## <a name="team-member-or-bot-addition"></a>チーム メンバーまたはボットの追加

イベント [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) は、追加されたチームのメンバーシップ更新に関する情報を受信すると、ボットに送信されます。 また、ボットが特定の個人の会話に初めて追加されたときにも更新を受け取ります。 ユーザー情報 (`Id`) はボットに対して一意であり、特定のユーザーにメッセージを送信するなどのサービスで将来使用するためにキャッシュできます。

### <a name="bot-or-user-added-to-a-team"></a>チームに追加されたボットまたはユーザー

ペイロード `conversationUpdate` 内のオブジェクト `membersAdded` を含むイベントは、ボットがチームに追加された場合、またはボットが追加されたチームに新しいユーザーが追加された場合に送信されます。 Microsoft Teamsオブジェクトにも`eventType.teamMemberAdded`追加`channelData`されます。

このイベントはどちらの `membersAdded` 場合も送信されますので、オブジェクトを解析して、追加がユーザーかボット自体かを判断する必要があります。 後者の場合、ベスト プラクティスは、ユーザーがボット[](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams)が提供する機能をユーザーが理解できるよう、チャネルにウェルカム メッセージを送信する方法です。

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>コード例: ボットが追加されたメンバーであるかどうかを確認する

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

#### <a name="schema-example-bot-added-to-team"></a>スキーマの例: ボットがチームに追加されました

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

### <a name="user-added-to-a-meeting"></a>会議に追加されたユーザー

ペイロード `conversationUpdate` 内のオブジェクトを `membersAdded` 含むイベントは、ユーザーがプライベートスケジュールされた会議に追加された場合に送信されます。 匿名ユーザーが会議に参加した場合でも、イベントの詳細が送信されます。

> [!NOTE]
>
>* 匿名ユーザーが会議に追加される場合、membersAdded ペイロード オブジェクトにはフィールド `aadObjectId` はありません。
>* 匿名ユーザーが会議 `from` に追加された場合、匿名ユーザーが別の発表者によって追加された場合でも、ペイロード内のオブジェクトは常に会議開催者の ID を持つ。

#### <a name="schema-example-user-added-to-meeting"></a>スキーマの例: 会議に追加されたユーザー

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

### <a name="bot-added-for-personal-context-only"></a>個人用コンテキスト用に追加されたボットのみ

ボットは、ユーザーが個人用 `conversationUpdate` チャット `membersAdded` に直接追加すると、そのメッセージを受信します。 この場合、ボットが受け取るペイロードにはオブジェクトが含 `channelData.team` まれます。 スコープに応じてボットが別のウェルカム メッセージを提供する場合は、これを [フィルターとして使用](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) する必要があります。

> [!NOTE]
> 個人用スコープボットの場合、 `conversationUpdate` ボットが削除され、再追加された場合でも、ボットはイベントを複数回受信します。 開発とテストでは、ボットを完全にリセットできるヘルパー関数を追加すると便利です。 この実装 [Node.js詳細については](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) C# [の例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) を参照してください。

#### <a name="schema-example-bot-added-to-personal-context"></a>スキーマの例: 個人用コンテキストにボットを追加する

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

## <a name="team-member-or-bot-removed"></a>チーム メンバーまたはボットが削除されました

ペイロード `conversationUpdate` 内のオブジェクト `membersRemoved` を含むイベントは、ボットがチームから削除されたか、ボットが追加されたチームからユーザーが削除されると送信されます。 Microsoft Teamsオブジェクトにも`eventType.teamMemberRemoved`追加`channelData`されます。 オブジェクトと同様に `membersAdded` 、ボット `membersRemoved` のアプリ ID のオブジェクトを解析して、削除されたユーザーを特定する必要があります。

### <a name="schema-example-team-member-removed"></a>スキーマの例: チーム メンバーが削除されました

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

### <a name="user-removed-from-a-meeting"></a>会議から削除されたユーザー

ペイロード `conversationUpdate` 内のオブジェクトを `membersRemoved` 含むイベントは、ユーザーがプライベートスケジュールされた会議から削除されると送信されます。 匿名ユーザーが会議に参加した場合でも、イベントの詳細が送信されます。

> [!NOTE]
>
>* 匿名ユーザーが会議から削除されると、membersRemoved ペイロード オブジェクトにはフィールド `aadObjectId` はありません。
>* 匿名ユーザーが会議 `from` から削除されると、匿名ユーザーが別の発表者によって削除された場合でも、ペイロード内のオブジェクトは常に会議開催者の ID を持つ。

#### <a name="schema-example-user-removed-from-meeting"></a>スキーマの例: 会議から削除されたユーザー

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
> すべてのチーム名を照会する機能はありません。また、他のイベントからのペイロードではチーム名は返されません。

ボットが含むチームの名前が変更された場合、ボットに通知されます。 オブジェクトでイベント `conversationUpdate` を受 `eventType.teamRenamed` け取 `channelData` ります。 ボットはチームの一部としてのみ存在し、追加されたスコープ外の可視性を持たないので、チームの作成または削除に関する通知はありません。

### <a name="schema-example-team-renamed"></a>スキーマの例: チームの名前が変更されました

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

チャネルが追加されたチームでチャネルが作成、名前変更、または削除されると、ボットに通知されます。 `conversationUpdate`繰り返しますが、イベントが受信され、Teams `channelData.eventType` `channel.id` 固有のイベント識別子がオブジェクトの一部として送信され、チャネル データはチャネルの GUID `channel.name` であり、チャネル名自体が含まれる。

チャネル イベントは次のとおりです。

* **channelCreated**&emsp;ユーザーがチームに新しいチャネルを追加します。
* **channelRenamed**&emsp;ユーザーが既存のチャネルの名前を変更します。
* **channelDeleted**&emsp;ユーザーがチャネルを削除します。

### <a name="full-schema-example-channelcreated"></a>完全なスキーマの例: channelCreated

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>スキーマの抜粋: channelData for channelRenamed

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>スキーマの抜粋: channelData for channelDeleted

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

イベント `messageReaction` は、ユーザーがボットから送信されたメッセージに対する反応を追加または削除すると送信されます。 `replyToId` には、特定のメッセージの ID が含まれる。

### <a name="schema-example-a-user-likes-a-message"></a>スキーマの例: ユーザーがメッセージを気に入る

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

### <a name="schema-example-a-user-un-likes-a-message"></a>スキーマの例: ユーザーがメッセージを好きにしない

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
