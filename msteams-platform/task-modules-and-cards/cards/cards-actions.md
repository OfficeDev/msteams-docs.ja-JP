---
title: ボットにカード アクションを追加する
description: ボットでのカード アクションMicrosoft Teams、ボットでカードを使用する方法について説明します。
localization_priority: Normal
ms.topic: conceptual
keywords: teams ボット カードアクション
ms.openlocfilehash: 4af152f6179785687d4fd7371d202c56e1aee170
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254203"
---
# <a name="card-actions"></a>カード アクション

ボットとメッセージング拡張機能で使用されるカードは、Teamsアクティビティの種類をサポート [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) します。

> [!NOTE]
> コネクタ `CardAction` と使用する `potentialActions` 場合Office 365コネクタ カードのアクションは異なります。

| Type | Action |
| --- | --- |
| `openUrl` | 既定のブラウザーで URL を開きます。 |
| `messageBack` | ボタンを選択したユーザーまたはカードをタップしたユーザーから、ボットにメッセージとペイロードを送信します。 チャット ストリームに別のメッセージを送信します。 |
| `imBack`| ボタンを選択したユーザーまたはカードをタップしたユーザーからボットにメッセージを送信します。 ユーザーからボットへのこのメッセージは、すべての会話参加者に表示されます。 |
| `invoke` | ボタンを選択したユーザーまたはカードをタップしたユーザーから、ボットにメッセージとペイロードを送信します。 このメッセージは表示されません。 |
| `signin` | OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。 |

> [!NOTE]
>* Teams前の表 `CardAction` にリストされていない型はサポートされていません。
>* Teamsプロパティはサポート `potentialActions` されていません。
>* カードアクションは、Bot Framework [または](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) Azure Bot Service で推奨されるアクションとは異なります。 推奨されるアクションは、Microsoft Teams。 ボット メッセージにボタンを表示する場合Teamsカードを使用します。
>* メッセージング拡張機能の一部としてカード アクションを使用している場合、カードがチャネルに送信されるまでアクションは機能しません。 カードがメッセージの作成ボックスにある間、アクションは機能しません。

## <a name="action-type-openurl"></a>アクションの種類 openUrl

`openUrl` action type は、既定のブラウザーで起動する URL を指定します。

> [!NOTE]
> ボットは、どのボタンが選択されたのか通知を受け取らない。

を `openUrl` 使用すると、次のプロパティを使用してアクションを作成できます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタン ラベルとして表示されます。 |
| `value` | このフィールドには、完全で適切に形成された URL が含まれている必要があります。 |

# <a name="json"></a>[JSON](#tab/json)

