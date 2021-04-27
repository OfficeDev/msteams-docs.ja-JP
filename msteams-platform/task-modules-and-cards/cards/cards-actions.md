---
title: ボットにカード アクションを追加する
description: Microsoft Teams でのカードアクションとボットでのカードアクションの使い方について説明します。
localization_priority: Normal
ms.topic: conceptual
keywords: teams ボット カードアクション
ms.openlocfilehash: 84f47540cee99738204007fd107743f922552e60
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019539"
---
# <a name="card-actions"></a>カードアクション

Teams のボットとメッセージング拡張機能で使用されるカードは、次のアクティビティ ( ) の種類 [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) をサポートします。 これらのアクションは、コネクタ `potentialActions` と使用Office 365 コネクタ カードの場合とは異なります。

| 種類 | 操作 |
| --- | --- |
| `openUrl` | 既定のブラウザーで URL を開きます。 |
| `messageBack` | ボットにメッセージとペイロードを送信し (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから) チャット ストリームに別のメッセージを送信します。 |
| `imBack`| ボットにメッセージを送信します (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから)。 このメッセージ (ユーザーからボットへ) は、すべての会話参加者に表示されます。 |
| `invoke` | ボットにメッセージとペイロードを送信します (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから)。 このメッセージは表示されません。 |
| `signin` | OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。 |

> [!NOTE]
>* Teams では、前 `CardAction` の表にリストされていない種類はサポートされていません。
>* Teams では、このプロパティはサポート `potentialActions` されていません。
>* カードアクションは、Bot [](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) Framework/Azure Bot Service で推奨されるアクションとは異なります。 推奨されるアクションは Microsoft Teams ではサポートされていません。Teams ボット メッセージにボタンを表示する場合は、カードを使用します。
>* メッセージング拡張機能の一部としてカード アクションを使用している場合、カードがチャネルに送信されるまでアクションは機能しません (カードがメッセージの作成ボックスに入っている間は動作しません)。

Teams ではアダプティブ [カードアクションもサポートされています](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)。これはアダプティブ カードでのみ使用されます。 これらのアクションは、この参照の最後にある独自のセクションに一覧表示されます。

## <a name="openurl"></a>openUrl

このアクションの種類は、既定のブラウザーで起動する URL を指定します。 ボットは、クリックされたボタンに関する通知を受け取らない点に注意してください。

フィールド `value` には、完全で適切に形成された URL が含まれている必要があります。

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

を `messageBack` 使用すると、次のプロパティを使用して完全にカスタマイズされたアクションを作成できます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタン ラベルとして表示されます。 |
| `displayText` | 省略可能。 アクションの実行時に、ユーザーがチャット ストリームにエコーします。 このテキストは *ボット* に送信されません。 |
| `value` | アクションの実行時にボットに送信されます。 アクションのコンテキスト (一意の識別子や JSON オブジェクトなど) をエンコードできます。 |
| `text` | アクションの実行時にボットに送信されます。 ボットの開発を簡略化するには、このプロパティを使用します。コードでは、ボット ロジックをディスパッチするために 1 つのトップ レベル プロパティをチェックできます。 |

柔軟性は、コードが単に使用しないだけで、表示されるユーザー メッセージを履歴に残すのを選択 `messageBack` できないという意味です `displayText` 。

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

プロパティ `value` には、シリアル化された JSON 文字列または JSON オブジェクトを指定できます。

### <a name="inbound-message-example"></a>受信メッセージの例

`replyToId` には、カード アクションが送信されたメッセージの ID が含まれる。 メッセージを更新する場合に使用します。

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

このアクションは、ユーザーが通常のチャット メッセージに入力した場合と同様に、ボットへの戻りメッセージをトリガーします。 チャネル内のユーザーと他のすべてのユーザーには、そのボタンの応答が表示されます。

フィールド `value` には、チャットにエコーされたテキスト文字列が含まれている必要があります。そのため、ボットに送信されます。 これは、目的のロジックを実行するためにボットで処理するメッセージ テキストです。 注: このフィールドは単純な文字列です。書式設定や非表示文字のサポートはありません。

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>invoke

この `invoke` アクションは、タスク モジュールの呼び出 [しに使用されます](~/task-modules-and-cards/task-modules/task-modules-bots.md)。

アクション `invoke` には、次の 3 つのプロパティ `type` が `title` 含まれる。 `value` この `value` プロパティには、文字列、文字列化された JSON オブジェクト、または JSON オブジェクトを含めできます。

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

ユーザーがボタンをクリックすると、ボットは追加の情報を `value` 含むオブジェクトを受信します。 アクティビティの種類は ( ) の `invoke` 代わりに使用されます `message` `activity.Type == "invoke"` 。

### <a name="example-invoke-button-definition-net"></a>例: ボタン定義の呼び出し (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>例: 受信呼び出しメッセージ

Top-level `replyToId` プロパティには、カードアクションが送信されたメッセージの ID が含まれる。 メッセージを更新する場合に使用します。

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

OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。詳細については、ボットの認証フロー [を参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。

## <a name="adaptive-cards-actions"></a>アダプティブ カードのアクション

アダプティブ カードは、次の 3 種類のアクションをサポートします。

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)

上記のアクションに加えて、アダプティブ カード ペイロードを変更して、オブジェクトのプロパティを使用して既存の Bot Framework アクション `Action.Submit` `msteams` `data` をサポートできます `Action.Submit` 。 以下のセクションでは、アダプティブ カードで既存の Bot Framework アクションを使用する方法について詳しく説明します。

> [!NOTE]
> Bot Framework アクションを使用してデータに追加しても、アダプティブ カード タスク `msteams` モジュールでは機能しません。

### <a name="adaptive-cards-with-messageback-action"></a>messageBack アクションを含むアダプティブ カード

アダプティブ カードに `messageBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。 必要に応じて、オブジェクトに追加の非表示プロパティ `data` を含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定する `messageBack` |
| `displayText` | 省略可能。 アクションの実行時に、ユーザーがチャット ストリームにエコーします。 このテキストは *ボット* に送信されません。 |
| `value` | アクションの実行時にボットに送信されます。 アクションのコンテキスト (一意の識別子や JSON オブジェクトなど) をエンコードできます。 |
| `text` | アクションの実行時にボットに送信されます。 ボットの開発を簡略化するには、このプロパティを使用します。コードでは、ボット ロジックをディスパッチするために 1 つのトップ レベル プロパティをチェックできます。 |

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

### <a name="adaptive-cards-with-imback-action"></a>imBack アクションを使用したアダプティブ カード

アダプティブ カードに `imBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。 必要に応じて、オブジェクトに追加の非表示プロパティ `data` を含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定する `imBack` |
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

### <a name="adaptive-cards-with-signin-action"></a>Signin アクションを使用したアダプティブ カード

アダプティブ カードに `signin` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。 必要に応じて、オブジェクトに追加の非表示プロパティ `data` を含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定する `signin` |
| `value` | リダイレクト先の URL に設定する  |

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

### <a name="adaptive-cards-with-invoke-action"></a>アクションを呼び出すアダプティブ カード
 
アダプティブ カードに `invoke` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。 必要に応じて、オブジェクトに追加の非表示プロパティ `data` を含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定する `task/fetch` |
| `data` | 値を設定する  |

#### <a name="example"></a>例

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

#### <a name="example-2-with-additional-payload-data"></a>例 2 (追加のペイロード データを含む)

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    },
    "Value1": "some value"
  }
}
```
