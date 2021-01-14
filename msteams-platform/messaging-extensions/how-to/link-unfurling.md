---
title: リンク展開
author: clearab
description: Microsoft Teams アプリでメッセージング拡張機能を使用してリンクの分岐を実行する方法。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 0d488638e63b8ec78bfa5bed8cf6f4f037883fb1
ms.sourcegitcommit: bf61ae5ad2afa4efdb0311158184d0cbb9c40174
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "49845638"
---
# <a name="link-unfurling"></a><span data-ttu-id="f90e6-103">リンク展開</span><span class="sxs-lookup"><span data-stu-id="f90e6-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> <span data-ttu-id="f90e6-104">現時点では、モバイル クライアントではリンクの分岐はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f90e6-104">Currently, Link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="f90e6-105">リンク展開を使用すると、特定のドメインの URL がメッセージの作成領域に貼り付けられたときに、アプリが `invoke` アクティビティを受信するように登録することができます。</span><span class="sxs-lookup"><span data-stu-id="f90e6-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="f90e6-106">作成 `invoke` メッセージ領域に貼り付けされた完全な URL が含まれるので、ユーザーがリンクを解除して追加の情報やアクションを提供できるカードで応答できます。</span><span class="sxs-lookup"><span data-stu-id="f90e6-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="f90e6-107">これは検索コマンドと非常に [似て機能し](~/messaging-extensions/how-to/search-commands/define-search-command.md)、URL は検索用語として機能します。</span><span class="sxs-lookup"><span data-stu-id="f90e6-107">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="f90e6-108">Azure DevOps メッセージング拡張機能は、リンクの分岐を使用して、作業項目を指すメッセージ作成領域に貼り付けされた URL を検索します。</span><span class="sxs-lookup"><span data-stu-id="f90e6-108">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="f90e6-109">次のスクリーンショットでは、ユーザーが Azure DevOps の作業項目の URL に貼り付け、メッセージング拡張機能がカードに解決されています。</span><span class="sxs-lookup"><span data-stu-id="f90e6-109">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![リンクの分岐の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="f90e6-111">アプリ マニフェストにリンクの分岐を追加する</span><span class="sxs-lookup"><span data-stu-id="f90e6-111">Add link unfurling to your app manifest</span></span>

 <span data-ttu-id="f90e6-112">リンク展開をアプリ マニフェストに追加するには、アプリ マニフェスト JSON のセクションに新しい `messageHandlers` `composeExtensions` 配列を追加します。</span><span class="sxs-lookup"><span data-stu-id="f90e6-112">To add link unfurling to your app manifest add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="f90e6-113">配列は、App Studio のヘルプを使用して追加するか、手動で追加できます。</span><span class="sxs-lookup"><span data-stu-id="f90e6-113">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="f90e6-114">たとえば、ドメイン一覧にはワイルドカードを含めできます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="f90e6-114">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="f90e6-115">これは、ドメインの 1 つのセグメントと正確に一致します。if you need to match `a.b.example.com` then use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="f90e6-115">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="f90e6-116">直接またはワイルドカードを使用して、制御の外部にあるドメインを追加しません。</span><span class="sxs-lookup"><span data-stu-id="f90e6-116">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="f90e6-117">たとえば、yourapp.onmicrosoft.comは有効ですが、\*.onmicrosoft.comは無効です。</span><span class="sxs-lookup"><span data-stu-id="f90e6-117">For example, yourapp.onmicrosoft.com is valid, but \*.onmicrosoft.com is not valid.</span></span> <span data-ttu-id="f90e6-118">また、トップ レベル ドメインは禁止されています。</span><span class="sxs-lookup"><span data-stu-id="f90e6-118">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="f90e6-119">たとえば、*.com、*.org などです。</span><span class="sxs-lookup"><span data-stu-id="f90e6-119">For example, \*.com, \*.org.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="f90e6-120">App Studio を使用する場合</span><span class="sxs-lookup"><span data-stu-id="f90e6-120">Using App Studio</span></span>

1. <span data-ttu-id="f90e6-121">App Studio の [マニフェスト エディター] タブで、アプリ マニフェストを読み込む。</span><span class="sxs-lookup"><span data-stu-id="f90e6-121">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="f90e6-122">[ **メッセージングの拡張機能] ページ** で、次のスクリーンショットに示すように、[ **メッセージ** ハンドラー] セクションで探すドメインを追加します。</span><span class="sxs-lookup"><span data-stu-id="f90e6-122">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![App Studio のメッセージ ハンドラー セクション](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="f90e6-124">手動</span><span class="sxs-lookup"><span data-stu-id="f90e6-124">Manually</span></span>

<span data-ttu-id="f90e6-125">この方法でメッセージング拡張機能がリンクとやり取りするには、まず、次の例に示すアプリ マニフェストに配列を `messageHandlers` 追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f90e6-125">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="f90e6-126">この例は完全なマニフェストではありません [。マニフェストの](~/resources/schema/manifest-schema.md) 完全な例については、マニフェスト リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f90e6-126">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

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

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="f90e6-127">呼び出しの `composeExtension/queryLink` 処理</span><span class="sxs-lookup"><span data-stu-id="f90e6-127">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="f90e6-128">アプリ マニフェストをリッスンするドメインを追加したら、呼び出し要求を処理するために Web サービス コードを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f90e6-128">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="f90e6-129">受け取った URL を使用してサービスを検索し、カードの応答を作成します。</span><span class="sxs-lookup"><span data-stu-id="f90e6-129">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="f90e6-130">複数のカードで応答する場合は、最初のカードだけが使用されます。</span><span class="sxs-lookup"><span data-stu-id="f90e6-130">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="f90e6-131">次のカードの種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f90e6-131">We support the following card types:</span></span>

* [<span data-ttu-id="f90e6-132">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="f90e6-132">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="f90e6-133">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="f90e6-133">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="f90e6-134">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="f90e6-134">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="f90e6-135">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="f90e6-135">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="f90e6-136">概要 [については、「カードについて](~/task-modules-and-cards/what-are-cards.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f90e6-136">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f90e6-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f90e6-137">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f90e6-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f90e6-138">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f90e6-139">JSON</span><span class="sxs-lookup"><span data-stu-id="f90e6-139">JSON</span></span>](#tab/json)

<span data-ttu-id="f90e6-140">これは、ボットに送信 `invoke` される例です。</span><span class="sxs-lookup"><span data-stu-id="f90e6-140">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="f90e6-141">応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="f90e6-141">An example of the response is shown below.</span></span>

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
