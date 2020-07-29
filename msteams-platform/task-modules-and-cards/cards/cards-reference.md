---
title: カードリファレンス
description: Teams のボットで利用可能なすべてのカードおよびカードアクションについて説明します。
keywords: bot カードリファレンス
ms.openlocfilehash: 7bd1cbea0aec03913c9bce205ae68eedba284637
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434546"
---
# <a name="cards-reference"></a><span data-ttu-id="25458-104">カードリファレンス</span><span class="sxs-lookup"><span data-stu-id="25458-104">Cards Reference</span></span>

<span data-ttu-id="25458-105">このセクションに記載されているカードは、Teams の bot でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="25458-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="25458-106">Bot フレームワークによって定義されたカードに基づいていますが、Teams はすべての Bot フレームワークカードをサポートしておらず、一部を追加しています。</span><span class="sxs-lookup"><span data-stu-id="25458-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="25458-107">相違点については、以下の参考資料を参照してください。</span><span class="sxs-lookup"><span data-stu-id="25458-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="25458-108">カードの例</span><span class="sxs-lookup"><span data-stu-id="25458-108">Card examples</span></span>

<span data-ttu-id="25458-109">カードの使用方法の詳細については、Bot ビルダー SDK (v3) のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="25458-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="25458-110">GitHub の Microsoft/BotBuilder リポジトリで使用可能なコードサンプルもあります。</span><span class="sxs-lookup"><span data-stu-id="25458-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="25458-111">.NET</span><span class="sxs-lookup"><span data-stu-id="25458-111">.NET</span></span>
  * [<span data-ttu-id="25458-112">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="25458-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="25458-113">カードサンプルコード (Bot ビルダー v3)</span><span class="sxs-lookup"><span data-stu-id="25458-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="25458-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="25458-114">Node.js</span></span>
  * [<span data-ttu-id="25458-115">メッセージに添付ファイルとしてカードを追加する</span><span class="sxs-lookup"><span data-stu-id="25458-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="25458-116">カードサンプルコード (Bot ビルダー v3)</span><span class="sxs-lookup"><span data-stu-id="25458-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="25458-117">カードの種類</span><span class="sxs-lookup"><span data-stu-id="25458-117">Types of cards</span></span>

<span data-ttu-id="25458-118">次の表に、使用できるカードの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="25458-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="25458-119">カードの種類</span><span class="sxs-lookup"><span data-stu-id="25458-119">Card Type</span></span> | <span data-ttu-id="25458-120">説明</span><span class="sxs-lookup"><span data-stu-id="25458-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="25458-121">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="25458-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="25458-122">テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含むことができる高度にカスタマイズ可能なカード。</span><span class="sxs-lookup"><span data-stu-id="25458-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="25458-123">英雄カード</span><span class="sxs-lookup"><span data-stu-id="25458-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="25458-124">通常は1つの大きな画像、1つまたは複数のボタン、および少量のテキストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="25458-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="25458-125">カードの一覧表示</span><span class="sxs-lookup"><span data-stu-id="25458-125">List Card</span></span>](#list-card) | <span data-ttu-id="25458-126">アイテムのスクロールリスト。</span><span class="sxs-lookup"><span data-stu-id="25458-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="25458-127">Office 365 コネクタカード</span><span class="sxs-lookup"><span data-stu-id="25458-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="25458-128">複数のセクション、フィールド、画像、アクションを持つ柔軟なレイアウト。</span><span class="sxs-lookup"><span data-stu-id="25458-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="25458-129">レシートカード</span><span class="sxs-lookup"><span data-stu-id="25458-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="25458-130">ユーザーに受信確認を提供します。</span><span class="sxs-lookup"><span data-stu-id="25458-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="25458-131">サインインカード</span><span class="sxs-lookup"><span data-stu-id="25458-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="25458-132">Bot がユーザーのサインインを要求できるようにします。</span><span class="sxs-lookup"><span data-stu-id="25458-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="25458-133">サムネイルカード</span><span class="sxs-lookup"><span data-stu-id="25458-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="25458-134">通常は、1つのサムネイル画像、短いテキスト、1つまたは複数のボタンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="25458-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="25458-135">カードコレクション</span><span class="sxs-lookup"><span data-stu-id="25458-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="25458-136">単一の応答で複数のアイテムを返すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="25458-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="25458-137">すべてのカードの共通プロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="25458-138">インラインカードの画像</span><span class="sxs-lookup"><span data-stu-id="25458-138">Inline card images</span></span>

<span data-ttu-id="25458-139">カードには、公開されている画像へのリンクを含めることで、インライン画像を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="25458-139">Your card can contain an inline image by including a link to your publicly available image.</span></span> <span data-ttu-id="25458-140">パフォーマンス上の理由から、公開されたコンテンツ配信ネットワーク (CDN) で画像をホストすることを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="25458-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="25458-141">画像を拡大または縮小して、画像領域をカバーしてから、カードの適切な縦横比を達成するために、画像の縦横比を維持しながら、サイズを拡大または縮小します。</span><span class="sxs-lookup"><span data-stu-id="25458-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="25458-142">画像は最大1024×1024で、PNG、JPEG、または GIF 形式では 1 MB でなければなりません。アニメーション GIF は正式にはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="25458-142">Images must be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="25458-143">プロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-143">Property</span></span> | <span data-ttu-id="25458-144">型</span><span class="sxs-lookup"><span data-stu-id="25458-144">Type</span></span>  | <span data-ttu-id="25458-145">説明</span><span class="sxs-lookup"><span data-stu-id="25458-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25458-146">url</span><span class="sxs-lookup"><span data-stu-id="25458-146">url</span></span> | <span data-ttu-id="25458-147">URL</span><span class="sxs-lookup"><span data-stu-id="25458-147">URL</span></span> | <span data-ttu-id="25458-148">画像への HTTPS URL</span><span class="sxs-lookup"><span data-stu-id="25458-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="25458-149">alt</span><span class="sxs-lookup"><span data-stu-id="25458-149">alt</span></span> | <span data-ttu-id="25458-150">String</span><span class="sxs-lookup"><span data-stu-id="25458-150">String</span></span> | <span data-ttu-id="25458-151">画像のアクセス可能な説明</span><span class="sxs-lookup"><span data-stu-id="25458-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="25458-152">ボタン</span><span class="sxs-lookup"><span data-stu-id="25458-152">Buttons</span></span>

<span data-ttu-id="25458-153">ボタンは、カードの下部に積み重ねて表示されます。</span><span class="sxs-lookup"><span data-stu-id="25458-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="25458-154">ボタンのテキストは常に1行になり、テキストがボタンの幅を超えた場合は切り捨てられます。</span><span class="sxs-lookup"><span data-stu-id="25458-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="25458-155">カードでサポートされている最大数を超える追加のボタンは表示されません。</span><span class="sxs-lookup"><span data-stu-id="25458-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="25458-156">詳細については、「[カードアクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="25458-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="25458-157">カードの書式設定</span><span class="sxs-lookup"><span data-stu-id="25458-157">Card Formatting</span></span>

<span data-ttu-id="25458-158">カードのテキストの書式設定の詳細については、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="25458-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="25458-159">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="25458-159">Adaptive card</span></span>

<span data-ttu-id="25458-160">テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含むことができるカスタマイズ可能なカード。</span><span class="sxs-lookup"><span data-stu-id="25458-160">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="25458-161">*「* [アダプティブカード v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="25458-161">*See* [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="25458-162">アダプティブカードのサポート</span><span class="sxs-lookup"><span data-stu-id="25458-162">Support for Adaptive cards</span></span>

| <span data-ttu-id="25458-163">Teams のボット</span><span class="sxs-lookup"><span data-stu-id="25458-163">Bots in Teams</span></span> | <span data-ttu-id="25458-164">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="25458-164">Messaging Extensions</span></span>  | <span data-ttu-id="25458-165">コネクタ</span><span class="sxs-lookup"><span data-stu-id="25458-165">Connectors</span></span> | <span data-ttu-id="25458-166">Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="25458-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25458-167">✔</span><span class="sxs-lookup"><span data-stu-id="25458-167">✔</span></span> | <span data-ttu-id="25458-168">✔</span><span class="sxs-lookup"><span data-stu-id="25458-168">✔</span></span> | <span data-ttu-id="25458-169">✖</span><span class="sxs-lookup"><span data-stu-id="25458-169">✖</span></span> | <span data-ttu-id="25458-170">✔</span><span class="sxs-lookup"><span data-stu-id="25458-170">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="25458-171">Media 要素は、現在 Teams プラットフォームのアダプティブカード v2.0 ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="25458-171">Media elements are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>

### <a name="example-adaptive-card"></a><span data-ttu-id="25458-172">アダプティブカードの例</span><span class="sxs-lookup"><span data-stu-id="25458-172">Example Adaptive card</span></span>

![アダプティブカードカードの例](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="25458-174">アダプティブカードの詳細については、</span><span class="sxs-lookup"><span data-stu-id="25458-174">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="25458-175">アダプティブ カードの概要</span><span class="sxs-lookup"><span data-stu-id="25458-175">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="25458-176">Teams でのアダプティブカードアクション</span><span class="sxs-lookup"><span data-stu-id="25458-176">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="25458-177">英雄カード</span><span class="sxs-lookup"><span data-stu-id="25458-177">Hero card</span></span>

<span data-ttu-id="25458-178">通常1つの大きな画像、1つまたは複数のボタンとテキストを含むカード。</span><span class="sxs-lookup"><span data-stu-id="25458-178">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="25458-179">英雄カードのサポート</span><span class="sxs-lookup"><span data-stu-id="25458-179">Support for Hero cards</span></span>

| <span data-ttu-id="25458-180">Teams のボット</span><span class="sxs-lookup"><span data-stu-id="25458-180">Bots in Teams</span></span> | <span data-ttu-id="25458-181">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="25458-181">Messaging Extensions</span></span>  | <span data-ttu-id="25458-182">コネクタ</span><span class="sxs-lookup"><span data-stu-id="25458-182">Connectors</span></span> | <span data-ttu-id="25458-183">Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="25458-183">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25458-184">✔</span><span class="sxs-lookup"><span data-stu-id="25458-184">✔</span></span> | <span data-ttu-id="25458-185">✔</span><span class="sxs-lookup"><span data-stu-id="25458-185">✔</span></span> | <span data-ttu-id="25458-186">✖</span><span class="sxs-lookup"><span data-stu-id="25458-186">✖</span></span> | <span data-ttu-id="25458-187">✔</span><span class="sxs-lookup"><span data-stu-id="25458-187">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="25458-188">英雄カードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-188">Properties of a Hero card</span></span>

| <span data-ttu-id="25458-189">プロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-189">Property</span></span> | <span data-ttu-id="25458-190">型</span><span class="sxs-lookup"><span data-stu-id="25458-190">Type</span></span>  | <span data-ttu-id="25458-191">説明</span><span class="sxs-lookup"><span data-stu-id="25458-191">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25458-192">title</span><span class="sxs-lookup"><span data-stu-id="25458-192">title</span></span> | <span data-ttu-id="25458-193">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-193">Rich text</span></span> | <span data-ttu-id="25458-194">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="25458-194">Title of the card.</span></span> <span data-ttu-id="25458-195">最大2行現在サポートされていない書式設定</span><span class="sxs-lookup"><span data-stu-id="25458-195">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="25458-196">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="25458-196">subtitle</span></span> | <span data-ttu-id="25458-197">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-197">Rich text</span></span> | <span data-ttu-id="25458-198">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="25458-198">Subtitle of the card.</span></span> <span data-ttu-id="25458-199">最大2行現在サポートされていない書式設定</span><span class="sxs-lookup"><span data-stu-id="25458-199">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="25458-200">text</span><span class="sxs-lookup"><span data-stu-id="25458-200">text</span></span> | <span data-ttu-id="25458-201">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-201">Rich text</span></span> | <span data-ttu-id="25458-202">テキストは、サブタイトルのすぐ下に表示されます。書式設定オプションの[カード書式](~/task-modules-and-cards/cards/cards-format.md)を表示する</span><span class="sxs-lookup"><span data-stu-id="25458-202">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="25458-203">images</span><span class="sxs-lookup"><span data-stu-id="25458-203">images</span></span> | <span data-ttu-id="25458-204">画像の配列</span><span class="sxs-lookup"><span data-stu-id="25458-204">Array of images</span></span> | <span data-ttu-id="25458-205">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="25458-205">Image displayed at top of card.</span></span> <span data-ttu-id="25458-206">縦横比16:9</span><span class="sxs-lookup"><span data-stu-id="25458-206">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="25458-207">リモコン</span><span class="sxs-lookup"><span data-stu-id="25458-207">buttons</span></span> | <span data-ttu-id="25458-208">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="25458-208">Array of action objects</span></span> | <span data-ttu-id="25458-209">現在のカードに適用できるアクションのセット。</span><span class="sxs-lookup"><span data-stu-id="25458-209">Set of actions applicable to the current card.</span></span> <span data-ttu-id="25458-210">最大6</span><span class="sxs-lookup"><span data-stu-id="25458-210">Maximum 6</span></span> |
| <span data-ttu-id="25458-211">搭載</span><span class="sxs-lookup"><span data-stu-id="25458-211">tap</span></span> | <span data-ttu-id="25458-212">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="25458-212">Action object</span></span> | <span data-ttu-id="25458-213">このアクションは、ユーザーがカード自体をタップしたときにアクティブになります。</span><span class="sxs-lookup"><span data-stu-id="25458-213">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="25458-214">英雄カードの例</span><span class="sxs-lookup"><span data-stu-id="25458-214">Example Hero card</span></span>

![英雄カードの例](~/assets/images/cards/hero.png)

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="25458-216">英雄カードの詳細については、</span><span class="sxs-lookup"><span data-stu-id="25458-216">For more information on Hero cards</span></span>

<span data-ttu-id="25458-217">Bot フレームワークリファレンス:</span><span class="sxs-lookup"><span data-stu-id="25458-217">Bot Framework reference:</span></span>

* [<span data-ttu-id="25458-218">英雄カードノード</span><span class="sxs-lookup"><span data-stu-id="25458-218">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="25458-219">英雄カード C#</span><span class="sxs-lookup"><span data-stu-id="25458-219">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a><span data-ttu-id="25458-220">カードの一覧表示</span><span class="sxs-lookup"><span data-stu-id="25458-220">List card</span></span>

<span data-ttu-id="25458-221">リストカードは Teams によって追加されており、リストコレクションが提供する機能を超える機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="25458-221">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="25458-222">リストカードは、アイテムのスクロールリストを提供します。</span><span class="sxs-lookup"><span data-stu-id="25458-222">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="25458-223">リストカードのサポート</span><span class="sxs-lookup"><span data-stu-id="25458-223">Support for List cards</span></span>

| <span data-ttu-id="25458-224">Teams のボット</span><span class="sxs-lookup"><span data-stu-id="25458-224">Bots in Teams</span></span> | <span data-ttu-id="25458-225">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="25458-225">Messaging Extensions</span></span>  | <span data-ttu-id="25458-226">コネクタ</span><span class="sxs-lookup"><span data-stu-id="25458-226">Connectors</span></span> | <span data-ttu-id="25458-227">Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="25458-227">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25458-228">✔</span><span class="sxs-lookup"><span data-stu-id="25458-228">✔</span></span> | <span data-ttu-id="25458-229">✖</span><span class="sxs-lookup"><span data-stu-id="25458-229">✖</span></span> | <span data-ttu-id="25458-230">✖</span><span class="sxs-lookup"><span data-stu-id="25458-230">✖</span></span> |<span data-ttu-id="25458-231">✔</span><span class="sxs-lookup"><span data-stu-id="25458-231">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="25458-232">リストカードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-232">Properties of a List card</span></span>

| <span data-ttu-id="25458-233">プロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-233">Property</span></span> | <span data-ttu-id="25458-234">型</span><span class="sxs-lookup"><span data-stu-id="25458-234">Type</span></span>  | <span data-ttu-id="25458-235">説明</span><span class="sxs-lookup"><span data-stu-id="25458-235">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25458-236">title</span><span class="sxs-lookup"><span data-stu-id="25458-236">title</span></span> | <span data-ttu-id="25458-237">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-237">Rich text</span></span> | <span data-ttu-id="25458-238">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="25458-238">Title of the card.</span></span> <span data-ttu-id="25458-239">最大2行現在サポートされていない書式設定</span><span class="sxs-lookup"><span data-stu-id="25458-239">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="25458-240">items</span><span class="sxs-lookup"><span data-stu-id="25458-240">items</span></span> | <span data-ttu-id="25458-241">リストアイテムの配列</span><span class="sxs-lookup"><span data-stu-id="25458-241">Array of list items</span></span>  ||
| <span data-ttu-id="25458-242">リモコン</span><span class="sxs-lookup"><span data-stu-id="25458-242">buttons</span></span> | <span data-ttu-id="25458-243">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="25458-243">Array of action objects</span></span> | <span data-ttu-id="25458-244">現在のカードに適用できるアクションのセット。</span><span class="sxs-lookup"><span data-stu-id="25458-244">Set of actions applicable to the current card.</span></span> <span data-ttu-id="25458-245">最大6。</span><span class="sxs-lookup"><span data-stu-id="25458-245">Maximum 6.</span></span> <span data-ttu-id="25458-246">モバイルでは表示されません。</span><span class="sxs-lookup"><span data-stu-id="25458-246">Does not render on mobile.</span></span> |
|

### <a name="example-list-card"></a><span data-ttu-id="25458-247">リストカードの例</span><span class="sxs-lookup"><span data-stu-id="25458-247">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="25458-248">Office 365 コネクタカード</span><span class="sxs-lookup"><span data-stu-id="25458-248">Office 365 connector card</span></span>

<span data-ttu-id="25458-249">Teams ではサポートされていません。 Bot フレームワークではサポートされません。</span><span class="sxs-lookup"><span data-stu-id="25458-249">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="25458-250">Office 365 コネクタカードには、複数のセクション、フィールド、画像、およびアクションを備えた柔軟なレイアウトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="25458-250">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="25458-251">このカードは、コネクタカードをカプセル化して、bot がそれを使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="25458-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="25458-252">コネクタカードと O365 カードの違いについては、「メモ」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="25458-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="25458-253">Office 365 コネクタカードのサポート</span><span class="sxs-lookup"><span data-stu-id="25458-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="25458-254">Teams のボット</span><span class="sxs-lookup"><span data-stu-id="25458-254">Bots in Teams</span></span> | <span data-ttu-id="25458-255">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="25458-255">Messaging Extensions</span></span>  | <span data-ttu-id="25458-256">コネクタ</span><span class="sxs-lookup"><span data-stu-id="25458-256">Connectors</span></span> | <span data-ttu-id="25458-257">Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="25458-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25458-258">✔</span><span class="sxs-lookup"><span data-stu-id="25458-258">✔</span></span> | <span data-ttu-id="25458-259">✔</span><span class="sxs-lookup"><span data-stu-id="25458-259">✔</span></span> | <span data-ttu-id="25458-260">✔</span><span class="sxs-lookup"><span data-stu-id="25458-260">✔</span></span> | <span data-ttu-id="25458-261">✖</span><span class="sxs-lookup"><span data-stu-id="25458-261">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="25458-262">Office 365 コネクタカードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="25458-263">プロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-263">Property</span></span> | <span data-ttu-id="25458-264">型</span><span class="sxs-lookup"><span data-stu-id="25458-264">Type</span></span>  | <span data-ttu-id="25458-265">説明</span><span class="sxs-lookup"><span data-stu-id="25458-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25458-266">title</span><span class="sxs-lookup"><span data-stu-id="25458-266">title</span></span> | <span data-ttu-id="25458-267">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-267">Rich text</span></span> | <span data-ttu-id="25458-268">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="25458-268">Title of the card.</span></span> <span data-ttu-id="25458-269">最大2行現在サポートされていない書式設定</span><span class="sxs-lookup"><span data-stu-id="25458-269">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="25458-270">summary</span><span class="sxs-lookup"><span data-stu-id="25458-270">summary</span></span> | <span data-ttu-id="25458-271">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-271">Rich text</span></span> | <span data-ttu-id="25458-272">カードの概要。</span><span class="sxs-lookup"><span data-stu-id="25458-272">Summary of the card.</span></span> <span data-ttu-id="25458-273">最大2行現在サポートされていない書式設定</span><span class="sxs-lookup"><span data-stu-id="25458-273">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="25458-274">text</span><span class="sxs-lookup"><span data-stu-id="25458-274">text</span></span> | <span data-ttu-id="25458-275">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-275">Rich text</span></span> | <span data-ttu-id="25458-276">テキストは、サブタイトルのすぐ下に表示されます。書式設定オプションの[カード書式](~/task-modules-and-cards/cards/cards-format.md)を表示する</span><span class="sxs-lookup"><span data-stu-id="25458-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="25458-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="25458-277">themeColor</span></span> | <span data-ttu-id="25458-278">16進文字列</span><span class="sxs-lookup"><span data-stu-id="25458-278">HEX string</span></span> | <span data-ttu-id="25458-279">アプリケーションマニフェストで提供される、表示色をオーバーライドする色</span><span class="sxs-lookup"><span data-stu-id="25458-279">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="25458-280">Office 365 コネクタカードのメモ</span><span class="sxs-lookup"><span data-stu-id="25458-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="25458-281">Office 365 のコネクタカードは、 [Actioncard アクション](/outlook/actionable-messages/card-reference#actioncard-action)を含む Microsoft Teams では正しく機能します。</span><span class="sxs-lookup"><span data-stu-id="25458-281">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="25458-282">コネクタからコネクタカードを使用することと、ボットでコネクタカードを使用することの重要な違いは、カードアクションの処理です。</span><span class="sxs-lookup"><span data-stu-id="25458-282">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="25458-283">コネクタの場合、エンドポイントは HTTP POST 経由でカードのペイロードを受信します。</span><span class="sxs-lookup"><span data-stu-id="25458-283">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="25458-284">Bot の場合、アクションは、 `HttpPOST` `invoke` アクション ID と本文のみを bot に送信するアクティビティをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="25458-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="25458-285">各コネクタカードには最大10個のセクションを表示でき、各セクションには最大5つの画像と5つのアクションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="25458-285">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="25458-286">メッセージ内の追加のセクション、画像、アクションは表示されません。</span><span class="sxs-lookup"><span data-stu-id="25458-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="25458-287">すべてのテキストフィールドは、Markdown と HTML をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="25458-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="25458-288">Markdown または HTML を使用するセクションは、メッセージでプロパティを設定することによって制御できます `markdown` 。</span><span class="sxs-lookup"><span data-stu-id="25458-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="25458-289">既定で `markdown` は、はに設定されています。 `true` 代わりに HTML を使用する場合は、 `markdown` をに設定 `false` します。</span><span class="sxs-lookup"><span data-stu-id="25458-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="25458-290">プロパティを指定すると `themeColor` 、そのプロパティはアプリマニフェストのプロパティより優先され `accentColor` ます。</span><span class="sxs-lookup"><span data-stu-id="25458-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="25458-291">のレンダリングスタイルを指定するに `activityImage` は、次のように設定し `activityImageType` ます。</span><span class="sxs-lookup"><span data-stu-id="25458-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="25458-292">値</span><span class="sxs-lookup"><span data-stu-id="25458-292">Value</span></span> | <span data-ttu-id="25458-293">説明</span><span class="sxs-lookup"><span data-stu-id="25458-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="25458-294">限り`activityImage`円としてトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="25458-294">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="25458-295">`activityImage`四角形として表示され、その縦横比を保持します。</span><span class="sxs-lookup"><span data-stu-id="25458-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="25458-296">コネクタカードのプロパティに関するその他の詳細については、「操作可能な[メッセージカードリファレンス](/outlook/actionable-messages/card-reference)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="25458-296">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="25458-297">Microsoft Teams が現在サポートしていないコネクタカードのプロパティは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="25458-297">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="25458-298">`startGroup`(常に `true` Teams で扱います)</span><span class="sxs-lookup"><span data-stu-id="25458-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="25458-299">Office 365 コネクタカードの例</span><span class="sxs-lookup"><span data-stu-id="25458-299">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="25458-300">レシートカード</span><span class="sxs-lookup"><span data-stu-id="25458-300">Receipt card</span></span>

<span data-ttu-id="25458-301">Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="25458-301">Supported in Teams.</span></span>

<span data-ttu-id="25458-302">Bot がユーザーにレシートを提供できるようにするカード。</span><span class="sxs-lookup"><span data-stu-id="25458-302">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="25458-303">通常、レシート、税金、およびその他のテキストに含めるアイテムの一覧が含まれます。</span><span class="sxs-lookup"><span data-stu-id="25458-303">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="25458-304">領収書カードのサポート</span><span class="sxs-lookup"><span data-stu-id="25458-304">Support for Receipts cards</span></span>

| <span data-ttu-id="25458-305">Teams のボット</span><span class="sxs-lookup"><span data-stu-id="25458-305">Bots in Teams</span></span> | <span data-ttu-id="25458-306">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="25458-306">Messaging Extensions</span></span>  | <span data-ttu-id="25458-307">コネクタ</span><span class="sxs-lookup"><span data-stu-id="25458-307">Connectors</span></span> | <span data-ttu-id="25458-308">Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="25458-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25458-309">✔</span><span class="sxs-lookup"><span data-stu-id="25458-309">✔</span></span> | <span data-ttu-id="25458-310">✔</span><span class="sxs-lookup"><span data-stu-id="25458-310">✔</span></span> | <span data-ttu-id="25458-311">✖</span><span class="sxs-lookup"><span data-stu-id="25458-311">✖</span></span> | <span data-ttu-id="25458-312">✔</span><span class="sxs-lookup"><span data-stu-id="25458-312">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="25458-313">受信カードの詳細については、</span><span class="sxs-lookup"><span data-stu-id="25458-313">For more information on Receipt cards</span></span>

<span data-ttu-id="25458-314">Bot フレームワークリファレンス:</span><span class="sxs-lookup"><span data-stu-id="25458-314">Bot Framework reference:</span></span>

* [<span data-ttu-id="25458-315">レシートカードノード</span><span class="sxs-lookup"><span data-stu-id="25458-315">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="25458-316">レシートカード C#</span><span class="sxs-lookup"><span data-stu-id="25458-316">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a><span data-ttu-id="25458-317">サインインカード</span><span class="sxs-lookup"><span data-stu-id="25458-317">Signin card</span></span>

<span data-ttu-id="25458-318">Bot がユーザーのサインインを要求することを可能にするカード。</span><span class="sxs-lookup"><span data-stu-id="25458-318">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="25458-319">Bot フレームワークで見つかったものとは異なる形式の Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="25458-319">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="25458-320">Teams のサインインカードは bot フレームワークのサインインカードに似ていますが、Teams のサインインカードでは、との2つのアクションのみがサポートされるという例外があり `signin` `openUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="25458-320">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="25458-321">*サインインアクション*は、サインインカードだけでなく、Teams のすべてのカードから使用できます。</span><span class="sxs-lookup"><span data-stu-id="25458-321">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="25458-322">認証の詳細については、「 [bot の Microsoft Teams 認証フロー](~/bots/how-to/authentication/auth-flow-bot.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="25458-322">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="25458-323">サインインカードのサポート</span><span class="sxs-lookup"><span data-stu-id="25458-323">Support for Signin cards</span></span>

| <span data-ttu-id="25458-324">Teams のボット</span><span class="sxs-lookup"><span data-stu-id="25458-324">Bots in Teams</span></span> | <span data-ttu-id="25458-325">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="25458-325">Messaging Extensions</span></span>  | <span data-ttu-id="25458-326">コネクタ</span><span class="sxs-lookup"><span data-stu-id="25458-326">Connectors</span></span> | <span data-ttu-id="25458-327">Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="25458-327">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25458-328">✔</span><span class="sxs-lookup"><span data-stu-id="25458-328">✔</span></span> | <span data-ttu-id="25458-329">✖</span><span class="sxs-lookup"><span data-stu-id="25458-329">✖</span></span> | <span data-ttu-id="25458-330">✖</span><span class="sxs-lookup"><span data-stu-id="25458-330">✖</span></span> | <span data-ttu-id="25458-331">✔</span><span class="sxs-lookup"><span data-stu-id="25458-331">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="25458-332">サインインカードの詳細については、</span><span class="sxs-lookup"><span data-stu-id="25458-332">For more information on Signin cards</span></span>

<span data-ttu-id="25458-333">Bot フレームワークリファレンス:</span><span class="sxs-lookup"><span data-stu-id="25458-333">Bot Framework reference:</span></span>

* [<span data-ttu-id="25458-334">サインインカードのノード</span><span class="sxs-lookup"><span data-stu-id="25458-334">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [<span data-ttu-id="25458-335">サインインカード C#</span><span class="sxs-lookup"><span data-stu-id="25458-335">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a><span data-ttu-id="25458-336">サムネイルカード</span><span class="sxs-lookup"><span data-stu-id="25458-336">Thumbnail card</span></span>

<span data-ttu-id="25458-337">通常は1つのサムネイル画像、1つまたは複数のボタン、テキストを含むカード。</span><span class="sxs-lookup"><span data-stu-id="25458-337">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="25458-338">サムネイルカードのサポート</span><span class="sxs-lookup"><span data-stu-id="25458-338">Support for Thumbnail cards</span></span>

| <span data-ttu-id="25458-339">Teams のボット</span><span class="sxs-lookup"><span data-stu-id="25458-339">Bots in Teams</span></span> | <span data-ttu-id="25458-340">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="25458-340">Messaging Extensions</span></span>  | <span data-ttu-id="25458-341">コネクタ</span><span class="sxs-lookup"><span data-stu-id="25458-341">Connectors</span></span> | <span data-ttu-id="25458-342">Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="25458-342">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25458-343">✔</span><span class="sxs-lookup"><span data-stu-id="25458-343">✔</span></span> | <span data-ttu-id="25458-344">✔</span><span class="sxs-lookup"><span data-stu-id="25458-344">✔</span></span> | <span data-ttu-id="25458-345">✖</span><span class="sxs-lookup"><span data-stu-id="25458-345">✖</span></span> | <span data-ttu-id="25458-346">✔</span><span class="sxs-lookup"><span data-stu-id="25458-346">✔</span></span> |
|

![サムネイルカードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="25458-348">サムネイルカードのプロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-348">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="25458-349">プロパティ</span><span class="sxs-lookup"><span data-stu-id="25458-349">Property</span></span> | <span data-ttu-id="25458-350">型</span><span class="sxs-lookup"><span data-stu-id="25458-350">Type</span></span>  | <span data-ttu-id="25458-351">説明</span><span class="sxs-lookup"><span data-stu-id="25458-351">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25458-352">title</span><span class="sxs-lookup"><span data-stu-id="25458-352">title</span></span> | <span data-ttu-id="25458-353">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-353">Rich text</span></span> | <span data-ttu-id="25458-354">カードのタイトル。</span><span class="sxs-lookup"><span data-stu-id="25458-354">Title of the card.</span></span> <span data-ttu-id="25458-355">最大2行現在サポートされていない書式設定</span><span class="sxs-lookup"><span data-stu-id="25458-355">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="25458-356">サブタイトル</span><span class="sxs-lookup"><span data-stu-id="25458-356">subtitle</span></span> | <span data-ttu-id="25458-357">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-357">Rich text</span></span> | <span data-ttu-id="25458-358">カードのサブタイトル。</span><span class="sxs-lookup"><span data-stu-id="25458-358">Subtitle of the card.</span></span> <span data-ttu-id="25458-359">最大2行現在サポートされていない書式設定</span><span class="sxs-lookup"><span data-stu-id="25458-359">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="25458-360">text</span><span class="sxs-lookup"><span data-stu-id="25458-360">text</span></span> | <span data-ttu-id="25458-361">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="25458-361">Rich text</span></span> | <span data-ttu-id="25458-362">テキストは、サブタイトルのすぐ下に表示されます。書式設定オプションの[カード書式](~/task-modules-and-cards/cards/cards-format.md)を表示する</span><span class="sxs-lookup"><span data-stu-id="25458-362">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="25458-363">images</span><span class="sxs-lookup"><span data-stu-id="25458-363">images</span></span> | <span data-ttu-id="25458-364">画像の配列</span><span class="sxs-lookup"><span data-stu-id="25458-364">Array of images</span></span> | <span data-ttu-id="25458-365">カードの上部に表示される画像。</span><span class="sxs-lookup"><span data-stu-id="25458-365">Image displayed at top of card.</span></span> <span data-ttu-id="25458-366">縦横比 1:1 (正方形)</span><span class="sxs-lookup"><span data-stu-id="25458-366">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="25458-367">リモコン</span><span class="sxs-lookup"><span data-stu-id="25458-367">buttons</span></span> | <span data-ttu-id="25458-368">Action オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="25458-368">Array of action objects</span></span> | <span data-ttu-id="25458-369">現在のカードに適用できるアクションのセット。</span><span class="sxs-lookup"><span data-stu-id="25458-369">Set of actions applicable to the current card.</span></span> <span data-ttu-id="25458-370">最大6</span><span class="sxs-lookup"><span data-stu-id="25458-370">Maximum 6</span></span> |
| <span data-ttu-id="25458-371">搭載</span><span class="sxs-lookup"><span data-stu-id="25458-371">tap</span></span> | <span data-ttu-id="25458-372">Action オブジェクト</span><span class="sxs-lookup"><span data-stu-id="25458-372">Action object</span></span> | <span data-ttu-id="25458-373">このアクションは、ユーザーがカード自体をタップしたときにアクティブになります。</span><span class="sxs-lookup"><span data-stu-id="25458-373">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="25458-374">サムネイルカードの例</span><span class="sxs-lookup"><span data-stu-id="25458-374">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="25458-375">詳細情報</span><span class="sxs-lookup"><span data-stu-id="25458-375">For more information</span></span>

<span data-ttu-id="25458-376">Bot フレームワークリファレンス:</span><span class="sxs-lookup"><span data-stu-id="25458-376">Bot Framework reference:</span></span>

* [<span data-ttu-id="25458-377">サムネイルカードノード</span><span class="sxs-lookup"><span data-stu-id="25458-377">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="25458-378">サムネイルカード C#</span><span class="sxs-lookup"><span data-stu-id="25458-378">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a><span data-ttu-id="25458-379">カードコレクション</span><span class="sxs-lookup"><span data-stu-id="25458-379">Card collections</span></span>

<span data-ttu-id="25458-380">カードコレクションは Teams でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="25458-380">Card collections are supported in Teams.</span></span>

<span data-ttu-id="25458-381">カードコレクションは Bot フレームワークによって提供 `builder.AttachmentLayout.carousel` されます。 `builder.AttachmentLayout.list`</span><span class="sxs-lookup"><span data-stu-id="25458-381">Card collections are provided by the Bot Framework: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="25458-382">これらのコレクションには、アダプティブ、英雄、またはサムネイルカードを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="25458-382">These collections can contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="25458-383">カルーセルコレクション</span><span class="sxs-lookup"><span data-stu-id="25458-383">Carousel collection</span></span>

<span data-ttu-id="25458-384">[カルーセルのレイアウト](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0)は、オプションで、関連付けられたアクションボタンを表示するカルーセルのカードを示しています。</span><span class="sxs-lookup"><span data-stu-id="25458-384">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="25458-385">カルーセルコレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="25458-385">Support for Carousel collections</span></span>

| <span data-ttu-id="25458-386">Teams のボット</span><span class="sxs-lookup"><span data-stu-id="25458-386">Bots in Teams</span></span> | <span data-ttu-id="25458-387">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="25458-387">Messaging Extensions</span></span>  | <span data-ttu-id="25458-388">コネクタ</span><span class="sxs-lookup"><span data-stu-id="25458-388">Connectors</span></span> | <span data-ttu-id="25458-389">Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="25458-389">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25458-390">✔</span><span class="sxs-lookup"><span data-stu-id="25458-390">✔</span></span> | <span data-ttu-id="25458-391">✖</span><span class="sxs-lookup"><span data-stu-id="25458-391">✖</span></span> | <span data-ttu-id="25458-392">✖</span><span class="sxs-lookup"><span data-stu-id="25458-392">✖</span></span> | <span data-ttu-id="25458-393">✔</span><span class="sxs-lookup"><span data-stu-id="25458-393">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="25458-394">カルーセルは、メッセージごとに最大10枚のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="25458-394">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="25458-395">カルーセルのコレクションの例</span><span class="sxs-lookup"><span data-stu-id="25458-395">Example Carousel collection</span></span>

![カードのカルーセルの例](~/assets/images/cards/carousel.png)

<span data-ttu-id="25458-397">プロパティは、英雄またはサムネイルカードの場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="25458-397">Properties are the same as for the hero or thumbnail card.</span></span>

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="25458-398">カルーセルコレクションの構文</span><span class="sxs-lookup"><span data-stu-id="25458-398">Syntax for Carousel collections</span></span>

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a><span data-ttu-id="25458-399">List コレクション</span><span class="sxs-lookup"><span data-stu-id="25458-399">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="25458-400">リストコレクションのサポート</span><span class="sxs-lookup"><span data-stu-id="25458-400">Support for List collections</span></span>

<span data-ttu-id="25458-401">リストレイアウトは、カードの縦に積み上げたリストを表示します。オプションで、関連付けられたアクションボタンを表示します。</span><span class="sxs-lookup"><span data-stu-id="25458-401">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="25458-402">Teams のボット</span><span class="sxs-lookup"><span data-stu-id="25458-402">Bots in Teams</span></span> | <span data-ttu-id="25458-403">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="25458-403">Messaging Extensions</span></span>  | <span data-ttu-id="25458-404">コネクタ</span><span class="sxs-lookup"><span data-stu-id="25458-404">Connectors</span></span> | <span data-ttu-id="25458-405">Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="25458-405">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25458-406">✔</span><span class="sxs-lookup"><span data-stu-id="25458-406">✔</span></span> | <span data-ttu-id="25458-407">✔</span><span class="sxs-lookup"><span data-stu-id="25458-407">✔</span></span> | <span data-ttu-id="25458-408">✖</span><span class="sxs-lookup"><span data-stu-id="25458-408">✖</span></span> | <span data-ttu-id="25458-409">✔</span><span class="sxs-lookup"><span data-stu-id="25458-409">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="25458-410">List コレクションの例</span><span class="sxs-lookup"><span data-stu-id="25458-410">Example List collection</span></span>

![カードリストの例](~/assets/images/cards/list.png)

<span data-ttu-id="25458-412">プロパティは、英雄またはサムネイルカードの場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="25458-412">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="25458-413">リストでは、メッセージごとに最大10個のカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="25458-413">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="25458-414">IOS および Android では、リストカードの一部の組み合わせはまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="25458-414">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="25458-415">リストコレクションの構文</span><span class="sxs-lookup"><span data-stu-id="25458-415">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="25458-416">Teams でサポートされていないカード</span><span class="sxs-lookup"><span data-stu-id="25458-416">Cards not supported in Teams</span></span>

<span data-ttu-id="25458-417">次のカードは Bot フレームワークによって実装されていますが、Teams ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="25458-417">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="25458-418">アニメーションカード</span><span class="sxs-lookup"><span data-stu-id="25458-418">Animation cards</span></span>
* <span data-ttu-id="25458-419">オーディオカード</span><span class="sxs-lookup"><span data-stu-id="25458-419">Audio cards</span></span>
* <span data-ttu-id="25458-420">ビデオカード</span><span class="sxs-lookup"><span data-stu-id="25458-420">Video cards</span></span>
