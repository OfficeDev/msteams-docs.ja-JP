---
title: Bot にカードアクションを追加する
description: Microsoft Teams でのカードアクションと、それらを bot で使用する方法について説明します。
keywords: teams のボットカードのアクション
ms.openlocfilehash: e0b050cde9adf5bd811d5d95ce1c6f1bf60546a1
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801268"
---
# <a name="card-actions"></a>カードのアクション

Teams のボットおよびメッセージング拡張機能によって使用されるカードは、次のアクティビティ () の種類をサポートして [`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) います。 これらのアクションは、 `potentialActions` コネクタから使用された場合、Office 365 コネクタカードとは異なることに注意してください。

| 型 | Action |
| --- | --- |
| `openUrl` | 既定のブラウザーで URL を開きます。 |
| `messageBack` | (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから) メッセージとペイロードを bot に送信し、別のメッセージをチャットストリームに送信します。 |
| `imBack`| Bot (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから) にメッセージを送信します。 このメッセージ (ユーザーから bot) は、すべての会話参加者に表示されます。 |
| `invoke` | Bot にメッセージとペイロードを送信します (ボタンをクリックしたユーザー、またはカードをタップしたユーザーから)。 このメッセージは表示されません。 |
| `signin` | OAuth フローを開始し、ボットがセキュリティ保護されたサービスで接続できるようにします。 |

> [!NOTE]
>* Teams `CardAction` では、上記の表に記載されていない種類はサポートされていません。
>* Teams はプロパティをサポートしていません `potentialActions` 。
>* カードアクションは、Bot フレームワーク/Azure Bot サービスの推奨される[アクション](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button)とは異なります。 Microsoft Teams では、推奨されるアクションはサポートされていません。 Teams の bot メッセージにボタンを表示する場合は、カードを使用します。
>* メッセージ拡張機能の一部としてカードアクションを使用している場合、カードがチャネルに送信されるまで、アクションは機能しません (カードが [新規作成] メッセージボックスにある間は機能しません)。

Teams は、アダプティブカードによってのみ使用される[アダプティブカードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)もサポートしています。 これらの操作は、このリファレンスの最後にあるセクションに記載されています。

## <a name="openurl"></a>openUrl

このアクションの種類では、既定のブラウザーで起動する URL を指定します。 Bot がクリックされたボタンに関する通知を受け取っていないことに注意してください。

このフィールドには、 `value` 完全で正しい形式の URL が含まれている必要があります。

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

では `messageBack` 、次のプロパティを使用して、完全にカスタマイズされたアクションを作成できます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタンのラベルとして表示されます。 |
| `displayText` | 省略可能です。 アクションの実行時にユーザーによってチャットストリームにエコーされます。 このテキストは bot に送信され*ません*。 |
| `value` | アクションが実行されたときに bot に送信されます。 一意の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードできます。 |
| `text` | アクションが実行されたときに bot に送信されます。 このプロパティを使用して、ボットの開発を簡素化します。コードでは、ボットロジックをディスパッチするために1つのトップレベルのプロパティをチェックできます。 |

柔軟には、 `messageBack` コードでは、を使用しないで、表示されるユーザーメッセージを履歴に残すことを選択でき `displayText` ます。

```json
{
  "buttons": [
    {
    "type": "messageBack",
    "title": "My MessageBack button",
    "displayText": "I clicked this button",
    "text": "User just clicked the MessageBack button",
    "value": "{\"property\": \"propertyValue\" }"
    }
  ]
}
```

このプロパティには、 `value` シリアル化された json 文字列または json オブジェクトのいずれかを指定できます。

### <a name="inbound-message-example"></a>受信メッセージの例

`replyToId`カードアクションの送信元のメッセージの ID が含まれます。 メッセージを更新する場合に使用します。

```json
{
   "text":"User just clicked the MessageBack button",
   "value":{
      "property":"propertyValue"
   },
   "type":"message",
   "timestamp":"2017-06-22T22:38:47.407Z",
   "id":"f:5261769396935243054",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:102jd210jd010icsoaeclaejcoa9ue09u",
      "name":"John Smith"
   },
   "conversation":{
      "id":"19:malejcou081i20ojmlcau0@thread.skype;messageid=1498171086622"
   },
   "recipient":{
      "id":"28:76096e45-119f-4736-859c-6dfff54395f7",
      "name":"MyBot"
   },
   "entities":[
      {
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo" 
      }
   ],
   "channelData":{
      "channel":{
         "id":"19:malejcou081i20ojmlcau0@thread.skype"
      },
      "team":{
         "id":"19:12d021jdoijsaeoaue0u@thread.skype"
      },
      "tenant":{
         "id":"bec8e231-67ad-484e-87f4-3e5438390a77"
      }
   },
        "replyToId": "1575667808184",
}
```

## <a name="imback"></a>imBack

この操作によって、ユーザーが通常のチャットメッセージに入力した場合と同じように、bot に返されるメッセージがトリガーされます。 チャネルを使用している場合、ユーザーとその他のすべてのユーザーは、そのボタンの応答を確認できます。

フィールドには `value` チャットでのテキスト文字列が含まれている必要があります。そのため、bot に送り返されます。 これは、ボットで処理して必要なロジックを実行するメッセージテキストです。 メモ: このフィールドは単純な文字列です。書式設定または隠し文字はサポートされていません。

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>invoke

`invoke`アクションは、[タスクモジュール](~/task-modules-and-cards/task-modules/task-modules-bots.md)を呼び出すために使用されます。

アクションには `invoke` `type` 、、、 `title` および `value` の3つのプロパティが含まれます。 このプロパティには、 `value` 文字列、文字列 json オブジェクト、または json オブジェクトを含めることができます。

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

ユーザーがボタンをクリックすると、bot は、 `value` 追加情報を含むオブジェクトを受け取ります。 アクティビティの種類は `invoke` () の代わりになることに注意してください `message` `activity.Type == "invoke"` 。

### <a name="example-invoke-button-definition-net"></a>例: Invoke button definition (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>例: 着信呼び出しメッセージ

トップレベルのプロパティには、 `replyToId` カードアクションの送信元であるメッセージの ID が含まれます。 メッセージを更新する場合に使用します。

```json
{
    "type": "invoke",
    "value": {
        "option": "opt1"
    },
    "timestamp": "2017-02-10T04:11:19.614Z",
    "localTimestamp": "2017-02-09T21:11:19.614-07:00",
    "id": "f:6894910862892785420",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1Eniglq0-uVL83xNB9GU6w_G5a4SZF0gcJLprZzhtEbel21G_5h-
    NgoprRw45mP0AXUIZVeqrsIHSYV4ntgfVJQ",
        "name": "John Doe"
    },
    "conversation": {
        "id": "19:97b1ec61-45bf-453c-9059-6e8984e0cef4_8d88f59b-ae61-4300-bec0-caace7d28446@unq.gbl.spaces"
    },
    "recipient": {
        "id": "28:8d88f59b-ae61-4300-bec0-caace7d28446",
        "name": "MyBot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Web",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "channel": {
            "id": "19:dc5ba12695be4eb7bf457cad6b4709eb@thread.skype"
        },
        "team": {
            "id": "19:712c61d0ef384e5fa681ba90ca943398@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

## <a name="signin"></a>signin

OAuth フローを開始し、次の詳細に説明するように、ボットでセキュリティ保護されたサービスとの接続を許可します。 [bot での認証フロー](~/bots/how-to/authentication/auth-flow-bot.md)。

## <a name="adaptive-cards-actions"></a>アダプティブカードのアクション

アダプティブカードは、次の3種類のアクションをサポートします。

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)

前述の操作に加え `Action.Submit` て、のオブジェクトのプロパティを使用して、既存の Bot フレームワークアクションをサポートするようにアダプティブカードのペイロードを変更でき `msteams` `data` `Action.Submit` ます。 次のセクションでは、既存の Bot フレームワークアクションをアダプティブカードで使用する方法について詳しく説明します。

### <a name="adaptive-cards-with-messageback-action"></a>MessageBack アクションを備えたアダプティブカード

アダプティブカードにアクションを含めるには、 `messageBack` オブジェクトに次の詳細情報が含まれて `msteams` います。 必要に応じて、追加の非表示プロパティをオブジェクトに含めることができることに注意 `data` してください。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定`messageBack` |
| `displayText` | 省略可能です。 アクションの実行時にユーザーによってチャットストリームにエコーされます。 このテキストは bot に送信され*ません*。 |
| `value` | アクションが実行されたときに bot に送信されます。 一意の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードできます。 |
| `text` | アクションが実行されたときに bot に送信されます。 このプロパティを使用して、ボットの開発を簡素化します。コードでは、ボットロジックをディスパッチするために1つのトップレベルのプロパティをチェックできます。 |

#### <a name="example"></a>例

```json
{
  "type": "Action.Submit",
  "title": "Click me for messageBack",
  "data": {
    "msteams": {
        "type": "messageBack",
        "displayText": "I clicked this button",
        "text": "text to bots",
        "value": "{\"bfKey\": \"bfVal\", \"conflictKey\": \"from value\"}"
    }
  }
}
```

### <a name="adaptive-cards-with-imback-action"></a>ImBack アクションを備えたアダプティブカード

アダプティブカードにアクションを含めるには、 `imBack` オブジェクトに次の詳細情報が含まれて `msteams` います。 必要に応じて、追加の非表示プロパティをオブジェクトに含めることができることに注意 `data` してください。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定`imBack` |
| `value` | チャットでエコーバックする必要がある文字列 |

#### <a name="example"></a>例

```json
{
  "type": "Action.Submit",
  "title": "Click me for imBack",
  "data": {
    "msteams": {
        "type": "imBack",
        "value": "Text to reply in chat"
    }
  }
}
```

### <a name="adaptive-cards-with-signin-action"></a>サインインカードとサインインアクション

アダプティブカードにアクションを含めるには、 `signin` オブジェクトに次の詳細情報が含まれて `msteams` います。 必要に応じて、追加の非表示プロパティをオブジェクトに含めることができることに注意 `data` してください。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定`signin` |
| `value` | リダイレクト先の URL に設定します。  |

#### <a name="example"></a>例

```json
{
  "type": "Action.Submit",
  "title": "Click me for signin",
  "data": {
    "msteams": {
        "type": "signin",
        "value": "https://signin.com"
    }
  }
}
```
