---
title: シーケンシャル ワークフロー
description: このモジュールでは、ユニバーサル アクションとコード サンプルを使用したアダプティブ カードのシーケンシャル ワークフローについて説明します
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 40743ccd67386aae72685536ede1ae50d5aea907
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143313"
---
# <a name="sequential-workflows"></a>シーケンシャル ワークフロー

アダプティブ カードでは、ユーザー アクションで更新されるシーケンシャル ワークフローがサポートされるようになりました。 シーケンシャル ワークフローを使用すると、アダプティブ カードはユーザー アクションで更新され、ユーザーはユーザー入力を必要とする一連のカードを進めることができます。 `Action.Execute` はシーケンシャル ワークフローをサポートしています。これにより、ボット開発者はユーザー アクションに応答してアダプティブ カードを返すことができます。

たとえば、カフェテリアがチームまたはチャネルの注文を受けたいと考えるシナリオを考えてみます。 `Action.Execute`食べ物や飲み物など、さまざまな項目に対するユーザーの選択を順番に記録できます。 ユーザーは、ボット開発者によって定義されたロジックに従ってカードを行き来することもできます。 <br/>

次の図は、シーケンシャル ワークフローを示しています。

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

ユーザーは、他のユーザーのカードを変更することなく、ワークフローを進めることができます。 このワークフローは、シーケンシャルアダプティブ カードを使用してクイズを行う場合にも役立ちます。 次の図は、さまざまなユーザーがワークフローのさまざまな段階にあり、カードの状態を示しています。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="ケータリング ボットの状態" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

> [!NOTE]
> デバイス間でユーザーの進行状況を同期するには、Adaptive Card JSON のプロパティを `refresh` 使用します。

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

`Action.Execute`ボットを呼び出すと、応答としてアダプティブ カードを返すことができます。これは、Teams内の既存のカードを置き換えます。
次の例では、ボットが食べ物や飲み物の選択または注文の確認で返す内容を示します。

* カード 1 からの食品の選択では、ボットはカード 2 である飲み物の選択用のカードを返すことができます。
* カード 2 からの飲料の選択では、ボットはカード 3 である注文確認カードを返すことができます。
* カード 3 からの注文確認時に、ボットはカード 4 である注文確認済みカードを返すことができます。

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

## <a name="code-samples"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Teams ケータリング ボット | アダプティブ カードを使用して、料理の注文を受け付けるボットを作成します。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| まだ利用できません。 |
| シーケンシャル ワークフロー アダプティブ カード | シーケンシャル ワークフロー、ユーザー固有のビュー、最新のアダプティブ カードをボットに実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [Teams でのアダプティブ カードのアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [ボットの機能](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
* [フォームの完了に関するフィードバック](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
