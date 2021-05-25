---
title: リンク展開
author: clearab
description: アプリでメッセージング拡張機能を使用してリンクを開Microsoft Teams方法。
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 405b320b887300837d51332a9548ff60aff450d0
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630685"
---
# <a name="link-unfurling"></a><span data-ttu-id="b2965-103">リンク展開</span><span class="sxs-lookup"><span data-stu-id="b2965-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="b2965-104">このドキュメントでは、App studio を使用して手動でアプリ マニフェストにリンク解除を追加する方法についてガイドします。</span><span class="sxs-lookup"><span data-stu-id="b2965-104">This document guides you on how to add link unfurling to your app manifest using App studio and manually.</span></span> <span data-ttu-id="b2965-105">リンク展開を使用すると、特定のドメインの URL がメッセージの作成領域に貼り付けられたときに、アプリが `invoke` アクティビティを受信するように登録することができます。</span><span class="sxs-lookup"><span data-stu-id="b2965-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="b2965-106">作成メッセージ領域に貼り付けされた完全な URL が含まれているので、ユーザーがリンクを解除できるカードで応答し、追加情報やアクション `invoke` を提供できます。</span><span class="sxs-lookup"><span data-stu-id="b2965-106">The `invoke` contains the full URL that was pasted into the compose message area, and you can respond with a card that the user can unfurl, providing additional information or actions.</span></span> <span data-ttu-id="b2965-107">これは、URL が検索用語として機能する検索コマンドと似ています。</span><span class="sxs-lookup"><span data-stu-id="b2965-107">This works similar to a search command with the URL serving as the search term.</span></span>

> [!NOTE]
> <span data-ttu-id="b2965-108">現時点では、モバイル クライアントではリンクのリンク解除はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b2965-108">Currently, link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="b2965-109">メッセージAzure DevOps拡張機能では、リンク解除を使用して、作業項目を指すメッセージ作成領域に貼り付け先の URL を探します。</span><span class="sxs-lookup"><span data-stu-id="b2965-109">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="b2965-110">次の図では、ユーザーが Azure DevOps で作業アイテムの URL を貼り付け、メッセージング拡張機能がカードに解決されています。</span><span class="sxs-lookup"><span data-stu-id="b2965-110">In the following image, a user has pasted a URL for a work item in Azure DevOps, which the messaging extension has resolved into a card:</span></span>

