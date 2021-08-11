---
title: ユーザー固有のビュー
description: ユニバーサル アクションを使用したユーザー固有のビューのサンプル
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 97d0aed313efebbdc55a1a6a96338f03a7d6f531359bfc198713bae4e006b3ef
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708665"
---
# <a name="user-specific-views"></a>ユーザー固有のビュー

以前、アダプティブ カードがスレッド内で送信Teams、すべてのユーザーにまったく同じカード コンテンツが表示されます。 ユニバーサル アクション モデルとアダプティブ カードの導入により、ボット開発者はアダプティブ カードのユーザー固有のビューをユーザーに `refresh` 提供できます。 同じアダプティブ カードをユーザー固有のアダプティブ カードに更新できます。 最大 60 人の異なるユーザーが、追加情報またはアクションを含む別のバージョンのカードを表示できます。 アダプティブ カードは、承認、投票作成者コントロール、チケット発行、インシデント管理、プロジェクト管理カードなど、強力なシナリオを提供します。

たとえば、Contoso の安全検査官である Megan は、インシデントを作成して Alex に割り当てる必要があります。 また、Megan は、チーム内のすべてのユーザーにインシデントを認識して欲しいと考えてもいます。 Megan は、アダプティブ カードのユニバーサル アクションを利用した Contoso インシデント レポート メッセージ拡張機能を使用します。

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="モバイル ユーザー固有のビュー":::

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="ユーザー固有のビュー":::

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

**アダプティブ カードを送信するには、ユーザー固有のビューを更新し、ボットに要求を呼び出します。**

1. Megan が新しいインシデントを作成すると、ボットはアダプティブ カードまたは共通カードにインシデントの詳細を送信Teamsします。
2. これで、このカードは、Megan と Alex のユーザー固有のビューに自動的に更新されます。 Alex と Megan のユーザー MRIs は、アダプティブ カード JSON のプロパティ `userIds` `refresh` のプロパティに追加されます。 カードは、会話内の他のユーザーに対して同じままです。
3. Megan の場合、自動更新によってボットへの `adaptiveCard/action` 呼び出し要求がトリガーされます。 ボットは、この呼び出し要求に対する応答として、ボタン付 `Edit` きインシデント作成者カードを返します。
4. Alex の場合と同様に、自動更新によってボットに対 `adaptiveCard/action` する別の呼び出し要求がトリガーされます。 ボットは、この呼び出し要求に対する応答として `Resolve` インシデント所有者カード ボタンを返します。

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>クライアントからボットにTeams要求を呼び出す

次のコードは、Alex と Megan のクライアントからボットに送信される呼び出しTeams例を示しています。

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

次のコードは、Megan のアダプティブ カード/アクション呼び出し応答カードの例を示しています。

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

次のコードは、Alex のアダプティブ カード/アクション呼び出し応答カードの例を示しています。

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

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

ユーザー固有のビューを設計する際に注意するカード設計ガイドライン:

* セクションで指定することで、チャットまたはチャネルに送信される特定のカードに対して最大 **60** のユーザー固有のビュー `userIds` を作成 `refresh` できます。
* **基本カード:** ボット開発者がチャットに送信するカードの基本バージョン。 基本バージョンは、セクションで指定されていないすべてのユーザーのアダプティブ カードのバージョン `userIds` です。
* メッセージの更新を使用して、基本カードを更新し、同時にユーザー固有のカードを更新できます。 チャットまたはチャネルを開く場合は、更新が有効になっているユーザーのカードも更新されます。
* ユーザーがアクションのビューに切り替える大規模なグループを持つシナリオでは、応答者の動的更新が必要です。最大 60 人のユーザーをリストに追加 `userIds` できます。 61st ユーザーが応答すると、最初のレスポンダーをリストから削除できます。 リストから削除されたユーザーの場合は、手動で更新ボタンを指定するか、メッセージ オプション メニューの更新ボタンを使用して最新の `userIds` 結果を取得できます。
* ユーザーに対して、カードの特定のビューまたは一部のアクションのみを表示するユーザー固有のビューを取得するように求めるメッセージを表示します。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| シーケンシャル ワークフローアダプティブ カード | シーケンシャル ワークフロー、ユーザー固有のビュー、最新のアダプティブ カードをボットに実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
* [最新のビュー](Up-To-Date-Views.md)
