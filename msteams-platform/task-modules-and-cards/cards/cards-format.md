---
title: カードでのテキストの書式設定
description: Microsoft Teams でのカードテキストの書式設定について説明します。
keywords: teams の bot カード形式
ms.date: 03/29/2018
ms.openlocfilehash: eb8aa13b9e75d08dadd5e615029a9d418c6c7892
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783970"
---
# <a name="card-formatting"></a><span data-ttu-id="d49ae-104">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="d49ae-104">Card formatting</span></span>

<span data-ttu-id="d49ae-105">カードの種類に応じて、markdown または HTML のどちらかを使用して、リッチテキスト形式をカードに追加できます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-105">You can add rich text formatting to your cards using either markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="d49ae-106">カードは、title または副題のプロパティではなく、text プロパティのみの書式設定をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d49ae-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="d49ae-107">書式は、カードの種類に応じて、XML (HTML) 形式のサブセットまたは Markdown を使用して指定できます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="d49ae-108">Markdown の書式設定を使用して、現在の amd の将来の展開用のアダプティブカードをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d49ae-108">For current amd future development Adaptive cards using markdown formatting is recommended.</span></span>

<span data-ttu-id="d49ae-109">カードの種類に応じて書式設定のサポートが異なります。また、カードのレンダリングはデスクトップとモバイルチームの両方のクライアントとデスクトップブラウザーの Teams で少しずつ異なります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

## <a name="card-types"></a><span data-ttu-id="d49ae-110">カードの種類</span><span class="sxs-lookup"><span data-stu-id="d49ae-110">Card types</span></span>

<span data-ttu-id="d49ae-111">Teams で Markdown をサポートするカードには、次の3種類があります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-111">There are three types of cards that support Markdown in Teams:</span></span>

* <span data-ttu-id="d49ae-112">**アダプティブカード**: Markdown は、 `Textblock` `Fact.Title`および`Fact.Value`と同様に、アダプティブカードフィールドでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d49ae-112">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="d49ae-113">HTML は、アダプティブカードではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-113">HTML is not supported in adaptive cards.</span></span>
* <span data-ttu-id="d49ae-114">**O365 コネクタカード**: Markdown および制限付き HTML は、テキストフィールドの Office 365 コネクタカードでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d49ae-114">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>
* <span data-ttu-id="d49ae-115">**シンプルなカード**: 制限付き HTML がサポートされていますが、markdown は単純なカードではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-115">**Simple Cards**: Limited HTML is supported, but markdown is not supported in simple cards.</span></span>