![リンクの分岐解除の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="b2965-112">アプリ マニフェストへのリンクのリンク解除の追加</span><span class="sxs-lookup"><span data-stu-id="b2965-112">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="b2965-113">リンク展開をアプリ マニフェストに追加するには、アプリ マニフェスト JSON のセクションに新しい `messageHandlers` `composeExtensions` 配列を追加します。</span><span class="sxs-lookup"><span data-stu-id="b2965-113">To add link unfurling to your app manifest, add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="b2965-114">配列は、App Studio の助けを借りて、または手動で追加できます。</span><span class="sxs-lookup"><span data-stu-id="b2965-114">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="b2965-115">ドメインの一覧には、ワイルドカードを含め、たとえば、 を含めできます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="b2965-115">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="b2965-116">これは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 `a.b.example.com` を使用します `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="b2965-116">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="b2965-117">Donot は、直接またはワイルドカードを使用して、コントロールに含まれているドメインを追加します。</span><span class="sxs-lookup"><span data-stu-id="b2965-117">Donot add domains that are not in your control, either directly or through wildcards.</span></span> <span data-ttu-id="b2965-118">たとえば、有効 `yourapp.onmicrosoft.com` ですが、 `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="b2965-118">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span> <span data-ttu-id="b2965-119">また、トップ レベルのドメインは禁止されています。</span><span class="sxs-lookup"><span data-stu-id="b2965-119">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="b2965-120">たとえば `*.com` 、. `*.org`</span><span class="sxs-lookup"><span data-stu-id="b2965-120">For example, `*.com`, `*.org`.</span></span>

### <a name="add-link-unfurling-using-app-studio"></a><span data-ttu-id="b2965-121">App Studio を使用してリンクの分岐を解除する</span><span class="sxs-lookup"><span data-stu-id="b2965-121">Add link unfurling using App Studio</span></span>

1. <span data-ttu-id="b2965-122">クライアント **から App Studio** をMicrosoft Teamsし、[マニフェスト エディター]**タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="b2965-122">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1. <span data-ttu-id="b2965-123">アプリ マニフェストを読み込む。</span><span class="sxs-lookup"><span data-stu-id="b2965-123">Load your app manifest.</span></span>
1. <span data-ttu-id="b2965-124">[メッセージング **拡張機能] ページ** で、探すドメインを [メッセージ ハンドラー] セクション **に追加** します。</span><span class="sxs-lookup"><span data-stu-id="b2965-124">On the **Messaging Extension** page, add the domain that you want to look for in the **Message handlers** section.</span></span> <span data-ttu-id="b2965-125">次の図は、プロセスを説明しています。</span><span class="sxs-lookup"><span data-stu-id="b2965-125">The following image explains the process:</span></span>

    ![App Studio の [メッセージ ハンドラー] セクション](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a><span data-ttu-id="b2965-127">リンクの手動でのリンク解除の追加</span><span class="sxs-lookup"><span data-stu-id="b2965-127">Add link unfurling manually</span></span>

<span data-ttu-id="b2965-128">メッセージング拡張機能でリンクを操作するには、まず配列をアプリ マニフェスト `messageHandlers` に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2965-128">To enable your messaging extension to interact with links, first you must add the `messageHandlers` array to your app manifest.</span></span> <span data-ttu-id="b2965-129">次の例では、リンクの分岐を手動で追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b2965-129">The following example explains how to add link unfurling manually:</span></span> 


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

<span data-ttu-id="b2965-130">マニフェストの完全な例については、「マニフェスト参照」 [を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="b2965-130">For a complete manifest example, see [manifest reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="b2965-131">呼び出しの `composeExtension/queryLink` 処理</span><span class="sxs-lookup"><span data-stu-id="b2965-131">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="b2965-132">アプリ マニフェストにドメインを追加した後、呼び出し要求を処理するために Web サービス コードを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2965-132">After adding the domain to the app manifest, you must update your web service code to handle the invoke request.</span></span> <span data-ttu-id="b2965-133">受信した URL を使用してサービスを検索し、カード応答を作成します。</span><span class="sxs-lookup"><span data-stu-id="b2965-133">Use the received URL to search your service and create a card response.</span></span> <span data-ttu-id="b2965-134">複数のカードで応答する場合は、最初のカード応答だけが使用されます。</span><span class="sxs-lookup"><span data-stu-id="b2965-134">If you respond with more than one card, only the first card response is used.</span></span>

<span data-ttu-id="b2965-135">次のカードの種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b2965-135">The following card types are supported:</span></span>

* [<span data-ttu-id="b2965-136">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="b2965-136">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="b2965-137">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="b2965-137">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="b2965-138">Office 365コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="b2965-138">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="b2965-139">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="b2965-139">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

### <a name="example"></a><span data-ttu-id="b2965-140">例</span><span class="sxs-lookup"><span data-stu-id="b2965-140">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b2965-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b2965-141">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="b2965-142">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="b2965-142">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="b2965-143">JSON</span><span class="sxs-lookup"><span data-stu-id="b2965-143">JSON</span></span>](#tab/json)

<span data-ttu-id="b2965-144">ボットに送信される送信の `invoke` 例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b2965-144">Following is an example of the `invoke` sent to your bot:</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="b2965-145">応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b2965-145">Following is an example of the response:</span></span>

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

## <a name="see-also"></a><span data-ttu-id="b2965-146">関連項目</span><span class="sxs-lookup"><span data-stu-id="b2965-146">See also</span></span> 

* [<span data-ttu-id="b2965-147">カード</span><span class="sxs-lookup"><span data-stu-id="b2965-147">Cards</span></span>](~/task-modules-and-cards/what-are-cards.md)
* [<span data-ttu-id="b2965-148">タブリンクの分岐解除とステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="b2965-148">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
