---
title: カード リファレンス
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
keywords: Bot のカード リファレンス
ms.openlocfilehash: 7c37d05ae4cfd07049eaec6dec5eda0f3312cefa
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346743"
---
# <a name="cards-reference"></a><span data-ttu-id="f7534-104">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="f7534-104">Cards Reference</span></span>

<span data-ttu-id="f7534-105">このセクションに記載されているカードは、Teams の Bot でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f7534-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="f7534-106">Bot Framework で定義されたカードに基づいていますが、すべての Bot Framework カードが Teams でサポートされているわけではなく、独自のカードがいくつか追加されています。</span><span class="sxs-lookup"><span data-stu-id="f7534-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="f7534-107">相違点については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="f7534-108">カードの例</span><span class="sxs-lookup"><span data-stu-id="f7534-108">Card examples</span></span>

<span data-ttu-id="f7534-109">カードの使用方法の詳細については、Bot Builder SDK (v3) のドキュメントで確認できます。</span><span class="sxs-lookup"><span data-stu-id="f7534-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="f7534-110">GitHub の Microsoft/BotBuilder のサンプル リポジトリでは、利用できるコード サンプルを参照することができます。</span><span class="sxs-lookup"><span data-stu-id="f7534-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="f7534-111">.NET</span><span class="sxs-lookup"><span data-stu-id="f7534-111">.NET</span></span>
  * [<span data-ttu-id="f7534-112">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="f7534-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="f7534-113">カード サンプル コード (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="f7534-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="f7534-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="f7534-114">Node.js</span></span>
  * [<span data-ttu-id="f7534-115">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="f7534-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="f7534-116">カード サンプル コード (Bot Builder v3)</span><span class="sxs-lookup"><span data-stu-id="f7534-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="f7534-117">カードの種類</span><span class="sxs-lookup"><span data-stu-id="f7534-117">Types of cards</span></span>

<span data-ttu-id="f7534-118">使用できるカードの種類を次の表に示します。</span><span class="sxs-lookup"><span data-stu-id="f7534-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="f7534-119">カードの種類</span><span class="sxs-lookup"><span data-stu-id="f7534-119">Card Type</span></span> | <span data-ttu-id="f7534-120">説明</span><span class="sxs-lookup"><span data-stu-id="f7534-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="f7534-121">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="f7534-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="f7534-122">高度なカスタマイズができるカード。テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせが可能です。</span><span class="sxs-lookup"><span data-stu-id="f7534-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="f7534-123">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="f7534-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="f7534-124">通常、1 つの大きな画像、1 つまたは複数のボタン、少量のテキストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f7534-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="f7534-125">リスト カード</span><span class="sxs-lookup"><span data-stu-id="f7534-125">List Card</span></span>](#list-card) | <span data-ttu-id="f7534-126">アイテムのスクロール リスト。</span><span class="sxs-lookup"><span data-stu-id="f7534-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="f7534-127">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="f7534-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="f7534-128">複数のセクション、フィールド、画像、アクションに対応した柔軟なレイアウトです。</span><span class="sxs-lookup"><span data-stu-id="f7534-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="f7534-129">レシート カード</span><span class="sxs-lookup"><span data-stu-id="f7534-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="f7534-130">ユーザーに受領確認を提供します。</span><span class="sxs-lookup"><span data-stu-id="f7534-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="f7534-131">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="f7534-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="f7534-132">Bot がユーザーのサインインを要求できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f7534-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="f7534-133">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="f7534-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="f7534-134">通常、1 つのサムネイル画像、短いテキスト、1 つまたは複数のボタンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f7534-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="f7534-135">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="f7534-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="f7534-136">単一の応答で複数のアイテムを返すときに使用します。</span><span class="sxs-lookup"><span data-stu-id="f7534-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="f7534-137">すべてのカードの共通プロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="f7534-138">インライン カードの画像</span><span class="sxs-lookup"><span data-stu-id="f7534-138">Inline card images</span></span>

<span data-ttu-id="f7534-139">公的に使用可能な画像へのリンクを挿入すれば、カードにインライン画像を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f7534-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="f7534-140">パフォーマンス上の観点から、公開されているコンテンツ配信ネットワーク (CDN) で画像をホストすることを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f7534-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="f7534-141">画像領域をカバーするように縦横比を保持しながらサイズを拡大または縮小し、カードの縦横比が適切になるように中央からトリミングします。</span><span class="sxs-lookup"><span data-stu-id="f7534-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="f7534-142">画像は最大 1024×1024 の PNG、JPEG、または GIF 形式である必要があります。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f7534-142">Images must be at most 1024×1024 in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="f7534-143">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-143">Property</span></span> | <span data-ttu-id="f7534-144">型</span><span class="sxs-lookup"><span data-stu-id="f7534-144">Type</span></span>  | <span data-ttu-id="f7534-145">説明</span><span class="sxs-lookup"><span data-stu-id="f7534-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7534-146">url</span><span class="sxs-lookup"><span data-stu-id="f7534-146">url</span></span> | <span data-ttu-id="f7534-147">URL</span><span class="sxs-lookup"><span data-stu-id="f7534-147">URL</span></span> | <span data-ttu-id="f7534-148">画像の HTTPS URL</span><span class="sxs-lookup"><span data-stu-id="f7534-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="f7534-149">alt</span><span class="sxs-lookup"><span data-stu-id="f7534-149">alt</span></span> | <span data-ttu-id="f7534-150">文字列</span><span class="sxs-lookup"><span data-stu-id="f7534-150">String</span></span> | <span data-ttu-id="f7534-151">画像へのアクセスに関する説明</span><span class="sxs-lookup"><span data-stu-id="f7534-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="f7534-152">ボタン</span><span class="sxs-lookup"><span data-stu-id="f7534-152">Buttons</span></span>

<span data-ttu-id="f7534-153">ボタンはカードの下部に上下に並んで表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7534-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="f7534-154">ボタンのテキストは常に 1 行で表示され、テキストがボタンの幅を超えた場合は切り捨てられます。</span><span class="sxs-lookup"><span data-stu-id="f7534-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="f7534-155">カードでサポートされている最大数を超えるボタンは表示されません。</span><span class="sxs-lookup"><span data-stu-id="f7534-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="f7534-156">詳細については、「[カード アクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="f7534-157">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="f7534-157">Card Formatting</span></span>

<span data-ttu-id="f7534-158">カードのテキストの書式設定の詳細については、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="f7534-159">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="f7534-159">Adaptive card</span></span>

<span data-ttu-id="f7534-160">カスタマイズができるカードで、テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f7534-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="f7534-161">\*\* [アダプティブ カード v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="f7534-162">アダプティブ カードのサポート</span><span class="sxs-lookup"><span data-stu-id="f7534-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="f7534-163">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="f7534-163">Bots in Teams</span></span> | <span data-ttu-id="f7534-164">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7534-164">Messaging Extensions</span></span>  | <span data-ttu-id="f7534-165">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7534-165">Connectors</span></span> | <span data-ttu-id="f7534-166">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f7534-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f7534-167">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-167">✔</span></span> | <span data-ttu-id="f7534-168">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-168">✔</span></span> | <span data-ttu-id="f7534-169">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-169">✖</span></span> | <span data-ttu-id="f7534-170">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-170">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="f7534-171">メディア要素は、現在、Teams プラットフォームのアダプティブ カード v1.2 ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f7534-171">Media elements are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>

### <a name="example-adaptive-card"></a><span data-ttu-id="f7534-172">アダプティブ カードの例</span><span class="sxs-lookup"><span data-stu-id="f7534-172">Example Adaptive card</span></span>

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="f7534-174">アダプティブ カードの詳細</span><span class="sxs-lookup"><span data-stu-id="f7534-174">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="f7534-175">アダプティブ カードの概要</span><span class="sxs-lookup"><span data-stu-id="f7534-175">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="f7534-176">Teams でのアダプティブ カードのアクション</span><span class="sxs-lookup"><span data-stu-id="f7534-176">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="f7534-177">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="f7534-177">Hero card</span></span>

<span data-ttu-id="f7534-178">通常、1 つの大きな画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="f7534-178">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="f7534-179">ヒーロー カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="f7534-179">Support for Hero cards</span></span>

| <span data-ttu-id="f7534-180">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="f7534-180">Bots in Teams</span></span> | <span data-ttu-id="f7534-181">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7534-181">Messaging Extensions</span></span>  | <span data-ttu-id="f7534-182">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7534-182">Connectors</span></span> | <span data-ttu-id="f7534-183">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f7534-183">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f7534-184">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-184">✔</span></span> | <span data-ttu-id="f7534-185">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-185">✔</span></span> | <span data-ttu-id="f7534-186">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-186">✖</span></span> | <span data-ttu-id="f7534-187">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-187">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="f7534-188">ヒーロー カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-188">Properties of a Hero card</span></span>

| <span data-ttu-id="f7534-189">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-189">Property</span></span> | <span data-ttu-id="f7534-190">型</span><span class="sxs-lookup"><span data-stu-id="f7534-190">Type</span></span>  | <span data-ttu-id="f7534-191">説明</span><span class="sxs-lookup"><span data-stu-id="f7534-191">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7534-192">title</span><span class="sxs-lookup"><span data-stu-id="f7534-192">title</span></span> | <span data-ttu-id="f7534-193">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-193">Rich text</span></span> | <span data-ttu-id="f7534-194">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="f7534-194">Title of the card.</span></span> <span data-ttu-id="f7534-195">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="f7534-195">Maximum 2 lines.</span></span> |
| <span data-ttu-id="f7534-196">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="f7534-196">subtitle</span></span> | <span data-ttu-id="f7534-197">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-197">Rich text</span></span> | <span data-ttu-id="f7534-198">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="f7534-198">Subtitle of the card.</span></span> <span data-ttu-id="f7534-199">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="f7534-199">Maximum 2 lines.</span></span>|
| <span data-ttu-id="f7534-200">テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-200">text</span></span> | <span data-ttu-id="f7534-201">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-201">Rich text</span></span> | <span data-ttu-id="f7534-202">テキストはサブタイトルのすぐ下に表示されます。書式設定のオプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-202">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="f7534-203">images</span><span class="sxs-lookup"><span data-stu-id="f7534-203">images</span></span> | <span data-ttu-id="f7534-204">画像の配列</span><span class="sxs-lookup"><span data-stu-id="f7534-204">Array of images</span></span> | <span data-ttu-id="f7534-205">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="f7534-205">Image displayed at top of card.</span></span> <span data-ttu-id="f7534-206">縦横比は 16:9 です</span><span class="sxs-lookup"><span data-stu-id="f7534-206">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="f7534-207">buttons</span><span class="sxs-lookup"><span data-stu-id="f7534-207">buttons</span></span> | <span data-ttu-id="f7534-208">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="f7534-208">Array of action objects</span></span> | <span data-ttu-id="f7534-209">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="f7534-209">Set of actions applicable to the current card.</span></span> <span data-ttu-id="f7534-210">最大で 6 までサポートされています</span><span class="sxs-lookup"><span data-stu-id="f7534-210">Maximum 6</span></span> |
| <span data-ttu-id="f7534-211">tap</span><span class="sxs-lookup"><span data-stu-id="f7534-211">tap</span></span> | <span data-ttu-id="f7534-212">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="f7534-212">Action object</span></span> | <span data-ttu-id="f7534-213">このアクションは、ユーザーがカード自体をタップしたときにアクティブになります</span><span class="sxs-lookup"><span data-stu-id="f7534-213">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="f7534-214">ヒーロー カードの例</span><span class="sxs-lookup"><span data-stu-id="f7534-214">Example Hero card</span></span>

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="f7534-216">ヒーロー カードの詳細</span><span class="sxs-lookup"><span data-stu-id="f7534-216">For more information on Hero cards</span></span>

<span data-ttu-id="f7534-217">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-217">Bot Framework reference:</span></span>

* [<span data-ttu-id="f7534-218">ヒーロー カード ノード</span><span class="sxs-lookup"><span data-stu-id="f7534-218">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="f7534-219">ヒーロー カード C#</span><span class="sxs-lookup"><span data-stu-id="f7534-219">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="f7534-220">リスト カード</span><span class="sxs-lookup"><span data-stu-id="f7534-220">List card</span></span>

<span data-ttu-id="f7534-221">リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。</span><span class="sxs-lookup"><span data-stu-id="f7534-221">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="f7534-222">リスト カードは、アイテムのスクロール リストを提供します。</span><span class="sxs-lookup"><span data-stu-id="f7534-222">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="f7534-223">リスト カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="f7534-223">Support for List cards</span></span>

| <span data-ttu-id="f7534-224">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="f7534-224">Bots in Teams</span></span> | <span data-ttu-id="f7534-225">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7534-225">Messaging Extensions</span></span>  | <span data-ttu-id="f7534-226">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7534-226">Connectors</span></span> | <span data-ttu-id="f7534-227">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f7534-227">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f7534-228">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-228">✔</span></span> | <span data-ttu-id="f7534-229">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-229">✖</span></span> | <span data-ttu-id="f7534-230">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-230">✖</span></span> |<span data-ttu-id="f7534-231">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-231">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="f7534-232">リスト カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-232">Properties of a List card</span></span>

| <span data-ttu-id="f7534-233">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-233">Property</span></span> | <span data-ttu-id="f7534-234">型</span><span class="sxs-lookup"><span data-stu-id="f7534-234">Type</span></span>  | <span data-ttu-id="f7534-235">説明</span><span class="sxs-lookup"><span data-stu-id="f7534-235">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7534-236">title</span><span class="sxs-lookup"><span data-stu-id="f7534-236">title</span></span> | <span data-ttu-id="f7534-237">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-237">Rich text</span></span> | <span data-ttu-id="f7534-238">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="f7534-238">Title of the card.</span></span> <span data-ttu-id="f7534-239">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="f7534-239">Maximum 2 lines.</span></span>|
| <span data-ttu-id="f7534-240">アイテム</span><span class="sxs-lookup"><span data-stu-id="f7534-240">items</span></span> | <span data-ttu-id="f7534-241">リスト アイテムの配列</span><span class="sxs-lookup"><span data-stu-id="f7534-241">Array of list items</span></span>  ||
| <span data-ttu-id="f7534-242">buttons</span><span class="sxs-lookup"><span data-stu-id="f7534-242">buttons</span></span> | <span data-ttu-id="f7534-243">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="f7534-243">Array of action objects</span></span> | <span data-ttu-id="f7534-244">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="f7534-244">Set of actions applicable to the current card.</span></span> <span data-ttu-id="f7534-245">最大で 6 までサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f7534-245">Maximum 6.</span></span> |

### <a name="example-list-card"></a><span data-ttu-id="f7534-246">リスト カードの例</span><span class="sxs-lookup"><span data-stu-id="f7534-246">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="f7534-247">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="f7534-247">Office 365 connector card</span></span>

<span data-ttu-id="f7534-248">Teams でサポートされています。Bot Framework ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f7534-248">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="f7534-249">Office 365 コネクタ カードには、複数のセクション、フィールド、画像、アクションに対応した柔軟なレイアウトが適用されています。</span><span class="sxs-lookup"><span data-stu-id="f7534-249">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="f7534-250">Bot が使用できるように、このカードがコネクタ カードをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="f7534-250">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="f7534-251">コネクタ カードと O365 カードの違いについては、「注意事項」の欄を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-251">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="f7534-252">Office 365 コネクタ カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="f7534-252">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="f7534-253">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="f7534-253">Bots in Teams</span></span> | <span data-ttu-id="f7534-254">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7534-254">Messaging Extensions</span></span>  | <span data-ttu-id="f7534-255">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7534-255">Connectors</span></span> | <span data-ttu-id="f7534-256">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f7534-256">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f7534-257">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-257">✔</span></span> | <span data-ttu-id="f7534-258">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-258">✔</span></span> | <span data-ttu-id="f7534-259">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-259">✔</span></span> | <span data-ttu-id="f7534-260">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-260">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="f7534-261">Office 365 コネクタ カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-261">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="f7534-262">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-262">Property</span></span> | <span data-ttu-id="f7534-263">型</span><span class="sxs-lookup"><span data-stu-id="f7534-263">Type</span></span>  | <span data-ttu-id="f7534-264">説明</span><span class="sxs-lookup"><span data-stu-id="f7534-264">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7534-265">title</span><span class="sxs-lookup"><span data-stu-id="f7534-265">title</span></span> | <span data-ttu-id="f7534-266">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-266">Rich text</span></span> | <span data-ttu-id="f7534-267">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="f7534-267">Title of the card.</span></span> <span data-ttu-id="f7534-268">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="f7534-268">Maximum 2 lines.</span></span> |
| <span data-ttu-id="f7534-269">概要</span><span class="sxs-lookup"><span data-stu-id="f7534-269">summary</span></span> | <span data-ttu-id="f7534-270">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-270">Rich text</span></span> | <span data-ttu-id="f7534-271">カードの概要。</span><span class="sxs-lookup"><span data-stu-id="f7534-271">Summary of the card.</span></span> <span data-ttu-id="f7534-272">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="f7534-272">Maximum 2 lines.</span></span> |
| <span data-ttu-id="f7534-273">テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-273">text</span></span> | <span data-ttu-id="f7534-274">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-274">Rich text</span></span> | <span data-ttu-id="f7534-275">テキストはサブタイトルのすぐ下に表示されます。書式設定のオプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-275">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="f7534-276">themeColor</span><span class="sxs-lookup"><span data-stu-id="f7534-276">themeColor</span></span> | <span data-ttu-id="f7534-277">16 進数文字列</span><span class="sxs-lookup"><span data-stu-id="f7534-277">HEX string</span></span> | <span data-ttu-id="f7534-278">アプリケーション マニフェストで提供される accentColor よりも優先される色です</span><span class="sxs-lookup"><span data-stu-id="f7534-278">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="f7534-279">Office 365 コネクタ カードに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="f7534-279">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="f7534-280">Office 365 コネクタ カードは、[Actioncard アクション](/outlook/actionable-messages/card-reference#actioncard-action)を含む Microsoft Teams で正しく機能します。</span><span class="sxs-lookup"><span data-stu-id="f7534-280">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="f7534-281">コネクタからコネクタ カードを使用するのと、Bot でコネクタ カードを使用する際の重要な違いは、カード アクションの処理です。</span><span class="sxs-lookup"><span data-stu-id="f7534-281">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="f7534-282">コネクタの場合、エンドポイントが HTTP POST 経由でカードのペイロードを受信します。</span><span class="sxs-lookup"><span data-stu-id="f7534-282">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="f7534-283">Bot の場合、`HttpPOST` アクションが、アクション ID と本文のみを Bot に送信する `invoke` アクティビティをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="f7534-283">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="f7534-284">各コネクタ カードは最大 10 個のセクションを表示でき、各セクションに最大 5 つの画像と 5 つのアクションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f7534-284">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="f7534-285">メッセージ内の他のセクション、画像、アクションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="f7534-285">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="f7534-286">すべてのテキスト フィールドは Markdown と HTML をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f7534-286">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="f7534-287">メッセージの `markdown` プロパティを設定して、Markdown または HTML を使用するセクションを制御することができます。</span><span class="sxs-lookup"><span data-stu-id="f7534-287">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="f7534-288">既定では、`markdown` は `true` に設定されています。代わりに HTML を使用する場合は、`markdown` を `false` に設定します。</span><span class="sxs-lookup"><span data-stu-id="f7534-288">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="f7534-289">`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="f7534-289">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="f7534-290">`activityImage` の表示スタイルを指定するには、`activityImageType` を次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="f7534-290">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="f7534-291">値</span><span class="sxs-lookup"><span data-stu-id="f7534-291">Value</span></span> | <span data-ttu-id="f7534-292">説明</span><span class="sxs-lookup"><span data-stu-id="f7534-292">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="f7534-293">既定では、`activityImage` は円としてトリミングされます</span><span class="sxs-lookup"><span data-stu-id="f7534-293">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="f7534-294">`activityImage` は四角形として表示され、縦横比は維持されます</span><span class="sxs-lookup"><span data-stu-id="f7534-294">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="f7534-295">コネクタ カードのプロパティのその他の詳細については、「[操作可能なメッセージ カード リファレンス](/outlook/actionable-messages/card-reference)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-295">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="f7534-296">Microsoft Teams が現在サポートしていないコネクタ カードのプロパティは、以下のみとなります。</span><span class="sxs-lookup"><span data-stu-id="f7534-296">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="f7534-297">`startGroup` (Teams では常に `true` として扱われます)</span><span class="sxs-lookup"><span data-stu-id="f7534-297">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="f7534-298">Office 365 コネクタ カードの例</span><span class="sxs-lookup"><span data-stu-id="f7534-298">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="f7534-299">レシート カード</span><span class="sxs-lookup"><span data-stu-id="f7534-299">Receipt card</span></span>

<span data-ttu-id="f7534-300">Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f7534-300">Supported in Teams.</span></span>

<span data-ttu-id="f7534-301">Bot がユーザーに受領確認を提供できるようにするカードです。</span><span class="sxs-lookup"><span data-stu-id="f7534-301">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="f7534-302">通常は、受領書、税金、合計情報、その他のテキストに含めるアイテムの一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f7534-302">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="f7534-303">レシート カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="f7534-303">Support for Receipts cards</span></span>

| <span data-ttu-id="f7534-304">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="f7534-304">Bots in Teams</span></span> | <span data-ttu-id="f7534-305">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7534-305">Messaging Extensions</span></span>  | <span data-ttu-id="f7534-306">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7534-306">Connectors</span></span> | <span data-ttu-id="f7534-307">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f7534-307">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f7534-308">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-308">✔</span></span> | <span data-ttu-id="f7534-309">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-309">✔</span></span> | <span data-ttu-id="f7534-310">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-310">✖</span></span> | <span data-ttu-id="f7534-311">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-311">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="f7534-312">レシート カードの詳細については</span><span class="sxs-lookup"><span data-stu-id="f7534-312">For more information on Receipt cards</span></span>

<span data-ttu-id="f7534-313">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-313">Bot Framework reference:</span></span>

* [<span data-ttu-id="f7534-314">レシート カード ノード</span><span class="sxs-lookup"><span data-stu-id="f7534-314">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="f7534-315">レシート カード C#</span><span class="sxs-lookup"><span data-stu-id="f7534-315">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="f7534-316">サインイン カード</span><span class="sxs-lookup"><span data-stu-id="f7534-316">Signin card</span></span>

<span data-ttu-id="f7534-317">Bot がユーザーのサインインを要求できるようにするカードです。</span><span class="sxs-lookup"><span data-stu-id="f7534-317">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="f7534-318">Bot Framework とは若干異なる形式で Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f7534-318">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="f7534-319">Teams のサインイン カードは Bot Framework のサインイン カードと似ていますが、Teams のサインイン カードでサポートされているアクションは `signin` と `openUrl` の 2 つのみです。</span><span class="sxs-lookup"><span data-stu-id="f7534-319">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="f7534-320">*サインイン アクション* は、サインイン カードだけでなく、Teams のすべてのカードで使用できます。</span><span class="sxs-lookup"><span data-stu-id="f7534-320">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="f7534-321">認証の詳細については、「[Microsoft Teams の Bot における認証フロー](~/bots/how-to/authentication/auth-flow-bot.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-321">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="f7534-322">サインイン カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="f7534-322">Support for Signin cards</span></span>

| <span data-ttu-id="f7534-323">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="f7534-323">Bots in Teams</span></span> | <span data-ttu-id="f7534-324">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7534-324">Messaging Extensions</span></span>  | <span data-ttu-id="f7534-325">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7534-325">Connectors</span></span> | <span data-ttu-id="f7534-326">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f7534-326">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f7534-327">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-327">✔</span></span> | <span data-ttu-id="f7534-328">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-328">✖</span></span> | <span data-ttu-id="f7534-329">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-329">✖</span></span> | <span data-ttu-id="f7534-330">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-330">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="f7534-331">サインイン カードの詳細</span><span class="sxs-lookup"><span data-stu-id="f7534-331">For more information on Signin cards</span></span>

<span data-ttu-id="f7534-332">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-332">Bot Framework reference:</span></span>

* [<span data-ttu-id="f7534-333">サインイン カード ノード</span><span class="sxs-lookup"><span data-stu-id="f7534-333">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="f7534-334">サインイン カード C#</span><span class="sxs-lookup"><span data-stu-id="f7534-334">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="f7534-335">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="f7534-335">Thumbnail card</span></span>

<span data-ttu-id="f7534-336">通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。</span><span class="sxs-lookup"><span data-stu-id="f7534-336">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="f7534-337">サムネイル カードでのサポート</span><span class="sxs-lookup"><span data-stu-id="f7534-337">Support for Thumbnail cards</span></span>

| <span data-ttu-id="f7534-338">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="f7534-338">Bots in Teams</span></span> | <span data-ttu-id="f7534-339">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7534-339">Messaging Extensions</span></span>  | <span data-ttu-id="f7534-340">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7534-340">Connectors</span></span> | <span data-ttu-id="f7534-341">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f7534-341">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f7534-342">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-342">✔</span></span> | <span data-ttu-id="f7534-343">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-343">✔</span></span> | <span data-ttu-id="f7534-344">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-344">✖</span></span> | <span data-ttu-id="f7534-345">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-345">✔</span></span> |
|

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="f7534-347">サムネイル カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-347">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="f7534-348">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f7534-348">Property</span></span> | <span data-ttu-id="f7534-349">型</span><span class="sxs-lookup"><span data-stu-id="f7534-349">Type</span></span>  | <span data-ttu-id="f7534-350">説明</span><span class="sxs-lookup"><span data-stu-id="f7534-350">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7534-351">title</span><span class="sxs-lookup"><span data-stu-id="f7534-351">title</span></span> | <span data-ttu-id="f7534-352">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-352">Rich text</span></span> | <span data-ttu-id="f7534-353">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="f7534-353">Title of the card.</span></span> <span data-ttu-id="f7534-354">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="f7534-354">Maximum 2 lines.</span></span>|
| <span data-ttu-id="f7534-355">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="f7534-355">subtitle</span></span> | <span data-ttu-id="f7534-356">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-356">Rich text</span></span> | <span data-ttu-id="f7534-357">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="f7534-357">Subtitle of the card.</span></span> <span data-ttu-id="f7534-358">最大 2 行。</span><span class="sxs-lookup"><span data-stu-id="f7534-358">Maximum 2 lines.</span></span>|
| <span data-ttu-id="f7534-359">テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-359">text</span></span> | <span data-ttu-id="f7534-360">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="f7534-360">Rich text</span></span> | <span data-ttu-id="f7534-361">テキストはサブタイトルのすぐ下に表示されます。書式設定のオプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-361">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="f7534-362">images</span><span class="sxs-lookup"><span data-stu-id="f7534-362">images</span></span> | <span data-ttu-id="f7534-363">画像の配列</span><span class="sxs-lookup"><span data-stu-id="f7534-363">Array of images</span></span> | <span data-ttu-id="f7534-364">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="f7534-364">Image displayed at top of card.</span></span> <span data-ttu-id="f7534-365">縦横比は 1:1 (正方形) です</span><span class="sxs-lookup"><span data-stu-id="f7534-365">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="f7534-366">buttons</span><span class="sxs-lookup"><span data-stu-id="f7534-366">buttons</span></span> | <span data-ttu-id="f7534-367">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="f7534-367">Array of action objects</span></span> | <span data-ttu-id="f7534-368">現在のカードに適用できるアクション一式。</span><span class="sxs-lookup"><span data-stu-id="f7534-368">Set of actions applicable to the current card.</span></span> <span data-ttu-id="f7534-369">最大で 6 までサポートされています</span><span class="sxs-lookup"><span data-stu-id="f7534-369">Maximum 6</span></span> |
| <span data-ttu-id="f7534-370">tap</span><span class="sxs-lookup"><span data-stu-id="f7534-370">tap</span></span> | <span data-ttu-id="f7534-371">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="f7534-371">Action object</span></span> | <span data-ttu-id="f7534-372">このアクションは、ユーザーがカード自体をタップしたときにアクティブになります</span><span class="sxs-lookup"><span data-stu-id="f7534-372">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="f7534-373">サムネイル カードの例</span><span class="sxs-lookup"><span data-stu-id="f7534-373">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="f7534-374">関連情報</span><span class="sxs-lookup"><span data-stu-id="f7534-374">For more information</span></span>

<span data-ttu-id="f7534-375">以下の Bot Framework リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7534-375">Bot Framework reference:</span></span>

* [<span data-ttu-id="f7534-376">サムネイル カード ノード</span><span class="sxs-lookup"><span data-stu-id="f7534-376">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="f7534-377">サムネイル カード C#</span><span class="sxs-lookup"><span data-stu-id="f7534-377">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="f7534-378">カード コレクション</span><span class="sxs-lookup"><span data-stu-id="f7534-378">Card collections</span></span>

<span data-ttu-id="f7534-379">カード コレクションは Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f7534-379">Card collections are supported in Teams.</span></span>

<span data-ttu-id="f7534-380">`builder.AttachmentLayout.carousel` と `builder.AttachmentLayout.list` のカード コレクションが Bot Framework によって提供されています。</span><span class="sxs-lookup"><span data-stu-id="f7534-380">Card collections are provided by the Bot Framework: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="f7534-381">これらのコレクションには、アダプティブ、ヒーロー、サムネイルのカードを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f7534-381">These collections can contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="f7534-382">カルーセル コレクション</span><span class="sxs-lookup"><span data-stu-id="f7534-382">Carousel collection</span></span>

<span data-ttu-id="f7534-383">[カルーセルのレイアウト](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="f7534-383">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="f7534-384">カルーセル コレクションでのサポート</span><span class="sxs-lookup"><span data-stu-id="f7534-384">Support for Carousel collections</span></span>

| <span data-ttu-id="f7534-385">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="f7534-385">Bots in Teams</span></span> | <span data-ttu-id="f7534-386">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7534-386">Messaging Extensions</span></span>  | <span data-ttu-id="f7534-387">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7534-387">Connectors</span></span> | <span data-ttu-id="f7534-388">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f7534-388">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f7534-389">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-389">✔</span></span> | <span data-ttu-id="f7534-390">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-390">✖</span></span> | <span data-ttu-id="f7534-391">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-391">✖</span></span> | <span data-ttu-id="f7534-392">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-392">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="f7534-393">カルーセルでは、メッセージごとに最大 10 枚のカードを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="f7534-393">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="f7534-394">カルーセル コレクションの例</span><span class="sxs-lookup"><span data-stu-id="f7534-394">Example Carousel collection</span></span>

![カードのカルーセルの例](~/assets/images/cards/carousel.png)

<span data-ttu-id="f7534-396">プロパティは、ヒーローやサムネイル カードの場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="f7534-396">Properties are the same as for the hero or thumbnail card.</span></span>

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="f7534-397">カルーセル コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="f7534-397">Syntax for Carousel collections</span></span>

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a><span data-ttu-id="f7534-398">リスト コレクション</span><span class="sxs-lookup"><span data-stu-id="f7534-398">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="f7534-399">リスト コレクションでのサポート</span><span class="sxs-lookup"><span data-stu-id="f7534-399">Support for List collections</span></span>

<span data-ttu-id="f7534-400">リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。</span><span class="sxs-lookup"><span data-stu-id="f7534-400">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="f7534-401">Teams の Bot</span><span class="sxs-lookup"><span data-stu-id="f7534-401">Bots in Teams</span></span> | <span data-ttu-id="f7534-402">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="f7534-402">Messaging Extensions</span></span>  | <span data-ttu-id="f7534-403">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7534-403">Connectors</span></span> | <span data-ttu-id="f7534-404">Bot Framework</span><span class="sxs-lookup"><span data-stu-id="f7534-404">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f7534-405">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-405">✔</span></span> | <span data-ttu-id="f7534-406">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-406">✔</span></span> | <span data-ttu-id="f7534-407">✖</span><span class="sxs-lookup"><span data-stu-id="f7534-407">✖</span></span> | <span data-ttu-id="f7534-408">✔</span><span class="sxs-lookup"><span data-stu-id="f7534-408">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="f7534-409">リスト コレクションの例</span><span class="sxs-lookup"><span data-stu-id="f7534-409">Example List collection</span></span>

![カードのリストの例](~/assets/images/cards/list.png)

<span data-ttu-id="f7534-411">プロパティは、ヒーローやサムネイル カードの場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="f7534-411">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="f7534-412">リストでは、メッセージごとに最大 10 枚のカードを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="f7534-412">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="f7534-413">iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f7534-413">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="f7534-414">リスト コレクションの構文</span><span class="sxs-lookup"><span data-stu-id="f7534-414">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="f7534-415">Teams でサポートされていないカード</span><span class="sxs-lookup"><span data-stu-id="f7534-415">Cards not supported in Teams</span></span>

<span data-ttu-id="f7534-416">次のカードは Bot Framework によって実装されていますが、Teams ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f7534-416">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="f7534-417">アニメーション カード</span><span class="sxs-lookup"><span data-stu-id="f7534-417">Animation cards</span></span>
* <span data-ttu-id="f7534-418">オーディオ カード</span><span class="sxs-lookup"><span data-stu-id="f7534-418">Audio cards</span></span>
* <span data-ttu-id="f7534-419">ビデオ カード</span><span class="sxs-lookup"><span data-stu-id="f7534-419">Video cards</span></span>
