---
title: ユーザー固有のビュー
description: ユニバーサル アクションを使用したユーザー固有のビューのサンプル
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: c24697b300d07ed53a172df162d0d3851361f579
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853516"
---
# <a name="user-specific-views"></a><span data-ttu-id="42e50-103">ユーザー固有のビュー</span><span class="sxs-lookup"><span data-stu-id="42e50-103">User Specific Views</span></span>

<span data-ttu-id="42e50-104">以前は、アダプティブ カードがスレッド内で送信Teams、すべてのユーザーにまったく同じカード コンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="42e50-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="42e50-105">ユニバーサル アクション モデルとアダプティブ カードの導入により、ボット開発者はアダプティブ カードのユーザー固有のビューをユーザーに `refresh` 提供できます。</span><span class="sxs-lookup"><span data-stu-id="42e50-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="42e50-106">同じアダプティブ カードをユーザー固有のアダプティブ カードに更新できます。</span><span class="sxs-lookup"><span data-stu-id="42e50-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span> <span data-ttu-id="42e50-107">最大 60 人の異なるユーザーが、追加情報またはアクションを含む別のバージョンのカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="42e50-107">Maximum 60 different users can see a different version of the card with additional information or actions.</span></span> <span data-ttu-id="42e50-108">これにより、承認、投票作成者コントロール、チケット発行、インシデント管理、プロジェクト管理カードなど、強力なシナリオが提供されます。</span><span class="sxs-lookup"><span data-stu-id="42e50-108">This provides powerful scenarios like approvals, poll creator controls, ticketing, incident management, and project management cards.</span></span>

<span data-ttu-id="42e50-109">たとえば、Contoso の安全検査官である Megan は、インシデントを作成して Alex に割り当てる必要があります。</span><span class="sxs-lookup"><span data-stu-id="42e50-109">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="42e50-110">また、チーム内のすべてのユーザーがインシデントを認識する必要があります。</span><span class="sxs-lookup"><span data-stu-id="42e50-110">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="42e50-111">Megan は、アダプティブ カードのユニバーサル アクションを利用した Contoso インシデント レポート メッセージ拡張機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="42e50-111">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

# <a name="mobile"></a>[<span data-ttu-id="42e50-112">モバイル</span><span class="sxs-lookup"><span data-stu-id="42e50-112">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="モバイル ユーザー固有のビュー":::

# <a name="desktop"></a>[<span data-ttu-id="42e50-114">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="42e50-114">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="ユーザー固有のビュー":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="42e50-116">アダプティブ カードのユーザー固有のビュー</span><span class="sxs-lookup"><span data-stu-id="42e50-116">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="42e50-117">次のコードは、アダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="42e50-117">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="42e50-118">**アダプティブ カードを送信するには、ユーザー固有のビューを更新し、ボットに要求を呼び出します。**</span><span class="sxs-lookup"><span data-stu-id="42e50-118">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="42e50-119">Megan が新しいインシデントを作成すると、ボットはアダプティブ カードまたは共通カードにインシデントの詳細を送信Teamsします。</span><span class="sxs-lookup"><span data-stu-id="42e50-119">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="42e50-120">これで、このカードは、Megan と Alex のユーザー固有のビューに自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="42e50-120">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="42e50-121">Alex と Megan のユーザー MRIs は、アダプティブ カード JSON のプロパティ `userIds` `refresh` のプロパティに追加されます。</span><span class="sxs-lookup"><span data-stu-id="42e50-121">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="42e50-122">カードは、会話内の他のユーザーに対して同じままです。</span><span class="sxs-lookup"><span data-stu-id="42e50-122">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="42e50-123">Megan の場合、自動更新によってボットへの `adaptiveCard/action` 呼び出し要求がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="42e50-123">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="42e50-124">ボットは、この呼び出し要求に対する応答として、ボタン付 `Edit` きインシデント作成者カードを返します。</span><span class="sxs-lookup"><span data-stu-id="42e50-124">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="42e50-125">Alex の場合と同様に、自動更新によってボットに対 `adaptiveCard/action` する別の呼び出し要求がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="42e50-125">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="42e50-126">ボットは、この呼び出し要求に対する応答として `Resolve` インシデント所有者カード ボタンを返します。</span><span class="sxs-lookup"><span data-stu-id="42e50-126">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="42e50-127">クライアントからボットにTeams要求を呼び出す</span><span class="sxs-lookup"><span data-stu-id="42e50-127">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="42e50-128">次のコードは、Alex と Megan のクライアントからボットに送信される呼び出しTeams例を示しています。</span><span class="sxs-lookup"><span data-stu-id="42e50-128">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="42e50-129">adaptiveCard/action invoke response card</span><span class="sxs-lookup"><span data-stu-id="42e50-129">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="42e50-130">次のコードは、Megan のアダプティブ カード/アクション呼び出し応答カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="42e50-130">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="42e50-131">adaptiveCard/action invoke response card for Alex</span><span class="sxs-lookup"><span data-stu-id="42e50-131">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="42e50-132">次のコードは、Alex のアダプティブ カード/アクション呼び出し応答カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="42e50-132">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="42e50-133">アダプティブ カードを返す応答を呼び出す</span><span class="sxs-lookup"><span data-stu-id="42e50-133">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="42e50-134">次のコードは、アダプティブ カードを返す呼び出し応答の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="42e50-134">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

