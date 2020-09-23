---
title: 効果的なカードを設計する
description: カードを作成するためのデザインガイドラインについて説明します。
keywords: teams 設計ガイドラインリファレンスフレームワークカードのアダプタブルライトウェイト
ms.openlocfilehash: 4ec410820e0288d99dacb6944a8096f4f61b9d34
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209838"
---
# <a name="design-effective-cards"></a><span data-ttu-id="4ed02-104">効果的なカードを設計する</span><span class="sxs-lookup"><span data-stu-id="4ed02-104">Design effective cards</span></span>

<span data-ttu-id="4ed02-105">カードは、ボット、コネクタ、またはアプリを介して会話に追加できる、コンテンツの操作可能なスニペットです。</span><span class="sxs-lookup"><span data-stu-id="4ed02-105">Cards are actionable snippets of content that you can add to a conversation through a bot, a connector, or app.</span></span> <span data-ttu-id="4ed02-106">カードを使用すると、テキスト、グラフィックス、ボタンを使用して、対象ユーザーと通信することができます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-106">Using text, graphics, and buttons, cards allow you to communicate with an audience.</span></span>

<span data-ttu-id="4ed02-107">カードフレームワークは、完全に機能する UX を設計する負担を排除します。</span><span class="sxs-lookup"><span data-stu-id="4ed02-107">Our card framework eliminates the burden of designing a fully functional UX.</span></span> <span data-ttu-id="4ed02-108">Microsoft は、いくつかの標準カードの種類を開発し、それぞれがサポートされるプラットフォーム内に収まるようにしました。</span><span class="sxs-lookup"><span data-stu-id="4ed02-108">We developed several standard card types and each one fits within our supported platforms.</span></span> <span data-ttu-id="4ed02-109">これは、レイアウトが完全に機能しており、プラットフォーム間で異なるカードの繰り返しを開発する必要がないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="4ed02-109">This means layout is completely taken care of, and you won’t need to develop different card iterations across platforms.</span></span> <span data-ttu-id="4ed02-110">代わりに、コンテンツでのダイヤルに集中できます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-110">Instead, you can focus on dialing in your content.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="4ed02-111">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="4ed02-111">Guidelines</span></span>

<span data-ttu-id="4ed02-112">カードをユーザーの質問または設定に対する応答として考えます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-112">Think of a card as a response to a user question or a setting.</span></span> <span data-ttu-id="4ed02-113">カードは、直接的な質問 ("開いているバグの数" など) または条件 (たとえば、"open バグの一覧を毎日午前9時に送信する" など) に応答できます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-113">A card can respond to a direct question (like, “How many open bugs do I have?”) or to a condition (like, “Send a list of my open bugs at 9 am every day”).</span></span>

> [!TIP]
> <span data-ttu-id="4ed02-114">標準カードの種類のいずれかを使用すると、サポートされている各プラットフォーム間ですべての応答が適切にレンダリングされることが既にわかっていることになります。</span><span class="sxs-lookup"><span data-stu-id="4ed02-114">Using one of our standard card types means you’ll already know that all your responses will render nicely across each supported platform.</span></span>

<span data-ttu-id="4ed02-115">カードには、次の要素のいずれかを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-115">A card could include any of the following elements:</span></span><br />

[!include[Card anatomy](~/includes/design/card-image-anatomy.html)]

1. <span data-ttu-id="4ed02-116">**封筒テキスト**: チャットメッセージに最適です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-116">**Envelope text**: Best used for chat messages.</span></span> <span data-ttu-id="4ed02-117">たとえば、次のようになります。「検索されたものが見つかりました!」と言います。</span><span class="sxs-lookup"><span data-stu-id="4ed02-117">For example, if you want a bot to say: “Here’s what I found!”</span></span> <span data-ttu-id="4ed02-118">または「1:00 ニュースダイジェストの時間」というメッセージは、封筒テキストに表示されるのが最適です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-118">or “Time for your 1:00 news digest”, that message is best displayed in envelope text.</span></span>

   <span data-ttu-id="4ed02-119">封筒テキストは、サービスに少しの個性を注入するための最適な方法です。これは、比較的短いままにしておくことを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="4ed02-119">Envelope text is a great way to inject a little personality into your service—just remember to keep it relatively short.</span></span>

2. <span data-ttu-id="4ed02-120">**タイトル**: タイトルは常に、カード内の最大のテキストになります。</span><span class="sxs-lookup"><span data-stu-id="4ed02-120">**Title**: Your title will always be the largest text in your card.</span></span> <span data-ttu-id="4ed02-121">また、"フック" として機能するので、タイトルは短くて覚えやすいものにして、スキャンしやすいものにしてください。</span><span class="sxs-lookup"><span data-stu-id="4ed02-121">It also serves as your “hook”, so try to keep the title short, memorable, and easy to scan.</span></span>

