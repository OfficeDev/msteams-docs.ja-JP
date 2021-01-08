---
title: カードの紹介
description: カードについて説明し、ボット、コネクタ、メッセージング拡張機能でカードがどのように使用されるのかについて説明します。
keywords: コネクタボット カードメッセージング
ms.openlocfilehash: 00c649a1339f05b782e03a2c0db5cba2445f66bc
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777925"
---
# <a name="cards"></a><span data-ttu-id="2d8aa-104">カード</span><span class="sxs-lookup"><span data-stu-id="2d8aa-104">Cards</span></span>

<span data-ttu-id="2d8aa-105">カード *は* 、短い情報または関連する情報のユーザー インターフェイス (UI) コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-105">A *card* is a user-interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="2d8aa-106">カードには、複数のプロパティと添付ファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-106">Cards can have multiple properties and attachments.</span></span> <span data-ttu-id="2d8aa-107">カードには、カードアクションをトリガーできるボタン [を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-107">Cards can include buttons which can trigger [Card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="2d8aa-108">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="2d8aa-108">Adaptive cards</span></span>

<span data-ttu-id="2d8aa-109">[アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) は、ボット、Cortana、Outlook、Windows など、Microsoft 製品のカードの新しいクロス製品仕様です。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-109">[Adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including Bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="2d8aa-110">これらは、新しい Teams 開発に推奨されるカードの種類です。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-110">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="2d8aa-111">アダプティブ カード チームからの一般的な情報については、「アダプティブ カード [の概要」を参照してください](/adaptive-cards)。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-111">For general information from the Adaptive cards team see [Adaptive Cards Overview](/adaptive-cards).</span></span> <span data-ttu-id="2d8aa-112">アダプティブ カードは、既存のヒーロー カード、Office365 カード、サムネイル カードを使用できる任意の場所で使用できます。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-112">You can use adaptive cards anywhere you can use existing Hero cards, Office365 cards, and Thumbnail cards.</span></span>

<span data-ttu-id="2d8aa-113">Teams では、アダプティブ カードに加えて、次の 2 種類のカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-113">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="2d8aa-114">365 コネクタの一部としてOfficeカード。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-114">Connector Cards, used as part of Office 365 connectors.</span></span>
* <span data-ttu-id="2d8aa-115">サムネイルやヒーロー カードなど、ボット フレームワークからの単純なカード。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-115">Simple cards from the bot framework, such as the thumbnail and hero cards.</span></span>

<span data-ttu-id="2d8aa-116">これらのカードの種類については、「Teams カード リファレンス」で [詳しい説明があります](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-116">These card types are described more fully in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

<span data-ttu-id="2d8aa-117">Teams は、次の 3 つの異なる場所でカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-117">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="2d8aa-118">コネクタ</span><span class="sxs-lookup"><span data-stu-id="2d8aa-118">Connectors</span></span>
* <span data-ttu-id="2d8aa-119">ボット</span><span class="sxs-lookup"><span data-stu-id="2d8aa-119">Bots</span></span>
* <span data-ttu-id="2d8aa-120">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="2d8aa-120">Messaging extensions</span></span>

## <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="2d8aa-121">アダプティブ カードと受信 Webhook</span><span class="sxs-lookup"><span data-stu-id="2d8aa-121">Adaptive cards and incoming webhooks</span></span>

> [!NOTE]
>
> <span data-ttu-id="2d8aa-122">✔ `Action.Submit` 以外のすべてのネイティブのアダプティブ カード スキーマ要素は、完全にサポートされます。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-122">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="2d8aa-123">✔サポートされているアクションは、Action.OpenURL、Action.ShowCard、Action.ToggleVisibility [**です**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)。 [](https://adaptivecards.io/explorer/Action.OpenUrl.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html)</span><span class="sxs-lookup"><span data-stu-id="2d8aa-123">✔ The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="2d8aa-124">コネクタ内のカード</span><span class="sxs-lookup"><span data-stu-id="2d8aa-124">Cards in Connectors</span></span>

<span data-ttu-id="2d8aa-125">カードは最初に Outlook および Office 365 の一部として定義され、Office 365 コネクタの一部として使用されます。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-125">Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors.</span></span> <span data-ttu-id="2d8aa-126">365 Officeの多くのアプリケーションと同様に、Teams はコネクタをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-126">Like many Office 365 applications, Teams supports Connectors.</span></span> <span data-ttu-id="2d8aa-127">Office [365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)のコネクタの詳細を確認し、コネクタ内のカードの仕様については、「操作可能なメッセージ カード リファレンス」 [を参照してください](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-127">You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), and find the specification for cards in connectors in [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="2d8aa-128">ボット内のカード</span><span class="sxs-lookup"><span data-stu-id="2d8aa-128">Cards in Bots</span></span>

<span data-ttu-id="2d8aa-129">Microsoft Bot Framework は、ボットがボット メッセージの一部として使用できる定義済みカードのセットを追加することで、カードの仕様を拡張しました。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-129">The Microsoft Bot Framework extended the cards specification by adding a set of predefined cards that bots could use as part of bot messages.</span></span> <span data-ttu-id="2d8aa-130">Teams は Bot Framework を使用したボットをサポートしますが、これらのカードの少し異なるセットをサポートします。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-130">Teams supports bots using the Bot Framework but it supports a slightly different set of these cards.</span></span> <span data-ttu-id="2d8aa-131">Bot Framework のカードに関する一般的な情報については、「リッチ カードの添付ファイルをメッセージ [に追加する」を参照してください](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-131">General information on cards in Bot Framework can be found in [Add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="2d8aa-132">これらのカードは、Teams では *簡易カード* と呼ばれるカードです。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-132">These cards are called *simple cards* in Teams.</span></span>

<span data-ttu-id="2d8aa-133">Teams のボットは、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-133">Bots in Teams can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="2d8aa-134">Teams のボットでサポートされているカードの詳細については、「Teams カード リファレンス」 [を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-134">Cards that are supported by bots in Teams are detailed in [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>  

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="2d8aa-135">メッセージング拡張機能のカード</span><span class="sxs-lookup"><span data-stu-id="2d8aa-135">Cards in Messaging Extensions</span></span>

<span data-ttu-id="2d8aa-136">[メッセージング拡張機能は、](~/messaging-extensions/what-are-messaging-extensions.md) カードを返す場合があります。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-136">[Messaging Extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="2d8aa-137">メッセージング拡張機能は、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-137">Messaging extensions can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="2d8aa-138">これらのカードは、Teams カード リファレンス [に含まれるものがあります](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-138">These cards are found in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="card-reference"></a><span data-ttu-id="2d8aa-139">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="2d8aa-139">Card reference</span></span>

<span data-ttu-id="2d8aa-140">Teams で使用されるカードはすべて、Teams カード リファレンスに [記載されています](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-140">All cards used by Teams are listed in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="2d8aa-141">このリファレンスでは、Teams での Bot Framework カードとカードの違いも説明します。</span><span class="sxs-lookup"><span data-stu-id="2d8aa-141">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>
