---
title: アプリのアダプティブ カードのデザイン
description: Teams のアダプティブ カードをデザインして、Microsoft Teams UI Kit を取得するする方法を説明します。
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8e56928da44e22006feb59715c8bdbf821ec4c42
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037657"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="e630e-103">Microsoft Teams のアプリのアダプティブ カードの設計</span><span class="sxs-lookup"><span data-stu-id="e630e-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="e630e-104">アダプティブ カードには、カード要素のフリーフォーム本体とオプションのアクション セットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e630e-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="e630e-105">アダプティブ カードは、ボットまたはメッセージングの拡張機能を介してスレッドに追加できる、アクション可能なコンテンツのスニペットです。</span><span class="sxs-lookup"><span data-stu-id="e630e-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="e630e-106">これらのカードは、テキスト、グラフィック、ボタンを使用して、対象ユーザーにリッチなコミュニケーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="e630e-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="e630e-107">アダプティブ カード フレームワークは、Teams を含む多くの Microsoft 製品で使用されています。</span><span class="sxs-lookup"><span data-stu-id="e630e-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="e630e-108">メッセージ内のカードは、ボットまたはメッセージングの拡張機能を介してユーザーに送信できます。</span><span class="sxs-lookup"><span data-stu-id="e630e-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="e630e-109">ユーザーは、カードが存在する場合、カードに対してアクションを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="e630e-109">Users can also take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="アダプティブ カードの概要の例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="e630e-111">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="e630e-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="e630e-112">Microsoft Teams UI Kit には、必要に応じて変更できる要素を含む、Teams のアダプティブ カードに関するより包括的なデザイン ガイドラインが掲載されています。</span><span class="sxs-lookup"><span data-stu-id="e630e-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="e630e-113">UI キットには、テーマ、アクセシビリティ、応答性の高いサイズ設定などの重要なトピックも含まれています。</span><span class="sxs-lookup"><span data-stu-id="e630e-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e630e-114">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="e630e-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="e630e-115">アダプティブ カード デザイナー。</span><span class="sxs-lookup"><span data-stu-id="e630e-115">Adaptive Cards designer</span></span>

<span data-ttu-id="e630e-116">ブラウザーで直接アダプティブ カードのデザインを開始することもできます。</span><span class="sxs-lookup"><span data-stu-id="e630e-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e630e-117">アダプティブ カード デザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="e630e-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="e630e-118">アダプティブ カードの種類</span><span class="sxs-lookup"><span data-stu-id="e630e-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="e630e-119">ヒーロー</span><span class="sxs-lookup"><span data-stu-id="e630e-119">Hero</span></span>

<span data-ttu-id="e630e-120">私たちの最大のカードです。</span><span class="sxs-lookup"><span data-stu-id="e630e-120">Our largest card.</span></span> <span data-ttu-id="e630e-121">画像がストーリーのほぼ全容を伝える記事やシナリオの共有に使用します。</span><span class="sxs-lookup"><span data-stu-id="e630e-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-122">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-122">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="アダプティブ カードのヒーロー カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-124">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-124">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="モバイルでのアダプティブ カード ヒーロー カードの例を示します。" border="false":::

---

### <a name="thumbnail"></a><span data-ttu-id="e630e-126">サムネイル</span><span class="sxs-lookup"><span data-stu-id="e630e-126">Thumbnail</span></span>

<span data-ttu-id="e630e-127">単純な、アクション可能なメッセージを送信するために使用します。</span><span class="sxs-lookup"><span data-stu-id="e630e-127">Use for sending a simple actionable message.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-128">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-128">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="アダプティブ カードのサムネイル カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-130">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="モバイルでのアダプティブ カードのサムネイル カードの例を示します。" border="false":::

---

### <a name="list"></a><span data-ttu-id="e630e-132">リスト</span><span class="sxs-lookup"><span data-stu-id="e630e-132">List</span></span>

