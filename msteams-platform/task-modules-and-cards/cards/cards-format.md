---
title: カード内のテキストの書式設定
description: カードテキストの書式設定について説明Microsoft Teams
keywords: teams ボット カードの形式
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 877a16f884e91138dc656434438a5fe1dd2ffd6e
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140640"
---
# <a name="format-cards-in-microsoft-teams"></a><span data-ttu-id="6ad39-104">カードの書式を設定Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6ad39-104">Format cards in Microsoft Teams</span></span>

<span data-ttu-id="6ad39-105">カードにリッチ テキストの書式設定を追加する 2 つの方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6ad39-105">Following are the two ways to add rich text formatting to your cards:</span></span>
* [<span data-ttu-id="6ad39-106">Markdown</span><span class="sxs-lookup"><span data-stu-id="6ad39-106">Markdown</span></span>](#format-cards-with-markdown)
* [<span data-ttu-id="6ad39-107">HTML</span><span class="sxs-lookup"><span data-stu-id="6ad39-107">HTML</span></span>](#format-cards-with-html)

<span data-ttu-id="6ad39-108">カードは、タイトルプロパティや字幕プロパティではなく、text プロパティでのみ書式設定をサポートします。</span><span class="sxs-lookup"><span data-stu-id="6ad39-108">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="6ad39-109">書式設定は、カードの種類に応じて、XML または HTML の書式設定または Markdown のサブセットを使用して指定できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-109">Formatting can be specified using a subset of XML or HTML formatting or Markdown, depending on the card type.</span></span> <span data-ttu-id="6ad39-110">アダプティブ カードの現在および将来の開発では、Markdown の書式設定をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="6ad39-110">For current and future development of Adaptive Cards, Markdown formatting is recommended.</span></span>

<span data-ttu-id="6ad39-111">書式設定のサポートは、カードの種類によって異なります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-111">Formatting support differs between card types.</span></span> <span data-ttu-id="6ad39-112">カードのレンダリングは、デスクトップ とモバイル クライアントの間で、Microsoft Teamsとデスクトップ ブラウザー Teams若干異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-112">Rendering of the card can differ slightly between the desktop and the mobile Microsoft Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="6ad39-113">インライン イメージは、任意のカードにTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-113">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="6ad39-114">イメージは、、、またはファイルとして書式設定できますし `.png` `.jpg` `.gif` 、1024 ピクセルまたは 1024 px または 1 MB を超え×する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-114">Images can be formatted as `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="6ad39-115">アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-115">Animated GIF is not supported.</span></span> <span data-ttu-id="6ad39-116">詳細については、「カードの [種類」を参照してください](./cards-reference.md#inline-card-images)。</span><span class="sxs-lookup"><span data-stu-id="6ad39-116">For more information, see [types of cards](./cards-reference.md#inline-card-images).</span></span>

<span data-ttu-id="6ad39-117">サポートされている特定のスタイルを含む markdown Office 365アダプティブ カードとコネクタ カードの書式を設定できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-117">You can format Adaptive Cards and Office 365 Connector cards with Markdown that include certain supported styles.</span></span>

## <a name="format-cards-with-markdown"></a><span data-ttu-id="6ad39-118">Markdown でカードを書式設定する</span><span class="sxs-lookup"><span data-stu-id="6ad39-118">Format cards with Markdown</span></span>

<span data-ttu-id="6ad39-119">次のカードの種類では、マークダウンの書式設定がサポートTeams。</span><span class="sxs-lookup"><span data-stu-id="6ad39-119">The following card types support Markdown formatting in Teams:</span></span>

* <span data-ttu-id="6ad39-120">アダプティブ カード: Markdown はアダプティブ カード フィールドおよび `Textblock` `Fact.Title` `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="6ad39-120">Adaptive Cards: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="6ad39-121">アダプティブ カードでは HTML はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-121">HTML is not supported in Adaptive Cards.</span></span>
* <span data-ttu-id="6ad39-122">O365 コネクタ カード: テキスト フィールドの O365 コネクタ カードでは、マークダウンと制限付き HTML がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-122">O365 Connector cards: Markdown and limited HTML is supported in O365 Connector cards in the text fields.</span></span>

<span data-ttu-id="6ad39-123">リスト内の改行に対して、アダプティブ カードの改行を使用するか、エスケープ `\r` `\n` シーケンスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-123">You can use newlines for Adaptive Cards using `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="6ad39-124">アダプティブ カード用のデスクトップとモバイル バージョンの書式Teams異なります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-124">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards.</span></span> <span data-ttu-id="6ad39-125">カード ベースのメンションは、Web クライアント、デスクトップ クライアント、モバイル クライアントでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-125">Card-based mentions are supported in web, desktop, and mobile clients.</span></span> <span data-ttu-id="6ad39-126">information masking プロパティを使用すると、アダプティブ カード入力要素内のユーザーからのパスワードや機密情報などの特定の情報を `Input.Text` マスクできます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-126">You can use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card `Input.Text` input element.</span></span> <span data-ttu-id="6ad39-127">アダプティブ カードの幅は、オブジェクトを使用して展開 `width` できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-127">You can expand the width of an Adaptive Card using the `width` object.</span></span> <span data-ttu-id="6ad39-128">アダプティブ カード内で typeahead サポートを有効にし、ユーザーが入力を入力すると、入力の選択肢のセットをフィルター処理できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-128">You can enable typeahead support within Adaptive Cards and filter the set of input choices as the user types the input.</span></span> <span data-ttu-id="6ad39-129">このプロパティを使用 `msteams` して、ステージ ビューに画像を選択的に表示する機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-129">You can use the `msteams` property to add the ability to display images in stage view selectively.</span></span>

<span data-ttu-id="6ad39-130">アダプティブ カードとコネクタ カードのデスクトップとモバイル バージョンのTeamsは異なります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-130">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards and connector cards.</span></span> <span data-ttu-id="6ad39-131">このセクションでは、アダプティブ カードとコネクタ カードの Markdown 形式の例を参照できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-131">In this section, you can go through the Markdown format example for Adaptive Cards and connector cards.</span></span>

# <a name="markdown-format-for-adaptive-cards"></a>[<span data-ttu-id="6ad39-132">アダプティブ カードのマークダウン形式</span><span class="sxs-lookup"><span data-stu-id="6ad39-132">Markdown format for Adaptive Cards</span></span>](#tab/adaptive-md)

 <span data-ttu-id="6ad39-133">次の表に、、 、およびのサポート `Textblock` されているスタイル `Fact.Title` を示します `Fact.Value` 。</span><span class="sxs-lookup"><span data-stu-id="6ad39-133">The following table provides the supported styles for `Textblock`, `Fact.Title`, and `Fact.Value`:</span></span>

| <span data-ttu-id="6ad39-134">Style</span><span class="sxs-lookup"><span data-stu-id="6ad39-134">Style</span></span> | <span data-ttu-id="6ad39-135">例</span><span class="sxs-lookup"><span data-stu-id="6ad39-135">Example</span></span> | <span data-ttu-id="6ad39-136">Markdown</span><span class="sxs-lookup"><span data-stu-id="6ad39-136">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ad39-137">太字</span><span class="sxs-lookup"><span data-stu-id="6ad39-137">Bold</span></span> | <span data-ttu-id="6ad39-138">**Bold**</span><span class="sxs-lookup"><span data-stu-id="6ad39-138">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="6ad39-139">斜体</span><span class="sxs-lookup"><span data-stu-id="6ad39-139">Italic</span></span> | <span data-ttu-id="6ad39-140">_Italic_</span><span class="sxs-lookup"><span data-stu-id="6ad39-140">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="6ad39-141">記号付きリスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-141">Unordered list</span></span> | <ul><li><span data-ttu-id="6ad39-142">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-142">text</span></span></li><li><span data-ttu-id="6ad39-143">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-143">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="6ad39-144">番号付きリスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-144">Ordered list</span></span> | <ol><li><span data-ttu-id="6ad39-145">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-145">text</span></span></li><li><span data-ttu-id="6ad39-146">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-146">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="6ad39-147">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="6ad39-147">Hyperlinks</span></span> |[<span data-ttu-id="6ad39-148">Bing</span><span class="sxs-lookup"><span data-stu-id="6ad39-148">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="6ad39-149">次の Markdown タグはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-149">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="6ad39-150">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="6ad39-150">Headers</span></span>
* <span data-ttu-id="6ad39-151">テーブル</span><span class="sxs-lookup"><span data-stu-id="6ad39-151">Tables</span></span>
* <span data-ttu-id="6ad39-152">画像</span><span class="sxs-lookup"><span data-stu-id="6ad39-152">Images</span></span>
* <span data-ttu-id="6ad39-153">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-153">Preformatted text</span></span>
* <span data-ttu-id="6ad39-154">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="6ad39-154">Blockquotes</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="6ad39-155">アダプティブ カードの改行</span><span class="sxs-lookup"><span data-stu-id="6ad39-155">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="6ad39-156">リスト内の改行 `\r` には、エスケープ `\n` シーケンスまたはエスケープ シーケンスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-156">You can use the `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="6ad39-157">リスト `\n\n` で使用すると、リスト内の次の要素がインデントされます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-157">Using `\n\n` in lists causes the next element in the list to be indented.</span></span> <span data-ttu-id="6ad39-158">TextBlock の他の場所で改行が必要な場合は、 を使用します `\n\n` 。</span><span class="sxs-lookup"><span data-stu-id="6ad39-158">If you require newlines elsewhere in the TextBlock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="6ad39-159">アダプティブ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="6ad39-159">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="6ad39-160">デスクトップでは、アダプティブ カード マークダウンの書式設定は、Web ブラウザーとクライアント アプリケーションの両方の次のTeams表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-160">On the desktop, Adaptive Card Markdown formatting appears as shown in the following image in both web browsers and in the Teams client application:</span></span>

![デスクトップ クライアントでのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="6ad39-162">iOS では、アダプティブ カード マークダウンの書式設定が次の図のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-162">On iOS, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![iOS でのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="6ad39-164">Android では、アダプティブ カード マークダウンの書式設定が次の図のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-164">On Android, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![Android でのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-Android.png)

<span data-ttu-id="6ad39-166">詳細については、「アダプティブ カード」 [のテキスト機能を参照してください](/adaptive-cards/create/textfeatures)。</span><span class="sxs-lookup"><span data-stu-id="6ad39-166">For more information, see [text features in Adaptive Cards](/adaptive-cards/create/textfeatures).</span></span>

> [!NOTE]
> <span data-ttu-id="6ad39-167">このセクションで説明する日付とローカライズ機能は、このセクションではTeams。</span><span class="sxs-lookup"><span data-stu-id="6ad39-167">The date and localization features mentioned in this section are not supported in Teams.</span></span>

### <a name="adaptive-cards-format-sample"></a><span data-ttu-id="6ad39-168">アダプティブ カード形式のサンプル</span><span class="sxs-lookup"><span data-stu-id="6ad39-168">Adaptive Cards format sample</span></span>

<span data-ttu-id="6ad39-169">次のコードは、アダプティブ カードの書式設定の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-169">The following code shows an example of Adaptive Cards formatting:</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="6ad39-170">アダプティブ カード v1.2 内でのサポートのメンション</span><span class="sxs-lookup"><span data-stu-id="6ad39-170">Mention support within Adaptive Cards v1.2</span></span>

<span data-ttu-id="6ad39-171">ボットおよびメッセージング拡張機能@mentionsアダプティブ カード本文内に追加できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-171">You can add @mentions within an Adaptive Card body for bots and messaging extension responses.</span></span> <span data-ttu-id="6ad39-172">カードに@mentionsするには、チャネルおよびグループ チャットの会話でメッセージ ベースのメンションと同じ通知ロジックとレンダリング [に従います](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)。</span><span class="sxs-lookup"><span data-stu-id="6ad39-172">To add @mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="6ad39-173">ボットとメッセージング拡張機能には [、TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 要素と FactSet 要素のカード コンテンツ内にメンション [を含](https://adaptivecards.io/explorer/FactSet.html) めることはできません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-173">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="6ad39-174">[メディア要素](https://adaptivecards.io/explorer/Media.html)は、現在、プラットフォーム上のアダプティブ カード v1.2 ではTeamsされていません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-174">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive Cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="6ad39-175">チャネルとチームのメンションはボット メッセージではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-175">Channel and team mentions are not supported in bot messages.</span></span>

<span data-ttu-id="6ad39-176">アダプティブ カードにメンションを含めるには、アプリに次の要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-176">To include a mention in an Adaptive Card, your app needs to include the following elements:</span></span>

* <span data-ttu-id="6ad39-177">`<at>username</at>` は、サポートされているアダプティブ カード要素に含まれます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-177">`<at>username</at>` in the supported Adaptive Card elements.</span></span>
* <span data-ttu-id="6ad39-178">カード `mention` コンテンツ内のプロパティ内のオブジェクトには、Teams `msteams` のユーザー ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-178">The `mention` object inside of an `msteams` property in the card content includes the Teams user ID of the user being mentioned.</span></span>
* <span data-ttu-id="6ad39-179">これは `userId` 、ボット ID と特定のユーザーに固有です。</span><span class="sxs-lookup"><span data-stu-id="6ad39-179">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="6ad39-180">特定のユーザーを@mention使用できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-180">It can be used to @mention a particular user.</span></span> <span data-ttu-id="6ad39-181">ユーザー `userId` ID の取得に記載されているオプションのいずれかを使用して [取得できます](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)。</span><span class="sxs-lookup"><span data-stu-id="6ad39-181">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="6ad39-182">メンション付きアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="6ad39-182">Sample Adaptive Card with a mention</span></span>

<span data-ttu-id="6ad39-183">次のコードは、メンションを持つアダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-183">The following code shows an example of Adaptive Card with a mention:</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="6ad39-184">アダプティブ カードの情報マスキング</span><span class="sxs-lookup"><span data-stu-id="6ad39-184">Information masking in Adaptive Cards</span></span>

<span data-ttu-id="6ad39-185">Information masking プロパティを使用して、アダプティブ カード入力要素内のユーザーからのパスワードや機密情報などの特定の情報を [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) マスクします。</span><span class="sxs-lookup"><span data-stu-id="6ad39-185">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span>

> [!NOTE]
> <span data-ttu-id="6ad39-186">この機能は、クライアント側の情報マスキングのみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="6ad39-186">The feature only supports client side information masking.</span></span> <span data-ttu-id="6ad39-187">マスクされた入力テキストは、ボットの構成中に指定された HTTPS エンドポイント アドレスにクリア テキスト [として送信されます](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="6ad39-187">The masked input text is sent as clear text to the HTTPS endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).</span></span>

<span data-ttu-id="6ad39-188">アダプティブ カードで情報をマスクするには、型に `isMasked` プロパティを追加 **し** `Input.Text` 、その値を true に設定 **します**。</span><span class="sxs-lookup"><span data-stu-id="6ad39-188">To mask information in Adaptive Cards, add the `isMasked` property to **type** `Input.Text`, and set its value to **true**.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="6ad39-189">マスキング プロパティを持つアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="6ad39-189">Sample Adaptive Card with masking property</span></span>

<span data-ttu-id="6ad39-190">次のコードは、マスキング プロパティを持つアダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-190">The following code shows an example of Adaptive Card with masking property:</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

<span data-ttu-id="6ad39-191">次の図は、アダプティブ カードのマスキング情報の例です。</span><span class="sxs-lookup"><span data-stu-id="6ad39-191">The following image is an example of masking information in Adaptive Cards:</span></span>

![マスキング情報イメージ](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="6ad39-193">全幅アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="6ad39-193">Full width Adaptive Card</span></span>

<span data-ttu-id="6ad39-194">このプロパティを使用 `msteams` すると、アダプティブ カードの幅を拡大し、追加のキャンバス領域を利用できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-194">You can use the `msteams` property to expand the width of an Adaptive Card and make use of additional canvas space.</span></span> <span data-ttu-id="6ad39-195">次のセクションでは、プロパティの使い方について説明します。</span><span class="sxs-lookup"><span data-stu-id="6ad39-195">The next section provides information on how to use the property.</span></span>

#### <a name="construct-full-width-cards"></a><span data-ttu-id="6ad39-196">全幅カードを作成する</span><span class="sxs-lookup"><span data-stu-id="6ad39-196">Construct full width cards</span></span>

<span data-ttu-id="6ad39-197">全幅アダプティブ カードを作成するには、カード コンテンツの `width` `msteams` プロパティのオブジェクトをに設定する必要があります `Full` 。</span><span class="sxs-lookup"><span data-stu-id="6ad39-197">To make a full width Adaptive Card, the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="6ad39-198">全幅のアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="6ad39-198">Sample Adaptive Card with full width</span></span>

<span data-ttu-id="6ad39-199">全幅アダプティブ カードを作成するには、アプリに次のコード サンプルの要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-199">To make a full width Adaptive Card, your app must include the elements from the following code sample:</span></span>

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

<span data-ttu-id="6ad39-200">次の図は、全幅アダプティブ カードを示しています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-200">The following image shows a full width Adaptive Card:</span></span>

![全幅アダプティブ カード ビュー](../../assets/images/cards/full-width-adaptive-card.png)

<span data-ttu-id="6ad39-202">次の図は、プロパティを Full に設定していない場合のアダプティブ カードの既定 `width` のビューを **示しています**。</span><span class="sxs-lookup"><span data-stu-id="6ad39-202">The following image shows the default view of the Adaptive Card when you have not set the `width` property to **Full**:</span></span>

![小幅アダプティブ カード ビュー](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a><span data-ttu-id="6ad39-204">Typeahead のサポート</span><span class="sxs-lookup"><span data-stu-id="6ad39-204">Typeahead support</span></span>

<span data-ttu-id="6ad39-205">schema 要素内で、ユーザーにフィルター処理を求め、サイズの大きい数の選択肢を選択すると、タスクの完了が大幅 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) に遅くなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-205">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter and select a sizeable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="6ad39-206">アダプティブ カード内の Typeahead サポートは、ユーザーが入力を入力する場合に、入力の選択肢のセットを絞り込むかフィルター処理することで、入力の選択を簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-206">Typeahead support within Adaptive Cards can simplify input selection by narrowing or filtering the set of input choices as the user types the input.</span></span>

<span data-ttu-id="6ad39-207">で typeahead を有効にするには `Input.Choiceset` 、に設定 `style` し、 `filtered` 必ずに `isMultiSelect` 設定します `false` 。</span><span class="sxs-lookup"><span data-stu-id="6ad39-207">To enable typeahead within the `Input.Choiceset`, set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span>

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="6ad39-208">Typeahead サポートを備えるアダプティブ カードのサンプル</span><span class="sxs-lookup"><span data-stu-id="6ad39-208">Sample Adaptive Card with typeahead support</span></span>

<span data-ttu-id="6ad39-209">次のコードは、typeahead サポートを備えるアダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-209">The following code shows an example of Adaptive Card with typeahead support:</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="6ad39-210">アダプティブ カードの画像のステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="6ad39-210">Stage view for images in Adaptive Cards</span></span>

<span data-ttu-id="6ad39-211">アダプティブ カードでは、このプロパティを使用して、ステージ ビューで画像を選択的 `msteams` に表示する機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-211">In an Adaptive Card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="6ad39-212">ユーザーが画像にカーソルを合わせると、展開アイコンが表示され、属性が `allowExpand` に設定されます `true` 。</span><span class="sxs-lookup"><span data-stu-id="6ad39-212">When users hover over the images, they can see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="6ad39-213">プロパティの使用方法については、次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6ad39-213">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="6ad39-214">ユーザーが画像の上にマウス ポインターを置くと、次の図に示すように、右上隅に展開アイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-214">When users hover over the image, an expand icon appears at the top right corner as shown in the following image:</span></span>

![展開可能なイメージを持つアダプティブ カード](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

<span data-ttu-id="6ad39-216">次の図に示すように、ユーザーが展開アイコンを選択すると、イメージがステージ ビューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-216">The image appears in stage view when the user selects the expand icon as shown in the following image:</span></span>

![ステージ ビューに展開されたイメージ](../../assets/images/cards/adaptivecard-expand-image.png)

<span data-ttu-id="6ad39-218">ステージ ビューでは、ユーザーは画像を拡大および縮小できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-218">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="6ad39-219">この機能が必要なアダプティブ カードの画像を選択できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-219">You can select the images in your Adaptive Card that must have this capability.</span></span>

> [!NOTE]
> * <span data-ttu-id="6ad39-220">拡大および縮小機能は、アダプティブ カードの画像の種類である画像要素にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-220">Zoom in and zoom out capability applies only to the image elements that is image type in an Adaptive Card.</span></span>
> * <span data-ttu-id="6ad39-221">モバイル Teamsでは、アダプティブ カードの画像のステージ ビュー機能が既定で使用できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-221">For Teams mobile apps, stage view functionality for images in Adaptive Cards is available by default.</span></span> <span data-ttu-id="6ad39-222">ユーザーは、属性が存在するかどうかに関係なく、画像をタップするだけでステージ ビューでアダプティブ カードイメージ `allowExpand` を表示できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-222">Users can view Adaptive Card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-format-for-o365-connector-cards"></a>[<span data-ttu-id="6ad39-223">O365 コネクタ カードのマークダウン形式</span><span class="sxs-lookup"><span data-stu-id="6ad39-223">Markdown format for O365 Connector cards</span></span>](#tab/connector-md)

<span data-ttu-id="6ad39-224">コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-224">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="6ad39-225">Style</span><span class="sxs-lookup"><span data-stu-id="6ad39-225">Style</span></span> | <span data-ttu-id="6ad39-226">例</span><span class="sxs-lookup"><span data-stu-id="6ad39-226">Example</span></span> | <span data-ttu-id="6ad39-227">Markdown</span><span class="sxs-lookup"><span data-stu-id="6ad39-227">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ad39-228">太字</span><span class="sxs-lookup"><span data-stu-id="6ad39-228">Bold</span></span> | <span data-ttu-id="6ad39-229">**text**</span><span class="sxs-lookup"><span data-stu-id="6ad39-229">**text**</span></span> | `**text**` |
| <span data-ttu-id="6ad39-230">斜体</span><span class="sxs-lookup"><span data-stu-id="6ad39-230">Italic</span></span> | <span data-ttu-id="6ad39-231">*text*</span><span class="sxs-lookup"><span data-stu-id="6ad39-231">*text*</span></span> | `*text*` |
| <span data-ttu-id="6ad39-232">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="6ad39-232">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="6ad39-233">**Text**</span><span class="sxs-lookup"><span data-stu-id="6ad39-233">**Text**</span></span> | `### Text`|
| <span data-ttu-id="6ad39-234">取り消し線</span><span class="sxs-lookup"><span data-stu-id="6ad39-234">Strikethrough</span></span> | <span data-ttu-id="6ad39-235">~~text~~</span><span class="sxs-lookup"><span data-stu-id="6ad39-235">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="6ad39-236">記号付きリスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-236">Unordered list</span></span> | <ul><li><span data-ttu-id="6ad39-237">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-237">text</span></span></li><li><span data-ttu-id="6ad39-238">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-238">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="6ad39-239">番号付きリスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-239">Ordered list</span></span> | <ol><li><span data-ttu-id="6ad39-240">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-240">text</span></span></li><li><span data-ttu-id="6ad39-241">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-241">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="6ad39-242">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-242">Preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="6ad39-243">Blockquote</span><span class="sxs-lookup"><span data-stu-id="6ad39-243">Blockquote</span></span> | <span data-ttu-id="6ad39-244">>をブロッククォートする</span><span class="sxs-lookup"><span data-stu-id="6ad39-244">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="6ad39-245">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="6ad39-245">Hyperlink</span></span> | [<span data-ttu-id="6ad39-246">Bing</span><span class="sxs-lookup"><span data-stu-id="6ad39-246">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="6ad39-247">画像リンク</span><span class="sxs-lookup"><span data-stu-id="6ad39-247">Image link</span></span> |![岩の上のアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="6ad39-249">コネクタ カードでは、改行はのためにレンダリングされますが `\n\n` 、for または `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="6ad39-249">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="6ad39-250">コネクタ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="6ad39-250">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="6ad39-251">デスクトップでは、次の図に示すように、コネクタ カードの Markdown 書式設定が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-251">On the desktop, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![デスクトップ クライアントでのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="6ad39-253">iOS では、次の図に示すように、コネクタ カードの Markdown 書式設定が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-253">On iOS, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![iOS クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="6ad39-255">iOS 用 Markdown を使用するコネクタ カードには、次の問題があります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-255">Connector cards using Markdown for iOS include the following issues:</span></span>

* <span data-ttu-id="6ad39-256">コネクタ カードの iOS クライアントTeamsマークダウンまたは HTML インライン イメージはレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-256">The iOS client for Teams does not render Markdown or HTML inline images in connector cards.</span></span>
* <span data-ttu-id="6ad39-257">ブロッククォートはインデントされますが、灰色の背景なしでレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-257">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="6ad39-258">Android では、次の図に示すように、コネクタ カードのマークダウンの書式設定が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-258">On Android, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Android クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a><span data-ttu-id="6ad39-260">Markdown コネクタ カードの形式の例</span><span class="sxs-lookup"><span data-stu-id="6ad39-260">Format example for Markdown connector cards</span></span>

<span data-ttu-id="6ad39-261">次のコードは、Markdown コネクタ カードの書式設定の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-261">The following code shows an example of formatting for Markdown connector cards:</span></span>

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

## <a name="format-cards-with-html"></a><span data-ttu-id="6ad39-262">HTML を使用してカードを書式設定する</span><span class="sxs-lookup"><span data-stu-id="6ad39-262">Format cards with HTML</span></span>

<span data-ttu-id="6ad39-263">次のカードの種類は、HTML 形式をサポートTeams。</span><span class="sxs-lookup"><span data-stu-id="6ad39-263">The following card types support HTML formatting in Teams:</span></span>

* <span data-ttu-id="6ad39-264">O365 コネクタ カード: 制限付きマークダウンと HTML の書式設定は、コネクタ カードOffice 365サポートされています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-264">O365 Connector cards: Limited Markdown and HTML formatting is supported in Office 365 Connector cards.</span></span>
* <span data-ttu-id="6ad39-265">ヒーロー カードとサムネイル カード: HTML タグは、ヒーロー カードやサムネイル カードなどの単純なカードでサポートされます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-265">Hero and thumbnail cards: HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span>

<span data-ttu-id="6ad39-266">O365 Connector カードと簡易カードの場合、Teamsとモバイル バージョンの書式は異なります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-266">Formatting is different between the desktop and the mobile versions of Teams for O365 Connector cards and simple cards.</span></span> <span data-ttu-id="6ad39-267">このセクションでは、コネクタ カードと簡易カードの HTML 形式の例を参照できます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-267">In this section, you can go through the HTML format example for connector cards and simple cards.</span></span>

# <a name="html-format-for-o365-connector-cards"></a>[<span data-ttu-id="6ad39-268">O365 コネクタ カードの HTML 形式</span><span class="sxs-lookup"><span data-stu-id="6ad39-268">HTML format for O365 Connector cards</span></span>](#tab/connector-html)

<span data-ttu-id="6ad39-269">コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-269">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="6ad39-270">Style</span><span class="sxs-lookup"><span data-stu-id="6ad39-270">Style</span></span> | <span data-ttu-id="6ad39-271">例</span><span class="sxs-lookup"><span data-stu-id="6ad39-271">Example</span></span> | <span data-ttu-id="6ad39-272">HTML</span><span class="sxs-lookup"><span data-stu-id="6ad39-272">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ad39-273">太字</span><span class="sxs-lookup"><span data-stu-id="6ad39-273">Bold</span></span> | <span data-ttu-id="6ad39-274">**text**</span><span class="sxs-lookup"><span data-stu-id="6ad39-274">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="6ad39-275">斜体</span><span class="sxs-lookup"><span data-stu-id="6ad39-275">Italic</span></span> | <span data-ttu-id="6ad39-276">*text*</span><span class="sxs-lookup"><span data-stu-id="6ad39-276">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="6ad39-277">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="6ad39-277">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="6ad39-278">**Text**</span><span class="sxs-lookup"><span data-stu-id="6ad39-278">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="6ad39-279">取り消し線</span><span class="sxs-lookup"><span data-stu-id="6ad39-279">Strikethrough</span></span> | <span data-ttu-id="6ad39-280">~~text~~</span><span class="sxs-lookup"><span data-stu-id="6ad39-280">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="6ad39-281">記号付きリスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-281">Unordered list</span></span> | <ul><li><span data-ttu-id="6ad39-282">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-282">text</span></span></li><li><span data-ttu-id="6ad39-283">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-283">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="6ad39-284">番号付きリスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-284">Ordered list</span></span> | <ol><li><span data-ttu-id="6ad39-285">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-285">text</span></span></li><li><span data-ttu-id="6ad39-286">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-286">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="6ad39-287">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-287">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="6ad39-288">Blockquote</span><span class="sxs-lookup"><span data-stu-id="6ad39-288">Blockquote</span></span> | <blockquote><span data-ttu-id="6ad39-289">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-289">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="6ad39-290">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="6ad39-290">Hyperlink</span></span> | [<span data-ttu-id="6ad39-291">Bing</span><span class="sxs-lookup"><span data-stu-id="6ad39-291">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="6ad39-292">画像リンク</span><span class="sxs-lookup"><span data-stu-id="6ad39-292">Image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="6ad39-293">コネクタ カードでは、タグを使用して改行が HTML でレンダリング `<p>` されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-293">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="6ad39-294">コネクタ カードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="6ad39-294">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="6ad39-295">デスクトップでは、次の図に示すように、コネクタ カードの HTML 書式が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-295">On the desktop, HTML formatting for connector cards appears as shown in the following image:</span></span>

![デスクトップ クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="6ad39-297">iOS では、次の図に示すように HTML 書式が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-297">On iOS, HTML formatting appears as shown in the following image:</span></span>

![iOS クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="6ad39-299">iOS 用 HTML を使用するコネクタ カードには、次の問題があります。</span><span class="sxs-lookup"><span data-stu-id="6ad39-299">Connector cards using HTML for iOS include the following issues:</span></span>

* <span data-ttu-id="6ad39-300">インライン イメージは、コネクタ カードの Markdown または HTML を使用して iOS ではレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-300">Inline images are not rendered on iOS using either Markdown or HTML in connector cards.</span></span>
* <span data-ttu-id="6ad39-301">書式設定済みのテキストはレンダリングされますが、背景が灰色ではありません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-301">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="6ad39-302">Android では、次の図に示すように HTML 書式が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-302">On Android, HTML formatting appears as shown in the following image:</span></span>

![Android クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a><span data-ttu-id="6ad39-304">HTML コネクタ カードの形式のサンプル</span><span class="sxs-lookup"><span data-stu-id="6ad39-304">Format sample for HTML connector cards</span></span>

<span data-ttu-id="6ad39-305">次のコードは、HTML コネクタ カードの書式設定の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="6ad39-305">The following code shows an example of formatting for HTML connector cards:</span></span>

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[<span data-ttu-id="6ad39-306">ヒーロー カードとサムネイル カードの HTML 形式</span><span class="sxs-lookup"><span data-stu-id="6ad39-306">HTML format for hero and thumbnail cards</span></span>](#tab/simple-html)

<span data-ttu-id="6ad39-307">HTML タグは、ヒーロー カードやサムネイル カードなどの単純なカードでサポートされます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-307">HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span> <span data-ttu-id="6ad39-308">Markdown はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-308">Markdown is not supported.</span></span>

| <span data-ttu-id="6ad39-309">Style</span><span class="sxs-lookup"><span data-stu-id="6ad39-309">Style</span></span> | <span data-ttu-id="6ad39-310">例</span><span class="sxs-lookup"><span data-stu-id="6ad39-310">Example</span></span> | <span data-ttu-id="6ad39-311">HTML</span><span class="sxs-lookup"><span data-stu-id="6ad39-311">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ad39-312">太字</span><span class="sxs-lookup"><span data-stu-id="6ad39-312">Bold</span></span> | <span data-ttu-id="6ad39-313">**text**</span><span class="sxs-lookup"><span data-stu-id="6ad39-313">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="6ad39-314">斜体</span><span class="sxs-lookup"><span data-stu-id="6ad39-314">Italic</span></span> | <span data-ttu-id="6ad39-315">*text*</span><span class="sxs-lookup"><span data-stu-id="6ad39-315">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="6ad39-316">ヘッダー (レベル 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="6ad39-316">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="6ad39-317">**Text**</span><span class="sxs-lookup"><span data-stu-id="6ad39-317">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="6ad39-318">取り消し線</span><span class="sxs-lookup"><span data-stu-id="6ad39-318">Strikethrough</span></span> | <span data-ttu-id="6ad39-319">~~text~~</span><span class="sxs-lookup"><span data-stu-id="6ad39-319">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="6ad39-320">記号付きリスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-320">Unordered list</span></span> | <ul><li><span data-ttu-id="6ad39-321">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-321">text</span></span></li><li><span data-ttu-id="6ad39-322">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-322">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="6ad39-323">番号付きリスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-323">Ordered list</span></span> | <ol><li><span data-ttu-id="6ad39-324">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-324">text</span></span></li><li><span data-ttu-id="6ad39-325">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-325">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="6ad39-326">書式設定済みのテキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-326">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="6ad39-327">Blockquote</span><span class="sxs-lookup"><span data-stu-id="6ad39-327">Blockquote</span></span> | <blockquote><span data-ttu-id="6ad39-328">テキスト</span><span class="sxs-lookup"><span data-stu-id="6ad39-328">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="6ad39-329">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="6ad39-329">Hyperlink</span></span> | [<span data-ttu-id="6ad39-330">Bing</span><span class="sxs-lookup"><span data-stu-id="6ad39-330">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="6ad39-331">画像リンク</span><span class="sxs-lookup"><span data-stu-id="6ad39-331">Image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="6ad39-332">単純なカードのモバイルとデスクトップの違い</span><span class="sxs-lookup"><span data-stu-id="6ad39-332">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="6ad39-333">デスクトップ プラットフォームとモバイル プラットフォームの解像度の違いがある場合、デスクトップとモバイル バージョンのモバイル プラットフォームでは書式設定が異Teams。</span><span class="sxs-lookup"><span data-stu-id="6ad39-333">As there are resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="6ad39-334">デスクトップでは、次の図に示すように HTML 書式が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-334">On the desktop, HTML formatting appears as shown in the following image:</span></span>

![デスクトップ クライアントでの HTML 書式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="6ad39-336">iOS では、次の図に示すように HTML 書式が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-336">On iOS, HTML formatting appears as shown in the following image:</span></span>

![iOS クライアントの HTML 書式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="6ad39-338">太字や斜体などの文字の書式設定は、iOS ではレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="6ad39-338">Character formatting, such as bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="6ad39-339">Android では、次の図に示すように HTML 書式が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-339">On Android, HTML formatting appears as shown in the following image:</span></span>

![Android クライアントでの HTML 書式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="6ad39-341">Android で太字や斜体などの文字の書式設定が正しく表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-341">Character formatting, such as bold and italic display correctly on Android.</span></span>

### <a name="format-example-for-simple-cards"></a><span data-ttu-id="6ad39-342">単純なカードの形式の例</span><span class="sxs-lookup"><span data-stu-id="6ad39-342">Format example for simple cards</span></span>

<span data-ttu-id="6ad39-343">前のセクションのイメージは、Teams **App Studio** を使用して作成され、ヒーロー カードの text プロパティは次の文字列に設定されます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-343">The images in the previous section were created using Teams **App Studio**, where the text property of a hero card is set to the following string:</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

<span data-ttu-id="6ad39-344">このコードを変更することで、独自のカードの書式設定をテストできます。</span><span class="sxs-lookup"><span data-stu-id="6ad39-344">You can test formatting in your own cards by modifying this code.</span></span>

---

## <a name="see-also"></a><span data-ttu-id="6ad39-345">関連項目</span><span class="sxs-lookup"><span data-stu-id="6ad39-345">See also</span></span>

* [<span data-ttu-id="6ad39-346">カードアクション</span><span class="sxs-lookup"><span data-stu-id="6ad39-346">Card actions</span></span>](./cards-actions.md)
* [<span data-ttu-id="6ad39-347">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="6ad39-347">Task modules</span></span>](~/task-modules-and-cards/cards/cards-format.md)
