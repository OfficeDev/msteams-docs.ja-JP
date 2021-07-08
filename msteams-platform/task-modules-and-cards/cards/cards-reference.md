---
title: カードの種類
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
localization_priority: Normal
keywords: Bot のカード リファレンス
ms.topic: reference
ms.openlocfilehash: d3b84344eccee7c2595b0e978c72d7e331b198cb
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328073"
---
# <a name="types-of-cards"></a><span data-ttu-id="3b4f2-104">カードの種類</span><span class="sxs-lookup"><span data-stu-id="3b4f2-104">Types of cards</span></span>

<span data-ttu-id="3b4f2-105">アダプティブ、ヒーロー、リスト、Office 365 コネクタ、レシート、サインイン、サムネイル カード、およびカード コレクションは、Microsoft Teams のボットでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="3b4f2-106">Bot Framework で定義されたカードに基づいていますが、すべての Bot Framework カードが Teams でサポートされているわけではなく、独自のカードがいくつか追加されています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span>

<span data-ttu-id="3b4f2-107">さまざまなカードの種類を特定する前に、ヒーロー カード、サムネイル カード、アダプティブ カードを作成する方法を理解してください。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-107">Before you identify the different card types, understand how to create a a hero card, thumbnail card, or Adaptive Card.</span></span>

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a><span data-ttu-id="3b4f2-108">ヒーロー カード、サムネイル カード、アダプティブ カードを作成する</span><span class="sxs-lookup"><span data-stu-id="3b4f2-108">Create a hero card, thumbnail card, or Adaptive Card</span></span>

<span data-ttu-id="3b4f2-109">**App Studio からヒーロー カード、サムネイル カード、アダプティブ カードを作成するには**</span><span class="sxs-lookup"><span data-stu-id="3b4f2-109">**To create a hero card, thumbnail card, or Adaptive Card from App Studio**</span></span>

