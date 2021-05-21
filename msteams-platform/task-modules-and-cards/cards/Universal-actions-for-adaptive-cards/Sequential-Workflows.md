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
# <a name="sequential-workflows"></a><span data-ttu-id="80cd4-103">シーケンシャル ワークフロー</span><span class="sxs-lookup"><span data-stu-id="80cd4-103">Sequential Workflows</span></span>

<span data-ttu-id="80cd4-104">アダプティブ カードは、ユーザーの操作でアダプティブ カードが更新され、ユーザー入力が必要な一連のカードをユーザーが進行できるシーケンシャル ワークフローをサポートします。</span><span class="sxs-lookup"><span data-stu-id="80cd4-104">Adaptive Cards now support Sequential Workflows that is when Adaptive Cards are updated on user action and user can progress through a series of cards that require user input.</span></span> <span data-ttu-id="80cd4-105">これは、ボット開発者がユーザーの操作に応答してアダプティブ カードを返す `Action.Execute` 方法でサポートされます。</span><span class="sxs-lookup"><span data-stu-id="80cd4-105">This is supported through `Action.Execute`, which allows bot developers to return Adaptive Cards in response to a user action.</span></span>

<span data-ttu-id="80cd4-106">たとえば、カフェテリアがチームまたはチャネルの注文を受け取るシナリオを考えます。</span><span class="sxs-lookup"><span data-stu-id="80cd4-106">For example, take a scenario where the cafeteria wants to take an order for a team or channel.</span></span> <span data-ttu-id="80cd4-107">食べ物、飲み物など、さまざまなアイテムに対するユーザーの選択を順番に `Action.Execute` 記録できます。</span><span class="sxs-lookup"><span data-stu-id="80cd4-107">With `Action.Execute` the user's choice for various items, such as food, drinks, and so on can be recorded sequentially.</span></span> <span data-ttu-id="80cd4-108">また、ボット開発者が定義したロジックに基いて、カードを行き来できます。</span><span class="sxs-lookup"><span data-stu-id="80cd4-108">User can also go back and forth through the cards as per the logic defined by the bot developer.</span></span> <br/>

<span data-ttu-id="80cd4-109">次の図は、シーケンシャル ワークフローを示しています。</span><span class="sxs-lookup"><span data-stu-id="80cd4-109">The following image shows the Sequential Workflow:</span></span>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="80cd4-110">ユーザーは、他のユーザーのカードを変更せずにワークフローを進めできます。</span><span class="sxs-lookup"><span data-stu-id="80cd4-110">A user can progress through their workflow without modifying the card for other users.</span></span> <span data-ttu-id="80cd4-111">これは、シーケンシャル アダプティブ カードを使用してクイズを実行する場合にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="80cd4-111">This is also useful for conducting quizzes using sequential Adaptive Cards.</span></span> <span data-ttu-id="80cd4-112">次の図に示すように、ユーザーはワークフローの異なる段階にいて、カードの状態が異なります。</span><span class="sxs-lookup"><span data-stu-id="80cd4-112">As shown in the following image, different users can be at different stages of the workflow and they see different states of the card:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="ケータリング ボットの状態":::

> [!NOTE]
> <span data-ttu-id="80cd4-114">デバイス間でユーザーの進行状況を同期するには、アダプティブ カード `refresh` JSON のプロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="80cd4-114">In order to sync the user's progress across devices, use the `refresh` property in Adaptive Card JSON.</span></span>

## <a name="sequential-workflow-for-adaptive-cards"></a><span data-ttu-id="80cd4-115">アダプティブ カードのシーケンシャル ワークフロー</span><span class="sxs-lookup"><span data-stu-id="80cd4-115">Sequential Workflow for Adaptive Cards</span></span>

<span data-ttu-id="80cd4-116">次のコードは、アダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="80cd4-116">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="80cd4-117">`Action.Execute`ボットを呼び出す場合、アダプティブ カードを応答として返す場合があります。この応答は、ボット内の既存のカードを置き換Teams。</span><span class="sxs-lookup"><span data-stu-id="80cd4-117">`Action.Execute` invoking the bot can return Adaptive Cards as a response, which replaces the existing card in Teams.</span></span>
<span data-ttu-id="80cd4-118">次の例は、ボットが食品や飲み物の選択または注文確認で返す内容を示しています。</span><span class="sxs-lookup"><span data-stu-id="80cd4-118">The following example provides what the bot returns on food or drink selection or order confirmation:</span></span>

* <span data-ttu-id="80cd4-119">カード 1 からのフードの選択では、ボットはカード 2 である飲み物の選択用のカードを返します。</span><span class="sxs-lookup"><span data-stu-id="80cd4-119">On food selection from Card 1, bot can return a card for selection of drinks that is Card 2.</span></span>
* <span data-ttu-id="80cd4-120">カード 2 からのドリンクの選択時に、ボットはカード 3 である注文確認カードを返します。</span><span class="sxs-lookup"><span data-stu-id="80cd4-120">On drink selection from Card 2, bot can return an order confirmation card that is Card 3.</span></span>
* <span data-ttu-id="80cd4-121">カード 3 からの注文確認で、ボットはカード 4 である注文確認済みカードを返します。</span><span class="sxs-lookup"><span data-stu-id="80cd4-121">On order confirmation from Card 3, bot can return an order confirmed card that is Card 4.</span></span>

## <a name="invoke-request-received-on-bot-side"></a><span data-ttu-id="80cd4-122">ボット側で受信した要求の呼び出し</span><span class="sxs-lookup"><span data-stu-id="80cd4-122">Invoke request received on bot side</span></span>

<span data-ttu-id="80cd4-123">次のコードは、ボット側で受信した呼び出し要求の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="80cd4-123">The following code provides an example of an invoke request received on bot side:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="80cd4-124">アダプティブ カードを返す応答を呼び出す</span><span class="sxs-lookup"><span data-stu-id="80cd4-124">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="80cd4-125">次のコードは、アダプティブ カードを返す呼び出し応答の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="80cd4-125">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="80cd4-126">関連項目</span><span class="sxs-lookup"><span data-stu-id="80cd4-126">See also</span></span>

* [<span data-ttu-id="80cd4-127">アダプティブ カードのアクション (Teams</span><span class="sxs-lookup"><span data-stu-id="80cd4-127">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="80cd4-128">ボットの機能</span><span class="sxs-lookup"><span data-stu-id="80cd4-128">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [<span data-ttu-id="80cd4-129">アダプティブ カードのユニバーサル アクションの操作</span><span class="sxs-lookup"><span data-stu-id="80cd4-129">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
