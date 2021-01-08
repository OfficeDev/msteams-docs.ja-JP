---
title: カード リファレンス
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
keywords: Bot のカード リファレンス
ms.openlocfilehash: 22a4faa932173387cbefe900e30106d063c49e50
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778395"
---
# <a name="cards-reference"></a><span data-ttu-id="99eb5-104">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="99eb5-104">Cards Reference</span></span>

<span data-ttu-id="99eb5-105">このセクションに記載されているカードは、Teams の Bot でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="99eb5-106">Bot Framework で定義されたカードに基づいていますが、すべての Bot Framework カードが Teams でサポートされているわけではなく、独自のカードがいくつか追加されています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="99eb5-107">相違点については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="99eb5-108">カードの例</span><span class="sxs-lookup"><span data-stu-id="99eb5-108">Card examples</span></span>

<span data-ttu-id="99eb5-109">カードの使用方法の詳細については、Bot Builder SDK (v3) のドキュメントで確認できます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="99eb5-110">GitHub の Microsoft/BotBuilder のサンプル リポジトリでは、利用できるコード サンプルを参照することができます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="99eb5-111">.NET</span><span class="sxs-lookup"><span data-stu-id="99eb5-111">.NET</span></span>
  * [<span data-ttu-id="99eb5-112">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="99eb5-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="99eb5-113">カード サンプル コード (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="99eb5-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="99eb5-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="99eb5-114">Node.js</span></span>
  * [<span data-ttu-id="99eb5-115">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="99eb5-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="99eb5-116">カード サンプル コード (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="99eb5-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="99eb5-117">カードの種類</span><span class="sxs-lookup"><span data-stu-id="99eb5-117">Types of cards</span></span>

<span data-ttu-id="99eb5-118">使用できるカードの種類を次の表に示します。</span><span class="sxs-lookup"><span data-stu-id="99eb5-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="99eb5-119">カードの種類</span><span class="sxs-lookup"><span data-stu-id="99eb5-119">Card Type</span></span> | <span data-ttu-id="99eb5-120">説明</span><span class="sxs-lookup"><span data-stu-id="99eb5-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="99eb5-121">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="99eb5-122">高度なカスタマイズができるカード。テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせが可能です。</span><span class="sxs-lookup"><span data-stu-id="99eb5-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="99eb5-123">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="99eb5-124">通常、1 つの大きな画像、1 つまたは複数のボタン、少量のテキストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="99eb5-125">リスト カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-125">List Card</span></span>](#list-card) | <span data-ttu-id="99eb5-126">アイテムのスクロール リスト。</span><span class="sxs-lookup"><span data-stu-id="99eb5-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="99eb5-127">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="99eb5-128">複数のセクション、フィールド、画像、アクションに対応した柔軟なレイアウトです。</span><span class="sxs-lookup"><span data-stu-id="99eb5-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="99eb5-129">レシート カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="99eb5-130">ユーザーに受領確認を提供します。</span><span class="sxs-lookup"><span data-stu-id="99eb5-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="99eb5-131">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="99eb5-132">Bot がユーザーのサインインを要求できるようにします。</span><span class="sxs-lookup"><span data-stu-id="99eb5-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="99eb5-133">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="99eb5-134">通常、1 つのサムネイル画像、短いテキスト、1 つまたは複数のボタンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="99eb5-135">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="99eb5-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="99eb5-136">単一の応答で複数のアイテムを返すときに使用します。</span><span class="sxs-lookup"><span data-stu-id="99eb5-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="99eb5-137">すべてのカードの共通プロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="99eb5-138">インライン カードの画像</span><span class="sxs-lookup"><span data-stu-id="99eb5-138">Inline card images</span></span>

<span data-ttu-id="99eb5-139">公的に使用可能な画像へのリンクを挿入すれば、カードにインライン画像を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="99eb5-140">パフォーマンス上の観点から、公開されているコンテンツ配信ネットワーク (CDN) で画像をホストすることを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="99eb5-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="99eb5-141">画像領域をカバーするように縦横比を保持しながらサイズを拡大または縮小し、カードの縦横比が適切になるように中央からトリミングします。</span><span class="sxs-lookup"><span data-stu-id="99eb5-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="99eb5-142">画像は最大 1024×1024 の PNG、JPEG、または GIF 形式である必要があります。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="99eb5-142">Images must be at most 1024×1024 in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="99eb5-143">プロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-143">Property</span></span> | <span data-ttu-id="99eb5-144">型</span><span class="sxs-lookup"><span data-stu-id="99eb5-144">Type</span></span>  | <span data-ttu-id="99eb5-145">説明</span><span class="sxs-lookup"><span data-stu-id="99eb5-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99eb5-146">url</span><span class="sxs-lookup"><span data-stu-id="99eb5-146">url</span></span> | <span data-ttu-id="99eb5-147">URL</span><span class="sxs-lookup"><span data-stu-id="99eb5-147">URL</span></span> | <span data-ttu-id="99eb5-148">画像の HTTPS URL</span><span class="sxs-lookup"><span data-stu-id="99eb5-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="99eb5-149">alt</span><span class="sxs-lookup"><span data-stu-id="99eb5-149">alt</span></span> | <span data-ttu-id="99eb5-150">文字列</span><span class="sxs-lookup"><span data-stu-id="99eb5-150">String</span></span> | <span data-ttu-id="99eb5-151">画像へのアクセスに関する説明</span><span class="sxs-lookup"><span data-stu-id="99eb5-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="99eb5-152">ボタン</span><span class="sxs-lookup"><span data-stu-id="99eb5-152">Buttons</span></span>

<span data-ttu-id="99eb5-153">ボタンはカードの下部に上下に並んで表示されます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="99eb5-154">ボタンのテキストは常に 1 行で表示され、テキストがボタンの幅を超えた場合は切り捨てられます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="99eb5-155">カードでサポートされている最大数を超えるボタンは表示されません。</span><span class="sxs-lookup"><span data-stu-id="99eb5-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="99eb5-156">詳細については、「[カード アクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="99eb5-157">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="99eb5-157">Card Formatting</span></span>

<span data-ttu-id="99eb5-158">カードのテキストの書式設定の詳細については、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="99eb5-159">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-159">Adaptive card</span></span>

<span data-ttu-id="99eb5-160">カスタマイズができるカードで、テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="99eb5-161">\*\* [アダプティブ カード v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="99eb5-162">アダプティブ カードのサポート</span><span class="sxs-lookup"><span data-stu-id="99eb5-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="99eb5-163">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="99eb5-163">Bots in Teams</span></span> | <span data-ttu-id="99eb5-164">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="99eb5-164">Messaging Extensions</span></span>  | <span data-ttu-id="99eb5-165">コネクタ</span><span class="sxs-lookup"><span data-stu-id="99eb5-165">Connectors</span></span> | <span data-ttu-id="99eb5-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="99eb5-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99eb5-167">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-167">✔</span></span> | <span data-ttu-id="99eb5-168">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-168">✔</span></span> | <span data-ttu-id="99eb5-169">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-169">✖</span></span> | <span data-ttu-id="99eb5-170">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-170">✔</span></span> |
|

> [!NOTE]
> * <span data-ttu-id="99eb5-171">Teams プラットフォームは、アダプティブ カード機能の v1.2 以前をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="99eb5-172">メディア要素は現在、Teams プラットフォームのアダプティブ カード v1.2 ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="99eb5-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>
### <a name="example-adaptive-card"></a><span data-ttu-id="99eb5-173">アダプティブ カードの例</span><span class="sxs-lookup"><span data-stu-id="99eb5-173">Example Adaptive card</span></span>

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="99eb5-175">アダプティブ カードの詳細</span><span class="sxs-lookup"><span data-stu-id="99eb5-175">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="99eb5-176">アダプティブ カードの概要</span><span class="sxs-lookup"><span data-stu-id="99eb5-176">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="99eb5-177">Teams でのアダプティブ カードのアクション</span><span class="sxs-lookup"><span data-stu-id="99eb5-177">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="99eb5-178">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-178">Hero card</span></span>

<span data-ttu-id="99eb5-179">通常、1 つの大きな画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="99eb5-179">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="99eb5-180">ヒーロー カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="99eb5-180">Support for Hero cards</span></span>

| <span data-ttu-id="99eb5-181">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="99eb5-181">Bots in Teams</span></span> | <span data-ttu-id="99eb5-182">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="99eb5-182">Messaging Extensions</span></span>  | <span data-ttu-id="99eb5-183">コネクタ</span><span class="sxs-lookup"><span data-stu-id="99eb5-183">Connectors</span></span> | <span data-ttu-id="99eb5-184">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="99eb5-184">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99eb5-185">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-185">✔</span></span> | <span data-ttu-id="99eb5-186">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-186">✔</span></span> | <span data-ttu-id="99eb5-187">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-187">✖</span></span> | <span data-ttu-id="99eb5-188">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-188">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="99eb5-189">ヒーロー カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-189">Properties of a Hero card</span></span>

| <span data-ttu-id="99eb5-190">プロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-190">Property</span></span> | <span data-ttu-id="99eb5-191">型</span><span class="sxs-lookup"><span data-stu-id="99eb5-191">Type</span></span>  | <span data-ttu-id="99eb5-192">説明</span><span class="sxs-lookup"><span data-stu-id="99eb5-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99eb5-193">title</span><span class="sxs-lookup"><span data-stu-id="99eb5-193">title</span></span> | <span data-ttu-id="99eb5-194">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-194">Rich text</span></span> | <span data-ttu-id="99eb5-195">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="99eb5-195">Title of the card.</span></span> <span data-ttu-id="99eb5-196">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="99eb5-196">Maximum 2 lines.</span></span> |
| <span data-ttu-id="99eb5-197">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="99eb5-197">subtitle</span></span> | <span data-ttu-id="99eb5-198">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-198">Rich text</span></span> | <span data-ttu-id="99eb5-199">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="99eb5-199">Subtitle of the card.</span></span> <span data-ttu-id="99eb5-200">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="99eb5-200">Maximum 2 lines.</span></span>|
| <span data-ttu-id="99eb5-201">テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-201">text</span></span> | <span data-ttu-id="99eb5-202">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-202">Rich text</span></span> | <span data-ttu-id="99eb5-203">テキストはサブタイトルのすぐ下に表示されます。書式設定のオプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-203">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="99eb5-204">images</span><span class="sxs-lookup"><span data-stu-id="99eb5-204">images</span></span> | <span data-ttu-id="99eb5-205">画像の配列</span><span class="sxs-lookup"><span data-stu-id="99eb5-205">Array of images</span></span> | <span data-ttu-id="99eb5-206">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="99eb5-206">Image displayed at top of card.</span></span> <span data-ttu-id="99eb5-207">縦横比は 16:9 です</span><span class="sxs-lookup"><span data-stu-id="99eb5-207">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="99eb5-208">buttons</span><span class="sxs-lookup"><span data-stu-id="99eb5-208">buttons</span></span> | <span data-ttu-id="99eb5-209">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="99eb5-209">Array of action objects</span></span> | <span data-ttu-id="99eb5-210">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="99eb5-210">Set of actions applicable to the current card.</span></span> <span data-ttu-id="99eb5-211">最大で 6 までサポートされています</span><span class="sxs-lookup"><span data-stu-id="99eb5-211">Maximum 6</span></span> |
| <span data-ttu-id="99eb5-212">tap</span><span class="sxs-lookup"><span data-stu-id="99eb5-212">tap</span></span> | <span data-ttu-id="99eb5-213">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="99eb5-213">Action object</span></span> | <span data-ttu-id="99eb5-214">このアクションは、ユーザーがカード自体をタップしたときにアクティブになります</span><span class="sxs-lookup"><span data-stu-id="99eb5-214">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="99eb5-215">ヒーロー カードの例</span><span class="sxs-lookup"><span data-stu-id="99eb5-215">Example Hero card</span></span>

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="99eb5-217">ヒーロー カードの詳細</span><span class="sxs-lookup"><span data-stu-id="99eb5-217">For more information on Hero cards</span></span>

<span data-ttu-id="99eb5-218">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-218">Bot Framework reference:</span></span>

* [<span data-ttu-id="99eb5-219">ヒーロー カード ノード</span><span class="sxs-lookup"><span data-stu-id="99eb5-219">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="99eb5-220">ヒーロー カード C#</span><span class="sxs-lookup"><span data-stu-id="99eb5-220">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="99eb5-221">リスト カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-221">List card</span></span>

<span data-ttu-id="99eb5-222">リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-222">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="99eb5-223">リスト カードは、アイテムのスクロール リストを提供します。</span><span class="sxs-lookup"><span data-stu-id="99eb5-223">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="99eb5-224">リスト カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="99eb5-224">Support for List cards</span></span>

| <span data-ttu-id="99eb5-225">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="99eb5-225">Bots in Teams</span></span> | <span data-ttu-id="99eb5-226">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="99eb5-226">Messaging Extensions</span></span>  | <span data-ttu-id="99eb5-227">コネクタ</span><span class="sxs-lookup"><span data-stu-id="99eb5-227">Connectors</span></span> | <span data-ttu-id="99eb5-228">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="99eb5-228">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99eb5-229">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-229">✔</span></span> | <span data-ttu-id="99eb5-230">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-230">✖</span></span> | <span data-ttu-id="99eb5-231">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-231">✖</span></span> |<span data-ttu-id="99eb5-232">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-232">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="99eb5-233">リスト カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-233">Properties of a List card</span></span>

| <span data-ttu-id="99eb5-234">プロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-234">Property</span></span> | <span data-ttu-id="99eb5-235">型</span><span class="sxs-lookup"><span data-stu-id="99eb5-235">Type</span></span>  | <span data-ttu-id="99eb5-236">説明</span><span class="sxs-lookup"><span data-stu-id="99eb5-236">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99eb5-237">title</span><span class="sxs-lookup"><span data-stu-id="99eb5-237">title</span></span> | <span data-ttu-id="99eb5-238">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-238">Rich text</span></span> | <span data-ttu-id="99eb5-239">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="99eb5-239">Title of the card.</span></span> <span data-ttu-id="99eb5-240">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="99eb5-240">Maximum 2 lines.</span></span>|
| <span data-ttu-id="99eb5-241">アイテム</span><span class="sxs-lookup"><span data-stu-id="99eb5-241">items</span></span> | <span data-ttu-id="99eb5-242">リスト アイテムの配列</span><span class="sxs-lookup"><span data-stu-id="99eb5-242">Array of list items</span></span>  ||
| <span data-ttu-id="99eb5-243">buttons</span><span class="sxs-lookup"><span data-stu-id="99eb5-243">buttons</span></span> | <span data-ttu-id="99eb5-244">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="99eb5-244">Array of action objects</span></span> | <span data-ttu-id="99eb5-245">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="99eb5-245">Set of actions applicable to the current card.</span></span> <span data-ttu-id="99eb5-246">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-246">Maximum 6.</span></span> |

### <a name="example-list-card"></a><span data-ttu-id="99eb5-247">リスト カードの例</span><span class="sxs-lookup"><span data-stu-id="99eb5-247">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="99eb5-248">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-248">Office 365 connector card</span></span>

<span data-ttu-id="99eb5-249">Teams でサポートされています。Bot Framework ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="99eb5-249">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="99eb5-250">Office 365 コネクタ カードには、複数のセクション、フィールド、画像、アクションに対応した柔軟なレイアウトが適用されています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-250">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="99eb5-251">Bot が使用できるように、このカードがコネクタ カードをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="99eb5-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="99eb5-252">コネクタ カードと O365 カードの違いについては、「注意事項」の欄を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="99eb5-253">Office 365 コネクタ カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="99eb5-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="99eb5-254">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="99eb5-254">Bots in Teams</span></span> | <span data-ttu-id="99eb5-255">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="99eb5-255">Messaging Extensions</span></span>  | <span data-ttu-id="99eb5-256">コネクタ</span><span class="sxs-lookup"><span data-stu-id="99eb5-256">Connectors</span></span> | <span data-ttu-id="99eb5-257">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="99eb5-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99eb5-258">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-258">✔</span></span> | <span data-ttu-id="99eb5-259">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-259">✔</span></span> | <span data-ttu-id="99eb5-260">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-260">✔</span></span> | <span data-ttu-id="99eb5-261">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-261">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="99eb5-262">Office 365 コネクタ カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="99eb5-263">プロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-263">Property</span></span> | <span data-ttu-id="99eb5-264">型</span><span class="sxs-lookup"><span data-stu-id="99eb5-264">Type</span></span>  | <span data-ttu-id="99eb5-265">説明</span><span class="sxs-lookup"><span data-stu-id="99eb5-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99eb5-266">title</span><span class="sxs-lookup"><span data-stu-id="99eb5-266">title</span></span> | <span data-ttu-id="99eb5-267">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-267">Rich text</span></span> | <span data-ttu-id="99eb5-268">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="99eb5-268">Title of the card.</span></span> <span data-ttu-id="99eb5-269">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="99eb5-269">Maximum 2 lines.</span></span> |
| <span data-ttu-id="99eb5-270">概要</span><span class="sxs-lookup"><span data-stu-id="99eb5-270">summary</span></span> | <span data-ttu-id="99eb5-271">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-271">Rich text</span></span> | <span data-ttu-id="99eb5-272">カードの概要。</span><span class="sxs-lookup"><span data-stu-id="99eb5-272">Summary of the card.</span></span> <span data-ttu-id="99eb5-273">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="99eb5-273">Maximum 2 lines.</span></span> |
| <span data-ttu-id="99eb5-274">テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-274">text</span></span> | <span data-ttu-id="99eb5-275">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-275">Rich text</span></span> | <span data-ttu-id="99eb5-276">テキストはサブタイトルのすぐ下に表示されます。書式設定のオプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="99eb5-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="99eb5-277">themeColor</span></span> | <span data-ttu-id="99eb5-278">16 進数文字列</span><span class="sxs-lookup"><span data-stu-id="99eb5-278">HEX string</span></span> | <span data-ttu-id="99eb5-279">アプリケーション マニフェストで提供される accentColor よりも優先される色です</span><span class="sxs-lookup"><span data-stu-id="99eb5-279">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="99eb5-280">Office 365 コネクタ カードに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="99eb5-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="99eb5-281">Office 365 コネクタ カードは、[Actioncard アクション](/outlook/actionable-messages/card-reference#actioncard-action)を含む Microsoft Teams で正しく機能します。</span><span class="sxs-lookup"><span data-stu-id="99eb5-281">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="99eb5-282">コネクタからコネクタ カードを使用するのと、Bot でコネクタ カードを使用する際の重要な違いは、カード アクションの処理です。</span><span class="sxs-lookup"><span data-stu-id="99eb5-282">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="99eb5-283">コネクタの場合、エンドポイントが HTTP POST 経由でカードのペイロードを受信します。</span><span class="sxs-lookup"><span data-stu-id="99eb5-283">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="99eb5-284">Bot の場合、`HttpPOST` アクションが、アクション ID と本文のみを Bot に送信する `invoke` アクティビティをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="99eb5-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="99eb5-285">各コネクタ カードは最大 10 個のセクションを表示でき、各セクションに最大 5 つの画像と 5 つのアクションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-285">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="99eb5-286">メッセージ内の他のセクション、画像、アクションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="99eb5-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="99eb5-287">すべてのテキスト フィールドは Markdown と HTML をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="99eb5-288">メッセージの `markdown` プロパティを設定して、Markdown または HTML を使用するセクションを制御することができます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="99eb5-289">既定では、`markdown` は `true` に設定されています。代わりに HTML を使用する場合は、`markdown` を `false` に設定します。</span><span class="sxs-lookup"><span data-stu-id="99eb5-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="99eb5-290">`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="99eb5-291">`activityImage` の表示スタイルを指定するには、`activityImageType` を次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="99eb5-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="99eb5-292">値</span><span class="sxs-lookup"><span data-stu-id="99eb5-292">Value</span></span> | <span data-ttu-id="99eb5-293">説明</span><span class="sxs-lookup"><span data-stu-id="99eb5-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="99eb5-294">既定では、`activityImage` は円としてトリミングされます</span><span class="sxs-lookup"><span data-stu-id="99eb5-294">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="99eb5-295">`activityImage` は四角形として表示され、縦横比は維持されます</span><span class="sxs-lookup"><span data-stu-id="99eb5-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="99eb5-296">コネクタ カードのプロパティのその他の詳細については、「[操作可能なメッセージ カード リファレンス](/outlook/actionable-messages/card-reference)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-296">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="99eb5-297">Microsoft Teams が現在サポートしていないコネクタ カードのプロパティは、以下のみとなります。</span><span class="sxs-lookup"><span data-stu-id="99eb5-297">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="99eb5-298">`startGroup` (Teams では常に `true` として扱われます)</span><span class="sxs-lookup"><span data-stu-id="99eb5-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="99eb5-299">Office 365 コネクタ カードの例</span><span class="sxs-lookup"><span data-stu-id="99eb5-299">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="99eb5-300">レシート カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-300">Receipt card</span></span>

<span data-ttu-id="99eb5-301">Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-301">Supported in Teams.</span></span>

<span data-ttu-id="99eb5-302">Bot がユーザーに受領確認を提供できるようにするカードです。</span><span class="sxs-lookup"><span data-stu-id="99eb5-302">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="99eb5-303">通常は、受領書、税金、合計情報、その他のテキストに含めるアイテムの一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-303">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="99eb5-304">レシート カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="99eb5-304">Support for Receipts cards</span></span>

| <span data-ttu-id="99eb5-305">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="99eb5-305">Bots in Teams</span></span> | <span data-ttu-id="99eb5-306">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="99eb5-306">Messaging Extensions</span></span>  | <span data-ttu-id="99eb5-307">コネクタ</span><span class="sxs-lookup"><span data-stu-id="99eb5-307">Connectors</span></span> | <span data-ttu-id="99eb5-308">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="99eb5-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99eb5-309">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-309">✔</span></span> | <span data-ttu-id="99eb5-310">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-310">✔</span></span> | <span data-ttu-id="99eb5-311">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-311">✖</span></span> | <span data-ttu-id="99eb5-312">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-312">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="99eb5-313">レシート カードの詳細については</span><span class="sxs-lookup"><span data-stu-id="99eb5-313">For more information on Receipt cards</span></span>

<span data-ttu-id="99eb5-314">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-314">Bot Framework reference:</span></span>

* [<span data-ttu-id="99eb5-315">レシート カード ノード</span><span class="sxs-lookup"><span data-stu-id="99eb5-315">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="99eb5-316">レシート カード C#</span><span class="sxs-lookup"><span data-stu-id="99eb5-316">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="99eb5-317">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-317">Signin card</span></span>

<span data-ttu-id="99eb5-318">Bot がユーザーのサインインを要求できるようにするカードです。</span><span class="sxs-lookup"><span data-stu-id="99eb5-318">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="99eb5-319">Bot Framework とは若干異なる形式で Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-319">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="99eb5-320">Teams のサインイン カードは Bot Framework のサインイン カードと似ていますが、Teams のサインイン カードでサポートされているアクションは `signin` と `openUrl` の 2 つのみです。</span><span class="sxs-lookup"><span data-stu-id="99eb5-320">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="99eb5-321">*サインイン アクション* は、サインイン カードだけでなく、Teams のすべてのカードで使用できます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-321">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="99eb5-322">認証の詳細については、「[Microsoft Teams の Bot における認証フロー](~/bots/how-to/authentication/auth-flow-bot.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-322">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="99eb5-323">サインイン カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="99eb5-323">Support for Signin cards</span></span>

| <span data-ttu-id="99eb5-324">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="99eb5-324">Bots in Teams</span></span> | <span data-ttu-id="99eb5-325">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="99eb5-325">Messaging Extensions</span></span>  | <span data-ttu-id="99eb5-326">コネクタ</span><span class="sxs-lookup"><span data-stu-id="99eb5-326">Connectors</span></span> | <span data-ttu-id="99eb5-327">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="99eb5-327">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99eb5-328">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-328">✔</span></span> | <span data-ttu-id="99eb5-329">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-329">✖</span></span> | <span data-ttu-id="99eb5-330">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-330">✖</span></span> | <span data-ttu-id="99eb5-331">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-331">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="99eb5-332">サインイン カードの詳細</span><span class="sxs-lookup"><span data-stu-id="99eb5-332">For more information on Signin cards</span></span>

<span data-ttu-id="99eb5-333">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-333">Bot Framework reference:</span></span>

* [<span data-ttu-id="99eb5-334">サインイン カード ノード</span><span class="sxs-lookup"><span data-stu-id="99eb5-334">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="99eb5-335">サインイン カード C#</span><span class="sxs-lookup"><span data-stu-id="99eb5-335">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="99eb5-336">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-336">Thumbnail card</span></span>

<span data-ttu-id="99eb5-337">通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="99eb5-337">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="99eb5-338">サムネイル カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="99eb5-338">Support for Thumbnail cards</span></span>

| <span data-ttu-id="99eb5-339">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="99eb5-339">Bots in Teams</span></span> | <span data-ttu-id="99eb5-340">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="99eb5-340">Messaging Extensions</span></span>  | <span data-ttu-id="99eb5-341">コネクタ</span><span class="sxs-lookup"><span data-stu-id="99eb5-341">Connectors</span></span> | <span data-ttu-id="99eb5-342">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="99eb5-342">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99eb5-343">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-343">✔</span></span> | <span data-ttu-id="99eb5-344">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-344">✔</span></span> | <span data-ttu-id="99eb5-345">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-345">✖</span></span> | <span data-ttu-id="99eb5-346">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-346">✔</span></span> |
|

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="99eb5-348">サムネイル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-348">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="99eb5-349">プロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-349">Property</span></span> | <span data-ttu-id="99eb5-350">型</span><span class="sxs-lookup"><span data-stu-id="99eb5-350">Type</span></span>  | <span data-ttu-id="99eb5-351">説明</span><span class="sxs-lookup"><span data-stu-id="99eb5-351">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99eb5-352">title</span><span class="sxs-lookup"><span data-stu-id="99eb5-352">title</span></span> | <span data-ttu-id="99eb5-353">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-353">Rich text</span></span> | <span data-ttu-id="99eb5-354">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="99eb5-354">Title of the card.</span></span> <span data-ttu-id="99eb5-355">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="99eb5-355">Maximum 2 lines.</span></span>|
| <span data-ttu-id="99eb5-356">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="99eb5-356">subtitle</span></span> | <span data-ttu-id="99eb5-357">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-357">Rich text</span></span> | <span data-ttu-id="99eb5-358">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="99eb5-358">Subtitle of the card.</span></span> <span data-ttu-id="99eb5-359">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="99eb5-359">Maximum 2 lines.</span></span>|
| <span data-ttu-id="99eb5-360">テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-360">text</span></span> | <span data-ttu-id="99eb5-361">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="99eb5-361">Rich text</span></span> | <span data-ttu-id="99eb5-362">テキストはサブタイトルのすぐ下に表示されます。書式設定のオプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-362">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="99eb5-363">images</span><span class="sxs-lookup"><span data-stu-id="99eb5-363">images</span></span> | <span data-ttu-id="99eb5-364">画像の配列</span><span class="sxs-lookup"><span data-stu-id="99eb5-364">Array of images</span></span> | <span data-ttu-id="99eb5-365">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="99eb5-365">Image displayed at top of card.</span></span> <span data-ttu-id="99eb5-366">縦横比は 1:1 (正方形) です</span><span class="sxs-lookup"><span data-stu-id="99eb5-366">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="99eb5-367">buttons</span><span class="sxs-lookup"><span data-stu-id="99eb5-367">buttons</span></span> | <span data-ttu-id="99eb5-368">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="99eb5-368">Array of action objects</span></span> | <span data-ttu-id="99eb5-369">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="99eb5-369">Set of actions applicable to the current card.</span></span> <span data-ttu-id="99eb5-370">最大で 6 までサポートされています</span><span class="sxs-lookup"><span data-stu-id="99eb5-370">Maximum 6</span></span> |
| <span data-ttu-id="99eb5-371">tap</span><span class="sxs-lookup"><span data-stu-id="99eb5-371">tap</span></span> | <span data-ttu-id="99eb5-372">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="99eb5-372">Action object</span></span> | <span data-ttu-id="99eb5-373">このアクションは、ユーザーがカード自体をタップしたときにアクティブになります</span><span class="sxs-lookup"><span data-stu-id="99eb5-373">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="99eb5-374">サムネイル カードの例</span><span class="sxs-lookup"><span data-stu-id="99eb5-374">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="99eb5-375">関連情報</span><span class="sxs-lookup"><span data-stu-id="99eb5-375">For more information</span></span>

<span data-ttu-id="99eb5-376">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="99eb5-376">Bot Framework reference:</span></span>

* [<span data-ttu-id="99eb5-377">サムネイル カード ノード</span><span class="sxs-lookup"><span data-stu-id="99eb5-377">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="99eb5-378">サムネイル カード C#</span><span class="sxs-lookup"><span data-stu-id="99eb5-378">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="99eb5-379">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="99eb5-379">Card collections</span></span>

<span data-ttu-id="99eb5-380">カード コレクションは Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="99eb5-380">Card collections are supported in Teams.</span></span>

<span data-ttu-id="99eb5-381">カード コレクション: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list` .</span><span class="sxs-lookup"><span data-stu-id="99eb5-381">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="99eb5-382">これらのコレクションには、アダプティブ カード、ヒーロー カード、サムネイル カードが含まれている。</span><span class="sxs-lookup"><span data-stu-id="99eb5-382">These collections contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="99eb5-383">カルーセル コレクション</span><span class="sxs-lookup"><span data-stu-id="99eb5-383">Carousel collection</span></span>

<span data-ttu-id="99eb5-384">[カルーセルのレイアウト](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-384">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="99eb5-385">カルーセル コレクションでのサポート</span><span class="sxs-lookup"><span data-stu-id="99eb5-385">Support for Carousel collections</span></span>

| <span data-ttu-id="99eb5-386">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="99eb5-386">Bots in Teams</span></span> | <span data-ttu-id="99eb5-387">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="99eb5-387">Messaging Extensions</span></span>  | <span data-ttu-id="99eb5-388">コネクタ</span><span class="sxs-lookup"><span data-stu-id="99eb5-388">Connectors</span></span> | <span data-ttu-id="99eb5-389">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="99eb5-389">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99eb5-390">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-390">✔</span></span> | <span data-ttu-id="99eb5-391">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-391">✖</span></span> | <span data-ttu-id="99eb5-392">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-392">✖</span></span> | <span data-ttu-id="99eb5-393">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-393">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="99eb5-394">カルーセルでは、メッセージごとに最大 10 枚のカードを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-394">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="99eb5-395">カルーセル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="99eb5-395">Properties of a Carousel card</span></span>

<span data-ttu-id="99eb5-396">カルーセル カードのプロパティは、ヒーロー カードとサムネイル カードのプロパティと同じです。</span><span class="sxs-lookup"><span data-stu-id="99eb5-396">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="99eb5-397">カルーセル コレクションの例</span><span class="sxs-lookup"><span data-stu-id="99eb5-397">Example Carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="99eb5-399">カルーセル コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="99eb5-399">Syntax for Carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="99eb5-400">リスト コレクション</span><span class="sxs-lookup"><span data-stu-id="99eb5-400">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="99eb5-401">リスト コレクションでのサポート</span><span class="sxs-lookup"><span data-stu-id="99eb5-401">Support for List collections</span></span>

<span data-ttu-id="99eb5-402">リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-402">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="99eb5-403">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="99eb5-403">Bots in Teams</span></span> | <span data-ttu-id="99eb5-404">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="99eb5-404">Messaging Extensions</span></span>  | <span data-ttu-id="99eb5-405">コネクタ</span><span class="sxs-lookup"><span data-stu-id="99eb5-405">Connectors</span></span> | <span data-ttu-id="99eb5-406">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="99eb5-406">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99eb5-407">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-407">✔</span></span> | <span data-ttu-id="99eb5-408">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-408">✔</span></span> | <span data-ttu-id="99eb5-409">✖</span><span class="sxs-lookup"><span data-stu-id="99eb5-409">✖</span></span> | <span data-ttu-id="99eb5-410">✔</span><span class="sxs-lookup"><span data-stu-id="99eb5-410">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="99eb5-411">リスト コレクションの例</span><span class="sxs-lookup"><span data-stu-id="99eb5-411">Example List collection</span></span>

![カードのリストの例](~/assets/images/cards/list.png)

<span data-ttu-id="99eb5-413">プロパティは、ヒーローやサムネイル カードの場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="99eb5-413">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="99eb5-414">リストでは、メッセージごとに最大 10 枚のカードを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="99eb5-414">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="99eb5-415">iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="99eb5-415">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="99eb5-416">リスト コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="99eb5-416">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="99eb5-417">Teams でサポートされていないカード</span><span class="sxs-lookup"><span data-stu-id="99eb5-417">Cards not supported in Teams</span></span>

<span data-ttu-id="99eb5-418">次のカードは Bot Framework によって実装されていますが、Teams ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="99eb5-418">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="99eb5-419">アニメーション カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-419">Animation cards</span></span>
* <span data-ttu-id="99eb5-420">オーディオ カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-420">Audio cards</span></span>
* <span data-ttu-id="99eb5-421">ビデオ カード</span><span class="sxs-lookup"><span data-stu-id="99eb5-421">Video cards</span></span>
