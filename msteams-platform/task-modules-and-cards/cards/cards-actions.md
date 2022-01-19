---
title: ボットにカード アクションを追加する
description: Microsoft Teams のカード アクションと、ボットでの使用方法について説明します。
ms.localizationpriority: medium
ms.topic: conceptual
keywords: チーム ボット カード アクション
ms.openlocfilehash: 9add163801cee511ccc636ab3abbb95c35b26590
ms.sourcegitcommit: c65a868744e4108b5d786de2350981e3f1f05718
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/19/2022
ms.locfileid: "62081059"
---
# <a name="card-actions"></a>カード アクション

Teams のボットやメッセージング拡張機能で使用されるカードは、以下のアクティビティ [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) タイプをサポートします。

> [!NOTE]
> `CardAction` アクションは、コネクタから使用する場合、Office 365 コネクタ カード向けの `potentialActions` とは異なります。

| タイプ | 操作 |
| --- | --- |
| `openUrl` | URL を既定のブラウザーで開きます。 |
| `messageBack` | ボタンを選択するか、またはカードをタップしたユーザーからのメッセージおよびペイロードをボットに送信します。 別のメッセージをチャット ストリームに送信します。 |
| `imBack`| ボタンを選択するか、またはカードをタップしたユーザーからのメッセージをボットに送信します。 ユーザーからボットに送信されたこのメッセージは、すべての会話参加者に表示されます。 |
| `invoke` | ボタンを選択するか、またはカードをタップしたユーザーからのメッセージおよびペイロードをボットに送信します。 このメッセージは表示されません。 |
| `signin` | OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。 |

> [!NOTE]
>* Teams は、前のテーブルに記載されていない `CardAction` タイプをサポートしていません。
>* Teams は `potentialActions` プロパティをサポートしていません。
>* カード アクションは、Bot Framework や Azure Bot Service の[おすすめの操作](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true)とは異なります。 おすすめの操作は、Microsoft Teams ではサポートされていません。 Teams ボット メッセージにボタンを表示させる場合は、カードを使用します。
>* カード アクションをメッセージング拡張機能の一部として使用している場合、カードがチャネルに送信されるまでアクションは機能しません。 カードがメッセージの作成ボックスに入っている間は、アクションは機能しません。

## <a name="action-type-openurl"></a>アクション タイプ openUrl

`openUrl` アクション タイプでは、既定のブラウザーで起動する URL を指定します。

> [!NOTE]
> どのボタンが選択されたかの通知は、ボットでは受信しません。

`openUrl` を使用すると、以下のプロパティを含むアクションを作成することができます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタンのラベルとして表示されます。 |
| `value` | このフィールドには、完全でかつ適切に形成された URL が含まれる必要があります。 |

# <a name="json"></a>[JSON](#tab/json)