3. <span data-ttu-id="4ed02-122">**副題**: 属性、taglines、またはセカンダリディレクティブとして最適に使用されます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-122">**Subtitle**: Best used for attribution, taglines, or as a secondary directive.</span></span> <span data-ttu-id="4ed02-123">このコンポーネントは、タイトルのすぐ下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-123">This component appears just below your title.</span></span>

4. <span data-ttu-id="4ed02-124">**画像**: コンテナーに合わせて画像を拡大または縮小します。</span><span class="sxs-lookup"><span data-stu-id="4ed02-124">**Image**: Images scale to fit their container.</span></span> <span data-ttu-id="4ed02-125">英雄カードの最大幅は420px、サムネイルの最大幅は100px、リストビューではデスクトップモードでは間隔のみが許可されています。</span><span class="sxs-lookup"><span data-stu-id="4ed02-125">Hero cards have a max width of 420px, thumbnails have a max width of 100px, and list views only allow for 32px in desktop mode.</span></span>

5. <span data-ttu-id="4ed02-126">**テキスト**: カードの本文にプレーンテキストを使用するのに最適です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-126">**Text**: Best used for plain text in the body of your card.</span></span> <span data-ttu-id="4ed02-127">最大長は、選択したカードの種類によって異なります。</span><span class="sxs-lookup"><span data-stu-id="4ed02-127">Your max length depends on the card type you’ve selected.</span></span>

6. <span data-ttu-id="4ed02-128">**ボタン**: web ページ、タブ、または追加のチャットコンテンツを開くために最適です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-128">**Buttons**: Best used to open web pages, tabs, or additional chat content.</span></span> <span data-ttu-id="4ed02-129">ボタンのテキストを短くして、その点まで維持するようにしてください。</span><span class="sxs-lookup"><span data-stu-id="4ed02-129">Make sure to keep your button text short and to the point.</span></span>

   <span data-ttu-id="4ed02-130">カードごとに最大6つのボタンを含めることができますが、ここでは「less is more」という原則に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4ed02-130">You can include up to 6 buttons per card, but we’d recommend following a ‘less is more’ philosophy here.</span></span>

7. <span data-ttu-id="4ed02-131">**タップ地域**: これは、カードのクリック可能な領域です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-131">**Tap region**: This is the clickable region of your card.</span></span> <span data-ttu-id="4ed02-132">ほとんどのユーザーは、画像を自動的にクリックする必要があるので、自分がタップまたはクリックした位置がわかるようにテキストを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4ed02-132">Most users will want to click on images automatically, so try and craft your text so they know where they should tap or click.</span></span>

> [!TIP]
> <span data-ttu-id="4ed02-133">作成した各カードにすべての要素を含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4ed02-133">There’s no need to include every element in each card you create.</span></span> <span data-ttu-id="4ed02-134">コンテンツに要素を説明します。</span><span class="sxs-lookup"><span data-stu-id="4ed02-134">Let your content dictate your elements.</span></span>

---

## <a name="types-of-cards"></a><span data-ttu-id="4ed02-135">カードの種類</span><span class="sxs-lookup"><span data-stu-id="4ed02-135">Types of cards</span></span>

### <a name="hero"></a><span data-ttu-id="4ed02-136">ヒーロー</span><span class="sxs-lookup"><span data-stu-id="4ed02-136">Hero</span></span>

<span data-ttu-id="4ed02-137">最大のカード</span><span class="sxs-lookup"><span data-stu-id="4ed02-137">Our largest card.</span></span> <span data-ttu-id="4ed02-138">最もよく使用されるのは、記事、詳細な説明、または画像がほとんどの話を伝えるシナリオです。</span><span class="sxs-lookup"><span data-stu-id="4ed02-138">Best used for articles, long descriptions, or scenarios where your image is telling most of the story.</span></span>

[!include[Card anatomy](~/includes/design/card-image-hero.html)]

### <a name="thumbnail"></a><span data-ttu-id="4ed02-139">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="4ed02-139">Thumbnail</span></span>

<span data-ttu-id="4ed02-140">短時間、かつ甘い。</span><span class="sxs-lookup"><span data-stu-id="4ed02-140">Short and sweet.</span></span> <span data-ttu-id="4ed02-141">これらのカードは、短い回答に適している場合や、一度に複数のカードを返して、ユーザーが一連のオプションから選択できるようにする場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-141">These cards are ideal for short answers, or if you want to return several cards at once so the user can choose from a bunch of options.</span></span> <span data-ttu-id="4ed02-142">他のタブまたは web サービスに深くリンクするには、これらの方法が適していると考えています。</span><span class="sxs-lookup"><span data-stu-id="4ed02-142">We think these are a great way to deep link to another tab or a web service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-thumbnail.html)]

