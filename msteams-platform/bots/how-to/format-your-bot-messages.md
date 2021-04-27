---
title: ボット メッセージの書式を設定する
author: clearab
description: ボット メッセージにリッチ書式を追加する
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 7dc082f4b17e123c9fa000552f02fc913c66dcf7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020906"
---
# <a name="format-your-bot-messages"></a><span data-ttu-id="a1227-103">ボット メッセージの書式を設定する</span><span class="sxs-lookup"><span data-stu-id="a1227-103">Format your bot messages</span></span>

<span data-ttu-id="a1227-104">メッセージの書式設定を使用すると、ボット メッセージを最適に表示できます。</span><span class="sxs-lookup"><span data-stu-id="a1227-104">Message formatting enables you to bring out the best in bot messages.</span></span> <span data-ttu-id="a1227-105">ボタン、テキスト、画像、オーディオ、ビデオなどの対話型要素を含む添付ファイルであるリッチ カードをボット メッセージに書式設定できます。</span><span class="sxs-lookup"><span data-stu-id="a1227-105">You can format your bot messages to include rich cards that are attachments that contain interactive elements, such as buttons, text, images, audio, video, and so on.</span></span>

## <a name="format-text-content"></a><span data-ttu-id="a1227-106">テキスト コンテンツの書式設定</span><span class="sxs-lookup"><span data-stu-id="a1227-106">Format text content</span></span>

<span data-ttu-id="a1227-107">ボット メッセージを書式設定するには、省略可能なプロパティを設定して、ボット メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) を制御できます。</span><span class="sxs-lookup"><span data-stu-id="a1227-107">To format your bot messages, you can set the optional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) property to control how your bot message's text content is rendered.</span></span>

<span data-ttu-id="a1227-108">Microsoft Teams では、次の書式設定オプションがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="a1227-108">Microsoft Teams supports the following formatting options:</span></span>

| <span data-ttu-id="a1227-109">`TextFormat` value</span><span class="sxs-lookup"><span data-stu-id="a1227-109">`TextFormat` value</span></span> | <span data-ttu-id="a1227-110">説明</span><span class="sxs-lookup"><span data-stu-id="a1227-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a1227-111">プレーン</span><span class="sxs-lookup"><span data-stu-id="a1227-111">plain</span></span> | <span data-ttu-id="a1227-112">テキストは、書式が適用されずに生テキストとして扱われる必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1227-112">The text must be treated as raw text with no formatting applied.</span></span>|
| <span data-ttu-id="a1227-113">markdown</span><span class="sxs-lookup"><span data-stu-id="a1227-113">markdown</span></span> | <span data-ttu-id="a1227-114">テキストはマークダウンの書式設定として扱い、必要に応じてチャネルにレンダリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1227-114">The text must be treated as markdown formatting and rendered on the channel as appropriate.</span></span> |
| <span data-ttu-id="a1227-115">xml</span><span class="sxs-lookup"><span data-stu-id="a1227-115">xml</span></span> | <span data-ttu-id="a1227-116">テキストは単純な XML マークアップです。</span><span class="sxs-lookup"><span data-stu-id="a1227-116">The text is simple XML markup.</span></span> |

<span data-ttu-id="a1227-117">Teams では、マークダウンタグと XML タグまたは HTML 書式タグのサブセットがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="a1227-117">Teams supports a subset of markdown and XML or HTML formatting tags.</span></span>

<span data-ttu-id="a1227-118">現在、書式設定には次の制限が適用されます。</span><span class="sxs-lookup"><span data-stu-id="a1227-118">Currently, the following limitations apply to formatting:</span></span>

* <span data-ttu-id="a1227-119">テキスト専用メッセージは、テーブルの書式設定をサポートしません。</span><span class="sxs-lookup"><span data-stu-id="a1227-119">Text-only messages do not support table formatting.</span></span>
* <span data-ttu-id="a1227-120">リッチ カードは、タイトルプロパティや字幕プロパティではなく、text プロパティの書式設定のみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="a1227-120">Rich cards support formatting in the text property only, not in the title or subtitle properties.</span></span>
* <span data-ttu-id="a1227-121">リッチ カードでは、マークダウンやテーブルの書式設定はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a1227-121">Rich cards do not support markdown or table formatting.</span></span>

<span data-ttu-id="a1227-122">テキスト コンテンツを書式設定した後は、Microsoft Teams でサポートされているすべてのプラットフォームで書式設定が機能します。</span><span class="sxs-lookup"><span data-stu-id="a1227-122">After you format text content, ensure that your formatting works across all platforms supported by Microsoft Teams.</span></span>

## <a name="cross-platform-support"></a><span data-ttu-id="a1227-123">クロスプラットフォームのサポート</span><span class="sxs-lookup"><span data-stu-id="a1227-123">Cross-platform support</span></span>

<span data-ttu-id="a1227-124">一部のスタイルは現在、すべてのプラットフォームでサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a1227-124">Some styles are currently not supported across all platforms.</span></span> <span data-ttu-id="a1227-125">次の表に、テキスト専用メッセージとリッチ カードでサポートされているスタイルとスタイルの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="a1227-125">The following table provides a list of styles and which of these styles are supported in text-only messages and rich cards:</span></span>