## <a name="markdown-formatting-for-adaptive-cards"></a><span data-ttu-id="d49ae-116">アダプティブカードの Markdown の書式設定</span><span class="sxs-lookup"><span data-stu-id="d49ae-116">Markdown formatting for Adaptive Cards</span></span>

 <span data-ttu-id="d49ae-117">と`Textblock` `Fact.Value`で`Fact.Title`サポートされているスタイルは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d49ae-117">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="d49ae-118">Style</span><span class="sxs-lookup"><span data-stu-id="d49ae-118">Style</span></span> | <span data-ttu-id="d49ae-119">例</span><span class="sxs-lookup"><span data-stu-id="d49ae-119">Example</span></span> | <span data-ttu-id="d49ae-120">Markdown</span><span class="sxs-lookup"><span data-stu-id="d49ae-120">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d49ae-121">bold</span><span class="sxs-lookup"><span data-stu-id="d49ae-121">bold</span></span> | <span data-ttu-id="d49ae-122">**Bold**</span><span class="sxs-lookup"><span data-stu-id="d49ae-122">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="d49ae-123">italic</span><span class="sxs-lookup"><span data-stu-id="d49ae-123">italic</span></span> | <span data-ttu-id="d49ae-124">_Italic_</span><span class="sxs-lookup"><span data-stu-id="d49ae-124">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="d49ae-125">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-125">unordered list</span></span> | <ul><li><span data-ttu-id="d49ae-126">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-126">text</span></span></li><li><span data-ttu-id="d49ae-127">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-127">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="d49ae-128">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-128">ordered list</span></span> | <ol><li><span data-ttu-id="d49ae-129">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-129">text</span></span></li><li><span data-ttu-id="d49ae-130">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-130">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="d49ae-131">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="d49ae-131">Hyperlinks</span></span> |[<span data-ttu-id="d49ae-132">Bing</span><span class="sxs-lookup"><span data-stu-id="d49ae-132">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="d49ae-133">次の markdown タグはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-133">The following markdown tags are not supported:</span></span>

* <span data-ttu-id="d49ae-134">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="d49ae-134">Headers</span></span>
* <span data-ttu-id="d49ae-135">テーブル</span><span class="sxs-lookup"><span data-stu-id="d49ae-135">Tables</span></span>
* <span data-ttu-id="d49ae-136">画像</span><span class="sxs-lookup"><span data-stu-id="d49ae-136">Images</span></span>
* <span data-ttu-id="d49ae-137">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-137">Preformatted text</span></span>
* <span data-ttu-id="d49ae-138">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="d49ae-138">Blockquotes</span></span>

<span data-ttu-id="d49ae-139">アダプティブカードでは、HTML 形式はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-139">Adaptive cards do not support any HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="d49ae-140">アダプティブカードの改行</span><span class="sxs-lookup"><span data-stu-id="d49ae-140">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="d49ae-141">リストでは、 `\r`または`\n`エスケープシーケンスを使用して改行することができます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-141">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="d49ae-142">リスト`\n\n`でを使用すると、リスト内の次の要素がインデントされます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-142">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="d49ae-143">Textblock の他の場所に改行が必要な`\n\n`場合は、を使用します。</span><span class="sxs-lookup"><span data-stu-id="d49ae-143">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="d49ae-144">アダプティブカードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="d49ae-144">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="d49ae-145">デスクトップとモバイルバージョンの Teams では、書式設定が若干異なります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-145">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="d49ae-146">デスクトップでは、アダプティブカードの markdown 書式は、web ブラウザーと Teams クライアントアプリケーションの両方で次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-146">On the desktop, Adaptive Card markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![デスクトップクライアントでのアダプティブカード Markdown の書式設定](~/assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="d49ae-148">IOS では、アダプティブカード markdown 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-148">On iOS, Adaptive Card markdown formatting appears like this:</span></span>

![IOS のアダプティブカード Markdown 形式](~/assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="d49ae-150">Android では、アダプティブカードの markdown 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-150">On Android, Adaptive Card markdown formatting appears like this:</span></span>

![Android のアダプティブカード Markdown 形式](~/assets/images/cards/Adaptive-markdown-Android.png)

### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="d49ae-152">アダプティブカードの詳細については、</span><span class="sxs-lookup"><span data-stu-id="d49ae-152">For more information on Adaptive Cards</span></span>

<span data-ttu-id="d49ae-153">[アダプティブカードのテキスト機能](/adaptive-cards/create/textfeatures)このトピックで説明する日付とローカリゼーションの機能は、Teams ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-153">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="d49ae-154">アダプティブカード用の書式設定のサンプル</span><span class="sxs-lookup"><span data-stu-id="d49ae-154">Formatting sample for Adaptive cards</span></span>

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

## <a name="mention-support-within-adaptive-cards"></a><span data-ttu-id="d49ae-155">アダプティブカード内でのサポートを伝えます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-155">Mention support within Adaptive cards</span></span> 

> [!NOTE]
> <span data-ttu-id="d49ae-156">現在、カードでのサポートは、[開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)のみでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d49ae-156">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="d49ae-157">ボットおよびメッセージング拡張機能は、テキストブロックと FactSet 要素のカードコンテンツ内にメンションを含めることができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="d49ae-157">Bots and Messaging extensions can now include mentions within the card content in Text Block and FactSet elements.</span></span> 

### <a name="constructing-mentions"></a><span data-ttu-id="d49ae-158">メンションの構築</span><span class="sxs-lookup"><span data-stu-id="d49ae-158">Constructing mentions</span></span>

<span data-ttu-id="d49ae-159">アダプティブカードにメンションを含めるには、アプリに次の要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-159">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="d49ae-160">`<at>username</at>`サポートされているアダプティブカード要素</span><span class="sxs-lookup"><span data-stu-id="d49ae-160">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="d49ae-161">カード`mention`コンテンツ内の`msteams`プロパティの内部にあるオブジェクト。このオブジェクトは、説明されているユーザーの Teams ユーザー id を含みます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-161">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

<span data-ttu-id="d49ae-162">この時点では、メンション付きのカードはモバイルクライアントではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-162">Note that cards with mentions aren't supported on mobile clients at the moment.</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="d49ae-163">アダプティブカードのサンプル</span><span class="sxs-lookup"><span data-stu-id="d49ae-163">Sample Adaptive card with a mention</span></span>

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

## <a name="html-formatting-for-connector-cards"></a><span data-ttu-id="d49ae-164">コネクタカードの HTML 形式</span><span class="sxs-lookup"><span data-stu-id="d49ae-164">HTML formatting for Connector Cards</span></span>

<span data-ttu-id="d49ae-165">コネクタカードは、制限付きの markdown および HTML 形式をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d49ae-165">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="d49ae-166">Markdown については、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="d49ae-166">Markdown is described in the next section.</span></span>

| <span data-ttu-id="d49ae-167">Style</span><span class="sxs-lookup"><span data-stu-id="d49ae-167">Style</span></span> | <span data-ttu-id="d49ae-168">例</span><span class="sxs-lookup"><span data-stu-id="d49ae-168">Example</span></span> | <span data-ttu-id="d49ae-169">HTML</span><span class="sxs-lookup"><span data-stu-id="d49ae-169">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d49ae-170">bold</span><span class="sxs-lookup"><span data-stu-id="d49ae-170">bold</span></span> | <span data-ttu-id="d49ae-171">**text**</span><span class="sxs-lookup"><span data-stu-id="d49ae-171">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="d49ae-172">italic</span><span class="sxs-lookup"><span data-stu-id="d49ae-172">italic</span></span> | <span data-ttu-id="d49ae-173">*text*</span><span class="sxs-lookup"><span data-stu-id="d49ae-173">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="d49ae-174">ヘッダー (レベル 1&ndash;3)</span><span class="sxs-lookup"><span data-stu-id="d49ae-174">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="d49ae-175">**Text**</span><span class="sxs-lookup"><span data-stu-id="d49ae-175">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="d49ae-176">打ち消し</span><span class="sxs-lookup"><span data-stu-id="d49ae-176">strikethrough</span></span> | <span data-ttu-id="d49ae-177">~~text~~</span><span class="sxs-lookup"><span data-stu-id="d49ae-177">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="d49ae-178">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-178">unordered list</span></span> | <ul><li><span data-ttu-id="d49ae-179">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-179">text</span></span></li><li><span data-ttu-id="d49ae-180">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-180">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="d49ae-181">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-181">ordered list</span></span> | <ol><li><span data-ttu-id="d49ae-182">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-182">text</span></span></li><li><span data-ttu-id="d49ae-183">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-183">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="d49ae-184">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-184">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="d49ae-185">blockquote</span><span class="sxs-lookup"><span data-stu-id="d49ae-185">blockquote</span></span> | <blockquote><span data-ttu-id="d49ae-186">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-186">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="d49ae-187">hyperlink</span><span class="sxs-lookup"><span data-stu-id="d49ae-187">hyperlink</span></span> | [<span data-ttu-id="d49ae-188">Bing</span><span class="sxs-lookup"><span data-stu-id="d49ae-188">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="d49ae-189">画像リンク</span><span class="sxs-lookup"><span data-stu-id="d49ae-189">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="d49ae-190">コネクタカードでは、改行は`<p>`タグを使用して HTML でレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-190">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="d49ae-191">HTML を使用するコネクタカードのモバイルとデスクトップの相違点</span><span class="sxs-lookup"><span data-stu-id="d49ae-191">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="d49ae-192">デスクトップでは、コネクタカードの HTML 書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-192">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![デスクトップクライアントのコネクタカードの HTML 形式](~/assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="d49ae-194">IOS では、HTML 形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-194">On iOS, HTML formatting looks like this:</span></span>

![IOS クライアントでのコネクタカードの HTML 書式設定](~/assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="d49ae-196">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="d49ae-196">Issues:</span></span>

* <span data-ttu-id="d49ae-197">インライン画像は、コネクタカードで markdown または HTML のどちらかを使用して iOS でレンダリングされることはありません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-197">Inline images are not rendered on iOS using either markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="d49ae-198">書式設定済みのテキストは表示されますが、灰色の背景は表示されません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-198">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="d49ae-199">Android では、HTML 形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-199">On Android, HTML formatting looks like this:</span></span>

![Android クライアントでのコネクタカードの HTML 書式設定](~/assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="d49ae-201">HTML コネクタカードの書式設定のサンプル</span><span class="sxs-lookup"><span data-stu-id="d49ae-201">Formatting sample for HTML Connector Cards</span></span>

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

## <a name="markdown-formatting-for-connector-cards"></a><span data-ttu-id="d49ae-202">コネクタカードの Markdown の書式設定</span><span class="sxs-lookup"><span data-stu-id="d49ae-202">Markdown formatting for Connector Cards</span></span>

<span data-ttu-id="d49ae-203">コネクタカードは、制限付きの markdown および HTML 形式をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d49ae-203">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="d49ae-204">HTML については、最後のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="d49ae-204">HTML is described in the last section.</span></span>

| <span data-ttu-id="d49ae-205">Style</span><span class="sxs-lookup"><span data-stu-id="d49ae-205">Style</span></span> | <span data-ttu-id="d49ae-206">例</span><span class="sxs-lookup"><span data-stu-id="d49ae-206">Example</span></span> | <span data-ttu-id="d49ae-207">Markdown</span><span class="sxs-lookup"><span data-stu-id="d49ae-207">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d49ae-208">bold</span><span class="sxs-lookup"><span data-stu-id="d49ae-208">bold</span></span> | <span data-ttu-id="d49ae-209">**text**</span><span class="sxs-lookup"><span data-stu-id="d49ae-209">**text**</span></span> | `**text**` |
| <span data-ttu-id="d49ae-210">italic</span><span class="sxs-lookup"><span data-stu-id="d49ae-210">italic</span></span> | <span data-ttu-id="d49ae-211">*text*</span><span class="sxs-lookup"><span data-stu-id="d49ae-211">*text*</span></span> | `*text*` |
| <span data-ttu-id="d49ae-212">ヘッダー (レベル 1&ndash;3)</span><span class="sxs-lookup"><span data-stu-id="d49ae-212">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="d49ae-213">**Text**</span><span class="sxs-lookup"><span data-stu-id="d49ae-213">**Text**</span></span> | `### Text`|
| <span data-ttu-id="d49ae-214">打ち消し</span><span class="sxs-lookup"><span data-stu-id="d49ae-214">strikethrough</span></span> | <span data-ttu-id="d49ae-215">~~text~~</span><span class="sxs-lookup"><span data-stu-id="d49ae-215">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="d49ae-216">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-216">unordered list</span></span> | <ul><li><span data-ttu-id="d49ae-217">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-217">text</span></span></li><li><span data-ttu-id="d49ae-218">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-218">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="d49ae-219">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-219">ordered list</span></span> | <ol><li><span data-ttu-id="d49ae-220">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-220">text</span></span></li><li><span data-ttu-id="d49ae-221">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-221">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="d49ae-222">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-222">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="d49ae-223">blockquote</span><span class="sxs-lookup"><span data-stu-id="d49ae-223">blockquote</span></span> | <span data-ttu-id="d49ae-224">>blockquote テキスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-224">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="d49ae-225">hyperlink</span><span class="sxs-lookup"><span data-stu-id="d49ae-225">hyperlink</span></span> | [<span data-ttu-id="d49ae-226">Bing</span><span class="sxs-lookup"><span data-stu-id="d49ae-226">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="d49ae-227">画像リンク</span><span class="sxs-lookup"><span data-stu-id="d49ae-227">image link</span></span> |![岩に関するアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="d49ae-229">コネクタカードで`\n\n` `\n`は、改行はに対してレンダリングされ`\r`ますが、では表示されません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-229">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="d49ae-230">Markdown を使用したコネクタカードのモバイルとデスクトップの相違点</span><span class="sxs-lookup"><span data-stu-id="d49ae-230">Mobile and desktop differences for connector cards using markdown</span></span>

<span data-ttu-id="d49ae-231">デスクトップでは、markdown のコネクタカードの書式は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-231">On the desktop, markdown formatting for connector cards looks like this:</span></span>

![デスクトップクライアントのコネクタカードの HTML 形式](~/assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="d49ae-233">IOS では、markdown のコネクタカードの書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-233">On iOS, markdown formatting for connector cards looks like this:</span></span>

![IOS クライアントでのコネクタカードの HTML 書式設定](~/assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="d49ae-235">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="d49ae-235">Issues:</span></span>

* <span data-ttu-id="d49ae-236">Teams の iOS クライアントは、コネクタカードで markdown または HTML インライン画像を表示しません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-236">The iOS client for Teams does not render markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="d49ae-237">Blockquotes はインデント付きですが、灰色は表示されません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-237">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="d49ae-238">Android では、markdown のコネクタカードの書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-238">On Android, markdown formatting for connector cards looks like this:</span></span>

![Android クライアントでのコネクタカードの HTML 書式設定](~/assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="d49ae-240">Markdown コネクタカードの書式設定の例</span><span class="sxs-lookup"><span data-stu-id="d49ae-240">Formatting example for markdown Connector Cards</span></span>

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

## <a name="html-formatting-for-simple-cards"></a><span data-ttu-id="d49ae-241">シンプルなカードの HTML 形式</span><span class="sxs-lookup"><span data-stu-id="d49ae-241">HTML Formatting for simple cards</span></span>

<span data-ttu-id="d49ae-242">これらの HTML タグは、ヒーローやサムネイルカードなどの単純なカードでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d49ae-242">These HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="d49ae-243">Markdown はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-243">Markdown is not supported.</span></span>

| <span data-ttu-id="d49ae-244">Style</span><span class="sxs-lookup"><span data-stu-id="d49ae-244">Style</span></span> | <span data-ttu-id="d49ae-245">例</span><span class="sxs-lookup"><span data-stu-id="d49ae-245">Example</span></span> | <span data-ttu-id="d49ae-246">HTML</span><span class="sxs-lookup"><span data-stu-id="d49ae-246">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d49ae-247">bold</span><span class="sxs-lookup"><span data-stu-id="d49ae-247">bold</span></span> | <span data-ttu-id="d49ae-248">**text**</span><span class="sxs-lookup"><span data-stu-id="d49ae-248">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="d49ae-249">italic</span><span class="sxs-lookup"><span data-stu-id="d49ae-249">italic</span></span> | <span data-ttu-id="d49ae-250">*text*</span><span class="sxs-lookup"><span data-stu-id="d49ae-250">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="d49ae-251">ヘッダー (レベル 1&ndash;3)</span><span class="sxs-lookup"><span data-stu-id="d49ae-251">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="d49ae-252">**Text**</span><span class="sxs-lookup"><span data-stu-id="d49ae-252">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="d49ae-253">打ち消し</span><span class="sxs-lookup"><span data-stu-id="d49ae-253">strikethrough</span></span> | <span data-ttu-id="d49ae-254">~~text~~</span><span class="sxs-lookup"><span data-stu-id="d49ae-254">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="d49ae-255">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-255">unordered list</span></span> | <ul><li><span data-ttu-id="d49ae-256">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-256">text</span></span></li><li><span data-ttu-id="d49ae-257">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-257">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="d49ae-258">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-258">ordered list</span></span> | <ol><li><span data-ttu-id="d49ae-259">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-259">text</span></span></li><li><span data-ttu-id="d49ae-260">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-260">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="d49ae-261">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="d49ae-261">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="d49ae-262">blockquote</span><span class="sxs-lookup"><span data-stu-id="d49ae-262">blockquote</span></span> | <blockquote><span data-ttu-id="d49ae-263">text</span><span class="sxs-lookup"><span data-stu-id="d49ae-263">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="d49ae-264">hyperlink</span><span class="sxs-lookup"><span data-stu-id="d49ae-264">hyperlink</span></span> | [<span data-ttu-id="d49ae-265">Bing</span><span class="sxs-lookup"><span data-stu-id="d49ae-265">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="d49ae-266">画像リンク</span><span class="sxs-lookup"><span data-stu-id="d49ae-266">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="d49ae-267">簡単なカードのモバイルとデスクトップの相違点</span><span class="sxs-lookup"><span data-stu-id="d49ae-267">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="d49ae-268">デスクトップとモバイルプラットフォームとの間には、解像度の違いがあるため、デスクトップとモバイルバージョンの Teams との間で書式設定が異なります。</span><span class="sxs-lookup"><span data-stu-id="d49ae-268">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="d49ae-269">デスクトップでは、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-269">On the desktop, HTML formatting appears like this:</span></span>

![デスクトップクライアントの HTML 形式](~/assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="d49ae-271">IOS では、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-271">On iOS, HTML formatting appears like this:</span></span>

![IOS クライアントでの HTML 形式](~/assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="d49ae-273">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="d49ae-273">Issues:</span></span>

* <span data-ttu-id="d49ae-274">太字や斜体などの文字書式は、iOS では表示されません。</span><span class="sxs-lookup"><span data-stu-id="d49ae-274">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="d49ae-275">Android では、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-275">On Android, HTML formatting appears like this:</span></span>

![Android クライアントでの HTML 形式](~/assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="d49ae-277">Android では、太字や斜体などの文字書式が正しく表示されます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-277">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="d49ae-278">シンプルなカードにおける HTML 形式の書式設定のサンプル</span><span class="sxs-lookup"><span data-stu-id="d49ae-278">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="d49ae-279">これらのスクリーンショットは Teams AppStudio を使用して作成されています。これは、ヒーローカードの text プロパティが次の文字列に設定されています。</span><span class="sxs-lookup"><span data-stu-id="d49ae-279">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="d49ae-280">このコードを変更することにより、独自のカードで書式設定をテストできます。</span><span class="sxs-lookup"><span data-stu-id="d49ae-280">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`