### <a name="sign-in"></a><span data-ttu-id="4ed02-143">サインイン</span><span class="sxs-lookup"><span data-stu-id="4ed02-143">Sign in</span></span>

<span data-ttu-id="4ed02-144">一部のサービスでは、ユーザーは認証とは無関係にサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ed02-144">Some services require users to sign in independently of our authentication.</span></span> <span data-ttu-id="4ed02-145">このイベントでは、ユーザーがサービスに接続する前に、サインインカードを提示します。</span><span class="sxs-lookup"><span data-stu-id="4ed02-145">In that event, you would present a sign-in card before the user can connect to your service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-signin.html)]

> [!TIP]
> <span data-ttu-id="4ed02-146">追加のサインインカードの発生を制限して、新しいユーザーのスピードを大幅に向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-146">Limit the occurrences of an additional sign-in card since they pose a significant speed bump for new users.</span></span>

---

## <a name="card-collections"></a><span data-ttu-id="4ed02-147">カードコレクション</span><span class="sxs-lookup"><span data-stu-id="4ed02-147">Card collections</span></span>

<span data-ttu-id="4ed02-148">また、複数の部分のコンテンツを一度に、またはすぐに表示する場合に最適な標準カードの種類が用意されています。</span><span class="sxs-lookup"><span data-stu-id="4ed02-148">We also have standard card types that are best used when you want to present several pieces of content at once or in quick succession.</span></span> <span data-ttu-id="4ed02-149">そのためには、カルーセル、ダイジェスト、リスト、および ' バブルマージ ' という呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="4ed02-149">For that purpose, we have a carousel, a digest, a list, and what we call a ‘bubble merge’.</span></span>

### <a name="carousel"></a><span data-ttu-id="4ed02-150">カルーセル</span><span class="sxs-lookup"><span data-stu-id="4ed02-150">Carousel</span></span>

<span data-ttu-id="4ed02-151">記事、ショッピング、およびカードを参照するのに最適です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-151">Best used for articles, shopping, and browsing through cards.</span></span>

[!include[Card anatomy](~/includes/design/card-image-carousel.html)]

> [!TIP]
> <span data-ttu-id="4ed02-152">カルーセルは、最も大きいカードの最大の高さになります。</span><span class="sxs-lookup"><span data-stu-id="4ed02-152">The carousel will be the max height of your largest card.</span></span> <span data-ttu-id="4ed02-153">同じ種類のカードとコンテンツフィールドを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4ed02-153">We recommend using the same card type and content fields throughout.</span></span>

### <a name="digest"></a><span data-ttu-id="4ed02-154">Digest</span><span class="sxs-lookup"><span data-stu-id="4ed02-154">Digest</span></span>

<span data-ttu-id="4ed02-155">ユーザーが複数のカードを一度に表示できるようにする場合に、ニュース、ダイジェスト、およびいつでも使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4ed02-155">Best used for news, digests, and whenever you want the user to view multiple cards at once.</span></span> <span data-ttu-id="4ed02-156">ダイジェストにはサムネイルカードを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4ed02-156">We recommend using thumbnail cards for digests.</span></span>

[!include[Card anatomy](~/includes/design/card-image-digest.html)]

### <a name="lists"></a><span data-ttu-id="4ed02-157">リスト</span><span class="sxs-lookup"><span data-stu-id="4ed02-157">Lists</span></span>

<span data-ttu-id="4ed02-158">リストは、"これらのうち1つを選ぶ" シナリオでオブジェクトの scannable セットを表示するための最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-158">Lists are a great way to present a scannable set of objects in a “pick one of these” scenario.</span></span> <span data-ttu-id="4ed02-159">リストは、多くの説明を必要としないアイテムに使用するのに最適です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-159">Lists are best used for items that don’t need a lot of explanation.</span></span>

[!include[Card anatomy](~/includes/design/card-image-list.html)]

### <a name="bubble-merge"></a><span data-ttu-id="4ed02-160">バブルマージ</span><span class="sxs-lookup"><span data-stu-id="4ed02-160">Bubble merge</span></span>

<span data-ttu-id="4ed02-161">いくつかの興味深い効果は、1つの英雄と複数のサムネイルをすばやく連続して送信することによって実現できます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-161">Some interesting effects can be achieved by sending one hero and several thumbnails in quick succession.</span></span> <span data-ttu-id="4ed02-162">メインの結果を提供するが、さらに多くの関連アイテムを含める場合は、この方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4ed02-162">We recommend this approach when you want to serve a main result but include a few more related items.</span></span>

