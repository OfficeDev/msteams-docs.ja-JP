---
title: カードの種類
description: このモジュールでは、Teams のボットで使用できるカードとカードアクションについて説明し、ヒーロー、サムネイル、アダプティブ カードを作成します。
ms.localizationpriority: high
ms.topic: reference
ms.openlocfilehash: 20654804580c4e52f9355f32cd742458cccfc88c
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586792"
---
# <a name="types-of-cards"></a>カードの種類

アダプティブ、ヒーロー、リスト、Office 365 コネクタ、レシート、サインイン、サムネイル カード、およびカード コレクションは、Microsoft Teams のボットでサポートされています。 これらはBot Framework で定義されたカードに基づいていますが、すべての Bot Framework カードが Teams でサポートされているわけではなく、独自のカードがいくつか追加されています。

さまざまなカードの種類を特定する前に、ヒーロー カード、サムネイル カード、アダプティブ カードを作成する方法を理解してください。

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a>ヒーロー カード、サムネイル カード、アダプティブ カードを作成する

Teams の開発者ポータルからヒーロー カード、サムネイル カード、アダプティブ カードを作成するには:

1. [Teams の開発者ポータル](https://dev.teams.microsoft.com/home)に移動します。
1. **[アダプティブ カードの設計と構築]** を選択します。
1. **[新しいカード]** を選択します。
1. カード名を入力し、**[保存]** を選択します。
1. **[ヒーロー カード]**、**[サムネイルカード]**、または **[アダプティブ カード]** のいずれかのカードを選択します。

   :::image type="content" source="../../assets/images/Cards/Herocarddetailsteams.PNG" alt-text="ヒーロー カード":::

1. **[保存]** を選択します。
1. **[この カードを送信する]** を選択します。 カードがチャット メッセージとして送信されます。

## <a name="card-examples"></a>カードの例

カードの使用方法の詳細については、Bot Builder SDK v3 のドキュメントで確認できます。 GitHub の **Microsoft/BotBuilder のサンプル** リポジトリでは、利用できるコード サンプルを参照することができます。 カードの例を次に示します:

* .NET
  * [メッセージに添付ファイルとしてカードを追加します](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)。
  * [カード サンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)。

* Node.js
  * [メッセージに添付ファイルとしてカードを追加します](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)。
  * [カード サンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)。

## <a name="card-types"></a>カードの種類

アプリケーション要件に基づいて、さまざまな種類のカードを識別して使用できます。 使用できるカードの種類を次の表に示します:

| カードの種類 | 説明 |
| --- | --- |
| [アダプティブ カード](#adaptive-card) | このカードは高度にカスタマイズできます。テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせが可能です。 |
| [ヒーロー カード](#hero-card) | このカードには、通常、1 つの大きな画像、1 つまたは複数のボタン、少量のテキストが含まれます。 |
| [リスト カード](#list-card) | このカードには、アイテムのスクロール リストが含まれています。 |
| [Office 365 コネクタ カード](#office-365-connector-card) | 複数のセクション、フィールド、画像、アクションを含む柔軟なレイアウトです。 |
| [レシート カード](#receipt-card) | このカードは、ユーザーに領収書を提供します。 |
| [サインイン カード](#signin-card) | このカードを使用すると、ボットはユーザーのサインインを要求できます。 |
| [サムネイル カード](#thumbnail-card) | このカードには通常、1 つのサムネイル画像、短いテキスト、1 つ以上のボタンが含まれています。 |
| [カード コレクション](#card-collections) | このカード コレクションは、1 つの応答で複数のアイテムを返す場合に使用します。 |

## <a name="features-that-support-different-card-types"></a>さまざまな種類のカードをサポートする機能

| カードの種類 | ボット | メッセージ拡張機能のプレビュー | メッセージ拡張機能の結果 | タスク モジュール | Webhookの送信 | 受信 Webhook | Office 365 コネクタ |
| --- | --- | --- | --- | --- | --- | --- | --- |
| アダプティブ カード | ✔️ | ❌ | ✔️ | ✔️ | ✔️ | ✔️ | ❌ |
| Office 365 コネクタ カード | ✔️ | ❌ | ✔️ | ❌ | ✔️ | ✔️ | ✔️ |
| ヒーロー カード | ✔️ | ✔️ | ✔️ | ❌ | ✔️ | ✔️ | ❌ |
| サムネイル カード | ✔️ | ✔️ | ✔️ | ❌ | ✔️ | ✔️ | ❌ |
| リスト カード | ✔️ | ❌ | ❌ | ❌ | ✔️ | ✔️ | ❌ |
| レシート カード | ✔️ | ❌ | ❌ | ❌ | ❌ | ✔️ | ❌ |
| サインイン カード | ✔️ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |

> [!NOTE]
>
> * 受信 Webhooks のアダプティブ カードでは、ネイティブのアダプティブ カード スキーマ要素 (ただし、`Action.Submit` を除く) がすべて完全にサポートされます。 サポートされているアクションは [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、[**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)、および [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)です。
>
> * アダプティブ カードでは、受信 Webhook O365 コネクタの種類のみがサポートされ、他の O365 コネクタの種類はサポートされません。

## <a name="common-properties-for-all-cards"></a>すべてのカードの共通プロパティ

すべてのカードに適用できる一般的なプロパティを確認できます。

> [!NOTE]
> 複数のアクションを持つヒーロー カードとサムネイル カードは、カルーセル レイアウト内の複数のカードに自動的に分割されます。

### <a name="inline-card-images"></a>インライン カードの画像

カードには、公開されているイメージへのリンクを含めることで、インライン画像を含めることができます。 パフォーマンス上の理由から、パブリック Content Delivery Network (CDN) でイメージをホストすることを強くお勧めします。

画像領域をカバーするために、縦横比を保持するように画像のサイズが拡大または縮小されます。画像は、カードの縦横比が適切になるように中央からトリミングされます。

画像は最大 1024 x 1024 で、PNG、JPEG、または GIF 形式である必要があります。 アニメーション GIF はサポートされていません。

次の表に、インライン カード画像のプロパティを示します。

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| url | URL | 画像の HTTPS URL。 |
| alt | 文字列 | 画像のアクセシビリティ対応の説明。 |

> [!NOTE]
> 最終的な画像の前にリダイレクトされるイメージ URL がカードに含まれる場合、イメージ URL のリダイレクトはサポートされません。これは、パブリック クラウドで共有される画像で生じます。

### <a name="buttons"></a>ボタン

ボタンはカードの下部に上下に並んで表示されます。 ボタンのテキストは常に 1 行で表示され、テキストがボタンの幅を超えた場合は切り捨てられます。 カードでサポートされている最大数を超えるボタンは表示されません。

詳細については、「[カード アクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。

### <a name="card-formatting"></a>カードの書式設定

カードのテキストの書式設定の詳細については、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。

すべてのカードの共通プロパティを特定した後、アダプティブ カードを操作し、アクション可能なコンテンツを使用するアプリに直接追加することで、エンゲージメントと効率を向上させることができます。

## <a name="adaptive-card"></a>アダプティブ カード

アダプティブ カードはカスタマイズ可能なカードであり、テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含めることができます。詳細については、「[アダプティブ カード](https://github.com/microsoft/AdaptiveCards/releases/tag/2020.07)」を参照してください。

### <a name="support-for-adaptive-cards"></a>アダプティブ カードのサポート

次の表に、アダプティブ カードをサポートする機能を示します:

| Teams の Bot | メッセージ拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔️ | ✔️ | ❌ | ✔️ |

> [!NOTE]
>
> * Teams プラットフォームでは、ボット送信カードとアクション ベースのメッセージ拡張機能に対して、v1.4 以前のアダプティブ カード機能がサポートされています。
> * Teams プラットフォームでは、ユーザーから送信されたカード (検索ベースのメッセージ拡張機能とリンク解除)、タブ、タスク モジュールなど、他の機能に対して v1.3 以前のアダプティブ カード機能がサポートされています。
> * 肯定的または破壊的なアクションのスタイル設定は、Teams プラットフォームのアダプティブ カードではサポートされていません。
> * メディア要素は、現在、Teams プラットフォームのアダプティブ カードではサポートされていません。
> * モバイル パネルや会議サイド パネルなどの狭いフォーム 要素で全幅アダプティブ カードをテストし、コンテンツが切り捨てられていないことを確認します。

### <a name="example-of-adaptive-card"></a>アダプティブ カードの例

:::image type="content" source="~/assets/images/cards/adaptivecard.png" alt-text="アダプティブ カードの例":::

次のコードは、アダプティブ カードの例を示しています。

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

#### <a name="additional-information-on-adaptive-cards"></a>アダプティブ カードの追加情報

アダプティブ カードでは、ドル記号 ($) と中かっこを使用して動的な値を渡すことができます。詳細については、「[アダプティブ カード のテンプレート作成](/adaptive-cards/templating/)」を参照してください。

例:

```json
{ 
 "type": "TextBlock",
 "text": "${titleText}",
 "size": "default",
 "weight": "bolder"
}

```

以下の Bot Framework リファレンスを参照してください。

* [アダプティブ カード ノード](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [アダプティブ カード C#](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

アダプティブ カードの詳細については、「[アダプティブ カード](/adaptive-cards/)」を参照してください。

これで、潜在的なユーザー選択を視覚的に強調表示するために使用する多目的カードであるヒーロー カードを使用できます。

## <a name="hero-card"></a>ヒーロー カード

通常、1 つの大きな画像、1 つまたは複数のボタン、テキストを含むカードです。

### <a name="support-for-hero-cards"></a>ヒーロー カードでのサポート

次の表に、ヒーロー カードをサポートする機能を示します。

| Teams の Bot | メッセージ拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔️ | ✔️ | ❌ | ✔️ |

### <a name="properties-of-a-hero-card"></a>ヒーロー カードのプロパティ

次の表に、ヒーロー カードのプロパティを示します。

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。 |
| サブタイトル | リッチ テキスト | カードのサブタイトル。 最大 2 行。|
| テキスト | リッチ テキスト | 字幕の下にテキストが表示されます。 書式設定オプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。 |
| images | 画像の配列 | カードの上部に表示される画像。 縦横比は 16:9 です。 |
| buttons | Action オブジェクトの配列 | 現在のカードに適用できるアクション一式。最大で 6 個です。 |
| tap | Action オブジェクト | ユーザーがカード自体をタップするとアクティブ化されます。 |

### <a name="example-of-a-hero-card"></a>ヒーロー カードの例

:::image type="content" source="../../assets/images/Cards/hero.png" alt-text="ヒーロー カード":::

次のコードはヒーロー カードの一例を示します:

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

### <a name="additional-information-on-hero-cards"></a>ヒーロー カードに関する追加情報

以下の Bot Framework リファレンスを参照してください。

* [ヒーロー カード Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [ヒーロー カード C#](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a>リスト カード

リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。 リスト カードは、アイテムのスクロール リストを提供します。

### <a name="support-for-list-cards"></a>リスト カードでのサポート

次の表に、リスト カードをサポートする機能を示します:

| Teams の Bot | メッセージ拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔️ | ❌ | ❌ |✔️ |

### <a name="properties-of-a-list-card"></a>リスト カードのプロパティ

次の表に、リスト カードのプロパティを示します:

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。|
| アイテム | リスト アイテムの配列 | カードに適用可能なアイテムのセット。|
| buttons | Action オブジェクトの配列 | 現在のカードに適用できるアクション一式。最大で 6 個です。 |

### <a name="example-of-a-list-card"></a>リスト カードの例

以下のコードはその例を示しています:

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

## <a name="office-365-connector-card"></a>Office 365 コネクタ カード

柔軟なレイアウトを提供し、役に立つ情報を得るための優れた方法である Office 365 コネクタ カードを使用できます。 Office 365 コネクタ カードは、Bot Framework ではなく、Teams でサポートされています。 このカードには、複数のセクション、フィールド、画像、アクションに対応した柔軟なレイアウトが適用されています。 このカードには、ボットで使用できるようにコネクタ カードが含まれています。 コネクタ カードと Office 365 コネクタ カードの違いについては、「[Office 365 コネクタ カードの追加情報](#additional-information-on-the-office-365-connector-card)」を参照してください。

### <a name="support-for-office-365-connector-cards"></a>Office 365 コネクタ カードでのサポート

次の表に、Office 365 コネクタ カードをサポートする機能を示します。

| Teams の Bot | メッセージ拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔️ | ✔️ | ✔️ | ❌ |

### <a name="properties-of-the-office-365-connector-card"></a>Office 365 コネクタ カードのプロパティ

次の表に、Office 365 コネクタ カードのプロパティを示します。

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。 |
| 概要 | リッチ テキスト | カードの概要。 最大 2 行。 |
| テキスト | リッチ テキスト | 字幕の下にテキストが表示されます。 書式設定オプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。 |
| themeColor | 16 進数文字列 | アプリケーション マニフェストで提供される `accentColor` よりも優先される色です。 |

### <a name="additional-information-on-the-office-365-connector-card"></a>Office 365 コネクタ カードの追加情報

Office 365 コネクタ カードは、[`ActionCard` アクション](/outlook/actionable-messages/card-reference#actioncard-action)など、Microsoft Teams で正しく機能します。

コネクタからコネクタ カードを使用するのと、ボットでコネクタ カードを使用する際の重要な違いは、カード アクションの処理です。以下の表では、その違いが一覧表示されています。

| Connector | Bot |
| --- | --- |
| エンドポイントは、HTTP POST を介してカード ペイロードを受け取ります。 | ボットの場合、`HttpPOST` アクションが、アクション ID と本文のみをボットに送信する `invoke` アクティビティをトリガーします。|

各コネクタ カードは最大 10 個のセクションを表示することができ、各セクションに最大 5 つの画像と 5 つのアクションを含めることができます。

> [!NOTE]
> メッセージ内の他のセクション、画像、アクションは表示されません。

すべてのテキスト フィールドは Markdown と HTML をサポートしています。 メッセージの `markdown` プロパティを設定して、Markdown または HTML を使用するセクションを制御することができます。 既定では `markdown` が `true` に設定されています。 HTML を代わりに使用する場合は、`markdown` を `false` に設定します。

`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。

`activityImage` のレンダリング スタイルを指定するには、次の表に示すように `activityImageType` を設定することができます。

| 値 | 説明 |
| --- | --- |
| `avatar` | 既定値は `activityImage` で円形にトリミングされます。 |
| `article` | `activityImage` は四角形として表示され、縦横比が維持されます。 |

コネクタ カードのプロパティのその他の詳細については、「[操作可能なメッセージ カードのリファレンス](/outlook/actionable-messages/card-reference)」を参照してください。 Microsoft Teams が現在サポートしていないコネクタ カードのプロパティは、以下のみとなります:

* `heroImage`
* `hideOriginalBody`
* Teams では `startGroup` は常に `true` として扱われます
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>Office 365 コネクタ カードの例

次のコードは、Office 365 コネクタ カードの例を示しています。

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

## <a name="receipt-card"></a>レシート カード

Teams ではレシート カードがサポートされています。これにより、ボットはユーザーに領収書を提供できます。 通常、税金や合計情報など、領収書に含めるアイテムの一覧が含まれます。

### <a name="support-for-receipt-cards"></a>レシート カードでのサポート

次の表に、レシート カードをサポートする機能を示します:

| Teams の Bot | メッセージ拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔️ | ✔️ | ❌ | ✔️ |

### <a name="example-of-a-receipt-card"></a>レシート カードの例

:::image type="content" source="../../assets/images/Cards/receipt.png" alt-text="レシート カード":::

次のコードはレシート カードの一例を示します:

```json
{
  "contentType": "application/vnd.microsoft.card.receipt",
  "content": {
    "title": "John Doe",
    "facts": [
      {
        "key": "Order Number",
        "value": "1234"
      },
      {
        "key": "Payment Method",
        "value": "VISA 5555-****"
      }
    ],
    "items": [
      {
        "title": "Data Transfer",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/traffic-manager.png"
        },
        "price": "$ 38.45",
        "quantity": "368"
      },
      {
        "title": "App Service",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/cloud-service.png"
        },
        "price": "$ 45.00",
        "quantity": "720"
      }
    ],
    "total": "$ 90.95",
    "tax": "$ 7.50",
    "buttons": [
      {
        "type": "openUrl",
        "title": "More information",
        "image": "https://account.windowsazure.com/content/6.10.1.38-.8225.160809-1618/aux-pre/images/offer-icon-freetrial.png",
        "value": "https://azure.microsoft.com/en-us/pricing/"
      }
    ]
  }
}
```

### <a name="additional-information-on-receipt-cards"></a>レシート カードに関する追加情報

以下の Bot Framework リファレンスを参照してください。

* [レシート カード Node.js](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [レシート カード C#](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>サインイン カード

Teams のサインイン カードは Bot Framework のサインイン カードと似ていますが、Teams のサインイン カードでサポートされているアクションは `signin` と `openUrl` の 2 つのみです。

ログイン アクションは、ログイン カードだけでなく、Teams 内の任意のカードから使用できます。 詳細については、「[ボットでの認証フロー](~/bots/how-to/authentication/auth-flow-bot.md)」を参照してください。

### <a name="support-for-log-in-cards"></a>ログイン カードのサポート

次の表に、サインイン カードをサポートする機能を示します。

| Teams の Bot | メッセージ拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔️ | ❌ | ❌ | ✔️ |

### <a name="additional-information-on-signin-cards"></a>サインイン カードに関する追加情報

以下の Bot Framework リファレンスを参照してください。

* [ログイン カード Node.js](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [サインイン カード C#](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>サムネイル カード

簡単な操作可能なメッセージの送信に使用されるサムネイル カードを操作できます。 通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。

### <a name="support-for-thumbnail-cards"></a>サムネイル カードでのサポート

次の表に、サムネイル カードをサポートする機能を示します:

| Teams の Bot | メッセージ拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔️ | ✔️ | ❌ | ✔️ |

:::image type="content" source="../../assets/images/Cards/thumbnail.png" alt-text="サムネイル カード":::

### <a name="properties-of-a-thumbnail-card"></a>サムネイル カードのプロパティ

次の表に、サムネイル カードのプロパティを示します:

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。|
| サブタイトル | リッチ テキスト | カードのサブタイトル。 最大 2 行。|
| テキスト | リッチ テキスト | 字幕の下にテキストが表示されます。 書式設定オプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。 |
| images | 画像の配列 | カードの上部に表示される画像。 縦横比は 1:1 の正方形です。 |
| buttons | Action オブジェクトの配列 | 現在のカードに適用できるアクション一式。最大で 6 個です。 |
| tap | Action オブジェクト | ユーザーがカード自体をタップするとアクティブ化されます。 |

### <a name="example-of-a-thumbnail-card"></a>サムネイル カードの例

次のコードはサムネイル カードの一例を示します:

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

### <a name="additional-information"></a>ページの先頭へ

以下の Bot Framework リファレンスを参照してください。

* [サムネイル カード Node.js](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [サムネイル カード C#](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>カード コレクション

カルーセル コレクションとリスト コレクションを含むカード コレクションを使用できます。 Teams ではカード コレクションがサポートされています。 カード コレクションには、 `builder.AttachmentLayout.carousel` と `builder.AttachmentLayout.list` が含まれます。 これらのコレクションには、アダプティブ カード、ヒーロー カード、またはサムネイル カードを含めることができます。

### <a name="carousel-collection"></a>カルーセル コレクション

[カルーセルのレイアウト](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。

#### <a name="support-for-carousel-collections"></a>カルーセル コレクションでのサポート

次の表に、カルーセル コレクションをサポートする機能を示します:

| Teams の Bot | メッセージ拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔️ | ❌ | ❌ | ✔️ |

> [!NOTE]
> カルーセルでは、メッセージごとに最大 10 枚のカードを表示することができます。

#### <a name="properties-of-a-carousel-card"></a>カルーセル カードのプロパティ

カルーセル カードのプロパティは、ヒーロー カードとサムネイル カードのプロパティと同じです。

#### <a name="example-of-a-carousel-collection"></a>カルーセル コレクションの例

:::image type="content" source="../../assets/images/Cards/carousel.png" alt-text="カルーセル コレクション":::

次のコードは、カルーセル コレクションの例を示しています:

```json
{
 "attachmentLayout": "carousel",
 "attachments":[
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "extraLarge",
                "weight": "bolder",
                "text": "Welcome to Employee Connect",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "size": "medium",
                "weight": "bolder",
                "text": "Add events to your calendar",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "The bot can send \r\rnotification to remind \r\ryou about the latest \r\revents and trainings.",
                "wrap": true,
                "height": "stretch"
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee connect"
              },
              {
                "type": "TextBlock",
                "text": "The bot can send notifications \r\rto remind you about the latest \r\r events and trainings",
                "wrap": true,
                "maxWidth": 2
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee Connect final"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Create and manage your tasks",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "text": "The app identifies all your pending tasks \r\r and helps you manage everything at \r\r one place.",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Try these commands \r\r- Pending Submissions \r\r- Pending Approvals- My Tools",
                "wrap": true,
                "height": "stretch"
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    }
  ]
}
```

#### <a name="syntax-for-carousel-collections"></a>カルーセル コレクションの構文

`builder.AttachmentLayoutTypes.Carousel` は、カルーセル コレクションの構文です。

### <a name="list-collection"></a>リスト コレクション

リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。

#### <a name="support-for-list-collections"></a>リスト コレクションでのサポート

次の表に、リスト コレクションをサポートする機能を示します:

| Teams の Bot | メッセージ拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔️ | ✔️ | ❌ | ✔️ |

#### <a name="example-of-a-list-collection"></a>リスト コレクションの例

:::image type="content" source="../../assets/images/Cards/list.png" alt-text="リスト コレクション":::

リスト コレクションのプロパティは、ヒーロー カードまたはサムネイル カードのプロパティと同じです。

リストには、メッセージごとに最大 10 枚のカードを表示することができます。

> [!NOTE]
> iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。

#### <a name="syntax-for-list-collections"></a>リスト コレクションの構文

`builder.AttachmentLayout.list` はリスト コレクションの構文です。

## <a name="cards-not-supported-in-teams"></a>Teams でサポートされていないカード

次のカードは Bot Framework によって実装されていますが、Teams ではサポートされていません。

* アニメーション カード
* オーディオ カード
* ビデオ カード

## <a name="see-also"></a>関連項目

* [タスク モジュール](~/task-modules-and-cards/what-are-task-modules.md)
* [カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)
* [最新のカード](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
* [アダプティブ カードのユニバーサル アクションの操作](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/work-with-universal-actions-for-adaptive-cards.md)
* [フォームの完了に関するフィードバック](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
