---
title: カード内のテキストの書式設定
description: Microsoft Teamsでのカード テキストの書式設定について説明します。
keywords: チームボットカード形式
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 848656097f2c865705cc0d91dece93049d8c6790
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566584"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="2a764-104">Teamsでカードをフォーマットする</span><span class="sxs-lookup"><span data-stu-id="2a764-104">Format cards in Teams</span></span>

<span data-ttu-id="2a764-105">カードの種類に応じて、マークダウンまたは HTML を使用して、リッチ テキスト形式を追加できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="2a764-106">カードは、タイトルやサブタイトルのプロパティではなく、text プロパティの書式設定のみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="2a764-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="2a764-107">フォーマットは、XML (HTML) フォーマットのサブセットを使用して指定することも、カードの種類に応じてマークダウンすることもできます。</span><span class="sxs-lookup"><span data-stu-id="2a764-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="2a764-108">現在および将来の開発のためにマークダウンフォーマットを使用してアダプティブカードをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2a764-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="2a764-109">フォーマットのサポートはカードの種類によって異なり、カードのレンダリングはデスクトップとモバイル Teamsクライアントの間で若干異なる場合があり、デスクトップ ブラウザーでTeamsします。</span><span class="sxs-lookup"><span data-stu-id="2a764-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="2a764-110">インライン画像は、任意のTeamsカードに含めることができます。</span><span class="sxs-lookup"><span data-stu-id="2a764-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="2a764-111">イメージは、 、または ファイルとしてフォーマットされ  `.png` `.jpg` `.gif` 、1024 × 1024 px または 1 MB を超えてはなりません。</span><span class="sxs-lookup"><span data-stu-id="2a764-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="2a764-112">アニメーション GIF は正式にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2a764-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="2a764-113">詳細については、 [カードリファレンス](./cards-reference.md#inline-card-images)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2a764-113">For more information, see [Cards reference](./cards-reference.md#inline-card-images).</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="2a764-114">マークダウンを使用したカードのフォーマット</span><span class="sxs-lookup"><span data-stu-id="2a764-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="2a764-115">Teamsでマークダウンをサポートするカードタイプは2つあります。</span><span class="sxs-lookup"><span data-stu-id="2a764-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2a764-116">**アダプティブカード**: マークダウンはアダプティブカード `Textblock` フィールドおよび `Fact.Title` `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="2a764-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="2a764-117">アダプティブ カードでは、HTML はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2a764-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="2a764-118">**O365 コネクタ カード**: マークダウンと制限付き HTML は、テキスト フィールドのコネクタ カードOffice 365でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="2a764-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="2a764-119">**マークダウンのフォーマット: アダプティブカード**</span><span class="sxs-lookup"><span data-stu-id="2a764-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="2a764-120">でサポートされているスタイル `Textblock` `Fact.Title` は `Fact.Value` 、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2a764-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="2a764-121">Style</span><span class="sxs-lookup"><span data-stu-id="2a764-121">Style</span></span> | <span data-ttu-id="2a764-122">例</span><span class="sxs-lookup"><span data-stu-id="2a764-122">Example</span></span> | <span data-ttu-id="2a764-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="2a764-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a764-124">bold</span><span class="sxs-lookup"><span data-stu-id="2a764-124">bold</span></span> | <span data-ttu-id="2a764-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="2a764-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="2a764-126">italic</span><span class="sxs-lookup"><span data-stu-id="2a764-126">italic</span></span> | <span data-ttu-id="2a764-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="2a764-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="2a764-128">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="2a764-128">unordered list</span></span> | <ul><li><span data-ttu-id="2a764-129">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-129">text</span></span></li><li><span data-ttu-id="2a764-130">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="2a764-131">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="2a764-131">ordered list</span></span> | <ol><li><span data-ttu-id="2a764-132">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-132">text</span></span></li><li><span data-ttu-id="2a764-133">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="2a764-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="2a764-134">Hyperlinks</span></span> |[<span data-ttu-id="2a764-135">Bing</span><span class="sxs-lookup"><span data-stu-id="2a764-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="2a764-136">次のマークダウン タグはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2a764-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="2a764-137">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="2a764-137">Headers</span></span>
* <span data-ttu-id="2a764-138">テーブル</span><span class="sxs-lookup"><span data-stu-id="2a764-138">Tables</span></span>
* <span data-ttu-id="2a764-139">画像</span><span class="sxs-lookup"><span data-stu-id="2a764-139">Images</span></span>
* <span data-ttu-id="2a764-140">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-140">Preformatted text</span></span>
* <span data-ttu-id="2a764-141">ブロッククォート</span><span class="sxs-lookup"><span data-stu-id="2a764-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a764-142">アダプティブ カードは HTML 形式をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="2a764-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="2a764-143">アダプティブ カードの改行</span><span class="sxs-lookup"><span data-stu-id="2a764-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="2a764-144">リストでは、改行に対して、 `\r` または `\n` エスケープ シーケンスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="2a764-145">`\n\n`リスト内で使用すると、リスト内の次の要素がインデントされます。</span><span class="sxs-lookup"><span data-stu-id="2a764-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="2a764-146">テキストブロック内の他の場所に改行が必要な場合は、 `\n\n` を使用します。</span><span class="sxs-lookup"><span data-stu-id="2a764-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="2a764-147">アダプティブカードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="2a764-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="2a764-148">フォーマットは、デスクトップとモバイル版のTeamsの間で若干異なります。</span><span class="sxs-lookup"><span data-stu-id="2a764-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="2a764-149">デスクトップでは、アダプティブ カード マークダウンの書式設定は、Web ブラウザとTeams クライアント アプリケーションの両方で次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a764-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![デスクトップ クライアントでのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="2a764-151">iOS では、アダプティブ カード マークダウンの書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a764-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![iOS でのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="2a764-153">Android では、アダプティブ カード マークダウンの書式設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a764-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![アンドロイドでアダプティブカードマークダウンフォーマット](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="2a764-155">アダプティブカードの詳細</span><span class="sxs-lookup"><span data-stu-id="2a764-155">More information on Adaptive cards</span></span>

<span data-ttu-id="2a764-156">[アダプティブ カードのテキスト機能](/adaptive-cards/create/textfeatures)このトピックで説明する日付およびローカライズ機能は、Teamsではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2a764-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="2a764-157">アダプティブ カードの書式設定サンプル</span><span class="sxs-lookup"><span data-stu-id="2a764-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="2a764-158">アダプティブカードv1.2内でのサポートについて言及</span><span class="sxs-lookup"><span data-stu-id="2a764-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="2a764-159">カードベースのメンションは、ウェブ、デスクトップ、モバイルクライアントでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="2a764-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="2a764-160">ボットおよびメッセージング拡張機能の応答に対して、アダプティブ カード本体内に @ メンションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="2a764-161">カードに @ メンションを追加するには、 [チャネルやグループチャットの会話で](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)メッセージベースのメンションと同じ通知ロジックとレンダリングを実行します。</span><span class="sxs-lookup"><span data-stu-id="2a764-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="2a764-162">ボットとメッセージング拡張機能には [、TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 要素と [FactSet](https://adaptivecards.io/explorer/FactSet.html) 要素のカード コンテンツ内にメンションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="2a764-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="2a764-163">[メディア要素](https://adaptivecards.io/explorer/Media.html)は、現在、Teamsプラットフォームのアダプティブ カード v1.2 ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2a764-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="2a764-164">チャンネル & チームのメンションは、ボット メッセージではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2a764-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="2a764-165">メンションの構築</span><span class="sxs-lookup"><span data-stu-id="2a764-165">Constructing mentions</span></span>

<span data-ttu-id="2a764-166">アダプティブ カードにメンションを含めるには、アプリに次の要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a764-166">To include a mention in an Adaptive Card your app needs to include the following elements:</span></span>

* <span data-ttu-id="2a764-167">`<at>username</at>` サポートされているアダプティブ カード要素で</span><span class="sxs-lookup"><span data-stu-id="2a764-167">`<at>username</at>` in the supported Adaptive card elements.</span></span>
* <span data-ttu-id="2a764-168">`mention` `msteams` カード Teams コンテンツ内のプロパティ内のオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="2a764-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned.</span></span>
* <span data-ttu-id="2a764-169">`userId`は、ボット ID と特定のユーザーに固有です。</span><span class="sxs-lookup"><span data-stu-id="2a764-169">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="2a764-170">特定のユーザーを@mentionするために使用できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-170">It can be used to @mention a particular user.</span></span> <span data-ttu-id="2a764-171">`userId`ユーザー ID の[取得](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)に記載されているオプションの 1 つを使用して取得できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-171">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="2a764-172">言及付きのサンプルアダプティブカード</span><span class="sxs-lookup"><span data-stu-id="2a764-172">Sample Adaptive card with a mention</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="2a764-173">アダプティブカードでの情報マスキング</span><span class="sxs-lookup"><span data-stu-id="2a764-173">Information masking in Adaptive cards</span></span>
<span data-ttu-id="2a764-174">情報マスク プロパティを使用して、Adaptive カード入力要素内のユーザーからのパスワードや機密情報などの特定の情報をマスク [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) します。</span><span class="sxs-lookup"><span data-stu-id="2a764-174">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="2a764-175">この機能はクライアント側の情報マスキングのみをサポートし、マスクされた入力テキストは [、ボットの設定](../../build-your-first-app/build-bot.md)中に指定された https エンドポイントアドレスにクリアテキストで送信されます。</span><span class="sxs-lookup"><span data-stu-id="2a764-175">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="2a764-176">情報マスク プロパティは、現在、開発者プレビューでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-176">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="2a764-177">アダプティブ カードの情報をマスクするには、プロパティを `isMasked` **type** `Input.Text` に追加し、その値を *true* に設定します。</span><span class="sxs-lookup"><span data-stu-id="2a764-177">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="2a764-178">マスク プロパティを使用したサンプル アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="2a764-178">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="2a764-179">次の図は、アダプティブ カードのマスキング情報の例です。</span><span class="sxs-lookup"><span data-stu-id="2a764-179">The following image is an example of masking information in Adaptive cards:</span></span>

![マスキング情報画像](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="2a764-181">全幅アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="2a764-181">Full width Adaptive card</span></span>
<span data-ttu-id="2a764-182">`msteams`このプロパティを使用して、アダプティブ カードの幅を広げ、追加のキャンバススペースを利用できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-182">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="2a764-183">プロパティの使用方法については、次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2a764-183">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="2a764-184">全幅カードの作成</span><span class="sxs-lookup"><span data-stu-id="2a764-184">Constructing full width cards</span></span>
<span data-ttu-id="2a764-185">全幅アダプティブ カードを作成するには、 `width` `msteams` カード コンテンツのオブジェクトのプロパティを に設定する必要があります `Full` 。</span><span class="sxs-lookup"><span data-stu-id="2a764-185">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="2a764-186">また、アプリには次の要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a764-186">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="2a764-187">全幅のサンプルアダプティブカード</span><span class="sxs-lookup"><span data-stu-id="2a764-187">Sample adaptive card with full width</span></span>

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

<span data-ttu-id="2a764-188">全幅アダプティブ カードは次のように表示されます。 ![](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="2a764-188">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="2a764-189">プロパティを `width` *[完全]* に設定していない場合、アダプティブ カードの既定のビューは次のようになります。 ![](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="2a764-189">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="2a764-190">タイプ先行サポート</span><span class="sxs-lookup"><span data-stu-id="2a764-190">Typeahead support</span></span>

<span data-ttu-id="2a764-191">schema [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) 要素内で、ユーザーにフィルター処理を依頼し、多数の選択肢を選択すると、タスクの完了が大幅に遅くなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2a764-191">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="2a764-192">アダプティブカード内での Typeahead サポートは、ユーザーが入力を入力する際に入力選択肢のセットを絞り込んだりフィルタリングしたりすることで、入力の選択を簡素化できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-192">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="2a764-193">アダプティブ カードでの入力を有効にする</span><span class="sxs-lookup"><span data-stu-id="2a764-193">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="2a764-194">に設定されている typeahead を有効に `Input.Choiceset` `style` `filtered` し、確実 `isMultiSelect` に `false` に設定するには</span><span class="sxs-lookup"><span data-stu-id="2a764-194">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="2a764-195">タイプ先行サポートを備えたサンプルアダプティブカード</span><span class="sxs-lookup"><span data-stu-id="2a764-195">Sample adaptive card with typeahead support</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="2a764-196">アダプティブカード内の画像のステージビュー</span><span class="sxs-lookup"><span data-stu-id="2a764-196">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="2a764-197">この機能は、現在、開発者プレビューでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-197">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="2a764-198">Adaptive カードでは、このプロパティを使用 `msteams` して、ステージ ビューでイメージを選択的に表示する機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-198">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="2a764-199">ユーザーが画像の上にマウスを置くと、展開アイコンが表示され、属性 `allowExpand` が に設定されます `true` 。</span><span class="sxs-lookup"><span data-stu-id="2a764-199">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="2a764-200">プロパティの使用方法については、次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2a764-200">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="2a764-201">ユーザーが画像の上にマウスを移動すると、画像の右上隅に展開アイコンが表示されます: ![ 展開可能な画像を持つアダプティブ カード](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="2a764-201">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="2a764-202">ユーザーが展開ボタンを選択すると、画像がステージビューに表示されます: ![ 画像はステージビューに展開されます。](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="2a764-202">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="2a764-203">ステージビューでは、ユーザーは画像を拡大表示したりズームアウトしたりできます。</span><span class="sxs-lookup"><span data-stu-id="2a764-203">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="2a764-204">アダプティブ カード内の画像にこの機能を適用する必要がある画像を選択できます。</span><span class="sxs-lookup"><span data-stu-id="2a764-204">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="2a764-205">拡大/縮小機能は、アダプティブ カードのイメージ エレメント(イメージ タイプ)にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="2a764-205">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="2a764-206">Teamsモバイルアプリでは、アダプティブカードの画像のステージビュー機能はデフォルトで利用可能であり、ユーザーはアトリビュートが存在するかどうかに関係なく、画像をタップするだけで、ステージビューでアダプティブカード画像を表示できます `allowExpand` 。</span><span class="sxs-lookup"><span data-stu-id="2a764-206">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="2a764-207">**マークダウンのフォーマット: O365 コネクタ カード**</span><span class="sxs-lookup"><span data-stu-id="2a764-207">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="2a764-208">コネクタ カードは、限定的なマークダウンおよび HTML 形式をサポートします。</span><span class="sxs-lookup"><span data-stu-id="2a764-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="2a764-209">HTML サポートについては、最後のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="2a764-209">HTML support is described in the last section.</span></span>

| <span data-ttu-id="2a764-210">Style</span><span class="sxs-lookup"><span data-stu-id="2a764-210">Style</span></span> | <span data-ttu-id="2a764-211">例</span><span class="sxs-lookup"><span data-stu-id="2a764-211">Example</span></span> | <span data-ttu-id="2a764-212">Markdown</span><span class="sxs-lookup"><span data-stu-id="2a764-212">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a764-213">bold</span><span class="sxs-lookup"><span data-stu-id="2a764-213">bold</span></span> | <span data-ttu-id="2a764-214">**text**</span><span class="sxs-lookup"><span data-stu-id="2a764-214">**text**</span></span> | `**text**` |
| <span data-ttu-id="2a764-215">italic</span><span class="sxs-lookup"><span data-stu-id="2a764-215">italic</span></span> | <span data-ttu-id="2a764-216">*text*</span><span class="sxs-lookup"><span data-stu-id="2a764-216">*text*</span></span> | `*text*` |
| <span data-ttu-id="2a764-217">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="2a764-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="2a764-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="2a764-218">**Text**</span></span> | `### Text`|
| <span data-ttu-id="2a764-219">取り消し線</span><span class="sxs-lookup"><span data-stu-id="2a764-219">strikethrough</span></span> | <span data-ttu-id="2a764-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="2a764-220">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="2a764-221">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="2a764-221">unordered list</span></span> | <ul><li><span data-ttu-id="2a764-222">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-222">text</span></span></li><li><span data-ttu-id="2a764-223">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-223">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="2a764-224">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="2a764-224">ordered list</span></span> | <ol><li><span data-ttu-id="2a764-225">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-225">text</span></span></li><li><span data-ttu-id="2a764-226">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-226">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="2a764-227">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-227">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="2a764-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="2a764-228">blockquote</span></span> | <span data-ttu-id="2a764-229">>ブロッククォートテキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-229">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="2a764-230">hyperlink</span><span class="sxs-lookup"><span data-stu-id="2a764-230">hyperlink</span></span> | [<span data-ttu-id="2a764-231">Bing</span><span class="sxs-lookup"><span data-stu-id="2a764-231">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="2a764-232">画像リンク</span><span class="sxs-lookup"><span data-stu-id="2a764-232">image link</span></span> |![岩の上のアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="2a764-234">コネクタ カードでは、改行線は に対してレンダリング `\n\n` されますが、 または にはレンダリングされません `\n` `\r` 。</span><span class="sxs-lookup"><span data-stu-id="2a764-234">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="2a764-235">マークダウンを使用したコネクタカードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="2a764-235">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="2a764-236">デスクトップでは、コネクタ カードのマークダウンの書式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2a764-236">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![デスクトップ クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="2a764-238">iOS では、コネクタ カードのマークダウンの書式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2a764-238">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![iOS クライアントのコネクタ カードのマークダウン形式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="2a764-240">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="2a764-240">Issues:</span></span>

* <span data-ttu-id="2a764-241">Teams用の iOS クライアントは、コネクタ カードにマークダウンまたは HTML インライン イメージをレンダリングしません。</span><span class="sxs-lookup"><span data-stu-id="2a764-241">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="2a764-242">ブロック引用符はインデントとしてレンダリングされますが、背景はグレーで表示されません。</span><span class="sxs-lookup"><span data-stu-id="2a764-242">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="2a764-243">Android では、コネクタ カードのマークダウンの書式設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2a764-243">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android クライアントのコネクタ カードのマークダウン形式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="2a764-245">マークダウン コネクタ カードの書式設定例</span><span class="sxs-lookup"><span data-stu-id="2a764-245">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="2a764-246">HTML を使用したカードの書式設定</span><span class="sxs-lookup"><span data-stu-id="2a764-246">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="2a764-247">**HTML 形式: O365 コネクタ カード**</span><span class="sxs-lookup"><span data-stu-id="2a764-247">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="2a764-248">コネクタ カードは、限定的なマークダウンおよび HTML 形式をサポートします。</span><span class="sxs-lookup"><span data-stu-id="2a764-248">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="2a764-249">マークダウンについては、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="2a764-249">Markdown is described in the next section.</span></span>

| <span data-ttu-id="2a764-250">Style</span><span class="sxs-lookup"><span data-stu-id="2a764-250">Style</span></span> | <span data-ttu-id="2a764-251">例</span><span class="sxs-lookup"><span data-stu-id="2a764-251">Example</span></span> | <span data-ttu-id="2a764-252">HTML</span><span class="sxs-lookup"><span data-stu-id="2a764-252">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a764-253">bold</span><span class="sxs-lookup"><span data-stu-id="2a764-253">bold</span></span> | <span data-ttu-id="2a764-254">**text**</span><span class="sxs-lookup"><span data-stu-id="2a764-254">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="2a764-255">italic</span><span class="sxs-lookup"><span data-stu-id="2a764-255">italic</span></span> | <span data-ttu-id="2a764-256">*text*</span><span class="sxs-lookup"><span data-stu-id="2a764-256">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="2a764-257">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="2a764-257">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="2a764-258">**Text**</span><span class="sxs-lookup"><span data-stu-id="2a764-258">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="2a764-259">取り消し線</span><span class="sxs-lookup"><span data-stu-id="2a764-259">strikethrough</span></span> | <span data-ttu-id="2a764-260">~~text~~</span><span class="sxs-lookup"><span data-stu-id="2a764-260">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="2a764-261">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="2a764-261">unordered list</span></span> | <ul><li><span data-ttu-id="2a764-262">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-262">text</span></span></li><li><span data-ttu-id="2a764-263">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-263">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="2a764-264">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="2a764-264">ordered list</span></span> | <ol><li><span data-ttu-id="2a764-265">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-265">text</span></span></li><li><span data-ttu-id="2a764-266">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-266">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="2a764-267">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-267">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="2a764-268">blockquote</span><span class="sxs-lookup"><span data-stu-id="2a764-268">blockquote</span></span> | <blockquote><span data-ttu-id="2a764-269">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-269">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="2a764-270">hyperlink</span><span class="sxs-lookup"><span data-stu-id="2a764-270">hyperlink</span></span> | [<span data-ttu-id="2a764-271">Bing</span><span class="sxs-lookup"><span data-stu-id="2a764-271">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="2a764-272">画像リンク</span><span class="sxs-lookup"><span data-stu-id="2a764-272">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="2a764-273">コネクタ カードでは、タグを使用して改行が HTML でレンダリングされます `<p>` 。</span><span class="sxs-lookup"><span data-stu-id="2a764-273">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="2a764-274">HTML を使用するコネクタ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="2a764-274">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="2a764-275">デスクトップでは、コネクタ カードの HTML 形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2a764-275">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![デスクトップ クライアントのコネクタ カードの HTML 形式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="2a764-277">iOS では、HTML 形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2a764-277">On iOS, HTML formatting looks like this:</span></span>

![iOS クライアントのコネクタ カードの HTML 形式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="2a764-279">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="2a764-279">Issues:</span></span>

* <span data-ttu-id="2a764-280">インライン イメージは、コネクタ カードでマークダウンまたは HTML を使用して iOS ではレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="2a764-280">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="2a764-281">書式設定済みのテキストはレンダリングされますが、背景は灰色ではありません。</span><span class="sxs-lookup"><span data-stu-id="2a764-281">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="2a764-282">Android では、HTML 形式は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2a764-282">On Android, HTML formatting looks like this:</span></span>

![Android クライアントのコネクタ カードの HTML 形式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="2a764-284">HTML コネクタ カードの書式設定サンプル</span><span class="sxs-lookup"><span data-stu-id="2a764-284">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="2a764-285">**HTML フォーマット: ヒーローカードとサムネイルカード**</span><span class="sxs-lookup"><span data-stu-id="2a764-285">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="2a764-286">HTML タグは、ヒーロー カードやサムネイル カードなどの単純なカードでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="2a764-286">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="2a764-287">マークダウンはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2a764-287">Markdown is not supported.</span></span>

| <span data-ttu-id="2a764-288">Style</span><span class="sxs-lookup"><span data-stu-id="2a764-288">Style</span></span> | <span data-ttu-id="2a764-289">例</span><span class="sxs-lookup"><span data-stu-id="2a764-289">Example</span></span> | <span data-ttu-id="2a764-290">HTML</span><span class="sxs-lookup"><span data-stu-id="2a764-290">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a764-291">bold</span><span class="sxs-lookup"><span data-stu-id="2a764-291">bold</span></span> | <span data-ttu-id="2a764-292">**text**</span><span class="sxs-lookup"><span data-stu-id="2a764-292">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="2a764-293">italic</span><span class="sxs-lookup"><span data-stu-id="2a764-293">italic</span></span> | <span data-ttu-id="2a764-294">*text*</span><span class="sxs-lookup"><span data-stu-id="2a764-294">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="2a764-295">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="2a764-295">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="2a764-296">**Text**</span><span class="sxs-lookup"><span data-stu-id="2a764-296">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="2a764-297">取り消し線</span><span class="sxs-lookup"><span data-stu-id="2a764-297">strikethrough</span></span> | <span data-ttu-id="2a764-298">~~text~~</span><span class="sxs-lookup"><span data-stu-id="2a764-298">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="2a764-299">順序なしリスト</span><span class="sxs-lookup"><span data-stu-id="2a764-299">unordered list</span></span> | <ul><li><span data-ttu-id="2a764-300">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-300">text</span></span></li><li><span data-ttu-id="2a764-301">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-301">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="2a764-302">順序付きリスト</span><span class="sxs-lookup"><span data-stu-id="2a764-302">ordered list</span></span> | <ol><li><span data-ttu-id="2a764-303">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-303">text</span></span></li><li><span data-ttu-id="2a764-304">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-304">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="2a764-305">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-305">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="2a764-306">blockquote</span><span class="sxs-lookup"><span data-stu-id="2a764-306">blockquote</span></span> | <blockquote><span data-ttu-id="2a764-307">テキスト</span><span class="sxs-lookup"><span data-stu-id="2a764-307">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="2a764-308">hyperlink</span><span class="sxs-lookup"><span data-stu-id="2a764-308">hyperlink</span></span> | [<span data-ttu-id="2a764-309">Bing</span><span class="sxs-lookup"><span data-stu-id="2a764-309">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="2a764-310">画像リンク</span><span class="sxs-lookup"><span data-stu-id="2a764-310">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="2a764-311">シンプルカードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="2a764-311">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="2a764-312">デスクトッププラットフォームとモバイルプラットフォームの解像度が異なるため、フォーマットはデスクトップバージョンとモバイル版のTeamsの間で異なります。</span><span class="sxs-lookup"><span data-stu-id="2a764-312">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="2a764-313">デスクトップでは、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a764-313">On the desktop, HTML formatting appears like this:</span></span>

![デスクトップ クライアントでの HTML 形式の書式設定](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="2a764-315">iOS では、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a764-315">On iOS, HTML formatting appears like this:</span></span>

![iOS クライアントでの HTML フォーマット](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="2a764-317">懸案事項:</span><span class="sxs-lookup"><span data-stu-id="2a764-317">Issues:</span></span>

* <span data-ttu-id="2a764-318">太字や斜体などの文字書式は iOS ではレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="2a764-318">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="2a764-319">Android では、HTML 形式は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a764-319">On Android, HTML formatting appears like this:</span></span>

![アンドロイドクライアントでのHTMLフォーマット](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="2a764-321">太字や斜体などの文字書式は、Android 上で正しく表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a764-321">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="2a764-322">シンプルカードでの HTML フォーマットのサンプルの書式設定</span><span class="sxs-lookup"><span data-stu-id="2a764-322">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="2a764-323">これらのスクリーンショットは、hero カードの text プロパティが次の文字列に設定されている AppStudio Teams使用して作成されました。</span><span class="sxs-lookup"><span data-stu-id="2a764-323">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="2a764-324">このコードを変更することで、独自のカードで書式設定をテストできます。</span><span class="sxs-lookup"><span data-stu-id="2a764-324">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
