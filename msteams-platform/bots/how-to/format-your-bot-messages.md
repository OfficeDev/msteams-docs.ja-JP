---
title: ボット メッセージの書式を設定する
author: surbhigupta
description: ボット メッセージにリッチ書式を追加する
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 56a34edee372cc6c5bcc5808015783f04867f141
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068983"
---
# <a name="format-your-bot-messages"></a><span data-ttu-id="20907-103">ボット メッセージの書式を設定する</span><span class="sxs-lookup"><span data-stu-id="20907-103">Format your bot messages</span></span>

<span data-ttu-id="20907-104">メッセージの書式設定を使用すると、ボット メッセージを最適に表示できます。</span><span class="sxs-lookup"><span data-stu-id="20907-104">Message formatting enables you to bring out the best in bot messages.</span></span> <span data-ttu-id="20907-105">ボタン、テキスト、画像、オーディオ、ビデオなどの対話型要素を含む添付ファイルであるリッチ カードをボット メッセージに書式設定できます。</span><span class="sxs-lookup"><span data-stu-id="20907-105">You can format your bot messages to include rich cards that are attachments that contain interactive elements, such as buttons, text, images, audio, video, and so on.</span></span>

## <a name="format-text-content"></a><span data-ttu-id="20907-106">テキスト コンテンツの書式設定</span><span class="sxs-lookup"><span data-stu-id="20907-106">Format text content</span></span>

<span data-ttu-id="20907-107">ボット メッセージを書式設定するには、省略可能なプロパティを設定して、ボット メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) を制御できます。</span><span class="sxs-lookup"><span data-stu-id="20907-107">To format your bot messages, you can set the optional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) property to control how your bot message's text content is rendered.</span></span>

<span data-ttu-id="20907-108">Microsoft Teamsは、次の書式設定オプションをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="20907-108">Microsoft Teams supports the following formatting options:</span></span>

| <span data-ttu-id="20907-109">`TextFormat` value</span><span class="sxs-lookup"><span data-stu-id="20907-109">`TextFormat` value</span></span> | <span data-ttu-id="20907-110">説明</span><span class="sxs-lookup"><span data-stu-id="20907-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="20907-111">プレーン</span><span class="sxs-lookup"><span data-stu-id="20907-111">plain</span></span> | <span data-ttu-id="20907-112">テキストは、書式が適用されずに生テキストとして扱われる必要があります。</span><span class="sxs-lookup"><span data-stu-id="20907-112">The text must be treated as raw text with no formatting applied.</span></span>|
| <span data-ttu-id="20907-113">markdown</span><span class="sxs-lookup"><span data-stu-id="20907-113">markdown</span></span> | <span data-ttu-id="20907-114">テキストはマークダウンの書式設定として扱い、必要に応じてチャネルにレンダリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="20907-114">The text must be treated as markdown formatting and rendered on the channel as appropriate.</span></span> |
| <span data-ttu-id="20907-115">xml</span><span class="sxs-lookup"><span data-stu-id="20907-115">xml</span></span> | <span data-ttu-id="20907-116">テキストは単純な XML マークアップです。</span><span class="sxs-lookup"><span data-stu-id="20907-116">The text is simple XML markup.</span></span> |

<span data-ttu-id="20907-117">Teamsマークダウンタグと XML 書式タグまたは HTML 書式タグのサブセットをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="20907-117">Teams supports a subset of markdown and XML or HTML formatting tags.</span></span>

<span data-ttu-id="20907-118">現在、書式設定には次の制限が適用されます。</span><span class="sxs-lookup"><span data-stu-id="20907-118">Currently, the following limitations apply to formatting:</span></span>

* <span data-ttu-id="20907-119">テキスト専用メッセージは、テーブルの書式設定をサポートしません。</span><span class="sxs-lookup"><span data-stu-id="20907-119">Text-only messages do not support table formatting.</span></span>
* <span data-ttu-id="20907-120">リッチ カードは、タイトルプロパティや字幕プロパティではなく、text プロパティの書式設定のみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="20907-120">Rich cards support formatting in the text property only, not in the title or subtitle properties.</span></span>
* <span data-ttu-id="20907-121">リッチ カードでは、マークダウンやテーブルの書式設定はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="20907-121">Rich cards do not support markdown or table formatting.</span></span>

<span data-ttu-id="20907-122">テキスト コンテンツの書式を設定した後、ユーザーがサポートしているすべてのプラットフォームで書式設定が機能Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="20907-122">After you format text content, ensure that your formatting works across all platforms supported by Microsoft Teams.</span></span>