1. <span data-ttu-id="3b4f2-110">[アプリ スタジオ]**に** 移動Teams。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-110">Go to **App Studio** from Teams.</span></span>
1. <span data-ttu-id="3b4f2-111">[カード **エディター] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-111">Select **Card editor**.</span></span>
1. <span data-ttu-id="3b4f2-112">[新 **しいカードを作成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-112">Select **Create a new card**.</span></span>
1. <span data-ttu-id="3b4f2-113">[**ヒーロー カード**]、[サムネイルカード]、または [アダプティブ カード] のいずれかのカードに対して [作成]**を選択します**。 </span><span class="sxs-lookup"><span data-stu-id="3b4f2-113">Select **Create** for one of the cards from **Hero Card**, **Thumbnail Card**, or **Adaptive Card**.</span></span> <span data-ttu-id="3b4f2-114">そのカードのメタデータの詳細、ボタン、json、csharp、およびノード コードの例が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-114">The metadata details, buttons, and json, csharp, and node code examples are shown for that card.</span></span>

    ![ヒーロー カードの詳細](~/assets/images/Cards/Herocarddetails.png)

1. <span data-ttu-id="3b4f2-116">[この **カードを送信する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-116">Select **Send me this card**.</span></span> <span data-ttu-id="3b4f2-117">カードがチャット メッセージとして送信されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-117">The card is sent to you as a chat message.</span></span>

## <a name="card-examples"></a><span data-ttu-id="3b4f2-118">カードの例</span><span class="sxs-lookup"><span data-stu-id="3b4f2-118">Card examples</span></span>

<span data-ttu-id="3b4f2-119">カードの使用方法に関する追加情報については、Bot Builder SDK v3 のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-119">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="3b4f2-120">コード サンプルは **、Microsoft/BotBuilder-Samples リポジトリ (microsoft/BotBuilder-Samples** リポジトリ) GitHub。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-120">Code samples are also available in the **Microsoft/BotBuilder-Samples** repository on GitHub.</span></span> <span data-ttu-id="3b4f2-121">カードの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-121">Following are a few card examples:</span></span>

* <span data-ttu-id="3b4f2-122">.NET</span><span class="sxs-lookup"><span data-stu-id="3b4f2-122">.NET</span></span>
  * <span data-ttu-id="3b4f2-123">[メッセージに添付ファイルとしてカードを追加します](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-123">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="3b4f2-124">[カードのサンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-124">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="3b4f2-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="3b4f2-125">Node.js</span></span>
  * <span data-ttu-id="3b4f2-126">[メッセージに添付ファイルとしてカードを追加します](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-126">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="3b4f2-127">[カードのサンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-127">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="card-types"></a><span data-ttu-id="3b4f2-128">カードの種類</span><span class="sxs-lookup"><span data-stu-id="3b4f2-128">Card types</span></span>

<span data-ttu-id="3b4f2-129">アプリケーション要件に基づいて、さまざまな種類のカードを識別して使用できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-129">You can identify and use different types of cards based on your application requirements.</span></span> <span data-ttu-id="3b4f2-130">次の表に、使用可能なカードの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-130">The following table shows the types of cards available to you:</span></span>

| <span data-ttu-id="3b4f2-131">カードの種類</span><span class="sxs-lookup"><span data-stu-id="3b4f2-131">Card type</span></span> | <span data-ttu-id="3b4f2-132">説明</span><span class="sxs-lookup"><span data-stu-id="3b4f2-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="3b4f2-133">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-133">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="3b4f2-134">このカードは高度にカスタマイズ可能で、テキスト、音声、画像、ボタン、および入力フィールドの任意の組み合わせを含めできます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-134">This card is highly customizable and can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="3b4f2-135">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-135">Hero card</span></span>](#hero-card) | <span data-ttu-id="3b4f2-136">このカードには、通常、1 つの大きな画像、1 つ以上のボタン、および少量のテキストが含まれる。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-136">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="3b4f2-137">リスト カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-137">List card</span></span>](#list-card) | <span data-ttu-id="3b4f2-138">このカードには、アイテムのスクロール リストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-138">This card contains a scrolling list of items.</span></span> |
| [<span data-ttu-id="3b4f2-139">Office 365コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-139">Office 365 Connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="3b4f2-140">このカードには、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトがあります。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-140">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="3b4f2-141">レシート カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-141">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="3b4f2-142">このカードは、ユーザーにレシートを提供します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-142">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="3b4f2-143">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-143">Signin card</span></span>](#signin-card) | <span data-ttu-id="3b4f2-144">このカードを使用すると、ボットはユーザーのサインインを要求できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-144">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="3b4f2-145">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-145">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="3b4f2-146">このカードには、通常、1 つのサムネイル 画像、短いテキスト、および 1 つ以上のボタンが含まれる。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-146">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="3b4f2-147">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="3b4f2-147">Card collections</span></span>](#card-collections) | <span data-ttu-id="3b4f2-148">このカード コレクションは、1 つの応答で複数のアイテムを返す場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-148">This card collection is used to return multiple items in a single response.</span></span> |

## <a name="features-that-support-different-card-types"></a><span data-ttu-id="3b4f2-149">さまざまな種類のカードをサポートする機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-149">Features that support different card types</span></span>

| <span data-ttu-id="3b4f2-150">カードの種類</span><span class="sxs-lookup"><span data-stu-id="3b4f2-150">Card type</span></span> | <span data-ttu-id="3b4f2-151">ボット</span><span class="sxs-lookup"><span data-stu-id="3b4f2-151">Bots</span></span> | <span data-ttu-id="3b4f2-152">メッセージ拡張機能のプレビュー</span><span class="sxs-lookup"><span data-stu-id="3b4f2-152">Message extension previews</span></span> | <span data-ttu-id="3b4f2-153">メッセージ拡張機能の結果</span><span class="sxs-lookup"><span data-stu-id="3b4f2-153">Message extension results</span></span> | <span data-ttu-id="3b4f2-154">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="3b4f2-154">Task modules</span></span> | <span data-ttu-id="3b4f2-155">送信 Webhooks</span><span class="sxs-lookup"><span data-stu-id="3b4f2-155">Outgoing Webhooks</span></span> | <span data-ttu-id="3b4f2-156">受信 Webhooks</span><span class="sxs-lookup"><span data-stu-id="3b4f2-156">Incoming Webhooks</span></span> | <span data-ttu-id="3b4f2-157">O365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-157">O365 Connectors</span></span> |
| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-158">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-158">Adaptive Card</span></span> | <span data-ttu-id="3b4f2-159">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-159">✔</span></span> | <span data-ttu-id="3b4f2-160">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-160">✖</span></span> | <span data-ttu-id="3b4f2-161">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-161">✔</span></span> | <span data-ttu-id="3b4f2-162">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-162">✔</span></span> | <span data-ttu-id="3b4f2-163">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-163">✔</span></span> | <span data-ttu-id="3b4f2-164">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-164">✔</span></span> | <span data-ttu-id="3b4f2-165">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-165">✖</span></span> |
| <span data-ttu-id="3b4f2-166">O365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-166">O365 Connector card</span></span> | <span data-ttu-id="3b4f2-167">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-167">✔</span></span> | <span data-ttu-id="3b4f2-168">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-168">✖</span></span> | <span data-ttu-id="3b4f2-169">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-169">✔</span></span> | <span data-ttu-id="3b4f2-170">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-170">✖</span></span> | <span data-ttu-id="3b4f2-171">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-171">✔</span></span> | <span data-ttu-id="3b4f2-172">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-172">✔</span></span> | <span data-ttu-id="3b4f2-173">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-173">✔</span></span> |
| <span data-ttu-id="3b4f2-174">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-174">Hero card</span></span> | <span data-ttu-id="3b4f2-175">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-175">✔</span></span> | <span data-ttu-id="3b4f2-176">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-176">✔</span></span> | <span data-ttu-id="3b4f2-177">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-177">✔</span></span> | <span data-ttu-id="3b4f2-178">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-178">✖</span></span> | <span data-ttu-id="3b4f2-179">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-179">✔</span></span> | <span data-ttu-id="3b4f2-180">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-180">✔</span></span> | <span data-ttu-id="3b4f2-181">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-181">✖</span></span> |
| <span data-ttu-id="3b4f2-182">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-182">Thumbnail card</span></span> | <span data-ttu-id="3b4f2-183">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-183">✔</span></span> | <span data-ttu-id="3b4f2-184">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-184">✔</span></span> | <span data-ttu-id="3b4f2-185">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-185">✔</span></span> | <span data-ttu-id="3b4f2-186">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-186">✖</span></span> | <span data-ttu-id="3b4f2-187">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-187">✔</span></span> | <span data-ttu-id="3b4f2-188">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-188">✔</span></span> | <span data-ttu-id="3b4f2-189">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-189">✖</span></span> |
| <span data-ttu-id="3b4f2-190">リスト カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-190">List card</span></span> | <span data-ttu-id="3b4f2-191">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-191">✔</span></span> | <span data-ttu-id="3b4f2-192">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-192">✖</span></span> | <span data-ttu-id="3b4f2-193">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-193">✖</span></span> | <span data-ttu-id="3b4f2-194">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-194">✖</span></span> | <span data-ttu-id="3b4f2-195">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-195">✔</span></span> | <span data-ttu-id="3b4f2-196">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-196">✔</span></span> | <span data-ttu-id="3b4f2-197">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-197">✖</span></span> |
| <span data-ttu-id="3b4f2-198">レシート カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-198">Receipt card</span></span> | <span data-ttu-id="3b4f2-199">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-199">✔</span></span> | <span data-ttu-id="3b4f2-200">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-200">✖</span></span> | <span data-ttu-id="3b4f2-201">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-201">✖</span></span> | <span data-ttu-id="3b4f2-202">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-202">✖</span></span> | <span data-ttu-id="3b4f2-203">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-203">✖</span></span> | <span data-ttu-id="3b4f2-204">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-204">✔</span></span> | <span data-ttu-id="3b4f2-205">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-205">✖</span></span> |
| <span data-ttu-id="3b4f2-206">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-206">Signin card</span></span> | <span data-ttu-id="3b4f2-207">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-207">✔</span></span> | <span data-ttu-id="3b4f2-208">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-208">✖</span></span> | <span data-ttu-id="3b4f2-209">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-209">✖</span></span> | <span data-ttu-id="3b4f2-210">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-210">✖</span></span> | <span data-ttu-id="3b4f2-211">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-211">✖</span></span> | <span data-ttu-id="3b4f2-212">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-212">✖</span></span> | <span data-ttu-id="3b4f2-213">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-213">✖</span></span> |

> [!NOTE]
> <span data-ttu-id="3b4f2-214">受信 Webhooks のアダプティブ カードでは、ネイティブのアダプティブ カード スキーマ要素 (ただし、 を除く) `Action.Submit` はすべて完全にサポートされます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-214">For Adaptive Cards in Incoming Webhooks, all native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span> <span data-ttu-id="3b4f2-215">サポートされているアクションは [**、Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**、Action.ShowCard、Action.ToggleVisibility、**](https://adaptivecards.io/explorer/Action.ShowCard.html)およびAction.Exe [**です**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。 [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)</span><span class="sxs-lookup"><span data-stu-id="3b4f2-215">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html), and [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="3b4f2-216">すべてのカードの共通プロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-216">Common properties for all cards</span></span>

<span data-ttu-id="3b4f2-217">すべてのカードに適用できる一般的なプロパティを確認できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-217">You can go through some common properties that are applicable to all cards.</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="3b4f2-218">インライン カードの画像</span><span class="sxs-lookup"><span data-stu-id="3b4f2-218">Inline card images</span></span>

<span data-ttu-id="3b4f2-219">カードには、公開されている画像へのリンクを含め、インライン イメージを含めできます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-219">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="3b4f2-220">パフォーマンス上の目的で、イメージをパブリック サーバー (Content Delivery Network) でホストCDN。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-220">For performance purposes, it is highly recommended you host the image on a public Content Delivery Network (CDN).</span></span>

<span data-ttu-id="3b4f2-221">画像のサイズを拡大または縮小して、画像領域をカバーするための縦横比を維持します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-221">Images are scaled up or down in size to maintain the aspect ratio for covering the image area.</span></span> <span data-ttu-id="3b4f2-222">次に、カードの適切な縦横比を実現するために、中央から画像がトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-222">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="3b4f2-223">画像は最大 1024、×1024、PNG、JPEG、または GIF 形式である必要があります。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-223">Images must be at most 1024×1024 and in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="3b4f2-224">アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-224">Animated GIF is not supported.</span></span>

<span data-ttu-id="3b4f2-225">次の表に、インライン カード イメージのプロパティを示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-225">The following table provides the properties of inline card images:</span></span>

| <span data-ttu-id="3b4f2-226">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-226">Property</span></span> | <span data-ttu-id="3b4f2-227">種類</span><span class="sxs-lookup"><span data-stu-id="3b4f2-227">Type</span></span>  | <span data-ttu-id="3b4f2-228">説明</span><span class="sxs-lookup"><span data-stu-id="3b4f2-228">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b4f2-229">url</span><span class="sxs-lookup"><span data-stu-id="3b4f2-229">url</span></span> | <span data-ttu-id="3b4f2-230">URL</span><span class="sxs-lookup"><span data-stu-id="3b4f2-230">URL</span></span> | <span data-ttu-id="3b4f2-231">イメージの HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-231">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="3b4f2-232">alt</span><span class="sxs-lookup"><span data-stu-id="3b4f2-232">alt</span></span> | <span data-ttu-id="3b4f2-233">文字列</span><span class="sxs-lookup"><span data-stu-id="3b4f2-233">String</span></span> | <span data-ttu-id="3b4f2-234">画像のアクセス可能な説明。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-234">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="3b4f2-235">最終的なイメージの前にリダイレクトされるイメージ URL がカードに含まれる場合、イメージ URL のリダイレクトはサポートされません。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-235">If a card includes an image URL that is redirected before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="3b4f2-236">これは、パブリック クラウド上で共有されるイメージに対して発生します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-236">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="3b4f2-237">ボタン</span><span class="sxs-lookup"><span data-stu-id="3b4f2-237">Buttons</span></span>

<span data-ttu-id="3b4f2-238">ボタンはカードの下部に上下に並んで表示されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-238">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="3b4f2-239">ボタンのテキストは常に 1 行に表示され、テキストがボタンの幅を超えると切り捨てされます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-239">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="3b4f2-240">カードでサポートされている最大数を超える追加のボタンは表示されません。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-240">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="3b4f2-241">詳細については、「カードアクション [」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-241">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="3b4f2-242">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="3b4f2-242">Card formatting</span></span>

<span data-ttu-id="3b4f2-243">カードのテキスト書式の詳細については、「カードの書式設定」 [を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-243">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

<span data-ttu-id="3b4f2-244">すべてのカードの共通プロパティを特定した後、アダプティブ カードを操作し、アクション可能なコンテンツを使用するアプリに直接追加することで、エンゲージメントと効率を向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-244">After identifying the common properties for all cards, you can now work with Adaptive Cards, which help you increase engagement and efficiency by adding your actionable content directly into the apps you use.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="3b4f2-245">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-245">Adaptive Card</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="3b4f2-246">アダプティブ カードは、テキスト、音声、画像、ボタン、および入力フィールドの任意の組み合わせを含むカスタマイズ可能なカードです。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-246">An Adaptive Card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="3b4f2-247">詳細については [、「Adaptive Cards v1.2.0」を参照してください](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-247">For more information, see [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="3b4f2-248">アダプティブ カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3b4f2-248">Support for Adaptive Cards</span></span>

<span data-ttu-id="3b4f2-249">次の表に、アダプティブ カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-249">The following table provides the features that support Adaptive Cards:</span></span>

| <span data-ttu-id="3b4f2-250">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-250">Bots in Teams</span></span> | <span data-ttu-id="3b4f2-251">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-251">Messaging extensions</span></span>  | <span data-ttu-id="3b4f2-252">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-252">Connectors</span></span> | <span data-ttu-id="3b4f2-253">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b4f2-253">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-254">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-254">✔</span></span> | <span data-ttu-id="3b4f2-255">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-255">✔</span></span> | <span data-ttu-id="3b4f2-256">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-256">✖</span></span> | <span data-ttu-id="3b4f2-257">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-257">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="3b4f2-258">Teamsプラットフォームは、アダプティブ カード機能の v1.2 以前をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-258">Teams platform supports v1.2 or earlier of Adaptive Card features.</span></span>
> * <span data-ttu-id="3b4f2-259">正または破壊的なアクションのスタイル設定は、プラットフォーム上のアダプティブ カードではTeamsされません。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-259">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="3b4f2-260">メディア要素は、現在、プラットフォーム上のアダプティブ カードTeamsされていません。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-260">Media elements are currently not supported in Adaptive Card on the Teams platform.</span></span>

### <a name="example-of-adaptive-card"></a><span data-ttu-id="3b4f2-261">アダプティブ カードの例</span><span class="sxs-lookup"><span data-stu-id="3b4f2-261">Example of Adaptive Card</span></span>

![アダプティブ カードの例](~/assets/images/cards/adaptivecard.png)

<span data-ttu-id="3b4f2-263">次のコードは、アダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-263">The following code shows an example of an Adaptive Card:</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="3b4f2-264">アダプティブ カードの追加情報</span><span class="sxs-lookup"><span data-stu-id="3b4f2-264">Additional information on Adaptive Cards</span></span>

<span data-ttu-id="3b4f2-265">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-265">Bot Framework reference:</span></span>

* [<span data-ttu-id="3b4f2-266">アダプティブ カード ノード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-266">Adaptive Cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="3b4f2-267">アダプティブ カード C#</span><span class="sxs-lookup"><span data-stu-id="3b4f2-267">Adaptive Card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

<span data-ttu-id="3b4f2-268">これで、潜在的なユーザー選択を視覚的に強調表示するために使用される多目的カードであるヒーロー カードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-268">You can now work with a hero card, which is a multipurpose card used to visually highlight a potential user selection.</span></span>

## <a name="hero-card"></a><span data-ttu-id="3b4f2-269">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-269">Hero card</span></span>

<span data-ttu-id="3b4f2-270">通常、1 つの大きな画像、1 つ以上のボタン、およびテキストを含むカード。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-270">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="3b4f2-271">ヒーロー カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3b4f2-271">Support for hero cards</span></span>

<span data-ttu-id="3b4f2-272">次の表に、ヒーロー カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-272">The following table provides the features that support hero cards:</span></span>

| <span data-ttu-id="3b4f2-273">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-273">Bots in Teams</span></span> | <span data-ttu-id="3b4f2-274">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-274">Messaging extensions</span></span>  | <span data-ttu-id="3b4f2-275">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-275">Connectors</span></span> | <span data-ttu-id="3b4f2-276">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b4f2-276">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-277">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-277">✔</span></span> | <span data-ttu-id="3b4f2-278">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-278">✔</span></span> | <span data-ttu-id="3b4f2-279">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-279">✖</span></span> | <span data-ttu-id="3b4f2-280">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-280">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="3b4f2-281">ヒーロー カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-281">Properties of a hero card</span></span>

<span data-ttu-id="3b4f2-282">次の表に、ヒーロー カードのプロパティを示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-282">The following table provides the properties of a hero card:</span></span>

| <span data-ttu-id="3b4f2-283">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-283">Property</span></span> | <span data-ttu-id="3b4f2-284">種類</span><span class="sxs-lookup"><span data-stu-id="3b4f2-284">Type</span></span>  | <span data-ttu-id="3b4f2-285">説明</span><span class="sxs-lookup"><span data-stu-id="3b4f2-285">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b4f2-286">title</span><span class="sxs-lookup"><span data-stu-id="3b4f2-286">title</span></span> | <span data-ttu-id="3b4f2-287">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-287">Rich text</span></span> | <span data-ttu-id="3b4f2-288">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-288">Title of the card.</span></span> <span data-ttu-id="3b4f2-289">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-289">Maximum two lines.</span></span> |
| <span data-ttu-id="3b4f2-290">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="3b4f2-290">subtitle</span></span> | <span data-ttu-id="3b4f2-291">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-291">Rich text</span></span> | <span data-ttu-id="3b4f2-292">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-292">Subtitle of the card.</span></span> <span data-ttu-id="3b4f2-293">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-293">Maximum two lines.</span></span>|
| <span data-ttu-id="3b4f2-294">テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-294">text</span></span> | <span data-ttu-id="3b4f2-295">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-295">Rich text</span></span> | <span data-ttu-id="3b4f2-296">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-296">Text appears under the subtitle.</span></span> <span data-ttu-id="3b4f2-297">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-297">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="3b4f2-298">images</span><span class="sxs-lookup"><span data-stu-id="3b4f2-298">images</span></span> | <span data-ttu-id="3b4f2-299">画像の配列</span><span class="sxs-lookup"><span data-stu-id="3b4f2-299">Array of images</span></span> | <span data-ttu-id="3b4f2-300">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-300">Image displayed at the top of the card.</span></span> <span data-ttu-id="3b4f2-301">縦横比 16:9。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-301">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="3b4f2-302">buttons</span><span class="sxs-lookup"><span data-stu-id="3b4f2-302">buttons</span></span> | <span data-ttu-id="3b4f2-303">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="3b4f2-303">Array of action objects</span></span> | <span data-ttu-id="3b4f2-304">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-304">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3b4f2-305">最大 6 個。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-305">Maximum six.</span></span> |
| <span data-ttu-id="3b4f2-306">tap</span><span class="sxs-lookup"><span data-stu-id="3b4f2-306">tap</span></span> | <span data-ttu-id="3b4f2-307">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-307">Action object</span></span> | <span data-ttu-id="3b4f2-308">ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-308">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="3b4f2-309">ヒーロー カードの例</span><span class="sxs-lookup"><span data-stu-id="3b4f2-309">Example of a hero card</span></span>

![ヒーロー カードの例](~/assets/images/cards/hero.png)

<span data-ttu-id="3b4f2-311">次のコードは、ヒーロー カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-311">The following code shows an example of a hero card:</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="3b4f2-312">ヒーロー カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="3b4f2-312">Additional information on hero cards</span></span>

<span data-ttu-id="3b4f2-313">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-313">Bot Framework reference:</span></span>

* [<span data-ttu-id="3b4f2-314">ヒーロー カード Node.js</span><span class="sxs-lookup"><span data-stu-id="3b4f2-314">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="3b4f2-315">ヒーロー カード C#</span><span class="sxs-lookup"><span data-stu-id="3b4f2-315">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="3b4f2-316">リスト カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-316">List card</span></span>

<span data-ttu-id="3b4f2-317">リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-317">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="3b4f2-318">リスト カードは、アイテムのスクロール リストを提供します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-318">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="3b4f2-319">リスト カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3b4f2-319">Support for list cards</span></span>

<span data-ttu-id="3b4f2-320">次の表に、リスト カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-320">The following table provides the features that support list cards:</span></span>

| <span data-ttu-id="3b4f2-321">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-321">Bots in Teams</span></span> | <span data-ttu-id="3b4f2-322">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-322">Messaging extensions</span></span>  | <span data-ttu-id="3b4f2-323">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-323">Connectors</span></span> | <span data-ttu-id="3b4f2-324">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b4f2-324">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-325">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-325">✔</span></span> | <span data-ttu-id="3b4f2-326">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-326">✖</span></span> | <span data-ttu-id="3b4f2-327">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-327">✖</span></span> |<span data-ttu-id="3b4f2-328">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-328">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="3b4f2-329">リスト カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-329">Properties of a list card</span></span>

<span data-ttu-id="3b4f2-330">次の表に、リスト カードのプロパティを示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-330">The following table provides the properties of a list card:</span></span>

| <span data-ttu-id="3b4f2-331">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-331">Property</span></span> | <span data-ttu-id="3b4f2-332">種類</span><span class="sxs-lookup"><span data-stu-id="3b4f2-332">Type</span></span>  | <span data-ttu-id="3b4f2-333">説明</span><span class="sxs-lookup"><span data-stu-id="3b4f2-333">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b4f2-334">title</span><span class="sxs-lookup"><span data-stu-id="3b4f2-334">title</span></span> | <span data-ttu-id="3b4f2-335">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-335">Rich text</span></span> | <span data-ttu-id="3b4f2-336">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-336">Title of the card.</span></span> <span data-ttu-id="3b4f2-337">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-337">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3b4f2-338">アイテム</span><span class="sxs-lookup"><span data-stu-id="3b4f2-338">items</span></span> | <span data-ttu-id="3b4f2-339">リスト アイテムの配列</span><span class="sxs-lookup"><span data-stu-id="3b4f2-339">Array of list items</span></span> | <span data-ttu-id="3b4f2-340">カードに適用可能なアイテムのセット。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-340">Set of items applicable to the card.</span></span>|
| <span data-ttu-id="3b4f2-341">buttons</span><span class="sxs-lookup"><span data-stu-id="3b4f2-341">buttons</span></span> | <span data-ttu-id="3b4f2-342">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="3b4f2-342">Array of action objects</span></span> | <span data-ttu-id="3b4f2-343">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-343">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3b4f2-344">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-344">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="3b4f2-345">リスト カードの例</span><span class="sxs-lookup"><span data-stu-id="3b4f2-345">Example of a list card</span></span>

<span data-ttu-id="3b4f2-346">次のコードは、リスト カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-346">The following code shows an example of a list card:</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="3b4f2-347">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-347">Office 365 connector card</span></span>

<span data-ttu-id="3b4f2-348">柔軟なレイアウトを提供し、Office 365情報を取得するための優れた方法であるコネクタ カードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-348">You can work with an Office 365 Connector card that provides a flexible layout and is a great way to get useful information.</span></span> <span data-ttu-id="3b4f2-349">コネクタ Office 365はボット フレームワークではなく、Teamsでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-349">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="3b4f2-350">このカードは、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトを提供します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-350">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="3b4f2-351">このカードにはコネクタ カードが含まれているので、ボットで使用できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-351">This card contains a connector card so that it can be used by bots.</span></span> <span data-ttu-id="3b4f2-352">コネクタ カードとコネクタ Office 365の違いについては、「コネクタ カードの追加情報[」をOffice 365してください](#additional-information-on-the-office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-352">For differences between connector cards and the Office 365 Connector card, see [Additional information on the Office 365 Connector card](#additional-information-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="3b4f2-353">コネクタ カードOffice 365サポート</span><span class="sxs-lookup"><span data-stu-id="3b4f2-353">Support for Office 365 Connector cards</span></span>

<span data-ttu-id="3b4f2-354">次の表に、コネクタ カードをサポートするOffice 365示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-354">The following table provides the features that support Office 365 Connector cards:</span></span>

| <span data-ttu-id="3b4f2-355">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-355">Bots in Teams</span></span> | <span data-ttu-id="3b4f2-356">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-356">Messaging extensions</span></span>  | <span data-ttu-id="3b4f2-357">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-357">Connectors</span></span> | <span data-ttu-id="3b4f2-358">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b4f2-358">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-359">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-359">✔</span></span> | <span data-ttu-id="3b4f2-360">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-360">✔</span></span> | <span data-ttu-id="3b4f2-361">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-361">✔</span></span> | <span data-ttu-id="3b4f2-362">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-362">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="3b4f2-363">コネクタ カードOffice 365プロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-363">Properties of the Office 365 Connector card</span></span>

<span data-ttu-id="3b4f2-364">次の表に、コネクタ カードのプロパティOffice 365示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-364">The following table provides the properties of the Office 365 connector card:</span></span>

| <span data-ttu-id="3b4f2-365">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-365">Property</span></span> | <span data-ttu-id="3b4f2-366">種類</span><span class="sxs-lookup"><span data-stu-id="3b4f2-366">Type</span></span>  | <span data-ttu-id="3b4f2-367">説明</span><span class="sxs-lookup"><span data-stu-id="3b4f2-367">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b4f2-368">title</span><span class="sxs-lookup"><span data-stu-id="3b4f2-368">title</span></span> | <span data-ttu-id="3b4f2-369">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-369">Rich text</span></span> | <span data-ttu-id="3b4f2-370">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-370">Title of the card.</span></span> <span data-ttu-id="3b4f2-371">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-371">Maximum two lines.</span></span> |
| <span data-ttu-id="3b4f2-372">概要</span><span class="sxs-lookup"><span data-stu-id="3b4f2-372">summary</span></span> | <span data-ttu-id="3b4f2-373">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-373">Rich text</span></span> | <span data-ttu-id="3b4f2-374">カードの概要。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-374">Summary of the card.</span></span> <span data-ttu-id="3b4f2-375">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-375">Maximum two lines.</span></span> |
| <span data-ttu-id="3b4f2-376">テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-376">text</span></span> | <span data-ttu-id="3b4f2-377">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-377">Rich text</span></span> | <span data-ttu-id="3b4f2-378">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-378">Text appears under the subtitle.</span></span> <span data-ttu-id="3b4f2-379">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-379">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="3b4f2-380">themeColor</span><span class="sxs-lookup"><span data-stu-id="3b4f2-380">themeColor</span></span> | <span data-ttu-id="3b4f2-381">16 進数文字列</span><span class="sxs-lookup"><span data-stu-id="3b4f2-381">HEX string</span></span> | <span data-ttu-id="3b4f2-382">アプリケーション マニフェストから提供される `accentColor` 色を上書きします。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-382">Color that overrides the `accentColor` provided from the application manifest.</span></span> |

### <a name="additional-information-on-the-office-365-connector-card"></a><span data-ttu-id="3b4f2-383">コネクタ カードのOffice 365情報</span><span class="sxs-lookup"><span data-stu-id="3b4f2-383">Additional information on the Office 365 Connector card</span></span>

<span data-ttu-id="3b4f2-384">Office 365コネクタ カードは、アクションなど、Microsoft Teamsで適切に[ `ActionCard` 機能します](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-384">Office 365 Connector cards function properly in Microsoft Teams, including [`ActionCard` actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="3b4f2-385">コネクタからコネクタ カードを使用する場合とボットでコネクタ カードを使用する場合の重要な違いは、カードアクションの処理です。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-385">The important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span> <span data-ttu-id="3b4f2-386">次の表に、相違点の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-386">The following table lists the difference:</span></span>

| <span data-ttu-id="3b4f2-387">Connector</span><span class="sxs-lookup"><span data-stu-id="3b4f2-387">Connector</span></span> | <span data-ttu-id="3b4f2-388">Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-388">Bot</span></span> |
| --- | --- |
| <span data-ttu-id="3b4f2-389">エンドポイントは、HTTP POST を介してカード ペイロードを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-389">The endpoint receives the card payload through HTTP POST.</span></span> | <span data-ttu-id="3b4f2-390">アクション `HttpPOST` は、アクション ID と本文のみをボットに送信 `invoke` するアクティビティをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-390">The `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>|

<span data-ttu-id="3b4f2-391">各コネクタ カードには最大 10 個のセクションを表示できます。各セクションには最大 5 つのイメージと 5 つのアクションを含めできます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-391">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="3b4f2-392">メッセージ内の追加のセクション、イメージ、またはアクションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-392">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="3b4f2-393">すべてのテキスト フィールドは Markdown と HTML をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-393">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="3b4f2-394">メッセージの `markdown` プロパティを設定して、Markdown または HTML を使用するセクションを制御することができます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-394">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="3b4f2-395">既定では `markdown` 、 に設定されています `true` 。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-395">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="3b4f2-396">HTML を代わりに使用する場合は、 に `markdown` 設定します `false` 。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-396">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="3b4f2-397">`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-397">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="3b4f2-398">レンダリング スタイルを指定するには `activityImage` 、次の `activityImageType` 表に示すように設定できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-398">To specify the rendering style for `activityImage`, you can set `activityImageType` as shown in the following table:</span></span>

| <span data-ttu-id="3b4f2-399">値</span><span class="sxs-lookup"><span data-stu-id="3b4f2-399">Value</span></span> | <span data-ttu-id="3b4f2-400">説明</span><span class="sxs-lookup"><span data-stu-id="3b4f2-400">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="3b4f2-401">既定値は `activityImage` 、円としてトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-401">Default, `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="3b4f2-402">`activityImage` は四角形として表示され、縦横比が保持されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-402">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="3b4f2-403">コネクタ カードのプロパティに関するその他の詳細については、「アクション可能な [メッセージ カードリファレンス」を参照してください](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-403">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="3b4f2-404">現在サポートされていないコネクタ Teamsのプロパティは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-404">The only connector card properties that Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="3b4f2-405">`startGroup`常に、次のように `true` 処理Teams</span><span class="sxs-lookup"><span data-stu-id="3b4f2-405">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="3b4f2-406">コネクタ カードOffice 365例</span><span class="sxs-lookup"><span data-stu-id="3b4f2-406">Example of an Office 365 Connector card</span></span>

<span data-ttu-id="3b4f2-407">次のコードは、コネクタ カードの例Office 365示しています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-407">The following code shows an example of an Office 365 Connector card:</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="3b4f2-408">レシート カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-408">Receipt card</span></span>

<span data-ttu-id="3b4f2-409">Teamsカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-409">Teams supports receipt card.</span></span> <span data-ttu-id="3b4f2-410">ボットがユーザーにレシートを提供できるカードです。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-410">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="3b4f2-411">通常、税金や合計情報など、領収書に含めるアイテムの一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-411">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="3b4f2-412">レシート カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3b4f2-412">Support for receipt cards</span></span>

<span data-ttu-id="3b4f2-413">次の表に、レシート カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-413">The following table provides the features that support receipt cards:</span></span>

| <span data-ttu-id="3b4f2-414">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-414">Bots in Teams</span></span> | <span data-ttu-id="3b4f2-415">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-415">Messaging extensions</span></span>  | <span data-ttu-id="3b4f2-416">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-416">Connectors</span></span> | <span data-ttu-id="3b4f2-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b4f2-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-418">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-418">✔</span></span> | <span data-ttu-id="3b4f2-419">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-419">✔</span></span> | <span data-ttu-id="3b4f2-420">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-420">✖</span></span> | <span data-ttu-id="3b4f2-421">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-421">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="3b4f2-422">レシート カードの例</span><span class="sxs-lookup"><span data-stu-id="3b4f2-422">Example of a receipt card</span></span>

![レシート カードの例](~/assets/images/cards/receipt.png)

<span data-ttu-id="3b4f2-424">次のコードは、レシート カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-424">The following code shows an example of a receipt card:</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="3b4f2-425">レシート カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="3b4f2-425">Additional information on receipt cards</span></span>

<span data-ttu-id="3b4f2-426">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-426">Bot Framework reference:</span></span>

* [<span data-ttu-id="3b4f2-427">レシート カードNode.js</span><span class="sxs-lookup"><span data-stu-id="3b4f2-427">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3b4f2-428">レシート カード C#</span><span class="sxs-lookup"><span data-stu-id="3b4f2-428">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="3b4f2-429">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-429">Signin card</span></span>

<span data-ttu-id="3b4f2-430">Teamsのサインイン カードは、ボット フレームワークのサインイン カードに似ていますが、Teams は 2 つのアクションのみをサポートしています `signin` `openUrl` 。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-430">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions `signin` and `openUrl`.</span></span>

<span data-ttu-id="3b4f2-431">サインイン アクションは、サインイン カードだけでなく、Teams のすべてのカードで使用できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-431">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="3b4f2-432">詳細については、「ボットの[認証フロー Teamsを参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-432">For more information, see [Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="3b4f2-433">サインイン カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3b4f2-433">Support for signin cards</span></span>

<span data-ttu-id="3b4f2-434">次の表に、サインイン カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-434">The following table provides the features that support signin cards:</span></span>

| <span data-ttu-id="3b4f2-435">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-435">Bots in Teams</span></span> | <span data-ttu-id="3b4f2-436">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-436">Messaging extensions</span></span>  | <span data-ttu-id="3b4f2-437">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-437">Connectors</span></span> | <span data-ttu-id="3b4f2-438">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b4f2-438">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-439">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-439">✔</span></span> | <span data-ttu-id="3b4f2-440">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-440">✖</span></span> | <span data-ttu-id="3b4f2-441">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-441">✖</span></span> | <span data-ttu-id="3b4f2-442">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-442">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="3b4f2-443">サインイン カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="3b4f2-443">Additional information on signin cards</span></span>

<span data-ttu-id="3b4f2-444">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-444">Bot Framework reference:</span></span>

* [<span data-ttu-id="3b4f2-445">Signin カード Node.js</span><span class="sxs-lookup"><span data-stu-id="3b4f2-445">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3b4f2-446">サインイン カード C#</span><span class="sxs-lookup"><span data-stu-id="3b4f2-446">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="3b4f2-447">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-447">Thumbnail card</span></span>

<span data-ttu-id="3b4f2-448">簡単な操作可能なメッセージの送信に使用されるサムネイル カードを操作できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-448">You can work with a thumbnail card that is used for sending a simple actionable message.</span></span> <span data-ttu-id="3b4f2-449">通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-449">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="3b4f2-450">サムネイル カードのサポート</span><span class="sxs-lookup"><span data-stu-id="3b4f2-450">Support for thumbnail cards</span></span>

<span data-ttu-id="3b4f2-451">次の表に、サムネイル カードをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-451">The following table provides the features that support thumbnail cards:</span></span>

| <span data-ttu-id="3b4f2-452">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-452">Bots in Teams</span></span> | <span data-ttu-id="3b4f2-453">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-453">Messaging extensions</span></span>  | <span data-ttu-id="3b4f2-454">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-454">Connectors</span></span> | <span data-ttu-id="3b4f2-455">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b4f2-455">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-456">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-456">✔</span></span> | <span data-ttu-id="3b4f2-457">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-457">✔</span></span> | <span data-ttu-id="3b4f2-458">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-458">✖</span></span> | <span data-ttu-id="3b4f2-459">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-459">✔</span></span> |

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="3b4f2-461">サムネイル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-461">Properties of a thumbnail card</span></span>

<span data-ttu-id="3b4f2-462">次の表に、サムネイル カードのプロパティを示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-462">The following table provides the properties of a thumbnail card:</span></span>

| <span data-ttu-id="3b4f2-463">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-463">Property</span></span> | <span data-ttu-id="3b4f2-464">種類</span><span class="sxs-lookup"><span data-stu-id="3b4f2-464">Type</span></span>  | <span data-ttu-id="3b4f2-465">説明</span><span class="sxs-lookup"><span data-stu-id="3b4f2-465">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b4f2-466">title</span><span class="sxs-lookup"><span data-stu-id="3b4f2-466">title</span></span> | <span data-ttu-id="3b4f2-467">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-467">Rich text</span></span> | <span data-ttu-id="3b4f2-468">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-468">Title of the card.</span></span> <span data-ttu-id="3b4f2-469">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-469">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3b4f2-470">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="3b4f2-470">subtitle</span></span> | <span data-ttu-id="3b4f2-471">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-471">Rich text</span></span> | <span data-ttu-id="3b4f2-472">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-472">Subtitle of the card.</span></span> <span data-ttu-id="3b4f2-473">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-473">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3b4f2-474">テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-474">text</span></span> | <span data-ttu-id="3b4f2-475">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-475">Rich text</span></span> | <span data-ttu-id="3b4f2-476">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-476">Text appears under the subtitle.</span></span> <span data-ttu-id="3b4f2-477">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-477">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="3b4f2-478">images</span><span class="sxs-lookup"><span data-stu-id="3b4f2-478">images</span></span> | <span data-ttu-id="3b4f2-479">画像の配列</span><span class="sxs-lookup"><span data-stu-id="3b4f2-479">Array of images</span></span> | <span data-ttu-id="3b4f2-480">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-480">Image displayed at the top of the card.</span></span> <span data-ttu-id="3b4f2-481">縦横比 1:1 平方</span><span class="sxs-lookup"><span data-stu-id="3b4f2-481">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="3b4f2-482">buttons</span><span class="sxs-lookup"><span data-stu-id="3b4f2-482">buttons</span></span> | <span data-ttu-id="3b4f2-483">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="3b4f2-483">Array of action objects</span></span> | <span data-ttu-id="3b4f2-484">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-484">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3b4f2-485">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-485">Maximum 6.</span></span> |
| <span data-ttu-id="3b4f2-486">tap</span><span class="sxs-lookup"><span data-stu-id="3b4f2-486">tap</span></span> | <span data-ttu-id="3b4f2-487">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="3b4f2-487">Action object</span></span> | <span data-ttu-id="3b4f2-488">ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-488">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="3b4f2-489">サムネイル カードの例</span><span class="sxs-lookup"><span data-stu-id="3b4f2-489">Example of a thumbnail card</span></span>

<span data-ttu-id="3b4f2-490">次のコードは、サムネイル カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-490">The following code shows an example of a thumbnail card:</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="3b4f2-491">ページの先頭へ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-491">Additional information</span></span>

<span data-ttu-id="3b4f2-492">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-492">Bot Framework reference:</span></span>

* [<span data-ttu-id="3b4f2-493">サムネイル カード Node.js</span><span class="sxs-lookup"><span data-stu-id="3b4f2-493">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3b4f2-494">サムネイル カード C#</span><span class="sxs-lookup"><span data-stu-id="3b4f2-494">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="3b4f2-495">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="3b4f2-495">Card collections</span></span>

<span data-ttu-id="3b4f2-496">カルーセル コレクションとリスト コレクションを含むカード コレクションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-496">You can work with card collections that include carousel and list collections.</span></span> <span data-ttu-id="3b4f2-497">Teamsはカード コレクションをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-497">Teams supports card collections.</span></span> <span data-ttu-id="3b4f2-498">カード コレクションには、 `builder.AttachmentLayout.carousel` と が含まれます `builder.AttachmentLayout.list` 。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-498">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="3b4f2-499">これらのコレクションには、アダプティブ カード、ヒーロー カード、またはサムネイル カードが含まれる。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-499">These collections contain Adaptive, hero, or thumbnail cards.</span></span>

### <a name="carousel-collection"></a><span data-ttu-id="3b4f2-500">カルーセル コレクション</span><span class="sxs-lookup"><span data-stu-id="3b4f2-500">Carousel collection</span></span>

<span data-ttu-id="3b4f2-501">[カルーセルのレイアウト](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-501">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-carousel-collections"></a><span data-ttu-id="3b4f2-502">カルーセル コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="3b4f2-502">Support for carousel collections</span></span>

<span data-ttu-id="3b4f2-503">次の表に、カルーセル コレクションをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-503">The following table provides the features that support carousel collections:</span></span>

| <span data-ttu-id="3b4f2-504">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-504">Bots in Teams</span></span> | <span data-ttu-id="3b4f2-505">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-505">Messaging extensions</span></span>  | <span data-ttu-id="3b4f2-506">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-506">Connectors</span></span> | <span data-ttu-id="3b4f2-507">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b4f2-507">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-508">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-508">✔</span></span> | <span data-ttu-id="3b4f2-509">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-509">✖</span></span> | <span data-ttu-id="3b4f2-510">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-510">✖</span></span> | <span data-ttu-id="3b4f2-511">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-511">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="3b4f2-512">カルーセルは、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-512">A carousel can display a maximum of ten cards per message.</span></span>

#### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="3b4f2-513">カルーセル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-513">Properties of a carousel card</span></span>

<span data-ttu-id="3b4f2-514">カルーセル カードのプロパティは、ヒーロー カードとサムネイル カードと同じです。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-514">Properties of a carousel card are same as the hero and thumbnail cards.</span></span>

#### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="3b4f2-515">カルーセル コレクションの例</span><span class="sxs-lookup"><span data-stu-id="3b4f2-515">Example of a carousel collection</span></span>

![カードのカルーセルの例](~/assets/images/cards/carousel.png)

<span data-ttu-id="3b4f2-517">次のコードは、カルーセル コレクションの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-517">The following code shows an example of a carousel collection:</span></span>

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

#### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="3b4f2-518">カルーセル コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="3b4f2-518">Syntax for carousel collections</span></span>

<span data-ttu-id="3b4f2-519">`builder.AttachmentLayoutTypes.Carousel` はカルーセル コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-519">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

### <a name="list-collection"></a><span data-ttu-id="3b4f2-520">リスト コレクション</span><span class="sxs-lookup"><span data-stu-id="3b4f2-520">List collection</span></span>

<span data-ttu-id="3b4f2-521">リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-521">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-list-collections"></a><span data-ttu-id="3b4f2-522">リスト コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="3b4f2-522">Support for list collections</span></span>

<span data-ttu-id="3b4f2-523">次の表に、リスト コレクションをサポートする機能を示します。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-523">The following table provides the features that support list collections:</span></span>

| <span data-ttu-id="3b4f2-524">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="3b4f2-524">Bots in Teams</span></span> | <span data-ttu-id="3b4f2-525">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3b4f2-525">Messaging extensions</span></span>  | <span data-ttu-id="3b4f2-526">コネクタ</span><span class="sxs-lookup"><span data-stu-id="3b4f2-526">Connectors</span></span> | <span data-ttu-id="3b4f2-527">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b4f2-527">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b4f2-528">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-528">✔</span></span> | <span data-ttu-id="3b4f2-529">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-529">✔</span></span> | <span data-ttu-id="3b4f2-530">✖</span><span class="sxs-lookup"><span data-stu-id="3b4f2-530">✖</span></span> | <span data-ttu-id="3b4f2-531">✔</span><span class="sxs-lookup"><span data-stu-id="3b4f2-531">✔</span></span> |

#### <a name="example-of-a-list-collection"></a><span data-ttu-id="3b4f2-532">リスト コレクションの例</span><span class="sxs-lookup"><span data-stu-id="3b4f2-532">Example of a list collection</span></span>

![カードのリストの例](~/assets/images/cards/list.png)

<span data-ttu-id="3b4f2-534">リスト コレクションのプロパティは、ヒーロー カードまたはサムネイル カードと同じです。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-534">Properties of list collections are same as the hero or thumbnail cards.</span></span>

<span data-ttu-id="3b4f2-535">リストには、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-535">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="3b4f2-536">iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-536">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

#### <a name="syntax-for-list-collections"></a><span data-ttu-id="3b4f2-537">リスト コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="3b4f2-537">Syntax for list collections</span></span>

<span data-ttu-id="3b4f2-538">`builder.AttachmentLayout.list` はリスト コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-538">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="3b4f2-539">Teams でサポートされていないカード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-539">Cards not supported in Teams</span></span>

<span data-ttu-id="3b4f2-540">次のカードは Bot Framework によって実装されますが、ボット フレームワークではTeams。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-540">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="3b4f2-541">アニメーション カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-541">Animation cards</span></span>
* <span data-ttu-id="3b4f2-542">オーディオ カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-542">Audio cards</span></span>
* <span data-ttu-id="3b4f2-543">ビデオ カード</span><span class="sxs-lookup"><span data-stu-id="3b4f2-543">Video cards</span></span>

## <a name="see-also"></a><span data-ttu-id="3b4f2-544">関連項目</span><span class="sxs-lookup"><span data-stu-id="3b4f2-544">See also</span></span>

* [<span data-ttu-id="3b4f2-545">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="3b4f2-545">Task modules</span></span>](~/task-modules-and-cards/what-are-task-modules.md)
* [<span data-ttu-id="3b4f2-546">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="3b4f2-546">Format cards</span></span>](~/task-modules-and-cards/cards/cards-format.md)
