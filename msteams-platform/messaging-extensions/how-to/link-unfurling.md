---
title: リンク展開
author: surbhigupta
description: アプリ マニフェストを含む Microsoft Teams アプリでメッセージングの拡張機能を使用するか、コード例とサンプルを手動で使用して、リンク展開を追加する方法について説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: c5f89847e374f6e7e2e15409f4a9fe019701788d
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032974"
---
# <a name="link-unfurling"></a>リンク展開

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

このドキュメントでは、App Studio または手動でアプリ マニフェストにリンク解除を追加する方法について説明します。 リンク展開を使用すると、特定のドメインの URL がメッセージ作成領域に貼り付けられたときに、アプリが `invoke` アクティビティを受信するように登録することができます。 には `invoke` 、作成メッセージ領域に貼り付けられた完全な URL が含まれています。 ユーザーが追加情報やアクションの登録を解除できるカードを使用して応答できます。 これは、URL を検索用語として使用する検索コマンドとして機能します。

> [!NOTE]
>
> * 現在、モバイル クライアントではリンク展開はサポートされていません。
> * リンク展開の結果は、30 分間キャッシュされます。

Azure DevOps メッセージ拡張機能では、作業項目をポイントするメッセージ作成領域に貼り付けられた URL を検索するためにリンク展開を使用します。 次の図では、ユーザーがメッセージ拡張機能がカードに解決したAzure DevOpsにアイテムの URL を貼り付けています。

:::image type="content" source="~/assets/images/compose-extensions/messagingextensions_linkunfurling.png" alt-text="リンク展開の例":::

## <a name="add-link-unfurling-to-your-app-manifest"></a>アプリ マニフェストにリンク展開を追加する

アプリ マニフェストにリンク展開を追加するには、アプリ マニフェスト JSON の `composeExtensions` セクションに新しい `messageHandlers` 配列を追加します。 App Studio の助けを借りて、または手動で配列を追加できます。 ドメイン リストには、`*.example.com` などのワイルドカードを含めることができます。 これは、ドメインの 1 つのセグメントと正確に一致します。`a.b.example.com` と一致させる必要がある場合は、`*.*.example.com` を使用してください。

> [!NOTE]
> 直接、またはワイルドカードを使用して、コントロールに含まれていないドメインを追加しないでください。 たとえば、`yourapp.onmicrosoft.com` は有効ですが、`*.onmicrosoft.com` は無効です。 最上位レベルのドメインは禁止されています 。たとえば、`*.com``*.org`.

### <a name="add-link-unfurling-using-app-studio"></a>App Studio を使用してリンク展開を追加する

1. Microsoft Teams クライアントから **App Studio** を開き、**[マニフェスト エディター]** タブを選択します。
1. アプリ マニフェストを読み込みます。
1. **[メッセージ拡張機能]** ページで、検索したいドメインを **[メッセージ ハンドラー]** セクションに追加します。次の画像では、プロセスについて説明します。

    :::image type="content" source="~/assets/images/link-unfurling.png" alt-text="App Studio の [メッセージ ハンドラー] セクション":::

### <a name="add-link-unfurling-manually"></a>手動でリンク展開を追加する

> [!NOTE]
> Azure AD 経由で認証が追加された場合は、[ボットを使用してTeamsにリンクを展開解除します](/microsoftteams/platform/sbs-botbuilder-linkunfurling?tabs=vs&tutorial-step=4)。

メッセージ拡張機能でリンクを操作できるようにするには、まずアプリ マニフェストに `messageHandlers` 配列を追加する必要があります。 次の例は、リンク展開を手動で追加する方法を説明しています。

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

完全なマニフェスト例については、[マニフェスト リファレンス](~/resources/schema/manifest-schema.md)を参照してください。

## <a name="handle-the-composeextensionquerylink-invoke"></a>`composeExtension/queryLink` 呼び出しを処理する

ドメインをアプリ マニフェストに追加した後、その呼び出し要求を処理するように Web サービス コードを更新する必要があります。 受信した URL を使用してサービスを検索し、カード応答を作成します。 複数のカードで応答する場合は、最初のカード応答のみが使用されます。

次の種類のカードがサポートされています。

* [サムネイル カード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [ヒーロー カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

詳細については、「[アクション タイプ invoke](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)」を参照してください。

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

ボットに送信された `invoke` の例を次に示します。

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

この[ステップバイステップ ガイド](../../sbs-botbuilder-linkunfurling.yml)に従うと、ボットを使用して Teams でリンクを展開できます。

## <a name="see-also"></a>関連項目

* [カード](~/task-modules-and-cards/what-are-cards.md)
* [タブのリンクの展開とステージ ビュー](~/tabs/tabs-link-unfurling.md)