次のコードは、JSON のアクション `openUrl` の種類の例を示しています。

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[C#](#tab/csharp)

次のコードは、アクションの種類の `openUrl` 例を示C#。

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

次のコードは `openUrl` 、JavaScript のアクションの種類の例を示しています。

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a>アクションの種類 messageBack

を `messageBack` 使用すると、次のプロパティを使用して完全にカスタマイズされたアクションを作成できます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタン ラベルとして表示されます。 |
| `displayText` | 省略可能です。 アクションの実行時にチャット ストリーム内のユーザーが使用します。 このテキストはボットに送信されません。 |
| `value` | アクションの実行時にボットに送信されます。 アクションのコンテキスト (一意の識別子や JSON オブジェクトなど) をエンコードできます。 |
| `text` | アクションの実行時にボットに送信されます。 ボットの開発を簡略化するには、このプロパティを使用します。 コードは、ボット ロジックをディスパッチするために、1 つのトップ レベル プロパティをチェックできます。 |

柔軟性は、コードが使用しないだけで、表示されるユーザー メッセージを履歴 `messageBack` に残せないという意味です `displayText` 。

# <a name="json"></a>[JSON](#tab/json)

次のコードは、JSON のアクション `messageBack` の種類の例を示しています。

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

# <a name="c"></a>[C#](#tab/csharp)

次のコードは、アクションの種類の `messageBack` 例を示C#。

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

次のコードは `messageBack` 、JavaScript のアクションの種類の例を示しています。

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

`replyToId` には、カード アクションが送信されたメッセージの ID が含まれる。 メッセージを更新する場合に使用します。

次のコードは、受信メッセージの例を示しています。

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

## <a name="action-type-imback"></a>アクションの種類 imBack

アクションは、ユーザーが通常のチャット メッセージに入力した場合と同様に、ボットへの戻り `imBack` メッセージをトリガーします。 ユーザーとチャネル内の他のすべてのユーザーは、ボタンの応答を確認できます。

を `imBack` 使用すると、次のプロパティを使用してアクションを作成できます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタン ラベルとして表示されます。 |
| `value` | このフィールドには、チャットで使用されるテキスト文字列が含まれている必要があります。そのため、ボットに返送されます。 これは、必要なロジックを実行するためにボットで処理するメッセージ テキストです。 |

> [!NOTE]
> フィールド `value` は単純な文字列です。 書式設定や非表示の文字はサポートされていません。

# <a name="json"></a>[JSON](#tab/json)

次のコードは、JSON のアクション `imBack` の種類の例を示しています。

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[C#](#tab/csharp)

次のコードは、アクションの種類の `imBack` 例を示C#。

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

次のコードは `imBack` 、JavaScript のアクションの種類の例を示しています。

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a>アクションの種類の呼び出し

この `invoke` アクションは、タスク モジュールの呼び出 [しに使用されます](~/task-modules-and-cards/task-modules/task-modules-bots.md)。

アクション `invoke` には、3 つのプロパティ `type` 、、 `title` およびが含まれる `value` 。

を `invoke` 使用すると、次のプロパティを使用してアクションを作成できます。

| プロパティ | 説明 |
| --- | --- |
| `title` | ボタン ラベルとして表示されます。 |
| `value` | このプロパティには、文字列、文字列化された JSON オブジェクト、または JSON オブジェクトを含めできます。 |

# <a name="json"></a>[JSON](#tab/json)

次のコードは、JSON のアクション `invoke` の種類の例を示しています。

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

ユーザーがボタンを選択すると、ボットは追加の情報 `value` を含むオブジェクトを受け取ります。

> [!NOTE]
> アクティビティの種類は `invoke` 、 の代 `message` わりにです `activity.Type == "invoke"` 。

# <a name="c"></a>[C#](#tab/csharp)

次のコードは、アクションの種類の `invoke` 例を示C#。

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

次のコードは、アクションの種類の例 `invoke` を示Node.js。

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

### <a name="example-of-incoming-invoke-message"></a>受信呼び出しメッセージの例

Top-level `replyToId` プロパティには、カードアクションが送信されたメッセージの ID が含まれる。 メッセージを更新する場合に使用します。

次のコードは、受信呼び出しメッセージの例を示しています。

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

## <a name="action-type-signin"></a>アクションの種類の signin

`signin` アクションの種類は、ボットがセキュリティで保護されたサービスに接続できる OAuth フローを開始します。 詳細については、「ボットの [認証フロー」を参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。

Teamsアダプティブ カード[でのみ使用されるアダプティブ](#adaptive-cards-actions)カード アクションもサポートしています。

# <a name="json"></a>[JSON](#tab/json)

次のコードは、JSON のアクション `signin` の種類の例を示しています。

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[C#](#tab/csharp)

次のコードは、アクションの種類の `signin` 例を示C#。

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

次のコードは `signin` 、JavaScript のアクションの種類の例を示しています。

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a>アダプティブ カードのアクション

アダプティブ カードは、次の 4 種類のアクションをサポートします。

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

アダプティブ カードペイロードを変更して、オブジェクトのプロパティを使用して既存の Bot Framework アクション `Action.Submit` `msteams` を `data` サポートすることができます `Action.Submit` 。 次のセクションでは、アダプティブ カードで既存の Bot Framework アクションを使用する方法の詳細について説明します。

> [!NOTE]
> `msteams`Bot Framework アクションを使用してデータに追加しても、アダプティブ カード タスク モジュールでは機能しません。

### <a name="adaptive-cards-with-messageback-action"></a>messageBack アクションを含むアダプティブ カード

アダプティブ カードに `messageBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。

> [!NOTE]
> 必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定します `messageBack` 。 |
| `displayText` | 省略可能です。 アクションの実行時にチャット ストリーム内のユーザーが使用します。 このテキストはボットに送信されません。 |
| `value` | アクションの実行時にボットに送信されます。 アクションのコンテキスト (一意の識別子や JSON オブジェクトなど) をエンコードできます。 |
| `text` | アクションの実行時にボットに送信されます。 ボットの開発を簡略化するには、このプロパティを使用します。 コードは、ボット ロジックをディスパッチするために、1 つのトップ レベル プロパティをチェックできます。 |

次のコードは、アクションを含むアダプティブ カードの例を示 `messageBack` しています。

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

アダプティブ カードで `imBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。

> [!NOTE]
> 必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定します `imBack` 。 |
| `value` | チャットでエコーバックする必要がある文字列。 |

次のコードは、アクションを含むアダプティブ カードの例を示 `imBack` しています。

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

アダプティブ カードに `signin` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。

> [!NOTE]
> 必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定します `signin` 。 |
| `value` | リダイレクトする URL に設定します。  |

次のコードは、アクションを含むアダプティブ カードの例を示 `signin` しています。

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

アダプティブ カードで `invoke` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。

> [!NOTE]
> 必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。

| プロパティ | 説明 |
| --- | --- |
| `type` | に設定します `task/fetch` 。 |
| `data` | 値を設定します。  |

次のコードは、アクションを含むアダプティブ カードの例を示 `invoke` しています。

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

次のコードは、追加のペイロード データを含むアクションを含むアダプティブ `invoke` カードの例を示しています。

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

## <a name="see-also"></a>関連項目

[カード リファレンス](./cards-reference.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アダプティブ カードのユニバーサル アクション](../cards/Universal-actions-for-adaptive-cards/Overview.md)
