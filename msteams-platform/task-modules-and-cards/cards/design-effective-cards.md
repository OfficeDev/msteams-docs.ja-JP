---
title: アプリのアダプティブ カードの設計
description: ユーザー向けアダプティブ カードを設計し、Teams UI キットMicrosoft Teamsする方法について学習します。
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 14ffff1264e716e04a1ffb5549b71a8b7ec5fc14
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101738"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="3d877-103">アプリのアダプティブ カードMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="3d877-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="3d877-104">アダプティブ カードには、カード要素のフリーフォーム本文とオプションのアクション セットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3d877-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="3d877-105">アダプティブ カードは、ボットまたはメッセージング拡張機能を介して会話に追加できる、アクション可能なコンテンツのスニペットです。</span><span class="sxs-lookup"><span data-stu-id="3d877-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="3d877-106">テキスト、グラフィックス、およびボタンを使用して、これらのカードはユーザーに豊富なコミュニケーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="3d877-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="3d877-107">アダプティブ カード フレームワークは、さまざまな Microsoft 製品で使用されます。このフレームワークは、Teams。</span><span class="sxs-lookup"><span data-stu-id="3d877-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="3d877-108">メッセージ内のカードは、ボットまたはメッセージング拡張機能を介してユーザーに送信できます。</span><span class="sxs-lookup"><span data-stu-id="3d877-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="3d877-109">ユーザーは、存在する場合にカードに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="3d877-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="アダプティブ カードの概要の例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="3d877-111">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="3d877-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3d877-112">アダプティブ カードのより包括的な設計ガイドラインについては、Teams の UI キットで、必要に応じて取得および変更できる要素を含む、Microsoft Teamsをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3d877-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="3d877-113">UI キットでは、テーマ、アクセシビリティ、応答性のサイジングなどの重要なトピックも扱います。</span><span class="sxs-lookup"><span data-stu-id="3d877-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3d877-114">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="3d877-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="3d877-115">アダプティブ カード デザイナー</span><span class="sxs-lookup"><span data-stu-id="3d877-115">Adaptive Cards designer</span></span>

<span data-ttu-id="3d877-116">アダプティブ カードの設計をブラウザーで直接開始することもできます。</span><span class="sxs-lookup"><span data-stu-id="3d877-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3d877-117">アダプティブ カード デザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="3d877-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="3d877-118">アダプティブ カードの種類</span><span class="sxs-lookup"><span data-stu-id="3d877-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="3d877-119">ヒーロー</span><span class="sxs-lookup"><span data-stu-id="3d877-119">Hero</span></span>

<span data-ttu-id="3d877-120">最大のカード。</span><span class="sxs-lookup"><span data-stu-id="3d877-120">Our largest card.</span></span> <span data-ttu-id="3d877-121">画像がほとんどのストーリーを伝える記事やシナリオを共有するために使用します。</span><span class="sxs-lookup"><span data-stu-id="3d877-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="アダプティブ カードのヒーロー カードの例を示します。" border="false":::

### <a name="thumbnail"></a><span data-ttu-id="3d877-123">サムネイル</span><span class="sxs-lookup"><span data-stu-id="3d877-123">Thumbnail</span></span>

<span data-ttu-id="3d877-124">単純な操作可能なメッセージの送信に使用します。</span><span class="sxs-lookup"><span data-stu-id="3d877-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="アダプティブ カードのサムネイル カードの例を示します。" border="false":::

### <a name="list"></a><span data-ttu-id="3d877-126">List</span><span class="sxs-lookup"><span data-stu-id="3d877-126">List</span></span>

<span data-ttu-id="3d877-127">ユーザーがリストからアイテムを選択するシナリオで使用しますが、項目に多くの説明は必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3d877-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="アダプティブ カードリスト カードの例を示します。" border="false":::

### <a name="digest"></a><span data-ttu-id="3d877-129">Digest</span><span class="sxs-lookup"><span data-stu-id="3d877-129">Digest</span></span>

<span data-ttu-id="3d877-130">ニュース ダイジェストと丸め投稿に使用します。</span><span class="sxs-lookup"><span data-stu-id="3d877-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="3d877-131">注: 1 つの更新またはニュース アイテムのサムネイル カードをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3d877-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="アダプティブ カードダイジェスト カードの例を示します。" border="false":::

### <a name="media"></a><span data-ttu-id="3d877-133">メディア</span><span class="sxs-lookup"><span data-stu-id="3d877-133">Media</span></span>

<span data-ttu-id="3d877-134">オーディオやビデオなど、テキストとメディアを組み合わせる場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="3d877-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="アダプティブ カード メディア カードの例を示します。" border="false":::

### <a name="people"></a><span data-ttu-id="3d877-136">ユーザー</span><span class="sxs-lookup"><span data-stu-id="3d877-136">People</span></span>

<span data-ttu-id="3d877-137">タスクに関わるユーザーを効率的に伝える場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="3d877-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="アダプティブ カードのユーザー カードの例を示します。" border="false":::

### <a name="request-ticket"></a><span data-ttu-id="3d877-139">チケットの要求</span><span class="sxs-lookup"><span data-stu-id="3d877-139">Request ticket</span></span>