## <a name="cross-platform-support"></a><span data-ttu-id="20907-123">クロスプラットフォームのサポート</span><span class="sxs-lookup"><span data-stu-id="20907-123">Cross-platform support</span></span>

<span data-ttu-id="20907-124">一部のスタイルは現在、すべてのプラットフォームでサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="20907-124">Some styles are currently not supported across all platforms.</span></span> <span data-ttu-id="20907-125">次の表に、テキスト専用メッセージとリッチ カードでサポートされているスタイルとスタイルの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="20907-125">The following table provides a list of styles and which of these styles are supported in text-only messages and rich cards:</span></span>

| <span data-ttu-id="20907-126">Style</span><span class="sxs-lookup"><span data-stu-id="20907-126">Style</span></span>                     | <span data-ttu-id="20907-127">テキスト専用メッセージ</span><span class="sxs-lookup"><span data-stu-id="20907-127">Text-only messages</span></span> | <span data-ttu-id="20907-128">リッチ カード - XML のみ</span><span class="sxs-lookup"><span data-stu-id="20907-128">Rich cards - XML only</span></span> |
| ---                       | :---: | :---: |
| <span data-ttu-id="20907-129">太字</span><span class="sxs-lookup"><span data-stu-id="20907-129">Bold</span></span>                      | <span data-ttu-id="20907-130">✔</span><span class="sxs-lookup"><span data-stu-id="20907-130">✔</span></span> | <span data-ttu-id="20907-131">✖</span><span class="sxs-lookup"><span data-stu-id="20907-131">✖</span></span> |
| <span data-ttu-id="20907-132">斜体</span><span class="sxs-lookup"><span data-stu-id="20907-132">Italic</span></span>                    | <span data-ttu-id="20907-133">✔</span><span class="sxs-lookup"><span data-stu-id="20907-133">✔</span></span> | <span data-ttu-id="20907-134">✔</span><span class="sxs-lookup"><span data-stu-id="20907-134">✔</span></span> |
| <span data-ttu-id="20907-135">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="20907-135">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="20907-136">✖</span><span class="sxs-lookup"><span data-stu-id="20907-136">✖</span></span> | <span data-ttu-id="20907-137">✔</span><span class="sxs-lookup"><span data-stu-id="20907-137">✔</span></span> |
| <span data-ttu-id="20907-138">取り消し線</span><span class="sxs-lookup"><span data-stu-id="20907-138">Strikethrough</span></span>             | <span data-ttu-id="20907-139">✖</span><span class="sxs-lookup"><span data-stu-id="20907-139">✖</span></span> | <span data-ttu-id="20907-140">✔</span><span class="sxs-lookup"><span data-stu-id="20907-140">✔</span></span> |
| <span data-ttu-id="20907-141">水平ルーラー</span><span class="sxs-lookup"><span data-stu-id="20907-141">Horizontal rule</span></span>           | <span data-ttu-id="20907-142">✖</span><span class="sxs-lookup"><span data-stu-id="20907-142">✖</span></span> | <span data-ttu-id="20907-143">✖</span><span class="sxs-lookup"><span data-stu-id="20907-143">✖</span></span> |
| <span data-ttu-id="20907-144">記号付きリスト</span><span class="sxs-lookup"><span data-stu-id="20907-144">Unordered list</span></span>            | <span data-ttu-id="20907-145">✖</span><span class="sxs-lookup"><span data-stu-id="20907-145">✖</span></span> | <span data-ttu-id="20907-146">✔</span><span class="sxs-lookup"><span data-stu-id="20907-146">✔</span></span> |
| <span data-ttu-id="20907-147">番号付きリスト</span><span class="sxs-lookup"><span data-stu-id="20907-147">Ordered list</span></span>              | <span data-ttu-id="20907-148">✖</span><span class="sxs-lookup"><span data-stu-id="20907-148">✖</span></span> | <span data-ttu-id="20907-149">✔</span><span class="sxs-lookup"><span data-stu-id="20907-149">✔</span></span> |
| <span data-ttu-id="20907-150">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="20907-150">Preformatted text</span></span>         | <span data-ttu-id="20907-151">✔</span><span class="sxs-lookup"><span data-stu-id="20907-151">✔</span></span> | <span data-ttu-id="20907-152">✔</span><span class="sxs-lookup"><span data-stu-id="20907-152">✔</span></span> |
| <span data-ttu-id="20907-153">Blockquote</span><span class="sxs-lookup"><span data-stu-id="20907-153">Blockquote</span></span>                | <span data-ttu-id="20907-154">✔</span><span class="sxs-lookup"><span data-stu-id="20907-154">✔</span></span> | <span data-ttu-id="20907-155">✔</span><span class="sxs-lookup"><span data-stu-id="20907-155">✔</span></span> |
| <span data-ttu-id="20907-156">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="20907-156">Hyperlink</span></span>                 | <span data-ttu-id="20907-157">✔</span><span class="sxs-lookup"><span data-stu-id="20907-157">✔</span></span> | <span data-ttu-id="20907-158">✔</span><span class="sxs-lookup"><span data-stu-id="20907-158">✔</span></span> |
| <span data-ttu-id="20907-159">画像リンク</span><span class="sxs-lookup"><span data-stu-id="20907-159">Image link</span></span>                | <span data-ttu-id="20907-160">✔</span><span class="sxs-lookup"><span data-stu-id="20907-160">✔</span></span> | <span data-ttu-id="20907-161">✖</span><span class="sxs-lookup"><span data-stu-id="20907-161">✖</span></span> |

