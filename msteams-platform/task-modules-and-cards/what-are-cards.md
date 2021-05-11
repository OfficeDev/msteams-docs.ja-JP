---
title: カードの紹介
description: カードと、ボット、コネクタ、メッセージング拡張機能でのカードの使い方について説明します。
localization_priority: Normal
ms.topic: conceptual
keywords: コネクタ ボット カード メッセージング
ms.openlocfilehash: 77dcbb7d0472b584623e878df956a6165296f4cf
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088753"
---
# <a name="cards"></a><span data-ttu-id="a60a7-104">カード</span><span class="sxs-lookup"><span data-stu-id="a60a7-104">Cards</span></span>

<span data-ttu-id="a60a7-105">カード *は* 、短い情報や関連する情報のユーザー インターフェイス (UI) コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="a60a7-105">A *card* is a user-interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="a60a7-106">カードには複数のプロパティと添付ファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a60a7-106">Cards can have multiple properties and attachments.</span></span> <span data-ttu-id="a60a7-107">カードには、カードアクションをトリガーできるボタン [を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="a60a7-107">Cards can include buttons which can trigger [Card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="a60a7-108">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="a60a7-108">Adaptive cards</span></span>

<span data-ttu-id="a60a7-109">[アダプティブ カードは](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)、Bots、Cortana、Outlook、および Windows などの Microsoft 製品のカードの新しいクロス製品仕様です。</span><span class="sxs-lookup"><span data-stu-id="a60a7-109">[Adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including Bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="a60a7-110">これらは、新しいカード開発に推奨されるTeamsです。</span><span class="sxs-lookup"><span data-stu-id="a60a7-110">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="a60a7-111">アダプティブ カード チームの一般的な情報については、「アダプティブ カード [の概要」を参照してください](/adaptive-cards)。</span><span class="sxs-lookup"><span data-stu-id="a60a7-111">For general information from the Adaptive cards team see [Adaptive Cards Overview](/adaptive-cards).</span></span> <span data-ttu-id="a60a7-112">アダプティブ カードは、既存のヒーロー カード、Office365 カード、およびサムネイル カードを使用できる任意の場所で使用できます。</span><span class="sxs-lookup"><span data-stu-id="a60a7-112">You can use adaptive cards anywhere you can use existing Hero cards, Office365 cards, and Thumbnail cards.</span></span>

<span data-ttu-id="a60a7-113">アダプティブ カードに加えて、Teams 2 種類のカードがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="a60a7-113">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="a60a7-114">コネクタ カード(コネクタ コネクタの一Office 365されます。</span><span class="sxs-lookup"><span data-stu-id="a60a7-114">Connector Cards, used as part of Office 365 connectors.</span></span>
* <span data-ttu-id="a60a7-115">サムネイルカードやヒーロー カードなど、ボット フレームワークからの単純なカード。</span><span class="sxs-lookup"><span data-stu-id="a60a7-115">Simple cards from the bot framework, such as the thumbnail and hero cards.</span></span>

<span data-ttu-id="a60a7-116">これらのカードの種類については、「カードリファレンス」[で詳Teams説明します](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="a60a7-116">These card types are described more fully in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

<span data-ttu-id="a60a7-117">Teamsは、次の 3 つの異なる場所でカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="a60a7-117">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="a60a7-118">コネクタ</span><span class="sxs-lookup"><span data-stu-id="a60a7-118">Connectors</span></span>
* <span data-ttu-id="a60a7-119">ボット</span><span class="sxs-lookup"><span data-stu-id="a60a7-119">Bots</span></span>
* <span data-ttu-id="a60a7-120">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="a60a7-120">Messaging extensions</span></span>

## <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="a60a7-121">アダプティブ カードと受信 Webhooks</span><span class="sxs-lookup"><span data-stu-id="a60a7-121">Adaptive cards and incoming webhooks</span></span>

> [!NOTE]
>
> <span data-ttu-id="a60a7-122">✔ `Action.Submit` 以外のすべてのネイティブのアダプティブ カード スキーマ要素は、完全にサポートされます。</span><span class="sxs-lookup"><span data-stu-id="a60a7-122">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="a60a7-123">✔サポートされているアクションは[](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)、Action.OpenURL、Action.ShowCard、Action.ToggleVisibility、およびAction.Exeです。 [](https://adaptivecards.io/explorer/Action.OpenUrl.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html) [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)</span><span class="sxs-lookup"><span data-stu-id="a60a7-123">✔ The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) and [**Action.Execute**](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="a60a7-124">コネクタ内のカード</span><span class="sxs-lookup"><span data-stu-id="a60a7-124">Cards in Connectors</span></span>

<span data-ttu-id="a60a7-125">カードは最初に、OutlookおよびOffice 365の一部として定義され、Office 365コネクタの一部として使用されます。</span><span class="sxs-lookup"><span data-stu-id="a60a7-125">Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors.</span></span> <span data-ttu-id="a60a7-126">多くのアプリケーションOffice 365同様に、Teamsコネクタもサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a60a7-126">Like many Office 365 applications, Teams supports Connectors.</span></span> <span data-ttu-id="a60a7-127">コネクタの詳細については、「Office 365 コネクタ[](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)for Microsoft Teams」、および「Actionable message card reference」の「コネクタ内のカードの仕様」[を参照してください](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="a60a7-127">You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), and find the specification for cards in connectors in [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="a60a7-128">ボット内のカード</span><span class="sxs-lookup"><span data-stu-id="a60a7-128">Cards in Bots</span></span>

<span data-ttu-id="a60a7-129">このMicrosoft Bot Frameworkボットがボット メッセージの一部として使用できる定義済みのカードのセットを追加することで、カードの仕様を拡張しました。</span><span class="sxs-lookup"><span data-stu-id="a60a7-129">The Microsoft Bot Framework extended the cards specification by adding a set of predefined cards that bots could use as part of bot messages.</span></span> <span data-ttu-id="a60a7-130">Teamsボットフレームワークを使用してボットをサポートしていますが、これらのカードの少し異なるセットをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a60a7-130">Teams supports bots using the Bot Framework but it supports a slightly different set of these cards.</span></span> <span data-ttu-id="a60a7-131">Bot Framework のカードに関する一般的な情報については、「メッセージにリッチ カード [の添付ファイルを追加する」を参照してください](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。</span><span class="sxs-lookup"><span data-stu-id="a60a7-131">General information on cards in Bot Framework can be found in [Add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="a60a7-132">これらのカードは、簡易 *カードと* 呼ばれるTeams。</span><span class="sxs-lookup"><span data-stu-id="a60a7-132">These cards are called *simple cards* in Teams.</span></span>

<span data-ttu-id="a60a7-133">ボットは、Teams、コネクタ、アダプティブなど、任意の種類のカードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="a60a7-133">Bots in Teams can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="a60a7-134">このページのボットでサポートされているTeamsについては[、「Teams」を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="a60a7-134">Cards that are supported by bots in Teams are detailed in [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>  

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="a60a7-135">メッセージング拡張機能のカード</span><span class="sxs-lookup"><span data-stu-id="a60a7-135">Cards in Messaging Extensions</span></span>

<span data-ttu-id="a60a7-136">[メッセージング拡張機能は、](~/messaging-extensions/what-are-messaging-extensions.md) カードを返す場合があります。</span><span class="sxs-lookup"><span data-stu-id="a60a7-136">[Messaging Extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="a60a7-137">メッセージング拡張機能では、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="a60a7-137">Messaging extensions can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="a60a7-138">これらのカードは、「カード リファレンス[」のTeamsに示されています](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="a60a7-138">These cards are found in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="card-reference"></a><span data-ttu-id="a60a7-139">カード参照</span><span class="sxs-lookup"><span data-stu-id="a60a7-139">Card reference</span></span>

<span data-ttu-id="a60a7-140">ユーザーが使用するTeamsは、[カードリファレンス] にTeams[一覧表示されます](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="a60a7-140">All cards used by Teams are listed in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="a60a7-141">このリファレンスでは、ボット フレームワーク カードとボット フレームワーク カードの違いについて説明Teams。</span><span class="sxs-lookup"><span data-stu-id="a60a7-141">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>
