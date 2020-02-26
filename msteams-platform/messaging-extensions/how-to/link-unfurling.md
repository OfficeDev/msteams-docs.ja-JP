---
title: Link unfurling
author: clearab
description: Microsoft Teams アプリでメッセージング拡張機能を使用してリンク unfurling を実行する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: ccc23f06fbe759dc4c38dfc63dfa356d38352c27
ms.sourcegitcommit: 67c021fa20eb5ea70c059fcc35be1c19c6c97c95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "42279775"
---
# <a name="link-unfurling"></a>Link unfurling

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Link unfurling を使用すると、アプリは、 `invoke`特定のドメインの url が [メッセージの作成] 領域に貼り付けられたときに、アクティビティを受信するように登録できます。 に`invoke`は、[メッセージの作成] 領域に貼り付けられた完全な url が格納されています。また、ユーザーが使用を中止して、追加の情報や*アクションを提供*することができます。 これは[検索コマンド](~/messaging-extensions/how-to/search-commands/define-search-command.md)とよく似ており、URL が検索用語として機能します。

Azure DevOps messaging extension は、リンク unfurling を使用して、作業項目を指す作成メッセージ領域に貼り付けられた Url を検索します。 次のスクリーンショットでは、ユーザーが Azure DevOps の作業項目の URL を貼り付けて、メッセージング拡張機能がカードに解決されたことを示しています。

![Link unfurling の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>アプリマニフェストにリンク unfurling を追加する

これを行うには、アプリマニフェスト`messageHandlers` JSON の`composeExtensions`セクションに新しい配列を追加します。 そのためには、アプリ Studio のヘルプを使用するか、手動で行うことができます。 ドメインリストには、たとえば`*.example.com`、ワイルドカードを含めることができます。 これは、1つのドメインのセグメントに一致します。に一致`a.b.example.com`させる必要がある`*.*.example.com`場合は、を使用します。

### <a name="using-app-studio"></a>App Studio を使用する場合

1. App Studio の [マニフェストエディター] タブで、アプリマニフェストを読み込みます。
1. [**メッセージング内線番号**] ページで、以下のスクリーンショットのように、[**メッセージハンドラ**] セクションで検索するドメインを追加します。

![App Studio の [メッセージハンドラ] セクション](~/assets/images/link-unfurling.png)

### <a name="manually"></a>手動

この方法でメッセージング拡張機能がリンクを操作できるようにするには、次`messageHandlers`の例に示すように、最初に、配列をアプリのマニフェストに追加する必要があります。 この例は完全なマニフェストではありません。マニフェストの完全な例については、「[マニフェストリファレンス](~/resources/schema/manifest-schema.md)」を参照してください。

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

## <a name="handle-the-composeextensionquerylink-invoke"></a>呼び出しを`composeExtension/queryLink`処理する

アプリマニフェストをリッスンするためにドメインを追加したら、呼び出し要求を処理するように web サービスコードを更新する必要があります。 受信した URL を使用してサービスを検索し、カード応答を作成します。 複数のカードで応答する場合は、最初のカードのみが使用されます。

次のカードの種類をサポートしています。

* [サムネイルカード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [英雄カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタカード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブカード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

概要については、「[カードとは](~/task-modules-and-cards/what-are-cards.md)」を参照してください。

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

# <a name="javascriptnodejs"></a>[JavaScript/node.js](#tab/javascript)

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

これは、 `invoke`ボットに送信される例です。

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
