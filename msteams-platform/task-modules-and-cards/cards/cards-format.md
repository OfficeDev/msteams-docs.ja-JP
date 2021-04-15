---
title: カード内のテキストの書式設定
description: Microsoft Teams のカード テキストの書式設定について説明します。
keywords: teams ボット カードの形式
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: e6b8cc835780e03cf4e23eae31fa447c8a03c002
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696536"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="421f9-104">Teams でカードを書式設定する</span><span class="sxs-lookup"><span data-stu-id="421f9-104">Format cards in Teams</span></span>

<span data-ttu-id="421f9-105">カードの種類に応じて、Markdown または HTML を使用してリッチ テキスト書式をカードに追加できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="421f9-106">カードは、タイトルプロパティや字幕プロパティではなく、text プロパティでのみ書式設定をサポートします。</span><span class="sxs-lookup"><span data-stu-id="421f9-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="421f9-107">書式設定は、カードの種類に応じて XML (HTML) 書式のサブセットまたは Markdown を使用して指定できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="421f9-108">現在および将来の開発では、Markdown 書式設定を使用したアダプティブ カードをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="421f9-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="421f9-109">書式設定のサポートはカードの種類によって異なりますが、カードのレンダリングはデスクトップとモバイル Teams クライアント、およびデスクトップ ブラウザーの Teams で若干異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="421f9-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="421f9-110">任意の Teams カードにインライン イメージを含めできます。</span><span class="sxs-lookup"><span data-stu-id="421f9-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="421f9-111">イメージは、、、またはファイルとして書式設定され  `.png` `.jpg` `.gif` 、1024 px または 1 MB を超え×する必要があります。</span><span class="sxs-lookup"><span data-stu-id="421f9-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="421f9-112">アニメーション GIF は公式にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="421f9-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="421f9-113">*「カード*[リファレンス」を参照してください。](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="421f9-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="421f9-114">Markdown を使用したカードの書式設定</span><span class="sxs-lookup"><span data-stu-id="421f9-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="421f9-115">Teams で Markdown をサポートするカードの種類は次の 2 種類です。</span><span class="sxs-lookup"><span data-stu-id="421f9-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="421f9-116">**アダプティブ カード**: Markdown はアダプティブ カード フィールドおよび . `Textblock` `Fact.Title` `Fact.Value`</span><span class="sxs-lookup"><span data-stu-id="421f9-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="421f9-117">アダプティブ カードでは HTML はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="421f9-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="421f9-118">**O365 コネクタ カード**: マークダウンと制限付き HTML は、テキスト フィールドOffice 365 コネクタ カードでサポートされます。</span><span class="sxs-lookup"><span data-stu-id="421f9-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="421f9-119">**Markdown の書式設定: アダプティブ カード**</span><span class="sxs-lookup"><span data-stu-id="421f9-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="421f9-120">サポートされているスタイルは `Textblock` 、次 `Fact.Title` `Fact.Value` のとおりです。</span><span class="sxs-lookup"><span data-stu-id="421f9-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="421f9-121">Style</span><span class="sxs-lookup"><span data-stu-id="421f9-121">Style</span></span> | <span data-ttu-id="421f9-122">例</span><span class="sxs-lookup"><span data-stu-id="421f9-122">Example</span></span> | <span data-ttu-id="421f9-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="421f9-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="421f9-124">bold</span><span class="sxs-lookup"><span data-stu-id="421f9-124">bold</span></span> | <span data-ttu-id="421f9-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="421f9-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="421f9-126">italic</span><span class="sxs-lookup"><span data-stu-id="421f9-126">italic</span></span> | <span data-ttu-id="421f9-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="421f9-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="421f9-128">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="421f9-128">unordered list</span></span> | <ul><li><span data-ttu-id="421f9-129">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-129">text</span></span></li><li><span data-ttu-id="421f9-130">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="421f9-131">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="421f9-131">ordered list</span></span> | <ol><li><span data-ttu-id="421f9-132">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-132">text</span></span></li><li><span data-ttu-id="421f9-133">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="421f9-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="421f9-134">Hyperlinks</span></span> |[<span data-ttu-id="421f9-135">Bing</span><span class="sxs-lookup"><span data-stu-id="421f9-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="421f9-136">次の Markdown タグはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="421f9-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="421f9-137">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="421f9-137">Headers</span></span>
* <span data-ttu-id="421f9-138">テーブル</span><span class="sxs-lookup"><span data-stu-id="421f9-138">Tables</span></span>
* <span data-ttu-id="421f9-139">画像</span><span class="sxs-lookup"><span data-stu-id="421f9-139">Images</span></span>
* <span data-ttu-id="421f9-140">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-140">Preformatted text</span></span>
* <span data-ttu-id="421f9-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="421f9-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="421f9-142">アダプティブ カードは HTML の書式設定をサポートしていない。</span><span class="sxs-lookup"><span data-stu-id="421f9-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="421f9-143">アダプティブ カードの改行</span><span class="sxs-lookup"><span data-stu-id="421f9-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="421f9-144">リストでは、改行に対 `\r` してエスケープ シーケンス `\n` またはエスケープ シーケンスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="421f9-145">リスト `\n\n` で使用すると、リスト内の次の要素がインデントされます。</span><span class="sxs-lookup"><span data-stu-id="421f9-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="421f9-146">テキスト ブロック内の他の場所に改行が必要な場合は、 を使用します `\n\n` 。</span><span class="sxs-lookup"><span data-stu-id="421f9-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="421f9-147">アダプティブ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="421f9-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="421f9-148">書式設定は、デスクトップとモバイル バージョンの Teams では少し異なります。</span><span class="sxs-lookup"><span data-stu-id="421f9-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="421f9-149">デスクトップでは、アダプティブ カードの Markdown 書式は、Web ブラウザーと Teams クライアント アプリケーションの両方で次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![デスクトップ クライアントでのアダプティブ カードマークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="421f9-151">iOS では、アダプティブ カードのマークダウンの書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![iOS でのアダプティブ カードマークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="421f9-153">Android では、アダプティブ カード マークダウンの書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Android のアダプティブ カード Markdown 書式設定](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="421f9-155">アダプティブ カードの詳細</span><span class="sxs-lookup"><span data-stu-id="421f9-155">More information on Adaptive cards</span></span>

<span data-ttu-id="421f9-156">[アダプティブ カードのテキスト機能](/adaptive-cards/create/textfeatures) このトピックで説明されている日付とローカライズ機能は、Teams ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="421f9-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="421f9-157">アダプティブ カードの書式設定サンプル</span><span class="sxs-lookup"><span data-stu-id="421f9-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="421f9-158">アダプティブ カード v1.2 内でのサポートのメンション</span><span class="sxs-lookup"><span data-stu-id="421f9-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="421f9-159">カード ベースのメンションは、Web、デスクトップ、モバイル クライアントでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="421f9-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="421f9-160">ボットおよびメッセージング拡張機能の応答に対して、アダプティブ カード本文内に @ メンションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="421f9-161">カードに @ メンションを追加するには、チャネルとグループ チャットの会話でメッセージ ベースのメンションと同じ通知ロジックとレンダリングに [従います](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)。</span><span class="sxs-lookup"><span data-stu-id="421f9-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="421f9-162">ボットとメッセージング拡張機能には [、TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 要素と FactSet 要素のカード コンテンツ内にメンション [を含](https://adaptivecards.io/explorer/FactSet.html) めることはできません。</span><span class="sxs-lookup"><span data-stu-id="421f9-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="421f9-163">[メディア要素](https://adaptivecards.io/explorer/Media.html) は、Teams プラットフォームのアダプティブ カード v1.2 では現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="421f9-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="421f9-164">チャネル &チームのメンションはボット メッセージではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="421f9-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="421f9-165">メンションの作成</span><span class="sxs-lookup"><span data-stu-id="421f9-165">Constructing mentions</span></span>

<span data-ttu-id="421f9-166">アダプティブ カードにメンションを含めるには、アプリに次の要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="421f9-166">To include a mention in an Adaptive card your app needs to include the following elements</span></span>

* <span data-ttu-id="421f9-167">`<at>username</at>` サポートされているアダプティブ カード要素で</span><span class="sxs-lookup"><span data-stu-id="421f9-167">`<at>username</at>` in the supported Adaptive card elements</span></span>
* <span data-ttu-id="421f9-168">カード コンテンツ内のプロパティ内のオブジェクト (言及されているユーザーの `mention` `msteams` Teams ユーザー ID を含む)</span><span class="sxs-lookup"><span data-stu-id="421f9-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="421f9-169">メンション付きアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="421f9-169">Sample Adaptive card with a mention</span></span>

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


### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="421f9-170">アダプティブ カードの情報マスキング</span><span class="sxs-lookup"><span data-stu-id="421f9-170">Information masking in Adaptive cards</span></span>
<span data-ttu-id="421f9-171">Information masking プロパティを使用して、アダプティブ カード入力要素内のユーザーからのパスワードや機密情報などの特定の情報を [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) マスクします。</span><span class="sxs-lookup"><span data-stu-id="421f9-171">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="421f9-172">この機能はクライアント側の情報マスキングのみをサポートします。マスクされた入力テキストは、ボットの構成中に指定された https エンドポイント アドレスにクリア テキスト [として送信されます](../../build-your-first-app/build-bot.md#4-configure-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="421f9-172">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-configure-your-bot).</span></span> 

> [!NOTE]
> <span data-ttu-id="421f9-173">information masking プロパティは現在、開発者プレビューでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-173">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="421f9-174">アダプティブ カードで情報をマスクするには、型に `isMasked` プロパティを追加 **し** `Input.Text` 、その値を true に設定 *します*。</span><span class="sxs-lookup"><span data-stu-id="421f9-174">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="421f9-175">マスキング プロパティを持つアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="421f9-175">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="421f9-176">次の図は、アダプティブ カードのマスキング情報の例です。</span><span class="sxs-lookup"><span data-stu-id="421f9-176">The following image is an example of masking information in Adaptive cards:</span></span>

![マスキング情報イメージ](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="421f9-178">全幅アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="421f9-178">Full width Adaptive card</span></span>
<span data-ttu-id="421f9-179">このプロパティを使用 `msteams` すると、アダプティブ カードの幅を拡大し、追加のキャンバス領域を利用できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-179">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="421f9-180">プロパティの使用方法については、次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="421f9-180">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="421f9-181">全幅カードの作成</span><span class="sxs-lookup"><span data-stu-id="421f9-181">Constructing full width cards</span></span>
<span data-ttu-id="421f9-182">全幅アダプティブ カードを作成するには、 `width` カード コンテンツのプロパティのオブジェクトをに `msteams` 設定する必要があります `Full` 。</span><span class="sxs-lookup"><span data-stu-id="421f9-182">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="421f9-183">さらに、アプリには次の要素が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="421f9-183">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="421f9-184">全幅のアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="421f9-184">Sample adaptive card with full width</span></span>

``` json
{
    "type": "AdaptiveCard",
    "body": [{
        "type": "Container",
        "items": [{
            "type": "TextBlock",
            "text": "Digest card",
            "size": "Large",
            "weight": "Bolder"
        }]
    }],

    "msteams": {
        "width": "Full"
    },
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="421f9-185">全幅アダプティブ カードは、次のように表示されます。 ![ 全幅アダプティブ カード ビュー](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="421f9-185">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="421f9-186">プロパティを Full に設定していない場合、アダプティブ カードの既定のビューは次のとおりです。小幅アダプティブ カード `width`  ![ ビュー](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="421f9-186">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="421f9-187">Typeahead のサポート</span><span class="sxs-lookup"><span data-stu-id="421f9-187">Typeahead support</span></span>

<span data-ttu-id="421f9-188">schema 要素内で、ユーザーにフィルター処理を求め、多数の選択肢を選択すると、タスクの完了が大幅 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) に遅くなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="421f9-188">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="421f9-189">アダプティブ カード内の Typeahead サポートは、ユーザーが入力を入力する場合に入力の選択肢のセットを絞り込むかフィルター処理することで、入力の選択を簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-189">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="421f9-190">アダプティブ カードで typeahead を有効にする</span><span class="sxs-lookup"><span data-stu-id="421f9-190">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="421f9-191">セット内で typeahead を有効 `Input.Choiceset` にし `style` 、 `filtered` 必ずに `isMultiSelect` に設定します `false` 。</span><span class="sxs-lookup"><span data-stu-id="421f9-191">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="421f9-192">typeahead サポートを備えるアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="421f9-192">Sample adaptive card with typeahead support</span></span>

``` json
{
   "type": "Input.ChoiceSet",
   "label": "Select a user",
   "isMultiSelect": false,
   "choices":  [
      { "title": "User 1", "value": "User1" },
      { "title": "User 2", "value": "User2" }
    ],
   "style": "filtered"
}
``` 

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="421f9-193">アダプティブ カードの画像のステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="421f9-193">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="421f9-194">この機能は現在、開発者プレビューでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-194">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="421f9-195">アダプティブ カードでは、このプロパティを使用して、ステージ ビューに画像を選択的 `msteams` に表示する機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-195">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="421f9-196">ユーザーが画像にカーソルを合わせると、展開アイコンが表示され、属性が `allowExpand` に設定されます `true` 。</span><span class="sxs-lookup"><span data-stu-id="421f9-196">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="421f9-197">プロパティの使用方法については、次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="421f9-197">For information on how to use the property, see the following example:</span></span>

``` json
{
    "type": "AdaptiveCard",
     "body": [
          {
            "type": "Image",
            "url": "https://picsum.photos/200/200?image=110",
            "msTeams": {
              "allowExpand": true
            }
          },
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="421f9-198">ユーザーが画像の上にマウス ポインターを置くと、画像の右上隅に展開アイコンが表示されます。展開可能なイメージを持つ ![ アダプティブ カード](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="421f9-198">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="421f9-199">ユーザーが展開ボタンを選択すると、イメージがステージ ビューに表示されます。 ![ イメージはステージ ビューに展開されます。](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="421f9-199">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="421f9-200">ステージ ビューでは、ユーザーは画像を拡大および縮小できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-200">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="421f9-201">アダプティブ カードでこの機能を使用する必要があるイメージを選択できます。</span><span class="sxs-lookup"><span data-stu-id="421f9-201">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="421f9-202">拡大および縮小機能は、アダプティブ カード内のイメージ要素 (画像の種類) にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-202">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="421f9-203">Teams モバイル アプリの場合、アダプティブ カードの画像のステージ ビュー機能は既定で利用できます。ユーザーは、属性が存在するかどうかに関係なく、画像をタップするだけでステージ ビューでアダプティブ カードイメージを表示できます。 `allowExpand`</span><span class="sxs-lookup"><span data-stu-id="421f9-203">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="421f9-204">**Markdown の書式設定: O365 コネクタ カード**</span><span class="sxs-lookup"><span data-stu-id="421f9-204">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="421f9-205">コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。</span><span class="sxs-lookup"><span data-stu-id="421f9-205">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="421f9-206">HTML サポートについては、最後のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="421f9-206">HTML support is described in the last section.</span></span>

| <span data-ttu-id="421f9-207">Style</span><span class="sxs-lookup"><span data-stu-id="421f9-207">Style</span></span> | <span data-ttu-id="421f9-208">例</span><span class="sxs-lookup"><span data-stu-id="421f9-208">Example</span></span> | <span data-ttu-id="421f9-209">Markdown</span><span class="sxs-lookup"><span data-stu-id="421f9-209">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="421f9-210">bold</span><span class="sxs-lookup"><span data-stu-id="421f9-210">bold</span></span> | <span data-ttu-id="421f9-211">**text**</span><span class="sxs-lookup"><span data-stu-id="421f9-211">**text**</span></span> | `**text**` |
| <span data-ttu-id="421f9-212">italic</span><span class="sxs-lookup"><span data-stu-id="421f9-212">italic</span></span> | <span data-ttu-id="421f9-213">*text*</span><span class="sxs-lookup"><span data-stu-id="421f9-213">*text*</span></span> | `*text*` |
| <span data-ttu-id="421f9-214">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="421f9-214">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="421f9-215">**Text**</span><span class="sxs-lookup"><span data-stu-id="421f9-215">**Text**</span></span> | `### Text`|
| <span data-ttu-id="421f9-216">取り消し線</span><span class="sxs-lookup"><span data-stu-id="421f9-216">strikethrough</span></span> | <span data-ttu-id="421f9-217">~~text~~</span><span class="sxs-lookup"><span data-stu-id="421f9-217">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="421f9-218">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="421f9-218">unordered list</span></span> | <ul><li><span data-ttu-id="421f9-219">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-219">text</span></span></li><li><span data-ttu-id="421f9-220">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-220">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="421f9-221">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="421f9-221">ordered list</span></span> | <ol><li><span data-ttu-id="421f9-222">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-222">text</span></span></li><li><span data-ttu-id="421f9-223">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-223">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="421f9-224">事前に書式設定されたテキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-224">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="421f9-225">blockquote</span><span class="sxs-lookup"><span data-stu-id="421f9-225">blockquote</span></span> | <span data-ttu-id="421f9-226">>をブロッククォートする</span><span class="sxs-lookup"><span data-stu-id="421f9-226">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="421f9-227">hyperlink</span><span class="sxs-lookup"><span data-stu-id="421f9-227">hyperlink</span></span> | [<span data-ttu-id="421f9-228">Bing</span><span class="sxs-lookup"><span data-stu-id="421f9-228">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="421f9-229">画像リンク</span><span class="sxs-lookup"><span data-stu-id="421f9-229">image link</span></span> |![岩の上のアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="421f9-231">コネクタ カードでは、改行はのためにレンダリングされますが `\n\n` 、for または `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="421f9-231">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="421f9-232">Markdown を使用したコネクタ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="421f9-232">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="421f9-233">デスクトップでは、コネクタ カードの Markdown 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-233">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![デスクトップ クライアントでのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="421f9-235">iOS では、コネクタ カードの Markdown 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-235">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![iOS クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="421f9-237">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="421f9-237">Issues:</span></span>

* <span data-ttu-id="421f9-238">Teams の iOS クライアントは、コネクタ カードで Markdown または HTML インライン イメージをレンダリングしない。</span><span class="sxs-lookup"><span data-stu-id="421f9-238">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="421f9-239">ブロッククォートはインデントされますが、灰色の背景なしでレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="421f9-239">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="421f9-240">Android では、コネクタ カードの Markdown 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-240">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="421f9-242">Markdown コネクタ カードの書式設定の例</span><span class="sxs-lookup"><span data-stu-id="421f9-242">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="421f9-243">HTML を使用したカードの書式設定</span><span class="sxs-lookup"><span data-stu-id="421f9-243">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="421f9-244">**HTML の書式設定: O365 コネクタ カード**</span><span class="sxs-lookup"><span data-stu-id="421f9-244">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="421f9-245">コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。</span><span class="sxs-lookup"><span data-stu-id="421f9-245">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="421f9-246">マークダウンについては、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="421f9-246">Markdown is described in the next section.</span></span>

| <span data-ttu-id="421f9-247">Style</span><span class="sxs-lookup"><span data-stu-id="421f9-247">Style</span></span> | <span data-ttu-id="421f9-248">例</span><span class="sxs-lookup"><span data-stu-id="421f9-248">Example</span></span> | <span data-ttu-id="421f9-249">HTML</span><span class="sxs-lookup"><span data-stu-id="421f9-249">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="421f9-250">bold</span><span class="sxs-lookup"><span data-stu-id="421f9-250">bold</span></span> | <span data-ttu-id="421f9-251">**text**</span><span class="sxs-lookup"><span data-stu-id="421f9-251">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="421f9-252">italic</span><span class="sxs-lookup"><span data-stu-id="421f9-252">italic</span></span> | <span data-ttu-id="421f9-253">*text*</span><span class="sxs-lookup"><span data-stu-id="421f9-253">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="421f9-254">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="421f9-254">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="421f9-255">**Text**</span><span class="sxs-lookup"><span data-stu-id="421f9-255">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="421f9-256">取り消し線</span><span class="sxs-lookup"><span data-stu-id="421f9-256">strikethrough</span></span> | <span data-ttu-id="421f9-257">~~text~~</span><span class="sxs-lookup"><span data-stu-id="421f9-257">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="421f9-258">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="421f9-258">unordered list</span></span> | <ul><li><span data-ttu-id="421f9-259">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-259">text</span></span></li><li><span data-ttu-id="421f9-260">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-260">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="421f9-261">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="421f9-261">ordered list</span></span> | <ol><li><span data-ttu-id="421f9-262">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-262">text</span></span></li><li><span data-ttu-id="421f9-263">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-263">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="421f9-264">事前に書式設定されたテキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-264">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="421f9-265">blockquote</span><span class="sxs-lookup"><span data-stu-id="421f9-265">blockquote</span></span> | <blockquote><span data-ttu-id="421f9-266">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-266">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="421f9-267">hyperlink</span><span class="sxs-lookup"><span data-stu-id="421f9-267">hyperlink</span></span> | [<span data-ttu-id="421f9-268">Bing</span><span class="sxs-lookup"><span data-stu-id="421f9-268">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="421f9-269">画像リンク</span><span class="sxs-lookup"><span data-stu-id="421f9-269">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="421f9-270">コネクタ カードでは、タグを使用して改行が HTML でレンダリング `<p>` されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-270">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="421f9-271">HTML を使用したコネクタ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="421f9-271">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="421f9-272">デスクトップでは、コネクタ カードの HTML 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-272">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![デスクトップ クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="421f9-274">iOS では、HTML の書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-274">On iOS, HTML formatting looks like this:</span></span>

![iOS クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="421f9-276">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="421f9-276">Issues:</span></span>

* <span data-ttu-id="421f9-277">インライン イメージは、コネクタ カードの Markdown または HTML を使用して iOS ではレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="421f9-277">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="421f9-278">書式設定済みのテキストはレンダリングされますが、背景が灰色ではありません。</span><span class="sxs-lookup"><span data-stu-id="421f9-278">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="421f9-279">Android では、HTML の書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-279">On Android, HTML formatting looks like this:</span></span>

![Android クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="421f9-281">HTML コネクタ カードの書式設定サンプル</span><span class="sxs-lookup"><span data-stu-id="421f9-281">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="421f9-282">**HTML の書式設定: ヒーローカードとサムネイル カード**</span><span class="sxs-lookup"><span data-stu-id="421f9-282">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="421f9-283">HTML タグは、ヒーロー カードやサムネイル カードなどの単純なカードでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="421f9-283">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="421f9-284">Markdown はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="421f9-284">Markdown is not supported.</span></span>

| <span data-ttu-id="421f9-285">Style</span><span class="sxs-lookup"><span data-stu-id="421f9-285">Style</span></span> | <span data-ttu-id="421f9-286">例</span><span class="sxs-lookup"><span data-stu-id="421f9-286">Example</span></span> | <span data-ttu-id="421f9-287">HTML</span><span class="sxs-lookup"><span data-stu-id="421f9-287">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="421f9-288">bold</span><span class="sxs-lookup"><span data-stu-id="421f9-288">bold</span></span> | <span data-ttu-id="421f9-289">**text**</span><span class="sxs-lookup"><span data-stu-id="421f9-289">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="421f9-290">italic</span><span class="sxs-lookup"><span data-stu-id="421f9-290">italic</span></span> | <span data-ttu-id="421f9-291">*text*</span><span class="sxs-lookup"><span data-stu-id="421f9-291">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="421f9-292">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="421f9-292">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="421f9-293">**Text**</span><span class="sxs-lookup"><span data-stu-id="421f9-293">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="421f9-294">取り消し線</span><span class="sxs-lookup"><span data-stu-id="421f9-294">strikethrough</span></span> | <span data-ttu-id="421f9-295">~~text~~</span><span class="sxs-lookup"><span data-stu-id="421f9-295">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="421f9-296">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="421f9-296">unordered list</span></span> | <ul><li><span data-ttu-id="421f9-297">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-297">text</span></span></li><li><span data-ttu-id="421f9-298">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-298">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="421f9-299">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="421f9-299">ordered list</span></span> | <ol><li><span data-ttu-id="421f9-300">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-300">text</span></span></li><li><span data-ttu-id="421f9-301">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-301">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="421f9-302">事前に書式設定されたテキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-302">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="421f9-303">blockquote</span><span class="sxs-lookup"><span data-stu-id="421f9-303">blockquote</span></span> | <blockquote><span data-ttu-id="421f9-304">テキスト</span><span class="sxs-lookup"><span data-stu-id="421f9-304">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="421f9-305">hyperlink</span><span class="sxs-lookup"><span data-stu-id="421f9-305">hyperlink</span></span> | [<span data-ttu-id="421f9-306">Bing</span><span class="sxs-lookup"><span data-stu-id="421f9-306">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="421f9-307">画像リンク</span><span class="sxs-lookup"><span data-stu-id="421f9-307">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="421f9-308">単純なカードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="421f9-308">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="421f9-309">デスクトップ プラットフォームとモバイル プラットフォームの解像度の違いにより、デスクトップとモバイル バージョンの Teams では書式設定が異なります。</span><span class="sxs-lookup"><span data-stu-id="421f9-309">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="421f9-310">デスクトップでは、HTML の書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-310">On the desktop, HTML formatting appears like this:</span></span>

![デスクトップ クライアントの HTML 書式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="421f9-312">iOS では、HTML 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-312">On iOS, HTML formatting appears like this:</span></span>

![iOS クライアントの HTML 書式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="421f9-314">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="421f9-314">Issues:</span></span>

* <span data-ttu-id="421f9-315">太字や斜体のような文字の書式設定は、iOS ではレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="421f9-315">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="421f9-316">Android では、HTML の書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-316">On Android, HTML formatting appears like this:</span></span>

![Android クライアントでの HTML 書式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="421f9-318">Android では太字や斜体のような文字の書式設定が正しく表示されます。</span><span class="sxs-lookup"><span data-stu-id="421f9-318">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="421f9-319">単純なカードの HTML 書式の書式設定サンプル</span><span class="sxs-lookup"><span data-stu-id="421f9-319">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="421f9-320">これらのスクリーンショットは Teams AppStudio を使用して作成され、ヒーロー カードの text プロパティは次の文字列に設定されています。</span><span class="sxs-lookup"><span data-stu-id="421f9-320">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="421f9-321">このコードを変更することで、独自のカードの書式設定をテストできます。</span><span class="sxs-lookup"><span data-stu-id="421f9-321">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