<span data-ttu-id="e630e-133">ユーザーにリストから項目を選択してもらいたいが、項目に多くの説明は必要ないシナリオで使用します。</span><span class="sxs-lookup"><span data-stu-id="e630e-133">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-134">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-134">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="アダプティブ カードのリスト カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-136">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-136">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="モバイルでのアダプティブ カードのリスト カードの例を示します。" border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a><span data-ttu-id="e630e-138">メディア</span><span class="sxs-lookup"><span data-stu-id="e630e-138">Media</span></span>

<span data-ttu-id="e630e-139">オーディオやビデオなどのテキストとメディアを組み合わせたい場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="e630e-139">Use when you want to combine text and media, like audio or video.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-140">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-140">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="アダプティブ カードのメディア カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-142">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-142">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="モバイルでのアダプティブ カードのメディア カードの例を示します。" border="false":::

---

### <a name="people"></a><span data-ttu-id="e630e-144">連絡先</span><span class="sxs-lookup"><span data-stu-id="e630e-144">People</span></span>

<span data-ttu-id="e630e-145">タスクに関係するユーザーを効率的に伝える場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="e630e-145">Best used when you to efficiently convey who's involved with a task.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-146">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="アダプティブ カードの連絡先カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-148">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="モバイルでのアダプティブ カードの連絡先カードの例を示します。" border="false":::

---

### <a name="request-ticket"></a><span data-ttu-id="e630e-150">要求チケット</span><span class="sxs-lookup"><span data-stu-id="e630e-150">Request ticket</span></span>

<span data-ttu-id="e630e-151">ユーザーから簡単な入力を取得して、タスクまたはチケットを自動的に作成するために使用します。</span><span class="sxs-lookup"><span data-stu-id="e630e-151">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-152">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="アダプティブ カードの要求チケット カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-154">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="モバイルでのアダプティブ カードの要求チケット カードの例を示します。" border="false":::

---

### <a name="image-set"></a><span data-ttu-id="e630e-156">イメージ</span><span class="sxs-lookup"><span data-stu-id="e630e-156">Image set</span></span>

<span data-ttu-id="e630e-157">複数の画像サムネイルを送信するために使用します。</span><span class="sxs-lookup"><span data-stu-id="e630e-157">Use to send multiple image thumbnails.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-158">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="アダプティブ カードの画像セット カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-160">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="モバイルでのアダプティブ カードの画像セット カードの例を示します。" border="false":::

---

### <a name="action-set"></a><span data-ttu-id="e630e-162">アクション セット</span><span class="sxs-lookup"><span data-stu-id="e630e-162">Action set</span></span>

<span data-ttu-id="e630e-163">ユーザーにボタンを選択してもらい、同じカードから追加のユーザー入力を収集する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="e630e-163">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-164">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-164">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="アダプティブ カードのアクション セット カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-166">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-166">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="モバイルでのアダプティブ カードのアクション セット カードの例を示します。" border="false":::

---

### <a name="choice-set"></a><span data-ttu-id="e630e-168">選択肢セット</span><span class="sxs-lookup"><span data-stu-id="e630e-168">Choice set</span></span>

<span data-ttu-id="e630e-169">ユーザーから複数の入力を収集するために使用します。</span><span class="sxs-lookup"><span data-stu-id="e630e-169">Use to gather multiple inputs from the user.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-170">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="アダプティブ カードの選択肢セット カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-172">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="モバイルでのアダプティブ カードの選択肢セット カードの例を示します。" border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="e630e-174">構造</span><span class="sxs-lookup"><span data-stu-id="e630e-174">Anatomy</span></span>

<span data-ttu-id="e630e-175">アダプティブ カードの柔軟性は高いです。</span><span class="sxs-lookup"><span data-stu-id="e630e-175">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="e630e-176">ただし、少なくとも、すべてのカードに次のコンポーネントを含めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e630e-176">But at minimum, we strongly suggest including the following components in every card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e630e-177">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e630e-177">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="アダプティブ カードの構造の例を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e630e-179">モバイル</span><span class="sxs-lookup"><span data-stu-id="e630e-179">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="モバイルでのアダプティブ カードの構造の例を示しています。" border="false":::

