---
title: カード リファレンス
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
localization_priority: Normal
keywords: Bot のカード リファレンス
ms.topic: reference
ms.openlocfilehash: 1e8cf2e474b8a74f6cab1cd6ef3439924b91892d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019532"
---
# <a name="cards-reference"></a><span data-ttu-id="319fb-104">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="319fb-104">Cards reference</span></span>

<span data-ttu-id="319fb-105">このドキュメントに記載されているカードは、ボットでサポートされているMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="319fb-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="319fb-106">これらは Bot Framework によって定義されたカードに基づいておりますが、Teams はボット フレームワーク カードの一部をサポートしているのではなく、一部の Teamsカードが追加されています。</span><span class="sxs-lookup"><span data-stu-id="319fb-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="319fb-107">相違点は、このドキュメントの参照で呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="319fb-108">カードの例</span><span class="sxs-lookup"><span data-stu-id="319fb-108">Card examples</span></span>

<span data-ttu-id="319fb-109">カードの使用方法に関する追加情報については、Bot Builder SDK v3 のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="319fb-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="319fb-110">コード サンプルは、Microsoft/BotBuilder-Samples リポジトリ (microsoft/BotBuilder-Samples リポジトリ) GitHub。</span><span class="sxs-lookup"><span data-stu-id="319fb-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="319fb-111">.NET</span><span class="sxs-lookup"><span data-stu-id="319fb-111">.NET</span></span>
  * [<span data-ttu-id="319fb-112">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="319fb-112">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="319fb-113">カードのサンプル コード Bot Builder v4</span><span class="sxs-lookup"><span data-stu-id="319fb-113">Cards sample code Bot Builder v4</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)

* <span data-ttu-id="319fb-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="319fb-114">Node.js</span></span>
  * [<span data-ttu-id="319fb-115">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="319fb-115">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="319fb-116">カードのサンプル コード Bot Builder v4</span><span class="sxs-lookup"><span data-stu-id="319fb-116">Cards sample code Bot Builder v4</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)

## <a name="types-of-cards"></a><span data-ttu-id="319fb-117">カードの種類</span><span class="sxs-lookup"><span data-stu-id="319fb-117">Types of cards</span></span>

