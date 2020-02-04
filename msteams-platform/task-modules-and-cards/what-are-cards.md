---
title: カードの紹介
description: カードと、ボット、コネクタ、およびメッセージング拡張機能での使用方法について説明します。
keywords: コネクタボットカードメッセージ
ms.openlocfilehash: a260313c6e9442ce7bd76524e41e6465617bafb5
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674824"
---
# <a name="cards"></a><span data-ttu-id="a06a5-104">Lcc</span><span class="sxs-lookup"><span data-stu-id="a06a5-104">Cards</span></span>

<span data-ttu-id="a06a5-105">*カード*は、短いまたは関連する情報のユーザーインターフェイス (UI) コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="a06a5-105">A *card* is a user-interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="a06a5-106">カードは複数のプロパティと添付ファイルを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="a06a5-106">Cards can have multiple properties and attachments.</span></span> <span data-ttu-id="a06a5-107">カードには、[カードアクション](~/task-modules-and-cards/cards/cards-actions.md)をトリガーできるボタンを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a06a5-107">Cards can include buttons which can trigger [Card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="a06a5-108">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="a06a5-108">Adaptive cards</span></span>

<span data-ttu-id="a06a5-109">[アダプティブカード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)は、ボット、Cortana、Outlook、Windows など、Microsoft 製品のカードの新しいクロスプロダクト仕様です。</span><span class="sxs-lookup"><span data-stu-id="a06a5-109">[Adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including Bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="a06a5-110">新しいチーム開発に推奨されるカードの種類です。</span><span class="sxs-lookup"><span data-stu-id="a06a5-110">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="a06a5-111">アダプティブカードチームからの一般的な情報については、「[アダプティブカードの概要](/adaptive-cards)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a06a5-111">For general information from the Adaptive cards team see [Adaptive Cards Overview](/adaptive-cards).</span></span> <span data-ttu-id="a06a5-112">既存のヒーローカード、Office365 カード、およびサムネイルカードを使用できる場所であれば、アダプティブカードを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="a06a5-112">You can use adaptive cards anywhere you can use existing Hero cards, Office365 cards, and Thumbnail cards.</span></span>

<span data-ttu-id="a06a5-113">アダプティブカードに加えて、Teams は次の2種類のカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a06a5-113">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="a06a5-114">コネクタカード。 Office 365 コネクタの一部として使用されます。</span><span class="sxs-lookup"><span data-stu-id="a06a5-114">Connector Cards, used as part of Office 365 connectors.</span></span>
* <span data-ttu-id="a06a5-115">Bot フレームワークからのシンプルなカード (サムネイルカード、英雄カードなど)。</span><span class="sxs-lookup"><span data-stu-id="a06a5-115">Simple cards from the bot framework, such as the thumbnail and hero cards.</span></span>

<span data-ttu-id="a06a5-116">これらのカードの種類については、 [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)でさらに詳しく説明されています。</span><span class="sxs-lookup"><span data-stu-id="a06a5-116">These card types are described more fully in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

<span data-ttu-id="a06a5-117">Teams では、次の3つの異なる場所にカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="a06a5-117">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="a06a5-118">コネクタ</span><span class="sxs-lookup"><span data-stu-id="a06a5-118">Connectors</span></span>
* <span data-ttu-id="a06a5-119">ボット</span><span class="sxs-lookup"><span data-stu-id="a06a5-119">Bots</span></span>
* <span data-ttu-id="a06a5-120">メッセージングの拡張機能</span><span class="sxs-lookup"><span data-stu-id="a06a5-120">Messaging extensions</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="a06a5-121">コネクタ内のカード</span><span class="sxs-lookup"><span data-stu-id="a06a5-121">Cards in Connectors</span></span>

<span data-ttu-id="a06a5-122">カードは、最初は Outlook および Office 365 の一部として定義されており、Office 365 コネクタの一部として使用されています。</span><span class="sxs-lookup"><span data-stu-id="a06a5-122">Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors.</span></span> <span data-ttu-id="a06a5-123">多くの Office 365 アプリケーションと同様に、Teams はコネクタをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a06a5-123">Like many Office 365 applications, Teams supports Connectors.</span></span> <span data-ttu-id="a06a5-124">[Microsoft Teams の Office 365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)のコネクタの詳細については、「操作可能な[メッセージカードリファレンス](/outlook/actionable-messages/card-reference)」の「コネクタ内のカードの仕様」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a06a5-124">You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), and find the specification for cards in connectors in [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="a06a5-125">Bot のカード</span><span class="sxs-lookup"><span data-stu-id="a06a5-125">Cards in Bots</span></span>

<span data-ttu-id="a06a5-126">Microsoft Bot フレームワークは、ボットメッセージの一部として使用できる定義済みのカードのセットを追加することによって、カードの仕様を拡張しました。</span><span class="sxs-lookup"><span data-stu-id="a06a5-126">The Microsoft Bot Framework extended the cards specification by adding a set of predefined cards that bots could use as part of bot messages.</span></span> <span data-ttu-id="a06a5-127">Teams は Bot フレームワークを使用してサポートされていますが、これらのカードの少し異なるセットをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a06a5-127">Teams supports bots using the Bot Framework but it supports a slightly different set of these cards.</span></span> <span data-ttu-id="a06a5-128">Bot フレームワークのカードに関する一般的な情報については、「[メッセージへのリッチカードの添付ファイルの追加](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a06a5-128">General information on cards in Bot Framework can be found in [Add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="a06a5-129">これらのカードは Teams で*シンプルカード*と呼ばれています。</span><span class="sxs-lookup"><span data-stu-id="a06a5-129">These cards are called *simple cards* in Teams.</span></span>

<span data-ttu-id="a06a5-130">Teams のボットは、任意の種類のカードを使用できます: simple、connector、またはアダプティブ。</span><span class="sxs-lookup"><span data-stu-id="a06a5-130">Bots in Teams can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="a06a5-131">Teams の bot がサポートするカードについては、 [Teams カードリファレンスを参照](~/task-modules-and-cards/cards/cards-reference.md)してください。</span><span class="sxs-lookup"><span data-stu-id="a06a5-131">Cards that are supported by bots in Teams are detailed in [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>  

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="a06a5-132">メッセージング拡張機能のカード</span><span class="sxs-lookup"><span data-stu-id="a06a5-132">Cards in Messaging Extensions</span></span>

<span data-ttu-id="a06a5-133">[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)もカードを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="a06a5-133">[Messaging Extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="a06a5-134">メッセージング拡張機能では、シンプル、コネクタ、またはアダプティブのいずれの種類のカードでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="a06a5-134">Messaging extensions can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="a06a5-135">これらのカードは[Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)に掲載されています。</span><span class="sxs-lookup"><span data-stu-id="a06a5-135">These cards are found in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="card-reference"></a><span data-ttu-id="a06a5-136">カードリファレンス</span><span class="sxs-lookup"><span data-stu-id="a06a5-136">Card reference</span></span>

<span data-ttu-id="a06a5-137">Teams で使用されるすべてのカードは[Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)に記載されています。</span><span class="sxs-lookup"><span data-stu-id="a06a5-137">All cards used by Teams are listed in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="a06a5-138">このリファレンスでは、Teams の Bot フレームワークカードとカードの相違点についても説明します。</span><span class="sxs-lookup"><span data-stu-id="a06a5-138">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>