| <span data-ttu-id="a1227-126">Style</span><span class="sxs-lookup"><span data-stu-id="a1227-126">Style</span></span>                     | <span data-ttu-id="a1227-127">テキスト専用メッセージ</span><span class="sxs-lookup"><span data-stu-id="a1227-127">Text-only messages</span></span> | <span data-ttu-id="a1227-128">リッチ カード - XML のみ</span><span class="sxs-lookup"><span data-stu-id="a1227-128">Rich cards - XML only</span></span> |
| ---                       | :---: | :---: |
| <span data-ttu-id="a1227-129">太字</span><span class="sxs-lookup"><span data-stu-id="a1227-129">Bold</span></span>                      | <span data-ttu-id="a1227-130">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-130">✔</span></span> | <span data-ttu-id="a1227-131">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-131">✖</span></span> |
| <span data-ttu-id="a1227-132">斜体</span><span class="sxs-lookup"><span data-stu-id="a1227-132">Italic</span></span>                    | <span data-ttu-id="a1227-133">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-133">✔</span></span> | <span data-ttu-id="a1227-134">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-134">✔</span></span> |
| <span data-ttu-id="a1227-135">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="a1227-135">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a1227-136">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-136">✖</span></span> | <span data-ttu-id="a1227-137">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-137">✔</span></span> |
| <span data-ttu-id="a1227-138">取り消し線</span><span class="sxs-lookup"><span data-stu-id="a1227-138">Strikethrough</span></span>             | <span data-ttu-id="a1227-139">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-139">✖</span></span> | <span data-ttu-id="a1227-140">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-140">✔</span></span> |
| <span data-ttu-id="a1227-141">水平ルーラー</span><span class="sxs-lookup"><span data-stu-id="a1227-141">Horizontal rule</span></span>           | <span data-ttu-id="a1227-142">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-142">✖</span></span> | <span data-ttu-id="a1227-143">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-143">✖</span></span> |
| <span data-ttu-id="a1227-144">記号付きリスト</span><span class="sxs-lookup"><span data-stu-id="a1227-144">Unordered list</span></span>            | <span data-ttu-id="a1227-145">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-145">✖</span></span> | <span data-ttu-id="a1227-146">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-146">✔</span></span> |
| <span data-ttu-id="a1227-147">番号付きリスト</span><span class="sxs-lookup"><span data-stu-id="a1227-147">Ordered list</span></span>              | <span data-ttu-id="a1227-148">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-148">✖</span></span> | <span data-ttu-id="a1227-149">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-149">✔</span></span> |
| <span data-ttu-id="a1227-150">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="a1227-150">Preformatted text</span></span>         | <span data-ttu-id="a1227-151">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-151">✔</span></span> | <span data-ttu-id="a1227-152">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-152">✔</span></span> |
| <span data-ttu-id="a1227-153">Blockquote</span><span class="sxs-lookup"><span data-stu-id="a1227-153">Blockquote</span></span>                | <span data-ttu-id="a1227-154">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-154">✔</span></span> | <span data-ttu-id="a1227-155">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-155">✔</span></span> |
| <span data-ttu-id="a1227-156">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="a1227-156">Hyperlink</span></span>                 | <span data-ttu-id="a1227-157">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-157">✔</span></span> | <span data-ttu-id="a1227-158">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-158">✔</span></span> |
| <span data-ttu-id="a1227-159">画像リンク</span><span class="sxs-lookup"><span data-stu-id="a1227-159">Image link</span></span>                | <span data-ttu-id="a1227-160">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-160">✔</span></span> | <span data-ttu-id="a1227-161">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-161">✖</span></span> |

<span data-ttu-id="a1227-162">クロスプラットフォーム サポートを確認した後、個々のプラットフォームによるサポートも利用できます。</span><span class="sxs-lookup"><span data-stu-id="a1227-162">After checking cross-platform support, ensure that support by individual platforms is also available.</span></span>

## <a name="support-by-individual-platform"></a><span data-ttu-id="a1227-163">個々のプラットフォームによるサポート</span><span class="sxs-lookup"><span data-stu-id="a1227-163">Support by individual platform</span></span>

<span data-ttu-id="a1227-164">テキストの書式設定のサポートは、メッセージとプラットフォームの種類によって異なります。</span><span class="sxs-lookup"><span data-stu-id="a1227-164">Support for text formatting varies by type of message and platform.</span></span>

### <a name="text-only-messages"></a><span data-ttu-id="a1227-165">テキスト専用メッセージ</span><span class="sxs-lookup"><span data-stu-id="a1227-165">Text-only messages</span></span>

<span data-ttu-id="a1227-166">次の表に、デスクトップ、iOS、Android でサポートされているスタイルとスタイルの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="a1227-166">The following table provides a list of styles and which of these styles are supported on desktop, iOS, and Android:</span></span>

