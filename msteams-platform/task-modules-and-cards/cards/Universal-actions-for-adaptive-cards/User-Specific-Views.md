---
title: ユーザー固有のビュー
description: ユニバーサル アクションを使用したユーザー固有ビューのサンプル
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 696fc5ce25c79d749b301309bfe0c737e39ad294
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555445"
---
# <a name="user-specific-views"></a><span data-ttu-id="701e4-103">ユーザー固有のビュー</span><span class="sxs-lookup"><span data-stu-id="701e4-103">User Specific Views</span></span>

<span data-ttu-id="701e4-104">以前は、Teams会話でアダプティブ カードが送信された場合、すべてのユーザーにまったく同じカード コンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="701e4-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="701e4-105">ユニバーサルアクションモデルと `refresh` アダプティブカードの導入により、ボット開発者はユーザーにアダプティブカードのユーザ固有のビューを提供できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="701e4-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="701e4-106">同じアダプティブ カードをユーザー固有のアダプティブ カードに更新できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="701e4-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span>

<span data-ttu-id="701e4-107">たとえば、Contoso 社の安全検査官である Megan は、インシデントを作成して Alex に割り当てる必要があります。</span><span class="sxs-lookup"><span data-stu-id="701e4-107">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="701e4-108">彼女はまた、チームの全員に事件について気づいてもらいたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="701e4-108">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="701e4-109">Megan は、アダプティブ カードのユニバーサル アクションを使用して、Contoso インシデント レポート メッセージ拡張機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="701e4-109">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="ユーザー固有のビュー":::

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="701e4-111">アダプティブ カードのユーザ固有のビュー</span><span class="sxs-lookup"><span data-stu-id="701e4-111">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="701e4-112">次のコードは、アダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="701e4-112">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="701e4-113">**アダプティブ カードを送信し、ユーザー固有のビューを更新し、ボットに要求を呼び出すには**</span><span class="sxs-lookup"><span data-stu-id="701e4-113">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="701e4-114">Megan が新しいインシデントを作成すると、ボットは、Teams会話でインシデントの詳細を含むアダプティブ カードまたは共通カードを送信します。</span><span class="sxs-lookup"><span data-stu-id="701e4-114">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="701e4-115">これで、このカードは、Megan と Alex のユーザー固有ビューに自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="701e4-115">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="701e4-116">アレックスとメーガンのユーザーMRIは、 `userIds` `refresh` アダプティブカードJSONのプロパティのプロパティに追加されます。</span><span class="sxs-lookup"><span data-stu-id="701e4-116">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="701e4-117">カードは、会話内の他のユーザーに対して同じままです。</span><span class="sxs-lookup"><span data-stu-id="701e4-117">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="701e4-118">Megan の場合、自動更新は `adaptiveCard/action` ボットへの呼び出し要求をトリガーします。</span><span class="sxs-lookup"><span data-stu-id="701e4-118">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="701e4-119">ボットは、 `Edit` この呼び出し要求への応答として、ボタン付きのインシデント作成者カードを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="701e4-119">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="701e4-120">同様に、Alexの場合も、自動リフレッシュによって `adaptiveCard/action` ボットに対する別の呼び出し要求がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="701e4-120">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="701e4-121">ボットは、 `Resolve` この呼び出し要求への応答としてインシデント所有者カード ボタンを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="701e4-121">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="701e4-122">クライアントからボットに送信Teams要求を呼び出す</span><span class="sxs-lookup"><span data-stu-id="701e4-122">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="701e4-123">次のコードは、Alex と Megan のTeamsクライアントからボットに送信される呼び出し要求の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="701e4-123">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="701e4-124">アダプティブカード/アクション呼び出し応答カード</span><span class="sxs-lookup"><span data-stu-id="701e4-124">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="701e4-125">次のコードは、Megan のアダプティブ カード/アクション呼び出し応答カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="701e4-125">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="701e4-126">アダプティブカード/アクション呼び出し応答カードアレックス</span><span class="sxs-lookup"><span data-stu-id="701e4-126">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="701e4-127">次のコードは、Alexのアダプティブカード/アクション呼び出しレスポンスカードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="701e4-127">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="701e4-128">アダプティブ カードを返す応答を呼び出す</span><span class="sxs-lookup"><span data-stu-id="701e4-128">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="701e4-129">次のコードは、アダプティブ カードを返す呼び出し応答の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="701e4-129">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

<span data-ttu-id="701e4-130">ユーザー固有のビューを設計する際に留意するカード設計ガイドライン:</span><span class="sxs-lookup"><span data-stu-id="701e4-130">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="701e4-131">チャットまたはチャンネルに送信される特定のカードに対して、最大 60 個の **ユーザー固有ビュー** を作成するには `userIds` `refresh` 、そのカードをセクションで指定します。</span><span class="sxs-lookup"><span data-stu-id="701e4-131">You can create a maximum of **60 User Specific Views** for a particular card being sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="701e4-132">**ベースカード:** ボット開発者がチャットに送信するカードの基本バージョン。</span><span class="sxs-lookup"><span data-stu-id="701e4-132">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="701e4-133">これは、セクションで指定されていないすべてのユーザーのアダプティブ カードのバージョンです `userIds` 。</span><span class="sxs-lookup"><span data-stu-id="701e4-133">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="701e4-134">メッセージの更新または編集を使用してベースカードを更新し、同時にユーザー固有のカードを更新することができます。</span><span class="sxs-lookup"><span data-stu-id="701e4-134">A message update or edit can be used to update the base card and simultaneously refresh the User Specific Card.</span></span>

## <a name="see-also"></a><span data-ttu-id="701e4-135">関連項目</span><span class="sxs-lookup"><span data-stu-id="701e4-135">See also</span></span>

* [<span data-ttu-id="701e4-136">アダプティブ カードのユニバーサル アクションの操作</span><span class="sxs-lookup"><span data-stu-id="701e4-136">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="701e4-137">最新のビュー</span><span class="sxs-lookup"><span data-stu-id="701e4-137">Up to date views</span></span>](Up-To-Date-Views.md)
