---
title: ボットにカードアクションを追加する
description: Microsoft Teamsでのカード アクションと、ボットでのカード アクションの使用方法について説明します。
localization_priority: Normal
ms.topic: conceptual
keywords: チームボットカードアクション
ms.openlocfilehash: b9276c7197070df43ba447707e6fa4d3d4098591
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566853"
---
# <a name="card-actions"></a>カードアクション

Teamsでボットやメッセージング拡張機能で使用されるカードは、次のアクティビティ ( [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ) タイプをサポートします。 コネクタから使用する場合、これらのアクションはOffice 365 コネクタ カードとは異なります `potentialActions` 。

| 型 | Action |
| --- | --- |
| `openUrl` | 既定のブラウザーで URL を開きます。 |
| `messageBack` | ボタンをクリックしたユーザーまたはカードをタップしたユーザーからボットにメッセージとペイロードを送信し、チャット ストリームに別のメッセージを送信します。 |
| `imBack`| ボタンをクリックしたユーザーまたはカードをタップしたユーザーからボットにメッセージを送信します。 このメッセージ (ユーザーからボットへ) は、すべての会話参加者に表示されます。 |
| `invoke` | ボタンをクリックしたユーザーまたはカードをタップしたユーザーから、ボットにメッセージとペイロードを送信します。 このメッセージは表示されません。 |
| `signin` | OAuth フローを開始し、ボットが安全なサービスと接続できるようにします。 |

> [!NOTE]
>* Teamsは、 `CardAction` 前の表に示されていない型をサポートしていません。
>* Teams `potentialActions` は、プロパティをサポートしていません。
>* カード アクションは、ボット フレームワーク/Azure Bot サービスで [推奨されるアクション](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) とは異なります。 Microsoft Teamsでは推奨されるアクションはサポートされていません: Teamsのボット メッセージにボタンを表示する場合は、カードを使用します。
>* カードアクションをメッセージング拡張機能の一部として使用している場合、カードがチャネルに送信されるまでアクションは機能しません。 カードが作成メッセージ ボックスにある間は機能しません。

Teamsは[、アダプティブ カードでのみ使用されるアダプティブ カード アクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)もサポートしています。 これらのアクションは、このリファレンスの最後にある独自のセクションにリストされています。

## <a name="openurl"></a>openUrl

このアクションタイプは、デフォルトのブラウザで起動するURLを指定します。 ボットはどのボタンがクリックされたか通知を受け取りません。

`value`フィールドには、完全で正しい形式の URL が含まれている必要があります。

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>メッセージバック

`messageBack`では、次のプロパティを使用して、完全にカスタマイズされたアクションを作成できます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタンラベルとして表示されます。 |
| `displayText` | 省略可能。 アクションが実行されると、ユーザーがチャット ストリームにエコーされます。 このテキストはボットに送信 *されません* 。 |
| `value` | アクションが実行されたときにボットに送信されます。 一意の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードできます。 |
| `text` | アクションが実行されたときにボットに送信されます。 このプロパティを使用してボット開発を簡略化する: コードでは、ボット ロジックをディスパッチする 1 つの最上位プロパティをチェックできます。 |

柔軟性 `messageBack` のあるコードでは、単に を使用しないことで、表示可能なユーザー メッセージを履歴に残さないことを選択できます `displayText` 。

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

`value`このプロパティには、シリアル化された JSON 文字列または JSON オブジェクトを指定できます。

### <a name="inbound-message-example"></a>受信メッセージの例

`replyToId` には、カード アクションの送信元のメッセージの ID が含まれています。 メッセージを更新する場合に使用します。

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

## <a name="imback"></a>イムバック

このアクションは、ユーザーが通常のチャット メッセージに入力した場合と同様に、ボットに返すメッセージをトリガーします。 ユーザー、およびチャネル内の他のすべてのユーザーには、そのボタンの応答が表示されます。

`value`フィールドには、チャットにエコーされるテキスト文字列を含める必要があります。 これは、必要なロジックを実行するためにボットで処理するメッセージ テキストです。 注: このフィールドは単純な文字列で、フォーマットや隠し文字はサポートされていません。

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>呼び出す

`invoke`このアクションは[、タスク モジュール](~/task-modules-and-cards/task-modules/task-modules-bots.md)の呼び出しに使用されます。

`invoke`このアクションには、 、 の 3 つのプロパティが含まれます `type` `title` `value` 。 `value`プロパティには、文字列、文字列化された JSON オブジェクト、または JSON オブジェクトを含めることができます。

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

ユーザーがボタンをクリックすると、ボットはオブジェクトを受け取り `value` 、追加情報が表示されます。 アクティビティの種類は( ) `invoke` ではなく、アクティビティタイプになります `message` `activity.Type == "invoke"` 。

### <a name="example-invoke-button-definition-net"></a>例: 呼び出しボタン定義 (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>例: 着信呼び出しメッセージ

最上位の `replyToId` プロパティには、カード アクションの送信元のメッセージの ID が含まれます。 メッセージを更新する場合に使用します。

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

## <a name="signin"></a>サインイン

OAuth フローを開始し、ボットが安全なサービスと接続[できるようにします。](~/bots/how-to/authentication/auth-flow-bot.md)

## <a name="adaptive-cards-actions"></a>アダプティブ カード アクション

アダプティブ カードは、次の 4 つのアクション タイプをサポートします。

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [アクション.ショーカード](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Exeかわいい](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

上記のアクションに加えて、アダプティブ カード `Action.Submit` ペイロードを変更して、 `msteams` のオブジェクトのプロパティを使用して既存の Bot Framework アクションをサポートできます `data` `Action.Submit` 。 以下のセクションでは、アダプティブ カードで既存の Bot Framework アクションを使用する方法について詳しく説明します。

> [!NOTE]
> `msteams`Bot Framework アクションを使用してデータに追加すると、アダプティブ カード タスク モジュールでは機能しません。

### <a name="adaptive-cards-with-messageback-action"></a>メッセージバック アクションを含むアダプティブ カード

`messageBack`アダプティブ カードにアクションを含めるには、オブジェクトに次の詳細が含 `msteams` まれます。 必要に応じて、オブジェクトに追加の非表示プロパティを含めることができます `data` 。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定 `messageBack` |
| `displayText` | 省略可能。 アクションが実行されると、ユーザーがチャット ストリームにエコーされます。 このテキストはボットに送信 *されません* 。 |
| `value` | アクションが実行されたときにボットに送信されます。 一意の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードできます。 |
| `text` | アクションが実行されたときにボットに送信されます。 このプロパティを使用してボット開発を簡略化する: コードでは、ボット ロジックをディスパッチする 1 つの最上位プロパティをチェックできます。 |

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

`imBack`アダプティブ カードにアクションを含めるには、オブジェクトに次の詳細が含 `msteams` まれます。 必要に応じて、オブジェクトに追加の非表示プロパティを含めることができます `data` 。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定 `imBack` |
| `value` | チャットにエコーバックする必要がある文字列 |

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

### <a name="adaptive-cards-with-signin-action"></a>サインインアクションを持つアダプティブカード

`signin`アダプティブ カードにアクションを含めるには、オブジェクトに次の詳細が含 `msteams` まれます。 必要に応じて、オブジェクトに追加の非表示プロパティを含めることができます `data` 。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定 `signin` します。 |
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

### <a name="adaptive-cards-with-invoke-action"></a>呼び出しアクションを持つアダプティブ カード
 
`invoke`アダプティブ カードにアクションを含めるには、オブジェクトに次の詳細が含 `msteams` まれます。 必要に応じて、オブジェクトに追加の非表示プロパティを含めることができます `data` 。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定 `task/fetch` |
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
