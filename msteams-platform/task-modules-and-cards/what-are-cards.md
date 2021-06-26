---
title: カード
description: カードと、ボット、コネクタ、メッセージング拡張機能でのカードの使い方について説明します。
localization_priority: Normal
keywords: コネクタ ボット カード メッセージング
ms.topic: overview
ms.openlocfilehash: f895423e5755dd85a7618b8907c4c3b0acbc3cf4
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140545"
---
# <a name="cards"></a><span data-ttu-id="e59ad-104">カード</span><span class="sxs-lookup"><span data-stu-id="e59ad-104">Cards</span></span>

<span data-ttu-id="e59ad-105">カードは、短い情報や関連する情報のユーザー インターフェイス (UI) コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="e59ad-105">A card is a user interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="e59ad-106">カードには複数のプロパティと添付ファイルを含め、ボタンを含め、カードアクション [をトリガーできます](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="e59ad-106">Cards can have multiple properties and attachments and can include buttons, which trigger [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span> <span data-ttu-id="e59ad-107">カードを使用して、情報をグループに整理し、ユーザーに情報の特定の部分を操作する機会を与える。</span><span class="sxs-lookup"><span data-stu-id="e59ad-107">Using cards, you can organize information into groups and give users the opportunity to interact with specific parts of the information.</span></span>

<span data-ttu-id="e59ad-108">Teams のボットは、アダプティブ カード、ヒーロー カード、リスト カード、Office 365 コネクタ カード、レシート カード、サインイン カード、サムネイル カード、カード コレクションの種類をサポートします。</span><span class="sxs-lookup"><span data-stu-id="e59ad-108">The bots for Teams support the following types of cards: Adaptive Card, hero card, list card, Office 365 Connector card, receipt card, signin card, thumbnail card, and card collections.</span></span> <span data-ttu-id="e59ad-109">カードの種類に応じて、Markdown または HTML を使用してリッチ テキスト書式をカードに追加できます。</span><span class="sxs-lookup"><span data-stu-id="e59ad-109">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span> <span data-ttu-id="e59ad-110">ボットとメッセージング拡張機能で使用されるカードは、Microsoft Teams、 で、これらのカードアクションに追加して `openUrl` `messageBack` `imBack` `invoke` 応答します `signin` 。</span><span class="sxs-lookup"><span data-stu-id="e59ad-110">Cards used by bots and messaging extensions in Microsoft Teams, add and respond to these card actions, `openUrl`, `messageBack`, `imBack`, `invoke`, and `signin`.</span></span>

<span data-ttu-id="e59ad-111">Teamsは、次の 3 つの異なる場所でカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="e59ad-111">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="e59ad-112">コネクタ</span><span class="sxs-lookup"><span data-stu-id="e59ad-112">Connectors</span></span>
* <span data-ttu-id="e59ad-113">ボット</span><span class="sxs-lookup"><span data-stu-id="e59ad-113">Bots</span></span>
* <span data-ttu-id="e59ad-114">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="e59ad-114">Messaging extensions</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="e59ad-115">コネクタ内のカード</span><span class="sxs-lookup"><span data-stu-id="e59ad-115">Cards in connectors</span></span>

<span data-ttu-id="e59ad-116">カードは、最初に、OutlookおよびOffice 365の一部として定義され、現在はコネクタコネクタのOffice 365されています。</span><span class="sxs-lookup"><span data-stu-id="e59ad-116">Cards were first defined as part of Outlook and Office 365 and are now used as part of Office 365 Connectors.</span></span> <span data-ttu-id="e59ad-117">多くのアプリケーションOffice 365同様に、Teamsをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="e59ad-117">Like many Office 365 applications, Teams supports connectors.</span></span> <span data-ttu-id="e59ad-118">詳細については、「Office 365[コネクタ」を参照Teams。](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="e59ad-118">For more information, see [Office 365 Connectors for Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span> <span data-ttu-id="e59ad-119">コネクタ内のカードの仕様は、アクション可能なメッセージ カード [リファレンスで確認できます](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="e59ad-119">You can find the specification for cards in connectors in [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="e59ad-120">ボット内のカード</span><span class="sxs-lookup"><span data-stu-id="e59ad-120">Cards in bots</span></span>

<span data-ttu-id="e59ad-121">このMicrosoft Bot Framework、ボットがボット メッセージの一部として使用できる定義済みのカードのセットを追加することで、カードの仕様を拡張します。</span><span class="sxs-lookup"><span data-stu-id="e59ad-121">The Microsoft Bot Framework extends the cards specification by adding a set of predefined cards that bots can use as part of bot messages.</span></span> <span data-ttu-id="e59ad-122">Teamsボット フレームワークを使用してボットをサポートしていますが、これらのカードの異なるセットをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="e59ad-122">Teams supports bots using the Bot Framework, but it supports a different set of these cards.</span></span> <span data-ttu-id="e59ad-123">Bot Framework のカードに関する一般的な情報は、メッセージにリッチ カード [添付ファイルを追加するで確認できます](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。</span><span class="sxs-lookup"><span data-stu-id="e59ad-123">General information on cards in Bot Framework can be found in [add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="e59ad-124">これらのカードは、簡易カードと呼ばれるTeams。</span><span class="sxs-lookup"><span data-stu-id="e59ad-124">These cards are called simple cards in Teams.</span></span>

<span data-ttu-id="e59ad-125">ボットはTeamsカード、コネクタ カード、アダプティブ カードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="e59ad-125">Bots in Teams can use simple cards, connector cards, or Adaptive Cards.</span></span> <span data-ttu-id="e59ad-126">[カードの種類は](~/task-modules-and-cards/cards/cards-reference.md)、カードに関する情報を提供します。Teams。</span><span class="sxs-lookup"><span data-stu-id="e59ad-126">[Types of cards](~/task-modules-and-cards/cards/cards-reference.md) provides information on cards, supported by bots in Teams.</span></span>

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="e59ad-127">メッセージング拡張機能のカード</span><span class="sxs-lookup"><span data-stu-id="e59ad-127">Cards in messaging extensions</span></span>

<span data-ttu-id="e59ad-128">[メッセージング拡張機能は、](~/messaging-extensions/what-are-messaging-extensions.md) カードを返す場合があります。</span><span class="sxs-lookup"><span data-stu-id="e59ad-128">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="e59ad-129">メッセージング拡張機能では、単純なカード、コネクタ カード、アダプティブ カードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="e59ad-129">Messaging extensions can use simple cards, connector cards, or Adaptive Cards.</span></span> <span data-ttu-id="e59ad-130">これらのカードは、カード [の種類で見つかりました](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="e59ad-130">These cards are found in [types of cards](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="e59ad-131">カードの種類</span><span class="sxs-lookup"><span data-stu-id="e59ad-131">Types of cards</span></span>

<span data-ttu-id="e59ad-132">ユーザーが使用するTeamsカードの種類[に一覧表示されます](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="e59ad-132">All cards used by Teams are listed in [types of cards](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="e59ad-133">このリファレンスでは、ボット フレームワーク カードとボット フレームワーク カードの違いについて説明Teams。</span><span class="sxs-lookup"><span data-stu-id="e59ad-133">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="e59ad-134">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="e59ad-134">Adaptive Cards</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="e59ad-135">[アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)は、ボット、Cortana、Outlook、および Windows を含む Microsoft 製品の新しいクロス製品仕様です。</span><span class="sxs-lookup"><span data-stu-id="e59ad-135">[Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="e59ad-136">これらは、新しいカード開発に推奨されるTeamsです。</span><span class="sxs-lookup"><span data-stu-id="e59ad-136">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="e59ad-137">アダプティブ カード チームの一般的な情報については、「アダプティブ カード [の概要」を参照してください](/adaptive-cards)。</span><span class="sxs-lookup"><span data-stu-id="e59ad-137">For general information from the Adaptive Cards team, see [Adaptive Cards overview](/adaptive-cards).</span></span> <span data-ttu-id="e59ad-138">アダプティブ カードは、既存のヒーロー カード、Office 365カードを使用する任意の場所で使用できます。</span><span class="sxs-lookup"><span data-stu-id="e59ad-138">You can use Adaptive Cards anywhere you use existing hero cards, Office 365 cards, and thumbnail cards.</span></span>

<span data-ttu-id="e59ad-139">アダプティブ カードに加えて、Teams 2 種類のカードがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="e59ad-139">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="e59ad-140">コネクタ カード: コネクタ コネクタの一Office 365されます。</span><span class="sxs-lookup"><span data-stu-id="e59ad-140">Connector cards: Used as part of Office 365 Connectors.</span></span>
* <span data-ttu-id="e59ad-141">単純なカード: サムネイルカードやヒーロー カードなど、ボット フレームワークから使用されます。</span><span class="sxs-lookup"><span data-stu-id="e59ad-141">Simple cards: Used from the Bot Framework, such as the thumbnail and hero cards.</span></span>

### <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="e59ad-142">アダプティブ カードと受信 Webhooks</span><span class="sxs-lookup"><span data-stu-id="e59ad-142">Adaptive Cards and Incoming Webhooks</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/y5pbJI43Zvg]

> [!NOTE]
> * <span data-ttu-id="e59ad-143">ネイティブのアダプティブ カード スキーマ要素 (ただし `Action.Submit` 、 を除く) はすべて完全にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="e59ad-143">All native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span>
> * <span data-ttu-id="e59ad-144">サポートされているアクションは [**、Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**、Action.ShowCard、Action.ToggleVisibility、**](https://adaptivecards.io/explorer/Action.ShowCard.html)およびAction.Exe [**です**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。 [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)</span><span class="sxs-lookup"><span data-stu-id="e59ad-144">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html), and [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="e59ad-145">受信 Webhook を使用したアダプティブ カードを使用すると、アダプティブ カードの豊富で柔軟な機能を使用できます。</span><span class="sxs-lookup"><span data-stu-id="e59ad-145">Adaptive Cards with Incoming Webhooks enables you to use the rich and flexible capabilities of Adaptive Cards.</span></span> <span data-ttu-id="e59ad-146">Web サービスから受信 Webhooks を使用Teamsデータを送信します。</span><span class="sxs-lookup"><span data-stu-id="e59ad-146">It sends data using Incoming Webhooks in Teams from their web service.</span></span>

## <a name="see-also"></a><span data-ttu-id="e59ad-147">関連項目</span><span class="sxs-lookup"><span data-stu-id="e59ad-147">See also</span></span>

* [<span data-ttu-id="e59ad-148">カードの書式を設定Teams</span><span class="sxs-lookup"><span data-stu-id="e59ad-148">Format cards in Teams</span></span>](~/task-modules-and-cards/cards/cards-format.md)
* [<span data-ttu-id="e59ad-149">アダプティブ カードの設計</span><span class="sxs-lookup"><span data-stu-id="e59ad-149">Design Adaptive Cards</span></span>](~/task-modules-and-cards/cards/design-effective-cards.md)

## <a name="next-step"></a><span data-ttu-id="e59ad-150">次の手順</span><span class="sxs-lookup"><span data-stu-id="e59ad-150">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e59ad-151">カードの種類</span><span class="sxs-lookup"><span data-stu-id="e59ad-151">Types of cards</span></span>](~/task-modules-and-cards/cards/cards-reference.md)