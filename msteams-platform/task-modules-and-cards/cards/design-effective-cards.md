---
title: アプリのアダプティブ カードの設計
description: Teams 用アダプティブ カードを設計し、Microsoft Teams UI キットを取得する方法について説明します。
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 67a2882a0a687d5ccb48759419ecefcdf9396fc3
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020283"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="9fbe8-103">Microsoft Teams アプリのアダプティブ カードの設計</span><span class="sxs-lookup"><span data-stu-id="9fbe8-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="9fbe8-104">アダプティブ カードには、カード要素のフリーフォーム本文とオプションのアクション セットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="9fbe8-105">アダプティブ カードは、ボットまたはメッセージング拡張機能を介して会話に追加できる、アクション可能なコンテンツのスニペットです。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="9fbe8-106">テキスト、グラフィックス、およびボタンを使用して、これらのカードはユーザーに豊富なコミュニケーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="9fbe8-107">アダプティブ カード フレームワークは、Teams を含む多くの Microsoft 製品で使用されます。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="9fbe8-108">メッセージ内のカードは、ボットまたはメッセージング拡張機能を介してユーザーに送信できます。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="9fbe8-109">ユーザーは、存在する場合にカードに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="アダプティブ カードの例を示します。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="9fbe8-111">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="9fbe8-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="9fbe8-112">必要に応じて取得および変更できる要素を含む、Teams のアダプティブ カードのより包括的な設計ガイドラインについては、「Microsoft Teams UI Kit」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="9fbe8-113">UI キットでは、テーマ、アクセシビリティ、応答性のサイジングなどの重要なトピックも扱います。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9fbe8-114">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="9fbe8-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="9fbe8-115">アダプティブ カード デザイナー</span><span class="sxs-lookup"><span data-stu-id="9fbe8-115">Adaptive Cards designer</span></span>

<span data-ttu-id="9fbe8-116">アダプティブ カードの設計をブラウザーで直接開始することもできます。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9fbe8-117">アダプティブ カード デザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="9fbe8-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="9fbe8-118">アダプティブ カードの種類</span><span class="sxs-lookup"><span data-stu-id="9fbe8-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="9fbe8-119">ヒーロー</span><span class="sxs-lookup"><span data-stu-id="9fbe8-119">Hero</span></span>

<span data-ttu-id="9fbe8-120">最大のカード。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-120">Our largest card.</span></span> <span data-ttu-id="9fbe8-121">画像がほとんどのストーリーを伝える記事やシナリオを共有するために使用します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="アダプティブ カードの例を示します。" border="false":::

### <a name="thumbnail"></a><span data-ttu-id="9fbe8-123">サムネイル</span><span class="sxs-lookup"><span data-stu-id="9fbe8-123">Thumbnail</span></span>

<span data-ttu-id="9fbe8-124">単純な操作可能なメッセージの送信に使用します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="アダプティブ カードの例。" border="false":::

### <a name="list"></a><span data-ttu-id="9fbe8-126">一覧表示</span><span class="sxs-lookup"><span data-stu-id="9fbe8-126">List</span></span>

<span data-ttu-id="9fbe8-127">ユーザーがリストからアイテムを選択するシナリオで使用しますが、項目に多くの説明は必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="アダプティブ カードの例。" border="false":::

### <a name="digest"></a><span data-ttu-id="9fbe8-129">ダイジェスト</span><span class="sxs-lookup"><span data-stu-id="9fbe8-129">Digest</span></span>

<span data-ttu-id="9fbe8-130">ニュース ダイジェストと丸め投稿に使用します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="9fbe8-131">注: 1 つの更新またはニュース アイテムのサムネイル カードをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="図はアダプティブ カードを示しています。" border="false":::

### <a name="media"></a><span data-ttu-id="9fbe8-133">メディア</span><span class="sxs-lookup"><span data-stu-id="9fbe8-133">Media</span></span>

<span data-ttu-id="9fbe8-134">オーディオやビデオなど、テキストとメディアを組み合わせる場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="図はアダプティブ カードを示しています。" border="false":::

### <a name="people"></a><span data-ttu-id="9fbe8-136">連絡先</span><span class="sxs-lookup"><span data-stu-id="9fbe8-136">People</span></span>

<span data-ttu-id="9fbe8-137">タスクに関わるユーザーを効率的に伝える場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="アダプティブ カードの図。" border="false":::

### <a name="request-ticket"></a><span data-ttu-id="9fbe8-139">チケットの要求</span><span class="sxs-lookup"><span data-stu-id="9fbe8-139">Request ticket</span></span>

