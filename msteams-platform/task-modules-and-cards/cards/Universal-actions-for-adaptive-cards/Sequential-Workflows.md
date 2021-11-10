---
title: シーケンシャル ワークフロー
description: コード サンプルを使用したユニバーサル アクションを使用したアダプティブ カードのシーケンシャル ワークフローの詳細
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: e80f3d41e4dcbd281654c8070862fd5df9b0c128
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889112"
---
# <a name="sequential-workflows"></a>シーケンシャル ワークフロー

アダプティブ カードは、ユーザーの操作で更新されるシーケンシャル ワークフローをサポートします。 シーケンシャル ワークフローを使用すると、アダプティブ カードはユーザーの操作で更新され、ユーザーはユーザー入力を必要とする一連のカードを進めできます。 `Action.Execute` シーケンシャル ワークフローがサポートされています。これにより、ボット開発者はユーザーの操作に応じてアダプティブ カードを返す事が可能です。

たとえば、カフェテリアがチームまたはチャネルの注文を受け取るシナリオを考えます。 食べ物や飲み物など、さまざまなアイテムに対するユーザーの選択を順番 `Action.Execute` に記録できます。 また、ボット開発者が定義したロジックに基いて、カードを行き来できます。 <br/>

次の図は、シーケンシャル ワークフローを示しています。

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

ユーザーは、他のユーザーのカードを変更せずにワークフローを進めできます。 このワークフローは、シーケンシャル アダプティブ カードを使用してクイズを実行する場合にも役立ちます。 次の図は、異なるユーザーがワークフローの異なる段階とカードの状態を示しています。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="ケータリング ボットの状態":::

> [!NOTE]
> デバイス間でユーザーの進行状況を同期するには、アダプティブ カード `refresh` JSON のプロパティを使用します。

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

`Action.Execute`ボットを呼び出す場合、アダプティブ カードを応答として返す場合があります。この応答は、ボット内の既存のカードを置き換Teams。
次の例は、ボットが食品や飲み物の選択または注文確認で返す内容を示しています。

* カード 1 からのフードの選択では、ボットはカード 2 である飲み物の選択用のカードを返します。
* カード 2 からのドリンクの選択時に、ボットはカード 3 である注文確認カードを返します。
* カード 3 からの注文確認で、ボットはカード 4 である注文確認済みカードを返します。

## <a name="invoke-request-received-on-bot-side"></a>ボット側で受信した要求の呼び出し

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

## <a name="code-samples"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Teams ケータリング ボット | アダプティブ カードを使用して、食品の注文を受け入れるボットを作成します。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| まだ利用できません。 |
| シーケンシャル ワークフローアダプティブ カード | シーケンシャル ワークフロー、ユーザー固有のビュー、最新のアダプティブ カードをボットに実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |


## <a name="see-also"></a>関連項目

* [Teams でのアダプティブ カードのアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [ボットの機能](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
