---
title: Link unfurling
author: clearab
description: Microsoft Teams アプリでメッセージング拡張機能を使用してリンク unfurling を実行する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5b20ea303a2c3d085651a53b01af4bb449d386de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675124"
---
# <a name="link-unfurling"></a><span data-ttu-id="75701-103">Link unfurling</span><span class="sxs-lookup"><span data-stu-id="75701-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="75701-104">Link unfurling を使用すると、アプリは、 `invoke`特定のドメインの url が [メッセージの作成] 領域に貼り付けられたときに、アクティビティを受信するように登録できます。</span><span class="sxs-lookup"><span data-stu-id="75701-104">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="75701-105">に`invoke`は、[メッセージの作成] 領域に貼り付けられた完全な url が格納されています。また、ユーザーが使用を中止して、追加の情報や*アクションを提供*することができます。</span><span class="sxs-lookup"><span data-stu-id="75701-105">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="75701-106">これは[検索コマンド](~/messaging-extensions/how-to/search-commands/define-search-command.md)とよく似ており、URL が検索用語として機能します。</span><span class="sxs-lookup"><span data-stu-id="75701-106">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="75701-107">Azure DevOps messaging extension は、リンク unfurling を使用して、作業項目を指す作成メッセージ領域に貼り付けられた Url を検索します。</span><span class="sxs-lookup"><span data-stu-id="75701-107">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="75701-108">次のスクリーンショットでは、ユーザーが Azure DevOps の作業項目の URL を貼り付けて、メッセージング拡張機能がカードに解決されたことを示しています。</span><span class="sxs-lookup"><span data-stu-id="75701-108">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Link unfurling の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="75701-110">アプリマニフェストにリンク unfurling を追加する</span><span class="sxs-lookup"><span data-stu-id="75701-110">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="75701-111">これを行うには、アプリマニフェスト`messageHandlers` JSON の`composeExtensions`セクションに新しい配列を追加します。</span><span class="sxs-lookup"><span data-stu-id="75701-111">To do this you'll add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="75701-112">そのためには、アプリ Studio のヘルプを使用するか、手動で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="75701-112">You can either do so with the help of App Studio, or manually.</span></span> <span data-ttu-id="75701-113">ドメインリストには、たとえば`*.example.com`、ワイルドカードを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="75701-113">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="75701-114">これは、1つのドメインのセグメントに一致します。に一致`a.b.example.com`させる必要がある`*.*.example.com`場合は、を使用します。</span><span class="sxs-lookup"><span data-stu-id="75701-114">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="75701-115">アプリ Studio の使用</span><span class="sxs-lookup"><span data-stu-id="75701-115">Using App Studio</span></span>

1. <span data-ttu-id="75701-116">App Studio の [マニフェストエディター] タブで、アプリマニフェストを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="75701-116">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="75701-117">[**メッセージング内線番号**] ページで、以下のスクリーンショットのように、[**メッセージハンドラ**] セクションで検索するドメインを追加します。</span><span class="sxs-lookup"><span data-stu-id="75701-117">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![App Studio の [メッセージハンドラ] セクション](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="75701-119">手動</span><span class="sxs-lookup"><span data-stu-id="75701-119">Manually</span></span>

<span data-ttu-id="75701-120">この方法でメッセージング拡張機能がリンクを操作できるようにするには、次`messageHandlers`の例に示すように、最初に、配列をアプリのマニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="75701-120">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="75701-121">この例は完全なマニフェストではありません。マニフェストの完全な例については、「[マニフェストリファレンス](~/resources/schema/manifest-schema.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="75701-121">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
],
...
```

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="75701-122">呼び出しを`composeExtension/queryLink`処理する</span><span class="sxs-lookup"><span data-stu-id="75701-122">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="75701-123">アプリマニフェストをリッスンするためにドメインを追加したら、呼び出し要求を処理するように web サービスコードを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="75701-123">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="75701-124">受信した URL を使用してサービスを検索し、カード応答を作成します。</span><span class="sxs-lookup"><span data-stu-id="75701-124">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="75701-125">複数のカードで応答する場合は、最初のカードのみが使用されます。</span><span class="sxs-lookup"><span data-stu-id="75701-125">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="75701-126">次のカードの種類をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="75701-126">We support the following card types:</span></span>

* [<span data-ttu-id="75701-127">サムネイルカード</span><span class="sxs-lookup"><span data-stu-id="75701-127">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="75701-128">英雄カード</span><span class="sxs-lookup"><span data-stu-id="75701-128">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="75701-129">Office 365 コネクタカード</span><span class="sxs-lookup"><span data-stu-id="75701-129">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="75701-130">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="75701-130">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="75701-131">概要については、「[カードとは](~/task-modules-and-cards/what-are-cards.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="75701-131">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="75701-132">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="75701-132">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var heroCard = new ThumbnailCard
    {
        Title = "Thumbnail Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, heroCard);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="75701-133">JavaScript/node.js</span><span class="sxs-lookup"><span data-stu-id="75701-133">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsLinkUnfurlingBot extends TeamsActivityHandler {
  handleTeamsAppBasedLinkQuery(context, query) {
    const attachment = CardFactory.thumbnailCard('Thumbnail Card',
      query.url,
      ['https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png']);

    const result = {
      attachmentLayout: 'list',
      type: 'result',
      attachments: [attachment]
    };

    const response = {
      composeExtension: result
    };
    return response;
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="75701-134">JSON</span><span class="sxs-lookup"><span data-stu-id="75701-134">JSON</span></span>](#tab/json)

<span data-ttu-id="75701-135">これは、 `invoke`ボットに送信される例です。</span><span class="sxs-lookup"><span data-stu-id="75701-135">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="75701-136">応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="75701-136">An example of the response is shown below.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

* * *
