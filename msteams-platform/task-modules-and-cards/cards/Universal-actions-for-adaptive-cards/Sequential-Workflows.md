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
# <a name="sequential-workflows"></a><span data-ttu-id="f0c4b-103">シーケンシャル ワークフロー</span><span class="sxs-lookup"><span data-stu-id="f0c4b-103">Sequential Workflows</span></span>

<span data-ttu-id="f0c4b-104">アダプティブ カードは、ユーザーの操作でアダプティブ カードが更新され、ユーザー入力が必要な一連のカードを通じて進めることができる順次ワークフローをサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-104">Adaptive Cards now support Sequential Workflows that is when Adaptive Cards are updated on user action and user can progress through a series of cards that require user input.</span></span> <span data-ttu-id="f0c4b-105">これは、 を通じてサポート `Action.Execute` されており、ボット開発者はユーザーの操作に応じてアダプティブ カードを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-105">This is supported through `Action.Execute`, which allows bot developers to return Adaptive Cards in response to a user action.</span></span>

<span data-ttu-id="f0c4b-106">たとえば、カフェテリアがチームやチャンネルの注文を受け取りたいシナリオを考えます。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-106">For example, take a scenario where the cafeteria wants to take an order for a team or channel.</span></span> <span data-ttu-id="f0c4b-107">`Action.Execute`食品、飲料など、さまざまなアイテムに対するユーザーの選択を順次記録することができます。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-107">With `Action.Execute` the user's choice for various items, such as food, drinks, and so on can be recorded sequentially.</span></span> <span data-ttu-id="f0c4b-108">ユーザーは、ボット開発者によって定義されたロジックに従ってカードを行ったり来たりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-108">User can also go back and forth through the cards as per the logic defined by the bot developer.</span></span> <br/>

<span data-ttu-id="f0c4b-109">次の図は、シーケンシャル ワークフローを示しています。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-109">The following image shows the Sequential Workflow:</span></span>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="f0c4b-110">ユーザーは、他のユーザーのカードを変更することなく、ワークフローを進めることができます。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-110">A user can progress through their workflow without modifying the card for other users.</span></span> <span data-ttu-id="f0c4b-111">これは、順次アダプティブカードを使用してクイズを行う場合にも便利です。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-111">This is also useful for conducting quizzes using sequential Adaptive Cards.</span></span> <span data-ttu-id="f0c4b-112">次の図に示すように、異なるユーザーはワークフローの異なる段階にあり、カードのさまざまな状態を表示します。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-112">As shown in the following image, different users can be at different stages of the workflow and they see different states of the card:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="ケータリングボットの状態":::

> [!NOTE]
> <span data-ttu-id="f0c4b-114">デバイス間でユーザーの進行状況を同期するには、 `refresh` アダプティブ カード JSON のプロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-114">In order to sync the user's progress across devices, use the `refresh` property in Adaptive Card JSON.</span></span>

## <a name="sequential-workflow-for-adaptive-cards"></a><span data-ttu-id="f0c4b-115">アダプティブ カードのシーケンシャル ワークフロー</span><span class="sxs-lookup"><span data-stu-id="f0c4b-115">Sequential Workflow for Adaptive Cards</span></span>

<span data-ttu-id="f0c4b-116">次のコードは、アダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-116">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="f0c4b-117">`Action.Execute`ボットを呼び出すと、アダプティブ カードを応答として返し、Teams内の既存のカードを置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-117">`Action.Execute` invoking the bot can return Adaptive Cards as a response, which replaces the existing card in Teams.</span></span>
<span data-ttu-id="f0c4b-118">次の例では、ボットが飲食の選択または注文確認で返す内容を示します。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-118">The following example provides what the bot returns on food or drink selection or order confirmation:</span></span>

* <span data-ttu-id="f0c4b-119">カード1からの食品の選択では、ボットはカード2である飲み物の選択のためのカードを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-119">On food selection from Card 1, bot can return a card for selection of drinks that is Card 2.</span></span>
* <span data-ttu-id="f0c4b-120">カード2からのドリンクの選択では、ボットはカード3である注文確認カードを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-120">On drink selection from Card 2, bot can return an order confirmation card that is Card 3.</span></span>
* <span data-ttu-id="f0c4b-121">カード3からの注文確認では、ボットはカード4である注文確認カードを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-121">On order confirmation from Card 3, bot can return an order confirmed card that is Card 4.</span></span>

## <a name="invoke-request-received-on-bot-side"></a><span data-ttu-id="f0c4b-122">ボット側で受信した呼び出し要求</span><span class="sxs-lookup"><span data-stu-id="f0c4b-122">Invoke request received on bot side</span></span>

<span data-ttu-id="f0c4b-123">次のコードは、ボット側で受信した呼び出し要求の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-123">The following code provides an example of an invoke request received on bot side:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="f0c4b-124">アダプティブ カードを返す応答を呼び出す</span><span class="sxs-lookup"><span data-stu-id="f0c4b-124">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="f0c4b-125">次のコードは、アダプティブ カードを返す呼び出し応答の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="f0c4b-125">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="f0c4b-126">関連項目</span><span class="sxs-lookup"><span data-stu-id="f0c4b-126">See also</span></span>

* [<span data-ttu-id="f0c4b-127">Teamsでのアダプティブ カード アクション</span><span class="sxs-lookup"><span data-stu-id="f0c4b-127">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="f0c4b-128">ボットの機能</span><span class="sxs-lookup"><span data-stu-id="f0c4b-128">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [<span data-ttu-id="f0c4b-129">アダプティブ カードのユニバーサル アクションの操作</span><span class="sxs-lookup"><span data-stu-id="f0c4b-129">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
