---
title: カード リファレンス
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
localization_priority: Normal
keywords: Bot のカード リファレンス
ms.topic: reference
ms.openlocfilehash: 1e8cf2e474b8a74f6cab1cd6ef3439924b91892d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019532"
---
# <a name="cards-reference"></a>カード リファレンス

このドキュメントに記載されているカードは、ボットでサポートされているMicrosoft Teams。 これらは Bot Framework によって定義されたカードに基づいておりますが、Teams はボット フレームワーク カードの一部をサポートしているのではなく、一部の Teamsカードが追加されています。 相違点は、このドキュメントの参照で呼び出されます。

## <a name="card-examples"></a>カードの例

カードの使用方法に関する追加情報については、Bot Builder SDK v3 のドキュメントを参照してください。 コード サンプルは、Microsoft/BotBuilder-Samples リポジトリ (microsoft/BotBuilder-Samples リポジトリ) GitHub。

* .NET
  * [メッセージに添付ファイルとしてカードを追加する](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [カードのサンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)

* Node.js
  * [メッセージに添付ファイルとしてカードを追加する](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [カードのサンプル コード Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)

## <a name="types-of-cards"></a>カードの種類

次の表に、使用可能なカードの種類を示します。

| カードの種類 | 説明 |
| --- | --- |
| [アダプティブ カード](#adaptive-card) | このカードは、テキスト、音声、画像、ボタン、および入力フィールドの任意の組み合わせを含む高度にカスタマイズ可能なカードです。 |
| [ヒーロー カード](#hero-card) | このカードには、通常、1 つの大きな画像、1 つ以上のボタン、および少量のテキストが含まれる。 |
| [リスト カード](#list-card) | このカードはアイテムのスクロール リストです。 |
| [Office 365 コネクタ カード](#office-365-connector-card) | このカードには、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトがあります。 |
| [レシート カード](#receipt-card) | このカードは、ユーザーにレシートを提供します。 |
| [サインイン カード](#signin-card) | このカードを使用すると、ボットはユーザーのサインインを要求できます。 |
| [サムネイル カード](#thumbnail-card) | このカードには、通常、1 つのサムネイル 画像、短いテキスト、および 1 つ以上のボタンが含まれる。 |
| [カード コレクション](#card-collections) | このカードは、1 つの応答で複数のアイテムを返す場合に使用します。 |

## <a name="common-properties-for-all-cards"></a>すべてのカードの共通プロパティ

### <a name="inline-card-images"></a>インライン カードの画像

カードには、公開されている画像へのリンクを含め、インライン イメージを含めできます。 パフォーマンス上の目的で、パブリック コンテンツ配信ネットワーク (CDN) でイメージをホストすることを強くお勧CDN。

画像のサイズは拡大または縮小され、縦横比を維持して画像領域をカバーします。 次に、カードの適切な縦横比を実現するために、中央から画像がトリミングされます。

画像は、PNG、JPEG、または GIF 形式×最大 1024、×1024 である必要があります。アニメーション GIF はサポートされていません。

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| url | URL | イメージの HTTPS URL。 |
| alt | 文字列 | 画像のアクセス可能な説明。 |

> [!NOTE]
> 最終的なイメージの前にリダイレクトを行うイメージ URL がカードに含まれる場合、イメージ URL のリダイレクトはサポートされません。 これは、パブリック クラウド上で共有されるイメージに対して発生します。

### <a name="buttons"></a>ボタン

ボタンはカードの下部に上下に並んで表示されます。 ボタンのテキストは常に 1 行に表示され、テキストがボタンの幅を超えると切り捨てされます。 カードでサポートされている最大数を超える追加のボタンは表示されません。

詳細については、「カードアクション [」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。

### <a name="card-formatting"></a>カードの書式設定

カードのテキスト書式の詳細については、「カードの書式設定」 [を参照してください](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="adaptive-card"></a>アダプティブ カード

アダプティブ カードは、テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含むカスタマイズ可能なカードです。 アダプティブ [カード v1.2.0 を参照してください](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)。

### <a name="support-for-adaptive-cards"></a>アダプティブ カードのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
> * Teamsプラットフォームは、v1.2 以前のアダプティブ カード機能をサポートしています。
> * メディア要素は、現在、プラットフォーム上のアダプティブ カード v1.2 ではTeamsされていません。

### <a name="example-of-an-adaptive-card"></a>アダプティブ カードの例

![アダプティブ カードの例](~/assets/images/cards/adaptivecard.png)

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

以下の Bot Framework リファレンスを参照してください。

* [アダプティブ カードNode.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [アダプティブ カード C#](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a>ヒーロー カード

通常、1 つの大きな画像、1 つ以上のボタン、およびテキストを含むカード。

### <a name="support-for-hero-cards"></a>ヒーロー カードのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>ヒーロー カードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。 |
| サブタイトル | リッチ テキスト | カードのサブタイトル。 最大 2 行。|
| テキスト | リッチ テキスト | 字幕の下にテキストが表示されます。 書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。 |
| images | 画像の配列 | カードの上部に表示される画像。 縦横比 16:9。 |
| buttons | Action オブジェクトの配列 | 現在のカードに適用できるアクション一式。 最大で 6 までサポートされています。 |
| tap | Action オブジェクト | ユーザーがカード自体をタップするとアクティブ化されます。 |

### <a name="example-of-a-hero-card"></a>ヒーロー カードの例

![ヒーロー カードの例](~/assets/images/cards/hero.png)

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

### <a name="support-for-list-cards"></a>リスト カードのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>リスト カードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。|
| アイテム | リスト アイテムの配列 ||
| buttons | Action オブジェクトの配列 | 現在のカードに適用できるアクション一式。 最大で 6 までサポートされています。 |

### <a name="example-of-a-list-card"></a>リスト カードの例

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

コネクタ Office 365はボット フレームワークではなく、Teamsでサポートされています。 このカードは、複数のセクション、フィールド、画像、およびアクションを含む柔軟なレイアウトを提供します。 Bot が使用できるように、このカードがコネクタ カードをカプセル化します。 コネクタ カードと O365 カードの違いについては、「コネクタ カードに関するOffice 365[を参照してください](#notes-on-the-office-365-connector-card)。

### <a name="support-for-office-365-connector-cards"></a>Office 365 コネクタ カードでのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>Office 365 コネクタ カードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。 |
| 概要 | リッチ テキスト | カードの概要。 最大 2 行。 |
| テキスト | リッチ テキスト | 字幕の下にテキストが表示されます。 書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。 |
| themeColor | 16 進数文字列 | アプリケーション マニフェストから提供される accentColor を上書きする色。 |

### <a name="notes-on-the-office-365-connector-card"></a>Office 365 コネクタ カードに関する注意事項

Office 365カードは、ActionCard アクションなど、Microsoft Teamsで[適切に機能します](/outlook/actionable-messages/card-reference#actioncard-action)。

コネクタからコネクタ カードを使用する場合とボットでコネクタ カードを使用する場合の重要な違いの 1 つは、カードアクションの処理です。

* コネクタの場合、エンドポイントは HTTP POST を介してカード ペイロードを受け取ります。
* Bot の場合、`HttpPOST` アクションが、アクション ID と本文のみを Bot に送信する `invoke` アクティビティをトリガーします。

各コネクタ カードには最大 10 個のセクションを表示できます。各セクションには最大 5 つのイメージと 5 つのアクションを含めできます。

> [!NOTE]
> メッセージ内の追加のセクション、イメージ、またはアクションは表示されません。

すべてのテキスト フィールドは、マークダウンと HTML をサポートします。 メッセージ内のプロパティを設定することで、マークダウンまたは HTML を使用 `markdown` するセクションを制御できます。 既定では `markdown` 、 に設定されています `true` 。 HTML を代わりに使用する場合は、 に `markdown` 設定します `false` 。

`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。

レンダリング スタイルを指定するには `activityImage` 、次のように `activityImageType` 設定できます。

| 値 | 説明 |
| --- | --- |
| `avatar` | 既定値。 `activityImage` は、円としてトリミングされます。 |
| `article` | `activityImage` は四角形として表示され、縦横比が保持されます。 |

コネクタ カードのプロパティに関するその他の詳細については、「アクション可能な [メッセージ カードリファレンス」を参照してください](/outlook/actionable-messages/card-reference)。 現在サポートされていないコネクタ Microsoft Teamsのプロパティは次のとおりです。

* `heroImage`
* `hideOriginalBody`
* `startGroup`常に、次のように `true` 処理Teams
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>コネクタ カードOffice 365例

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

Teamsカードをサポートしています。 ボットがユーザーにレシートを提供できるカードです。 通常、税金や合計情報など、領収書に含めるアイテムの一覧が含まれます。

### <a name="support-for-receipt-cards"></a>レシート カードのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>レシート カードの例

![レシート カードの例](~/assets/images/cards/receipt.png)

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

* [レシート カードNode.js](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [レシート カード C#](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>サインイン カード

Signin card を使用すると、ボットはユーザーにサインインを要求できます。 これは、ボット フレームワークTeams少し異なる形式でサポートされています。 Teams のサインイン カードはボット フレームワークのサインイン カードに似ていますが、Teams のサインイン カードは 2 つのアクションのみをサポートしています。 `signin` `openUrl`

サインイン アクションは、サインイン カードだけでなく、Teams のすべてのカードで使用できます。 認証の詳細については、「ボットMicrosoft Teams[認証フロー」を参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。

### <a name="support-for-signin-cards"></a>サインイン カードのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>サインイン カードに関する追加情報

以下の Bot Framework リファレンスを参照してください。

* [Signin カード Node.js](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [サインイン カード C#](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>サムネイル カード

通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。

### <a name="support-for-thumbnail-cards"></a>サムネイル カードのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>サムネイル カードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。|
| サブタイトル | リッチ テキスト | カードのサブタイトル。 最大 2 行。|
| テキスト | リッチ テキスト | 字幕の下にテキストが表示されます。 書式設定オプションについては、「カードの書式設定 [」を参照してください](~/task-modules-and-cards/cards/cards-format.md)。 |
| images | 画像の配列 | カードの上部に表示される画像。 縦横比 1:1 平方 |
| buttons | Action オブジェクトの配列 | 現在のカードに適用できるアクション一式。 最大で 6 までサポートされています。 |
| tap | Action オブジェクト | ユーザーがカード自体をタップするとアクティブ化されます。 |

### <a name="example-of-a-thumbnail-card"></a>サムネイル カードの例

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

### <a name="additional-information"></a>追加情報

以下の Bot Framework リファレンスを参照してください。

* [サムネイル カード Node.js](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [サムネイル カード C#](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>カード コレクション

Teams Card コレクションをサポートしています。

カード コレクションには、 `builder.AttachmentLayout.carousel` と が含まれます `builder.AttachmentLayout.list` 。 これらのコレクションには、アダプティブ カード、ヒーロー カード、またはサムネイル カードが含まれる。

## <a name="carousel-collection"></a>カルーセル コレクション

[カルーセルのレイアウト](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。

### <a name="support-for-carousel-collections"></a>カルーセル コレクションのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> カルーセルは、メッセージごとに最大 10 枚のカードを表示できます。

### <a name="properties-of-a-carousel-card"></a>カルーセル カードのプロパティ

カルーセル カードのプロパティは、ヒーロー カードとサムネイル カードのプロパティと同じです。

### <a name="example-of-a-carousel-collection"></a>カルーセル コレクションの例

![カードのカルーセルの例](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a>カルーセル コレクションの構文

`builder.AttachmentLayoutTypes.Carousel` はカルーセル コレクションの構文です。

## <a name="list-collection"></a>リスト コレクション

### <a name="support-for-list-collections"></a>リスト コレクションのサポート

リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-list-collection"></a>リスト コレクションの例

![カードのリストの例](~/assets/images/cards/list.png)

プロパティは、ヒーローやサムネイル カードの場合と同じです。

リストには、メッセージごとに最大 10 枚のカードを表示できます。

> [!NOTE]
> iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。

### <a name="syntax-for-list-collections"></a>リスト コレクションの構文

`builder.AttachmentLayout.list` はリスト コレクションの構文です。

## <a name="cards-not-supported-in-teams"></a>Teams でサポートされていないカード

次のカードは Bot Framework によって実装されますが、ボット フレームワークではTeams。

* アニメーション カード
* オーディオ カード
* ビデオ カード
