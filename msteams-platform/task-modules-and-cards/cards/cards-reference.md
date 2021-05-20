---
title: カード リファレンス
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
localization_priority: Normal
keywords: Bot のカード リファレンス
ms.topic: reference
ms.openlocfilehash: cab7f1659759f40beb1aba59531ee6c1a84662c1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566860"
---
# <a name="cards-reference"></a><span data-ttu-id="39315-104">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="39315-104">Cards reference</span></span>

<span data-ttu-id="39315-105">このドキュメントに記載されているカードは、ボットでMicrosoft Teamsでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="39315-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="39315-106">これらは Bot Framework によって定義されたカードに基づいていますが、Teamsはすべての Bot Framework カードをサポートしている Teamsわけではありません。</span><span class="sxs-lookup"><span data-stu-id="39315-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="39315-107">このドキュメントの参照では、相違点が示されています。</span><span class="sxs-lookup"><span data-stu-id="39315-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="39315-108">カードの例</span><span class="sxs-lookup"><span data-stu-id="39315-108">Card examples</span></span>

<span data-ttu-id="39315-109">カードの使用方法に関する追加情報は、Bot Builder SDK v3 のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="39315-110">コード サンプルは、GitHubの Microsoft/BotBuilder-サンプル リポジトリでも入手できます。</span><span class="sxs-lookup"><span data-stu-id="39315-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="39315-111">.NET</span><span class="sxs-lookup"><span data-stu-id="39315-111">.NET</span></span>
  * <span data-ttu-id="39315-112">[メッセージに添付ファイルとしてカードを追加する](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true):</span><span class="sxs-lookup"><span data-stu-id="39315-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="39315-113">[カードサンプルコード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="39315-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="39315-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="39315-114">Node.js</span></span>
  * <span data-ttu-id="39315-115">[メッセージに添付ファイルとしてカードを追加する](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true):</span><span class="sxs-lookup"><span data-stu-id="39315-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="39315-116">[カードサンプルコード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="39315-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="39315-117">カードの種類</span><span class="sxs-lookup"><span data-stu-id="39315-117">Types of cards</span></span>