| <span data-ttu-id="a1227-167">Style</span><span class="sxs-lookup"><span data-stu-id="a1227-167">Style</span></span>                     | <span data-ttu-id="a1227-168">Desktop</span><span class="sxs-lookup"><span data-stu-id="a1227-168">Desktop</span></span> | <span data-ttu-id="a1227-169">iOS</span><span class="sxs-lookup"><span data-stu-id="a1227-169">iOS</span></span> | <span data-ttu-id="a1227-170">Android</span><span class="sxs-lookup"><span data-stu-id="a1227-170">Android</span></span> |
| ---                       | :---: | :---: | :---: |
| <span data-ttu-id="a1227-171">太字</span><span class="sxs-lookup"><span data-stu-id="a1227-171">Bold</span></span>                      | <span data-ttu-id="a1227-172">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-172">✔</span></span> | <span data-ttu-id="a1227-173">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-173">✔</span></span> | <span data-ttu-id="a1227-174">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-174">✔</span></span> |
| <span data-ttu-id="a1227-175">斜体</span><span class="sxs-lookup"><span data-stu-id="a1227-175">Italic</span></span>                    | <span data-ttu-id="a1227-176">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-176">✔</span></span> | <span data-ttu-id="a1227-177">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-177">✔</span></span> | <span data-ttu-id="a1227-178">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-178">✔</span></span> |
| <span data-ttu-id="a1227-179">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="a1227-179">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a1227-180">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-180">✖</span></span> | <span data-ttu-id="a1227-181">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-181">✖</span></span> | <span data-ttu-id="a1227-182">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-182">✖</span></span> |
| <span data-ttu-id="a1227-183">取り消し線</span><span class="sxs-lookup"><span data-stu-id="a1227-183">Strikethrough</span></span>             | <span data-ttu-id="a1227-184">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-184">✔</span></span> | <span data-ttu-id="a1227-185">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-185">✔</span></span> | <span data-ttu-id="a1227-186">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-186">✖</span></span> |
| <span data-ttu-id="a1227-187">水平ルーラー</span><span class="sxs-lookup"><span data-stu-id="a1227-187">Horizontal rule</span></span>           | <span data-ttu-id="a1227-188">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-188">✖</span></span> | <span data-ttu-id="a1227-189">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-189">✖</span></span> | <span data-ttu-id="a1227-190">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-190">✖</span></span> |
| <span data-ttu-id="a1227-191">記号付きリスト</span><span class="sxs-lookup"><span data-stu-id="a1227-191">Unordered list</span></span>            | <span data-ttu-id="a1227-192">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-192">✔</span></span> | <span data-ttu-id="a1227-193">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-193">✖</span></span> | <span data-ttu-id="a1227-194">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-194">✖</span></span> |
| <span data-ttu-id="a1227-195">番号付きリスト</span><span class="sxs-lookup"><span data-stu-id="a1227-195">Ordered list</span></span>              | <span data-ttu-id="a1227-196">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-196">✔</span></span> | <span data-ttu-id="a1227-197">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-197">✖</span></span> | <span data-ttu-id="a1227-198">✖</span><span class="sxs-lookup"><span data-stu-id="a1227-198">✖</span></span> |
| <span data-ttu-id="a1227-199">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="a1227-199">Preformatted text</span></span>         | <span data-ttu-id="a1227-200">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-200">✔</span></span> | <span data-ttu-id="a1227-201">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-201">✔</span></span> | <span data-ttu-id="a1227-202">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-202">✔</span></span> |
| <span data-ttu-id="a1227-203">Blockquote</span><span class="sxs-lookup"><span data-stu-id="a1227-203">Blockquote</span></span>                | <span data-ttu-id="a1227-204">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-204">✔</span></span> | <span data-ttu-id="a1227-205">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-205">✔</span></span> | <span data-ttu-id="a1227-206">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-206">✔</span></span> |
| <span data-ttu-id="a1227-207">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="a1227-207">Hyperlink</span></span>                 | <span data-ttu-id="a1227-208">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-208">✔</span></span> | <span data-ttu-id="a1227-209">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-209">✔</span></span> | <span data-ttu-id="a1227-210">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-210">✔</span></span> |
| <span data-ttu-id="a1227-211">画像リンク</span><span class="sxs-lookup"><span data-stu-id="a1227-211">Image link</span></span>                | <span data-ttu-id="a1227-212">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-212">✔</span></span> | <span data-ttu-id="a1227-213">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-213">✔</span></span> | <span data-ttu-id="a1227-214">✔</span><span class="sxs-lookup"><span data-stu-id="a1227-214">✔</span></span> |

### <a name="cards"></a><span data-ttu-id="a1227-215">カード</span><span class="sxs-lookup"><span data-stu-id="a1227-215">Cards</span></span>

<span data-ttu-id="a1227-216">カードのサポートについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="a1227-216">For card support, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="a1227-217">次の手順</span><span class="sxs-lookup"><span data-stu-id="a1227-217">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1227-218">ボット メッセージの更新および削除</span><span class="sxs-lookup"><span data-stu-id="a1227-218">Update and delete bot messages</span></span>](~/bots/how-to/update-and-delete-bot-messages.md)
