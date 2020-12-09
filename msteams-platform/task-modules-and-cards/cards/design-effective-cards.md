---
title: アプリに適応カードを設計する
description: Teams 用のアダプティブカードを設計し、Microsoft Teams UI キットを取得する方法について説明します。
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bd48846284620415cc8cadabc59f2ab7b61d5189
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604555"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="1c79e-103">Microsoft Teams アプリ用のアダプティブカードの設計</span><span class="sxs-lookup"><span data-stu-id="1c79e-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="1c79e-104">アダプティブカードには、フリーフォームのカード要素と任意のアクションセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1c79e-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="1c79e-105">アダプティブカードは、ボットまたはメッセージング拡張機能を使用して会話に追加できる、実行可能なコンテンツのスニペットです。</span><span class="sxs-lookup"><span data-stu-id="1c79e-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="1c79e-106">これらのカードは、テキスト、グラフィックス、ボタンを使用して、対象ユーザーに豊富なコミュニケーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="1c79e-107">アダプティブカードフレームワークは、Teams を含む多くの Microsoft 製品で使用されています。</span><span class="sxs-lookup"><span data-stu-id="1c79e-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="1c79e-108">Bot またはメッセージング拡張機能を使用して、メッセージ内のカードをユーザーに送信することができます。</span><span class="sxs-lookup"><span data-stu-id="1c79e-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="1c79e-109">ユーザーは、表示されている場合は、カードに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="1c79e-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="1c79e-111">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="1c79e-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="1c79e-112">Microsoft Teams UI キットでは、必要に応じて取得して変更できる要素を含め、Teams のアダプティブカードについて、より包括的な設計ガイドラインを参照できます。</span><span class="sxs-lookup"><span data-stu-id="1c79e-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="1c79e-113">UI キットでは、テーマ、アクセシビリティ、応答性の高いサイズ設定など、重要なトピックについても説明しています。</span><span class="sxs-lookup"><span data-stu-id="1c79e-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c79e-114">Microsoft Teams UI Kit (Figma) を取得する</span><span class="sxs-lookup"><span data-stu-id="1c79e-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="1c79e-115">アダプティブカードデザイナー</span><span class="sxs-lookup"><span data-stu-id="1c79e-115">Adaptive Cards designer</span></span>

<span data-ttu-id="1c79e-116">また、アダプティブカードのデザインをブラウザーで直接開始することもできます。</span><span class="sxs-lookup"><span data-stu-id="1c79e-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c79e-117">アダプティブカードデザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="1c79e-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="1c79e-118">アダプティブカードの種類</span><span class="sxs-lookup"><span data-stu-id="1c79e-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="1c79e-119">ヒーロー</span><span class="sxs-lookup"><span data-stu-id="1c79e-119">Hero</span></span>

<span data-ttu-id="1c79e-120">最大のカード</span><span class="sxs-lookup"><span data-stu-id="1c79e-120">Our largest card.</span></span> <span data-ttu-id="1c79e-121">画像が最も多くの話を伝える記事やシナリオを共有するために使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="thumbnail"></a><span data-ttu-id="1c79e-123">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="1c79e-123">Thumbnail</span></span>

<span data-ttu-id="1c79e-124">簡単な操作可能なメッセージを送信するために使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="list"></a><span data-ttu-id="1c79e-126">リスト</span><span class="sxs-lookup"><span data-stu-id="1c79e-126">List</span></span>

<span data-ttu-id="1c79e-127">ユーザーがリストからアイテムを選択する必要があるが、アイテムには多くの説明は必要ない場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="digest"></a><span data-ttu-id="1c79e-129">Digest</span><span class="sxs-lookup"><span data-stu-id="1c79e-129">Digest</span></span>

<span data-ttu-id="1c79e-130">ニュースダイジェストおよび切り上げられた投稿に使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="1c79e-131">注: 1 つの更新プログラムまたはニュースアイテムには、サムネイルカードをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1c79e-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="media"></a><span data-ttu-id="1c79e-133">メディア</span><span class="sxs-lookup"><span data-stu-id="1c79e-133">Media</span></span>

<span data-ttu-id="1c79e-134">音声やビデオなどのテキストとメディアを結合する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="people"></a><span data-ttu-id="1c79e-136">People</span><span class="sxs-lookup"><span data-stu-id="1c79e-136">People</span></span>

<span data-ttu-id="1c79e-137">タスクに関係する人物を効率的に伝える場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="1c79e-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="request-ticket"></a><span data-ttu-id="1c79e-139">要求チケット</span><span class="sxs-lookup"><span data-stu-id="1c79e-139">Request ticket</span></span>