<span data-ttu-id="39315-118">次の表に、使用できるカードの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="39315-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="39315-119">カードタイプ</span><span class="sxs-lookup"><span data-stu-id="39315-119">Card type</span></span> | <span data-ttu-id="39315-120">説明</span><span class="sxs-lookup"><span data-stu-id="39315-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="39315-121">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="39315-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="39315-122">このカードは、テキスト、音声、画像、ボタン、および入力フィールドの任意の組み合わせを含むことができる高度にカスタマイズ可能なカードです。</span><span class="sxs-lookup"><span data-stu-id="39315-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="39315-123">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="39315-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="39315-124">このカードには、通常、1 つの大きなイメージ、1 つ以上のボタン、および少量のテキストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="39315-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="39315-125">リスト カード</span><span class="sxs-lookup"><span data-stu-id="39315-125">List card</span></span>](#list-card) | <span data-ttu-id="39315-126">このカードは項目のスクロールリストです。</span><span class="sxs-lookup"><span data-stu-id="39315-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="39315-127">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="39315-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="39315-128">このカードには、複数のセクション、フィールド、画像、アクションを含む柔軟なレイアウトがあります。</span><span class="sxs-lookup"><span data-stu-id="39315-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="39315-129">レシート カード</span><span class="sxs-lookup"><span data-stu-id="39315-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="39315-130">このカードは、ユーザーに領収書を提供します。</span><span class="sxs-lookup"><span data-stu-id="39315-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="39315-131">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="39315-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="39315-132">このカードを使用すると、ボットはユーザーがサインインするように要求できます。</span><span class="sxs-lookup"><span data-stu-id="39315-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="39315-133">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="39315-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="39315-134">このカードには、通常、サムネイル画像が 1 つ、短いテキストと 1 つ以上のボタンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="39315-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="39315-135">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="39315-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="39315-136">このカードは、1 つの応答で複数のアイテムを返すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="39315-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="39315-137">すべてのカードの共通プロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="39315-138">インライン カードの画像</span><span class="sxs-lookup"><span data-stu-id="39315-138">Inline card images</span></span>

<span data-ttu-id="39315-139">カードには、一般に公開されている画像へのリンクを含めることによって、インライン画像を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="39315-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="39315-140">パフォーマンスを向上するために、パブリック コンテンツ配信ネットワーク (CDN) でイメージをホストすることを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="39315-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="39315-141">画像は、縦横比を維持しながら、画像領域を覆うサイズを拡大または縮小します。</span><span class="sxs-lookup"><span data-stu-id="39315-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="39315-142">次に、画像を中央から切り取って、カードの適切な縦横比を実現します。</span><span class="sxs-lookup"><span data-stu-id="39315-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="39315-143">画像は、PNG、JPEG、または GIF 形式で最大 1024×1024 である必要があり、アニメーション GIF はサポートされません。</span><span class="sxs-lookup"><span data-stu-id="39315-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="39315-144">プロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-144">Property</span></span> | <span data-ttu-id="39315-145">型</span><span class="sxs-lookup"><span data-stu-id="39315-145">Type</span></span>  | <span data-ttu-id="39315-146">説明</span><span class="sxs-lookup"><span data-stu-id="39315-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39315-147">url</span><span class="sxs-lookup"><span data-stu-id="39315-147">url</span></span> | <span data-ttu-id="39315-148">URL</span><span class="sxs-lookup"><span data-stu-id="39315-148">URL</span></span> | <span data-ttu-id="39315-149">イメージへの HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="39315-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="39315-150">alt</span><span class="sxs-lookup"><span data-stu-id="39315-150">alt</span></span> | <span data-ttu-id="39315-151">文字列</span><span class="sxs-lookup"><span data-stu-id="39315-151">String</span></span> | <span data-ttu-id="39315-152">画像のアクセス可能な説明。</span><span class="sxs-lookup"><span data-stu-id="39315-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="39315-153">カードに、最終イメージの前にリダイレクトを通過するイメージ URL が含まれている場合、イメージ URL のリダイレクトはサポートされません。</span><span class="sxs-lookup"><span data-stu-id="39315-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="39315-154">これは、パブリック クラウドで共有されているイメージに対して発生します。</span><span class="sxs-lookup"><span data-stu-id="39315-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="39315-155">ボタン</span><span class="sxs-lookup"><span data-stu-id="39315-155">Buttons</span></span>

<span data-ttu-id="39315-156">ボタンはカードの下部に上下に並んで表示されます。</span><span class="sxs-lookup"><span data-stu-id="39315-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="39315-157">ボタンテキストは常に 1 行で、テキストがボタンの幅を超えると切り捨てられます。</span><span class="sxs-lookup"><span data-stu-id="39315-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="39315-158">カードでサポートされている最大数を超える追加ボタンは表示されません。</span><span class="sxs-lookup"><span data-stu-id="39315-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="39315-159">詳細については、「 [カードアクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="39315-160">カードのフォーマット</span><span class="sxs-lookup"><span data-stu-id="39315-160">Card formatting</span></span>

<span data-ttu-id="39315-161">カードのテキストの書式設定の詳細については、「 [カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="39315-162">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="39315-162">Adaptive card</span></span>

<span data-ttu-id="39315-163">アダプティブ カードは、テキスト、音声、画像、ボタン、および入力フィールドの任意の組み合わせを含むことができるカスタマイズ可能なカードです。</span><span class="sxs-lookup"><span data-stu-id="39315-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="39315-164">詳細については、 [アダプティブ カード v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="39315-165">アダプティブカードのサポート</span><span class="sxs-lookup"><span data-stu-id="39315-165">Support for adaptive cards</span></span>

| <span data-ttu-id="39315-166">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="39315-166">Bots in Teams</span></span> | <span data-ttu-id="39315-167">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="39315-167">Messaging extensions</span></span>  | <span data-ttu-id="39315-168">コネクタ</span><span class="sxs-lookup"><span data-stu-id="39315-168">Connectors</span></span> | <span data-ttu-id="39315-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="39315-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39315-170">✔</span><span class="sxs-lookup"><span data-stu-id="39315-170">✔</span></span> | <span data-ttu-id="39315-171">✔</span><span class="sxs-lookup"><span data-stu-id="39315-171">✔</span></span> | <span data-ttu-id="39315-172">✖</span><span class="sxs-lookup"><span data-stu-id="39315-172">✖</span></span> | <span data-ttu-id="39315-173">✔</span><span class="sxs-lookup"><span data-stu-id="39315-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="39315-174">Teamsプラットフォームは、v1.2以前のアダプティブカード機能をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="39315-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="39315-175">メディア要素は、現在、Teams プラットフォームのアダプティブ カード v1.2 ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="39315-175">Media elements are currently not supported in adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="39315-176">アダプティブ カードの例</span><span class="sxs-lookup"><span data-stu-id="39315-176">Example of an adaptive card</span></span>

![アダプティブ カードの例](~/assets/images/cards/adaptivecard.png)

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="39315-178">アダプティブ カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="39315-178">Additional information on adaptive cards</span></span>

<span data-ttu-id="39315-179">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-179">Bot Framework reference:</span></span>

* [<span data-ttu-id="39315-180">アダプティブカードNode.js</span><span class="sxs-lookup"><span data-stu-id="39315-180">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="39315-181">アダプティブカードC#</span><span class="sxs-lookup"><span data-stu-id="39315-181">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="39315-182">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="39315-182">Hero card</span></span>

<span data-ttu-id="39315-183">通常、1 つの大きなイメージ、1 つ以上のボタン、およびテキストを含むカード。</span><span class="sxs-lookup"><span data-stu-id="39315-183">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="39315-184">ヒーローカードのサポート</span><span class="sxs-lookup"><span data-stu-id="39315-184">Support for hero cards</span></span>

| <span data-ttu-id="39315-185">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="39315-185">Bots in Teams</span></span> | <span data-ttu-id="39315-186">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="39315-186">Messaging extensions</span></span>  | <span data-ttu-id="39315-187">コネクタ</span><span class="sxs-lookup"><span data-stu-id="39315-187">Connectors</span></span> | <span data-ttu-id="39315-188">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="39315-188">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39315-189">✔</span><span class="sxs-lookup"><span data-stu-id="39315-189">✔</span></span> | <span data-ttu-id="39315-190">✔</span><span class="sxs-lookup"><span data-stu-id="39315-190">✔</span></span> | <span data-ttu-id="39315-191">✖</span><span class="sxs-lookup"><span data-stu-id="39315-191">✖</span></span> | <span data-ttu-id="39315-192">✔</span><span class="sxs-lookup"><span data-stu-id="39315-192">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="39315-193">ヒーローカードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-193">Properties of a hero card</span></span>

| <span data-ttu-id="39315-194">プロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-194">Property</span></span> | <span data-ttu-id="39315-195">型</span><span class="sxs-lookup"><span data-stu-id="39315-195">Type</span></span>  | <span data-ttu-id="39315-196">説明</span><span class="sxs-lookup"><span data-stu-id="39315-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39315-197">title</span><span class="sxs-lookup"><span data-stu-id="39315-197">title</span></span> | <span data-ttu-id="39315-198">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-198">Rich text</span></span> | <span data-ttu-id="39315-199">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="39315-199">Title of the card.</span></span> <span data-ttu-id="39315-200">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="39315-200">Maximum 2 lines.</span></span> |
| <span data-ttu-id="39315-201">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="39315-201">subtitle</span></span> | <span data-ttu-id="39315-202">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-202">Rich text</span></span> | <span data-ttu-id="39315-203">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="39315-203">Subtitle of the card.</span></span> <span data-ttu-id="39315-204">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="39315-204">Maximum 2 lines.</span></span>|
| <span data-ttu-id="39315-205">テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-205">text</span></span> | <span data-ttu-id="39315-206">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-206">Rich text</span></span> | <span data-ttu-id="39315-207">サブタイトルの下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="39315-207">Text appears under the subtitle.</span></span> <span data-ttu-id="39315-208">書式設定オプションについては、「 [カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-208">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="39315-209">images</span><span class="sxs-lookup"><span data-stu-id="39315-209">images</span></span> | <span data-ttu-id="39315-210">画像の配列</span><span class="sxs-lookup"><span data-stu-id="39315-210">Array of images</span></span> | <span data-ttu-id="39315-211">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="39315-211">Image displayed at the top of the card.</span></span> <span data-ttu-id="39315-212">アスペクト比 16:9.</span><span class="sxs-lookup"><span data-stu-id="39315-212">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="39315-213">buttons</span><span class="sxs-lookup"><span data-stu-id="39315-213">buttons</span></span> | <span data-ttu-id="39315-214">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="39315-214">Array of action objects</span></span> | <span data-ttu-id="39315-215">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="39315-215">Set of actions applicable to the current card.</span></span> <span data-ttu-id="39315-216">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="39315-216">Maximum 6.</span></span> |
| <span data-ttu-id="39315-217">tap</span><span class="sxs-lookup"><span data-stu-id="39315-217">tap</span></span> | <span data-ttu-id="39315-218">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="39315-218">Action object</span></span> | <span data-ttu-id="39315-219">ユーザーがカード自体をタップするとアクティブになります。</span><span class="sxs-lookup"><span data-stu-id="39315-219">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="39315-220">ヒーロー カードの例</span><span class="sxs-lookup"><span data-stu-id="39315-220">Example of a hero card</span></span>

![ヒーロー カードの例](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="39315-222">ヒーローカードの追加情報</span><span class="sxs-lookup"><span data-stu-id="39315-222">Additional information on hero cards</span></span>

<span data-ttu-id="39315-223">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-223">Bot Framework reference:</span></span>

* [<span data-ttu-id="39315-224">ヒーローカードNode.js</span><span class="sxs-lookup"><span data-stu-id="39315-224">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="39315-225">ヒーロー カード C#</span><span class="sxs-lookup"><span data-stu-id="39315-225">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="39315-226">リスト カード</span><span class="sxs-lookup"><span data-stu-id="39315-226">List card</span></span>

<span data-ttu-id="39315-227">リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。</span><span class="sxs-lookup"><span data-stu-id="39315-227">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="39315-228">リスト カードは、アイテムのスクロール リストを提供します。</span><span class="sxs-lookup"><span data-stu-id="39315-228">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="39315-229">リストカードのサポート</span><span class="sxs-lookup"><span data-stu-id="39315-229">Support for list cards</span></span>

| <span data-ttu-id="39315-230">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="39315-230">Bots in Teams</span></span> | <span data-ttu-id="39315-231">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="39315-231">Messaging extensions</span></span>  | <span data-ttu-id="39315-232">コネクタ</span><span class="sxs-lookup"><span data-stu-id="39315-232">Connectors</span></span> | <span data-ttu-id="39315-233">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="39315-233">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39315-234">✔</span><span class="sxs-lookup"><span data-stu-id="39315-234">✔</span></span> | <span data-ttu-id="39315-235">✖</span><span class="sxs-lookup"><span data-stu-id="39315-235">✖</span></span> | <span data-ttu-id="39315-236">✖</span><span class="sxs-lookup"><span data-stu-id="39315-236">✖</span></span> |<span data-ttu-id="39315-237">✔</span><span class="sxs-lookup"><span data-stu-id="39315-237">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="39315-238">リスト カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-238">Properties of a list card</span></span>

| <span data-ttu-id="39315-239">プロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-239">Property</span></span> | <span data-ttu-id="39315-240">型</span><span class="sxs-lookup"><span data-stu-id="39315-240">Type</span></span>  | <span data-ttu-id="39315-241">説明</span><span class="sxs-lookup"><span data-stu-id="39315-241">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39315-242">title</span><span class="sxs-lookup"><span data-stu-id="39315-242">title</span></span> | <span data-ttu-id="39315-243">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-243">Rich text</span></span> | <span data-ttu-id="39315-244">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="39315-244">Title of the card.</span></span> <span data-ttu-id="39315-245">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="39315-245">Maximum 2 lines.</span></span>|
| <span data-ttu-id="39315-246">アイテム</span><span class="sxs-lookup"><span data-stu-id="39315-246">items</span></span> | <span data-ttu-id="39315-247">リスト アイテムの配列</span><span class="sxs-lookup"><span data-stu-id="39315-247">Array of list items</span></span> ||
| <span data-ttu-id="39315-248">buttons</span><span class="sxs-lookup"><span data-stu-id="39315-248">buttons</span></span> | <span data-ttu-id="39315-249">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="39315-249">Array of action objects</span></span> | <span data-ttu-id="39315-250">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="39315-250">Set of actions applicable to the current card.</span></span> <span data-ttu-id="39315-251">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="39315-251">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="39315-252">リスト カードの例</span><span class="sxs-lookup"><span data-stu-id="39315-252">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="39315-253">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="39315-253">Office 365 connector card</span></span>

<span data-ttu-id="39315-254">Office 365コネクタ カードは、bot Framework ではなく、Teamsでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="39315-254">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="39315-255">このカードは、複数のセクション、フィールド、画像、アクションを含む柔軟なレイアウトを提供します。</span><span class="sxs-lookup"><span data-stu-id="39315-255">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="39315-256">Bot が使用できるように、このカードがコネクタ カードをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="39315-256">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="39315-257">コネクタ カードと O365 カードの違いについては[、Office 365 コネクタ カードの注意を](#notes-on-the-office-365-connector-card)参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-257">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="39315-258">Office 365 コネクタ カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="39315-258">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="39315-259">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="39315-259">Bots in Teams</span></span> | <span data-ttu-id="39315-260">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="39315-260">Messaging extensions</span></span>  | <span data-ttu-id="39315-261">コネクタ</span><span class="sxs-lookup"><span data-stu-id="39315-261">Connectors</span></span> | <span data-ttu-id="39315-262">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="39315-262">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39315-263">✔</span><span class="sxs-lookup"><span data-stu-id="39315-263">✔</span></span> | <span data-ttu-id="39315-264">✔</span><span class="sxs-lookup"><span data-stu-id="39315-264">✔</span></span> | <span data-ttu-id="39315-265">✔</span><span class="sxs-lookup"><span data-stu-id="39315-265">✔</span></span> | <span data-ttu-id="39315-266">✖</span><span class="sxs-lookup"><span data-stu-id="39315-266">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="39315-267">Office 365 コネクタ カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-267">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="39315-268">プロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-268">Property</span></span> | <span data-ttu-id="39315-269">型</span><span class="sxs-lookup"><span data-stu-id="39315-269">Type</span></span>  | <span data-ttu-id="39315-270">説明</span><span class="sxs-lookup"><span data-stu-id="39315-270">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39315-271">title</span><span class="sxs-lookup"><span data-stu-id="39315-271">title</span></span> | <span data-ttu-id="39315-272">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-272">Rich text</span></span> | <span data-ttu-id="39315-273">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="39315-273">Title of the card.</span></span> <span data-ttu-id="39315-274">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="39315-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="39315-275">概要</span><span class="sxs-lookup"><span data-stu-id="39315-275">summary</span></span> | <span data-ttu-id="39315-276">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-276">Rich text</span></span> | <span data-ttu-id="39315-277">カードの概要。</span><span class="sxs-lookup"><span data-stu-id="39315-277">Summary of the card.</span></span> <span data-ttu-id="39315-278">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="39315-278">Maximum 2 lines.</span></span> |
| <span data-ttu-id="39315-279">テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-279">text</span></span> | <span data-ttu-id="39315-280">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-280">Rich text</span></span> | <span data-ttu-id="39315-281">サブタイトルの下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="39315-281">Text appears under the subtitle.</span></span> <span data-ttu-id="39315-282">書式設定オプションについては、「 [カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-282">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="39315-283">themeColor</span><span class="sxs-lookup"><span data-stu-id="39315-283">themeColor</span></span> | <span data-ttu-id="39315-284">16 進数文字列</span><span class="sxs-lookup"><span data-stu-id="39315-284">HEX string</span></span> | <span data-ttu-id="39315-285">アプリケーション マニフェストから提供されるアクセントカラーをオーバーライドする色。</span><span class="sxs-lookup"><span data-stu-id="39315-285">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="39315-286">Office 365 コネクタ カードに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="39315-286">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="39315-287">Office 365コネクタカードは、[アクションカードアクション](/outlook/actionable-messages/card-reference#actioncard-action)を含むMicrosoft Teamsで正しく機能します。</span><span class="sxs-lookup"><span data-stu-id="39315-287">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="39315-288">コネクタのコネクタ カードを使用することと、ボットでコネクタ カードを使用する場合の重要な違いの 1 つは、カード アクションの処理です。</span><span class="sxs-lookup"><span data-stu-id="39315-288">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="39315-289">コネクタの場合、エンドポイントは HTTP POST を介してカード ペイロードを受信します。</span><span class="sxs-lookup"><span data-stu-id="39315-289">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="39315-290">Bot の場合、`HttpPOST` アクションが、アクション ID と本文のみを Bot に送信する `invoke` アクティビティをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="39315-290">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="39315-291">各コネクタ カードには最大 10 個のセクションを表示でき、各セクションには最大 5 つのイメージと 5 つのアクションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="39315-291">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="39315-292">メッセージ内の追加のセクション、画像、またはアクションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="39315-292">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="39315-293">すべてのテキストフィールドは、マークダウンとHTMLをサポートします。</span><span class="sxs-lookup"><span data-stu-id="39315-293">All text fields support markdown and HTML.</span></span> <span data-ttu-id="39315-294">メッセージでプロパティを設定することで、マークダウンまたは HTML を使用するセクションを制御できます `markdown` 。</span><span class="sxs-lookup"><span data-stu-id="39315-294">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="39315-295">既定では `markdown` 、 が `true` に設定されています。</span><span class="sxs-lookup"><span data-stu-id="39315-295">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="39315-296">HTML を使用する場合は、 `markdown` に設定 `false` します。</span><span class="sxs-lookup"><span data-stu-id="39315-296">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="39315-297">`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="39315-297">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="39315-298">のレンダリング スタイルを指定するには `activityImage` 、 `activityImageType` 次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="39315-298">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="39315-299">値</span><span class="sxs-lookup"><span data-stu-id="39315-299">Value</span></span> | <span data-ttu-id="39315-300">説明</span><span class="sxs-lookup"><span data-stu-id="39315-300">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="39315-301">デフォルト。 `activityImage` は円として切り取られます。</span><span class="sxs-lookup"><span data-stu-id="39315-301">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="39315-302">`activityImage` は長方形で表示され、アスペクト比を保持します。</span><span class="sxs-lookup"><span data-stu-id="39315-302">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="39315-303">コネクタ カードのプロパティに関するその他の詳細については、 [アクション可能なメッセージ カード のリファレンス](/outlook/actionable-messages/card-reference)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-303">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="39315-304">Microsoft Teamsが現在サポートしていないコネクタ カードのプロパティは、次の場合に限られます。</span><span class="sxs-lookup"><span data-stu-id="39315-304">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="39315-305">`startGroup`常に `true` Teamsのように扱われます</span><span class="sxs-lookup"><span data-stu-id="39315-305">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="39315-306">Office 365コネクタ カードの例</span><span class="sxs-lookup"><span data-stu-id="39315-306">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="39315-307">レシート カード</span><span class="sxs-lookup"><span data-stu-id="39315-307">Receipt card</span></span>

<span data-ttu-id="39315-308">Teamsはレシート カードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="39315-308">Teams supports receipt card.</span></span> <span data-ttu-id="39315-309">ボットがユーザーに領収書を提供できるようにするカードです。</span><span class="sxs-lookup"><span data-stu-id="39315-309">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="39315-310">通常、税や合計情報など、領収書に含める品目の一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="39315-310">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="39315-311">レシートカードのサポート</span><span class="sxs-lookup"><span data-stu-id="39315-311">Support for receipt cards</span></span>

| <span data-ttu-id="39315-312">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="39315-312">Bots in Teams</span></span> | <span data-ttu-id="39315-313">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="39315-313">Messaging extensions</span></span>  | <span data-ttu-id="39315-314">コネクタ</span><span class="sxs-lookup"><span data-stu-id="39315-314">Connectors</span></span> | <span data-ttu-id="39315-315">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="39315-315">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39315-316">✔</span><span class="sxs-lookup"><span data-stu-id="39315-316">✔</span></span> | <span data-ttu-id="39315-317">✔</span><span class="sxs-lookup"><span data-stu-id="39315-317">✔</span></span> | <span data-ttu-id="39315-318">✖</span><span class="sxs-lookup"><span data-stu-id="39315-318">✖</span></span> | <span data-ttu-id="39315-319">✔</span><span class="sxs-lookup"><span data-stu-id="39315-319">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="39315-320">レシート カードの例</span><span class="sxs-lookup"><span data-stu-id="39315-320">Example of a receipt card</span></span>

![レシート カードの例](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="39315-322">レシート カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="39315-322">Additional information on receipt cards</span></span>

<span data-ttu-id="39315-323">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-323">Bot Framework reference:</span></span>

* [<span data-ttu-id="39315-324">レシートカードNode.js</span><span class="sxs-lookup"><span data-stu-id="39315-324">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="39315-325">レシート カード C#</span><span class="sxs-lookup"><span data-stu-id="39315-325">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="39315-326">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="39315-326">Signin card</span></span>

<span data-ttu-id="39315-327">サインイン カードを使用すると、ボットはユーザーにサインインを要求できます。</span><span class="sxs-lookup"><span data-stu-id="39315-327">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="39315-328">これは、bot フレームワークで見られるのとは少し異なる形式でTeamsでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="39315-328">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="39315-329">Teamsのサインイン カードは、Teamsのサインイン カードが 2 つのアクションのみをサポートしている点を除き、bot Framework のサインイン カードと似ています。 `signin` `openUrl`</span><span class="sxs-lookup"><span data-stu-id="39315-329">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="39315-330">サインイン アクションは、サインイン カードだけでなく、Teams のすべてのカードで使用できます。</span><span class="sxs-lookup"><span data-stu-id="39315-330">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="39315-331">認証の詳細については、「[ボットの認証フローのMicrosoft Teams」を](~/bots/how-to/authentication/auth-flow-bot.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-331">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="39315-332">サインイン カードのサポート</span><span class="sxs-lookup"><span data-stu-id="39315-332">Support for signin cards</span></span>

| <span data-ttu-id="39315-333">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="39315-333">Bots in Teams</span></span> | <span data-ttu-id="39315-334">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="39315-334">Messaging extensions</span></span>  | <span data-ttu-id="39315-335">コネクタ</span><span class="sxs-lookup"><span data-stu-id="39315-335">Connectors</span></span> | <span data-ttu-id="39315-336">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="39315-336">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39315-337">✔</span><span class="sxs-lookup"><span data-stu-id="39315-337">✔</span></span> | <span data-ttu-id="39315-338">✖</span><span class="sxs-lookup"><span data-stu-id="39315-338">✖</span></span> | <span data-ttu-id="39315-339">✖</span><span class="sxs-lookup"><span data-stu-id="39315-339">✖</span></span> | <span data-ttu-id="39315-340">✔</span><span class="sxs-lookup"><span data-stu-id="39315-340">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="39315-341">サインイン カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="39315-341">Additional information on signin cards</span></span>

<span data-ttu-id="39315-342">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-342">Bot Framework reference:</span></span>

* [<span data-ttu-id="39315-343">サインイン カード Node.js</span><span class="sxs-lookup"><span data-stu-id="39315-343">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="39315-344">サインイン カード C#</span><span class="sxs-lookup"><span data-stu-id="39315-344">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="39315-345">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="39315-345">Thumbnail card</span></span>

<span data-ttu-id="39315-346">通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="39315-346">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="39315-347">サムネイルカードのサポート</span><span class="sxs-lookup"><span data-stu-id="39315-347">Support for thumbnail cards</span></span>

| <span data-ttu-id="39315-348">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="39315-348">Bots in Teams</span></span> | <span data-ttu-id="39315-349">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="39315-349">Messaging extensions</span></span>  | <span data-ttu-id="39315-350">コネクタ</span><span class="sxs-lookup"><span data-stu-id="39315-350">Connectors</span></span> | <span data-ttu-id="39315-351">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="39315-351">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39315-352">✔</span><span class="sxs-lookup"><span data-stu-id="39315-352">✔</span></span> | <span data-ttu-id="39315-353">✔</span><span class="sxs-lookup"><span data-stu-id="39315-353">✔</span></span> | <span data-ttu-id="39315-354">✖</span><span class="sxs-lookup"><span data-stu-id="39315-354">✖</span></span> | <span data-ttu-id="39315-355">✔</span><span class="sxs-lookup"><span data-stu-id="39315-355">✔</span></span> |

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="39315-357">サムネイル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-357">Properties of a thumbnail card</span></span>

| <span data-ttu-id="39315-358">プロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-358">Property</span></span> | <span data-ttu-id="39315-359">型</span><span class="sxs-lookup"><span data-stu-id="39315-359">Type</span></span>  | <span data-ttu-id="39315-360">説明</span><span class="sxs-lookup"><span data-stu-id="39315-360">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39315-361">title</span><span class="sxs-lookup"><span data-stu-id="39315-361">title</span></span> | <span data-ttu-id="39315-362">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-362">Rich text</span></span> | <span data-ttu-id="39315-363">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="39315-363">Title of the card.</span></span> <span data-ttu-id="39315-364">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="39315-364">Maximum 2 lines.</span></span>|
| <span data-ttu-id="39315-365">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="39315-365">subtitle</span></span> | <span data-ttu-id="39315-366">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-366">Rich text</span></span> | <span data-ttu-id="39315-367">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="39315-367">Subtitle of the card.</span></span> <span data-ttu-id="39315-368">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="39315-368">Maximum 2 lines.</span></span>|
| <span data-ttu-id="39315-369">テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-369">text</span></span> | <span data-ttu-id="39315-370">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="39315-370">Rich text</span></span> | <span data-ttu-id="39315-371">サブタイトルの下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="39315-371">Text appears under the subtitle.</span></span> <span data-ttu-id="39315-372">書式設定オプションについては、「 [カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-372">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="39315-373">images</span><span class="sxs-lookup"><span data-stu-id="39315-373">images</span></span> | <span data-ttu-id="39315-374">画像の配列</span><span class="sxs-lookup"><span data-stu-id="39315-374">Array of images</span></span> | <span data-ttu-id="39315-375">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="39315-375">Image displayed at the top of the card.</span></span> <span data-ttu-id="39315-376">アスペクト比 1:1 四角。</span><span class="sxs-lookup"><span data-stu-id="39315-376">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="39315-377">buttons</span><span class="sxs-lookup"><span data-stu-id="39315-377">buttons</span></span> | <span data-ttu-id="39315-378">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="39315-378">Array of action objects</span></span> | <span data-ttu-id="39315-379">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="39315-379">Set of actions applicable to the current card.</span></span> <span data-ttu-id="39315-380">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="39315-380">Maximum 6.</span></span> |
| <span data-ttu-id="39315-381">tap</span><span class="sxs-lookup"><span data-stu-id="39315-381">tap</span></span> | <span data-ttu-id="39315-382">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="39315-382">Action object</span></span> | <span data-ttu-id="39315-383">ユーザーがカード自体をタップするとアクティブになります。</span><span class="sxs-lookup"><span data-stu-id="39315-383">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="39315-384">サムネイル カードの例</span><span class="sxs-lookup"><span data-stu-id="39315-384">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="39315-385">追加情報</span><span class="sxs-lookup"><span data-stu-id="39315-385">Additional information</span></span>

<span data-ttu-id="39315-386">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="39315-386">Bot Framework reference:</span></span>

* [<span data-ttu-id="39315-387">サムネイル カード Node.js</span><span class="sxs-lookup"><span data-stu-id="39315-387">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="39315-388">サムネイル カード C#</span><span class="sxs-lookup"><span data-stu-id="39315-388">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="39315-389">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="39315-389">Card collections</span></span>

<span data-ttu-id="39315-390">Teamsカード コレクションをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="39315-390">Teams supports Card collections.</span></span>

<span data-ttu-id="39315-391">カード コレクションには `builder.AttachmentLayout.carousel` 、 および が含まれます `builder.AttachmentLayout.list` 。</span><span class="sxs-lookup"><span data-stu-id="39315-391">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="39315-392">これらのコレクションには、アダプティブ カード、ヒーロー カード、またはサムネイル カードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="39315-392">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="39315-393">カルーセル コレクション</span><span class="sxs-lookup"><span data-stu-id="39315-393">Carousel collection</span></span>

<span data-ttu-id="39315-394">[カルーセルのレイアウト](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="39315-394">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="39315-395">カルーセルコレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="39315-395">Support for carousel collections</span></span>

| <span data-ttu-id="39315-396">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="39315-396">Bots in Teams</span></span> | <span data-ttu-id="39315-397">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="39315-397">Messaging extensions</span></span>  | <span data-ttu-id="39315-398">コネクタ</span><span class="sxs-lookup"><span data-stu-id="39315-398">Connectors</span></span> | <span data-ttu-id="39315-399">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="39315-399">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39315-400">✔</span><span class="sxs-lookup"><span data-stu-id="39315-400">✔</span></span> | <span data-ttu-id="39315-401">✖</span><span class="sxs-lookup"><span data-stu-id="39315-401">✖</span></span> | <span data-ttu-id="39315-402">✖</span><span class="sxs-lookup"><span data-stu-id="39315-402">✖</span></span> | <span data-ttu-id="39315-403">✔</span><span class="sxs-lookup"><span data-stu-id="39315-403">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="39315-404">カルーセルは、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="39315-404">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="39315-405">カルーセル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="39315-405">Properties of a carousel card</span></span>

<span data-ttu-id="39315-406">カルーセルカードのプロパティは、ヒーローカードやサムネイルカードのプロパティと同じです。</span><span class="sxs-lookup"><span data-stu-id="39315-406">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="39315-407">カルーセル コレクションの例</span><span class="sxs-lookup"><span data-stu-id="39315-407">Example of a carousel collection</span></span>

![カードのカルーセルの例](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="39315-409">カルーセル コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="39315-409">Syntax for carousel collections</span></span>

<span data-ttu-id="39315-410">`builder.AttachmentLayoutTypes.Carousel` はカルーセル コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="39315-410">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="39315-411">リスト コレクション</span><span class="sxs-lookup"><span data-stu-id="39315-411">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="39315-412">リスト コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="39315-412">Support for list collections</span></span>

<span data-ttu-id="39315-413">リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="39315-413">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="39315-414">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="39315-414">Bots in Teams</span></span> | <span data-ttu-id="39315-415">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="39315-415">Messaging extensions</span></span>  | <span data-ttu-id="39315-416">コネクタ</span><span class="sxs-lookup"><span data-stu-id="39315-416">Connectors</span></span> | <span data-ttu-id="39315-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="39315-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39315-418">✔</span><span class="sxs-lookup"><span data-stu-id="39315-418">✔</span></span> | <span data-ttu-id="39315-419">✔</span><span class="sxs-lookup"><span data-stu-id="39315-419">✔</span></span> | <span data-ttu-id="39315-420">✖</span><span class="sxs-lookup"><span data-stu-id="39315-420">✖</span></span> | <span data-ttu-id="39315-421">✔</span><span class="sxs-lookup"><span data-stu-id="39315-421">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="39315-422">リスト コレクションの例</span><span class="sxs-lookup"><span data-stu-id="39315-422">Example of a list collection</span></span>

![カードのリストの例](~/assets/images/cards/list.png)

<span data-ttu-id="39315-424">プロパティは、ヒーローやサムネイル カードの場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="39315-424">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="39315-425">リストには、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="39315-425">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="39315-426">iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="39315-426">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="39315-427">リスト コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="39315-427">Syntax for list collections</span></span>

<span data-ttu-id="39315-428">`builder.AttachmentLayout.list` は、リスト コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="39315-428">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="39315-429">Teams でサポートされていないカード</span><span class="sxs-lookup"><span data-stu-id="39315-429">Cards not supported in Teams</span></span>

<span data-ttu-id="39315-430">次のカードは Bot フレームワークによって実装されますが、Teamsではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="39315-430">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="39315-431">アニメーション カード</span><span class="sxs-lookup"><span data-stu-id="39315-431">Animation cards</span></span>
* <span data-ttu-id="39315-432">オーディオ カード</span><span class="sxs-lookup"><span data-stu-id="39315-432">Audio cards</span></span>
* <span data-ttu-id="39315-433">ビデオ カード</span><span class="sxs-lookup"><span data-stu-id="39315-433">Video cards</span></span>
