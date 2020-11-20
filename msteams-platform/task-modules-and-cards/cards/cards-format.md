---
title: カードでのテキストの書式設定
description: Microsoft Teams でのカードテキストの書式設定について説明します。
keywords: teams の bot カード形式
ms.date: 03/29/2018
ms.openlocfilehash: fcf0692fe033cd3c30ea1e3ac7bda8ddd06297ca
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346708"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="512df-104">Teams の書式設定カード</span><span class="sxs-lookup"><span data-stu-id="512df-104">Format cards in Teams</span></span>

<span data-ttu-id="512df-105">カードの種類に応じて、Markdown または HTML のどちらかを使用して、リッチテキスト形式をカードに追加できます。</span><span class="sxs-lookup"><span data-stu-id="512df-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="512df-106">カードは、title または副題のプロパティではなく、text プロパティのみの書式設定をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="512df-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="512df-107">書式は、カードの種類に応じて、XML (HTML) 形式のサブセットまたは Markdown を使用して指定できます。</span><span class="sxs-lookup"><span data-stu-id="512df-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="512df-108">Markdown の書式設定を使用して、現在および今後の開発用のアダプティブカード用にお勧めします。</span><span class="sxs-lookup"><span data-stu-id="512df-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="512df-109">カードの種類に応じて書式設定のサポートが異なります。また、カードのレンダリングはデスクトップとモバイルチームの両方のクライアントとデスクトップブラウザーの Teams で少しずつ異なります。</span><span class="sxs-lookup"><span data-stu-id="512df-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="512df-110">任意の Teams カードを含むインライン画像を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="512df-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="512df-111">画像は、、またはのファイルとして書式設定さ  `.png` `.jpg` れ、 `.gif` 1024 × 1024 px または 1 MB を超えることはできません。</span><span class="sxs-lookup"><span data-stu-id="512df-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="512df-112">アニメーション GIF は正式にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="512df-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="512df-113">*See* [カードリファレンス](./cards-reference.md#inline-card-images)を参照</span><span class="sxs-lookup"><span data-stu-id="512df-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="512df-114">Markdown を使用したカードの書式設定</span><span class="sxs-lookup"><span data-stu-id="512df-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="512df-115">Teams で Markdown をサポートするカードには、次の2つの種類があります。</span><span class="sxs-lookup"><span data-stu-id="512df-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="512df-116">**アダプティブカード**: Markdown は、およびと同様に、アダプティブカードフィールドでサポートされています `Textblock` `Fact.Title` `Fact.Value` 。</span><span class="sxs-lookup"><span data-stu-id="512df-116">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="512df-117">HTML は、アダプティブカードではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="512df-117">HTML is not supported in adaptive cards.</span></span>
> * <span data-ttu-id="512df-118">**O365 コネクタカード**: Markdown および制限付き HTML は、テキストフィールドの Office 365 コネクタカードでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="512df-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="512df-119">**Markdown の書式設定: アダプティブカード**</span><span class="sxs-lookup"><span data-stu-id="512df-119">**Markdown formatting: Adaptive Cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="512df-120">とでサポートされているスタイル `Textblock` `Fact.Title` は、次のとおりです `Fact.Value` 。</span><span class="sxs-lookup"><span data-stu-id="512df-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="512df-121">Style</span><span class="sxs-lookup"><span data-stu-id="512df-121">Style</span></span> | <span data-ttu-id="512df-122">例</span><span class="sxs-lookup"><span data-stu-id="512df-122">Example</span></span> | <span data-ttu-id="512df-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="512df-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="512df-124">bold</span><span class="sxs-lookup"><span data-stu-id="512df-124">bold</span></span> | <span data-ttu-id="512df-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="512df-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="512df-126">italic</span><span class="sxs-lookup"><span data-stu-id="512df-126">italic</span></span> | <span data-ttu-id="512df-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="512df-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="512df-128">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="512df-128">unordered list</span></span> | <ul><li><span data-ttu-id="512df-129">text</span><span class="sxs-lookup"><span data-stu-id="512df-129">text</span></span></li><li><span data-ttu-id="512df-130">text</span><span class="sxs-lookup"><span data-stu-id="512df-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="512df-131">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="512df-131">ordered list</span></span> | <ol><li><span data-ttu-id="512df-132">text</span><span class="sxs-lookup"><span data-stu-id="512df-132">text</span></span></li><li><span data-ttu-id="512df-133">text</span><span class="sxs-lookup"><span data-stu-id="512df-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="512df-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="512df-134">Hyperlinks</span></span> |[<span data-ttu-id="512df-135">Bing</span><span class="sxs-lookup"><span data-stu-id="512df-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="512df-136">次の Markdown タグはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="512df-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="512df-137">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="512df-137">Headers</span></span>
* <span data-ttu-id="512df-138">テーブル</span><span class="sxs-lookup"><span data-stu-id="512df-138">Tables</span></span>
* <span data-ttu-id="512df-139">画像</span><span class="sxs-lookup"><span data-stu-id="512df-139">Images</span></span>
* <span data-ttu-id="512df-140">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="512df-140">Preformatted text</span></span>
* <span data-ttu-id="512df-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="512df-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="512df-142">アダプティブカードは、HTML 形式をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="512df-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="512df-143">アダプティブカードの改行</span><span class="sxs-lookup"><span data-stu-id="512df-143">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="512df-144">リストで `\r` は、または `\n` エスケープシーケンスを使用して改行することができます。</span><span class="sxs-lookup"><span data-stu-id="512df-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="512df-145">`\n\n`リストでを使用すると、リスト内の次の要素がインデントされます。</span><span class="sxs-lookup"><span data-stu-id="512df-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="512df-146">Textblock の他の場所に改行が必要な場合は、を使用 `\n\n` します。</span><span class="sxs-lookup"><span data-stu-id="512df-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="512df-147">アダプティブカードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="512df-147">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="512df-148">デスクトップとモバイルバージョンの Teams では、書式設定が若干異なります。</span><span class="sxs-lookup"><span data-stu-id="512df-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="512df-149">デスクトップでは、アダプティブカードの Markdown 書式は、web ブラウザーと Teams クライアントアプリケーションの両方で次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="512df-149">On the desktop, Adaptive Card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![デスクトップクライアントでのアダプティブカード Markdown の書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="512df-151">IOS では、アダプティブカード Markdown 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="512df-151">On iOS, Adaptive Card Markdown formatting appears like this:</span></span>

![IOS のアダプティブカード Markdown 形式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="512df-153">Android では、アダプティブカードの Markdown 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="512df-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Android のアダプティブカード Markdown 形式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="512df-155">アダプティブカードの詳細情報</span><span class="sxs-lookup"><span data-stu-id="512df-155">More information on Adaptive Cards</span></span>

<span data-ttu-id="512df-156">[アダプティブカードのテキスト機能](/adaptive-cards/create/textfeatures) このトピックで説明する日付とローカリゼーションの機能は、Teams ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="512df-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="512df-157">アダプティブカード用の書式設定のサンプル</span><span class="sxs-lookup"><span data-stu-id="512df-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
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
            "text": "Check out [Adaptive Cards](https://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="512df-158">アダプティブカード v2.0 でのサポートを説明します。</span><span class="sxs-lookup"><span data-stu-id="512df-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="512df-159">カードベースのメンションは、Web、デスクトップ、モバイルクライアントでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="512df-159">Card based mentions are supported in Web, Desktop and mobile clients.</span></span> <span data-ttu-id="512df-160">ボットおよびメッセージング拡張機能の応答には、アダプティブカードの本文内に @ メンションを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="512df-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span>  <span data-ttu-id="512df-161">カードに @ メンションを追加するには、同じ通知ロジックに従って、 [チャネルおよびグループチャットの会話に](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions )あるメッセージに基づいたものとしてレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="512df-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).</span></span>

<span data-ttu-id="512df-162">ボットおよびメッセージング拡張機能には、 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) および [FactSet](https://adaptivecards.io/explorer/FactSet.html) 要素のカードコンテンツ内のメンションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="512df-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="512df-163">[Media 要素](https://adaptivecards.io/explorer/Media.html) は、現在 Teams プラットフォームのアダプティブカード v2.0 ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="512df-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="512df-164">チャネル & チームメンションは bot メッセージではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="512df-164">Channel & Team mentions are not supported in bot messages.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="512df-165">メンションの構築</span><span class="sxs-lookup"><span data-stu-id="512df-165">Constructing mentions</span></span>

<span data-ttu-id="512df-166">アダプティブカードにメンションを含めるには、アプリに次の要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="512df-166">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="512df-167">`<at>username</at>` サポートされているアダプティブカード要素</span><span class="sxs-lookup"><span data-stu-id="512df-167">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="512df-168">`mention`カードコンテンツ内のプロパティの内部にあるオブジェクト。このオブジェクトは、 `msteams` 説明されているユーザーの Teams ユーザー id を含みます。</span><span class="sxs-lookup"><span data-stu-id="512df-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="512df-169">アダプティブカードのサンプル</span><span class="sxs-lookup"><span data-stu-id="512df-169">Sample Adaptive card with a mention</span></span>

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
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
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

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="512df-170">**Markdown の形式: O365 コネクタカード**</span><span class="sxs-lookup"><span data-stu-id="512df-170">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="512df-171">コネクタカードは、制限付きの Markdown および HTML 形式をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="512df-171">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="512df-172">HTML サポートについては、前のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="512df-172">HTML support is described in the last section.</span></span>

| <span data-ttu-id="512df-173">Style</span><span class="sxs-lookup"><span data-stu-id="512df-173">Style</span></span> | <span data-ttu-id="512df-174">例</span><span class="sxs-lookup"><span data-stu-id="512df-174">Example</span></span> | <span data-ttu-id="512df-175">Markdown</span><span class="sxs-lookup"><span data-stu-id="512df-175">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="512df-176">bold</span><span class="sxs-lookup"><span data-stu-id="512df-176">bold</span></span> | <span data-ttu-id="512df-177">**text**</span><span class="sxs-lookup"><span data-stu-id="512df-177">**text**</span></span> | `**text**` |
| <span data-ttu-id="512df-178">italic</span><span class="sxs-lookup"><span data-stu-id="512df-178">italic</span></span> | <span data-ttu-id="512df-179">*text*</span><span class="sxs-lookup"><span data-stu-id="512df-179">*text*</span></span> | `*text*` |
| <span data-ttu-id="512df-180">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="512df-180">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="512df-181">**Text**</span><span class="sxs-lookup"><span data-stu-id="512df-181">**Text**</span></span> | `### Text`|
| <span data-ttu-id="512df-182">打ち消し</span><span class="sxs-lookup"><span data-stu-id="512df-182">strikethrough</span></span> | <span data-ttu-id="512df-183">~~text~~</span><span class="sxs-lookup"><span data-stu-id="512df-183">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="512df-184">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="512df-184">unordered list</span></span> | <ul><li><span data-ttu-id="512df-185">text</span><span class="sxs-lookup"><span data-stu-id="512df-185">text</span></span></li><li><span data-ttu-id="512df-186">text</span><span class="sxs-lookup"><span data-stu-id="512df-186">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="512df-187">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="512df-187">ordered list</span></span> | <ol><li><span data-ttu-id="512df-188">text</span><span class="sxs-lookup"><span data-stu-id="512df-188">text</span></span></li><li><span data-ttu-id="512df-189">text</span><span class="sxs-lookup"><span data-stu-id="512df-189">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="512df-190">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="512df-190">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="512df-191">blockquote</span><span class="sxs-lookup"><span data-stu-id="512df-191">blockquote</span></span> | <span data-ttu-id="512df-192">>blockquote テキスト</span><span class="sxs-lookup"><span data-stu-id="512df-192">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="512df-193">hyperlink</span><span class="sxs-lookup"><span data-stu-id="512df-193">hyperlink</span></span> | [<span data-ttu-id="512df-194">Bing</span><span class="sxs-lookup"><span data-stu-id="512df-194">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="512df-195">画像リンク</span><span class="sxs-lookup"><span data-stu-id="512df-195">image link</span></span> |![岩に関するアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="512df-197">コネクタカードでは、改行はに対してレンダリングされますが、では表示され `\n\n` ません `\n` `\r` 。</span><span class="sxs-lookup"><span data-stu-id="512df-197">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="512df-198">Markdown を使用したコネクタカードのモバイルとデスクトップの相違点</span><span class="sxs-lookup"><span data-stu-id="512df-198">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="512df-199">デスクトップでは、Markdown のコネクタカードの書式は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="512df-199">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![デスクトップクライアントでのコネクタカードの Markdown の書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="512df-201">IOS では、Markdown のコネクタカードの書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="512df-201">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![IOS クライアントでのコネクタカードの Markdown の書式設定](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="512df-203">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="512df-203">Issues:</span></span>

* <span data-ttu-id="512df-204">Teams の iOS クライアントは、コネクタカードで Markdown または HTML インライン画像を表示しません。</span><span class="sxs-lookup"><span data-stu-id="512df-204">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="512df-205">Blockquotes はインデント付きですが、灰色は表示されません。</span><span class="sxs-lookup"><span data-stu-id="512df-205">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="512df-206">Android では、Markdown のコネクタカードの書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="512df-206">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android クライアントでのコネクタカードの Markdown の書式設定](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="512df-208">Markdown コネクタカードの書式設定の例</span><span class="sxs-lookup"><span data-stu-id="512df-208">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
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
            "text": "embedded image link: ![Duck on a rock](https://aka.ms/Fo983c)"
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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="512df-209">HTML を使用してカードを書式設定する</span><span class="sxs-lookup"><span data-stu-id="512df-209">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="512df-210">**HTML 形式: O365 コネクタカード**</span><span class="sxs-lookup"><span data-stu-id="512df-210">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="512df-211">コネクタカードは、制限付きの Markdown および HTML 形式をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="512df-211">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="512df-212">Markdown については、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="512df-212">Markdown is described in the next section.</span></span>

| <span data-ttu-id="512df-213">Style</span><span class="sxs-lookup"><span data-stu-id="512df-213">Style</span></span> | <span data-ttu-id="512df-214">例</span><span class="sxs-lookup"><span data-stu-id="512df-214">Example</span></span> | <span data-ttu-id="512df-215">HTML</span><span class="sxs-lookup"><span data-stu-id="512df-215">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="512df-216">bold</span><span class="sxs-lookup"><span data-stu-id="512df-216">bold</span></span> | <span data-ttu-id="512df-217">**text**</span><span class="sxs-lookup"><span data-stu-id="512df-217">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="512df-218">italic</span><span class="sxs-lookup"><span data-stu-id="512df-218">italic</span></span> | <span data-ttu-id="512df-219">*text*</span><span class="sxs-lookup"><span data-stu-id="512df-219">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="512df-220">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="512df-220">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="512df-221">**Text**</span><span class="sxs-lookup"><span data-stu-id="512df-221">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="512df-222">打ち消し</span><span class="sxs-lookup"><span data-stu-id="512df-222">strikethrough</span></span> | <span data-ttu-id="512df-223">~~text~~</span><span class="sxs-lookup"><span data-stu-id="512df-223">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="512df-224">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="512df-224">unordered list</span></span> | <ul><li><span data-ttu-id="512df-225">text</span><span class="sxs-lookup"><span data-stu-id="512df-225">text</span></span></li><li><span data-ttu-id="512df-226">text</span><span class="sxs-lookup"><span data-stu-id="512df-226">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="512df-227">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="512df-227">ordered list</span></span> | <ol><li><span data-ttu-id="512df-228">text</span><span class="sxs-lookup"><span data-stu-id="512df-228">text</span></span></li><li><span data-ttu-id="512df-229">text</span><span class="sxs-lookup"><span data-stu-id="512df-229">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="512df-230">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="512df-230">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="512df-231">blockquote</span><span class="sxs-lookup"><span data-stu-id="512df-231">blockquote</span></span> | <blockquote><span data-ttu-id="512df-232">text</span><span class="sxs-lookup"><span data-stu-id="512df-232">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="512df-233">hyperlink</span><span class="sxs-lookup"><span data-stu-id="512df-233">hyperlink</span></span> | [<span data-ttu-id="512df-234">Bing</span><span class="sxs-lookup"><span data-stu-id="512df-234">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="512df-235">画像リンク</span><span class="sxs-lookup"><span data-stu-id="512df-235">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="512df-236">コネクタカードでは、改行はタグを使用して HTML でレンダリングされ `<p>` ます。</span><span class="sxs-lookup"><span data-stu-id="512df-236">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="512df-237">HTML を使用するコネクタカードのモバイルとデスクトップの相違点</span><span class="sxs-lookup"><span data-stu-id="512df-237">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="512df-238">デスクトップでは、コネクタカードの HTML 書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="512df-238">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![デスクトップクライアントのコネクタカードの HTML 形式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="512df-240">IOS では、HTML 形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="512df-240">On iOS, HTML formatting looks like this:</span></span>

![IOS クライアントでのコネクタカードの HTML 書式設定](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="512df-242">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="512df-242">Issues:</span></span>

* <span data-ttu-id="512df-243">インライン画像は、コネクタカードで Markdown または HTML のどちらかを使用して iOS でレンダリングされることはありません。</span><span class="sxs-lookup"><span data-stu-id="512df-243">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="512df-244">書式設定済みのテキストは表示されますが、灰色の背景は表示されません。</span><span class="sxs-lookup"><span data-stu-id="512df-244">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="512df-245">Android では、HTML 形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="512df-245">On Android, HTML formatting looks like this:</span></span>

![Android クライアントでのコネクタカードの HTML 書式設定](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="512df-247">HTML コネクタカードの書式設定のサンプル</span><span class="sxs-lookup"><span data-stu-id="512df-247">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
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
            "text": "embedded image <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="512df-248">**HTML 形式: 英雄とサムネイルカード**</span><span class="sxs-lookup"><span data-stu-id="512df-248">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="512df-249">HTML タグは、ヒーローやサムネイルカードなどの単純なカードでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="512df-249">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="512df-250">Markdown はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="512df-250">Markdown is not supported.</span></span>

| <span data-ttu-id="512df-251">Style</span><span class="sxs-lookup"><span data-stu-id="512df-251">Style</span></span> | <span data-ttu-id="512df-252">例</span><span class="sxs-lookup"><span data-stu-id="512df-252">Example</span></span> | <span data-ttu-id="512df-253">HTML</span><span class="sxs-lookup"><span data-stu-id="512df-253">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="512df-254">bold</span><span class="sxs-lookup"><span data-stu-id="512df-254">bold</span></span> | <span data-ttu-id="512df-255">**text**</span><span class="sxs-lookup"><span data-stu-id="512df-255">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="512df-256">italic</span><span class="sxs-lookup"><span data-stu-id="512df-256">italic</span></span> | <span data-ttu-id="512df-257">*text*</span><span class="sxs-lookup"><span data-stu-id="512df-257">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="512df-258">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="512df-258">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="512df-259">**Text**</span><span class="sxs-lookup"><span data-stu-id="512df-259">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="512df-260">打ち消し</span><span class="sxs-lookup"><span data-stu-id="512df-260">strikethrough</span></span> | <span data-ttu-id="512df-261">~~text~~</span><span class="sxs-lookup"><span data-stu-id="512df-261">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="512df-262">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="512df-262">unordered list</span></span> | <ul><li><span data-ttu-id="512df-263">text</span><span class="sxs-lookup"><span data-stu-id="512df-263">text</span></span></li><li><span data-ttu-id="512df-264">text</span><span class="sxs-lookup"><span data-stu-id="512df-264">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="512df-265">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="512df-265">ordered list</span></span> | <ol><li><span data-ttu-id="512df-266">text</span><span class="sxs-lookup"><span data-stu-id="512df-266">text</span></span></li><li><span data-ttu-id="512df-267">text</span><span class="sxs-lookup"><span data-stu-id="512df-267">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="512df-268">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="512df-268">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="512df-269">blockquote</span><span class="sxs-lookup"><span data-stu-id="512df-269">blockquote</span></span> | <blockquote><span data-ttu-id="512df-270">text</span><span class="sxs-lookup"><span data-stu-id="512df-270">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="512df-271">hyperlink</span><span class="sxs-lookup"><span data-stu-id="512df-271">hyperlink</span></span> | [<span data-ttu-id="512df-272">Bing</span><span class="sxs-lookup"><span data-stu-id="512df-272">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="512df-273">画像リンク</span><span class="sxs-lookup"><span data-stu-id="512df-273">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="512df-274">簡単なカードのモバイルとデスクトップの相違点</span><span class="sxs-lookup"><span data-stu-id="512df-274">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="512df-275">デスクトップとモバイルプラットフォームとの間には、解像度の違いがあるため、デスクトップとモバイルバージョンの Teams との間で書式設定が異なります。</span><span class="sxs-lookup"><span data-stu-id="512df-275">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="512df-276">デスクトップでは、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="512df-276">On the desktop, HTML formatting appears like this:</span></span>

![デスクトップクライアントの HTML 形式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="512df-278">IOS では、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="512df-278">On iOS, HTML formatting appears like this:</span></span>

![IOS クライアントでの HTML 形式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="512df-280">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="512df-280">Issues:</span></span>

* <span data-ttu-id="512df-281">太字や斜体などの文字書式は、iOS では表示されません。</span><span class="sxs-lookup"><span data-stu-id="512df-281">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="512df-282">Android では、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="512df-282">On Android, HTML formatting appears like this:</span></span>

![Android クライアントでの HTML 形式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="512df-284">Android では、太字や斜体などの文字書式が正しく表示されます。</span><span class="sxs-lookup"><span data-stu-id="512df-284">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="512df-285">シンプルなカードにおける HTML 形式の書式設定のサンプル</span><span class="sxs-lookup"><span data-stu-id="512df-285">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="512df-286">これらのスクリーンショットは Teams AppStudio を使用して作成されています。これは、ヒーローカードの text プロパティが次の文字列に設定されています。</span><span class="sxs-lookup"><span data-stu-id="512df-286">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="512df-287">このコードを変更することにより、独自のカードで書式設定をテストできます。</span><span class="sxs-lookup"><span data-stu-id="512df-287">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
