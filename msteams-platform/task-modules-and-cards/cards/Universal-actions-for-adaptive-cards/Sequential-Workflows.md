---
title: シーケンシャル ワークフロー
description: ユニバーサル アクションを使用したシーケンシャル ワークフローのサンプル
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 7f285bf76aac4f0ca276321aee2ce4b4e5c3e7e4
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555403"
---
# <a name="sequential-workflows"></a>シーケンシャル ワークフロー

アダプティブ カードは、ユーザーの操作でアダプティブ カードが更新され、ユーザー入力が必要な一連のカードを通じて進めることができる順次ワークフローをサポートするようになりました。 これは、 を通じてサポート `Action.Execute` されており、ボット開発者はユーザーの操作に応じてアダプティブ カードを返すことができます。

たとえば、カフェテリアがチームやチャンネルの注文を受け取りたいシナリオを考えます。 `Action.Execute`食品、飲料など、さまざまなアイテムに対するユーザーの選択を順次記録することができます。 ユーザーは、ボット開発者によって定義されたロジックに従ってカードを行ったり来たりすることもできます。 <br/>

次の図は、シーケンシャル ワークフローを示しています。

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

ユーザーは、他のユーザーのカードを変更することなく、ワークフローを進めることができます。 これは、順次アダプティブカードを使用してクイズを行う場合にも便利です。 次の図に示すように、異なるユーザーはワークフローの異なる段階にあり、カードのさまざまな状態を表示します。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="ケータリングボットの状態":::

> [!NOTE]
> デバイス間でユーザーの進行状況を同期するには、 `refresh` アダプティブ カード JSON のプロパティを使用します。

## <a name="sequential-workflow-for-adaptive-cards"></a>アダプティブ カードのシーケンシャル ワークフロー

次のコードは、アダプティブ カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "body": [
    {
      "type": "TextBlock",
      "text": "Select from food options"
    },
    { 
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Execute",
          "title": "Chicken",
          "verb": "food",
          "data": {
              "item": "chicken"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Beef",
          "verb": "food",
          "data": {
              "item": "beef"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Vegan",
          "verb": "food",
          "data": {
              "item": "vegan"
          }
        }
      ]
    }
  ]
}
```

`Action.Execute`ボットを呼び出すと、アダプティブ カードを応答として返し、Teams内の既存のカードを置き換えることができます。
次の例では、ボットが飲食の選択または注文確認で返す内容を示します。

* カード1からの食品の選択では、ボットはカード2である飲み物の選択のためのカードを返すことができます。
* カード2からのドリンクの選択では、ボットはカード3である注文確認カードを返すことができます。
* カード3からの注文確認では、ボットはカード4である注文確認カードを返すことができます。

## <a name="invoke-request-received-on-bot-side"></a>ボット側で受信した呼び出し要求

次のコードは、ボット側で受信した呼び出し要求の例を示しています。

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "food",
      "data": { 
            "item": "vegan"
      } 
    },
    "trigger": "manual" 
  }
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

## <a name="see-also"></a>関連項目

* [Teamsでのアダプティブ カード アクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [ボットの機能](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
