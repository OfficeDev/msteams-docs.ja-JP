---
title: ユーザー固有のビュー
description: ユニバーサル アクションとコード サンプルを使用したユーザー固有のビューの詳細
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: b2e5b8d6dd00104fab819ba7d05d5913bb891d83
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073681"
---
# <a name="user-specific-views"></a>ユーザー固有のビュー

以前、アダプティブ カードがTeams会話で送信された場合、すべてのユーザーにまったく同じカード コンテンツが表示されます。 ユニバーサル アクション モデルと `refresh` アダプティブ カードの導入により、ボット開発者はアダプティブ カードのユーザー固有のビューをユーザーに提供できるようになりました。 同じアダプティブ カードをユーザー固有のアダプティブ カードに更新できるようになりました。 最大 60 人の異なるユーザーが、追加情報やアクションを含む異なるバージョンのカードを表示できます。 アダプティブ カードは、承認、投票作成者コントロール、チケット発行、インシデント管理、プロジェクト管理カードなどの強力なシナリオを提供します。

> [!NOTE]
> ユーザー固有のビューは、ボットによって送信されるアダプティブ カードでサポートされ、ユニバーサル アクションに依存します。

たとえば、Contoso の安全検査員である Megan は、インシデントを作成し、それを Alex に割り当てたいと考えています。 また、Megan は、チーム内のすべてのユーザーにインシデントについて認識してもらいたいと考えています。 Megan では、アダプティブ カード用のユニバーサル アクションを搭載した Contoso インシデント レポート メッセージ拡張機能を使用します。

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="モバイル ユーザー固有のビュー" lightbox="../../../assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg":::

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="ユーザー固有のビュー" lightbox="../../../assets/images/adaptive-cards/universal-bots-incident-management.png":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a>アダプティブ カードのユーザー固有のビュー

次のコードは、アダプティブ カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView",
      "data": {
            "refresh info": "<refresh info>"
      }
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ]
}
```

アダプティブ カードを送信するには、ユーザー固有のビューを更新し、ボットに要求を呼び出します。

1. Megan が新しいインシデントを作成すると、ボットは、Teams会話にインシデントの詳細を含むアダプティブ カードまたは共通カードを送信します。
2. このカードは、Megan と Alex のユーザー固有のビューに自動的に更新されます。 Alex と Megan のユーザー MRI は、Adaptive Card JSON の`refresh`プロパティに追加`userIds`されます。 このカードは、会話内の他のユーザーと同じままです。
3. Megan の場合、自動更新によって `adaptiveCard/action` ボットへの呼び出し要求がトリガーされます。 ボットは、この呼び出し要求に対する応答として、ボタンを含む `Edit` インシデント作成者カードを返すことができます。
4. Alex の場合と同様に、自動更新によってボットに対する別 `adaptiveCard/action` の呼び出し要求がトリガーされます。 ボットは、この呼び出し要求に対する応答としてインシデント所有者カード `Resolve` ボタンを返すことができます。

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>クライアントからボットに送信された要求Teams呼び出す

次のコードは、Alex と Megan のTeams クライアントからボットに送信される呼び出し要求の例を示しています。

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "editOrResolveView",
      "data": { 
            "refresh info": "<refresh info>"
      } 
    },
    "trigger": "automatic" 
  }
}
```

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action invoke response card

次のコードは、Megan の adaptiveCard/action invoke 応答カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Edit",
      "verb": "edit",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>adaptiveCard/action invoke response card for Alex

次のコードは、Alex の adaptiveCard/action invoke 応答カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Resolve",
      "verb": "resolve",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a>アダプティブ カードを返す応答を呼び出す

次のコードは、アダプティブ カードを返す呼び出し応答の例を示しています。

### <a name="c"></a>[C#](#tab/C)

```csharp
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
var card = "<adaptive card json>";
 
const cardRes = {
        statusCode: 200,
        type: 'application/vnd.microsoft.card.adaptive',
        value: card
    };
    const res = {
        status: 200,
        body: cardRes
    };
    return res;

```

***

ユーザー固有のビューを設計するときに留意すべきカード設計ガイドライン:

* セクションで指定することで、チャットまたはチャネルに送信される特定のカードに対して最大 **60 個のユーザー固有** ビューを`userIds``refresh`作成できます。
* **ベース カード:** ボット開発者がチャットに送信するカードの基本バージョン。 基本バージョンは、セクションで指定されていないすべてのユーザーのアダプティブ カードの `userIds` バージョンです。
* メッセージの更新を使用して、ベース カードを更新し、同時にユーザー固有のカードを更新できます。 チャットまたはチャネルを開くと、更新が有効になっているユーザーのカードも更新されます。
* ユーザーがアクションのビューに切り替える大規模なグループを使用するシナリオでは、レスポンダーの動的な更新が必要な場合は、最大 60 人のユーザーを `userIds` リストに追加し続けることができます。 61 番目のユーザーが応答したときに、最初のレスポンダーをリストから削除できます。 リストから `userIds` 削除されたユーザーには、手動で更新ボタンを指定するか、メッセージ オプション メニューの [更新] ボタンを使用して最新の結果を取得できます。
* ユーザー固有のビューを取得するようにユーザーに求めるメッセージを表示します。このビューには、カードまたは一部のアクションの特定のビューのみが表示されます。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| シーケンシャル ワークフローアダプティブ カード | シーケンシャル ワークフロー、ユーザー固有のビュー、最新のアダプティブ カードをボットに実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
* [最新のビュー](Up-To-Date-Views.md)
* [フォームの完了に関するフィードバック](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