<span data-ttu-id="3d877-140">タスクまたはチケットを自動的に作成するために、ユーザーからのクイック入力を取得するために使用します。</span><span class="sxs-lookup"><span data-stu-id="3d877-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="アダプティブ カード要求チケット カードの例を示します。" border="false":::

### <a name="imageset"></a><span data-ttu-id="3d877-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="3d877-142">ImageSet</span></span>

<span data-ttu-id="3d877-143">複数の画像サムネイルを送信する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="3d877-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="アダプティブ カードイメージ セット カードの例を示します。" border="false":::

### <a name="actionset"></a><span data-ttu-id="3d877-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="3d877-145">ActionSet</span></span>

<span data-ttu-id="3d877-146">ユーザーがボタンを選択し、追加ユーザー入力を同じカードから収集する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="3d877-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="アダプティブ カード アクション セット カードの例を示します。" border="false":::

### <a name="choiceset"></a><span data-ttu-id="3d877-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="3d877-148">ChoiceSet</span></span>

<span data-ttu-id="3d877-149">ユーザーから複数の入力を収集するために使用します。</span><span class="sxs-lookup"><span data-stu-id="3d877-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="アダプティブ カードの選択肢セット カードの例を示します。" border="false":::

## <a name="anatomy"></a><span data-ttu-id="3d877-151">構造</span><span class="sxs-lookup"><span data-stu-id="3d877-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="例は、アダプティブ カードの解剖学カードを示しています。" border="false":::

<span data-ttu-id="3d877-153">アダプティブ カードには多くの柔軟性があります。</span><span class="sxs-lookup"><span data-stu-id="3d877-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="3d877-154">ただし、少なくとも、すべてのカードに次のコンポーネントを含め、強く推奨します。</span><span class="sxs-lookup"><span data-stu-id="3d877-154">But at minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="3d877-155">カウンター</span><span class="sxs-lookup"><span data-stu-id="3d877-155">Counter</span></span>|<span data-ttu-id="3d877-156">説明</span><span class="sxs-lookup"><span data-stu-id="3d877-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3d877-157">A</span><span class="sxs-lookup"><span data-stu-id="3d877-157">A</span></span>|<span data-ttu-id="3d877-158">**ヘッダー**: ヘッダーを明確かつ簡潔にし、説明的にします。</span><span class="sxs-lookup"><span data-stu-id="3d877-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="3d877-159">B</span><span class="sxs-lookup"><span data-stu-id="3d877-159">B</span></span>|<span data-ttu-id="3d877-160">**本文コピー**: ヘッダーに含めるほど長すぎるか、重要ではない詳細を伝えるために使用します。</span><span class="sxs-lookup"><span data-stu-id="3d877-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="3d877-161">C</span><span class="sxs-lookup"><span data-stu-id="3d877-161">C</span></span>|<span data-ttu-id="3d877-162">**主なアクション**: ベスト プラクティスとして、1 ~ 3 の主なアクションを含める。</span><span class="sxs-lookup"><span data-stu-id="3d877-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="3d877-163">最大 6 個まで使用できます。</span><span class="sxs-lookup"><span data-stu-id="3d877-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="3d877-164">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="3d877-164">Best practices</span></span>

<span data-ttu-id="3d877-165">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="3d877-165">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="3d877-166">プライマリアクションとセカンダリ アクション</span><span class="sxs-lookup"><span data-stu-id="3d877-166">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブ カードにアクションの小さなセットのみを含める方法に関するベスト プラクティス。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="3d877-168">Do: 最大 6 つのプライマリ アクションを使用する</span><span class="sxs-lookup"><span data-stu-id="3d877-168">Do: Use up to six primary actions</span></span>

<span data-ttu-id="3d877-169">アダプティブ カードは 6 つの主なアクションをサポートすることができますが、ほとんどのカードでは必要とされていません。</span><span class="sxs-lookup"><span data-stu-id="3d877-169">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="3d877-170">アクションは明確で簡潔で、簡単に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d877-170">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="3d877-171">より少ない方が多い。</span><span class="sxs-lookup"><span data-stu-id="3d877-171">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブ カードのアクションが多すぎるとユーザーを圧倒しない方法に関するベスト プラクティス。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="3d877-173">[しない]: 6 つ以上の主なアクションを使用する</span><span class="sxs-lookup"><span data-stu-id="3d877-173">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="3d877-174">アダプティブ カードは、迅速で操作可能なコンテンツを提示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d877-174">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="3d877-175">アクションが多すぎると、ユーザーが圧倒される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3d877-175">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="3d877-176">Frequency</span><span class="sxs-lookup"><span data-stu-id="3d877-176">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブ カードの頻度に関するベスト プラクティス。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="3d877-178">Do: 簡潔に</span><span class="sxs-lookup"><span data-stu-id="3d877-178">Do: Be concise</span></span>

<span data-ttu-id="3d877-179">複数のカードを会話に送信するのは簡単ですが、カードが表示から外にスクロールすると、あまり役に立たなくなります。</span><span class="sxs-lookup"><span data-stu-id="3d877-179">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="3d877-180">自分を必需品に限定してみてください。</span><span class="sxs-lookup"><span data-stu-id="3d877-180">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="3d877-181">これは、ユーザーが "ノイズ" と認識する値に対する許容度が低いチャネルでは特に当てはまる。</span><span class="sxs-lookup"><span data-stu-id="3d877-181">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
