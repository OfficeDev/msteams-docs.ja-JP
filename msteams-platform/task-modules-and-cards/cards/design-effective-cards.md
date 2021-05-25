---
title: アプリのアダプティブ カードの設計
description: ユーザー向けアダプティブ カードを設計し、Teams UI キットMicrosoft Teamsする方法について学習します。
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b4d5f43268c7bd5afecb56d26eb0d49ed6c9002b
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630281"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="d07f3-103">アプリのアダプティブ カードMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="d07f3-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="d07f3-104">アダプティブ カードには、カード要素のフリーフォーム本文とオプションのアクション セットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="d07f3-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="d07f3-105">アダプティブ カードは、ボットまたはメッセージング拡張機能を介して会話に追加できる、アクション可能なコンテンツのスニペットです。</span><span class="sxs-lookup"><span data-stu-id="d07f3-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="d07f3-106">テキスト、グラフィックス、およびボタンを使用して、これらのカードはユーザーに豊富なコミュニケーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="d07f3-107">アダプティブ カード フレームワークは、さまざまな Microsoft 製品で使用されます。このフレームワークは、Teams。</span><span class="sxs-lookup"><span data-stu-id="d07f3-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="d07f3-108">メッセージ内のカードは、ボットまたはメッセージング拡張機能を介してユーザーに送信できます。</span><span class="sxs-lookup"><span data-stu-id="d07f3-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="d07f3-109">ユーザーは、存在する場合にカードに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="d07f3-109">Users can also take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="アダプティブ カードの概要の例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d07f3-111">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="d07f3-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d07f3-112">アダプティブ カードのより包括的な設計ガイドラインについては、Teams の UI キットで、必要に応じて取得および変更できる要素を含む、Microsoft Teamsをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="d07f3-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="d07f3-113">UI キットでは、テーマ、アクセシビリティ、応答性のサイジングなどの重要なトピックも扱います。</span><span class="sxs-lookup"><span data-stu-id="d07f3-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d07f3-114">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="d07f3-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="d07f3-115">アダプティブ カード デザイナー</span><span class="sxs-lookup"><span data-stu-id="d07f3-115">Adaptive Cards designer</span></span>

<span data-ttu-id="d07f3-116">アダプティブ カードの設計をブラウザーで直接開始することもできます。</span><span class="sxs-lookup"><span data-stu-id="d07f3-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d07f3-117">アダプティブ カード デザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="d07f3-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="d07f3-118">アダプティブ カードの種類</span><span class="sxs-lookup"><span data-stu-id="d07f3-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="d07f3-119">ヒーロー</span><span class="sxs-lookup"><span data-stu-id="d07f3-119">Hero</span></span>

<span data-ttu-id="d07f3-120">最大のカード。</span><span class="sxs-lookup"><span data-stu-id="d07f3-120">Our largest card.</span></span> <span data-ttu-id="d07f3-121">画像がほとんどのストーリーを伝える記事やシナリオを共有するために使用します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-122">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-122">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="アダプティブ カードのヒーロー カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-124">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-124">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="例は、モバイルでのアダプティブ カードのヒーロー カードを示しています。" border="false":::

---

### <a name="thumbnail"></a><span data-ttu-id="d07f3-126">サムネイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-126">Thumbnail</span></span>

<span data-ttu-id="d07f3-127">単純な操作可能なメッセージの送信に使用します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-127">Use for sending a simple actionable message.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-128">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-128">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="アダプティブ カードのサムネイル カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-130">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="例では、モバイルでアダプティブ カードのサムネイル カードを表示します。" border="false":::

---

### <a name="list"></a><span data-ttu-id="d07f3-132">List</span><span class="sxs-lookup"><span data-stu-id="d07f3-132">List</span></span>