<span data-ttu-id="20907-162">クロスプラットフォーム サポートを確認した後、個々のプラットフォームによるサポートも利用できます。</span><span class="sxs-lookup"><span data-stu-id="20907-162">After checking cross-platform support, ensure that support by individual platforms is also available.</span></span>

## <a name="support-by-individual-platform"></a><span data-ttu-id="20907-163">個々のプラットフォームによるサポート</span><span class="sxs-lookup"><span data-stu-id="20907-163">Support by individual platform</span></span>

<span data-ttu-id="20907-164">テキストの書式設定のサポートは、メッセージとプラットフォームの種類によって異なります。</span><span class="sxs-lookup"><span data-stu-id="20907-164">Support for text formatting varies by type of message and platform.</span></span>

### <a name="text-only-messages"></a><span data-ttu-id="20907-165">テキスト専用メッセージ</span><span class="sxs-lookup"><span data-stu-id="20907-165">Text-only messages</span></span>

<span data-ttu-id="20907-166">次の表に、デスクトップ、iOS、Android でサポートされているスタイルとスタイルの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="20907-166">The following table provides a list of styles and which of these styles are supported on desktop, iOS, and Android:</span></span>

| <span data-ttu-id="20907-167">Style</span><span class="sxs-lookup"><span data-stu-id="20907-167">Style</span></span>                     | <span data-ttu-id="20907-168">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="20907-168">Desktop</span></span> | <span data-ttu-id="20907-169">iOS</span><span class="sxs-lookup"><span data-stu-id="20907-169">iOS</span></span> | <span data-ttu-id="20907-170">Android</span><span class="sxs-lookup"><span data-stu-id="20907-170">Android</span></span> |
| ---                       | :---: | :---: | :---: |
| <span data-ttu-id="20907-171">太字</span><span class="sxs-lookup"><span data-stu-id="20907-171">Bold</span></span>                      | <span data-ttu-id="20907-172">✔</span><span class="sxs-lookup"><span data-stu-id="20907-172">✔</span></span> | <span data-ttu-id="20907-173">✔</span><span class="sxs-lookup"><span data-stu-id="20907-173">✔</span></span> | <span data-ttu-id="20907-174">✔</span><span class="sxs-lookup"><span data-stu-id="20907-174">✔</span></span> |
| <span data-ttu-id="20907-175">斜体</span><span class="sxs-lookup"><span data-stu-id="20907-175">Italic</span></span>                    | <span data-ttu-id="20907-176">✔</span><span class="sxs-lookup"><span data-stu-id="20907-176">✔</span></span> | <span data-ttu-id="20907-177">✔</span><span class="sxs-lookup"><span data-stu-id="20907-177">✔</span></span> | <span data-ttu-id="20907-178">✔</span><span class="sxs-lookup"><span data-stu-id="20907-178">✔</span></span> |
| <span data-ttu-id="20907-179">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="20907-179">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="20907-180">✖</span><span class="sxs-lookup"><span data-stu-id="20907-180">✖</span></span> | <span data-ttu-id="20907-181">✖</span><span class="sxs-lookup"><span data-stu-id="20907-181">✖</span></span> | <span data-ttu-id="20907-182">✖</span><span class="sxs-lookup"><span data-stu-id="20907-182">✖</span></span> |
| <span data-ttu-id="20907-183">取り消し線</span><span class="sxs-lookup"><span data-stu-id="20907-183">Strikethrough</span></span>             | <span data-ttu-id="20907-184">✔</span><span class="sxs-lookup"><span data-stu-id="20907-184">✔</span></span> | <span data-ttu-id="20907-185">✔</span><span class="sxs-lookup"><span data-stu-id="20907-185">✔</span></span> | <span data-ttu-id="20907-186">✖</span><span class="sxs-lookup"><span data-stu-id="20907-186">✖</span></span> |
| <span data-ttu-id="20907-187">水平ルーラー</span><span class="sxs-lookup"><span data-stu-id="20907-187">Horizontal rule</span></span>           | <span data-ttu-id="20907-188">✖</span><span class="sxs-lookup"><span data-stu-id="20907-188">✖</span></span> | <span data-ttu-id="20907-189">✖</span><span class="sxs-lookup"><span data-stu-id="20907-189">✖</span></span> | <span data-ttu-id="20907-190">✖</span><span class="sxs-lookup"><span data-stu-id="20907-190">✖</span></span> |
| <span data-ttu-id="20907-191">記号付きリスト</span><span class="sxs-lookup"><span data-stu-id="20907-191">Unordered list</span></span>            | <span data-ttu-id="20907-192">✔</span><span class="sxs-lookup"><span data-stu-id="20907-192">✔</span></span> | <span data-ttu-id="20907-193">✖</span><span class="sxs-lookup"><span data-stu-id="20907-193">✖</span></span> | <span data-ttu-id="20907-194">✖</span><span class="sxs-lookup"><span data-stu-id="20907-194">✖</span></span> |
| <span data-ttu-id="20907-195">番号付きリスト</span><span class="sxs-lookup"><span data-stu-id="20907-195">Ordered list</span></span>              | <span data-ttu-id="20907-196">✔</span><span class="sxs-lookup"><span data-stu-id="20907-196">✔</span></span> | <span data-ttu-id="20907-197">✖</span><span class="sxs-lookup"><span data-stu-id="20907-197">✖</span></span> | <span data-ttu-id="20907-198">✖</span><span class="sxs-lookup"><span data-stu-id="20907-198">✖</span></span> |
| <span data-ttu-id="20907-199">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="20907-199">Preformatted text</span></span>         | <span data-ttu-id="20907-200">✔</span><span class="sxs-lookup"><span data-stu-id="20907-200">✔</span></span> | <span data-ttu-id="20907-201">✔</span><span class="sxs-lookup"><span data-stu-id="20907-201">✔</span></span> | <span data-ttu-id="20907-202">✔</span><span class="sxs-lookup"><span data-stu-id="20907-202">✔</span></span> |
| <span data-ttu-id="20907-203">Blockquote</span><span class="sxs-lookup"><span data-stu-id="20907-203">Blockquote</span></span>                | <span data-ttu-id="20907-204">✔</span><span class="sxs-lookup"><span data-stu-id="20907-204">✔</span></span> | <span data-ttu-id="20907-205">✔</span><span class="sxs-lookup"><span data-stu-id="20907-205">✔</span></span> | <span data-ttu-id="20907-206">✔</span><span class="sxs-lookup"><span data-stu-id="20907-206">✔</span></span> |
| <span data-ttu-id="20907-207">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="20907-207">Hyperlink</span></span>                 | <span data-ttu-id="20907-208">✔</span><span class="sxs-lookup"><span data-stu-id="20907-208">✔</span></span> | <span data-ttu-id="20907-209">✔</span><span class="sxs-lookup"><span data-stu-id="20907-209">✔</span></span> | <span data-ttu-id="20907-210">✔</span><span class="sxs-lookup"><span data-stu-id="20907-210">✔</span></span> |
| <span data-ttu-id="20907-211">画像リンク</span><span class="sxs-lookup"><span data-stu-id="20907-211">Image link</span></span>                | <span data-ttu-id="20907-212">✔</span><span class="sxs-lookup"><span data-stu-id="20907-212">✔</span></span> | <span data-ttu-id="20907-213">✔</span><span class="sxs-lookup"><span data-stu-id="20907-213">✔</span></span> | <span data-ttu-id="20907-214">✔</span><span class="sxs-lookup"><span data-stu-id="20907-214">✔</span></span> |

### <a name="cards"></a><span data-ttu-id="20907-215">カード</span><span class="sxs-lookup"><span data-stu-id="20907-215">Cards</span></span>

<span data-ttu-id="20907-216">カードのサポートについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="20907-216">For card support, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="20907-217">次の手順</span><span class="sxs-lookup"><span data-stu-id="20907-217">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="20907-218">ボット メッセージの更新および削除</span><span class="sxs-lookup"><span data-stu-id="20907-218">Update and delete bot messages</span></span>](~/bots/how-to/update-and-delete-bot-messages.md)
