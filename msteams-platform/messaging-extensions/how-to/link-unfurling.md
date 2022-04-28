---
title: リンク展開
author: surbhigupta
description: アプリ マニフェストを含むMicrosoft Teams アプリで、またはコード例とサンプルを手動で使用して、メッセージ拡張機能を使用してリンクを展開しないリンクを追加する方法について説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 2dee02545a522b202e9cc695f7099848269e8944
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104407"
---
# <a name="link-unfurling"></a>リンク展開

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

このドキュメントでは、App Studio を使用して手動でアプリ マニフェストにリンク解除を追加する方法について説明します。 リンクの展開を解除すると、アプリは、特定の `invoke` ドメインの URL が作成メッセージ領域に貼り付けられたときにアクティビティを受信するように登録できます。 メッセージ `invoke` 作成領域に貼り付けられた完全な URL が含まれており、ユーザーが展開できるカードで応答し、追加情報やアクションを提供できます。 これは、検索語句として機能する URL を持つ検索コマンドと同様に機能します。

> [!NOTE]
>
> * 現在、モバイル クライアントではリンクの展開はサポートされていません。
> * リンクの展開解除結果は、30 分間キャッシュされます。

Azure DevOps メッセージ拡張機能では、リンクの展開を使用して、作業項目を指す作成メッセージ領域に貼り付けられた URL を検索します。 次の図では、ユーザーがAzure DevOpsで作業項目の URL を貼り付けています。この URL は、メッセージ拡張機能がカードに解決されています。

![リンクの展開解除の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>アプリ マニフェストへのリンク解除の追加

アプリ マニフェストへのリンク解除を追加するには、アプリ マニフェスト JSON のセクションに`composeExtensions`新しい`messageHandlers`配列を追加します。 配列は、App Studio の助けを借りて追加することも、手動で追加することもできます。 ドメインの一覧には、たとえば `*.example.com`ワイルドカードを含めることができます。 これは、ドメインの 1 つのセグメントとまったく一致します。一致 `a.b.example.com` する必要がある場合は、 `*.*.example.com`.

> [!NOTE]
> 直接またはワイルドカードを使用して、コントロールに含まれていないドメインを追加しないでください。 たとえば、 `yourapp.onmicrosoft.com` 有効ですが `*.onmicrosoft.com` 、無効です。 また、最上位レベルのドメインは禁止されています。 たとえば、. `*.com``*.org`

### <a name="add-link-unfurling-using-app-studio"></a>App Studio を使用してリンクを展開解除する

1. Microsoft Teams クライアントから **App Studio** を開き、[**マニフェスト エディター**] タブを選択します。
1. アプリ マニフェストを読み込みます。
1. [ **メッセージ拡張機能** ] ページで、[ **メッセージ ハンドラー** ] セクションで探すドメインを追加します。 次の図では、プロセスについて説明します。

    ![App Studio の [メッセージ ハンドラー] セクション](~/assets/images/link-unfurling.png)

### <a name="add-link-unfurling-manually"></a>リンクの展開を手動で追加する

メッセージ拡張機能がリンクを操作できるようにするには、まずアプリ マニフェストに `messageHandlers` 配列を追加する必要があります。 次の例では、リンクの展開を手動で追加する方法について説明します。

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

マニフェストの完全な例については、 [マニフェストリファレンスを参照してください](~/resources/schema/manifest-schema.md)。

## <a name="handle-the-composeextensionquerylink-invoke"></a>呼び出しを処理する`composeExtension/queryLink`

ドメインをアプリ マニフェストに追加した後、呼び出し要求を処理するように Web サービス コードを更新する必要があります。 受信した URL を使用してサービスを検索し、カード応答を作成します。 複数のカードで応答する場合は、最初のカード応答のみが使用されます。

次の種類のカードがサポートされています。

* [サムネイル カード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [ヒーロー カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

詳細については、「 [アクションの種類の呼び出し」を](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)参照してください。

### <a name="example"></a>例

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

ボットに送信された例を `invoke` 次に示します。

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

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

ステップ [バイ ステップ ガイドに](../../sbs-botbuilder-linkunfurling.yml)従って、ボットを使用してTeamsでリンクを展開解除します。

## <a name="see-also"></a>関連項目

* [カード](~/task-modules-and-cards/what-are-cards.md)
* [タブのリンクの展開とステージ ビュー](~/tabs/tabs-link-unfurling.md)