<span data-ttu-id="1c79e-140">ユーザーからすばやく入力を取得して、タスクまたはチケットを自動的に作成するために使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="imageset"></a><span data-ttu-id="1c79e-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="1c79e-142">ImageSet</span></span>

<span data-ttu-id="1c79e-143">複数の画像のサムネイルを送信するために使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="actionset"></a><span data-ttu-id="1c79e-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="1c79e-145">ActionSet</span></span>

<span data-ttu-id="1c79e-146">ユーザーにボタンを選択させ、そのカードから追加のユーザー入力を収集する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="choiceset"></a><span data-ttu-id="1c79e-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="1c79e-148">ChoiceSet</span></span>

<span data-ttu-id="1c79e-149">ユーザーから複数の入力を収集するために使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

## <a name="anatomy"></a><span data-ttu-id="1c79e-151">構造</span><span class="sxs-lookup"><span data-stu-id="1c79e-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="アダプティブカードの UI の構造を示す図。" border="false":::

<span data-ttu-id="1c79e-153">アダプティブカードには多くの柔軟性があります。</span><span class="sxs-lookup"><span data-stu-id="1c79e-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="1c79e-154">ただし、少なくとも、以下のコンポーネントをすべてのカードに含めることを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1c79e-154">But at a minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="1c79e-155">カウンター</span><span class="sxs-lookup"><span data-stu-id="1c79e-155">Counter</span></span>|<span data-ttu-id="1c79e-156">説明</span><span class="sxs-lookup"><span data-stu-id="1c79e-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1c79e-157">A</span><span class="sxs-lookup"><span data-stu-id="1c79e-157">A</span></span>|<span data-ttu-id="1c79e-158">**ヘッダー**: ヘッダーを明瞭で簡潔なものにします。ただし、わかりやすくする。</span><span class="sxs-lookup"><span data-stu-id="1c79e-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="1c79e-159">B</span><span class="sxs-lookup"><span data-stu-id="1c79e-159">B</span></span>|<span data-ttu-id="1c79e-160">**本文のコピー**: ヘッダーに含めるには、長すぎる、または重要ではない詳細情報を伝達するために使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="1c79e-161">C</span><span class="sxs-lookup"><span data-stu-id="1c79e-161">C</span></span>|<span data-ttu-id="1c79e-162">**主な処置**: ベストプラクティスとして、1-3 プライマリアクションを含めます。</span><span class="sxs-lookup"><span data-stu-id="1c79e-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="1c79e-163">最大6個が許可されます。</span><span class="sxs-lookup"><span data-stu-id="1c79e-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="1c79e-164">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="1c79e-164">Best practices</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="1c79e-165">プライマリおよびセカンダリのアクション</span><span class="sxs-lookup"><span data-stu-id="1c79e-165">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブカードのベストプラクティスを示す例。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="1c79e-167">Do: 最大6つの主要なアクションを使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-167">Do: Use up to six primary actions</span></span>

<span data-ttu-id="1c79e-168">アダプティブカードは6つの主要なアクションをサポートしていますが、ほとんどのカードはそれを必要としません。</span><span class="sxs-lookup"><span data-stu-id="1c79e-168">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="1c79e-169">アクションは、明瞭、簡潔、およびまっすぐに実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1c79e-169">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="1c79e-170">これよりも少なくなります。</span><span class="sxs-lookup"><span data-stu-id="1c79e-170">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブカードのベストプラクティスを示す例。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="1c79e-172">6つ以上の主なアクションを使用します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-172">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="1c79e-173">アダプティブカードは、すぐに実行可能なコンテンツを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1c79e-173">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="1c79e-174">ユーザーが過負荷になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="1c79e-174">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="1c79e-175">Frequency</span><span class="sxs-lookup"><span data-stu-id="1c79e-175">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブカードのベストプラクティスを示す例。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="1c79e-177">実行: 簡潔</span><span class="sxs-lookup"><span data-stu-id="1c79e-177">Do: Be concise</span></span>

<span data-ttu-id="1c79e-178">複数のカードを1つの会話に簡単に送信できますが、カードが表示されなくなると、利便性が低下します。</span><span class="sxs-lookup"><span data-stu-id="1c79e-178">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="1c79e-179">Essentials に制限するようにしてください。</span><span class="sxs-lookup"><span data-stu-id="1c79e-179">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="1c79e-180">これは、ユーザーが "ノイズ" として認識される許容範囲を下回っているチャネルの場合に特に当てはまります。</span><span class="sxs-lookup"><span data-stu-id="1c79e-180">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