<span data-ttu-id="d07f3-133">ユーザーがリストからアイテムを選択するシナリオで使用しますが、項目に多くの説明は必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d07f3-133">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-134">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-134">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="アダプティブ カードリスト カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-136">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-136">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="例は、モバイル上のアダプティブ カード リスト カードを示しています。" border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a><span data-ttu-id="d07f3-138">メディア</span><span class="sxs-lookup"><span data-stu-id="d07f3-138">Media</span></span>

<span data-ttu-id="d07f3-139">オーディオやビデオなど、テキストとメディアを組み合わせる場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-139">Use when you want to combine text and media, like audio or video.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-140">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-140">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="アダプティブ カード メディア カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-142">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-142">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="例は、モバイル上のアダプティブ カード メディア カードを示しています。" border="false":::

---

### <a name="people"></a><span data-ttu-id="d07f3-144">連絡先</span><span class="sxs-lookup"><span data-stu-id="d07f3-144">People</span></span>

<span data-ttu-id="d07f3-145">タスクに関わるユーザーを効率的に伝える場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="d07f3-145">Best used when you to efficiently convey who's involved with a task.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-146">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="アダプティブ カードのユーザー カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-148">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="例は、モバイル上のアダプティブ カードのユーザー カードを示しています。" border="false":::

---

### <a name="request-ticket"></a><span data-ttu-id="d07f3-150">チケットの要求</span><span class="sxs-lookup"><span data-stu-id="d07f3-150">Request ticket</span></span>

<span data-ttu-id="d07f3-151">タスクまたはチケットを自動的に作成するために、ユーザーからのクイック入力を取得するために使用します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-151">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-152">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="アダプティブ カード要求チケット カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-154">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="例は、モバイル上のアダプティブ カード要求チケット カードを示しています。" border="false":::

---

### <a name="image-set"></a><span data-ttu-id="d07f3-156">イメージ セット</span><span class="sxs-lookup"><span data-stu-id="d07f3-156">Image set</span></span>

<span data-ttu-id="d07f3-157">複数の画像サムネイルを送信する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-157">Use to send multiple image thumbnails.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-158">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="アダプティブ カードイメージ セット カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-160">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="例は、モバイル上のアダプティブ カード イメージ セット カードを示しています。" border="false":::

---

### <a name="action-set"></a><span data-ttu-id="d07f3-162">アクション セット</span><span class="sxs-lookup"><span data-stu-id="d07f3-162">Action set</span></span>

<span data-ttu-id="d07f3-163">ユーザーがボタンを選択し、追加ユーザー入力を同じカードから収集する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-163">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-164">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-164">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="アダプティブ カード アクション セット カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-166">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-166">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="例は、モバイル上のアダプティブ カード アクション セット カードを示しています。" border="false":::

---

### <a name="choice-set"></a><span data-ttu-id="d07f3-168">選択肢セット</span><span class="sxs-lookup"><span data-stu-id="d07f3-168">Choice set</span></span>

<span data-ttu-id="d07f3-169">ユーザーから複数の入力を収集するために使用します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-169">Use to gather multiple inputs from the user.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-170">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="アダプティブ カードの選択肢セット カードの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-172">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="例は、モバイル上のアダプティブ カード選択セット カードを示しています。" border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="d07f3-174">構造</span><span class="sxs-lookup"><span data-stu-id="d07f3-174">Anatomy</span></span>

<span data-ttu-id="d07f3-175">アダプティブ カードには多くの柔軟性があります。</span><span class="sxs-lookup"><span data-stu-id="d07f3-175">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="d07f3-176">ただし、少なくとも、すべてのカードに次のコンポーネントを含め、強く提案します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-176">But at minimum, we strongly suggest including the following components in every card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d07f3-177">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d07f3-177">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="EExample はアダプティブ カードの構造を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d07f3-179">モバイル</span><span class="sxs-lookup"><span data-stu-id="d07f3-179">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="例は、モバイルでのアダプティブ カードの構造を示しています。" border="false":::

---

