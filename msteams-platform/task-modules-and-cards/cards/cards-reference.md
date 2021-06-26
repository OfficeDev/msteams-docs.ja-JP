---
title: カードの種類
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
localization_priority: Normal
keywords: Bot のカード リファレンス
ms.topic: reference
ms.openlocfilehash: be38454daac519530d0fdf10b5170e128219f6fc
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140487"
---
# <a name="types-of-cards"></a><span data-ttu-id="3fcc9-104">カードの種類</span><span class="sxs-lookup"><span data-stu-id="3fcc9-104">Types of cards</span></span>

<span data-ttu-id="3fcc9-105">アダプティブ、ヒーロー、リスト、Office 365 コネクタ、レシート、サインイン、サムネイル カード、およびカード コレクションは、Microsoft Teams のボットでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="3fcc9-106">Bot Framework で定義されたカードに基づいていますが、すべての Bot Framework カードが Teams でサポートされているわけではなく、独自のカードがいくつか追加されています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span>

<span data-ttu-id="3fcc9-107">さまざまなカードの種類を特定する前に、ヒーロー カード、サムネイル カード、アダプティブ カードを作成する方法を理解してください。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-107">Before you identify the different card types, understand how to create a a hero card, thumbnail card, or Adaptive Card.</span></span>

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a><span data-ttu-id="3fcc9-108">ヒーロー カード、サムネイル カード、アダプティブ カードを作成する</span><span class="sxs-lookup"><span data-stu-id="3fcc9-108">Create a hero card, thumbnail card, or Adaptive Card</span></span>

<span data-ttu-id="3fcc9-109">**App Studio からヒーロー カード、サムネイル カード、アダプティブ カードを作成するには**</span><span class="sxs-lookup"><span data-stu-id="3fcc9-109">**To create a hero card, thumbnail card, or Adaptive Card from App Studio**</span></span>

