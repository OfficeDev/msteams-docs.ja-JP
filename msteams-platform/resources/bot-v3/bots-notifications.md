---
title: Bot イベントを処理する
description: Microsoft Teams でボットのイベントを処理する方法について説明します。
keywords: teams の bot イベント
ms.date: 05/20/2019
ms.openlocfilehash: 06da5e6b0668e86012d87af3184493cdeb70aecd
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801232"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Microsoft Teams で bot イベントを処理する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams は、bot がアクティブである範囲で発生した変更やイベントについて、bot に通知を送信します。 これらのイベントを使用して、次のようなサービスロジックをトリガーできます。

* Bot がチームに追加されたときに開始メッセージをトリガーする
* Bot がグループチャットに追加されたときに、グループ情報を照会およびキャッシュする
* チームメンバーシップまたはチャネル情報のキャッシュされた情報を更新する
* Bot が削除された場合にチームのキャッシュされた情報を削除する
* Bot メッセージがユーザーによって好評になった場合

各 bot イベントは、 `Activity` `messageType` オブジェクトに含まれている情報を定義するオブジェクトとして送信されます。 受信メッセージの種類につい `message` ては、「[メッセージの送受信](~/resources/bot-v3/bot-conversations/bots-conversations.md)」を参照してください。

通常、チームおよびグループイベントは、通常は型から呼び出され、 `conversationUpdate` 追加の teams イベント情報がオブジェクトの一部として渡される `channelData` ため、イベントハンドラーは `channelData` teams `eventType` および追加のイベント固有のメタデータのペイロードを照会する必要があります。

次の表に、ボットが受信してアクションを実行できるイベントを示します。

|型|ペイロードオブジェクト|Teams の eventType |説明|範囲|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[チームに追加されたメンバー](#team-member-or-bot-addition)| すべての |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[メンバーがチームから削除されました](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [チームの名前変更](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [チャネルが作成されました](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [チャネルの名前が変更されました](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [チャネルが削除されました](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Bot メッセージへの反応](#reactions)| すべての |
| `messageReaction` |`reactionsRemoved`|| [Bot メッセージからの反力の削除](#reactions)| すべての |

## <a name="team-member-or-bot-addition"></a>チームメンバーまたはボットの追加

イベントは、 [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) 追加されたチームのメンバーシップ更新に関する情報を受け取ったときに bot に送信されます。 また、ボットが特定の個人の会話に初めて追加されたときにも更新を受け取ります。 ユーザー情報 ( `Id` ) は bot に対して一意であることに注意してください。また、サービス (特定のユーザーへのメッセージの送信など) で将来使用するためにキャッシュすることができます。

### <a name="bot-or-user-added-to-a-team"></a>チームに追加された Bot またはユーザー

`conversationUpdate` `membersAdded` ユーザーがチームに bot が追加されるか、または bot が追加されたチームに新しいユーザーが追加されると、ペイロード内のオブジェクトを持つイベントが送信されます。 Microsoft Teams でも `eventType.teamMemberAdded` オブジェクトが追加さ `channelData` れます。

このイベントは両方の場合で送信されるため、オブジェクトを解析して、 `membersAdded` 追加がユーザーか bot 自体かを判断する必要があります。 後者の場合は、ユーザーが bot が提供する機能を理解できるように、[開始メッセージ](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams)をチャネルに送信することをお勧めします。

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>コード例: bot が追加されたメンバーであるかどうかを確認する

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

#### <a name="schema-example-bot-added-to-team"></a>スキーマの例: チームに追加された Bot

```json
{
    "membersAdded": [
        {
            "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:38:35.312Z",
    "localTimestamp": "2017-02-23T12:38:35.312-07:00",
    "id": "f:5f85c2ad",
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
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="bot-added-for-personal-context-only"></a>個人コンテキストのみに追加された Bot

Bot は、 `conversationUpdate` ユーザーが `membersAdded` 個人チャット用に直接追加したを使用してを受信します。 この場合、ボットが受け取るペイロードにはオブジェクトが含まれていません `channelData.team` 。 この範囲に応じて、bot が異なる[ウェルカムメッセージ](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations)を提供するようにする場合に備えて、これをフィルターとして使用する必要があります。

> [!NOTE]
> 個人のスコープのボットの場合、bot が削除されて再度追加されても、そのイベントは1回だけ受信され `conversationUpdate` ます。 開発およびテストの場合は、ボットを完全にリセットできるヘルパー関数を追加すると便利です。 これを実装する方法の詳細については、 [Node.js 例](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts)または[C# の例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238)を参照してください。

#### <a name="schema-example-bot-added-to-personal-context"></a>スキーマの例: 個人コンテキストに追加された bot

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

## <a name="team-member-or-bot-removed"></a>チームメンバーまたは bot が削除されました

`conversationUpdate` `membersRemoved` ユーザーがチームから bot を削除したとき、または bot が追加されたチームからユーザーが削除されたときに、ペイロード内のオブジェクトを含むイベントが送信されます。 Microsoft Teams でも `eventType.teamMemberRemoved` オブジェクトが追加さ `channelData` れます。 オブジェクトと同様に、 `membersAdded` `membersRemoved` Bot のアプリ ID のオブジェクトを解析して、削除されたユーザーを特定する必要があります。

### <a name="schema-example-team-member-removed"></a>スキーマの例: チームメンバーが削除されました

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

## <a name="team-name-updates"></a>チーム名の更新

> [!NOTE]
> すべてのチーム名を照会する機能はありません。また、他のイベントからのペイロードではチーム名が返されません。

自分のチームの名前が変更されると、ボットに通知されます。 `conversationUpdate` `eventType.teamRenamed` オブジェクト内でイベントを受け取り `channelData` ます。 Bot は teams の一部としてのみ存在し、追加された範囲外には表示されないので、チーム作成または削除の通知はありません。

### <a name="schema-example-team-renamed"></a>スキーマの例: チームの名前変更

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

Bot が追加されたチームでチャネルが作成、名前変更、または削除されると、ボットに通知されます。 `conversationUpdate`イベントが受信され、チーム固有のイベント識別子がオブジェクトの一部として送信され `channelData.eventType` ます。ここで、チャネルデータはチャネルの GUID で、チャネル `channel.id` `channel.name` 名自体が含まれます。

チャネルイベントは次のとおりです。

* **Channelcreated** &emsp;ユーザーが新しいチャネルをチームに追加した
* **Channelrenamed 名前変更** &emsp;ユーザーが既存のチャネルの名前を変更する
* **Channeldeleted** &emsp;ユーザーがチャネルを削除した場合

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>スキーマの抜粋: channelData が名前変更されました

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>スキーマの抜粋: チャネルが削除された channelData

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

## <a name="reactions"></a>感想

この `messageReaction` イベントは、ユーザーが最初に bot によって送信されたメッセージに対して、自分の反応を追加または削除したときに送信されます。 `replyToId`特定のメッセージの ID を格納します。

### <a name="schema-example-a-user-likes-a-message"></a>スキーマの例: ユーザーがメッセージを好む

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

### <a name="schema-example-a-user-un-likes-a-message"></a>スキーマの例: ユーザーがメッセージの表示を取り消す

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