---

|<span data-ttu-id="e630e-181">カウンター</span><span class="sxs-lookup"><span data-stu-id="e630e-181">Counter</span></span>|<span data-ttu-id="e630e-182">説明</span><span class="sxs-lookup"><span data-stu-id="e630e-182">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="e630e-183">A</span><span class="sxs-lookup"><span data-stu-id="e630e-183">A</span></span>|<span data-ttu-id="e630e-184">**ヘッダー**: ヘッダーを明確かつ簡潔にします。</span><span class="sxs-lookup"><span data-stu-id="e630e-184">**Header**: Make your headers clear and concise.</span></span>|
|<span data-ttu-id="e630e-185">B</span><span class="sxs-lookup"><span data-stu-id="e630e-185">B</span></span>|<span data-ttu-id="e630e-186">**本文のコピー**: ヘッダーに含めるには長すぎるか、ヘッダーに含めるほど重要ではない詳細を伝えます。</span><span class="sxs-lookup"><span data-stu-id="e630e-186">**Body copy**: Convey details that are either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="e630e-187">C</span><span class="sxs-lookup"><span data-stu-id="e630e-187">C</span></span>|<span data-ttu-id="e630e-188">**プライマリ アクション**: ベスト プラクティスとして、1 ~ 3 個のプライマリ アクションを含めます。</span><span class="sxs-lookup"><span data-stu-id="e630e-188">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="e630e-189">グループには最大 6 個のコントロールを指定できます。</span><span class="sxs-lookup"><span data-stu-id="e630e-189">You can have up to six.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="e630e-190">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="e630e-190">Best practices</span></span>

<span data-ttu-id="e630e-191">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="e630e-191">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="e630e-192">プライマリとセカンダリ</span><span class="sxs-lookup"><span data-stu-id="e630e-192">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブ カードに少数のアクションのみを含める方法に関するベスト プラクティス。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="e630e-194">Do: 最大 6 つの主要なアクションを使用します</span><span class="sxs-lookup"><span data-stu-id="e630e-194">Do: Use up to six primary actions</span></span>

<span data-ttu-id="e630e-195">アダプティブ カードは 6 つの主要なアクションをサポートできますが、ほとんどのカードではそれを必要としません。</span><span class="sxs-lookup"><span data-stu-id="e630e-195">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="e630e-196">アクションは明確で簡潔で率直なものである必要があります。</span><span class="sxs-lookup"><span data-stu-id="e630e-196">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="e630e-197">少なければ少ない方がいいです。</span><span class="sxs-lookup"><span data-stu-id="e630e-197">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブ カードに対するアクションが多すぎてユーザーに負荷をかけないようにする方法についてのベスト プラクティスです。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="e630e-199">Don't: 6 つ以上のプライマリ アクションを使用しないでください</span><span class="sxs-lookup"><span data-stu-id="e630e-199">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="e630e-200">アダプティブ カードは、迅速で実用的なコンテンツを提示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e630e-200">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="e630e-201">アクションが多すぎると、ユーザーの負担になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e630e-201">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="e630e-202">頻度</span><span class="sxs-lookup"><span data-stu-id="e630e-202">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブ カードの頻度に関するベスト プラクティス。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="e630e-204">Do: 簡潔にしてください</span><span class="sxs-lookup"><span data-stu-id="e630e-204">Do: Be concise</span></span>

<span data-ttu-id="e630e-205">スレッドに複数のカードを送信するのは簡単ですが、スクロールしてカードが見えなくなると、役に立たなくなります。</span><span class="sxs-lookup"><span data-stu-id="e630e-205">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="e630e-206">必須項目にのみ制限するようにしてください。</span><span class="sxs-lookup"><span data-stu-id="e630e-206">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="e630e-207">これは、ユーザーが "ノイズ" と認識する内容に対する許容度が低いチャネルでは特に当てはまります。</span><span class="sxs-lookup"><span data-stu-id="e630e-207">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