<span data-ttu-id="319fb-118">次の表に、使用可能なカードの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="319fb-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="319fb-119">カードの種類</span><span class="sxs-lookup"><span data-stu-id="319fb-119">Card type</span></span> | <span data-ttu-id="319fb-120">説明</span><span class="sxs-lookup"><span data-stu-id="319fb-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="319fb-121">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="319fb-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="319fb-122">このカードは、テキスト、音声、画像、ボタン、および入力フィールドの任意の組み合わせを含む高度にカスタマイズ可能なカードです。</span><span class="sxs-lookup"><span data-stu-id="319fb-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="319fb-123">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="319fb-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="319fb-124">このカードには、通常、1 つの大きな画像、1 つ以上のボタン、および少量のテキストが含まれる。</span><span class="sxs-lookup"><span data-stu-id="319fb-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="319fb-125">リスト カード</span><span class="sxs-lookup"><span data-stu-id="319fb-125">List card</span></span>](#list-card) | <span data-ttu-id="319fb-126">このカードはアイテムのスクロール リストです。</span><span class="sxs-lookup"><span data-stu-id="319fb-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="319fb-127">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="319fb-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="319fb-128">このカードには、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトがあります。</span><span class="sxs-lookup"><span data-stu-id="319fb-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="319fb-129">レシート カード</span><span class="sxs-lookup"><span data-stu-id="319fb-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="319fb-130">このカードは、ユーザーにレシートを提供します。</span><span class="sxs-lookup"><span data-stu-id="319fb-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="319fb-131">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="319fb-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="319fb-132">このカードを使用すると、ボットはユーザーのサインインを要求できます。</span><span class="sxs-lookup"><span data-stu-id="319fb-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="319fb-133">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="319fb-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="319fb-134">このカードには、通常、1 つのサムネイル 画像、短いテキスト、および 1 つ以上のボタンが含まれる。</span><span class="sxs-lookup"><span data-stu-id="319fb-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="319fb-135">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="319fb-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="319fb-136">このカードは、1 つの応答で複数のアイテムを返す場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="319fb-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="319fb-137">すべてのカードの共通プロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="319fb-138">インライン カードの画像</span><span class="sxs-lookup"><span data-stu-id="319fb-138">Inline card images</span></span>

<span data-ttu-id="319fb-139">カードには、公開されている画像へのリンクを含め、インライン イメージを含めできます。</span><span class="sxs-lookup"><span data-stu-id="319fb-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="319fb-140">パフォーマンス上の目的で、パブリック コンテンツ配信ネットワーク (CDN) でイメージをホストすることを強くお勧CDN。</span><span class="sxs-lookup"><span data-stu-id="319fb-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="319fb-141">画像のサイズは拡大または縮小され、縦横比を維持して画像領域をカバーします。</span><span class="sxs-lookup"><span data-stu-id="319fb-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="319fb-142">次に、カードの適切な縦横比を実現するために、中央から画像がトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="319fb-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="319fb-143">画像は、PNG、JPEG、または GIF 形式×最大 1024、×1024 である必要があります。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="319fb-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="319fb-144">プロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-144">Property</span></span> | <span data-ttu-id="319fb-145">型</span><span class="sxs-lookup"><span data-stu-id="319fb-145">Type</span></span>  | <span data-ttu-id="319fb-146">説明</span><span class="sxs-lookup"><span data-stu-id="319fb-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="319fb-147">url</span><span class="sxs-lookup"><span data-stu-id="319fb-147">url</span></span> | <span data-ttu-id="319fb-148">URL</span><span class="sxs-lookup"><span data-stu-id="319fb-148">URL</span></span> | <span data-ttu-id="319fb-149">イメージの HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="319fb-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="319fb-150">alt</span><span class="sxs-lookup"><span data-stu-id="319fb-150">alt</span></span> | <span data-ttu-id="319fb-151">文字列</span><span class="sxs-lookup"><span data-stu-id="319fb-151">String</span></span> | <span data-ttu-id="319fb-152">画像のアクセス可能な説明。</span><span class="sxs-lookup"><span data-stu-id="319fb-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="319fb-153">最終的なイメージの前にリダイレクトを行うイメージ URL がカードに含まれる場合、イメージ URL のリダイレクトはサポートされません。</span><span class="sxs-lookup"><span data-stu-id="319fb-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="319fb-154">これは、パブリック クラウド上で共有されるイメージに対して発生します。</span><span class="sxs-lookup"><span data-stu-id="319fb-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="319fb-155">ボタン</span><span class="sxs-lookup"><span data-stu-id="319fb-155">Buttons</span></span>

<span data-ttu-id="319fb-156">ボタンはカードの下部に上下に並んで表示されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="319fb-157">ボタンのテキストは常に 1 行に表示され、テキストがボタンの幅を超えると切り捨てされます。</span><span class="sxs-lookup"><span data-stu-id="319fb-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="319fb-158">カードでサポートされている最大数を超える追加のボタンは表示されません。</span><span class="sxs-lookup"><span data-stu-id="319fb-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="319fb-159">詳細については、「カードアクション [」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="319fb-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="319fb-160">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="319fb-160">Card formatting</span></span>

<span data-ttu-id="319fb-161">カードのテキスト書式の詳細については、「カードの書式設定」 [を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="319fb-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="319fb-162">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="319fb-162">Adaptive card</span></span>

<span data-ttu-id="319fb-163">アダプティブ カードは、テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含むカスタマイズ可能なカードです。</span><span class="sxs-lookup"><span data-stu-id="319fb-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="319fb-164">アダプティブ [カード v1.2.0 を参照してください](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)。</span><span class="sxs-lookup"><span data-stu-id="319fb-164">See [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="319fb-165">アダプティブ カードのサポート</span><span class="sxs-lookup"><span data-stu-id="319fb-165">Support for adaptive cards</span></span>

| <span data-ttu-id="319fb-166">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="319fb-166">Bots in Teams</span></span> | <span data-ttu-id="319fb-167">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="319fb-167">Messaging extensions</span></span>  | <span data-ttu-id="319fb-168">コネクタ</span><span class="sxs-lookup"><span data-stu-id="319fb-168">Connectors</span></span> | <span data-ttu-id="319fb-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="319fb-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="319fb-170">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-170">✔</span></span> | <span data-ttu-id="319fb-171">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-171">✔</span></span> | <span data-ttu-id="319fb-172">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-172">✖</span></span> | <span data-ttu-id="319fb-173">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="319fb-174">Teamsプラットフォームは、v1.2 以前のアダプティブ カード機能をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="319fb-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="319fb-175">メディア要素は、現在、プラットフォーム上のアダプティブ カード v1.2 ではTeamsされていません。</span><span class="sxs-lookup"><span data-stu-id="319fb-175">Media elements are currently not supported in adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="319fb-176">アダプティブ カードの例</span><span class="sxs-lookup"><span data-stu-id="319fb-176">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="319fb-178">アダプティブ カードの追加情報</span><span class="sxs-lookup"><span data-stu-id="319fb-178">Additional information on adaptive cards</span></span>

<span data-ttu-id="319fb-179">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="319fb-179">Bot Framework reference:</span></span>

* [<span data-ttu-id="319fb-180">アダプティブ カードNode.js</span><span class="sxs-lookup"><span data-stu-id="319fb-180">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="319fb-181">アダプティブ カード C#</span><span class="sxs-lookup"><span data-stu-id="319fb-181">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="319fb-182">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="319fb-182">Hero card</span></span>

<span data-ttu-id="319fb-183">通常、1 つの大きな画像、1 つ以上のボタン、およびテキストを含むカード。</span><span class="sxs-lookup"><span data-stu-id="319fb-183">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="319fb-184">ヒーロー カードのサポート</span><span class="sxs-lookup"><span data-stu-id="319fb-184">Support for hero cards</span></span>

| <span data-ttu-id="319fb-185">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="319fb-185">Bots in Teams</span></span> | <span data-ttu-id="319fb-186">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="319fb-186">Messaging extensions</span></span>  | <span data-ttu-id="319fb-187">コネクタ</span><span class="sxs-lookup"><span data-stu-id="319fb-187">Connectors</span></span> | <span data-ttu-id="319fb-188">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="319fb-188">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="319fb-189">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-189">✔</span></span> | <span data-ttu-id="319fb-190">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-190">✔</span></span> | <span data-ttu-id="319fb-191">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-191">✖</span></span> | <span data-ttu-id="319fb-192">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-192">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="319fb-193">ヒーロー カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-193">Properties of a hero card</span></span>

| <span data-ttu-id="319fb-194">プロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-194">Property</span></span> | <span data-ttu-id="319fb-195">型</span><span class="sxs-lookup"><span data-stu-id="319fb-195">Type</span></span>  | <span data-ttu-id="319fb-196">説明</span><span class="sxs-lookup"><span data-stu-id="319fb-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="319fb-197">title</span><span class="sxs-lookup"><span data-stu-id="319fb-197">title</span></span> | <span data-ttu-id="319fb-198">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-198">Rich text</span></span> | <span data-ttu-id="319fb-199">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="319fb-199">Title of the card.</span></span> <span data-ttu-id="319fb-200">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="319fb-200">Maximum 2 lines.</span></span> |
| <span data-ttu-id="319fb-201">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="319fb-201">subtitle</span></span> | <span data-ttu-id="319fb-202">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-202">Rich text</span></span> | <span data-ttu-id="319fb-203">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="319fb-203">Subtitle of the card.</span></span> <span data-ttu-id="319fb-204">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="319fb-204">Maximum 2 lines.</span></span>|
| <span data-ttu-id="319fb-205">テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-205">text</span></span> | <span data-ttu-id="319fb-206">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-206">Rich text</span></span> | <span data-ttu-id="319fb-207">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-207">Text appears under the subtitle.</span></span> <span data-ttu-id="319fb-208">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="319fb-208">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="319fb-209">images</span><span class="sxs-lookup"><span data-stu-id="319fb-209">images</span></span> | <span data-ttu-id="319fb-210">画像の配列</span><span class="sxs-lookup"><span data-stu-id="319fb-210">Array of images</span></span> | <span data-ttu-id="319fb-211">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="319fb-211">Image displayed at the top of the card.</span></span> <span data-ttu-id="319fb-212">縦横比 16:9。</span><span class="sxs-lookup"><span data-stu-id="319fb-212">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="319fb-213">buttons</span><span class="sxs-lookup"><span data-stu-id="319fb-213">buttons</span></span> | <span data-ttu-id="319fb-214">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="319fb-214">Array of action objects</span></span> | <span data-ttu-id="319fb-215">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="319fb-215">Set of actions applicable to the current card.</span></span> <span data-ttu-id="319fb-216">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="319fb-216">Maximum 6.</span></span> |
| <span data-ttu-id="319fb-217">tap</span><span class="sxs-lookup"><span data-stu-id="319fb-217">tap</span></span> | <span data-ttu-id="319fb-218">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="319fb-218">Action object</span></span> | <span data-ttu-id="319fb-219">ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-219">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="319fb-220">ヒーロー カードの例</span><span class="sxs-lookup"><span data-stu-id="319fb-220">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="319fb-222">ヒーロー カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="319fb-222">Additional information on hero cards</span></span>

<span data-ttu-id="319fb-223">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="319fb-223">Bot Framework reference:</span></span>

* [<span data-ttu-id="319fb-224">ヒーロー カード Node.js</span><span class="sxs-lookup"><span data-stu-id="319fb-224">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="319fb-225">ヒーロー カード C#</span><span class="sxs-lookup"><span data-stu-id="319fb-225">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="319fb-226">リスト カード</span><span class="sxs-lookup"><span data-stu-id="319fb-226">List card</span></span>

<span data-ttu-id="319fb-227">リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。</span><span class="sxs-lookup"><span data-stu-id="319fb-227">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="319fb-228">リスト カードは、アイテムのスクロール リストを提供します。</span><span class="sxs-lookup"><span data-stu-id="319fb-228">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="319fb-229">リスト カードのサポート</span><span class="sxs-lookup"><span data-stu-id="319fb-229">Support for list cards</span></span>

| <span data-ttu-id="319fb-230">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="319fb-230">Bots in Teams</span></span> | <span data-ttu-id="319fb-231">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="319fb-231">Messaging extensions</span></span>  | <span data-ttu-id="319fb-232">コネクタ</span><span class="sxs-lookup"><span data-stu-id="319fb-232">Connectors</span></span> | <span data-ttu-id="319fb-233">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="319fb-233">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="319fb-234">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-234">✔</span></span> | <span data-ttu-id="319fb-235">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-235">✖</span></span> | <span data-ttu-id="319fb-236">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-236">✖</span></span> |<span data-ttu-id="319fb-237">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-237">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="319fb-238">リスト カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-238">Properties of a list card</span></span>

| <span data-ttu-id="319fb-239">プロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-239">Property</span></span> | <span data-ttu-id="319fb-240">型</span><span class="sxs-lookup"><span data-stu-id="319fb-240">Type</span></span>  | <span data-ttu-id="319fb-241">説明</span><span class="sxs-lookup"><span data-stu-id="319fb-241">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="319fb-242">title</span><span class="sxs-lookup"><span data-stu-id="319fb-242">title</span></span> | <span data-ttu-id="319fb-243">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-243">Rich text</span></span> | <span data-ttu-id="319fb-244">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="319fb-244">Title of the card.</span></span> <span data-ttu-id="319fb-245">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="319fb-245">Maximum 2 lines.</span></span>|
| <span data-ttu-id="319fb-246">アイテム</span><span class="sxs-lookup"><span data-stu-id="319fb-246">items</span></span> | <span data-ttu-id="319fb-247">リスト アイテムの配列</span><span class="sxs-lookup"><span data-stu-id="319fb-247">Array of list items</span></span> ||
| <span data-ttu-id="319fb-248">buttons</span><span class="sxs-lookup"><span data-stu-id="319fb-248">buttons</span></span> | <span data-ttu-id="319fb-249">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="319fb-249">Array of action objects</span></span> | <span data-ttu-id="319fb-250">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="319fb-250">Set of actions applicable to the current card.</span></span> <span data-ttu-id="319fb-251">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="319fb-251">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="319fb-252">リスト カードの例</span><span class="sxs-lookup"><span data-stu-id="319fb-252">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="319fb-253">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="319fb-253">Office 365 connector card</span></span>

<span data-ttu-id="319fb-254">コネクタ Office 365はボット フレームワークではなく、Teamsでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="319fb-254">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="319fb-255">このカードは、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトを提供します。</span><span class="sxs-lookup"><span data-stu-id="319fb-255">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="319fb-256">Bot が使用できるように、このカードがコネクタ カードをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="319fb-256">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="319fb-257">コネクタ カードと O365 カードの違いについては、「コネクタ カードに関するOffice 365[を参照してください](#notes-on-the-office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="319fb-257">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="319fb-258">Office 365 コネクタ カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="319fb-258">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="319fb-259">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="319fb-259">Bots in Teams</span></span> | <span data-ttu-id="319fb-260">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="319fb-260">Messaging extensions</span></span>  | <span data-ttu-id="319fb-261">コネクタ</span><span class="sxs-lookup"><span data-stu-id="319fb-261">Connectors</span></span> | <span data-ttu-id="319fb-262">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="319fb-262">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="319fb-263">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-263">✔</span></span> | <span data-ttu-id="319fb-264">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-264">✔</span></span> | <span data-ttu-id="319fb-265">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-265">✔</span></span> | <span data-ttu-id="319fb-266">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-266">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="319fb-267">Office 365 コネクタ カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-267">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="319fb-268">プロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-268">Property</span></span> | <span data-ttu-id="319fb-269">型</span><span class="sxs-lookup"><span data-stu-id="319fb-269">Type</span></span>  | <span data-ttu-id="319fb-270">説明</span><span class="sxs-lookup"><span data-stu-id="319fb-270">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="319fb-271">title</span><span class="sxs-lookup"><span data-stu-id="319fb-271">title</span></span> | <span data-ttu-id="319fb-272">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-272">Rich text</span></span> | <span data-ttu-id="319fb-273">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="319fb-273">Title of the card.</span></span> <span data-ttu-id="319fb-274">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="319fb-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="319fb-275">概要</span><span class="sxs-lookup"><span data-stu-id="319fb-275">summary</span></span> | <span data-ttu-id="319fb-276">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-276">Rich text</span></span> | <span data-ttu-id="319fb-277">カードの概要。</span><span class="sxs-lookup"><span data-stu-id="319fb-277">Summary of the card.</span></span> <span data-ttu-id="319fb-278">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="319fb-278">Maximum 2 lines.</span></span> |
| <span data-ttu-id="319fb-279">テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-279">text</span></span> | <span data-ttu-id="319fb-280">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-280">Rich text</span></span> | <span data-ttu-id="319fb-281">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-281">Text appears under the subtitle.</span></span> <span data-ttu-id="319fb-282">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="319fb-282">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="319fb-283">themeColor</span><span class="sxs-lookup"><span data-stu-id="319fb-283">themeColor</span></span> | <span data-ttu-id="319fb-284">16 進数文字列</span><span class="sxs-lookup"><span data-stu-id="319fb-284">HEX string</span></span> | <span data-ttu-id="319fb-285">アプリケーション マニフェストから提供される accentColor を上書きする色。</span><span class="sxs-lookup"><span data-stu-id="319fb-285">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="319fb-286">Office 365 コネクタ カードに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="319fb-286">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="319fb-287">Office 365カードは、ActionCard アクションなど、Microsoft Teamsで[適切に機能します](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="319fb-287">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="319fb-288">コネクタからコネクタ カードを使用する場合とボットでコネクタ カードを使用する場合の重要な違いの 1 つは、カードアクションの処理です。</span><span class="sxs-lookup"><span data-stu-id="319fb-288">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="319fb-289">コネクタの場合、エンドポイントは HTTP POST を介してカード ペイロードを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="319fb-289">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="319fb-290">Bot の場合、`HttpPOST` アクションが、アクション ID と本文のみを Bot に送信する `invoke` アクティビティをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="319fb-290">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="319fb-291">各コネクタ カードには最大 10 個のセクションを表示できます。各セクションには最大 5 つのイメージと 5 つのアクションを含めできます。</span><span class="sxs-lookup"><span data-stu-id="319fb-291">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="319fb-292">メッセージ内の追加のセクション、イメージ、またはアクションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="319fb-292">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="319fb-293">すべてのテキスト フィールドは、マークダウンと HTML をサポートします。</span><span class="sxs-lookup"><span data-stu-id="319fb-293">All text fields support markdown and HTML.</span></span> <span data-ttu-id="319fb-294">メッセージ内のプロパティを設定することで、マークダウンまたは HTML を使用 `markdown` するセクションを制御できます。</span><span class="sxs-lookup"><span data-stu-id="319fb-294">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="319fb-295">既定では `markdown` 、 に設定されています `true` 。</span><span class="sxs-lookup"><span data-stu-id="319fb-295">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="319fb-296">HTML を代わりに使用する場合は、 に `markdown` 設定します `false` 。</span><span class="sxs-lookup"><span data-stu-id="319fb-296">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="319fb-297">`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-297">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="319fb-298">レンダリング スタイルを指定するには `activityImage` 、次のように `activityImageType` 設定できます。</span><span class="sxs-lookup"><span data-stu-id="319fb-298">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="319fb-299">値</span><span class="sxs-lookup"><span data-stu-id="319fb-299">Value</span></span> | <span data-ttu-id="319fb-300">説明</span><span class="sxs-lookup"><span data-stu-id="319fb-300">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="319fb-301">既定値。 `activityImage` は、円としてトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="319fb-301">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="319fb-302">`activityImage` は四角形として表示され、縦横比が保持されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-302">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="319fb-303">コネクタ カードのプロパティに関するその他の詳細については、「アクション可能な [メッセージ カードリファレンス」を参照してください](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="319fb-303">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="319fb-304">現在サポートされていないコネクタ Microsoft Teamsのプロパティは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="319fb-304">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="319fb-305">`startGroup`常に、次のように `true` 処理Teams</span><span class="sxs-lookup"><span data-stu-id="319fb-305">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="319fb-306">コネクタ カードOffice 365例</span><span class="sxs-lookup"><span data-stu-id="319fb-306">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="319fb-307">レシート カード</span><span class="sxs-lookup"><span data-stu-id="319fb-307">Receipt card</span></span>

<span data-ttu-id="319fb-308">Teamsカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="319fb-308">Teams supports receipt card.</span></span> <span data-ttu-id="319fb-309">ボットがユーザーにレシートを提供できるカードです。</span><span class="sxs-lookup"><span data-stu-id="319fb-309">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="319fb-310">通常、税金や合計情報など、領収書に含めるアイテムの一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="319fb-310">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="319fb-311">レシート カードのサポート</span><span class="sxs-lookup"><span data-stu-id="319fb-311">Support for receipt cards</span></span>

| <span data-ttu-id="319fb-312">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="319fb-312">Bots in Teams</span></span> | <span data-ttu-id="319fb-313">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="319fb-313">Messaging extensions</span></span>  | <span data-ttu-id="319fb-314">コネクタ</span><span class="sxs-lookup"><span data-stu-id="319fb-314">Connectors</span></span> | <span data-ttu-id="319fb-315">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="319fb-315">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="319fb-316">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-316">✔</span></span> | <span data-ttu-id="319fb-317">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-317">✔</span></span> | <span data-ttu-id="319fb-318">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-318">✖</span></span> | <span data-ttu-id="319fb-319">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-319">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="319fb-320">レシート カードの例</span><span class="sxs-lookup"><span data-stu-id="319fb-320">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="319fb-322">レシート カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="319fb-322">Additional information on receipt cards</span></span>

<span data-ttu-id="319fb-323">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="319fb-323">Bot Framework reference:</span></span>

* [<span data-ttu-id="319fb-324">レシート カードNode.js</span><span class="sxs-lookup"><span data-stu-id="319fb-324">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="319fb-325">レシート カード C#</span><span class="sxs-lookup"><span data-stu-id="319fb-325">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="319fb-326">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="319fb-326">Signin card</span></span>

<span data-ttu-id="319fb-327">Signin card を使用すると、ボットはユーザーにサインインを要求できます。</span><span class="sxs-lookup"><span data-stu-id="319fb-327">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="319fb-328">これは、ボット フレームワークTeams少し異なる形式でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="319fb-328">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="319fb-329">Teams のサインイン カードはボット フレームワークのサインイン カードに似ていますが、Teams のサインイン カードは 2 つのアクションのみをサポートしています。 `signin` `openUrl`</span><span class="sxs-lookup"><span data-stu-id="319fb-329">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="319fb-330">サインイン アクションは、サインイン カードだけでなく、Teams のすべてのカードで使用できます。</span><span class="sxs-lookup"><span data-stu-id="319fb-330">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="319fb-331">認証の詳細については、「ボットMicrosoft Teams[認証フロー」を参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="319fb-331">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="319fb-332">サインイン カードのサポート</span><span class="sxs-lookup"><span data-stu-id="319fb-332">Support for signin cards</span></span>

| <span data-ttu-id="319fb-333">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="319fb-333">Bots in Teams</span></span> | <span data-ttu-id="319fb-334">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="319fb-334">Messaging extensions</span></span>  | <span data-ttu-id="319fb-335">コネクタ</span><span class="sxs-lookup"><span data-stu-id="319fb-335">Connectors</span></span> | <span data-ttu-id="319fb-336">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="319fb-336">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="319fb-337">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-337">✔</span></span> | <span data-ttu-id="319fb-338">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-338">✖</span></span> | <span data-ttu-id="319fb-339">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-339">✖</span></span> | <span data-ttu-id="319fb-340">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-340">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="319fb-341">サインイン カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="319fb-341">Additional information on signin cards</span></span>

<span data-ttu-id="319fb-342">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="319fb-342">Bot Framework reference:</span></span>

* [<span data-ttu-id="319fb-343">Signin カード Node.js</span><span class="sxs-lookup"><span data-stu-id="319fb-343">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="319fb-344">サインイン カード C#</span><span class="sxs-lookup"><span data-stu-id="319fb-344">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="319fb-345">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="319fb-345">Thumbnail card</span></span>

<span data-ttu-id="319fb-346">通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="319fb-346">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="319fb-347">サムネイル カードのサポート</span><span class="sxs-lookup"><span data-stu-id="319fb-347">Support for thumbnail cards</span></span>

| <span data-ttu-id="319fb-348">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="319fb-348">Bots in Teams</span></span> | <span data-ttu-id="319fb-349">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="319fb-349">Messaging extensions</span></span>  | <span data-ttu-id="319fb-350">コネクタ</span><span class="sxs-lookup"><span data-stu-id="319fb-350">Connectors</span></span> | <span data-ttu-id="319fb-351">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="319fb-351">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="319fb-352">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-352">✔</span></span> | <span data-ttu-id="319fb-353">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-353">✔</span></span> | <span data-ttu-id="319fb-354">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-354">✖</span></span> | <span data-ttu-id="319fb-355">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-355">✔</span></span> |

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="319fb-357">サムネイル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-357">Properties of a thumbnail card</span></span>

| <span data-ttu-id="319fb-358">プロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-358">Property</span></span> | <span data-ttu-id="319fb-359">型</span><span class="sxs-lookup"><span data-stu-id="319fb-359">Type</span></span>  | <span data-ttu-id="319fb-360">説明</span><span class="sxs-lookup"><span data-stu-id="319fb-360">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="319fb-361">title</span><span class="sxs-lookup"><span data-stu-id="319fb-361">title</span></span> | <span data-ttu-id="319fb-362">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-362">Rich text</span></span> | <span data-ttu-id="319fb-363">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="319fb-363">Title of the card.</span></span> <span data-ttu-id="319fb-364">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="319fb-364">Maximum 2 lines.</span></span>|
| <span data-ttu-id="319fb-365">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="319fb-365">subtitle</span></span> | <span data-ttu-id="319fb-366">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-366">Rich text</span></span> | <span data-ttu-id="319fb-367">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="319fb-367">Subtitle of the card.</span></span> <span data-ttu-id="319fb-368">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="319fb-368">Maximum 2 lines.</span></span>|
| <span data-ttu-id="319fb-369">テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-369">text</span></span> | <span data-ttu-id="319fb-370">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="319fb-370">Rich text</span></span> | <span data-ttu-id="319fb-371">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-371">Text appears under the subtitle.</span></span> <span data-ttu-id="319fb-372">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="319fb-372">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="319fb-373">images</span><span class="sxs-lookup"><span data-stu-id="319fb-373">images</span></span> | <span data-ttu-id="319fb-374">画像の配列</span><span class="sxs-lookup"><span data-stu-id="319fb-374">Array of images</span></span> | <span data-ttu-id="319fb-375">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="319fb-375">Image displayed at the top of the card.</span></span> <span data-ttu-id="319fb-376">縦横比 1:1 平方</span><span class="sxs-lookup"><span data-stu-id="319fb-376">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="319fb-377">buttons</span><span class="sxs-lookup"><span data-stu-id="319fb-377">buttons</span></span> | <span data-ttu-id="319fb-378">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="319fb-378">Array of action objects</span></span> | <span data-ttu-id="319fb-379">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="319fb-379">Set of actions applicable to the current card.</span></span> <span data-ttu-id="319fb-380">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="319fb-380">Maximum 6.</span></span> |
| <span data-ttu-id="319fb-381">tap</span><span class="sxs-lookup"><span data-stu-id="319fb-381">tap</span></span> | <span data-ttu-id="319fb-382">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="319fb-382">Action object</span></span> | <span data-ttu-id="319fb-383">ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-383">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="319fb-384">サムネイル カードの例</span><span class="sxs-lookup"><span data-stu-id="319fb-384">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="319fb-385">追加情報</span><span class="sxs-lookup"><span data-stu-id="319fb-385">Additional information</span></span>

<span data-ttu-id="319fb-386">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="319fb-386">Bot Framework reference:</span></span>

* [<span data-ttu-id="319fb-387">サムネイル カード Node.js</span><span class="sxs-lookup"><span data-stu-id="319fb-387">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="319fb-388">サムネイル カード C#</span><span class="sxs-lookup"><span data-stu-id="319fb-388">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="319fb-389">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="319fb-389">Card collections</span></span>

<span data-ttu-id="319fb-390">Teams Card コレクションをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="319fb-390">Teams supports Card collections.</span></span>

<span data-ttu-id="319fb-391">カード コレクションには、 `builder.AttachmentLayout.carousel` と が含まれます `builder.AttachmentLayout.list` 。</span><span class="sxs-lookup"><span data-stu-id="319fb-391">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="319fb-392">これらのコレクションには、アダプティブ カード、ヒーロー カード、またはサムネイル カードが含まれる。</span><span class="sxs-lookup"><span data-stu-id="319fb-392">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="319fb-393">カルーセル コレクション</span><span class="sxs-lookup"><span data-stu-id="319fb-393">Carousel collection</span></span>

<span data-ttu-id="319fb-394">[カルーセルのレイアウト](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-394">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="319fb-395">カルーセル コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="319fb-395">Support for carousel collections</span></span>

| <span data-ttu-id="319fb-396">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="319fb-396">Bots in Teams</span></span> | <span data-ttu-id="319fb-397">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="319fb-397">Messaging extensions</span></span>  | <span data-ttu-id="319fb-398">コネクタ</span><span class="sxs-lookup"><span data-stu-id="319fb-398">Connectors</span></span> | <span data-ttu-id="319fb-399">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="319fb-399">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="319fb-400">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-400">✔</span></span> | <span data-ttu-id="319fb-401">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-401">✖</span></span> | <span data-ttu-id="319fb-402">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-402">✖</span></span> | <span data-ttu-id="319fb-403">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-403">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="319fb-404">カルーセルは、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="319fb-404">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="319fb-405">カルーセル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="319fb-405">Properties of a carousel card</span></span>

<span data-ttu-id="319fb-406">カルーセル カードのプロパティは、ヒーロー カードとサムネイル カードのプロパティと同じです。</span><span class="sxs-lookup"><span data-stu-id="319fb-406">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="319fb-407">カルーセル コレクションの例</span><span class="sxs-lookup"><span data-stu-id="319fb-407">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="319fb-409">カルーセル コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="319fb-409">Syntax for carousel collections</span></span>

<span data-ttu-id="319fb-410">`builder.AttachmentLayoutTypes.Carousel` はカルーセル コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="319fb-410">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="319fb-411">リスト コレクション</span><span class="sxs-lookup"><span data-stu-id="319fb-411">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="319fb-412">リスト コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="319fb-412">Support for list collections</span></span>

<span data-ttu-id="319fb-413">リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="319fb-413">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="319fb-414">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="319fb-414">Bots in Teams</span></span> | <span data-ttu-id="319fb-415">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="319fb-415">Messaging extensions</span></span>  | <span data-ttu-id="319fb-416">コネクタ</span><span class="sxs-lookup"><span data-stu-id="319fb-416">Connectors</span></span> | <span data-ttu-id="319fb-417">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="319fb-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="319fb-418">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-418">✔</span></span> | <span data-ttu-id="319fb-419">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-419">✔</span></span> | <span data-ttu-id="319fb-420">✖</span><span class="sxs-lookup"><span data-stu-id="319fb-420">✖</span></span> | <span data-ttu-id="319fb-421">✔</span><span class="sxs-lookup"><span data-stu-id="319fb-421">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="319fb-422">リスト コレクションの例</span><span class="sxs-lookup"><span data-stu-id="319fb-422">Example of a list collection</span></span>

![カードのリストの例](~/assets/images/cards/list.png)

<span data-ttu-id="319fb-424">プロパティは、ヒーローやサムネイル カードの場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="319fb-424">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="319fb-425">リストには、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="319fb-425">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="319fb-426">iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="319fb-426">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="319fb-427">リスト コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="319fb-427">Syntax for list collections</span></span>

<span data-ttu-id="319fb-428">`builder.AttachmentLayout.list` はリスト コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="319fb-428">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="319fb-429">Teams でサポートされていないカード</span><span class="sxs-lookup"><span data-stu-id="319fb-429">Cards not supported in Teams</span></span>

<span data-ttu-id="319fb-430">次のカードは Bot Framework によって実装されますが、ボット フレームワークではTeams。</span><span class="sxs-lookup"><span data-stu-id="319fb-430">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="319fb-431">アニメーション カード</span><span class="sxs-lookup"><span data-stu-id="319fb-431">Animation cards</span></span>
* <span data-ttu-id="319fb-432">オーディオ カード</span><span class="sxs-lookup"><span data-stu-id="319fb-432">Audio cards</span></span>
* <span data-ttu-id="319fb-433">ビデオ カード</span><span class="sxs-lookup"><span data-stu-id="319fb-433">Video cards</span></span>
