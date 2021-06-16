---
title: カード内のテキストの書式設定
description: カードテキストの書式設定について説明Microsoft Teams
keywords: teams ボット カードの形式
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 6a420ca549cd5131afc50813b5c8267f28073e5b
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949764"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="d6c53-104">カードの書式を設定Teams</span><span class="sxs-lookup"><span data-stu-id="d6c53-104">Format cards in Teams</span></span>

<span data-ttu-id="d6c53-105">カードの種類に応じて、Markdown または HTML を使用してリッチ テキスト書式をカードに追加できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="d6c53-106">カードは、タイトルプロパティや字幕プロパティではなく、text プロパティでのみ書式設定をサポートします。</span><span class="sxs-lookup"><span data-stu-id="d6c53-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="d6c53-107">書式設定は、カードの種類に応じて XML (HTML) 書式のサブセットまたは Markdown を使用して指定できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="d6c53-108">現在および将来の開発では、Markdown 書式設定を使用したアダプティブ カードをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d6c53-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="d6c53-109">書式設定のサポートはカードの種類によって異なります。また、カードのレンダリングはデスクトップ クライアントとモバイル Teams クライアント、およびデスクトップ ブラウザーの Teams によって若干異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="d6c53-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="d6c53-110">インライン イメージは、任意のカードにTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="d6c53-111">イメージは、、、またはファイルとして書式設定され  `.png` `.jpg` `.gif` 、1024 px または 1 MB を超え×する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d6c53-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="d6c53-112">アニメーション GIF は公式にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="d6c53-113">詳細については、「カードリファレンス [」を参照してください](./cards-reference.md#inline-card-images)。</span><span class="sxs-lookup"><span data-stu-id="d6c53-113">For more information, see [Cards reference](./cards-reference.md#inline-card-images).</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="d6c53-114">Markdown を使用したカードの書式設定</span><span class="sxs-lookup"><span data-stu-id="d6c53-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="d6c53-115">Markdown をサポートするカードの種類は次の 2 Teams。</span><span class="sxs-lookup"><span data-stu-id="d6c53-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d6c53-116">**アダプティブ カード**: Markdown はアダプティブ カード フィールドおよび . `Textblock` `Fact.Title` `Fact.Value`</span><span class="sxs-lookup"><span data-stu-id="d6c53-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="d6c53-117">アダプティブ カードでは HTML はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="d6c53-118">**O365 コネクタ カード**: マークダウンと制限付き HTML は、テキスト フィールドOffice 365コネクタ カードでサポートされます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="d6c53-119">**Markdown の書式設定: アダプティブ カード**</span><span class="sxs-lookup"><span data-stu-id="d6c53-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="d6c53-120">サポートされているスタイルは `Textblock` 、次 `Fact.Title` `Fact.Value` のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d6c53-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="d6c53-121">Style</span><span class="sxs-lookup"><span data-stu-id="d6c53-121">Style</span></span> | <span data-ttu-id="d6c53-122">例</span><span class="sxs-lookup"><span data-stu-id="d6c53-122">Example</span></span> | <span data-ttu-id="d6c53-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="d6c53-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6c53-124">bold</span><span class="sxs-lookup"><span data-stu-id="d6c53-124">bold</span></span> | <span data-ttu-id="d6c53-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="d6c53-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="d6c53-126">italic</span><span class="sxs-lookup"><span data-stu-id="d6c53-126">italic</span></span> | <span data-ttu-id="d6c53-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="d6c53-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="d6c53-128">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-128">unordered list</span></span> | <ul><li><span data-ttu-id="d6c53-129">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-129">text</span></span></li><li><span data-ttu-id="d6c53-130">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="d6c53-131">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-131">ordered list</span></span> | <ol><li><span data-ttu-id="d6c53-132">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-132">text</span></span></li><li><span data-ttu-id="d6c53-133">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="d6c53-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="d6c53-134">Hyperlinks</span></span> |[<span data-ttu-id="d6c53-135">Bing</span><span class="sxs-lookup"><span data-stu-id="d6c53-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="d6c53-136">次の Markdown タグはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="d6c53-137">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="d6c53-137">Headers</span></span>
* <span data-ttu-id="d6c53-138">テーブル</span><span class="sxs-lookup"><span data-stu-id="d6c53-138">Tables</span></span>
* <span data-ttu-id="d6c53-139">画像</span><span class="sxs-lookup"><span data-stu-id="d6c53-139">Images</span></span>
* <span data-ttu-id="d6c53-140">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-140">Preformatted text</span></span>
* <span data-ttu-id="d6c53-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="d6c53-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6c53-142">アダプティブ カードは HTML の書式設定をサポートしていない。</span><span class="sxs-lookup"><span data-stu-id="d6c53-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="d6c53-143">アダプティブ カードの改行</span><span class="sxs-lookup"><span data-stu-id="d6c53-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="d6c53-144">リストでは、改行に対 `\r` してエスケープ シーケンス `\n` またはエスケープ シーケンスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="d6c53-145">リスト `\n\n` で使用すると、リスト内の次の要素がインデントされます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="d6c53-146">テキスト ブロック内の他の場所に改行が必要な場合は、 を使用します `\n\n` 。</span><span class="sxs-lookup"><span data-stu-id="d6c53-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="d6c53-147">アダプティブ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="d6c53-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="d6c53-148">書式設定は、デスクトップとモバイル バージョンの間で少し異Teams。</span><span class="sxs-lookup"><span data-stu-id="d6c53-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="d6c53-149">デスクトップでは、アダプティブ カード Markdown の書式設定は、Web ブラウザーとクライアント アプリケーションの両方で次Teams表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![デスクトップ クライアントでのアダプティブ カードマークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="d6c53-151">iOS では、アダプティブ カードのマークダウンの書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![iOS でのアダプティブ カードマークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="d6c53-153">Android では、アダプティブ カード マークダウンの書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Android のアダプティブ カード Markdown 書式設定](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="d6c53-155">アダプティブ カードの詳細</span><span class="sxs-lookup"><span data-stu-id="d6c53-155">More information on Adaptive cards</span></span>

<span data-ttu-id="d6c53-156">[アダプティブ カードのテキスト機能](/adaptive-cards/create/textfeatures)このトピックで説明する日付とローカライズ機能は、このトピックではTeams。</span><span class="sxs-lookup"><span data-stu-id="d6c53-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="d6c53-157">アダプティブ カードの書式設定サンプル</span><span class="sxs-lookup"><span data-stu-id="d6c53-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="d6c53-158">アダプティブ カード v1.2 内でのサポートのメンション</span><span class="sxs-lookup"><span data-stu-id="d6c53-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="d6c53-159">カード ベースのメンションは、Web、デスクトップ、モバイル クライアントでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d6c53-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="d6c53-160">ボットおよびメッセージング拡張機能の応答に対して、アダプティブ カード本文内に @ メンションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="d6c53-161">カードに @ メンションを追加するには、チャネルとグループ チャットの会話でメッセージ ベースのメンションと同じ通知ロジックとレンダリングに [従います](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)。</span><span class="sxs-lookup"><span data-stu-id="d6c53-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="d6c53-162">ボットとメッセージング拡張機能には [、TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 要素と FactSet 要素のカード コンテンツ内にメンション [を含](https://adaptivecards.io/explorer/FactSet.html) めることはできません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="d6c53-163">[メディア要素](https://adaptivecards.io/explorer/Media.html)は、現在、プラットフォーム上のアダプティブ カード v1.2 ではTeamsされていません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="d6c53-164">チャネル &チームのメンションはボット メッセージではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="d6c53-165">メンションの作成</span><span class="sxs-lookup"><span data-stu-id="d6c53-165">Constructing mentions</span></span>

<span data-ttu-id="d6c53-166">アダプティブ カードにメンションを含めるには、アプリに次の要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d6c53-166">To include a mention in an Adaptive Card your app needs to include the following elements:</span></span>

* <span data-ttu-id="d6c53-167">`<at>username</at>` は、サポートされているアダプティブ カード要素に含まれます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-167">`<at>username</at>` in the supported Adaptive card elements.</span></span>
* <span data-ttu-id="d6c53-168">カード コンテンツ内のプロパティ内のオブジェクトで、このオブジェクトには、Teams `mention` `msteams` のユーザー ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned.</span></span>
* <span data-ttu-id="d6c53-169">これは `userId` 、ボット ID と特定のユーザーに固有です。</span><span class="sxs-lookup"><span data-stu-id="d6c53-169">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="d6c53-170">特定のユーザーを@mention使用できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-170">It can be used to @mention a particular user.</span></span> <span data-ttu-id="d6c53-171">ユーザー `userId` ID の取得に記載されているオプションのいずれかを使用して [取得できます](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)。</span><span class="sxs-lookup"><span data-stu-id="d6c53-171">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="d6c53-172">メンション付きアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="d6c53-172">Sample Adaptive card with a mention</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="d6c53-173">アダプティブ カードの情報マスキング</span><span class="sxs-lookup"><span data-stu-id="d6c53-173">Information masking in Adaptive cards</span></span>
<span data-ttu-id="d6c53-174">Information masking プロパティを使用して、アダプティブ カード入力要素内のユーザーからのパスワードや機密情報などの特定の情報を [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) マスクします。</span><span class="sxs-lookup"><span data-stu-id="d6c53-174">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="d6c53-175">この機能はクライアント側の情報マスキングのみをサポートします。マスクされた入力テキストは、ボットの構成中に指定された https エンドポイント アドレスにクリア テキスト [として送信されます](../../build-your-first-app/build-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="d6c53-175">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="d6c53-176">information masking プロパティは現在、開発者プレビューでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-176">The information masking property is currently available in the developer preview only.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="d6c53-177">マスキング プロパティを持つアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="d6c53-177">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

<span data-ttu-id="d6c53-178">次の図は、アダプティブ カードのマスキング情報の例です。</span><span class="sxs-lookup"><span data-stu-id="d6c53-178">The following image is an example of masking information in Adaptive cards:</span></span>

![マスキング情報イメージ](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="d6c53-180">全幅アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="d6c53-180">Full width Adaptive card</span></span>
<span data-ttu-id="d6c53-181">このプロパティを使用 `msteams` すると、アダプティブ カードの幅を拡大し、追加のキャンバス領域を利用できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-181">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="d6c53-182">プロパティの使用方法については、次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d6c53-182">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="d6c53-183">全幅カードの作成</span><span class="sxs-lookup"><span data-stu-id="d6c53-183">Constructing full width cards</span></span>
<span data-ttu-id="d6c53-184">全幅アダプティブ カードを作成するには、 `width` カード コンテンツのプロパティのオブジェクトをに `msteams` 設定する必要があります `Full` 。</span><span class="sxs-lookup"><span data-stu-id="d6c53-184">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="d6c53-185">さらに、アプリには次の要素が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d6c53-185">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="d6c53-186">全幅のアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="d6c53-186">Sample adaptive card with full width</span></span>

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

<span data-ttu-id="d6c53-187">全幅アダプティブ カードは、次のように表示されます。 ![ 全幅アダプティブ カード ビュー](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="d6c53-187">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="d6c53-188">プロパティを Full に設定していない場合、アダプティブ カードの既定のビューは次のように `width` 表示されます。小幅アダプティブカード ![ ビュー](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="d6c53-188">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card appears as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="d6c53-189">Typeahead のサポート</span><span class="sxs-lookup"><span data-stu-id="d6c53-189">Typeahead support</span></span>

<span data-ttu-id="d6c53-190">schema 要素内で、ユーザーにフィルター処理を求め、多数の選択肢を選択すると、タスクの完了が大幅 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) に遅くなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d6c53-190">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="d6c53-191">アダプティブ カード内の Typeahead サポートは、ユーザーが入力を入力する場合に入力の選択肢のセットを絞り込むかフィルター処理することで、入力の選択を簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-191">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="d6c53-192">アダプティブ カードで typeahead を有効にする</span><span class="sxs-lookup"><span data-stu-id="d6c53-192">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="d6c53-193">セット内で typeahead を有効 `Input.Choiceset` にし `style` 、 `filtered` 必ずに `isMultiSelect` に設定します `false` 。</span><span class="sxs-lookup"><span data-stu-id="d6c53-193">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="d6c53-194">typeahead サポートを備えるアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="d6c53-194">Sample adaptive card with typeahead support</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="d6c53-195">アダプティブ カードの画像のステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="d6c53-195">Stage view for images in Adaptive Cards</span></span>

<span data-ttu-id="d6c53-196">アダプティブ カードでは、このプロパティを使用して、ステージ ビューに画像を選択的 `msteams` に表示する機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-196">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="d6c53-197">ユーザーが画像にカーソルを合わせると、展開アイコンが表示され、属性が `allowExpand` に設定されます `true` 。</span><span class="sxs-lookup"><span data-stu-id="d6c53-197">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="d6c53-198">プロパティの使用方法については、次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d6c53-198">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="d6c53-199">ユーザーが画像の上にマウス ポインターを置くと、画像の右上隅に展開アイコンが表示されます。展開可能なイメージを持つ ![ アダプティブ カード](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="d6c53-199">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="d6c53-200">ユーザーが展開ボタンを選択すると、イメージがステージ ビューに表示されます。 ![ イメージはステージ ビューに展開されます。](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="d6c53-200">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="d6c53-201">ステージ ビューでは、ユーザーは画像を拡大および縮小できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-201">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="d6c53-202">アダプティブ カードでこの機能を使用する必要があるイメージを選択できます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-202">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="d6c53-203">拡大および縮小機能は、アダプティブ カード内のイメージ要素 (画像の種類) にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-203">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="d6c53-204">Teams モバイル アプリの場合、アダプティブ カードの画像のステージ ビュー機能は既定で利用できます。ユーザーは、属性が存在するかどうかに関係なく、画像をタップするだけでステージ ビューでアダプティブ カードイメージを表示できます。 `allowExpand`</span><span class="sxs-lookup"><span data-stu-id="d6c53-204">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="d6c53-205">**Markdown の書式設定: O365 コネクタ カード**</span><span class="sxs-lookup"><span data-stu-id="d6c53-205">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="d6c53-206">コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。</span><span class="sxs-lookup"><span data-stu-id="d6c53-206">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="d6c53-207">HTML サポートについては、最後のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="d6c53-207">HTML support is described in the last section.</span></span>

| <span data-ttu-id="d6c53-208">Style</span><span class="sxs-lookup"><span data-stu-id="d6c53-208">Style</span></span> | <span data-ttu-id="d6c53-209">例</span><span class="sxs-lookup"><span data-stu-id="d6c53-209">Example</span></span> | <span data-ttu-id="d6c53-210">Markdown</span><span class="sxs-lookup"><span data-stu-id="d6c53-210">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6c53-211">bold</span><span class="sxs-lookup"><span data-stu-id="d6c53-211">bold</span></span> | <span data-ttu-id="d6c53-212">**text**</span><span class="sxs-lookup"><span data-stu-id="d6c53-212">**text**</span></span> | `**text**` |
| <span data-ttu-id="d6c53-213">italic</span><span class="sxs-lookup"><span data-stu-id="d6c53-213">italic</span></span> | <span data-ttu-id="d6c53-214">*text*</span><span class="sxs-lookup"><span data-stu-id="d6c53-214">*text*</span></span> | `*text*` |
| <span data-ttu-id="d6c53-215">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="d6c53-215">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="d6c53-216">**Text**</span><span class="sxs-lookup"><span data-stu-id="d6c53-216">**Text**</span></span> | `### Text`|
| <span data-ttu-id="d6c53-217">取り消し線</span><span class="sxs-lookup"><span data-stu-id="d6c53-217">strikethrough</span></span> | <span data-ttu-id="d6c53-218">~~text~~</span><span class="sxs-lookup"><span data-stu-id="d6c53-218">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="d6c53-219">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-219">unordered list</span></span> | <ul><li><span data-ttu-id="d6c53-220">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-220">text</span></span></li><li><span data-ttu-id="d6c53-221">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-221">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="d6c53-222">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-222">ordered list</span></span> | <ol><li><span data-ttu-id="d6c53-223">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-223">text</span></span></li><li><span data-ttu-id="d6c53-224">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-224">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="d6c53-225">事前に書式設定されたテキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-225">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="d6c53-226">blockquote</span><span class="sxs-lookup"><span data-stu-id="d6c53-226">blockquote</span></span> | <span data-ttu-id="d6c53-227">>をブロッククォートする</span><span class="sxs-lookup"><span data-stu-id="d6c53-227">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="d6c53-228">hyperlink</span><span class="sxs-lookup"><span data-stu-id="d6c53-228">hyperlink</span></span> | [<span data-ttu-id="d6c53-229">Bing</span><span class="sxs-lookup"><span data-stu-id="d6c53-229">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="d6c53-230">画像リンク</span><span class="sxs-lookup"><span data-stu-id="d6c53-230">image link</span></span> |![岩の上のアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="d6c53-232">コネクタ カードでは、改行はのためにレンダリングされますが `\n\n` 、for または `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="d6c53-232">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="d6c53-233">Markdown を使用したコネクタ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="d6c53-233">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="d6c53-234">デスクトップでは、コネクタ カードの Markdown 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-234">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![デスクトップ クライアントでのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="d6c53-236">iOS では、コネクタ カードの Markdown 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-236">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![iOS クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="d6c53-238">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="d6c53-238">Issues:</span></span>

* <span data-ttu-id="d6c53-239">コネクタ カードの iOS クライアントTeams、Markdown または HTML インライン イメージはレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-239">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="d6c53-240">ブロッククォートはインデントされますが、灰色の背景なしでレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-240">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="d6c53-241">Android では、コネクタ カードの Markdown 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-241">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="d6c53-243">Markdown コネクタ カードの書式設定の例</span><span class="sxs-lookup"><span data-stu-id="d6c53-243">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="d6c53-244">HTML を使用したカードの書式設定</span><span class="sxs-lookup"><span data-stu-id="d6c53-244">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="d6c53-245">**HTML の書式設定: O365 コネクタ カード**</span><span class="sxs-lookup"><span data-stu-id="d6c53-245">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="d6c53-246">コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。</span><span class="sxs-lookup"><span data-stu-id="d6c53-246">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="d6c53-247">マークダウンについては、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="d6c53-247">Markdown is described in the next section.</span></span>

| <span data-ttu-id="d6c53-248">Style</span><span class="sxs-lookup"><span data-stu-id="d6c53-248">Style</span></span> | <span data-ttu-id="d6c53-249">例</span><span class="sxs-lookup"><span data-stu-id="d6c53-249">Example</span></span> | <span data-ttu-id="d6c53-250">HTML</span><span class="sxs-lookup"><span data-stu-id="d6c53-250">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6c53-251">bold</span><span class="sxs-lookup"><span data-stu-id="d6c53-251">bold</span></span> | <span data-ttu-id="d6c53-252">**text**</span><span class="sxs-lookup"><span data-stu-id="d6c53-252">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="d6c53-253">italic</span><span class="sxs-lookup"><span data-stu-id="d6c53-253">italic</span></span> | <span data-ttu-id="d6c53-254">*text*</span><span class="sxs-lookup"><span data-stu-id="d6c53-254">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="d6c53-255">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="d6c53-255">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="d6c53-256">**Text**</span><span class="sxs-lookup"><span data-stu-id="d6c53-256">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="d6c53-257">取り消し線</span><span class="sxs-lookup"><span data-stu-id="d6c53-257">strikethrough</span></span> | <span data-ttu-id="d6c53-258">~~text~~</span><span class="sxs-lookup"><span data-stu-id="d6c53-258">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="d6c53-259">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-259">unordered list</span></span> | <ul><li><span data-ttu-id="d6c53-260">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-260">text</span></span></li><li><span data-ttu-id="d6c53-261">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-261">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="d6c53-262">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-262">ordered list</span></span> | <ol><li><span data-ttu-id="d6c53-263">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-263">text</span></span></li><li><span data-ttu-id="d6c53-264">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-264">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="d6c53-265">事前に書式設定されたテキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-265">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="d6c53-266">blockquote</span><span class="sxs-lookup"><span data-stu-id="d6c53-266">blockquote</span></span> | <blockquote><span data-ttu-id="d6c53-267">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-267">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="d6c53-268">hyperlink</span><span class="sxs-lookup"><span data-stu-id="d6c53-268">hyperlink</span></span> | [<span data-ttu-id="d6c53-269">Bing</span><span class="sxs-lookup"><span data-stu-id="d6c53-269">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="d6c53-270">画像リンク</span><span class="sxs-lookup"><span data-stu-id="d6c53-270">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="d6c53-271">コネクタ カードでは、タグを使用して改行が HTML でレンダリング `<p>` されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-271">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="d6c53-272">HTML を使用したコネクタ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="d6c53-272">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="d6c53-273">デスクトップでは、コネクタ カードの HTML 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-273">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![デスクトップ クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="d6c53-275">iOS では、HTML の書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-275">On iOS, HTML formatting looks like this:</span></span>

![iOS クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="d6c53-277">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="d6c53-277">Issues:</span></span>

* <span data-ttu-id="d6c53-278">インライン イメージは、コネクタ カードの Markdown または HTML を使用して iOS ではレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-278">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="d6c53-279">書式設定済みのテキストはレンダリングされますが、背景が灰色ではありません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-279">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="d6c53-280">Android では、HTML の書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-280">On Android, HTML formatting looks like this:</span></span>

![Android クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="d6c53-282">HTML コネクタ カードの書式設定サンプル</span><span class="sxs-lookup"><span data-stu-id="d6c53-282">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="d6c53-283">**HTML の書式設定: ヒーローカードとサムネイル カード**</span><span class="sxs-lookup"><span data-stu-id="d6c53-283">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="d6c53-284">HTML タグは、ヒーロー カードやサムネイル カードなどの単純なカードでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d6c53-284">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="d6c53-285">Markdown はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-285">Markdown is not supported.</span></span>

| <span data-ttu-id="d6c53-286">Style</span><span class="sxs-lookup"><span data-stu-id="d6c53-286">Style</span></span> | <span data-ttu-id="d6c53-287">例</span><span class="sxs-lookup"><span data-stu-id="d6c53-287">Example</span></span> | <span data-ttu-id="d6c53-288">HTML</span><span class="sxs-lookup"><span data-stu-id="d6c53-288">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6c53-289">bold</span><span class="sxs-lookup"><span data-stu-id="d6c53-289">bold</span></span> | <span data-ttu-id="d6c53-290">**text**</span><span class="sxs-lookup"><span data-stu-id="d6c53-290">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="d6c53-291">italic</span><span class="sxs-lookup"><span data-stu-id="d6c53-291">italic</span></span> | <span data-ttu-id="d6c53-292">*text*</span><span class="sxs-lookup"><span data-stu-id="d6c53-292">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="d6c53-293">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="d6c53-293">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="d6c53-294">**Text**</span><span class="sxs-lookup"><span data-stu-id="d6c53-294">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="d6c53-295">取り消し線</span><span class="sxs-lookup"><span data-stu-id="d6c53-295">strikethrough</span></span> | <span data-ttu-id="d6c53-296">~~text~~</span><span class="sxs-lookup"><span data-stu-id="d6c53-296">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="d6c53-297">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-297">unordered list</span></span> | <ul><li><span data-ttu-id="d6c53-298">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-298">text</span></span></li><li><span data-ttu-id="d6c53-299">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-299">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="d6c53-300">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-300">ordered list</span></span> | <ol><li><span data-ttu-id="d6c53-301">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-301">text</span></span></li><li><span data-ttu-id="d6c53-302">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-302">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="d6c53-303">事前に書式設定されたテキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-303">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="d6c53-304">blockquote</span><span class="sxs-lookup"><span data-stu-id="d6c53-304">blockquote</span></span> | <blockquote><span data-ttu-id="d6c53-305">テキスト</span><span class="sxs-lookup"><span data-stu-id="d6c53-305">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="d6c53-306">hyperlink</span><span class="sxs-lookup"><span data-stu-id="d6c53-306">hyperlink</span></span> | [<span data-ttu-id="d6c53-307">Bing</span><span class="sxs-lookup"><span data-stu-id="d6c53-307">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="d6c53-308">画像リンク</span><span class="sxs-lookup"><span data-stu-id="d6c53-308">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="d6c53-309">単純なカードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="d6c53-309">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="d6c53-310">デスクトップ プラットフォームとモバイル プラットフォームの解像度の違いにより、デスクトップとモバイル バージョンの間で書式設定が異Teams。</span><span class="sxs-lookup"><span data-stu-id="d6c53-310">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="d6c53-311">デスクトップでは、HTML の書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-311">On the desktop, HTML formatting appears like this:</span></span>

![デスクトップ クライアントの HTML 書式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="d6c53-313">iOS では、HTML 書式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-313">On iOS, HTML formatting appears like this:</span></span>

![iOS クライアントの HTML 書式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="d6c53-315">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="d6c53-315">Issues:</span></span>

* <span data-ttu-id="d6c53-316">太字や斜体のような文字の書式設定は、iOS ではレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="d6c53-316">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="d6c53-317">Android では、HTML の書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-317">On Android, HTML formatting appears like this:</span></span>

![Android クライアントでの HTML 書式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="d6c53-319">Android では太字や斜体のような文字の書式設定が正しく表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-319">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="d6c53-320">単純なカードの HTML 書式の書式設定サンプル</span><span class="sxs-lookup"><span data-stu-id="d6c53-320">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="d6c53-321">これらのスクリーンショットは、Teams AppStudio を使用して作成され、ヒーロー カードの text プロパティは次の文字列に設定されています。</span><span class="sxs-lookup"><span data-stu-id="d6c53-321">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="d6c53-322">このコードを変更することで、独自のカードの書式設定をテストできます。</span><span class="sxs-lookup"><span data-stu-id="d6c53-322">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
