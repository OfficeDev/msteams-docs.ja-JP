---
title: カードの紹介
description: カードと、ボット、コネクタ、およびメッセージング拡張機能での使用方法について説明します。
keywords: コネクタボットカードメッセージ
ms.openlocfilehash: 6d850f83183f12fa0c228a7a89b23e58f523e15b
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651657"
---
# <a name="cards"></a><span data-ttu-id="ced32-104">カード</span><span class="sxs-lookup"><span data-stu-id="ced32-104">Cards</span></span>

<span data-ttu-id="ced32-105">*カード*は、短いまたは関連する情報のユーザーインターフェイス (UI) コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="ced32-105">A *card* is a user-interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="ced32-106">カードは複数のプロパティと添付ファイルを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="ced32-106">Cards can have multiple properties and attachments.</span></span> <span data-ttu-id="ced32-107">カードには、 [カードアクション](~/task-modules-and-cards/cards/cards-actions.md)をトリガーできるボタンを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="ced32-107">Cards can include buttons which can trigger [Card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="ced32-108">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="ced32-108">Adaptive cards</span></span>

<span data-ttu-id="ced32-109">[アダプティブカード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) は、ボット、Cortana、Outlook、Windows など、Microsoft 製品のカードの新しいクロスプロダクト仕様です。</span><span class="sxs-lookup"><span data-stu-id="ced32-109">[Adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including Bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="ced32-110">新しいチーム開発に推奨されるカードの種類です。</span><span class="sxs-lookup"><span data-stu-id="ced32-110">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="ced32-111">アダプティブカードチームからの一般的な情報については、「 [アダプティブカードの概要](/adaptive-cards)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ced32-111">For general information from the Adaptive cards team see [Adaptive Cards Overview](/adaptive-cards).</span></span> <span data-ttu-id="ced32-112">既存のヒーローカード、Office365 カード、およびサムネイルカードを使用できる場所であれば、アダプティブカードを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="ced32-112">You can use adaptive cards anywhere you can use existing Hero cards, Office365 cards, and Thumbnail cards.</span></span>

<span data-ttu-id="ced32-113">アダプティブカードに加えて、Teams は次の2種類のカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ced32-113">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="ced32-114">コネクタカード。 Office 365 コネクタの一部として使用されます。</span><span class="sxs-lookup"><span data-stu-id="ced32-114">Connector Cards, used as part of Office 365 connectors.</span></span>
* <span data-ttu-id="ced32-115">Bot フレームワークからのシンプルなカード (サムネイルカード、英雄カードなど)。</span><span class="sxs-lookup"><span data-stu-id="ced32-115">Simple cards from the bot framework, such as the thumbnail and hero cards.</span></span>

<span data-ttu-id="ced32-116">これらのカードの種類については、 [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)でさらに詳しく説明されています。</span><span class="sxs-lookup"><span data-stu-id="ced32-116">These card types are described more fully in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

<span data-ttu-id="ced32-117">Teams では、次の3つの異なる場所にカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="ced32-117">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="ced32-118">コネクタ</span><span class="sxs-lookup"><span data-stu-id="ced32-118">Connectors</span></span>
* <span data-ttu-id="ced32-119">ボット</span><span class="sxs-lookup"><span data-stu-id="ced32-119">Bots</span></span>
* <span data-ttu-id="ced32-120">メッセージングの拡張機能</span><span class="sxs-lookup"><span data-stu-id="ced32-120">Messaging extensions</span></span>

## <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="ced32-121">アダプティブカードと受信 web フック</span><span class="sxs-lookup"><span data-stu-id="ced32-121">Adaptive cards and incoming webhooks</span></span>

> [!NOTE]
> <span data-ttu-id="ced32-122">アダプティブカードは、 [一般開発者向けプレビュープログラム](../resources/dev-preview/developer-preview-intro.md)の一部として受信 web フックでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ced32-122">Adaptive cards are supported in incoming webhooks as part of the [public developer preview program](../resources/dev-preview/developer-preview-intro.md).</span></span> <span data-ttu-id="ced32-123">パブリックプレビューは、早期アクセスおよびフィードバックに使用できます。</span><span class="sxs-lookup"><span data-stu-id="ced32-123">Public previews are available for early-access and feedback.</span></span> <span data-ttu-id="ced32-124">リリースは安定しており、広範なテストを行っていますが、運用環境での使用は想定されていません。</span><span class="sxs-lookup"><span data-stu-id="ced32-124">Although the release is stable and has undergone extensive testing, it is not intended for use in production.</span></span>
>
> <span data-ttu-id="ced32-125">✔開発者向けプレビューでは、を除くすべてのネイティブアダプティブカードスキーマ要素 `Action.Submit` が完全にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ced32-125">✔ Within the developer preview, all native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="ced32-126">サポートされているアクションは✔ [**OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、 [**showcard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、および [**action.togglevisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)です。</span><span class="sxs-lookup"><span data-stu-id="ced32-126">✔ The supported Actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="ced32-127">コネクタ内のカード</span><span class="sxs-lookup"><span data-stu-id="ced32-127">Cards in Connectors</span></span>

<span data-ttu-id="ced32-128">カードは、最初は Outlook および Office 365 の一部として定義されており、Office 365 コネクタの一部として使用されています。</span><span class="sxs-lookup"><span data-stu-id="ced32-128">Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors.</span></span> <span data-ttu-id="ced32-129">多くの Office 365 アプリケーションと同様に、Teams はコネクタをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ced32-129">Like many Office 365 applications, Teams supports Connectors.</span></span> <span data-ttu-id="ced32-130">[Microsoft Teams の Office 365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)のコネクタの詳細については、「操作可能な[メッセージカードリファレンス](/outlook/actionable-messages/card-reference)」の「コネクタ内のカードの仕様」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ced32-130">You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), and find the specification for cards in connectors in [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="ced32-131">Bot のカード</span><span class="sxs-lookup"><span data-stu-id="ced32-131">Cards in Bots</span></span>

<span data-ttu-id="ced32-132">Microsoft Bot フレームワークは、ボットメッセージの一部として使用できる定義済みのカードのセットを追加することによって、カードの仕様を拡張しました。</span><span class="sxs-lookup"><span data-stu-id="ced32-132">The Microsoft Bot Framework extended the cards specification by adding a set of predefined cards that bots could use as part of bot messages.</span></span> <span data-ttu-id="ced32-133">Teams は Bot フレームワークを使用してサポートされていますが、これらのカードの少し異なるセットをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ced32-133">Teams supports bots using the Bot Framework but it supports a slightly different set of these cards.</span></span> <span data-ttu-id="ced32-134">Bot フレームワークのカードに関する一般的な情報については、「 [メッセージへのリッチカードの添付ファイルの追加](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ced32-134">General information on cards in Bot Framework can be found in [Add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="ced32-135">これらのカードは Teams で *シンプルカード* と呼ばれています。</span><span class="sxs-lookup"><span data-stu-id="ced32-135">These cards are called *simple cards* in Teams.</span></span>

<span data-ttu-id="ced32-136">Teams のボットは、任意の種類のカードを使用できます: simple、connector、またはアダプティブ。</span><span class="sxs-lookup"><span data-stu-id="ced32-136">Bots in Teams can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="ced32-137">Teams の bot がサポートするカードについては、 [Teams カードリファレンスを参照](~/task-modules-and-cards/cards/cards-reference.md)してください。</span><span class="sxs-lookup"><span data-stu-id="ced32-137">Cards that are supported by bots in Teams are detailed in [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>  

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="ced32-138">メッセージング拡張機能のカード</span><span class="sxs-lookup"><span data-stu-id="ced32-138">Cards in Messaging Extensions</span></span>

<span data-ttu-id="ced32-139">[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md) もカードを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="ced32-139">[Messaging Extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="ced32-140">メッセージング拡張機能では、シンプル、コネクタ、またはアダプティブのいずれの種類のカードでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="ced32-140">Messaging extensions can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="ced32-141">これらのカードは [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)に掲載されています。</span><span class="sxs-lookup"><span data-stu-id="ced32-141">These cards are found in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="card-reference"></a><span data-ttu-id="ced32-142">カードリファレンス</span><span class="sxs-lookup"><span data-stu-id="ced32-142">Card reference</span></span>

<span data-ttu-id="ced32-143">Teams で使用されるすべてのカードは [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)に記載されています。</span><span class="sxs-lookup"><span data-stu-id="ced32-143">All cards used by Teams are listed in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="ced32-144">このリファレンスでは、Teams の Bot フレームワークカードとカードの相違点についても説明します。</span><span class="sxs-lookup"><span data-stu-id="ced32-144">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>
