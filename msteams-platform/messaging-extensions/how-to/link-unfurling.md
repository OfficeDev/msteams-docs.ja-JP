---
title: リンク展開
author: surbhigupta
description: アプリ マニフェストを使用して、またはコード例とサンプルを手動で使用して、Microsoft Teams拡張機能を使用してリンクを追加する方法について説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1ecab904f21d84cfa329e1c390d51ebade6a8e05
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453867"
---
# <a name="link-unfurling"></a>リンク展開

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

このドキュメントでは、App studio を使用して手動でアプリ マニフェストにリンク解除を追加する方法についてガイドします。 リンクの分岐を解除すると、 `invoke` 特定のドメインを持つ URL を作成メッセージ領域に貼り付けるときに、アプリがアクティビティを受信するために登録できます。 作成 `invoke` メッセージ領域に貼り付けされた完全な URL が含まれているので、ユーザーがリンクを解除できるカードで応答し、追加情報やアクションを提供できます。 これは、URL が検索用語として機能する検索コマンドと似ています。

> [!NOTE]
>
> * 現時点では、モバイル クライアントではリンクのリンク解除はサポートされていません。
> * リンクの分岐解除結果は 30 分間キャッシュされます。

メッセージAzure DevOps拡張機能では、リンク解除を使用して、作業項目を指すメッセージ作成領域に貼り付け先の URL を探します。 次の図では、ユーザーが Azure DevOps のワーク アイテムの URL を貼り付け、メッセージング拡張機能がカードに解決されています。

![リンクの分岐解除の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>アプリ マニフェストへのリンクのリンク解除の追加

リンク展開をアプリ マニフェストに追加するには、アプリ `messageHandlers` `composeExtensions` マニフェスト JSON のセクションに新しい配列を追加します。 配列は、App Studio の助けを借りて、または手動で追加できます。 ドメインの一覧には、ワイルドカードを含め、たとえば、 を含めできます `*.example.com`。 これは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 を `a.b.example.com` 使用します `*.*.example.com`。

> [!NOTE]
> 直接またはワイルドカードを使用して、コントロールに含まれているドメインを追加しません。 たとえば、有効 `yourapp.onmicrosoft.com` ですが、 `*.onmicrosoft.com` 無効です。 また、トップ レベルのドメインは禁止されています。 たとえば、. `*.com``*.org`

### <a name="add-link-unfurling-using-app-studio"></a>App Studio を使用してリンクの分岐を解除する

1. クライアント **から App Studio** をMicrosoft Teamsし、[マニフェスト エディター] **タブを選択** します。
1. アプリ マニフェストを読み込む。
1. [メッセージング **拡張機能] ページ** で、探すドメインを [メッセージ ハンドラー] セクション **に追加** します。 次の図は、プロセスを説明しています。

    ![App Studio の [メッセージ ハンドラー] セクション](~/assets/images/link-unfurling.png)

### <a name="add-link-unfurling-manually"></a>リンクの手動でのリンク解除の追加

メッセージング拡張機能でリンクを操作 `messageHandlers` するには、まず配列をアプリ マニフェストに追加する必要があります。 次の例では、リンクの分岐を手動で追加する方法について説明します。

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

マニフェストの完全な例については、「マニフェスト参照 [」を参照してください](~/resources/schema/manifest-schema.md)。

## <a name="handle-the-composeextensionquerylink-invoke"></a>呼び出しの `composeExtension/queryLink` 処理

アプリ マニフェストにドメインを追加した後、呼び出し要求を処理するために Web サービス コードを更新する必要があります。 受信した URL を使用してサービスを検索し、カード応答を作成します。 複数のカードで応答する場合は、最初のカード応答だけが使用されます。

次のカードの種類がサポートされています。

* [サムネイル カード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [ヒーロー カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

詳細については、「Action type [invoke」を参照してください](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)。

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

ボットに送信される送信の例 `invoke` を次に示します。

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

## <a name="see-also"></a>関連項目

* [カード](~/task-modules-and-cards/what-are-cards.md)
* [タブリンクの分岐解除とステージ ビュー](~/tabs/tabs-link-unfurling.md)
