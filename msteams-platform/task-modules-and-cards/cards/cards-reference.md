---
title: カード リファレンス
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
localization_priority: Normal
keywords: Bot のカード リファレンス
ms.topic: reference
ms.openlocfilehash: 741980ea79dd23659dd2b8a240d767b8292ca251
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994386"
---
# <a name="cards-reference"></a><span data-ttu-id="1bf3c-104">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="1bf3c-104">Cards reference</span></span>

<span data-ttu-id="1bf3c-105">このドキュメントに記載されているカードは、ボットでサポートされているMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="1bf3c-106">これらは Bot Framework (BF) で定義されたカードに基づいておりますが、Teams ではすべてのボット フレームワーク カードがサポートされるのではなく、一部の Teams カードが追加されています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-106">They are based on cards defined by the Bot Framework (BF), but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="1bf3c-107">相違点は、このドキュメントの参照で呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="1bf3c-108">カードの例</span><span class="sxs-lookup"><span data-stu-id="1bf3c-108">Card examples</span></span>

<span data-ttu-id="1bf3c-109">カードの使用方法に関する追加情報については、Bot Builder SDK v3 のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="1bf3c-110">コード サンプルは、Microsoft/BotBuilder-Samples リポジトリ (microsoft/BotBuilder-Samples リポジトリ) GitHub。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="1bf3c-111">.NET</span><span class="sxs-lookup"><span data-stu-id="1bf3c-111">.NET</span></span>
  * <span data-ttu-id="1bf3c-112">[メッセージに添付ファイルとしてカードを追加します](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="1bf3c-113">[カードのサンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="1bf3c-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="1bf3c-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="1bf3c-114">Node.js</span></span>
  * <span data-ttu-id="1bf3c-115">[メッセージに添付ファイルとしてカードを追加します](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="1bf3c-116">[カードのサンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span><span class="sxs-lookup"><span data-stu-id="1bf3c-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="1bf3c-117">カードの種類</span><span class="sxs-lookup"><span data-stu-id="1bf3c-117">Types of cards</span></span>

<span data-ttu-id="1bf3c-118">次の表に、使用可能なカードの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="1bf3c-119">カードの種類</span><span class="sxs-lookup"><span data-stu-id="1bf3c-119">Card type</span></span> | <span data-ttu-id="1bf3c-120">説明</span><span class="sxs-lookup"><span data-stu-id="1bf3c-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="1bf3c-121">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="1bf3c-122">このカードは、テキスト、音声、画像、ボタン、および入力フィールドの任意の組み合わせを含む高度にカスタマイズ可能なカードです。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="1bf3c-123">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="1bf3c-124">このカードには、通常、1 つの大きな画像、1 つ以上のボタン、および少量のテキストが含まれる。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="1bf3c-125">リスト カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-125">List card</span></span>](#list-card) | <span data-ttu-id="1bf3c-126">このカードはアイテムのスクロール リストです。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="1bf3c-127">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="1bf3c-128">このカードには、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトがあります。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="1bf3c-129">レシート カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="1bf3c-130">このカードは、ユーザーにレシートを提供します。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="1bf3c-131">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="1bf3c-132">このカードを使用すると、ボットはユーザーのサインインを要求できます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="1bf3c-133">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="1bf3c-134">このカードには、通常、1 つのサムネイル 画像、短いテキスト、および 1 つ以上のボタンが含まれる。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="1bf3c-135">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="1bf3c-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="1bf3c-136">このカードは、1 つの応答で複数のアイテムを返す場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="1bf3c-137">すべてのカードの共通プロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="1bf3c-138">インライン カードの画像</span><span class="sxs-lookup"><span data-stu-id="1bf3c-138">Inline card images</span></span>

<span data-ttu-id="1bf3c-139">カードには、公開されている画像へのリンクを含め、インライン イメージを含めできます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="1bf3c-140">パフォーマンス上の目的で、パブリック コンテンツ配信ネットワーク (CDN) でイメージをホストすることを強くお勧CDN。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="1bf3c-141">画像のサイズは拡大または縮小され、縦横比を維持して画像領域をカバーします。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="1bf3c-142">次に、カードの適切な縦横比を実現するために、中央から画像がトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="1bf3c-143">画像は、PNG、JPEG、または GIF 形式×最大 1024、×1024 である必要があります。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="1bf3c-144">プロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-144">Property</span></span> | <span data-ttu-id="1bf3c-145">型</span><span class="sxs-lookup"><span data-stu-id="1bf3c-145">Type</span></span>  | <span data-ttu-id="1bf3c-146">説明</span><span class="sxs-lookup"><span data-stu-id="1bf3c-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bf3c-147">url</span><span class="sxs-lookup"><span data-stu-id="1bf3c-147">url</span></span> | <span data-ttu-id="1bf3c-148">URL</span><span class="sxs-lookup"><span data-stu-id="1bf3c-148">URL</span></span> | <span data-ttu-id="1bf3c-149">イメージの HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="1bf3c-150">alt</span><span class="sxs-lookup"><span data-stu-id="1bf3c-150">alt</span></span> | <span data-ttu-id="1bf3c-151">文字列</span><span class="sxs-lookup"><span data-stu-id="1bf3c-151">String</span></span> | <span data-ttu-id="1bf3c-152">画像のアクセス可能な説明。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="1bf3c-153">最終的なイメージの前にリダイレクトを行うイメージ URL がカードに含まれる場合、イメージ URL のリダイレクトはサポートされません。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="1bf3c-154">これは、パブリック クラウド上で共有されるイメージに対して発生します。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="1bf3c-155">ボタン</span><span class="sxs-lookup"><span data-stu-id="1bf3c-155">Buttons</span></span>

<span data-ttu-id="1bf3c-156">ボタンはカードの下部に上下に並んで表示されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="1bf3c-157">ボタンのテキストは常に 1 行に表示され、テキストがボタンの幅を超えると切り捨てされます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="1bf3c-158">カードでサポートされている最大数を超える追加のボタンは表示されません。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="1bf3c-159">詳細については、「カードアクション [」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="1bf3c-160">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="1bf3c-160">Card formatting</span></span>

<span data-ttu-id="1bf3c-161">カードのテキスト書式の詳細については、「カードの書式設定」 [を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="1bf3c-162">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-162">Adaptive card</span></span>

<span data-ttu-id="1bf3c-163">アダプティブ カードは、テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含むカスタマイズ可能なカードです。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="1bf3c-164">詳細については、「アダプティブ カード [v1.2.0」を参照してください](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="1bf3c-165">アダプティブ カードのサポート</span><span class="sxs-lookup"><span data-stu-id="1bf3c-165">Support for adaptive cards</span></span>

| <span data-ttu-id="1bf3c-166">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="1bf3c-166">Bots in Teams</span></span> | <span data-ttu-id="1bf3c-167">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1bf3c-167">Messaging extensions</span></span>  | <span data-ttu-id="1bf3c-168">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-168">Connectors</span></span> | <span data-ttu-id="1bf3c-169">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf3c-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bf3c-170">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-170">✔</span></span> | <span data-ttu-id="1bf3c-171">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-171">✔</span></span> | <span data-ttu-id="1bf3c-172">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-172">✖</span></span> | <span data-ttu-id="1bf3c-173">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="1bf3c-174">Teamsプラットフォームは、v1.2 以前のアダプティブ カード機能をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="1bf3c-175">正または破壊的なアクションのスタイル設定は、プラットフォーム上のアダプティブ カードではTeamsされません。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-175">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="1bf3c-176">メディア要素は、現在、プラットフォーム上のアダプティブ カードTeamsされていません。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-176">Media elements are currently not supported in Adaptive Cards on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="1bf3c-177">アダプティブ カードの例</span><span class="sxs-lookup"><span data-stu-id="1bf3c-177">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="1bf3c-179">アダプティブ カードの追加情報</span><span class="sxs-lookup"><span data-stu-id="1bf3c-179">Additional information on adaptive cards</span></span>

<span data-ttu-id="1bf3c-180">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-180">Bot Framework reference:</span></span>

* [<span data-ttu-id="1bf3c-181">アダプティブ カードNode.js</span><span class="sxs-lookup"><span data-stu-id="1bf3c-181">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="1bf3c-182">アダプティブ カード C#</span><span class="sxs-lookup"><span data-stu-id="1bf3c-182">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="1bf3c-183">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-183">Hero card</span></span>

<span data-ttu-id="1bf3c-184">通常、1 つの大きな画像、1 つ以上のボタン、およびテキストを含むカード。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-184">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="1bf3c-185">ヒーロー カードのサポート</span><span class="sxs-lookup"><span data-stu-id="1bf3c-185">Support for hero cards</span></span>

| <span data-ttu-id="1bf3c-186">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="1bf3c-186">Bots in Teams</span></span> | <span data-ttu-id="1bf3c-187">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1bf3c-187">Messaging extensions</span></span>  | <span data-ttu-id="1bf3c-188">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-188">Connectors</span></span> | <span data-ttu-id="1bf3c-189">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf3c-189">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bf3c-190">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-190">✔</span></span> | <span data-ttu-id="1bf3c-191">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-191">✔</span></span> | <span data-ttu-id="1bf3c-192">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-192">✖</span></span> | <span data-ttu-id="1bf3c-193">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-193">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="1bf3c-194">ヒーロー カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-194">Properties of a hero card</span></span>

| <span data-ttu-id="1bf3c-195">プロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-195">Property</span></span> | <span data-ttu-id="1bf3c-196">型</span><span class="sxs-lookup"><span data-stu-id="1bf3c-196">Type</span></span>  | <span data-ttu-id="1bf3c-197">説明</span><span class="sxs-lookup"><span data-stu-id="1bf3c-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bf3c-198">title</span><span class="sxs-lookup"><span data-stu-id="1bf3c-198">title</span></span> | <span data-ttu-id="1bf3c-199">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-199">Rich text</span></span> | <span data-ttu-id="1bf3c-200">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-200">Title of the card.</span></span> <span data-ttu-id="1bf3c-201">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-201">Maximum 2 lines.</span></span> |
| <span data-ttu-id="1bf3c-202">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="1bf3c-202">subtitle</span></span> | <span data-ttu-id="1bf3c-203">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-203">Rich text</span></span> | <span data-ttu-id="1bf3c-204">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-204">Subtitle of the card.</span></span> <span data-ttu-id="1bf3c-205">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-205">Maximum 2 lines.</span></span>|
| <span data-ttu-id="1bf3c-206">テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-206">text</span></span> | <span data-ttu-id="1bf3c-207">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-207">Rich text</span></span> | <span data-ttu-id="1bf3c-208">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-208">Text appears under the subtitle.</span></span> <span data-ttu-id="1bf3c-209">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-209">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="1bf3c-210">images</span><span class="sxs-lookup"><span data-stu-id="1bf3c-210">images</span></span> | <span data-ttu-id="1bf3c-211">画像の配列</span><span class="sxs-lookup"><span data-stu-id="1bf3c-211">Array of images</span></span> | <span data-ttu-id="1bf3c-212">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-212">Image displayed at the top of the card.</span></span> <span data-ttu-id="1bf3c-213">縦横比 16:9。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-213">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="1bf3c-214">buttons</span><span class="sxs-lookup"><span data-stu-id="1bf3c-214">buttons</span></span> | <span data-ttu-id="1bf3c-215">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="1bf3c-215">Array of action objects</span></span> | <span data-ttu-id="1bf3c-216">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-216">Set of actions applicable to the current card.</span></span> <span data-ttu-id="1bf3c-217">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-217">Maximum 6.</span></span> |
| <span data-ttu-id="1bf3c-218">tap</span><span class="sxs-lookup"><span data-stu-id="1bf3c-218">tap</span></span> | <span data-ttu-id="1bf3c-219">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-219">Action object</span></span> | <span data-ttu-id="1bf3c-220">ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-220">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="1bf3c-221">ヒーロー カードの例</span><span class="sxs-lookup"><span data-stu-id="1bf3c-221">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="1bf3c-223">ヒーロー カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="1bf3c-223">Additional information on hero cards</span></span>

<span data-ttu-id="1bf3c-224">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-224">Bot Framework reference:</span></span>

* [<span data-ttu-id="1bf3c-225">ヒーロー カード Node.js</span><span class="sxs-lookup"><span data-stu-id="1bf3c-225">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="1bf3c-226">ヒーロー カード C#</span><span class="sxs-lookup"><span data-stu-id="1bf3c-226">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="1bf3c-227">リスト カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-227">List card</span></span>

<span data-ttu-id="1bf3c-228">リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-228">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="1bf3c-229">リスト カードは、アイテムのスクロール リストを提供します。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-229">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="1bf3c-230">リスト カードのサポート</span><span class="sxs-lookup"><span data-stu-id="1bf3c-230">Support for list cards</span></span>

| <span data-ttu-id="1bf3c-231">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="1bf3c-231">Bots in Teams</span></span> | <span data-ttu-id="1bf3c-232">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1bf3c-232">Messaging extensions</span></span>  | <span data-ttu-id="1bf3c-233">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-233">Connectors</span></span> | <span data-ttu-id="1bf3c-234">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf3c-234">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bf3c-235">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-235">✔</span></span> | <span data-ttu-id="1bf3c-236">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-236">✖</span></span> | <span data-ttu-id="1bf3c-237">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-237">✖</span></span> |<span data-ttu-id="1bf3c-238">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-238">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="1bf3c-239">リスト カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-239">Properties of a list card</span></span>

| <span data-ttu-id="1bf3c-240">プロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-240">Property</span></span> | <span data-ttu-id="1bf3c-241">型</span><span class="sxs-lookup"><span data-stu-id="1bf3c-241">Type</span></span>  | <span data-ttu-id="1bf3c-242">説明</span><span class="sxs-lookup"><span data-stu-id="1bf3c-242">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bf3c-243">title</span><span class="sxs-lookup"><span data-stu-id="1bf3c-243">title</span></span> | <span data-ttu-id="1bf3c-244">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-244">Rich text</span></span> | <span data-ttu-id="1bf3c-245">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-245">Title of the card.</span></span> <span data-ttu-id="1bf3c-246">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-246">Maximum 2 lines.</span></span>|
| <span data-ttu-id="1bf3c-247">アイテム</span><span class="sxs-lookup"><span data-stu-id="1bf3c-247">items</span></span> | <span data-ttu-id="1bf3c-248">リスト アイテムの配列</span><span class="sxs-lookup"><span data-stu-id="1bf3c-248">Array of list items</span></span> ||
| <span data-ttu-id="1bf3c-249">buttons</span><span class="sxs-lookup"><span data-stu-id="1bf3c-249">buttons</span></span> | <span data-ttu-id="1bf3c-250">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="1bf3c-250">Array of action objects</span></span> | <span data-ttu-id="1bf3c-251">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-251">Set of actions applicable to the current card.</span></span> <span data-ttu-id="1bf3c-252">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-252">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="1bf3c-253">リスト カードの例</span><span class="sxs-lookup"><span data-stu-id="1bf3c-253">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="1bf3c-254">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-254">Office 365 connector card</span></span>

<span data-ttu-id="1bf3c-255">コネクタ Office 365はボット フレームワークではなく、Teamsでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-255">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="1bf3c-256">このカードは、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトを提供します。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-256">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="1bf3c-257">Bot が使用できるように、このカードがコネクタ カードをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-257">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="1bf3c-258">コネクタ カードと O365 カードの違いについては、「コネクタ カードに関するOffice 365[を参照してください](#notes-on-the-office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-258">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="1bf3c-259">Office 365 コネクタ カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="1bf3c-259">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="1bf3c-260">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="1bf3c-260">Bots in Teams</span></span> | <span data-ttu-id="1bf3c-261">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1bf3c-261">Messaging extensions</span></span>  | <span data-ttu-id="1bf3c-262">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-262">Connectors</span></span> | <span data-ttu-id="1bf3c-263">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf3c-263">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bf3c-264">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-264">✔</span></span> | <span data-ttu-id="1bf3c-265">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-265">✔</span></span> | <span data-ttu-id="1bf3c-266">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-266">✔</span></span> | <span data-ttu-id="1bf3c-267">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-267">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="1bf3c-268">Office 365 コネクタ カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-268">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="1bf3c-269">プロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-269">Property</span></span> | <span data-ttu-id="1bf3c-270">型</span><span class="sxs-lookup"><span data-stu-id="1bf3c-270">Type</span></span>  | <span data-ttu-id="1bf3c-271">説明</span><span class="sxs-lookup"><span data-stu-id="1bf3c-271">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bf3c-272">title</span><span class="sxs-lookup"><span data-stu-id="1bf3c-272">title</span></span> | <span data-ttu-id="1bf3c-273">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-273">Rich text</span></span> | <span data-ttu-id="1bf3c-274">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-274">Title of the card.</span></span> <span data-ttu-id="1bf3c-275">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-275">Maximum 2 lines.</span></span> |
| <span data-ttu-id="1bf3c-276">概要</span><span class="sxs-lookup"><span data-stu-id="1bf3c-276">summary</span></span> | <span data-ttu-id="1bf3c-277">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-277">Rich text</span></span> | <span data-ttu-id="1bf3c-278">カードの概要。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-278">Summary of the card.</span></span> <span data-ttu-id="1bf3c-279">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-279">Maximum 2 lines.</span></span> |
| <span data-ttu-id="1bf3c-280">テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-280">text</span></span> | <span data-ttu-id="1bf3c-281">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-281">Rich text</span></span> | <span data-ttu-id="1bf3c-282">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-282">Text appears under the subtitle.</span></span> <span data-ttu-id="1bf3c-283">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-283">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="1bf3c-284">themeColor</span><span class="sxs-lookup"><span data-stu-id="1bf3c-284">themeColor</span></span> | <span data-ttu-id="1bf3c-285">16 進数文字列</span><span class="sxs-lookup"><span data-stu-id="1bf3c-285">HEX string</span></span> | <span data-ttu-id="1bf3c-286">アプリケーション マニフェストから提供される accentColor を上書きする色。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-286">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="1bf3c-287">Office 365 コネクタ カードに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="1bf3c-287">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="1bf3c-288">Office 365カードは、ActionCard アクションなど、Microsoft Teamsで[適切に機能します](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-288">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="1bf3c-289">コネクタからコネクタ カードを使用する場合とボットでコネクタ カードを使用する場合の重要な違いの 1 つは、カードアクションの処理です。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-289">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="1bf3c-290">コネクタの場合、エンドポイントは HTTP POST を介してカード ペイロードを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-290">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="1bf3c-291">Bot の場合、`HttpPOST` アクションが、アクション ID と本文のみを Bot に送信する `invoke` アクティビティをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-291">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="1bf3c-292">各コネクタ カードには最大 10 個のセクションを表示できます。各セクションには最大 5 つのイメージと 5 つのアクションを含めできます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-292">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf3c-293">メッセージ内の追加のセクション、イメージ、またはアクションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-293">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="1bf3c-294">すべてのテキスト フィールドは、マークダウンと HTML をサポートします。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-294">All text fields support markdown and HTML.</span></span> <span data-ttu-id="1bf3c-295">メッセージ内のプロパティを設定することで、マークダウンまたは HTML を使用 `markdown` するセクションを制御できます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-295">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="1bf3c-296">既定では `markdown` 、 に設定されています `true` 。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-296">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="1bf3c-297">HTML を代わりに使用する場合は、 に `markdown` 設定します `false` 。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-297">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="1bf3c-298">`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-298">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="1bf3c-299">レンダリング スタイルを指定するには `activityImage` 、次のように `activityImageType` 設定できます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-299">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="1bf3c-300">値</span><span class="sxs-lookup"><span data-stu-id="1bf3c-300">Value</span></span> | <span data-ttu-id="1bf3c-301">説明</span><span class="sxs-lookup"><span data-stu-id="1bf3c-301">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="1bf3c-302">既定値。 `activityImage` は、円としてトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-302">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="1bf3c-303">`activityImage` は四角形として表示され、縦横比が保持されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-303">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="1bf3c-304">コネクタ カードのプロパティに関するその他の詳細については、「アクション可能な [メッセージ カードリファレンス」を参照してください](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-304">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="1bf3c-305">現在サポートされていないコネクタ Microsoft Teamsのプロパティは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-305">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="1bf3c-306">`startGroup`常に、次のように `true` 処理Teams</span><span class="sxs-lookup"><span data-stu-id="1bf3c-306">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="1bf3c-307">コネクタ カードOffice 365例</span><span class="sxs-lookup"><span data-stu-id="1bf3c-307">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="1bf3c-308">レシート カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-308">Receipt card</span></span>

<span data-ttu-id="1bf3c-309">Teamsカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-309">Teams supports receipt card.</span></span> <span data-ttu-id="1bf3c-310">ボットがユーザーにレシートを提供できるカードです。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-310">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="1bf3c-311">通常、税金や合計情報など、領収書に含めるアイテムの一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-311">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="1bf3c-312">レシート カードのサポート</span><span class="sxs-lookup"><span data-stu-id="1bf3c-312">Support for receipt cards</span></span>

| <span data-ttu-id="1bf3c-313">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="1bf3c-313">Bots in Teams</span></span> | <span data-ttu-id="1bf3c-314">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1bf3c-314">Messaging extensions</span></span>  | <span data-ttu-id="1bf3c-315">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-315">Connectors</span></span> | <span data-ttu-id="1bf3c-316">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf3c-316">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bf3c-317">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-317">✔</span></span> | <span data-ttu-id="1bf3c-318">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-318">✔</span></span> | <span data-ttu-id="1bf3c-319">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-319">✖</span></span> | <span data-ttu-id="1bf3c-320">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-320">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="1bf3c-321">レシート カードの例</span><span class="sxs-lookup"><span data-stu-id="1bf3c-321">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="1bf3c-323">レシート カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="1bf3c-323">Additional information on receipt cards</span></span>

<span data-ttu-id="1bf3c-324">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-324">Bot Framework reference:</span></span>

* [<span data-ttu-id="1bf3c-325">レシート カードNode.js</span><span class="sxs-lookup"><span data-stu-id="1bf3c-325">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="1bf3c-326">レシート カード C#</span><span class="sxs-lookup"><span data-stu-id="1bf3c-326">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="1bf3c-327">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-327">Signin card</span></span>

<span data-ttu-id="1bf3c-328">Signin card を使用すると、ボットはユーザーにサインインを要求できます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-328">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="1bf3c-329">これは、ボット フレームワークTeams少し異なる形式でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-329">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="1bf3c-330">Teams のサインイン カードはボット フレームワークのサインイン カードに似ていますが、Teams のサインイン カードは 2 つのアクションのみをサポートしています。 `signin` `openUrl`</span><span class="sxs-lookup"><span data-stu-id="1bf3c-330">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="1bf3c-331">サインイン アクションは、サインイン カードだけでなく、Teams のすべてのカードで使用できます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-331">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="1bf3c-332">認証の詳細については、「ボットMicrosoft Teams[認証フロー」を参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-332">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="1bf3c-333">サインイン カードのサポート</span><span class="sxs-lookup"><span data-stu-id="1bf3c-333">Support for signin cards</span></span>

| <span data-ttu-id="1bf3c-334">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="1bf3c-334">Bots in Teams</span></span> | <span data-ttu-id="1bf3c-335">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1bf3c-335">Messaging extensions</span></span>  | <span data-ttu-id="1bf3c-336">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-336">Connectors</span></span> | <span data-ttu-id="1bf3c-337">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf3c-337">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bf3c-338">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-338">✔</span></span> | <span data-ttu-id="1bf3c-339">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-339">✖</span></span> | <span data-ttu-id="1bf3c-340">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-340">✖</span></span> | <span data-ttu-id="1bf3c-341">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-341">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="1bf3c-342">サインイン カードに関する追加情報</span><span class="sxs-lookup"><span data-stu-id="1bf3c-342">Additional information on signin cards</span></span>

<span data-ttu-id="1bf3c-343">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-343">Bot Framework reference:</span></span>

* [<span data-ttu-id="1bf3c-344">Signin カード Node.js</span><span class="sxs-lookup"><span data-stu-id="1bf3c-344">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="1bf3c-345">サインイン カード C#</span><span class="sxs-lookup"><span data-stu-id="1bf3c-345">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="1bf3c-346">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-346">Thumbnail card</span></span>

<span data-ttu-id="1bf3c-347">通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-347">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="1bf3c-348">サムネイル カードのサポート</span><span class="sxs-lookup"><span data-stu-id="1bf3c-348">Support for thumbnail cards</span></span>

| <span data-ttu-id="1bf3c-349">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="1bf3c-349">Bots in Teams</span></span> | <span data-ttu-id="1bf3c-350">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1bf3c-350">Messaging extensions</span></span>  | <span data-ttu-id="1bf3c-351">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-351">Connectors</span></span> | <span data-ttu-id="1bf3c-352">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf3c-352">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bf3c-353">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-353">✔</span></span> | <span data-ttu-id="1bf3c-354">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-354">✔</span></span> | <span data-ttu-id="1bf3c-355">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-355">✖</span></span> | <span data-ttu-id="1bf3c-356">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-356">✔</span></span> |

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="1bf3c-358">サムネイル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-358">Properties of a thumbnail card</span></span>

| <span data-ttu-id="1bf3c-359">プロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-359">Property</span></span> | <span data-ttu-id="1bf3c-360">型</span><span class="sxs-lookup"><span data-stu-id="1bf3c-360">Type</span></span>  | <span data-ttu-id="1bf3c-361">説明</span><span class="sxs-lookup"><span data-stu-id="1bf3c-361">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bf3c-362">title</span><span class="sxs-lookup"><span data-stu-id="1bf3c-362">title</span></span> | <span data-ttu-id="1bf3c-363">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-363">Rich text</span></span> | <span data-ttu-id="1bf3c-364">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-364">Title of the card.</span></span> <span data-ttu-id="1bf3c-365">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-365">Maximum 2 lines.</span></span>|
| <span data-ttu-id="1bf3c-366">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="1bf3c-366">subtitle</span></span> | <span data-ttu-id="1bf3c-367">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-367">Rich text</span></span> | <span data-ttu-id="1bf3c-368">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-368">Subtitle of the card.</span></span> <span data-ttu-id="1bf3c-369">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-369">Maximum 2 lines.</span></span>|
| <span data-ttu-id="1bf3c-370">テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-370">text</span></span> | <span data-ttu-id="1bf3c-371">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-371">Rich text</span></span> | <span data-ttu-id="1bf3c-372">字幕の下にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-372">Text appears under the subtitle.</span></span> <span data-ttu-id="1bf3c-373">書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-373">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="1bf3c-374">images</span><span class="sxs-lookup"><span data-stu-id="1bf3c-374">images</span></span> | <span data-ttu-id="1bf3c-375">画像の配列</span><span class="sxs-lookup"><span data-stu-id="1bf3c-375">Array of images</span></span> | <span data-ttu-id="1bf3c-376">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-376">Image displayed at the top of the card.</span></span> <span data-ttu-id="1bf3c-377">縦横比 1:1 平方</span><span class="sxs-lookup"><span data-stu-id="1bf3c-377">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="1bf3c-378">buttons</span><span class="sxs-lookup"><span data-stu-id="1bf3c-378">buttons</span></span> | <span data-ttu-id="1bf3c-379">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="1bf3c-379">Array of action objects</span></span> | <span data-ttu-id="1bf3c-380">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-380">Set of actions applicable to the current card.</span></span> <span data-ttu-id="1bf3c-381">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-381">Maximum 6.</span></span> |
| <span data-ttu-id="1bf3c-382">tap</span><span class="sxs-lookup"><span data-stu-id="1bf3c-382">tap</span></span> | <span data-ttu-id="1bf3c-383">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="1bf3c-383">Action object</span></span> | <span data-ttu-id="1bf3c-384">ユーザーがカード自体をタップするとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-384">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="1bf3c-385">サムネイル カードの例</span><span class="sxs-lookup"><span data-stu-id="1bf3c-385">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="1bf3c-386">追加情報</span><span class="sxs-lookup"><span data-stu-id="1bf3c-386">Additional information</span></span>

<span data-ttu-id="1bf3c-387">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-387">Bot Framework reference:</span></span>

* [<span data-ttu-id="1bf3c-388">サムネイル カード Node.js</span><span class="sxs-lookup"><span data-stu-id="1bf3c-388">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="1bf3c-389">サムネイル カード C#</span><span class="sxs-lookup"><span data-stu-id="1bf3c-389">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="1bf3c-390">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="1bf3c-390">Card collections</span></span>

<span data-ttu-id="1bf3c-391">Teams Card コレクションをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-391">Teams supports Card collections.</span></span>

<span data-ttu-id="1bf3c-392">カード コレクションには、 `builder.AttachmentLayout.carousel` と が含まれます `builder.AttachmentLayout.list` 。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-392">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="1bf3c-393">これらのコレクションには、アダプティブ カード、ヒーロー カード、またはサムネイル カードが含まれる。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-393">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="1bf3c-394">カルーセル コレクション</span><span class="sxs-lookup"><span data-stu-id="1bf3c-394">Carousel collection</span></span>

<span data-ttu-id="1bf3c-395">[カルーセルのレイアウト](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-395">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="1bf3c-396">カルーセル コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="1bf3c-396">Support for carousel collections</span></span>

| <span data-ttu-id="1bf3c-397">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="1bf3c-397">Bots in Teams</span></span> | <span data-ttu-id="1bf3c-398">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1bf3c-398">Messaging extensions</span></span>  | <span data-ttu-id="1bf3c-399">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-399">Connectors</span></span> | <span data-ttu-id="1bf3c-400">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf3c-400">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bf3c-401">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-401">✔</span></span> | <span data-ttu-id="1bf3c-402">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-402">✖</span></span> | <span data-ttu-id="1bf3c-403">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-403">✖</span></span> | <span data-ttu-id="1bf3c-404">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-404">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="1bf3c-405">カルーセルは、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-405">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="1bf3c-406">カルーセル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-406">Properties of a carousel card</span></span>

<span data-ttu-id="1bf3c-407">カルーセル カードのプロパティは、ヒーロー カードとサムネイル カードのプロパティと同じです。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-407">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="1bf3c-408">カルーセル コレクションの例</span><span class="sxs-lookup"><span data-stu-id="1bf3c-408">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="1bf3c-410">カルーセル コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="1bf3c-410">Syntax for carousel collections</span></span>

<span data-ttu-id="1bf3c-411">`builder.AttachmentLayoutTypes.Carousel` はカルーセル コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-411">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="1bf3c-412">リスト コレクション</span><span class="sxs-lookup"><span data-stu-id="1bf3c-412">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="1bf3c-413">リスト コレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="1bf3c-413">Support for list collections</span></span>

<span data-ttu-id="1bf3c-414">リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-414">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="1bf3c-415">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="1bf3c-415">Bots in Teams</span></span> | <span data-ttu-id="1bf3c-416">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1bf3c-416">Messaging extensions</span></span>  | <span data-ttu-id="1bf3c-417">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1bf3c-417">Connectors</span></span> | <span data-ttu-id="1bf3c-418">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="1bf3c-418">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bf3c-419">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-419">✔</span></span> | <span data-ttu-id="1bf3c-420">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-420">✔</span></span> | <span data-ttu-id="1bf3c-421">✖</span><span class="sxs-lookup"><span data-stu-id="1bf3c-421">✖</span></span> | <span data-ttu-id="1bf3c-422">✔</span><span class="sxs-lookup"><span data-stu-id="1bf3c-422">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="1bf3c-423">リスト コレクションの例</span><span class="sxs-lookup"><span data-stu-id="1bf3c-423">Example of a list collection</span></span>

![カードのリストの例](~/assets/images/cards/list.png)

<span data-ttu-id="1bf3c-425">プロパティは、ヒーローやサムネイル カードの場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-425">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="1bf3c-426">リストには、メッセージごとに最大 10 枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-426">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf3c-427">iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-427">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="1bf3c-428">リスト コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="1bf3c-428">Syntax for list collections</span></span>

<span data-ttu-id="1bf3c-429">`builder.AttachmentLayout.list` はリスト コレクションの構文です。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-429">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="1bf3c-430">Teams でサポートされていないカード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-430">Cards not supported in Teams</span></span>

<span data-ttu-id="1bf3c-431">次のカードは Bot Framework によって実装されますが、ボット フレームワークではTeams。</span><span class="sxs-lookup"><span data-stu-id="1bf3c-431">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="1bf3c-432">アニメーション カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-432">Animation cards</span></span>
* <span data-ttu-id="1bf3c-433">オーディオ カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-433">Audio cards</span></span>
* <span data-ttu-id="1bf3c-434">ビデオ カード</span><span class="sxs-lookup"><span data-stu-id="1bf3c-434">Video cards</span></span>
