---
title: カードでのテキストの書式設定
description: Microsoft Teams でのカードテキストの書式設定について説明します。
keywords: teams の bot カード形式
ms.date: 03/29/2018
ms.openlocfilehash: 9ced8a8956265322e91b9d40dc7dc7064ee4659f
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550953"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="df097-104">Teams の書式設定カード</span><span class="sxs-lookup"><span data-stu-id="df097-104">Format cards in Teams</span></span>

<span data-ttu-id="df097-105">カードの種類に応じて、Markdown または HTML のどちらかを使用して、リッチテキスト形式をカードに追加できます。</span><span class="sxs-lookup"><span data-stu-id="df097-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="df097-106">カードは、title または副題のプロパティではなく、text プロパティのみの書式設定をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="df097-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="df097-107">書式は、カードの種類に応じて、XML (HTML) 形式のサブセットまたは Markdown を使用して指定できます。</span><span class="sxs-lookup"><span data-stu-id="df097-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="df097-108">Markdown の書式設定を使用して、現在および今後の開発用のアダプティブカード用にお勧めします。</span><span class="sxs-lookup"><span data-stu-id="df097-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="df097-109">カードの種類に応じて書式設定のサポートが異なります。また、カードのレンダリングはデスクトップとモバイルチームの両方のクライアントとデスクトップブラウザーの Teams で少しずつ異なります。</span><span class="sxs-lookup"><span data-stu-id="df097-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="df097-110">任意の Teams カードを含むインライン画像を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="df097-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="df097-111">画像は、 `.png` `.jpg`、または`.gif`のファイルとして書式設定され、1024× 1024 px または 1 MB を超えることはできません。</span><span class="sxs-lookup"><span data-stu-id="df097-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="df097-112">アニメーション GIF は正式にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="df097-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="df097-113">*See* [カードリファレンス](./cards-reference.md#inline-card-images)を参照</span><span class="sxs-lookup"><span data-stu-id="df097-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="df097-114">Markdown を使用したカードの書式設定</span><span class="sxs-lookup"><span data-stu-id="df097-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="df097-115">Teams で Markdown をサポートするカードには、次の2つの種類があります。</span><span class="sxs-lookup"><span data-stu-id="df097-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="df097-116">**アダプティブカード**: Markdown は、 `Textblock` `Fact.Title`および`Fact.Value`と同様に、アダプティブカードフィールドでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="df097-116">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="df097-117">HTML は、アダプティブカードではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="df097-117">HTML is not supported in adaptive cards.</span></span>
> * <span data-ttu-id="df097-118">**O365 コネクタカード**: Markdown および制限付き HTML は、テキストフィールドの Office 365 コネクタカードでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="df097-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="df097-119">**Markdown の書式設定: アダプティブカード**</span><span class="sxs-lookup"><span data-stu-id="df097-119">**Markdown formatting: Adaptive Cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="df097-120">と`Textblock` `Fact.Value`で`Fact.Title`サポートされているスタイルは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="df097-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="df097-121">Style</span><span class="sxs-lookup"><span data-stu-id="df097-121">Style</span></span> | <span data-ttu-id="df097-122">例</span><span class="sxs-lookup"><span data-stu-id="df097-122">Example</span></span> | <span data-ttu-id="df097-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="df097-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df097-124">bold</span><span class="sxs-lookup"><span data-stu-id="df097-124">bold</span></span> | <span data-ttu-id="df097-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="df097-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="df097-126">italic</span><span class="sxs-lookup"><span data-stu-id="df097-126">italic</span></span> | <span data-ttu-id="df097-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="df097-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="df097-128">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="df097-128">unordered list</span></span> | <ul><li><span data-ttu-id="df097-129">text</span><span class="sxs-lookup"><span data-stu-id="df097-129">text</span></span></li><li><span data-ttu-id="df097-130">text</span><span class="sxs-lookup"><span data-stu-id="df097-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="df097-131">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="df097-131">ordered list</span></span> | <ol><li><span data-ttu-id="df097-132">text</span><span class="sxs-lookup"><span data-stu-id="df097-132">text</span></span></li><li><span data-ttu-id="df097-133">text</span><span class="sxs-lookup"><span data-stu-id="df097-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="df097-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="df097-134">Hyperlinks</span></span> |[<span data-ttu-id="df097-135">Bing</span><span class="sxs-lookup"><span data-stu-id="df097-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="df097-136">次の Markdown タグはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="df097-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="df097-137">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="df097-137">Headers</span></span>
* <span data-ttu-id="df097-138">テーブル</span><span class="sxs-lookup"><span data-stu-id="df097-138">Tables</span></span>
* <span data-ttu-id="df097-139">画像</span><span class="sxs-lookup"><span data-stu-id="df097-139">Images</span></span>
* <span data-ttu-id="df097-140">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="df097-140">Preformatted text</span></span>
* <span data-ttu-id="df097-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="df097-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df097-142">アダプティブカードでは、HTML 形式はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="df097-142">Adaptive cards do not support any HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="df097-143">アダプティブカードの改行</span><span class="sxs-lookup"><span data-stu-id="df097-143">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="df097-144">リストでは、 `\r`または`\n`エスケープシーケンスを使用して改行することができます。</span><span class="sxs-lookup"><span data-stu-id="df097-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="df097-145">リスト`\n\n`でを使用すると、リスト内の次の要素がインデントされます。</span><span class="sxs-lookup"><span data-stu-id="df097-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="df097-146">Textblock の他の場所に改行が必要な`\n\n`場合は、を使用します。</span><span class="sxs-lookup"><span data-stu-id="df097-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="df097-147">アダプティブカードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="df097-147">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="df097-148">デスクトップとモバイルバージョンの Teams では、書式設定が若干異なります。</span><span class="sxs-lookup"><span data-stu-id="df097-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="df097-149">デスクトップでは、アダプティブカードの Markdown 書式は、web ブラウザーと Teams クライアントアプリケーションの両方で次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="df097-149">On the desktop, Adaptive Card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![デスクトップクライアントでのアダプティブカード Markdown の書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="df097-151">IOS では、アダプティブカード Markdown 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="df097-151">On iOS, Adaptive Card Markdown formatting appears like this:</span></span>

![IOS のアダプティブカード Markdown 形式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="df097-153">Android では、アダプティブカードの Markdown 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="df097-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Android のアダプティブカード Markdown 形式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="df097-155">アダプティブカードの詳細情報</span><span class="sxs-lookup"><span data-stu-id="df097-155">More information on Adaptive Cards</span></span>

<span data-ttu-id="df097-156">[アダプティブカードのテキスト機能](/adaptive-cards/create/textfeatures)このトピックで説明する日付とローカリゼーションの機能は、Teams ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="df097-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="df097-157">アダプティブカード用の書式設定のサンプル</span><span class="sxs-lookup"><span data-stu-id="df097-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "This is some **bold** text"
        },
        {
            "type": "TextBlock",
            "text": "This is some _italic_ text"
        },
        {
            "type": "TextBlock",
            "text": "- Bullet \r- List \r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "1. Numbered\r2. List\r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Check out [Adaptive Cards](http://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards"></a><span data-ttu-id="df097-158">アダプティブカード内でのサポートを伝えます。</span><span class="sxs-lookup"><span data-stu-id="df097-158">Mention support within Adaptive cards</span></span>

> [!NOTE]
> <span data-ttu-id="df097-159">現在、カードでのサポートは、[開発者向けプレビュー](../../resources/dev-preview/developer-preview-intro.md)のみでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="df097-159">Mention support in cards is currently supported in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="df097-160">ボットおよびメッセージング拡張機能は、テキストブロックと FactSet 要素のカードコンテンツ内にメンションを含めることができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="df097-160">Bots and Messaging extensions can now include mentions within the card content in Text Block and FactSet elements.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="df097-161">メンションの構築</span><span class="sxs-lookup"><span data-stu-id="df097-161">Constructing mentions</span></span>

<span data-ttu-id="df097-162">アダプティブカードにメンションを含めるには、アプリに次の要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="df097-162">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="df097-163">`<at>username</at>`サポートされているアダプティブカード要素</span><span class="sxs-lookup"><span data-stu-id="df097-163">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="df097-164">カード`mention`コンテンツ内の`msteams`プロパティの内部にあるオブジェクト。このオブジェクトは、説明されているユーザーの Teams ユーザー id を含みます。</span><span class="sxs-lookup"><span data-stu-id="df097-164">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

<span data-ttu-id="df097-165">この時点では、メンション付きのカードはモバイルクライアントではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="df097-165">Note that cards with mentions aren't supported on mobile clients at the moment.</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="df097-166">アダプティブカードのサンプル</span><span class="sxs-lookup"><span data-stu-id="df097-166">Sample Adaptive card with a mention</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "type": "AdaptiveCard",
    "body": [
      {
        "type": "TextBlock",
        "text": "Hi <at>John Doe</at>"
      }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.0",
    "msteams": {
      "entities": [
        {
          "type": "mention",
          "text": "<at>John Doe</at>",
          "mentioned": {
            "id": "29:123124124124",
            "name": "John Doe"
          }
        }
      ]
    }
  }
}
```

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="df097-167">**Markdown の形式: O365 コネクタカード**</span><span class="sxs-lookup"><span data-stu-id="df097-167">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="df097-168">コネクタカードは、制限付きの Markdown および HTML 形式をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="df097-168">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="df097-169">HTML サポートについては、前のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="df097-169">HTML support is described in the last section.</span></span>

| <span data-ttu-id="df097-170">Style</span><span class="sxs-lookup"><span data-stu-id="df097-170">Style</span></span> | <span data-ttu-id="df097-171">例</span><span class="sxs-lookup"><span data-stu-id="df097-171">Example</span></span> | <span data-ttu-id="df097-172">Markdown</span><span class="sxs-lookup"><span data-stu-id="df097-172">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df097-173">bold</span><span class="sxs-lookup"><span data-stu-id="df097-173">bold</span></span> | <span data-ttu-id="df097-174">**text**</span><span class="sxs-lookup"><span data-stu-id="df097-174">**text**</span></span> | `**text**` |
| <span data-ttu-id="df097-175">italic</span><span class="sxs-lookup"><span data-stu-id="df097-175">italic</span></span> | <span data-ttu-id="df097-176">*text*</span><span class="sxs-lookup"><span data-stu-id="df097-176">*text*</span></span> | `*text*` |
| <span data-ttu-id="df097-177">ヘッダー (レベル 1&ndash;3)</span><span class="sxs-lookup"><span data-stu-id="df097-177">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="df097-178">**テキスト**</span><span class="sxs-lookup"><span data-stu-id="df097-178">**Text**</span></span> | `### Text`|
| <span data-ttu-id="df097-179">打ち消し</span><span class="sxs-lookup"><span data-stu-id="df097-179">strikethrough</span></span> | <span data-ttu-id="df097-180">~~text~~</span><span class="sxs-lookup"><span data-stu-id="df097-180">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="df097-181">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="df097-181">unordered list</span></span> | <ul><li><span data-ttu-id="df097-182">text</span><span class="sxs-lookup"><span data-stu-id="df097-182">text</span></span></li><li><span data-ttu-id="df097-183">text</span><span class="sxs-lookup"><span data-stu-id="df097-183">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="df097-184">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="df097-184">ordered list</span></span> | <ol><li><span data-ttu-id="df097-185">text</span><span class="sxs-lookup"><span data-stu-id="df097-185">text</span></span></li><li><span data-ttu-id="df097-186">text</span><span class="sxs-lookup"><span data-stu-id="df097-186">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="df097-187">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="df097-187">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="df097-188">blockquote</span><span class="sxs-lookup"><span data-stu-id="df097-188">blockquote</span></span> | <span data-ttu-id="df097-189">>blockquote テキスト</span><span class="sxs-lookup"><span data-stu-id="df097-189">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="df097-190">hyperlink</span><span class="sxs-lookup"><span data-stu-id="df097-190">hyperlink</span></span> | [<span data-ttu-id="df097-191">Bing</span><span class="sxs-lookup"><span data-stu-id="df097-191">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="df097-192">画像リンク</span><span class="sxs-lookup"><span data-stu-id="df097-192">image link</span></span> |![岩に関するアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="df097-194">コネクタカードで`\n\n` `\n`は、改行はに対してレンダリングされ`\r`ますが、では表示されません。</span><span class="sxs-lookup"><span data-stu-id="df097-194">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="df097-195">Markdown を使用したコネクタカードのモバイルとデスクトップの相違点</span><span class="sxs-lookup"><span data-stu-id="df097-195">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="df097-196">デスクトップでは、Markdown のコネクタカードの書式は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="df097-196">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![デスクトップクライアントでのコネクタカードの Markdown の書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="df097-198">IOS では、Markdown のコネクタカードの書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="df097-198">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![IOS クライアントでのコネクタカードの Markdown の書式設定](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="df097-200">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="df097-200">Issues:</span></span>

* <span data-ttu-id="df097-201">Teams の iOS クライアントは、コネクタカードで Markdown または HTML インライン画像を表示しません。</span><span class="sxs-lookup"><span data-stu-id="df097-201">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="df097-202">Blockquotes はインデント付きですが、灰色は表示されません。</span><span class="sxs-lookup"><span data-stu-id="df097-202">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="df097-203">Android では、Markdown のコネクタカードの書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="df097-203">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android クライアントでのコネクタカードの Markdown の書式設定](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="df097-205">Markdown コネクタカードの書式設定の例</span><span class="sxs-lookup"><span data-stu-id="df097-205">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card Markdown formatting",
    "sections": [
        {
            "text": "This is some **bold** text"
        },
        {
            "text": "This is some _italic_ text"
        },
        {
            "text": "# Header 1\r## Header 2\r### Header 3"
        },
        {
            "text": "- Bullet \r- List \r"
        },
        {
            "text": "1. Numbered\r1. List \r"
        },
        {
            "text": "Link: [Bing](https://www.bing.com)"
        },
        {
            "text": "embedded image link: ![Duck on a rock](http://aka.ms/Fo983c)"
        },
        {
            "text": "`preformatted text`"
        },
        {
            "text": "Newlines (backslash n, backslash n):\n\nline a\n\nline b\n\nline c"
        },
        {
            "text": ">This is a blockquote"
        }
     ]
  }
}

```

---

## <a name="formatting-cards-with-html"></a><span data-ttu-id="df097-206">HTML を使用してカードを書式設定する</span><span class="sxs-lookup"><span data-stu-id="df097-206">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="df097-207">**HTML 形式: O365 コネクタカード**</span><span class="sxs-lookup"><span data-stu-id="df097-207">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="df097-208">コネクタカードは、制限付きの Markdown および HTML 形式をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="df097-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="df097-209">Markdown については、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="df097-209">Markdown is described in the next section.</span></span>

| <span data-ttu-id="df097-210">Style</span><span class="sxs-lookup"><span data-stu-id="df097-210">Style</span></span> | <span data-ttu-id="df097-211">例</span><span class="sxs-lookup"><span data-stu-id="df097-211">Example</span></span> | <span data-ttu-id="df097-212">HTML</span><span class="sxs-lookup"><span data-stu-id="df097-212">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df097-213">bold</span><span class="sxs-lookup"><span data-stu-id="df097-213">bold</span></span> | <span data-ttu-id="df097-214">**text**</span><span class="sxs-lookup"><span data-stu-id="df097-214">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="df097-215">italic</span><span class="sxs-lookup"><span data-stu-id="df097-215">italic</span></span> | <span data-ttu-id="df097-216">*text*</span><span class="sxs-lookup"><span data-stu-id="df097-216">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="df097-217">ヘッダー (レベル 1&ndash;3)</span><span class="sxs-lookup"><span data-stu-id="df097-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="df097-218">**テキスト**</span><span class="sxs-lookup"><span data-stu-id="df097-218">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="df097-219">打ち消し</span><span class="sxs-lookup"><span data-stu-id="df097-219">strikethrough</span></span> | <span data-ttu-id="df097-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="df097-220">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="df097-221">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="df097-221">unordered list</span></span> | <ul><li><span data-ttu-id="df097-222">text</span><span class="sxs-lookup"><span data-stu-id="df097-222">text</span></span></li><li><span data-ttu-id="df097-223">text</span><span class="sxs-lookup"><span data-stu-id="df097-223">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="df097-224">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="df097-224">ordered list</span></span> | <ol><li><span data-ttu-id="df097-225">text</span><span class="sxs-lookup"><span data-stu-id="df097-225">text</span></span></li><li><span data-ttu-id="df097-226">text</span><span class="sxs-lookup"><span data-stu-id="df097-226">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="df097-227">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="df097-227">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="df097-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="df097-228">blockquote</span></span> | <blockquote><span data-ttu-id="df097-229">text</span><span class="sxs-lookup"><span data-stu-id="df097-229">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="df097-230">hyperlink</span><span class="sxs-lookup"><span data-stu-id="df097-230">hyperlink</span></span> | [<span data-ttu-id="df097-231">Bing</span><span class="sxs-lookup"><span data-stu-id="df097-231">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="df097-232">画像リンク</span><span class="sxs-lookup"><span data-stu-id="df097-232">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="df097-233">コネクタカードでは、改行は`<p>`タグを使用して HTML でレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="df097-233">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="df097-234">HTML を使用するコネクタカードのモバイルとデスクトップの相違点</span><span class="sxs-lookup"><span data-stu-id="df097-234">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="df097-235">デスクトップでは、コネクタカードの HTML 書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="df097-235">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![デスクトップクライアントのコネクタカードの HTML 形式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="df097-237">IOS では、HTML 形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="df097-237">On iOS, HTML formatting looks like this:</span></span>

![IOS クライアントでのコネクタカードの HTML 書式設定](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="df097-239">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="df097-239">Issues:</span></span>

* <span data-ttu-id="df097-240">インライン画像は、コネクタカードで Markdown または HTML のどちらかを使用して iOS でレンダリングされることはありません。</span><span class="sxs-lookup"><span data-stu-id="df097-240">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="df097-241">書式設定済みのテキストは表示されますが、灰色の背景は表示されません。</span><span class="sxs-lookup"><span data-stu-id="df097-241">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="df097-242">Android では、HTML 形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="df097-242">On Android, HTML formatting looks like this:</span></span>

![Android クライアントでのコネクタカードの HTML 書式設定](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="df097-244">HTML コネクタカードの書式設定のサンプル</span><span class="sxs-lookup"><span data-stu-id="df097-244">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card HTML formatting",
    "sections": [
        {
            "text": "This is some <strong>bold</strong> text"
        },
        {
            "text": "This is some <em>italic</em> text"
        },
        {
            "text": "This is some <strike>strikethrough</strike> text"
        },
        {
            "text": "<h1>Header 1</h1>\r<h2>Header 2</h2>\r <h3>Header 3</h3>"
        },
        {
            "text": "bullet list <ul><li>text</li><li>text</li></ul>"
        },
        {
            "text": "ordered list <ol><li>text</li><li>text</li></ol>"
        },
        {
            "text": "hyperlink <a href=\"https://www.bing.com/\">Bing</a>"
        },
        {
            "text": "embedded image <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
        },
        {
            "text": "preformatted text <pre>text</pre>"
        },
        {
            "text": "Paragraphs <p>Line a</p><p>Line b</p>"
        },
        {
            "text": "<blockquote>Blockquote text</blockquote>"
        }
     ]
  }
}

```

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="df097-245">**HTML 形式: 英雄とサムネイルカード**</span><span class="sxs-lookup"><span data-stu-id="df097-245">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="df097-246">HTML タグは、ヒーローやサムネイルカードなどの単純なカードでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="df097-246">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="df097-247">Markdown はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="df097-247">Markdown is not supported.</span></span>

| <span data-ttu-id="df097-248">Style</span><span class="sxs-lookup"><span data-stu-id="df097-248">Style</span></span> | <span data-ttu-id="df097-249">例</span><span class="sxs-lookup"><span data-stu-id="df097-249">Example</span></span> | <span data-ttu-id="df097-250">HTML</span><span class="sxs-lookup"><span data-stu-id="df097-250">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df097-251">bold</span><span class="sxs-lookup"><span data-stu-id="df097-251">bold</span></span> | <span data-ttu-id="df097-252">**text**</span><span class="sxs-lookup"><span data-stu-id="df097-252">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="df097-253">italic</span><span class="sxs-lookup"><span data-stu-id="df097-253">italic</span></span> | <span data-ttu-id="df097-254">*text*</span><span class="sxs-lookup"><span data-stu-id="df097-254">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="df097-255">ヘッダー (レベル 1&ndash;3)</span><span class="sxs-lookup"><span data-stu-id="df097-255">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="df097-256">**テキスト**</span><span class="sxs-lookup"><span data-stu-id="df097-256">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="df097-257">打ち消し</span><span class="sxs-lookup"><span data-stu-id="df097-257">strikethrough</span></span> | <span data-ttu-id="df097-258">~~text~~</span><span class="sxs-lookup"><span data-stu-id="df097-258">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="df097-259">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="df097-259">unordered list</span></span> | <ul><li><span data-ttu-id="df097-260">text</span><span class="sxs-lookup"><span data-stu-id="df097-260">text</span></span></li><li><span data-ttu-id="df097-261">text</span><span class="sxs-lookup"><span data-stu-id="df097-261">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="df097-262">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="df097-262">ordered list</span></span> | <ol><li><span data-ttu-id="df097-263">text</span><span class="sxs-lookup"><span data-stu-id="df097-263">text</span></span></li><li><span data-ttu-id="df097-264">text</span><span class="sxs-lookup"><span data-stu-id="df097-264">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="df097-265">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="df097-265">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="df097-266">blockquote</span><span class="sxs-lookup"><span data-stu-id="df097-266">blockquote</span></span> | <blockquote><span data-ttu-id="df097-267">text</span><span class="sxs-lookup"><span data-stu-id="df097-267">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="df097-268">hyperlink</span><span class="sxs-lookup"><span data-stu-id="df097-268">hyperlink</span></span> | [<span data-ttu-id="df097-269">Bing</span><span class="sxs-lookup"><span data-stu-id="df097-269">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="df097-270">画像リンク</span><span class="sxs-lookup"><span data-stu-id="df097-270">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="df097-271">簡単なカードのモバイルとデスクトップの相違点</span><span class="sxs-lookup"><span data-stu-id="df097-271">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="df097-272">デスクトップとモバイルプラットフォームとの間には、解像度の違いがあるため、デスクトップとモバイルバージョンの Teams との間で書式設定が異なります。</span><span class="sxs-lookup"><span data-stu-id="df097-272">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="df097-273">デスクトップでは、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="df097-273">On the desktop, HTML formatting appears like this:</span></span>

![デスクトップクライアントの HTML 形式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="df097-275">IOS では、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="df097-275">On iOS, HTML formatting appears like this:</span></span>

![IOS クライアントでの HTML 形式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="df097-277">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="df097-277">Issues:</span></span>

* <span data-ttu-id="df097-278">太字や斜体などの文字書式は、iOS では表示されません。</span><span class="sxs-lookup"><span data-stu-id="df097-278">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="df097-279">Android では、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="df097-279">On Android, HTML formatting appears like this:</span></span>

![Android クライアントでの HTML 形式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="df097-281">Android では、太字や斜体などの文字書式が正しく表示されます。</span><span class="sxs-lookup"><span data-stu-id="df097-281">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="df097-282">シンプルなカードにおける HTML 形式の書式設定のサンプル</span><span class="sxs-lookup"><span data-stu-id="df097-282">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="df097-283">これらのスクリーンショットは Teams AppStudio を使用して作成されています。これは、ヒーローカードの text プロパティが次の文字列に設定されています。</span><span class="sxs-lookup"><span data-stu-id="df097-283">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="df097-284">このコードを変更することにより、独自のカードで書式設定をテストできます。</span><span class="sxs-lookup"><span data-stu-id="df097-284">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