<span data-ttu-id="42e50-135">ユーザー固有のビューを設計する際に注意するカード設計ガイドライン:</span><span class="sxs-lookup"><span data-stu-id="42e50-135">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="42e50-136">セクションで指定することで、チャットまたはチャネルに送信される特定のカードに対して最大 **60** のユーザー固有のビュー `userIds` を作成 `refresh` できます。</span><span class="sxs-lookup"><span data-stu-id="42e50-136">You can create a maximum of **60 User Specific Views** for a particular card sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="42e50-137">**基本カード:** ボット開発者がチャットに送信するカードの基本バージョン。</span><span class="sxs-lookup"><span data-stu-id="42e50-137">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="42e50-138">これは、セクションで指定されていないすべてのユーザーのアダプティブ カードのバージョン `userIds` です。</span><span class="sxs-lookup"><span data-stu-id="42e50-138">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="42e50-139">メッセージの更新を使用して、基本カードを更新し、同時にユーザー固有のカードを更新できます。</span><span class="sxs-lookup"><span data-stu-id="42e50-139">A message update can be used to update the base card and simultaneously refresh the User Specific Card.</span></span> <span data-ttu-id="42e50-140">チャットまたはチャネルを開く場合は、更新が有効になっているユーザーのカードも更新されます。</span><span class="sxs-lookup"><span data-stu-id="42e50-140">Opening the chat or channel also refreshes the card for users with refresh enabled.</span></span>
* <span data-ttu-id="42e50-141">ユーザーがアクションのビューに切り替える大規模なグループを持つシナリオでは、応答者の動的更新が必要です。最大 60 人のユーザーをリストに追加 `userIds` できます。</span><span class="sxs-lookup"><span data-stu-id="42e50-141">For scenarios with larger groups where users switch to a view on action, which needs dynamic updates for responders, you can keep adding up to 60 users to the `userIds` list.</span></span> <span data-ttu-id="42e50-142">61st ユーザーが応答すると、最初のレスポンダーをリストから削除できます。</span><span class="sxs-lookup"><span data-stu-id="42e50-142">You can remove the first responder from the list when the 61st user responds.</span></span> <span data-ttu-id="42e50-143">リストから削除されたユーザーの場合は、手動で更新ボタンを指定するか、メッセージ オプション メニューの更新ボタンを使用して最新の `userIds` 結果を取得できます。</span><span class="sxs-lookup"><span data-stu-id="42e50-143">For the users who get removed from the `userIds` list, you can provide a manual refresh button or use the refresh button in the message options menu to get the latest result.</span></span>
* <span data-ttu-id="42e50-144">ユーザーに対して、カードの特定のビューまたは一部のアクションのみを表示するユーザー固有のビューを取得するように求めるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="42e50-144">Give a prompt to users to get a User Specific View, where they see only a particular view of the card or some actions.</span></span>

## <a name="see-also"></a><span data-ttu-id="42e50-145">関連項目</span><span class="sxs-lookup"><span data-stu-id="42e50-145">See also</span></span>

* [<span data-ttu-id="42e50-146">アダプティブ カードのユニバーサル アクションの操作</span><span class="sxs-lookup"><span data-stu-id="42e50-146">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="42e50-147">最新のビュー</span><span class="sxs-lookup"><span data-stu-id="42e50-147">Up to date views</span></span>](Up-To-Date-Views.md)
