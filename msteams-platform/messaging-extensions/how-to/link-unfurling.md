---
title: リンク展開
author: clearab
description: Microsoft Teams アプリでメッセージング拡張機能を使用してリンク unfurling を実行する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 32d19fcd44f2475047539350706d2745aeec3691
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587805"
---
# <a name="link-unfurling"></a><span data-ttu-id="17e70-103">リンク展開</span><span class="sxs-lookup"><span data-stu-id="17e70-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> <span data-ttu-id="17e70-104">現時点では、リンク unfurling はモバイルクライアントではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="17e70-104">Currently, Link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="17e70-105">リンク展開を使用すると、特定のドメインの URL がメッセージの作成領域に貼り付けられたときに、アプリが `invoke` アクティビティを受信するように登録することができます。</span><span class="sxs-lookup"><span data-stu-id="17e70-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="17e70-106">に `invoke` は、[メッセージの作成] 領域に貼り付けられた完全な url が格納されています*unfurl*。また、ユーザーが使用を中止して、追加の情報やアクションを提供することができます。</span><span class="sxs-lookup"><span data-stu-id="17e70-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="17e70-107">これは[検索コマンド](~/messaging-extensions/how-to/search-commands/define-search-command.md)とよく似ており、URL が検索用語として機能します。</span><span class="sxs-lookup"><span data-stu-id="17e70-107">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="17e70-108">Azure DevOps messaging extension は、リンク unfurling を使用して、作業項目を指す作成メッセージ領域に貼り付けられた Url を検索します。</span><span class="sxs-lookup"><span data-stu-id="17e70-108">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="17e70-109">次のスクリーンショットでは、ユーザーが Azure DevOps の作業項目の URL を貼り付けて、メッセージング拡張機能がカードに解決されたことを示しています。</span><span class="sxs-lookup"><span data-stu-id="17e70-109">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Link unfurling の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="17e70-111">アプリマニフェストにリンク unfurling を追加する</span><span class="sxs-lookup"><span data-stu-id="17e70-111">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="17e70-112">これを行うには、 `messageHandlers` `composeExtensions` アプリマニフェスト JSON のセクションに新しい配列を追加します。</span><span class="sxs-lookup"><span data-stu-id="17e70-112">To do this you'll add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="17e70-113">そのためには、アプリ Studio のヘルプを使用するか、手動で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="17e70-113">You can either do so with the help of App Studio, or manually.</span></span> <span data-ttu-id="17e70-114">ドメインリストには、たとえば、ワイルドカードを含めることができ `*.example.com` ます。</span><span class="sxs-lookup"><span data-stu-id="17e70-114">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="17e70-115">これは、1つのドメインのセグメントに一致します。に一致させる必要がある場合は `a.b.example.com` 、を使用 `*.*.example.com` します。</span><span class="sxs-lookup"><span data-stu-id="17e70-115">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="17e70-116">App Studio を使用する場合</span><span class="sxs-lookup"><span data-stu-id="17e70-116">Using App Studio</span></span>

1. <span data-ttu-id="17e70-117">App Studio の [マニフェストエディター] タブで、アプリマニフェストを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="17e70-117">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="17e70-118">[**メッセージング内線番号**] ページで、以下のスクリーンショットのように、[**メッセージハンドラ**] セクションで検索するドメインを追加します。</span><span class="sxs-lookup"><span data-stu-id="17e70-118">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![App Studio の [メッセージハンドラ] セクション](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="17e70-120">手動</span><span class="sxs-lookup"><span data-stu-id="17e70-120">Manually</span></span>

<span data-ttu-id="17e70-121">この方法でメッセージング拡張機能がリンクを操作できるようにするには、 `messageHandlers` 次の例に示すように、最初に、配列をアプリのマニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="17e70-121">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="17e70-122">この例は完全なマニフェストではありません。マニフェストの完全な例については、「[マニフェストリファレンス](~/resources/schema/manifest-schema.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="17e70-122">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

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

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="17e70-123">呼び出しを処理する `composeExtension/queryLink`</span><span class="sxs-lookup"><span data-stu-id="17e70-123">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="17e70-124">アプリマニフェストをリッスンするためにドメインを追加したら、呼び出し要求を処理するように web サービスコードを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="17e70-124">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="17e70-125">受信した URL を使用してサービスを検索し、カード応答を作成します。</span><span class="sxs-lookup"><span data-stu-id="17e70-125">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="17e70-126">複数のカードで応答する場合は、最初のカードのみが使用されます。</span><span class="sxs-lookup"><span data-stu-id="17e70-126">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="17e70-127">次のカードの種類をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="17e70-127">We support the following card types:</span></span>

* [<span data-ttu-id="17e70-128">サムネイルカード</span><span class="sxs-lookup"><span data-stu-id="17e70-128">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="17e70-129">英雄カード</span><span class="sxs-lookup"><span data-stu-id="17e70-129">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="17e70-130">Office 365 コネクタカード</span><span class="sxs-lookup"><span data-stu-id="17e70-130">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="17e70-131">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="17e70-131">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="17e70-132">概要については、「[カードとは](~/task-modules-and-cards/what-are-cards.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="17e70-132">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="17e70-133">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="17e70-133">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var card = new HeroCard
    {
        Title = "Hero Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, card);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="17e70-134">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="17e70-134">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="17e70-135">JSON</span><span class="sxs-lookup"><span data-stu-id="17e70-135">JSON</span></span>](#tab/json)

<span data-ttu-id="17e70-136">これは、 `invoke` ボットに送信される例です。</span><span class="sxs-lookup"><span data-stu-id="17e70-136">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="17e70-137">応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="17e70-137">An example of the response is shown below.</span></span>

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
