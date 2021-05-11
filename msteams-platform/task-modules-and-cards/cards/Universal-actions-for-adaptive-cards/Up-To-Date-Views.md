---
title: 最新のビュー
description: ユニバーサル ボットを使用した最新のビューのサンプル
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 2027d07961929fb40e7afc3ee268e1267b235a02
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088889"
---
# <a name="up-to-date-cards"></a><span data-ttu-id="a420b-103">最新のカード</span><span class="sxs-lookup"><span data-stu-id="a420b-103">Up to date cards</span></span>

<span data-ttu-id="a420b-104">アダプティブ カードでは、更新とメッセージの編集を組み合わせて、ユーザーに最新の情報を提供Teams。</span><span class="sxs-lookup"><span data-stu-id="a420b-104">You can now provide latest information to your users on Adaptive Cards with a combination of refresh and message edits in Teams.</span></span> <span data-ttu-id="a420b-105">これにより、サービスに変更がある場合と同様に、ユーザー固有のビューを動的に最新の状態に更新できます。</span><span class="sxs-lookup"><span data-stu-id="a420b-105">With this you are able to update the User Specific Views dynamically to its latest state as and when there is a change on your service.</span></span> <span data-ttu-id="a420b-106">たとえば、プロジェクト管理カードまたはチケット カードの場合は、コメントとタスクの状態を更新できます。</span><span class="sxs-lookup"><span data-stu-id="a420b-106">For example, in the case of project management or ticketing cards, you can update comments and the status of the task.</span></span> <span data-ttu-id="a420b-107">承認の場合、最新の状態が反映され、差別化された情報とアクションも提供されます。</span><span class="sxs-lookup"><span data-stu-id="a420b-107">In case of approvals the latest state is reflected while also providing differentiated information and actions.</span></span>

<span data-ttu-id="a420b-108">たとえば、ユーザーは、スレッド内にアセット承認要求をTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="a420b-108">For example, a user can create an asset approval request in a Teams conversation.</span></span> <span data-ttu-id="a420b-109">Alex は承認要求を作成し、それを Megan と Nestor に割り当てる。</span><span class="sxs-lookup"><span data-stu-id="a420b-109">Alex creates an approval request and assigns it to Megan and Nestor.</span></span> <span data-ttu-id="a420b-110">承認要求を作成する 2 つの部分を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a420b-110">The following are the two parts to create the approval request:</span></span>

* <span data-ttu-id="a420b-111">アダプティブ カードのプロパティを使用して、ユーザー `refresh` 固有のビューを利用できます。</span><span class="sxs-lookup"><span data-stu-id="a420b-111">User Specific Views can be leveraged using the `refresh` property of the Adaptive Cards.</span></span>
<span data-ttu-id="a420b-112">ユーザー固有のビューを使用すると、一連のユーザーに [承認] または [拒否] ボタンを含むカードを表示し、他のユーザーにこれらのボタンのないカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="a420b-112">Using User Specific Views one can show a card with **Approve** or **Reject** buttons to a set of users, and show a card without these buttons to other users.</span></span>

* <span data-ttu-id="a420b-113">カードの状態を常に更新するために、Teams編集メカニズムを利用できます。</span><span class="sxs-lookup"><span data-stu-id="a420b-113">To keep the card state updated at all times, Teams message edit mechanism can be leveraged.</span></span> <span data-ttu-id="a420b-114">たとえば、承認が行うごとに、ボットはすべてのユーザーに対してメッセージ編集をトリガーできます。</span><span class="sxs-lookup"><span data-stu-id="a420b-114">For example, each time there is an approval, bot can trigger a message edit to all users.</span></span> <span data-ttu-id="a420b-115">このボット メッセージの編集は、更新されたユーザー固有のカードでボットが応答できる、すべての自動更新ユーザーに対する呼び出し `adaptiveCard/action` 要求をトリガーします。</span><span class="sxs-lookup"><span data-stu-id="a420b-115">This bot message edit triggers an `adaptiveCard/action` invoke request for all automatic refresh users, to which the bot can respond with the updated user specific card.</span></span>

<span data-ttu-id="a420b-116">詳細については、「ボット メッセージの [編集方法」を参照してください](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)。</span><span class="sxs-lookup"><span data-stu-id="a420b-116">For more information, see [how to do a bot message edit](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).</span></span>