次のコードは JSON での `openUrl` アクション タイプの一例を示します。

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[C#](#tab/csharp)

次のコードは C# での `openUrl` アクション タイプの一例を示します。

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

次のコードは JavaScript での `openUrl` アクション タイプの一例を示します。

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a>アクション タイプ messageBack

`messageBack` を使用すると、以下のプロパティを含む完全にカスタマイズされたアクションを作成することができます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタンのラベルとして表示されます。 |
| `displayText` | 省略可能。 アクションが実行されたときに、チャット ストリームでユーザーが使用します。 このテキストは、お使いのボットには送信されません。 |
| `value` | アクションが実行された場合に、ボットに送信されます。 固有の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードすることができます。 |
| `text` | アクションが実行された場合に、ボットに送信されます。 このプロパティを使用して、ボット開発を簡略化します。 コードでは、トップレベルのプロパティをチェックして、ボット ロジックをディスパッチすることができます。 |

`messageBack` の柔軟性は、`displayText` を使用しないだけでは、コードが視覚的なユーザー メッセージを履歴に残すことができないことを意味します。

# <a name="json"></a>[JSON](#tab/json)

次のコードは JSON での `messageBack` アクション タイプの一例を示します。

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

`value` プロパティには、シリアル化された JSON 文字列または JSON オブジェクトを指定できます。

# <a name="c"></a>[C#](#tab/csharp)

次のコードは C# での `messageBack` アクション タイプの一例を示します。

```csharp
var button = new CardAction()
{
    Type = ActionTypes.MessageBack,
    Title = "My MessageBack button",
    DisplayText = "I clicked this button",
    Text = "User just clicked the MessageBack button",
    Value = "{\"property\": \"propertyValue\" }"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

次のコードは JavaScript での `messageBack` アクション タイプの一例を示します。

```javascript
CardFactory.actions([
{
    type: 'messageBack',
    title: "My MessageBack button",
    displayText: "I clicked this button",
    text: "User just clicked the MessageBack button",
    value: {property: "propertyValue" }
}])
```

---

### <a name="inbound-message-example"></a>受信メッセージの例

`replyToId` には、カード アクションの発信元であるメッセージ ID が含まれます。 これは、メッセージを更新する場合に使用します。

以下のコードは、受信メッセージの一例を示しています。

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

## <a name="action-type-imback"></a>アクション タイプ imBack

`imBack` アクションは、ユーザーが通常のチャット メッセージで入力した場合のように、ボットへの返信メッセージをトリガーします。 ユーザーおよびチャネル内の他のすべてのユーザーがボタンの応答を確認することができます。

`imBack` を使用すると、以下のプロパティを含むアクションを作成することができます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタンのラベルとして表示されます。 |
| `value` | このフィールドには、チャットで使用されるテキスト文字列が含まれている必要があるため、ボットに送り返されます。 これは、ボットで目的のロジックを実行するために処理するメッセージ テキストです。 |

> [!NOTE]
> `value` フィールドはシンプルな文字列です。 書式設定や隠し文字のサポートはありません。

# <a name="json"></a>[JSON](#tab/json)

次のコードは JSON での `imBack` アクション タイプの一例を示します。

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[C#](#tab/csharp)

次のコードは C# での `imBack` アクション タイプの一例を示します。

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

次のコードは JavaScript での `imBack` アクション タイプの一例を示します。

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a>アクション タイプ invoke

`invoke` アクションは、[タスク モジュール](~/task-modules-and-cards/task-modules/task-modules-bots.md)を起動するために使用されます。

`invoke` アクションには、`type`、`title`、`value` の 3 つのプロパティが含まれています。

`invoke` を使用すると、以下のプロパティを含むアクションを作成することができます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタンのラベルとして表示されます。 |
| `value` | このプロパティには、文字列、文字列化された JSON オブジェクト、または JSON オブジェクトを含めることができます。 |

# <a name="json"></a>[JSON](#tab/json)

次のコードは JSON での `invoke` アクション タイプの一例を示します。

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

ユーザーがボタンを選択した場合、ボットはいくつかの追加情報を含む `value` オブジェクトを受け取ります。

> [!NOTE]
> アクティビティ タイプは、`activity.Type == "invoke"` である `message` の代わりに `invoke` です。

# <a name="c"></a>[C#](#tab/csharp)

次のコードは C# での `invoke` アクション タイプの一例を示します。

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

次のコードは Node.js での `invoke` アクション タイプの一例を示します。

```javascript
CardFactory.actions([
{
    type: "invoke",
    title: "Option 1",
    value: {
        option: "opt1"
    }
}])
```

---

### <a name="example-of-incoming-invoke-message"></a>受信した起動メッセージの例

上位の `replyToId` プロパティには、カード アクションの発信元であるメッセージ ID が含まれます。 これは、メッセージを更新する場合に使用します。

以下のコードは、受信する起動メッセージの一例を示しています。

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

## <a name="action-type-signin"></a>アクション タイプ signin

`signin`アクション タイプは、ボットがセキュリティで保護されたサービスに接続することを許可する OAuth フローを開始します。 詳細については、「[ボットでの認証フロー](~/bots/how-to/authentication/auth-flow-bot.md)」を参照してください。

また、Teams は、アダプティブ カードでのみ使用される[アダプティブ カード アクション](#adaptive-cards-actions)をサポートしています。

# <a name="json"></a>[JSON](#tab/json)

次のコードは JSON での `signin` アクション タイプの一例を示します。

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[C#](#tab/csharp)

次のコードは C# での `signin` アクション タイプの一例を示します。

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

次のコードは JavaScript での `signin` アクション タイプの一例を示します。

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a>アダプティブ カード アクション

アダプティブ カードは、次の 4 つのアクション タイプをサポートします。

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

アダプティブ カード `Action.Submit`のペイロードを変更して、`Action.Submit` の `data` オブジェクトで `msteams` プロパティを使用して、既存の Bot Framework アクションをサポートすることもできます。 次のセクションでは、既存の Bot Framework アクションをアダプティブ カードで使用する方法について詳しく説明します。

> [!NOTE]
> Bot Framework アクションを含むデータに `msteams` を追加しても、アダプティブ カード タスク モジュールでは動作しません。

### <a name="adaptive-cards-with-messageback-action"></a>messageBack アクションを備えたアダプティブ カード

`msteams` オブジェクトに次の詳細を含むアダプティブ カードに `messageBack` アクションを含めるには、以下の操作を行います。

> [!NOTE]
> 必要に応じて、`data` オブジェクトに追加の隠しプロパティを含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | `messageBack` に設定します。 |
| `displayText` | 省略可能。 アクションが実行されたときに、チャット ストリームでユーザーが使用します。 このテキストは、お使いのボットには送信されません。 |
| `value` | アクションが実行された場合に、ボットに送信されます。 固有の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードすることができます。 |
| `text` | アクションが実行された場合に、ボットに送信されます。 このプロパティを使用して、ボット開発を簡略化します。 コードでは、トップレベルのプロパティをチェックして、ボット ロジックをディスパッチすることができます。 |

次のコードは `messageBack` アクションを備えたアダプティブ カードの一例を示します。

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

### <a name="adaptive-cards-with-imback-action"></a>imBack アクションを備えたアダプティブ カード

`msteams` オブジェクトに次の詳細を含むアダプティブ カードに `imBack` アクションを含めるには、以下の操作を行います。

> [!NOTE]
> 必要に応じて、`data` オブジェクトに追加の隠しプロパティを含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | `imBack` に設定します。 |
| `value` | チャットでエコー バックされる必要のある文字列。 |

次のコードは `imBack` アクションを備えたアダプティブ カードの一例を示します。

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

### <a name="adaptive-cards-with-signin-action"></a>signin アクションを備えたアダプティブ カード

`msteams` オブジェクトに次の詳細を含むアダプティブ カードに `signin` アクションを含めるには、以下の操作を行います。

> [!NOTE]
> 必要に応じて、`data` オブジェクトに追加の隠しプロパティを含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | `signin` に設定します。 |
| `value` | リダイレクトさせる URL に設定します。  |

次のコードは `signin` アクションを備えたアダプティブ カードの一例を示します。

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

### <a name="adaptive-cards-with-invoke-action"></a>invoke アクションを備えたアダプティブ カード

`msteams` オブジェクトに次の詳細を含むアダプティブ カードに `invoke` アクションを含めるには、以下の操作を行います。

> [!NOTE]
> 必要に応じて、`data` オブジェクトに追加の隠しプロパティを含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | `task/fetch` に設定します。 |
| `data` | 値を設定します。  |

次のコードは `invoke` アクションを備えたアダプティブ カードの一例を示します。

```json
{
  "type": "Action.Submit",
  "title": "submit",
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

次のコードは、追加のペイロードデータを含む `invoke` アクションを備えたアダプティブ カードの一例を示します。

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
## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アダプティブ カードのユニバーサル アクション](../cards/Universal-actions-for-adaptive-cards/Overview.md)

## <a name="see-also"></a>関連項目

* [カード リファレンス](./cards-reference.md)
* [ボットでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [ボットのアダプティブ カード](../../bots/how-to/conversations/conversation-messages.md#adaptive-cards)
* [アダプティブ カードのユニバーサル アクション](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md)
* [フォームの完成に関するフィードバック](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)