1. <span data-ttu-id="3fcc9-110">[アプリ スタジオ]**に** 移動Teams。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-110">Go to **App Studio** from Teams.</span></span>
1. <span data-ttu-id="3fcc9-111">[カード **エディター] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-111">Select **Card editor**.</span></span>
1. <span data-ttu-id="3fcc9-112">[新 **しいカードを作成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-112">Select **Create a new card**.</span></span>
1. <span data-ttu-id="3fcc9-113">[**ヒーロー カード**]、[サムネイルカード]、または [アダプティブ カード] のいずれかのカードに対して [作成]**を選択します**。 </span><span class="sxs-lookup"><span data-stu-id="3fcc9-113">Select **Create** for one of the cards from **Hero Card**, **Thumbnail Card**, or **Adaptive Card**.</span></span> <span data-ttu-id="3fcc9-114">そのカードのメタデータの詳細、ボタン、json、csharp、およびノード コードの例が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-114">The metadata details, buttons, and json, csharp, and node code examples are shown for that card.</span></span>

    ![ヒーロー カードの詳細](~/assets/images/Cards/Herocarddetails.png)

1. <span data-ttu-id="3fcc9-116">[この **カードを送信する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-116">Select **Send me this card**.</span></span> <span data-ttu-id="3fcc9-117">カードがチャット メッセージとして送信されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-117">The card is sent to you as a chat message.</span></span>

## <a name="card-examples"></a><span data-ttu-id="3fcc9-118">カードの例</span><span class="sxs-lookup"><span data-stu-id="3fcc9-118">Card examples</span></span>

<span data-ttu-id="3fcc9-119">カードの使用方法に関する追加情報については、Bot Builder SDK v3 のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-119">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="3fcc9-120">コード サンプルは **、Microsoft/BotBuilder-Samples リポジトリ (microsoft/BotBuilder-Samples** リポジトリ) GitHub。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-120">Code samples are also available in the **Microsoft/BotBuilder-Samples** repository on GitHub.</span></span> <span data-ttu-id="3fcc9-121">カードの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-121">Following are a few card examples:</span></span>

* <span data-ttu-id="3fcc9-122">.NET</span><span class="sxs-lookup"><span data-stu-id="3fcc9-122">.NET</span></span>
  * <span data-ttu-id="3fcc9-123">[メッセージに添付ファイルとしてカードを追加します](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-123">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="3fcc9-124">[カードのサンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="3fcc9-124">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="3fcc9-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="3fcc9-125">Node.js</span></span>
  * <span data-ttu-id="3fcc9-126">[メッセージに添付ファイルとしてカードを追加します](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-126">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="3fcc9-127">[カードのサンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="3fcc9-127">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="card-types"></a><span data-ttu-id="3fcc9-128">カードの種類</span><span class="sxs-lookup"><span data-stu-id="3fcc9-128">Card types</span></span>

<span data-ttu-id="3fcc9-129">アプリケーション要件に基づいて、さまざまな種類のカードを識別して使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-129">You can identify and use different types of cards based on your application requirements.</span></span> <span data-ttu-id="3fcc9-130">次の表に、使用可能なカードの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-130">The following table shows the types of cards available to you:</span></span>

| <span data-ttu-id="3fcc9-131">カードの種類</span><span class="sxs-lookup"><span data-stu-id="3fcc9-131">Card type</span></span> | <span data-ttu-id="3fcc9-132">説明</span><span class="sxs-lookup"><span data-stu-id="3fcc9-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="3fcc9-133">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-133">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="3fcc9-134">このカードは高度にカスタマイズ可能で、テキスト、音声、画像、ボタン、および入力フィールドの任意の組み合わせを含めできます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-134">This card is highly customizable and can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="3fcc9-135">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-135">Hero card</span></span>](#hero-card) | <span data-ttu-id="3fcc9-136">このカードには、通常、1 つの大きな画像、1 つ以上のボタン、および少量のテキストが含まれる。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-136">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="3fcc9-137">リスト カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-137">List card</span></span>](#list-card) | <span data-ttu-id="3fcc9-138">このカードには、アイテムのスクロール リストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-138">This card contains a scrolling list of items.</span></span> |
| [<span data-ttu-id="3fcc9-139">Office 365コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-139">Office 365 Connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="3fcc9-140">このカードには、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトがあります。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-140">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="3fcc9-141">レシート カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-141">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="3fcc9-142">このカードは、ユーザーにレシートを提供します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-142">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="3fcc9-143">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-143">Signin card</span></span>](#signin-card) | <span data-ttu-id="3fcc9-144">このカードを使用すると、ボットはユーザーのサインインを要求できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-144">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="3fcc9-145">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-145">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="3fcc9-146">このカードには、通常、1 つのサムネイル 画像、短いテキスト、および 1 つ以上のボタンが含まれる。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-146">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="3fcc9-147">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="3fcc9-147">Card collections</span></span>](#card-collections) | <span data-ttu-id="3fcc9-148">このカード コレクションは、1 つの応答で複数のアイテムを返す場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-148">This card collection is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="3fcc9-149">すべてのカードの共通プロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-149">Common properties for all cards</span></span>

<span data-ttu-id="3fcc9-150">すべてのカードに適用できる一般的なプロパティを確認できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-150">You can go through some common properties that are applicable to all cards.</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="3fcc9-151">インライン カードの画像</span><span class="sxs-lookup"><span data-stu-id="3fcc9-151">Inline card images</span></span>

<span data-ttu-id="3fcc9-152">カードには、公開されている画像へのリンクを含め、インライン イメージを含めできます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-152">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="3fcc9-153">パフォーマンス上の目的で、イメージをパブリック サーバー (Content Delivery Network) でホストCDN。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-153">For performance purposes, it is highly recommended you host the image on a public Content Delivery Network (CDN).</span></span>

<span data-ttu-id="3fcc9-154">画像のサイズを拡大または縮小して、画像領域をカバーするための縦横比を維持します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-154">Images are scaled up or down in size to maintain the aspect ratio for covering the image area.</span></span> <span data-ttu-id="3fcc9-155">次に、カードの適切な縦横比を実現するために、中央から画像がトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-155">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="3fcc9-156">画像は最大 1024、×1024、PNG、JPEG、または GIF 形式である必要があります。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-156">Images must be at most 1024×1024 and in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="3fcc9-157">アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-157">Animated GIF is not supported.</span></span>

<span data-ttu-id="3fcc9-158">次の表に、インライン カード イメージのプロパティを示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-158">The following table provides the properties of inline card images:</span></span>

| <span data-ttu-id="3fcc9-159">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-159">Property</span></span> | <span data-ttu-id="3fcc9-160">型</span><span class="sxs-lookup"><span data-stu-id="3fcc9-160">Type</span></span>  | <span data-ttu-id="3fcc9-161">説明</span><span class="sxs-lookup"><span data-stu-id="3fcc9-161">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3fcc9-162">url</span><span class="sxs-lookup"><span data-stu-id="3fcc9-162">url</span></span> | <span data-ttu-id="3fcc9-163">URL</span><span class="sxs-lookup"><span data-stu-id="3fcc9-163">URL</span></span> | <span data-ttu-id="3fcc9-164">イメージの HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-164">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="3fcc9-165">alt</span><span class="sxs-lookup"><span data-stu-id="3fcc9-165">alt</span></span> | <span data-ttu-id="3fcc9-166">文字列</span><span class="sxs-lookup"><span data-stu-id="3fcc9-166">String</span></span> | <span data-ttu-id="3fcc9-167">画像のアクセス可能な説明。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-167">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="3fcc9-168">最終的なイメージの前にリダイレクトされるイメージ URL がカードに含まれる場合、イメージ URL のリダイレクトはサポートされません。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-168">If a card includes an image URL that is redirected before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="3fcc9-169">これは、パブリック クラウド上で共有されるイメージに対して発生します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-169">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="3fcc9-170">ボタン</span><span class="sxs-lookup"><span data-stu-id="3fcc9-170">Buttons</span></span>

<span data-ttu-id="3fcc9-171">ボタンはカードの下部に上下に並んで表示されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-171">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="3fcc9-172">ボタンのテキストは常に 1 行に表示され、テキストがボタンの幅を超えると切り捨てされます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-172">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="3fcc9-173">カードでサポートされている最大数を超える追加のボタンは表示されません。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-173">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="3fcc9-174">詳細については、「カードアクション [」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-174">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="3fcc9-175">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="3fcc9-175">Card formatting</span></span>

<span data-ttu-id="3fcc9-176">カードのテキスト書式の詳細については、「カードの書式設定」 [を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-176">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

<span data-ttu-id="3fcc9-177">すべてのカードの共通プロパティを特定した後、アダプティブ カードを操作し、アクション可能なコンテンツを使用するアプリに直接追加することで、エンゲージメントと効率を向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-177">After identifying the common properties for all cards, you can now work with Adaptive Cards, which help you increase engagement and efficiency by adding your actionable content directly into the apps you use.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="3fcc9-178">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-178">Adaptive Card</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="3fcc9-179">アダプティブ カードは、テキスト、音声、画像、ボタン、および入力フィールドの任意の組み合わせを含むカスタマイズ可能なカードです。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-179">An Adaptive Card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="3fcc9-180">詳細については [、「Adaptive Cards v1.2.0」を参照してください](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-180">For more information, see [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="3fcc9-181">アダプティブ カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3fcc9-181">Support for Adaptive Cards</span></span>

<span data-ttu-id="3fcc9-182">次の表に、アダプティブ カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-182">The following table provides the features that support Adaptive Cards:</span></span>

| <span data-ttu-id="3fcc9-183">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3fcc9-183">Bots in Teams</span></span> | <span data-ttu-id="3fcc9-184">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3fcc9-184">Messaging extensions</span></span>  | <span data-ttu-id="3fcc9-185">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-185">Connectors</span></span> | <span data-ttu-id="3fcc9-186">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3fcc9-186">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fcc9-187">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-187">✔</span></span> | <span data-ttu-id="3fcc9-188">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-188">✔</span></span> | <span data-ttu-id="3fcc9-189">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-189">✖</span></span> | <span data-ttu-id="3fcc9-190">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-190">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="3fcc9-191">Teamsプラットフォームは、アダプティブ カード機能の v1.2 以前をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-191">Teams platform supports v1.2 or earlier of Adaptive Card features.</span></span>
> * <span data-ttu-id="3fcc9-192">正または破壊的なアクションのスタイル設定は、プラットフォーム上のアダプティブ カードではTeamsされません。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-192">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="3fcc9-193">メディア要素は、現在、プラットフォーム上のアダプティブ カードTeamsされていません。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-193">Media elements are currently not supported in Adaptive Card on the Teams platform.</span></span>

### <a name="example-of-adaptive-card"></a><span data-ttu-id="3fcc9-194">アダプティブ カードの例</span><span class="sxs-lookup"><span data-stu-id="3fcc9-194">Example of Adaptive Card</span></span>

![アダプティブ カードの例](~/assets/images/cards/adaptivecard.png)

<span data-ttu-id="3fcc9-196">次のコードは、アダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-196">The following code shows an example of an Adaptive Card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Publish Adaptive Card schema",
            "weight": "bolder",
            "size": "medium"
          },
          {
            "type": "ColumnSet",
            "columns": [
              {
                "type": "Column",
                "width": "auto",
                "items": [
                  {
                    "type": "Image",
                    "url": "https://pbs.twimg.com/profile_images/3647943215/d7f12830b3c17a5a9e4afcc370e3a37e_400x400.jpeg",
                    "size": "small",
                    "style": "person"
                  }
                ]
              },
              {
                "type": "Column",
                "width": "stretch",
                "items": [
                  {
                    "type": "TextBlock",
                    "text": "Matt Hidinger",
                    "weight": "bolder",
                    "wrap": true
                  },
                  {
                    "type": "TextBlock",
                    "spacing": "none",
                    "text": "Created {{DATE(2017-02-14T06:08:39Z, SHORT)}}",
                    "isSubtle": true,
                    "wrap": true
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Now that we have defined the main rules and features of the format, we need to produce a schema and publish it to GitHub. The schema will be the starting point of our reference documentation.",
            "wrap": true
          },
          {
            "type": "FactSet",
            "facts": [
              {
                "title": "Board:",
                "value": "Adaptive Card"
              },
              {
                "title": "List:",
                "value": "Backlog"
              },
              {
                "title": "Assigned to:",
                "value": "Matt Hidinger"
              },
              {
                "title": "Due date:",
                "value": "Not set"
              }
            ]
          }
        ]
      }
    ],
    "actions": [
      {
        "type": "Action.ShowCard",
        "title": "Set due date",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Date",
              "id": "dueDate"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      },
      {
        "type": "Action.ShowCard",
        "title": "Comment",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Text",
              "id": "comment",
              "isMultiline": true,
              "placeholder": "Enter your comment"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      }
    ]
  }  
}
```

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="3fcc9-197">アダプティブ カードの追加情報</span><span class="sxs-lookup"><span data-stu-id="3fcc9-197">Additional information on Adaptive Cards</span></span>

<span data-ttu-id="3fcc9-198">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-198">Bot Framework reference:</span></span>

* [<span data-ttu-id="3fcc9-199">アダプティブ カード ノード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-199">Adaptive Cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="3fcc9-200">アダプティブ カード C#</span><span class="sxs-lookup"><span data-stu-id="3fcc9-200">Adaptive Card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

<span data-ttu-id="3fcc9-201">これで、潜在的なユーザー選択を視覚的に強調表示するために使用される多目的カードであるヒーロー カードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-201">You can now work with a hero card, which is a multipurpose card used to visually highlight a potential user selection.</span></span>

## <a name="hero-card"></a><span data-ttu-id="3fcc9-202">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-202">Hero card</span></span>

<span data-ttu-id="3fcc9-203">通常、1 つの大きな画像、1 つ以上のボタン、およびテキストを含むカード。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-203">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="3fcc9-204">ヒーロー カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3fcc9-204">Support for hero cards</span></span>

<span data-ttu-id="3fcc9-205">次の表に、ヒーロー カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-205">The following table provides the features that support hero cards:</span></span>

| <span data-ttu-id="3fcc9-206">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3fcc9-206">Bots in Teams</span></span> | <span data-ttu-id="3fcc9-207">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3fcc9-207">Messaging extensions</span></span>  | <span data-ttu-id="3fcc9-208">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-208">Connectors</span></span> | <span data-ttu-id="3fcc9-209">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3fcc9-209">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fcc9-210">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-210">✔</span></span> | <span data-ttu-id="3fcc9-211">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-211">✔</span></span> | <span data-ttu-id="3fcc9-212">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-212">✖</span></span> | <span data-ttu-id="3fcc9-213">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-213">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="3fcc9-214">ヒーロー カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-214">Properties of a hero card</span></span>

<span data-ttu-id="3fcc9-215">次の表に、ヒーロー カードのプロパティを示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-215">The following table provides the properties of a hero card:</span></span>

| <span data-ttu-id="3fcc9-216">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-216">Property</span></span> | <span data-ttu-id="3fcc9-217">型</span><span class="sxs-lookup"><span data-stu-id="3fcc9-217">Type</span></span>  | <span data-ttu-id="3fcc9-218">説明</span><span class="sxs-lookup"><span data-stu-id="3fcc9-218">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3fcc9-219">title</span><span class="sxs-lookup"><span data-stu-id="3fcc9-219">title</span></span> | <span data-ttu-id="3fcc9-220">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-220">Rich text</span></span> | <span data-ttu-id="3fcc9-221">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-221">Title of the card.</span></span> <span data-ttu-id="3fcc9-222">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-222">Maximum two lines.</span></span> |
| <span data-ttu-id="3fcc9-223">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="3fcc9-223">subtitle</span></span> | <span data-ttu-id="3fcc9-224">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-224">Rich text</span></span> | <span data-ttu-id="3fcc9-225">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-225">Subtitle of the card.</span></span> <span data-ttu-id="3fcc9-226">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-226">Maximum two lines.</span></span>|
| <span data-ttu-id="3fcc9-227">テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-227">text</span></span> | <span data-ttu-id="3fcc9-228">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-228">Rich text</span></span> | <span data-ttu-id="3fcc9-229">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-229">Text appears under the subtitle.</span></span> <span data-ttu-id="3fcc9-230">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-230">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="3fcc9-231">images</span><span class="sxs-lookup"><span data-stu-id="3fcc9-231">images</span></span> | <span data-ttu-id="3fcc9-232">画像の配列</span><span class="sxs-lookup"><span data-stu-id="3fcc9-232">Array of images</span></span> | <span data-ttu-id="3fcc9-233">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-233">Image displayed at the top of the card.</span></span> <span data-ttu-id="3fcc9-234">縦横比 16:9。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-234">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="3fcc9-235">buttons</span><span class="sxs-lookup"><span data-stu-id="3fcc9-235">buttons</span></span> | <span data-ttu-id="3fcc9-236">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="3fcc9-236">Array of action objects</span></span> | <span data-ttu-id="3fcc9-237">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-237">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3fcc9-238">最大 6 個。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-238">Maximum six.</span></span> |
| <span data-ttu-id="3fcc9-239">tap</span><span class="sxs-lookup"><span data-stu-id="3fcc9-239">tap</span></span> | <span data-ttu-id="3fcc9-240">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-240">Action object</span></span> | <span data-ttu-id="3fcc9-241">ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-241">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="3fcc9-242">ヒーロー カードの例</span><span class="sxs-lookup"><span data-stu-id="3fcc9-242">Example of a hero card</span></span>

![ヒーロー カードの例](~/assets/images/cards/hero.png)

<span data-ttu-id="3fcc9-244">次のコードは、ヒーロー カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-244">The following code shows an example of a hero card:</span></span>

```json
{
   "contentType": "application/vnd.microsoft.card.hero",
   "content": {
     "title": "Seattle Center Monorail",
     "subtitle": "Seattle Center Monorail",
     "text": "The Seattle Center Monorail is an elevated train line between Seattle Center (near the Space Needle) and downtown Seattle. It was built for the 1962 World's Fair. Its original two trains, completed in 1961, are still in service.",
     "images": [
       {
         "url":"https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Seattle_monorail01_2008-02-25.jpg/1024px-Seattle_monorail01_2008-02-25.jpg"
       }
     ],
    "buttons": [
      {
         "type": "openUrl",
         "title": "Official website",
         "value": "https://www.seattlemonorail.com"
       },
      {
        "type": "openUrl",
        "title": "Wikipeda page",
        "value": "https://en.wikipedia.org/wiki/Seattle_Center_Monorail"
       }
     ]
   }
}

```

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="3fcc9-245">ヒーロー カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="3fcc9-245">Additional information on hero cards</span></span>

<span data-ttu-id="3fcc9-246">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-246">Bot Framework reference:</span></span>

* [<span data-ttu-id="3fcc9-247">ヒーロー カード Node.js</span><span class="sxs-lookup"><span data-stu-id="3fcc9-247">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="3fcc9-248">ヒーロー カード C#</span><span class="sxs-lookup"><span data-stu-id="3fcc9-248">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="3fcc9-249">リスト カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-249">List card</span></span>

<span data-ttu-id="3fcc9-250">リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-250">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="3fcc9-251">リスト カードは、アイテムのスクロール リストを提供します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-251">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="3fcc9-252">リスト カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3fcc9-252">Support for list cards</span></span>

<span data-ttu-id="3fcc9-253">次の表に、リスト カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-253">The following table provides the features that support list cards:</span></span>

| <span data-ttu-id="3fcc9-254">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3fcc9-254">Bots in Teams</span></span> | <span data-ttu-id="3fcc9-255">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3fcc9-255">Messaging extensions</span></span>  | <span data-ttu-id="3fcc9-256">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-256">Connectors</span></span> | <span data-ttu-id="3fcc9-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3fcc9-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fcc9-258">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-258">✔</span></span> | <span data-ttu-id="3fcc9-259">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-259">✖</span></span> | <span data-ttu-id="3fcc9-260">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-260">✖</span></span> |<span data-ttu-id="3fcc9-261">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-261">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="3fcc9-262">リスト カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-262">Properties of a list card</span></span>

<span data-ttu-id="3fcc9-263">次の表に、リスト カードのプロパティを示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-263">The following table provides the properties of a list card:</span></span>

| <span data-ttu-id="3fcc9-264">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-264">Property</span></span> | <span data-ttu-id="3fcc9-265">型</span><span class="sxs-lookup"><span data-stu-id="3fcc9-265">Type</span></span>  | <span data-ttu-id="3fcc9-266">説明</span><span class="sxs-lookup"><span data-stu-id="3fcc9-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3fcc9-267">title</span><span class="sxs-lookup"><span data-stu-id="3fcc9-267">title</span></span> | <span data-ttu-id="3fcc9-268">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-268">Rich text</span></span> | <span data-ttu-id="3fcc9-269">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-269">Title of the card.</span></span> <span data-ttu-id="3fcc9-270">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-270">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3fcc9-271">アイテム</span><span class="sxs-lookup"><span data-stu-id="3fcc9-271">items</span></span> | <span data-ttu-id="3fcc9-272">リスト アイテムの配列</span><span class="sxs-lookup"><span data-stu-id="3fcc9-272">Array of list items</span></span> | <span data-ttu-id="3fcc9-273">カードに適用可能なアイテムのセット。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-273">Set of items applicable to the card.</span></span>|
| <span data-ttu-id="3fcc9-274">buttons</span><span class="sxs-lookup"><span data-stu-id="3fcc9-274">buttons</span></span> | <span data-ttu-id="3fcc9-275">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="3fcc9-275">Array of action objects</span></span> | <span data-ttu-id="3fcc9-276">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-276">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3fcc9-277">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-277">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="3fcc9-278">リスト カードの例</span><span class="sxs-lookup"><span data-stu-id="3fcc9-278">Example of a list card</span></span>

<span data-ttu-id="3fcc9-279">次のコードは、リスト カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-279">The following code shows an example of a list card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.teams.card.list",
  "content": {
    "title": "Card title",
    "items": [
      {
        "type": "file",
        "id": "https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx",
        "title": "Report",
        "subtitle": "teams > new > design",
        "tap": {
          "type": "imBack",
          "value": "editOnline https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx"
        }
      },
      {
        "type": "resultItem",
        "icon": "https://cdn2.iconfinder.com/data/icons/social-icons-33/128/Trello-128.png",
        "title": "Trello title",
        "subtitle": "A Trello subtitle",
        "tap": {
          "type": "openUrl",
          "value": "http://trello.com"
        }
      },
      {
        "type": "section",
        "title": "Manager"
      },
      {
        "type": "person",
        "id": "JohnDoe@contoso.com",
        "title": "John Doe",
        "subtitle": "Manager",
        "tap": {
          "type": "imBack",
          "value": "whois JohnDoe@contoso.com"
        }
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Select",
        "value": "whois"
      }
    ]
  }
}
```

## <a name="office-365-connector-card"></a><span data-ttu-id="3fcc9-280">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-280">Office 365 connector card</span></span>

<span data-ttu-id="3fcc9-281">柔軟なレイアウトを提供し、Office 365情報を取得するための優れた方法であるコネクタ カードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-281">You can work with an Office 365 Connector card that provides a flexible layout and is a great way to get useful information.</span></span> <span data-ttu-id="3fcc9-282">コネクタ Office 365はボット フレームワークではなく、Teamsでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-282">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="3fcc9-283">このカードは、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトを提供します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-283">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="3fcc9-284">このカードにはコネクタ カードが含まれているので、ボットで使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-284">This card contains a connector card so that it can be used by bots.</span></span> <span data-ttu-id="3fcc9-285">コネクタ カードとコネクタ Office 365の違いについては、「コネクタ カードの追加情報[」をOffice 365してください](#additional-information-on-the-office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-285">For differences between connector cards and the Office 365 Connector card, see [Additional information on the Office 365 Connector card](#additional-information-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="3fcc9-286">コネクタ カードOffice 365サポート</span><span class="sxs-lookup"><span data-stu-id="3fcc9-286">Support for Office 365 Connector cards</span></span>

<span data-ttu-id="3fcc9-287">次の表に、コネクタ カードをサポートするOffice 365示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-287">The following table provides the features that support Office 365 Connector cards:</span></span>

| <span data-ttu-id="3fcc9-288">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3fcc9-288">Bots in Teams</span></span> | <span data-ttu-id="3fcc9-289">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3fcc9-289">Messaging extensions</span></span>  | <span data-ttu-id="3fcc9-290">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-290">Connectors</span></span> | <span data-ttu-id="3fcc9-291">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3fcc9-291">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fcc9-292">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-292">✔</span></span> | <span data-ttu-id="3fcc9-293">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-293">✔</span></span> | <span data-ttu-id="3fcc9-294">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-294">✔</span></span> | <span data-ttu-id="3fcc9-295">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-295">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="3fcc9-296">コネクタ カードOffice 365プロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-296">Properties of the Office 365 Connector card</span></span>

<span data-ttu-id="3fcc9-297">次の表に、コネクタ カードのプロパティOffice 365示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-297">The following table provides the properties of the Office 365 connector card:</span></span>

| <span data-ttu-id="3fcc9-298">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-298">Property</span></span> | <span data-ttu-id="3fcc9-299">型</span><span class="sxs-lookup"><span data-stu-id="3fcc9-299">Type</span></span>  | <span data-ttu-id="3fcc9-300">説明</span><span class="sxs-lookup"><span data-stu-id="3fcc9-300">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3fcc9-301">title</span><span class="sxs-lookup"><span data-stu-id="3fcc9-301">title</span></span> | <span data-ttu-id="3fcc9-302">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-302">Rich text</span></span> | <span data-ttu-id="3fcc9-303">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-303">Title of the card.</span></span> <span data-ttu-id="3fcc9-304">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-304">Maximum two lines.</span></span> |
| <span data-ttu-id="3fcc9-305">概要</span><span class="sxs-lookup"><span data-stu-id="3fcc9-305">summary</span></span> | <span data-ttu-id="3fcc9-306">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-306">Rich text</span></span> | <span data-ttu-id="3fcc9-307">カードの概要。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-307">Summary of the card.</span></span> <span data-ttu-id="3fcc9-308">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-308">Maximum two lines.</span></span> |
| <span data-ttu-id="3fcc9-309">テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-309">text</span></span> | <span data-ttu-id="3fcc9-310">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-310">Rich text</span></span> | <span data-ttu-id="3fcc9-311">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-311">Text appears under the subtitle.</span></span> <span data-ttu-id="3fcc9-312">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-312">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="3fcc9-313">themeColor</span><span class="sxs-lookup"><span data-stu-id="3fcc9-313">themeColor</span></span> | <span data-ttu-id="3fcc9-314">16 進数文字列</span><span class="sxs-lookup"><span data-stu-id="3fcc9-314">HEX string</span></span> | <span data-ttu-id="3fcc9-315">アプリケーション マニフェストから提供される `accentColor` 色を上書きします。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-315">Color that overrides the `accentColor` provided from the application manifest.</span></span> |

### <a name="additional-information-on-the-office-365-connector-card"></a><span data-ttu-id="3fcc9-316">コネクタ カードのOffice 365情報</span><span class="sxs-lookup"><span data-stu-id="3fcc9-316">Additional information on the Office 365 Connector card</span></span>

<span data-ttu-id="3fcc9-317">Office 365コネクタ カードは、アクションなど、Microsoft Teamsで適切に[ `ActionCard` 機能します](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-317">Office 365 Connector cards function properly in Microsoft Teams, including [`ActionCard` actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="3fcc9-318">コネクタからコネクタ カードを使用する場合とボットでコネクタ カードを使用する場合の重要な違いは、カードアクションの処理です。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-318">The important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span> <span data-ttu-id="3fcc9-319">次の表に、相違点の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-319">The following table lists the difference:</span></span>

| <span data-ttu-id="3fcc9-320">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-320">Connector</span></span> | <span data-ttu-id="3fcc9-321">ボット</span><span class="sxs-lookup"><span data-stu-id="3fcc9-321">Bot</span></span> |
| --- | --- |
| <span data-ttu-id="3fcc9-322">エンドポイントは、HTTP POST を介してカード ペイロードを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-322">The endpoint receives the card payload through HTTP POST.</span></span> | <span data-ttu-id="3fcc9-323">アクション `HttpPOST` は、アクション ID と本文のみをボットに送信 `invoke` するアクティビティをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-323">The `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>|

<span data-ttu-id="3fcc9-324">各コネクタ カードには最大 10 個のセクションを表示できます。各セクションには最大 5 つのイメージと 5 つのアクションを含めできます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-324">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="3fcc9-325">メッセージ内の追加のセクション、イメージ、またはアクションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-325">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="3fcc9-326">すべてのテキスト フィールドは Markdown と HTML をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-326">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="3fcc9-327">メッセージの `markdown` プロパティを設定して、Markdown または HTML を使用するセクションを制御することができます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-327">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="3fcc9-328">既定では `markdown` 、 に設定されています `true` 。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-328">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="3fcc9-329">HTML を代わりに使用する場合は、 に `markdown` 設定します `false` 。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-329">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="3fcc9-330">`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-330">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="3fcc9-331">レンダリング スタイルを指定するには `activityImage` 、次の `activityImageType` 表に示すように設定できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-331">To specify the rendering style for `activityImage`, you can set `activityImageType` as shown in the following table:</span></span>

| <span data-ttu-id="3fcc9-332">値</span><span class="sxs-lookup"><span data-stu-id="3fcc9-332">Value</span></span> | <span data-ttu-id="3fcc9-333">説明</span><span class="sxs-lookup"><span data-stu-id="3fcc9-333">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="3fcc9-334">既定値は `activityImage` 、円としてトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-334">Default, `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="3fcc9-335">`activityImage` は四角形として表示され、縦横比が保持されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-335">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="3fcc9-336">コネクタ カードのプロパティに関するその他の詳細については、「アクション可能な [メッセージ カードリファレンス」を参照してください](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-336">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="3fcc9-337">現在サポートされていないコネクタ Teamsのプロパティは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-337">The only connector card properties that Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="3fcc9-338">`startGroup`常に、次のように `true` 処理Teams</span><span class="sxs-lookup"><span data-stu-id="3fcc9-338">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="3fcc9-339">コネクタ カードOffice 365例</span><span class="sxs-lookup"><span data-stu-id="3fcc9-339">Example of an Office 365 Connector card</span></span>

<span data-ttu-id="3fcc9-340">次のコードは、コネクタ カードの例Office 365示しています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-340">The following code shows an example of an Office 365 Connector card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "John Doe commented on Trello",
    "title": "Project Tango",
    "sections": [
        {
            "activityTitle": "John Doe commented",
            "activitySubtitle": "On Project Tango",
            "activityText": "\"Here are the designs\"",
            "activityImage": "http://connectorsdemo.azurewebsites.net/images/MSC12_Oscar_002.jpg"
        },
        {
            "title": "Details",
            "facts": [
                {
                    "name": "Labels",
                    "value": "Designs, redlines"
                },
                {
                    "name": "Due date",
                    "value": "Dec 7, 2016"
                },
                {
                    "name": "Attachments",
                    "value": "[final.jpg](http://connectorsdemo.azurewebsites.net/images/WIN14_Jan_04.jpg)"
                }
            ]
        },
        {
            "title": "Images",
            "images": [
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/MicrosoftSurface_024_Cafe_OH-06315_VS_R1c.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Scene_01.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Anthony_02.jpg"
                }
            ]
        }
    ],
    "potentialAction": [
        {
            "@context": "http://schema.org",
            "@type": "ViewAction",
            "name": "View in Trello",
            "target": [
                "https://trello.com/c/1101/"
            ]
        }
    ]
  }
}
```

## <a name="receipt-card"></a><span data-ttu-id="3fcc9-341">レシート カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-341">Receipt card</span></span>

<span data-ttu-id="3fcc9-342">Teamsカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-342">Teams supports receipt card.</span></span> <span data-ttu-id="3fcc9-343">ボットがユーザーにレシートを提供できるカードです。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-343">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="3fcc9-344">通常、税金や合計情報など、領収書に含めるアイテムの一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-344">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="3fcc9-345">レシート カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3fcc9-345">Support for receipt cards</span></span>

<span data-ttu-id="3fcc9-346">次の表に、レシート カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-346">The following table provides the features that support receipt cards:</span></span>

| <span data-ttu-id="3fcc9-347">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3fcc9-347">Bots in Teams</span></span> | <span data-ttu-id="3fcc9-348">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3fcc9-348">Messaging extensions</span></span>  | <span data-ttu-id="3fcc9-349">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-349">Connectors</span></span> | <span data-ttu-id="3fcc9-350">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3fcc9-350">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fcc9-351">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-351">✔</span></span> | <span data-ttu-id="3fcc9-352">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-352">✔</span></span> | <span data-ttu-id="3fcc9-353">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-353">✖</span></span> | <span data-ttu-id="3fcc9-354">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-354">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="3fcc9-355">レシート カードの例</span><span class="sxs-lookup"><span data-stu-id="3fcc9-355">Example of a receipt card</span></span>

![レシート カードの例](~/assets/images/cards/receipt.png)

<span data-ttu-id="3fcc9-357">次のコードは、レシート カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-357">The following code shows an example of a receipt card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.receipt",
  "content": {
    "title": "John Doe",
    "facts": [
      {
        "key": "Order Number",
        "value": "1234"
      },
      {
        "key": "Payment Method",
        "value": "VISA 5555-****"
      }
    ],
    "items": [
      {
        "title": "Data Transfer",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/traffic-manager.png"
        },
        "price": "$ 38.45",
        "quantity": "368"
      },
      {
        "title": "App Service",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/cloud-service.png"
        },
        "price": "$ 45.00",
        "quantity": "720"
      }
    ],
    "total": "$ 90.95",
    "tax": "$ 7.50",
    "buttons": [
      {
        "type": "openUrl",
        "title": "More information",
        "image": "https://account.windowsazure.com/content/6.10.1.38-.8225.160809-1618/aux-pre/images/offer-icon-freetrial.png",
        "value": "https://azure.microsoft.com/en-us/pricing/"
      }
    ]
  }
}
```

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="3fcc9-358">レシート カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="3fcc9-358">Additional information on receipt cards</span></span>

<span data-ttu-id="3fcc9-359">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-359">Bot Framework reference:</span></span>

* [<span data-ttu-id="3fcc9-360">レシート カードNode.js</span><span class="sxs-lookup"><span data-stu-id="3fcc9-360">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3fcc9-361">レシート カード C#</span><span class="sxs-lookup"><span data-stu-id="3fcc9-361">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="3fcc9-362">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-362">Signin card</span></span>

<span data-ttu-id="3fcc9-363">Teamsのサインイン カードは、ボット フレームワークのサインイン カードに似ていますが、Teams は 2 つのアクションのみをサポートしています `signin` `openUrl` 。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-363">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions `signin` and `openUrl`.</span></span>

<span data-ttu-id="3fcc9-364">サインイン アクションは、サインイン カードだけでなく、Teams のすべてのカードで使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-364">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="3fcc9-365">詳細については、「ボットの[認証フロー Teamsを参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-365">For more information, see [Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="3fcc9-366">サインイン カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3fcc9-366">Support for signin cards</span></span>

<span data-ttu-id="3fcc9-367">次の表に、サインイン カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-367">The following table provides the features that support signin cards:</span></span>

| <span data-ttu-id="3fcc9-368">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3fcc9-368">Bots in Teams</span></span> | <span data-ttu-id="3fcc9-369">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3fcc9-369">Messaging extensions</span></span>  | <span data-ttu-id="3fcc9-370">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-370">Connectors</span></span> | <span data-ttu-id="3fcc9-371">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3fcc9-371">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fcc9-372">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-372">✔</span></span> | <span data-ttu-id="3fcc9-373">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-373">✖</span></span> | <span data-ttu-id="3fcc9-374">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-374">✖</span></span> | <span data-ttu-id="3fcc9-375">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-375">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="3fcc9-376">サインイン カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="3fcc9-376">Additional information on signin cards</span></span>

<span data-ttu-id="3fcc9-377">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-377">Bot Framework reference:</span></span>

* [<span data-ttu-id="3fcc9-378">Signin カード Node.js</span><span class="sxs-lookup"><span data-stu-id="3fcc9-378">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3fcc9-379">サインイン カード C#</span><span class="sxs-lookup"><span data-stu-id="3fcc9-379">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="3fcc9-380">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-380">Thumbnail card</span></span>

<span data-ttu-id="3fcc9-381">簡単な操作可能なメッセージの送信に使用されるサムネイル カードを操作できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-381">You can work with a thumbnail card that is used for sending a simple actionable message.</span></span> <span data-ttu-id="3fcc9-382">通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-382">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="3fcc9-383">サムネイル カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3fcc9-383">Support for thumbnail cards</span></span>

<span data-ttu-id="3fcc9-384">次の表に、サムネイル カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-384">The following table provides the features that support thumbnail cards:</span></span>

| <span data-ttu-id="3fcc9-385">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3fcc9-385">Bots in Teams</span></span> | <span data-ttu-id="3fcc9-386">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3fcc9-386">Messaging extensions</span></span>  | <span data-ttu-id="3fcc9-387">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-387">Connectors</span></span> | <span data-ttu-id="3fcc9-388">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3fcc9-388">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fcc9-389">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-389">✔</span></span> | <span data-ttu-id="3fcc9-390">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-390">✔</span></span> | <span data-ttu-id="3fcc9-391">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-391">✖</span></span> | <span data-ttu-id="3fcc9-392">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-392">✔</span></span> |

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="3fcc9-394">サムネイル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-394">Properties of a thumbnail card</span></span>

<span data-ttu-id="3fcc9-395">次の表に、サムネイル カードのプロパティを示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-395">The following table provides the properties of a thumbnail card:</span></span>

| <span data-ttu-id="3fcc9-396">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-396">Property</span></span> | <span data-ttu-id="3fcc9-397">型</span><span class="sxs-lookup"><span data-stu-id="3fcc9-397">Type</span></span>  | <span data-ttu-id="3fcc9-398">説明</span><span class="sxs-lookup"><span data-stu-id="3fcc9-398">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3fcc9-399">title</span><span class="sxs-lookup"><span data-stu-id="3fcc9-399">title</span></span> | <span data-ttu-id="3fcc9-400">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-400">Rich text</span></span> | <span data-ttu-id="3fcc9-401">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-401">Title of the card.</span></span> <span data-ttu-id="3fcc9-402">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-402">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3fcc9-403">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="3fcc9-403">subtitle</span></span> | <span data-ttu-id="3fcc9-404">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-404">Rich text</span></span> | <span data-ttu-id="3fcc9-405">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-405">Subtitle of the card.</span></span> <span data-ttu-id="3fcc9-406">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-406">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3fcc9-407">テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-407">text</span></span> | <span data-ttu-id="3fcc9-408">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-408">Rich text</span></span> | <span data-ttu-id="3fcc9-409">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-409">Text appears under the subtitle.</span></span> <span data-ttu-id="3fcc9-410">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-410">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="3fcc9-411">images</span><span class="sxs-lookup"><span data-stu-id="3fcc9-411">images</span></span> | <span data-ttu-id="3fcc9-412">画像の配列</span><span class="sxs-lookup"><span data-stu-id="3fcc9-412">Array of images</span></span> | <span data-ttu-id="3fcc9-413">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-413">Image displayed at the top of the card.</span></span> <span data-ttu-id="3fcc9-414">縦横比 1:1 平方</span><span class="sxs-lookup"><span data-stu-id="3fcc9-414">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="3fcc9-415">buttons</span><span class="sxs-lookup"><span data-stu-id="3fcc9-415">buttons</span></span> | <span data-ttu-id="3fcc9-416">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="3fcc9-416">Array of action objects</span></span> | <span data-ttu-id="3fcc9-417">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-417">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3fcc9-418">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-418">Maximum 6.</span></span> |
| <span data-ttu-id="3fcc9-419">tap</span><span class="sxs-lookup"><span data-stu-id="3fcc9-419">tap</span></span> | <span data-ttu-id="3fcc9-420">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="3fcc9-420">Action object</span></span> | <span data-ttu-id="3fcc9-421">ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-421">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="3fcc9-422">サムネイル カードの例</span><span class="sxs-lookup"><span data-stu-id="3fcc9-422">Example of a thumbnail card</span></span>

<span data-ttu-id="3fcc9-423">次のコードは、サムネイル カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-423">The following code shows an example of a thumbnail card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.thumbnail",
  "content": {
    "title": "Bender",
    "subtitle": "tale of a robot who dared to love",
    "text": "Bender Bending Rodríguez is a main character in the animated television series Futurama. He was created by series creators Matt Groening and David X. Cohen, and is voiced by John DiMaggio",
    "images": [
      {
        "url": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
        "alt": "Bender Rodríguez"
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Thumbs Up",
        "image": "http://moopz.com/assets_c/2012/06/emoji-thumbs-up-150-thumb-autox125-140616.jpg",
        "value": "I like it"
      },
      {
        "type": "imBack",
        "title": "Thumbs Down",
        "image": "http://yourfaceisstupid.com/wp-content/uploads/2014/08/thumbs-down.png",
        "value": "I don't like it"
      },
      {
        "type": "openUrl",
        "title": "I feel lucky",
        "image": "http://thumb9.shutterstock.com/photos/thumb_large/683806/148441982.jpg",
        "value": "https://www.bing.com/images/search?q=bender&qpvt=bender&qpvt=bender&qpvt=bender&FORM=IGRE"
      }
    ],
    "tap": {
      "type": "imBack",
      "value": "Tapped it!"
    }
  }
}
```

### <a name="additional-information"></a><span data-ttu-id="3fcc9-424">追加情報</span><span class="sxs-lookup"><span data-stu-id="3fcc9-424">Additional information</span></span>

<span data-ttu-id="3fcc9-425">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-425">Bot Framework reference:</span></span>

* [<span data-ttu-id="3fcc9-426">サムネイル カード Node.js</span><span class="sxs-lookup"><span data-stu-id="3fcc9-426">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3fcc9-427">サムネイル カード C#</span><span class="sxs-lookup"><span data-stu-id="3fcc9-427">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="3fcc9-428">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="3fcc9-428">Card collections</span></span>

<span data-ttu-id="3fcc9-429">カルーセル コレクションとリスト コレクションを含むカード コレクションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-429">You can work with card collections that include carousel and list collections.</span></span> <span data-ttu-id="3fcc9-430">Teamsはカード コレクションをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-430">Teams supports card collections.</span></span> <span data-ttu-id="3fcc9-431">カード コレクションには、 `builder.AttachmentLayout.carousel` と が含まれます `builder.AttachmentLayout.list` 。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-431">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="3fcc9-432">これらのコレクションには、アダプティブ カード、ヒーロー カード、またはサムネイル カードが含まれる。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-432">These collections contain Adaptive, hero, or thumbnail cards.</span></span>

### <a name="carousel-collection"></a><span data-ttu-id="3fcc9-433">カルーセル コレクション</span><span class="sxs-lookup"><span data-stu-id="3fcc9-433">Carousel collection</span></span>

<span data-ttu-id="3fcc9-434">[カルーセルのレイアウト](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-434">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-carousel-collections"></a><span data-ttu-id="3fcc9-435">カルーセル コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="3fcc9-435">Support for carousel collections</span></span>

<span data-ttu-id="3fcc9-436">次の表に、カルーセル コレクションをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-436">The following table provides the features that support carousel collections:</span></span>

| <span data-ttu-id="3fcc9-437">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3fcc9-437">Bots in Teams</span></span> | <span data-ttu-id="3fcc9-438">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3fcc9-438">Messaging extensions</span></span>  | <span data-ttu-id="3fcc9-439">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-439">Connectors</span></span> | <span data-ttu-id="3fcc9-440">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3fcc9-440">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fcc9-441">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-441">✔</span></span> | <span data-ttu-id="3fcc9-442">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-442">✖</span></span> | <span data-ttu-id="3fcc9-443">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-443">✖</span></span> | <span data-ttu-id="3fcc9-444">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-444">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="3fcc9-445">カルーセルは、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-445">A carousel can display a maximum of ten cards per message.</span></span>

#### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="3fcc9-446">カルーセル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-446">Properties of a carousel card</span></span>

<span data-ttu-id="3fcc9-447">カルーセル カードのプロパティは、ヒーロー カードとサムネイル カードと同じです。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-447">Properties of a carousel card are same as the hero and thumbnail cards.</span></span>

#### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="3fcc9-448">カルーセル コレクションの例</span><span class="sxs-lookup"><span data-stu-id="3fcc9-448">Example of a carousel collection</span></span>

![カードのカルーセルの例](~/assets/images/cards/carousel.png)

<span data-ttu-id="3fcc9-450">次のコードは、カルーセル コレクションの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-450">The following code shows an example of a carousel collection:</span></span>

```json
{
 "attachmentLayout": "carousel",
 "attachments":[
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "extraLarge",
                "weight": "bolder",
                "text": "Welcome to Employee Connect",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "size": "medium",
                "weight": "bolder",
                "text": "Add events to your calendar",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "The bot can send \r\rnotification to remind \r\ryou about the latest \r\revents and trainings.",
                "wrap": true,
                "height": "stretch"
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee connect"
              },
              {
                "type": "TextBlock",
                "text": "The bot can send notifications \r\rto remind you about the latest \r\r events and trainings",
                "wrap": true,
                "maxWidth": 2
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee Connect final"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Create and manage your tasks",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "text": "The app identifies all your pending tasks \r\r and helps you manage everything at \r\r one place.",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Try these commands \r\r- Pending Submissions \r\r- Pending Approvals- My Tools",
                "wrap": true,
                "height": "stretch"
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    }
  ]
}
```

#### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="3fcc9-451">カルーセル コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="3fcc9-451">Syntax for carousel collections</span></span>

<span data-ttu-id="3fcc9-452">`builder.AttachmentLayoutTypes.Carousel` はカルーセル コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-452">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

### <a name="list-collection"></a><span data-ttu-id="3fcc9-453">リスト コレクション</span><span class="sxs-lookup"><span data-stu-id="3fcc9-453">List collection</span></span>

<span data-ttu-id="3fcc9-454">リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-454">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-list-collections"></a><span data-ttu-id="3fcc9-455">リスト コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="3fcc9-455">Support for list collections</span></span>

<span data-ttu-id="3fcc9-456">次の表に、リスト コレクションをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-456">The following table provides the features that support list collections:</span></span>

| <span data-ttu-id="3fcc9-457">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3fcc9-457">Bots in Teams</span></span> | <span data-ttu-id="3fcc9-458">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3fcc9-458">Messaging extensions</span></span>  | <span data-ttu-id="3fcc9-459">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3fcc9-459">Connectors</span></span> | <span data-ttu-id="3fcc9-460">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3fcc9-460">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fcc9-461">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-461">✔</span></span> | <span data-ttu-id="3fcc9-462">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-462">✔</span></span> | <span data-ttu-id="3fcc9-463">✖</span><span class="sxs-lookup"><span data-stu-id="3fcc9-463">✖</span></span> | <span data-ttu-id="3fcc9-464">✔</span><span class="sxs-lookup"><span data-stu-id="3fcc9-464">✔</span></span> |

#### <a name="example-of-a-list-collection"></a><span data-ttu-id="3fcc9-465">リスト コレクションの例</span><span class="sxs-lookup"><span data-stu-id="3fcc9-465">Example of a list collection</span></span>

![カードのリストの例](~/assets/images/cards/list.png)

<span data-ttu-id="3fcc9-467">リスト コレクションのプロパティは、ヒーロー カードまたはサムネイル カードと同じです。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-467">Properties of list collections are same as the hero or thumbnail cards.</span></span>

<span data-ttu-id="3fcc9-468">リストには、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-468">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="3fcc9-469">iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-469">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

#### <a name="syntax-for-list-collections"></a><span data-ttu-id="3fcc9-470">リスト コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="3fcc9-470">Syntax for list collections</span></span>

<span data-ttu-id="3fcc9-471">`builder.AttachmentLayout.list` はリスト コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-471">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="3fcc9-472">Teams でサポートされていないカード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-472">Cards not supported in Teams</span></span>

<span data-ttu-id="3fcc9-473">次のカードは Bot Framework によって実装されますが、ボット フレームワークではTeams。</span><span class="sxs-lookup"><span data-stu-id="3fcc9-473">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="3fcc9-474">アニメーション カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-474">Animation cards</span></span>
* <span data-ttu-id="3fcc9-475">オーディオ カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-475">Audio cards</span></span>
* <span data-ttu-id="3fcc9-476">ビデオ カード</span><span class="sxs-lookup"><span data-stu-id="3fcc9-476">Video cards</span></span>

## <a name="see-also"></a><span data-ttu-id="3fcc9-477">関連項目</span><span class="sxs-lookup"><span data-stu-id="3fcc9-477">See also</span></span>

* [<span data-ttu-id="3fcc9-478">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="3fcc9-478">Task modules</span></span>](~/task-modules-and-cards/what-are-task-modules.md)
* [<span data-ttu-id="3fcc9-479">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="3fcc9-479">Format cards</span></span>](~/task-modules-and-cards/cards/cards-format.md)