## <a name="approval-base-card"></a><span data-ttu-id="a420b-117">承認ベース カード</span><span class="sxs-lookup"><span data-stu-id="a420b-117">Approval base card</span></span>

<span data-ttu-id="a420b-118">次のコードは、承認ベース カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="a420b-118">The following code provides an example of an approval base card:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>", "<Nestor's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ]
}
```

## <a name="approval-card-with-approve-and-reject-buttons"></a><span data-ttu-id="a420b-119">[承認] ボタンと [拒否] ボタンを含む承認カード</span><span class="sxs-lookup"><span data-stu-id="a420b-119">Approval card with Approve and Reject buttons</span></span>

<span data-ttu-id="a420b-120">次のコードは、[承認] ボタンと [拒否] ボタンを含 **む承認** カード **の例を** 示しています。</span><span class="sxs-lookup"><span data-stu-id="a420b-120">The following code provides an example of an approval card with **Approve** and **Reject** buttons:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Nestor's user MRI>", "<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

<span data-ttu-id="a420b-121">承認要求への関与に応じて、ユーザーに表示される 2 つの役割を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a420b-121">Following are the two roles that are shown to users depending on their involvement in the approval request:</span></span>

* <span data-ttu-id="a420b-122">承認ベース カード: 承認者リストの一部ではなく、まだ要求を承認または拒否していないユーザーに表示され、アダプティブ カード JSON のプロパティのリストの一部ではありません `userIds` `refresh` 。</span><span class="sxs-lookup"><span data-stu-id="a420b-122">Approval base card: Shown to users who are not part of approvers list and have not yet approved or rejected the request, and are not part of `userIds` list in `refresh` property of the Adaptive Card JSON.</span></span>
* <span data-ttu-id="a420b-123">[承認] または **[** 拒否] ボタンを持つ承認カード: 承認者リストの一部であるユーザーとアダプティブ カード JSON のプロパティの一覧 `userIds` `refresh` に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a420b-123">Approval card with **Approve** or **Reject** buttons: Shown to the users who are part of the approvers list and the `userIds` list in the `refresh` property of the Adaptive Card JSON.</span></span>

<span data-ttu-id="a420b-124">**資産承認要求を送信するには**</span><span class="sxs-lookup"><span data-stu-id="a420b-124">**To send the asset approval request**</span></span>

1. <span data-ttu-id="a420b-125">Alex は、スレッド内で資産承認要求をTeamsし、それを Megan と Nestor に割り当てる。</span><span class="sxs-lookup"><span data-stu-id="a420b-125">Alex raises an asset approval request in a Teams conversation and assigns it to Megan and Nestor.</span></span>
2. <span data-ttu-id="a420b-126">ボットは、会話で承認ベース カードを送信します。</span><span class="sxs-lookup"><span data-stu-id="a420b-126">Bot sends the approval base card in the conversation.</span></span>
3. <span data-ttu-id="a420b-127">会話内の他のすべてのユーザーには、ボットから送信されたカードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a420b-127">All other users in the conversation see the card sent by the bot.</span></span> <span data-ttu-id="a420b-128">Megan と Nestor で自動更新がトリガーされ、アダプティブ カードのプロパティの一覧にユーザーの MRIs が追加されると、[承認] ボタンまたは [拒否] ボタンが表示されるユーザー固有のカードが表示されます。 `userIds` `refresh`</span><span class="sxs-lookup"><span data-stu-id="a420b-128">Automatic refresh is triggered for Megan and Nestor, who now see the user specific card with **Approve** or **Reject** buttons as their user MRIs are added to the `userIds` list in the `refresh` property of the Adaptive Card.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="ユーザー固有のビュー":::

4. <span data-ttu-id="a420b-130">Nestor は、電源が **入った [承認** ] ボタンを選択します `Action.Execute` 。</span><span class="sxs-lookup"><span data-stu-id="a420b-130">Nestor selects the **Approve** button which is powered with `Action.Execute`.</span></span> <span data-ttu-id="a420b-131">ボットは、応答 `adaptiveCard/action` でアダプティブ カードを返す呼び出し要求を取得します。</span><span class="sxs-lookup"><span data-stu-id="a420b-131">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
5. <span data-ttu-id="a420b-132">ボットは、Megan の承認が保留されている間に Nestor が要求を承認したという更新されたカードでメッセージ編集をトリガーします。</span><span class="sxs-lookup"><span data-stu-id="a420b-132">The bot triggers a message edit with an updated card which says Nestor has approved the request while Megan's approval is pending.</span></span>
6. <span data-ttu-id="a420b-133">ボット メッセージの編集では、Megan の自動更新がトリガーされ、更新されたユーザー固有のカードが表示され、Nestor は要求を承認しましたが、[承認]または[拒否] ボタンも表示されます。</span><span class="sxs-lookup"><span data-stu-id="a420b-133">Bot message edit triggers an automatic refresh for Megan and she sees the updated user specific card, which says Nestor has approved the request, but also sees the **Approve** or **Reject** buttons.</span></span> <span data-ttu-id="a420b-134">Nestor のユーザーの MRI は、手順 4 と 5 のこのアダプティブ カード JSON のプロパティのリストから `userIds` `refresh` 削除されます。</span><span class="sxs-lookup"><span data-stu-id="a420b-134">Nestor's user MRI is removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 4 and 5.</span></span> <span data-ttu-id="a420b-135">これで、自動更新は Megan でのみトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="a420b-135">Now, automatic refresh is only triggered for Megan.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="最新のユーザー固有のビュー":::

7. <span data-ttu-id="a420b-137">これで、Megan は [承認] **ボタンを選択** します。このボタンの電源 `Action.Execute` は .</span><span class="sxs-lookup"><span data-stu-id="a420b-137">Now, Megan selects the **Approve** button, which is powered with `Action.Execute`.</span></span> <span data-ttu-id="a420b-138">ボットは、応答 `adaptiveCard/action` でアダプティブ カードを返す呼び出し要求を取得します。</span><span class="sxs-lookup"><span data-stu-id="a420b-138">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
8. <span data-ttu-id="a420b-139">ボットは、更新されたカードを使用してメッセージ編集をトリガーします。このカードでは、Nestor と Megan が要求を承認しました。</span><span class="sxs-lookup"><span data-stu-id="a420b-139">The bot triggers a message edit with an updated card, which says Nestor and Megan have approved the request.</span></span>
9. <span data-ttu-id="a420b-140">ボット メッセージの編集では、自動更新はトリガーされません。</span><span class="sxs-lookup"><span data-stu-id="a420b-140">Bot message edit does not trigger any automatic refresh.</span></span> <span data-ttu-id="a420b-141">Megan のユーザーの MRI は、手順 7 と 8 のこのアダプティブ カード JSON のプロパティのリストから `userIds` `refresh` 削除されます。</span><span class="sxs-lookup"><span data-stu-id="a420b-141">Megan's user MRI is also removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 7 and 8.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="最新のビュー":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a><span data-ttu-id="a420b-143">アダプティブ カードの応答として送信 `adaptiveCard/action` され、 `message edit`</span><span class="sxs-lookup"><span data-stu-id="a420b-143">Adaptive Card sent as response of `adaptiveCard/action` and `message edit`</span></span>

<span data-ttu-id="a420b-144">次のコードは、手順 4 と 5 の応答として送信されるアダプティブ カードの `adaptiveCard/action` `message edit` 例を示しています。</span><span class="sxs-lookup"><span data-stu-id="a420b-144">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 4 and 5:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ]
}
```

<span data-ttu-id="a420b-145">次のコードは、手順 6 の自動更新を介して呼び出しの応答として送信されるアダプティブ `adaptiveCard/action` カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="a420b-145">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` invoke through automatic refresh for step 6:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

<span data-ttu-id="a420b-146">次のコードは、手順 7 と 8 の応答として送信されるアダプティブ `adaptiveCard/action` `message edit` カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="a420b-146">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 7 and 8:</span></span>

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": []
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor and Megan**"
    }
  ]
}
```

## <a name="see-also"></a><span data-ttu-id="a420b-147">関連項目</span><span class="sxs-lookup"><span data-stu-id="a420b-147">See also</span></span>

* [<span data-ttu-id="a420b-148">アダプティブ カードのユニバーサル アクションの操作</span><span class="sxs-lookup"><span data-stu-id="a420b-148">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="a420b-149">ユーザー固有のビュー</span><span class="sxs-lookup"><span data-stu-id="a420b-149">User Specific Views</span></span>](User-Specific-Views.md)
