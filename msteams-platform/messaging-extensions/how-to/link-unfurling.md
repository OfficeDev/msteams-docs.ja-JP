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
# <a name="link-unfurling"></a>リンク展開

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> 現時点では、モバイル クライアントではリンクの分岐はサポートされていません。

リンク展開を使用すると、特定のドメインの URL がメッセージの作成領域に貼り付けられたときに、アプリが `invoke` アクティビティを受信するように登録することができます。 作成 `invoke` メッセージ領域に貼り付けされた完全な URL が含まれるので、ユーザーがリンクを解除して追加の情報やアクションを提供できるカードで応答できます。 これは検索コマンドと非常に [似て機能し](~/messaging-extensions/how-to/search-commands/define-search-command.md)、URL は検索用語として機能します。

Azure DevOps メッセージング拡張機能は、リンクの分岐を使用して、作業項目を指すメッセージ作成領域に貼り付けされた URL を検索します。 次のスクリーンショットでは、ユーザーが Azure DevOps の作業項目の URL に貼り付け、メッセージング拡張機能がカードに解決されています。

![リンクの分岐の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>アプリ マニフェストにリンクの分岐を追加する

 リンク展開をアプリ マニフェストに追加するには、アプリ マニフェスト JSON のセクションに新しい `messageHandlers` `composeExtensions` 配列を追加します。 配列は、App Studio のヘルプを使用して追加するか、手動で追加できます。 たとえば、ドメイン一覧にはワイルドカードを含めできます `*.example.com` 。 これは、ドメインの 1 つのセグメントと正確に一致します。if you need to match `a.b.example.com` then use `*.*.example.com` .

> [!NOTE]
> 直接またはワイルドカードを使用して、制御の外部にあるドメインを追加しません。 たとえば、yourapp.onmicrosoft.comは有効ですが、*.onmicrosoft.comは無効です。 また、トップ レベル ドメインは禁止されています。 たとえば、*.com、*.org などです。

### <a name="using-app-studio"></a>App Studio を使用する場合

1. App Studio の [マニフェスト エディター] タブで、アプリ マニフェストを読み込む。
1. [ **メッセージングの拡張機能] ページ** で、次のスクリーンショットに示すように、[ **メッセージ** ハンドラー] セクションで探すドメインを追加します。

![App Studio のメッセージ ハンドラー セクション](~/assets/images/link-unfurling.png)

### <a name="manually"></a>手動

この方法でメッセージング拡張機能がリンクとやり取りするには、まず、次の例に示すアプリ マニフェストに配列を `messageHandlers` 追加する必要があります。 この例は完全なマニフェストではありません [。マニフェストの](~/resources/schema/manifest-schema.md) 完全な例については、マニフェスト リファレンスを参照してください。

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

## <a name="handle-the-composeextensionquerylink-invoke"></a>呼び出しの `composeExtension/queryLink` 処理

アプリ マニフェストをリッスンするドメインを追加したら、呼び出し要求を処理するために Web サービス コードを更新する必要があります。 受け取った URL を使用してサービスを検索し、カードの応答を作成します。 複数のカードで応答する場合は、最初のカードだけが使用されます。

次のカードの種類がサポートされています。

* [サムネイル カード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [ヒーロー カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

概要 [については、「カードについて](~/task-modules-and-cards/what-are-cards.md) 」を参照してください。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

これは、ボットに送信 `invoke` される例です。

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

応答の例を次に示します。

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
