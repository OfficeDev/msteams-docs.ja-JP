---
title: カードの紹介
description: カードと、ボット、コネクタ、メッセージング拡張機能でのカードの使い方について説明します。
localization_priority: Normal
ms.topic: conceptual
keywords: コネクタ ボット カード メッセージング
ms.openlocfilehash: acf5dc95b742a433c092be9e293d589b5919bb4d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020269"
---
# <a name="cards"></a><span data-ttu-id="d1451-104">カード</span><span class="sxs-lookup"><span data-stu-id="d1451-104">Cards</span></span>

<span data-ttu-id="d1451-105">カード *は* 、短い情報や関連する情報のユーザー インターフェイス (UI) コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="d1451-105">A *card* is a user-interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="d1451-106">カードには複数のプロパティと添付ファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d1451-106">Cards can have multiple properties and attachments.</span></span> <span data-ttu-id="d1451-107">カードには、カードアクションをトリガーできるボタン [を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="d1451-107">Cards can include buttons which can trigger [Card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="d1451-108">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="d1451-108">Adaptive cards</span></span>

<span data-ttu-id="d1451-109">[アダプティブ カードは](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) 、ボット、Cortana、Outlook、Windows などの Microsoft 製品のカードの新しいクロス製品仕様です。</span><span class="sxs-lookup"><span data-stu-id="d1451-109">[Adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including Bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="d1451-110">これらは、新しい Teams 開発に推奨されるカードの種類です。</span><span class="sxs-lookup"><span data-stu-id="d1451-110">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="d1451-111">アダプティブ カード チームの一般的な情報については、「アダプティブ カード [の概要」を参照してください](/adaptive-cards)。</span><span class="sxs-lookup"><span data-stu-id="d1451-111">For general information from the Adaptive cards team see [Adaptive Cards Overview](/adaptive-cards).</span></span> <span data-ttu-id="d1451-112">アダプティブ カードは、既存のヒーロー カード、Office365 カード、およびサムネイル カードを使用できる任意の場所で使用できます。</span><span class="sxs-lookup"><span data-stu-id="d1451-112">You can use adaptive cards anywhere you can use existing Hero cards, Office365 cards, and Thumbnail cards.</span></span>

<span data-ttu-id="d1451-113">アダプティブ カードに加えて、Teams は次の 2 種類のカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d1451-113">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="d1451-114">365 コネクタの一部としてOfficeカード。</span><span class="sxs-lookup"><span data-stu-id="d1451-114">Connector Cards, used as part of Office 365 connectors.</span></span>
* <span data-ttu-id="d1451-115">サムネイルカードやヒーロー カードなど、ボット フレームワークからの単純なカード。</span><span class="sxs-lookup"><span data-stu-id="d1451-115">Simple cards from the bot framework, such as the thumbnail and hero cards.</span></span>

<span data-ttu-id="d1451-116">これらのカードの種類については、「Teams カードリファレンス」 [を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="d1451-116">These card types are described more fully in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

<span data-ttu-id="d1451-117">Teams は、次の 3 つの異なる場所でカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="d1451-117">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="d1451-118">コネクタ</span><span class="sxs-lookup"><span data-stu-id="d1451-118">Connectors</span></span>
* <span data-ttu-id="d1451-119">ボット</span><span class="sxs-lookup"><span data-stu-id="d1451-119">Bots</span></span>
* <span data-ttu-id="d1451-120">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="d1451-120">Messaging extensions</span></span>

## <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="d1451-121">アダプティブ カードと受信 Webhooks</span><span class="sxs-lookup"><span data-stu-id="d1451-121">Adaptive cards and incoming webhooks</span></span>

> [!NOTE]
>
> <span data-ttu-id="d1451-122">✔ `Action.Submit` 以外のすべてのネイティブのアダプティブ カード スキーマ要素は、完全にサポートされます。</span><span class="sxs-lookup"><span data-stu-id="d1451-122">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="d1451-123">✔サポートされているアクションは [**、Action.OpenURL、Action.ShowCard、**](https://adaptivecards.io/explorer/Action.OpenUrl.html)[**および Action.ToggleVisibility です**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)。 [](https://adaptivecards.io/explorer/Action.ShowCard.html)</span><span class="sxs-lookup"><span data-stu-id="d1451-123">✔ The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="d1451-124">コネクタ内のカード</span><span class="sxs-lookup"><span data-stu-id="d1451-124">Cards in Connectors</span></span>

<span data-ttu-id="d1451-125">カードは、最初に Outlook および Office 365 の一部として定義され、365 コネクタOffice使用されます。</span><span class="sxs-lookup"><span data-stu-id="d1451-125">Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors.</span></span> <span data-ttu-id="d1451-126">365 Officeの多くのアプリケーションと同様に、Teams はコネクタをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d1451-126">Like many Office 365 applications, Teams supports Connectors.</span></span> <span data-ttu-id="d1451-127">Microsoft Teams 用 Office [365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)コネクタのコネクタの詳細については、「アクション可能なメッセージ カードリファレンス」の「コネクタ内のカードの仕様」 [を参照してください](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="d1451-127">You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), and find the specification for cards in connectors in [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="d1451-128">ボット内のカード</span><span class="sxs-lookup"><span data-stu-id="d1451-128">Cards in Bots</span></span>

<span data-ttu-id="d1451-129">Microsoft Bot Framework は、ボットがボット メッセージの一部として使用できる定義済みのカードのセットを追加することで、カードの仕様を拡張しました。</span><span class="sxs-lookup"><span data-stu-id="d1451-129">The Microsoft Bot Framework extended the cards specification by adding a set of predefined cards that bots could use as part of bot messages.</span></span> <span data-ttu-id="d1451-130">Teams はボット フレームワークを使用してボットをサポートしますが、これらのカードの少し異なるセットをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d1451-130">Teams supports bots using the Bot Framework but it supports a slightly different set of these cards.</span></span> <span data-ttu-id="d1451-131">Bot Framework のカードに関する一般的な情報については、「メッセージにリッチ カード [の添付ファイルを追加する」を参照してください](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。</span><span class="sxs-lookup"><span data-stu-id="d1451-131">General information on cards in Bot Framework can be found in [Add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="d1451-132">これらのカードは Teams の簡易 *カードと* 呼ばれる。</span><span class="sxs-lookup"><span data-stu-id="d1451-132">These cards are called *simple cards* in Teams.</span></span>

<span data-ttu-id="d1451-133">Teams のボットは、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="d1451-133">Bots in Teams can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="d1451-134">Teams のボットでサポートされているカードについては、「Teams カードリファレンス [」を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="d1451-134">Cards that are supported by bots in Teams are detailed in [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>  

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="d1451-135">メッセージング拡張機能のカード</span><span class="sxs-lookup"><span data-stu-id="d1451-135">Cards in Messaging Extensions</span></span>

<span data-ttu-id="d1451-136">[メッセージング拡張機能は、](~/messaging-extensions/what-are-messaging-extensions.md) カードを返す場合があります。</span><span class="sxs-lookup"><span data-stu-id="d1451-136">[Messaging Extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="d1451-137">メッセージング拡張機能では、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="d1451-137">Messaging extensions can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="d1451-138">これらのカードは[、Teams カードリファレンスに含まれる。](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="d1451-138">These cards are found in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="card-reference"></a><span data-ttu-id="d1451-139">カード参照</span><span class="sxs-lookup"><span data-stu-id="d1451-139">Card reference</span></span>

<span data-ttu-id="d1451-140">Teams で使用されるカードはすべて、Teams カードリファレンス [に一覧表示されます](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="d1451-140">All cards used by Teams are listed in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="d1451-141">このリファレンスでは、Teams の Bot Framework カードとカードの違いについて説明します。</span><span class="sxs-lookup"><span data-stu-id="d1451-141">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>
