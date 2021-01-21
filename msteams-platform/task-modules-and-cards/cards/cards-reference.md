---
title: カード リファレンス
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
keywords: Bot のカード リファレンス
ms.topic: reference
ms.openlocfilehash: 839430baa5ce5e8950a21a1472036c6fd96f4edf
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911901"
---
# <a name="cards-reference"></a><span data-ttu-id="eebb0-104">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="eebb0-104">Cards reference</span></span>

<span data-ttu-id="eebb0-105">このセクションに記載されているカードは、Microsoft Teams のボットでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-105">The cards listed in this section are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="eebb0-106">Bot Framework で定義されたカードに基づいていますが、すべての Bot Framework カードが Teams でサポートされているわけではなく、独自のカードがいくつか追加されています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="eebb0-107">このドキュメントのリファレンスでは、相違点について説明します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="eebb0-108">カードの例</span><span class="sxs-lookup"><span data-stu-id="eebb0-108">Card examples</span></span>

<span data-ttu-id="eebb0-109">カードの使用方法の詳細については、Bot Builder SDK (v3) のドキュメントで確認できます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="eebb0-110">コード サンプルは、GitHub の Microsoft/BotBuilder-Samples リポジトリでも利用できます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="eebb0-111">.NET</span><span class="sxs-lookup"><span data-stu-id="eebb0-111">.NET</span></span>
  * [<span data-ttu-id="eebb0-112">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="eebb0-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="eebb0-113">カード サンプル コード (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="eebb0-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="eebb0-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="eebb0-114">Node.js</span></span>
  * [<span data-ttu-id="eebb0-115">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="eebb0-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="eebb0-116">カード サンプル コード (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="eebb0-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="eebb0-117">カードの種類</span><span class="sxs-lookup"><span data-stu-id="eebb0-117">Types of cards</span></span>

<span data-ttu-id="eebb0-118">次の表に、使用可能なカードの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="eebb0-119">カードの種類</span><span class="sxs-lookup"><span data-stu-id="eebb0-119">Card type</span></span> | <span data-ttu-id="eebb0-120">説明</span><span class="sxs-lookup"><span data-stu-id="eebb0-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="eebb0-121">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="eebb0-122">高度なカスタマイズができるカード。テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせが可能です。</span><span class="sxs-lookup"><span data-stu-id="eebb0-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="eebb0-123">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="eebb0-124">通常、1 つの大きな画像、1 つまたは複数のボタン、少量のテキストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="eebb0-125">カードを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="eebb0-125">List card</span></span>](#list-card) | <span data-ttu-id="eebb0-126">アイテムのスクロール リスト。</span><span class="sxs-lookup"><span data-stu-id="eebb0-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="eebb0-127">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="eebb0-128">複数のセクション、フィールド、画像、アクションに対応した柔軟なレイアウトです。</span><span class="sxs-lookup"><span data-stu-id="eebb0-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="eebb0-129">レシート カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="eebb0-130">ユーザーに受領確認を提供します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="eebb0-131">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="eebb0-132">Bot がユーザーのサインインを要求できるようにします。</span><span class="sxs-lookup"><span data-stu-id="eebb0-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="eebb0-133">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="eebb0-134">通常、1 つのサムネイル画像、短いテキスト、1 つまたは複数のボタンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="eebb0-135">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="eebb0-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="eebb0-136">1 つの応答で複数のアイテムを返す場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-136">Used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="eebb0-137">すべてのカードの共通プロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="eebb0-138">インライン カードの画像</span><span class="sxs-lookup"><span data-stu-id="eebb0-138">Inline card images</span></span>

<span data-ttu-id="eebb0-139">カードには、公開されている画像へのリンクを含めてインライン画像を含めできます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="eebb0-140">パフォーマンスを向上させる目的で、パブリック コンテンツ配信ネットワーク (CDN) でイメージをホストすることを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="eebb0-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="eebb0-141">画像領域をカバーするように縦横比を保持しながらサイズを拡大または縮小し、カードの縦横比が適切になるように中央からトリミングします。</span><span class="sxs-lookup"><span data-stu-id="eebb0-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="eebb0-142">画像は PNG、JPEG、または GIF 形式で最大 1024×1024 である必要があります。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="eebb0-142">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and animated GIF is not supported.</span></span>

| <span data-ttu-id="eebb0-143">プロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-143">Property</span></span> | <span data-ttu-id="eebb0-144">型</span><span class="sxs-lookup"><span data-stu-id="eebb0-144">Type</span></span>  | <span data-ttu-id="eebb0-145">説明</span><span class="sxs-lookup"><span data-stu-id="eebb0-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eebb0-146">url</span><span class="sxs-lookup"><span data-stu-id="eebb0-146">url</span></span> | <span data-ttu-id="eebb0-147">URL</span><span class="sxs-lookup"><span data-stu-id="eebb0-147">URL</span></span> | <span data-ttu-id="eebb0-148">画像の HTTPS URL</span><span class="sxs-lookup"><span data-stu-id="eebb0-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="eebb0-149">alt</span><span class="sxs-lookup"><span data-stu-id="eebb0-149">alt</span></span> | <span data-ttu-id="eebb0-150">文字列</span><span class="sxs-lookup"><span data-stu-id="eebb0-150">String</span></span> | <span data-ttu-id="eebb0-151">画像へのアクセスに関する説明</span><span class="sxs-lookup"><span data-stu-id="eebb0-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="eebb0-152">ボタン</span><span class="sxs-lookup"><span data-stu-id="eebb0-152">Buttons</span></span>

<span data-ttu-id="eebb0-153">ボタンはカードの下部に上下に並んで表示されます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="eebb0-154">ボタンのテキストは常に 1 行で表示され、テキストがボタンの幅を超えた場合は切り捨てられます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="eebb0-155">カードでサポートされている最大数を超えるボタンは表示されません。</span><span class="sxs-lookup"><span data-stu-id="eebb0-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="eebb0-156">詳細については、「[カード アクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="eebb0-157">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="eebb0-157">Card formatting</span></span>

<span data-ttu-id="eebb0-158">カードのテキストの書式設定の詳細については、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="eebb0-159">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-159">Adaptive card</span></span>

<span data-ttu-id="eebb0-160">アダプティブ カードは、テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含むカスタマイズ可能なカードです。</span><span class="sxs-lookup"><span data-stu-id="eebb0-160">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="eebb0-161">アダプティブ [カード v1.2.0 をご覧ください](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)。</span><span class="sxs-lookup"><span data-stu-id="eebb0-161">See [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="eebb0-162">アダプティブ カードのサポート</span><span class="sxs-lookup"><span data-stu-id="eebb0-162">Support for adaptive cards</span></span>

| <span data-ttu-id="eebb0-163">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="eebb0-163">Bots in Teams</span></span> | <span data-ttu-id="eebb0-164">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eebb0-164">Messaging extensions</span></span>  | <span data-ttu-id="eebb0-165">コネクタ</span><span class="sxs-lookup"><span data-stu-id="eebb0-165">Connectors</span></span> | <span data-ttu-id="eebb0-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eebb0-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eebb0-167">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-167">✔</span></span> | <span data-ttu-id="eebb0-168">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-168">✔</span></span> | <span data-ttu-id="eebb0-169">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-169">✖</span></span> | <span data-ttu-id="eebb0-170">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-170">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="eebb0-171">Teams プラットフォームは、アダプティブ カード機能の v1.2 以前をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="eebb0-172">メディア要素は現在、Teams プラットフォームのアダプティブ カード v1.2 ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="eebb0-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="eebb0-173">アダプティブ カードの例</span><span class="sxs-lookup"><span data-stu-id="eebb0-173">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="eebb0-175">アダプティブ カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="eebb0-175">Additional information on adaptive cards</span></span>

* [<span data-ttu-id="eebb0-176">アダプティブ カードの概要</span><span class="sxs-lookup"><span data-stu-id="eebb0-176">Adaptive cards overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="eebb0-177">Teams でのアダプティブ カードのアクション</span><span class="sxs-lookup"><span data-stu-id="eebb0-177">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="eebb0-178">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-178">Hero card</span></span>

<span data-ttu-id="eebb0-179">通常、1 つの大きな画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="eebb0-179">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="eebb0-180">ヒーロー カードのサポート</span><span class="sxs-lookup"><span data-stu-id="eebb0-180">Support for hero cards</span></span>

| <span data-ttu-id="eebb0-181">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="eebb0-181">Bots in Teams</span></span> | <span data-ttu-id="eebb0-182">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eebb0-182">Messaging Extensions</span></span>  | <span data-ttu-id="eebb0-183">コネクタ</span><span class="sxs-lookup"><span data-stu-id="eebb0-183">Connectors</span></span> | <span data-ttu-id="eebb0-184">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eebb0-184">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eebb0-185">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-185">✔</span></span> | <span data-ttu-id="eebb0-186">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-186">✔</span></span> | <span data-ttu-id="eebb0-187">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-187">✖</span></span> | <span data-ttu-id="eebb0-188">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-188">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="eebb0-189">ヒーロー カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-189">Properties of a hero card</span></span>

| <span data-ttu-id="eebb0-190">プロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-190">Property</span></span> | <span data-ttu-id="eebb0-191">種類</span><span class="sxs-lookup"><span data-stu-id="eebb0-191">Type</span></span>  | <span data-ttu-id="eebb0-192">説明</span><span class="sxs-lookup"><span data-stu-id="eebb0-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eebb0-193">title</span><span class="sxs-lookup"><span data-stu-id="eebb0-193">title</span></span> | <span data-ttu-id="eebb0-194">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-194">Rich text</span></span> | <span data-ttu-id="eebb0-195">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="eebb0-195">Title of the card.</span></span> <span data-ttu-id="eebb0-196">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="eebb0-196">Maximum 2 lines.</span></span> |
| <span data-ttu-id="eebb0-197">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="eebb0-197">subtitle</span></span> | <span data-ttu-id="eebb0-198">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-198">Rich text</span></span> | <span data-ttu-id="eebb0-199">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="eebb0-199">Subtitle of the card.</span></span> <span data-ttu-id="eebb0-200">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="eebb0-200">Maximum 2 lines.</span></span>|
| <span data-ttu-id="eebb0-201">テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-201">text</span></span> | <span data-ttu-id="eebb0-202">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-202">Rich text</span></span> | <span data-ttu-id="eebb0-203">テキストは字幕の下に表示されます。書式設定オプション [については、「カードの書式設定](~/task-modules-and-cards/cards/cards-format.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-203">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="eebb0-204">images</span><span class="sxs-lookup"><span data-stu-id="eebb0-204">images</span></span> | <span data-ttu-id="eebb0-205">画像の配列</span><span class="sxs-lookup"><span data-stu-id="eebb0-205">Array of images</span></span> | <span data-ttu-id="eebb0-206">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="eebb0-206">Image displayed at top of card.</span></span> <span data-ttu-id="eebb0-207">縦横比 16:9。</span><span class="sxs-lookup"><span data-stu-id="eebb0-207">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="eebb0-208">buttons</span><span class="sxs-lookup"><span data-stu-id="eebb0-208">buttons</span></span> | <span data-ttu-id="eebb0-209">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="eebb0-209">Array of action objects</span></span> | <span data-ttu-id="eebb0-210">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="eebb0-210">Set of actions applicable to the current card.</span></span> <span data-ttu-id="eebb0-211">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-211">Maximum 6.</span></span> |
| <span data-ttu-id="eebb0-212">tap</span><span class="sxs-lookup"><span data-stu-id="eebb0-212">tap</span></span> | <span data-ttu-id="eebb0-213">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="eebb0-213">Action object</span></span> | <span data-ttu-id="eebb0-214">このアクションは、ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-214">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="eebb0-215">ヒーロー カードの例</span><span class="sxs-lookup"><span data-stu-id="eebb0-215">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="eebb0-217">ヒーロー カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="eebb0-217">Additional information on hero cards</span></span>

<span data-ttu-id="eebb0-218">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-218">Bot Framework reference:</span></span>

* [<span data-ttu-id="eebb0-219">ヒーロー カード ノード</span><span class="sxs-lookup"><span data-stu-id="eebb0-219">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="eebb0-220">ヒーロー カード C#</span><span class="sxs-lookup"><span data-stu-id="eebb0-220">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="eebb0-221">リスト カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-221">List card</span></span>

<span data-ttu-id="eebb0-222">リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-222">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="eebb0-223">リスト カードは、アイテムのスクロール リストを提供します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-223">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="eebb0-224">リスト カードのサポート</span><span class="sxs-lookup"><span data-stu-id="eebb0-224">Support for list cards</span></span>

| <span data-ttu-id="eebb0-225">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="eebb0-225">Bots in Teams</span></span> | <span data-ttu-id="eebb0-226">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eebb0-226">Messaging extensions</span></span>  | <span data-ttu-id="eebb0-227">コネクタ</span><span class="sxs-lookup"><span data-stu-id="eebb0-227">Connectors</span></span> | <span data-ttu-id="eebb0-228">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eebb0-228">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eebb0-229">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-229">✔</span></span> | <span data-ttu-id="eebb0-230">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-230">✖</span></span> | <span data-ttu-id="eebb0-231">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-231">✖</span></span> |<span data-ttu-id="eebb0-232">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-232">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="eebb0-233">リスト カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-233">Properties of a list card</span></span>

| <span data-ttu-id="eebb0-234">プロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-234">Property</span></span> | <span data-ttu-id="eebb0-235">種類</span><span class="sxs-lookup"><span data-stu-id="eebb0-235">Type</span></span>  | <span data-ttu-id="eebb0-236">説明</span><span class="sxs-lookup"><span data-stu-id="eebb0-236">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eebb0-237">title</span><span class="sxs-lookup"><span data-stu-id="eebb0-237">title</span></span> | <span data-ttu-id="eebb0-238">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-238">Rich text</span></span> | <span data-ttu-id="eebb0-239">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="eebb0-239">Title of the card.</span></span> <span data-ttu-id="eebb0-240">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="eebb0-240">Maximum 2 lines.</span></span>|
| <span data-ttu-id="eebb0-241">アイテム</span><span class="sxs-lookup"><span data-stu-id="eebb0-241">items</span></span> | <span data-ttu-id="eebb0-242">リスト アイテムの配列</span><span class="sxs-lookup"><span data-stu-id="eebb0-242">Array of list items</span></span>  ||
| <span data-ttu-id="eebb0-243">buttons</span><span class="sxs-lookup"><span data-stu-id="eebb0-243">buttons</span></span> | <span data-ttu-id="eebb0-244">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="eebb0-244">Array of action objects</span></span> | <span data-ttu-id="eebb0-245">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="eebb0-245">Set of actions applicable to the current card.</span></span> <span data-ttu-id="eebb0-246">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-246">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="eebb0-247">リスト カードの例</span><span class="sxs-lookup"><span data-stu-id="eebb0-247">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="eebb0-248">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-248">Office 365 connector card</span></span>

<span data-ttu-id="eebb0-249">Office 365 コネクタ カードは、Bot Framework ではなく Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-249">The Office 365 Connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="eebb0-250">このカードは、複数のセクション、フィールド、画像、アクションを含む柔軟なレイアウトを提供します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-250">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="eebb0-251">Bot が使用できるように、このカードがコネクタ カードをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="eebb0-252">コネクタ カードと O365 カードの違いについては、「注意事項」の欄を参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="eebb0-253">Office 365 コネクタ カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="eebb0-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="eebb0-254">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="eebb0-254">Bots in Teams</span></span> | <span data-ttu-id="eebb0-255">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eebb0-255">Messaging extensions</span></span>  | <span data-ttu-id="eebb0-256">コネクタ</span><span class="sxs-lookup"><span data-stu-id="eebb0-256">Connectors</span></span> | <span data-ttu-id="eebb0-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eebb0-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eebb0-258">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-258">✔</span></span> | <span data-ttu-id="eebb0-259">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-259">✔</span></span> | <span data-ttu-id="eebb0-260">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-260">✔</span></span> | <span data-ttu-id="eebb0-261">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-261">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="eebb0-262">Office 365 コネクタ カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="eebb0-263">プロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-263">Property</span></span> | <span data-ttu-id="eebb0-264">種類</span><span class="sxs-lookup"><span data-stu-id="eebb0-264">Type</span></span>  | <span data-ttu-id="eebb0-265">説明</span><span class="sxs-lookup"><span data-stu-id="eebb0-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eebb0-266">title</span><span class="sxs-lookup"><span data-stu-id="eebb0-266">title</span></span> | <span data-ttu-id="eebb0-267">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-267">Rich text</span></span> | <span data-ttu-id="eebb0-268">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="eebb0-268">Title of the card.</span></span> <span data-ttu-id="eebb0-269">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="eebb0-269">Maximum 2 lines.</span></span> |
| <span data-ttu-id="eebb0-270">概要</span><span class="sxs-lookup"><span data-stu-id="eebb0-270">summary</span></span> | <span data-ttu-id="eebb0-271">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-271">Rich text</span></span> | <span data-ttu-id="eebb0-272">カードの概要。</span><span class="sxs-lookup"><span data-stu-id="eebb0-272">Summary of the card.</span></span> <span data-ttu-id="eebb0-273">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="eebb0-273">Maximum 2 lines.</span></span> |
| <span data-ttu-id="eebb0-274">テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-274">text</span></span> | <span data-ttu-id="eebb0-275">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-275">Rich text</span></span> | <span data-ttu-id="eebb0-276">テキストは字幕の下に表示されます。書式設定オプション [については、「カードの書式設定](~/task-modules-and-cards/cards/cards-format.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="eebb0-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="eebb0-277">themeColor</span></span> | <span data-ttu-id="eebb0-278">16 進数文字列</span><span class="sxs-lookup"><span data-stu-id="eebb0-278">HEX string</span></span> | <span data-ttu-id="eebb0-279">アプリケーション マニフェストから提供される accentColor を上書きする色。</span><span class="sxs-lookup"><span data-stu-id="eebb0-279">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="eebb0-280">Office 365 コネクタ カードに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="eebb0-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="eebb0-281">Office 365 コネクタ カードは、ActionCard アクションなど、Microsoft Teams [で適切に機能します](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="eebb0-281">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="eebb0-282">コネクタからコネクタ カードを使用する場合とボットでコネクタ カードを使用する場合の重要な違いの 1 つは、カードアクションの処理です。</span><span class="sxs-lookup"><span data-stu-id="eebb0-282">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="eebb0-283">コネクタの場合、エンドポイントは HTTP POST 経由でカードペイロードを受信します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-283">For a connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="eebb0-284">Bot の場合、`HttpPOST` アクションが、アクション ID と本文のみを Bot に送信する `invoke` アクティビティをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="eebb0-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="eebb0-285">各コネクタ カードには最大 10 のセクションを表示できます。各セクションには最大 5 つの画像と 5 つのアクションを含めできます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-285">Each connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="eebb0-286">メッセージ内の他のセクション、画像、アクションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="eebb0-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="eebb0-287">すべてのテキスト フィールドは Markdown と HTML をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="eebb0-288">メッセージの `markdown` プロパティを設定して、Markdown または HTML を使用するセクションを制御することができます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="eebb0-289">既定では、`markdown` は `true` に設定されています。代わりに HTML を使用する場合は、`markdown` を `false` に設定します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="eebb0-290">`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="eebb0-291">レンダリング スタイルを指定するには `activityImage` 、次のように `activityImageType` 設定します。</span><span class="sxs-lookup"><span data-stu-id="eebb0-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="eebb0-292">値</span><span class="sxs-lookup"><span data-stu-id="eebb0-292">Value</span></span> | <span data-ttu-id="eebb0-293">説明</span><span class="sxs-lookup"><span data-stu-id="eebb0-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="eebb0-294">既定値です。 `activityImage` は、円としてトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-294">Default; `activityImage` will be cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="eebb0-295">`activityImage` が四角形として表示され、縦横比が維持されます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio.</span></span> |

<span data-ttu-id="eebb0-296">コネクタ カードのプロパティに関するその他の詳細については、操作可能なメッセージ カード [のリファレンスを参照してください](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="eebb0-296">For all other details about connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="eebb0-297">Microsoft Teams が現在サポートしていないコネクタ カードのプロパティは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="eebb0-297">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="eebb0-298">`startGroup` (Teams では常に `true` として扱われます)</span><span class="sxs-lookup"><span data-stu-id="eebb0-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="eebb0-299">Office 365 コネクタ カードの例</span><span class="sxs-lookup"><span data-stu-id="eebb0-299">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="eebb0-300">レシート カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-300">Receipt card</span></span>

<span data-ttu-id="eebb0-301">Teams はレシート カードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-301">Teams supports receipt card.</span></span> <span data-ttu-id="eebb0-302">ボットがユーザーに受領通知を提供できるカードです。</span><span class="sxs-lookup"><span data-stu-id="eebb0-302">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="eebb0-303">通常は、税金や合計情報など、受領通知に含めるアイテムのリストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-303">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="eebb0-304">受領通知カードのサポート</span><span class="sxs-lookup"><span data-stu-id="eebb0-304">Support for receipt cards</span></span>

| <span data-ttu-id="eebb0-305">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="eebb0-305">Bots in Teams</span></span> | <span data-ttu-id="eebb0-306">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eebb0-306">Messaging extensions</span></span>  | <span data-ttu-id="eebb0-307">コネクタ</span><span class="sxs-lookup"><span data-stu-id="eebb0-307">Connectors</span></span> | <span data-ttu-id="eebb0-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eebb0-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eebb0-309">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-309">✔</span></span> | <span data-ttu-id="eebb0-310">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-310">✔</span></span> | <span data-ttu-id="eebb0-311">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-311">✖</span></span> | <span data-ttu-id="eebb0-312">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-312">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="eebb0-313">受領通知カードの例</span><span class="sxs-lookup"><span data-stu-id="eebb0-313">Example of a receipt card</span></span>

![受領通知カードの例](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="eebb0-315">受領通知カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="eebb0-315">Additional information on receipt cards</span></span>

<span data-ttu-id="eebb0-316">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-316">Bot Framework reference:</span></span>

* [<span data-ttu-id="eebb0-317">レシート カード ノード</span><span class="sxs-lookup"><span data-stu-id="eebb0-317">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="eebb0-318">レシート カード C#</span><span class="sxs-lookup"><span data-stu-id="eebb0-318">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="eebb0-319">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-319">Signin card</span></span>

<span data-ttu-id="eebb0-320">サインイン カードを使用すると、ボットはユーザーにサインインを要求できます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-320">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="eebb0-321">Bot Framework とは若干異なる形式で Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-321">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="eebb0-322">Teams のサインイン カードは Bot Framework のサインイン カードに似ていますが、Teams のサインイン カードは次の 2 つのアクションのみをサポートします `signin` `openUrl` 。</span><span class="sxs-lookup"><span data-stu-id="eebb0-322">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="eebb0-323">*サインイン アクション* は、サインイン カードだけでなく、Teams のすべてのカードで使用できます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-323">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="eebb0-324">認証の詳細については、「ボットの [Microsoft Teams 認証フロー」を参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="eebb0-324">For more details on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="eebb0-325">サインイン カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="eebb0-325">Support for Signin cards</span></span>

| <span data-ttu-id="eebb0-326">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="eebb0-326">Bots in Teams</span></span> | <span data-ttu-id="eebb0-327">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eebb0-327">Messaging extensions</span></span>  | <span data-ttu-id="eebb0-328">コネクタ</span><span class="sxs-lookup"><span data-stu-id="eebb0-328">Connectors</span></span> | <span data-ttu-id="eebb0-329">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eebb0-329">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eebb0-330">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-330">✔</span></span> | <span data-ttu-id="eebb0-331">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-331">✖</span></span> | <span data-ttu-id="eebb0-332">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-332">✖</span></span> | <span data-ttu-id="eebb0-333">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-333">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="eebb0-334">サインイン カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="eebb0-334">Additional information on signin cards</span></span>

<span data-ttu-id="eebb0-335">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-335">Bot Framework reference:</span></span>

* [<span data-ttu-id="eebb0-336">サインイン カード ノード</span><span class="sxs-lookup"><span data-stu-id="eebb0-336">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="eebb0-337">サインイン カード C#</span><span class="sxs-lookup"><span data-stu-id="eebb0-337">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="eebb0-338">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-338">Thumbnail card</span></span>

<span data-ttu-id="eebb0-339">通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="eebb0-339">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="eebb0-340">サムネイル カードのサポート</span><span class="sxs-lookup"><span data-stu-id="eebb0-340">Support for thumbnail cards</span></span>

| <span data-ttu-id="eebb0-341">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="eebb0-341">Bots in Teams</span></span> | <span data-ttu-id="eebb0-342">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eebb0-342">Messaging extensions</span></span>  | <span data-ttu-id="eebb0-343">コネクタ</span><span class="sxs-lookup"><span data-stu-id="eebb0-343">Connectors</span></span> | <span data-ttu-id="eebb0-344">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eebb0-344">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eebb0-345">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-345">✔</span></span> | <span data-ttu-id="eebb0-346">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-346">✔</span></span> | <span data-ttu-id="eebb0-347">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-347">✖</span></span> | <span data-ttu-id="eebb0-348">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-348">✔</span></span> |

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="eebb0-350">サムネイル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-350">Properties of a thumbnail card</span></span>

| <span data-ttu-id="eebb0-351">プロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-351">Property</span></span> | <span data-ttu-id="eebb0-352">種類</span><span class="sxs-lookup"><span data-stu-id="eebb0-352">Type</span></span>  | <span data-ttu-id="eebb0-353">説明</span><span class="sxs-lookup"><span data-stu-id="eebb0-353">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eebb0-354">title</span><span class="sxs-lookup"><span data-stu-id="eebb0-354">title</span></span> | <span data-ttu-id="eebb0-355">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-355">Rich text</span></span> | <span data-ttu-id="eebb0-356">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="eebb0-356">Title of the card.</span></span> <span data-ttu-id="eebb0-357">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="eebb0-357">Maximum 2 lines.</span></span>|
| <span data-ttu-id="eebb0-358">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="eebb0-358">subtitle</span></span> | <span data-ttu-id="eebb0-359">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-359">Rich text</span></span> | <span data-ttu-id="eebb0-360">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="eebb0-360">Subtitle of the card.</span></span> <span data-ttu-id="eebb0-361">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="eebb0-361">Maximum 2 lines.</span></span>|
| <span data-ttu-id="eebb0-362">テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-362">text</span></span> | <span data-ttu-id="eebb0-363">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="eebb0-363">Rich text</span></span> | <span data-ttu-id="eebb0-364">テキストは字幕の下に表示されます。書式設定オプション [については、「カードの書式設定](~/task-modules-and-cards/cards/cards-format.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-364">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="eebb0-365">images</span><span class="sxs-lookup"><span data-stu-id="eebb0-365">images</span></span> | <span data-ttu-id="eebb0-366">画像の配列</span><span class="sxs-lookup"><span data-stu-id="eebb0-366">Array of images</span></span> | <span data-ttu-id="eebb0-367">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="eebb0-367">Image displayed at top of card.</span></span> <span data-ttu-id="eebb0-368">縦横比 1:1 (正方形)。</span><span class="sxs-lookup"><span data-stu-id="eebb0-368">Aspect ratio 1:1 (square).</span></span> |
| <span data-ttu-id="eebb0-369">buttons</span><span class="sxs-lookup"><span data-stu-id="eebb0-369">buttons</span></span> | <span data-ttu-id="eebb0-370">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="eebb0-370">Array of action objects</span></span> | <span data-ttu-id="eebb0-371">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="eebb0-371">Set of actions applicable to the current card.</span></span> <span data-ttu-id="eebb0-372">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="eebb0-372">Maximum 6.</span></span> |
| <span data-ttu-id="eebb0-373">tap</span><span class="sxs-lookup"><span data-stu-id="eebb0-373">tap</span></span> | <span data-ttu-id="eebb0-374">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="eebb0-374">Action object</span></span> | <span data-ttu-id="eebb0-375">このアクションは、ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-375">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="eebb0-376">サムネイル カードの例</span><span class="sxs-lookup"><span data-stu-id="eebb0-376">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="eebb0-377">追加情報</span><span class="sxs-lookup"><span data-stu-id="eebb0-377">Additional information</span></span>

<span data-ttu-id="eebb0-378">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="eebb0-378">Bot Framework reference:</span></span>

* [<span data-ttu-id="eebb0-379">サムネイル カード ノード</span><span class="sxs-lookup"><span data-stu-id="eebb0-379">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="eebb0-380">サムネイル カード C#</span><span class="sxs-lookup"><span data-stu-id="eebb0-380">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="eebb0-381">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="eebb0-381">Card collections</span></span>

<span data-ttu-id="eebb0-382">Teams はカード コレクションをサポートします。</span><span class="sxs-lookup"><span data-stu-id="eebb0-382">Teams supports Card collections.</span></span>

<span data-ttu-id="eebb0-383">カード コレクション: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="eebb0-383">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="eebb0-384">これらのコレクションには、アダプティブ カード、ヒーロー カード、またはサムネイル カードが含まれている。</span><span class="sxs-lookup"><span data-stu-id="eebb0-384">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="eebb0-385">カルーセル コレクション</span><span class="sxs-lookup"><span data-stu-id="eebb0-385">Carousel collection</span></span>

<span data-ttu-id="eebb0-386">[カルーセルのレイアウト](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-386">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="eebb0-387">カルーセル コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="eebb0-387">Support for carousel collections</span></span>

| <span data-ttu-id="eebb0-388">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="eebb0-388">Bots in Teams</span></span> | <span data-ttu-id="eebb0-389">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eebb0-389">Messaging extensions</span></span>  | <span data-ttu-id="eebb0-390">コネクタ</span><span class="sxs-lookup"><span data-stu-id="eebb0-390">Connectors</span></span> | <span data-ttu-id="eebb0-391">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eebb0-391">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eebb0-392">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-392">✔</span></span> | <span data-ttu-id="eebb0-393">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-393">✖</span></span> | <span data-ttu-id="eebb0-394">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-394">✖</span></span> | <span data-ttu-id="eebb0-395">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-395">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="eebb0-396">カルーセルでは、メッセージごとに最大 10 枚のカードを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-396">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="eebb0-397">カルーセル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="eebb0-397">Properties of a carousel card</span></span>

<span data-ttu-id="eebb0-398">カルーセル カードのプロパティは、ヒーロー カードとサムネイル カードのプロパティと同じです。</span><span class="sxs-lookup"><span data-stu-id="eebb0-398">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="eebb0-399">カルーセル コレクションの例</span><span class="sxs-lookup"><span data-stu-id="eebb0-399">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="eebb0-401">カルーセル コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="eebb0-401">Syntax for carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="eebb0-402">リスト コレクション</span><span class="sxs-lookup"><span data-stu-id="eebb0-402">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="eebb0-403">リスト コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="eebb0-403">Support for list collections</span></span>

<span data-ttu-id="eebb0-404">リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-404">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="eebb0-405">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="eebb0-405">Bots in Teams</span></span> | <span data-ttu-id="eebb0-406">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eebb0-406">Messaging extensions</span></span>  | <span data-ttu-id="eebb0-407">コネクタ</span><span class="sxs-lookup"><span data-stu-id="eebb0-407">Connectors</span></span> | <span data-ttu-id="eebb0-408">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="eebb0-408">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eebb0-409">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-409">✔</span></span> | <span data-ttu-id="eebb0-410">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-410">✔</span></span> | <span data-ttu-id="eebb0-411">✖</span><span class="sxs-lookup"><span data-stu-id="eebb0-411">✖</span></span> | <span data-ttu-id="eebb0-412">✔</span><span class="sxs-lookup"><span data-stu-id="eebb0-412">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="eebb0-413">リスト コレクションの例</span><span class="sxs-lookup"><span data-stu-id="eebb0-413">Example of a list collection</span></span>

![カードのリストの例](~/assets/images/cards/list.png)

<span data-ttu-id="eebb0-415">プロパティは、ヒーローやサムネイル カードの場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="eebb0-415">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="eebb0-416">リストでは、メッセージごとに最大 10 枚のカードを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="eebb0-416">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="eebb0-417">iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="eebb0-417">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="eebb0-418">リスト コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="eebb0-418">Syntax for list collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="eebb0-419">Teams でサポートされていないカード</span><span class="sxs-lookup"><span data-stu-id="eebb0-419">Cards not supported in Teams</span></span>

<span data-ttu-id="eebb0-420">次のカードは Bot Framework によって実装されていますが、Teams ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="eebb0-420">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="eebb0-421">アニメーション カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-421">Animation cards</span></span>
* <span data-ttu-id="eebb0-422">オーディオ カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-422">Audio cards</span></span>
* <span data-ttu-id="eebb0-423">ビデオ カード</span><span class="sxs-lookup"><span data-stu-id="eebb0-423">Video cards</span></span>