|<span data-ttu-id="d07f3-181">カウンター</span><span class="sxs-lookup"><span data-stu-id="d07f3-181">Counter</span></span>|<span data-ttu-id="d07f3-182">説明</span><span class="sxs-lookup"><span data-stu-id="d07f3-182">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d07f3-183">A</span><span class="sxs-lookup"><span data-stu-id="d07f3-183">A</span></span>|<span data-ttu-id="d07f3-184">**ヘッダー**: ヘッダーを明確かつ簡潔にします。</span><span class="sxs-lookup"><span data-stu-id="d07f3-184">**Header**: Make your headers clear and concise.</span></span>|
|<span data-ttu-id="d07f3-185">B</span><span class="sxs-lookup"><span data-stu-id="d07f3-185">B</span></span>|<span data-ttu-id="d07f3-186">**本文コピー**: ヘッダーに含めるほど長すぎるか、重要ではない詳細を伝える。</span><span class="sxs-lookup"><span data-stu-id="d07f3-186">**Body copy**: Convey details that are either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="d07f3-187">C</span><span class="sxs-lookup"><span data-stu-id="d07f3-187">C</span></span>|<span data-ttu-id="d07f3-188">**主なアクション**: ベスト プラクティスとして、1 ~ 3 の主なアクションを含める。</span><span class="sxs-lookup"><span data-stu-id="d07f3-188">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="d07f3-189">最大 6 個まで使用できます。</span><span class="sxs-lookup"><span data-stu-id="d07f3-189">You can have up to six.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="d07f3-190">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="d07f3-190">Best practices</span></span>

<span data-ttu-id="d07f3-191">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="d07f3-191">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="d07f3-192">プライマリアクションとセカンダリ アクション</span><span class="sxs-lookup"><span data-stu-id="d07f3-192">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブ カードにアクションの小さなセットのみを含める方法に関するベスト プラクティス。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="d07f3-194">Do: 最大 6 つのプライマリ アクションを使用する</span><span class="sxs-lookup"><span data-stu-id="d07f3-194">Do: Use up to six primary actions</span></span>

<span data-ttu-id="d07f3-195">アダプティブ カードは 6 つの主なアクションをサポートすることができますが、ほとんどのカードでは必要とされていません。</span><span class="sxs-lookup"><span data-stu-id="d07f3-195">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="d07f3-196">アクションは明確で簡潔で、簡単に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="d07f3-196">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="d07f3-197">より少ない方が多い。</span><span class="sxs-lookup"><span data-stu-id="d07f3-197">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブ カードのアクションが多すぎるとユーザーを圧倒しない方法に関するベスト プラクティス。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="d07f3-199">[しない]: 6 つ以上の主なアクションを使用する</span><span class="sxs-lookup"><span data-stu-id="d07f3-199">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="d07f3-200">アダプティブ カードは、迅速で操作可能なコンテンツを提示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d07f3-200">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="d07f3-201">アクションが多すぎると、ユーザーが圧倒される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d07f3-201">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="d07f3-202">Frequency</span><span class="sxs-lookup"><span data-stu-id="d07f3-202">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブ カードの頻度に関するベスト プラクティス。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="d07f3-204">Do: 簡潔に</span><span class="sxs-lookup"><span data-stu-id="d07f3-204">Do: Be concise</span></span>

<span data-ttu-id="d07f3-205">複数のカードを会話に送信するのは簡単ですが、カードが表示から外にスクロールすると、あまり役に立たなくなります。</span><span class="sxs-lookup"><span data-stu-id="d07f3-205">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="d07f3-206">自分を必需品に限定してみてください。</span><span class="sxs-lookup"><span data-stu-id="d07f3-206">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="d07f3-207">これは、ユーザーが "ノイズ" と認識する値に対する許容度が低いチャネルでは特に当てはまる。</span><span class="sxs-lookup"><span data-stu-id="d07f3-207">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