<span data-ttu-id="9fbe8-140">タスクまたはチケットを自動的に作成するために、ユーザーからのクイック入力を取得するために使用します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="アダプティブ カードの図。" border="false":::

### <a name="imageset"></a><span data-ttu-id="9fbe8-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="9fbe8-142">ImageSet</span></span>

<span data-ttu-id="9fbe8-143">複数の画像サムネイルを送信する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="アダプティブ カードのサンプル。" border="false":::

### <a name="actionset"></a><span data-ttu-id="9fbe8-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="9fbe8-145">ActionSet</span></span>

<span data-ttu-id="9fbe8-146">ユーザーがボタンを選択し、追加ユーザー入力を同じカードから収集する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="サンプルはアダプティブ カードを示しています。" border="false":::

### <a name="choiceset"></a><span data-ttu-id="9fbe8-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="9fbe8-148">ChoiceSet</span></span>

<span data-ttu-id="9fbe8-149">ユーザーから複数の入力を収集するために使用します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="アダプティブ カードを表示する例。" border="false":::

## <a name="anatomy"></a><span data-ttu-id="9fbe8-151">構造</span><span class="sxs-lookup"><span data-stu-id="9fbe8-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="アダプティブ カードの UI 構造を示す図。" border="false":::

<span data-ttu-id="9fbe8-153">アダプティブ カードには多くの柔軟性があります。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="9fbe8-154">ただし、少なくとも、すべてのカードに次のコンポーネントを含め、強く推奨します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-154">But at minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="9fbe8-155">カウンター</span><span class="sxs-lookup"><span data-stu-id="9fbe8-155">Counter</span></span>|<span data-ttu-id="9fbe8-156">説明</span><span class="sxs-lookup"><span data-stu-id="9fbe8-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9fbe8-157">A</span><span class="sxs-lookup"><span data-stu-id="9fbe8-157">A</span></span>|<span data-ttu-id="9fbe8-158">**ヘッダー**: ヘッダーを明確かつ簡潔にし、説明的にします。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="9fbe8-159">B</span><span class="sxs-lookup"><span data-stu-id="9fbe8-159">B</span></span>|<span data-ttu-id="9fbe8-160">**本文コピー**: ヘッダーに含めるほど長すぎるか、重要ではない詳細を伝えるために使用します。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="9fbe8-161">C</span><span class="sxs-lookup"><span data-stu-id="9fbe8-161">C</span></span>|<span data-ttu-id="9fbe8-162">**主なアクション**: ベスト プラクティスとして、1 ~ 3 の主なアクションを含める。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="9fbe8-163">最大 6 個まで使用できます。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="9fbe8-164">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="9fbe8-164">Best practices</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="9fbe8-165">プライマリアクションとセカンダリ アクション</span><span class="sxs-lookup"><span data-stu-id="9fbe8-165">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブ カードのベスト プラクティスを示す例。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="9fbe8-167">Do: 最大 6 つのプライマリ アクションを使用する</span><span class="sxs-lookup"><span data-stu-id="9fbe8-167">Do: Use up to six primary actions</span></span>

<span data-ttu-id="9fbe8-168">アダプティブ カードは 6 つの主なアクションをサポートすることができますが、ほとんどのカードでは必要とされていません。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-168">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="9fbe8-169">アクションは明確で簡潔で、簡単に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-169">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="9fbe8-170">より少ない方が多い。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-170">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブ カードのベスト プラクティスの例を示します。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="9fbe8-172">[しない]: 6 つ以上の主なアクションを使用する</span><span class="sxs-lookup"><span data-stu-id="9fbe8-172">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="9fbe8-173">アダプティブ カードは、迅速で操作可能なコンテンツを提示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-173">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="9fbe8-174">アクションが多すぎると、ユーザーが圧倒される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-174">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="9fbe8-175">Frequency</span><span class="sxs-lookup"><span data-stu-id="9fbe8-175">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブ カードのベスト プラクティスを表示する図。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="9fbe8-177">Do: 簡潔に</span><span class="sxs-lookup"><span data-stu-id="9fbe8-177">Do: Be concise</span></span>

<span data-ttu-id="9fbe8-178">複数のカードを会話に送信するのは簡単ですが、カードが表示から外にスクロールすると、あまり役に立たなくなります。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-178">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="9fbe8-179">自分を必需品に限定してみてください。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-179">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="9fbe8-180">これは、ユーザーが "ノイズ" と認識する値に対する許容度が低いチャネルでは特に当てはまる。</span><span class="sxs-lookup"><span data-stu-id="9fbe8-180">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