[!include[Card anatomy](~/includes/design/card-image-bubble-merge.html)]

---

## <a name="best-practices"></a><span data-ttu-id="4ed02-163">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="4ed02-163">Best practices</span></span>

### <a name="keep-the-noise-down"></a><span data-ttu-id="4ed02-164">ノイズを抑える</span><span class="sxs-lookup"><span data-stu-id="4ed02-164">Keep the noise down</span></span>

<span data-ttu-id="4ed02-165">複数のカードを1つの会話に簡単に送信できますが、カードが表示されなくなると、利便性が低下します。</span><span class="sxs-lookup"><span data-stu-id="4ed02-165">It’s easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="4ed02-166">Essentials に制限するようにしてください。</span><span class="sxs-lookup"><span data-stu-id="4ed02-166">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="4ed02-167">これは、ユーザーが "ノイズ" として認識される許容範囲を下回っているチャネルの場合に特に当てはまります。</span><span class="sxs-lookup"><span data-stu-id="4ed02-167">This is especially true in a channel where users have less tolerance for what they perceive as “noise”.</span></span>

### <a name="test-on-mobile"></a><span data-ttu-id="4ed02-168">モバイルでのテスト</span><span class="sxs-lookup"><span data-stu-id="4ed02-168">Test on mobile</span></span>

<span data-ttu-id="4ed02-169">モバイル環境は、スペースと帯域幅に制約があるため、サイズの大きい画像と大規模なデータセットをリストと carousels に含めることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4ed02-169">Mobile environments are space- and bandwidth-constrained, so be cautious about including oversized images and large data sets in lists and carousels.</span></span> <span data-ttu-id="4ed02-170">また、タイトルの幅とテキストの長さはモバイルで切り捨てられるので、もう1つ注目することもあります。</span><span class="sxs-lookup"><span data-stu-id="4ed02-170">Also, title widths and text lengths will truncate on mobile, so that’s another thing to keep an eye on.</span></span>

### <a name="check-your-graphics"></a><span data-ttu-id="4ed02-171">グラフィックスを確認する</span><span class="sxs-lookup"><span data-stu-id="4ed02-171">Check your graphics</span></span>

<span data-ttu-id="4ed02-172">画像は拡大していきますので、必ずすべてのプラットフォームでプレビューしてください。</span><span class="sxs-lookup"><span data-stu-id="4ed02-172">Graphics are going to scale, so be sure to preview them on all platforms.</span></span>

### <a name="avoid-including-text-in-a-graphic"></a><span data-ttu-id="4ed02-173">テキストをグラフィックに含めないようにする</span><span class="sxs-lookup"><span data-stu-id="4ed02-173">Avoid including text in a graphic</span></span>

<span data-ttu-id="4ed02-174">ユーザーが読み取る必要があるものは、すべてテキストフィールドに含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="4ed02-174">Anything that needs to be read by a user should be included in a text field.</span></span> <span data-ttu-id="4ed02-175">画像が動的に拡大縮小されると、画像に追加したテキストが判読できなくなることがあります。</span><span class="sxs-lookup"><span data-stu-id="4ed02-175">Once an image is dynamically scaled, any text you add to a graphic may become unintelligible.</span></span>

### <a name="use-mentions-if-you-want-the-attention-of-specific-users"></a><span data-ttu-id="4ed02-176">特定のユーザーの注意を引く場合は、メンションを使用します。</span><span class="sxs-lookup"><span data-stu-id="4ed02-176">Use mentions if you want the attention of specific users</span></span>

> [!NOTE]
> <span data-ttu-id="4ed02-177">現在、カードでのサポートは、 [開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md) のみでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="4ed02-177">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="4ed02-178">メンションは、チームまたはグループのチャットで特定のユーザーに通知するための最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="4ed02-178">Mentions are a great way to notify specific users in a Team or group chat.</span></span> <span data-ttu-id="4ed02-179">ユーザーに割り当てられたタスクや、チームメイトに称賛を付与するようなシナリオで、カードに説明を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="4ed02-179">You can include a mention in card in scenarios like, a task thats assigned to a user or giving Kudos to a teammate.</span></span> <span data-ttu-id="4ed02-180">[カード形式ページ](~/task-modules-and-cards/cards/cards-format.md)のカードにメンションを含める方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4ed02-180">Learn how to include mentions in cards in the [card formatting page](~/task-modules-and-cards/cards/cards-format.md).</span></span> 
