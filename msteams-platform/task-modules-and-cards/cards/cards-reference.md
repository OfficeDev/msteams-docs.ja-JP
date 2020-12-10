---
title: カード リファレンス
description: Teams の Bot で使用できるすべてのカードとカード アクションについての説明
keywords: Bot のカード リファレンス
ms.openlocfilehash: 7c37d05ae4cfd07049eaec6dec5eda0f3312cefa
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346743"
---
# <a name="cards-reference"></a>カード リファレンス

このセクションに記載されているカードは、Teams の Bot でサポートされています。 Bot Framework で定義されたカードに基づいていますが、すべての Bot Framework カードが Teams でサポートされているわけではなく、独自のカードがいくつか追加されています。 相違点については、以下を参照してください。

## <a name="card-examples"></a>カードの例

カードの使用方法の詳細については、Bot Builder SDK (v3) のドキュメントで確認できます。 GitHub の Microsoft/BotBuilder のサンプル リポジトリでは、利用できるコード サンプルを参照することができます。

* .NET
  * [メッセージに添付ファイルとしてカードを追加する](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [カード サンプル コード (Bot Builder v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [メッセージに添付ファイルとしてカードを追加する](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [カード サンプル コード (Bot Builder v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>カードの種類

使用できるカードの種類を次の表に示します。

| カードの種類 | 説明 |
| --- | --- |
| [アダプティブ カード](#adaptive-card) | 高度なカスタマイズができるカード。テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせが可能です。 |
| [ヒーロー カード](#hero-card) | 通常、1 つの大きな画像、1 つまたは複数のボタン、少量のテキストが含まれます。 |
| [リスト カード](#list-card) | アイテムのスクロール リスト。 |
| [Office 365 コネクタ カード](#office-365-connector-card) | 複数のセクション、フィールド、画像、アクションに対応した柔軟なレイアウトです。 |
| [レシート カード](#receipt-card) | ユーザーに受領確認を提供します。 |
| [サインイン カード](#signin-card) | Bot がユーザーのサインインを要求できるようにします。 |
| [サムネイル カード](#thumbnail-card) | 通常、1 つのサムネイル画像、短いテキスト、1 つまたは複数のボタンが含まれます。 |
| [カード コレクション](#card-collections) | 単一の応答で複数のアイテムを返すときに使用します。 |

## <a name="common-properties-for-all-cards"></a>すべてのカードの共通プロパティ

### <a name="inline-card-images"></a>インライン カードの画像

公的に使用可能な画像へのリンクを挿入すれば、カードにインライン画像を含めることができます。 パフォーマンス上の観点から、公開されているコンテンツ配信ネットワーク (CDN) で画像をホストすることを強くお勧めします。

画像領域をカバーするように縦横比を保持しながらサイズを拡大または縮小し、カードの縦横比が適切になるように中央からトリミングします。

画像は最大 1024×1024 の PNG、JPEG、または GIF 形式である必要があります。アニメーション GIF はサポートされていません。

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| url | URL | 画像の HTTPS URL |
| alt | 文字列 | 画像へのアクセスに関する説明 |

### <a name="buttons"></a>ボタン

ボタンはカードの下部に上下に並んで表示されます。 ボタンのテキストは常に 1 行で表示され、テキストがボタンの幅を超えた場合は切り捨てられます。 カードでサポートされている最大数を超えるボタンは表示されません。

詳細については、「[カード アクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。

### <a name="card-formatting"></a>カードの書式設定

カードのテキストの書式設定の詳細については、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。

## <a name="adaptive-card"></a>アダプティブ カード

カスタマイズができるカードで、テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含めることができます。 ** [アダプティブ カード v 1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) を参照してください。

### <a name="support-for-adaptive-cards"></a>アダプティブ カードのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

> [!NOTE]
> メディア要素は、現在、Teams プラットフォームのアダプティブ カード v1.2 ではサポートされていません。

### <a name="example-adaptive-card"></a>アダプティブ カードの例

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

#### <a name="for-more-information-on-adaptive-cards"></a>アダプティブ カードの詳細

* [アダプティブ カードの概要](/adaptive-cards/)
* [Teams でのアダプティブ カードのアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>ヒーロー カード

通常、1 つの大きな画像、1 つまたは複数のボタン、テキストを含むカードです。

### <a name="support-for-hero-cards"></a>ヒーロー カードでのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="properties-of-a-hero-card"></a>ヒーロー カードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。 |
| サブタイトル | リッチ テキスト | カードのサブタイトル。 最大 2 行。|
| テキスト | リッチ テキスト | テキストはサブタイトルのすぐ下に表示されます。書式設定のオプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。 |
| images | 画像の配列 | カードの上部に表示される画像。 縦横比は 16:9 です |
| buttons | Action オブジェクトの配列 | 現在のカードに適用できるアクション一式。 最大で 6 までサポートされています |
| tap | Action オブジェクト | このアクションは、ユーザーがカード自体をタップしたときにアクティブになります |
|

### <a name="example-hero-card"></a>ヒーロー カードの例

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

### <a name="for-more-information-on-hero-cards"></a>ヒーロー カードの詳細

以下の Bot Framework リファレンスを参照してください。

* [ヒーロー カード ノード](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [ヒーロー カード C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a>リスト カード

リスト カードは Teams で追加されたもので、リスト コレクションを上回る機能が備わっています。 リスト カードは、アイテムのスクロール リストを提供します。

### <a name="support-for-list-cards"></a>リスト カードでのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |
|

### <a name="properties-of-a-list-card"></a>リスト カードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。|
| アイテム | リスト アイテムの配列  ||
| buttons | Action オブジェクトの配列 | 現在のカードに適用できるアクション一式。 最大で 6 までサポートされています。 |

### <a name="example-list-card"></a>リスト カードの例

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

Teams でサポートされています。Bot Framework ではサポートされていません。

Office 365 コネクタ カードには、複数のセクション、フィールド、画像、アクションに対応した柔軟なレイアウトが適用されています。 Bot が使用できるように、このカードがコネクタ カードをカプセル化します。 コネクタ カードと O365 カードの違いについては、「注意事項」の欄を参照してください。

### <a name="support-for-office-365-connector-cards"></a>Office 365 コネクタ カードでのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |
|

### <a name="properties-of-the-office-365-connector-card"></a>Office 365 コネクタ カードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。 |
| 概要 | リッチ テキスト | カードの概要。 最大 2 行。 |
| テキスト | リッチ テキスト | テキストはサブタイトルのすぐ下に表示されます。書式設定のオプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。 |
| themeColor | 16 進数文字列 | アプリケーション マニフェストで提供される accentColor よりも優先される色です |

### <a name="notes-on-the-office-365-connector-card"></a>Office 365 コネクタ カードに関する注意事項

Office 365 コネクタ カードは、[Actioncard アクション](/outlook/actionable-messages/card-reference#actioncard-action)を含む Microsoft Teams で正しく機能します。

コネクタからコネクタ カードを使用するのと、Bot でコネクタ カードを使用する際の重要な違いは、カード アクションの処理です。

* コネクタの場合、エンドポイントが HTTP POST 経由でカードのペイロードを受信します。
* Bot の場合、`HttpPOST` アクションが、アクション ID と本文のみを Bot に送信する `invoke` アクティビティをトリガーします。

各コネクタ カードは最大 10 個のセクションを表示でき、各セクションに最大 5 つの画像と 5 つのアクションを含めることができます。

> [!NOTE]
> メッセージ内の他のセクション、画像、アクションは表示されません。

すべてのテキスト フィールドは Markdown と HTML をサポートしています。 メッセージの `markdown` プロパティを設定して、Markdown または HTML を使用するセクションを制御することができます。 既定では、`markdown` は `true` に設定されています。代わりに HTML を使用する場合は、`markdown` を `false` に設定します。

`themeColor` プロパティを指定すると、そのプロパティがアプリのマニフェストの `accentColor` プロパティよりも優先されます。

`activityImage` の表示スタイルを指定するには、`activityImageType` を次のように設定します。

| 値 | 説明 |
| --- | --- |
| `avatar` | 既定では、`activityImage` は円としてトリミングされます |
| `article` | `activityImage` は四角形として表示され、縦横比は維持されます |

コネクタ カードのプロパティのその他の詳細については、「[操作可能なメッセージ カード リファレンス](/outlook/actionable-messages/card-reference)」を参照してください。 Microsoft Teams が現在サポートしていないコネクタ カードのプロパティは、以下のみとなります。

* `heroImage`
* `hideOriginalBody`
* `startGroup` (Teams では常に `true` として扱われます)
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a>Office 365 コネクタ カードの例

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

Teams でサポートされています。

Bot がユーザーに受領確認を提供できるようにするカードです。 通常は、受領書、税金、合計情報、その他のテキストに含めるアイテムの一覧が含まれます。

### <a name="support-for-receipts-cards"></a>レシート カードでのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="for-more-information-on-receipt-cards"></a>レシート カードの詳細については

以下の Bot Framework リファレンスを参照してください。

* [レシート カード ノード](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [レシート カード C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a>サインイン カード

Bot がユーザーのサインインを要求できるようにするカードです。 Bot Framework とは若干異なる形式で Teams でサポートされています。 Teams のサインイン カードは Bot Framework のサインイン カードと似ていますが、Teams のサインイン カードでサポートされているアクションは `signin` と `openUrl` の 2 つのみです。

*サインイン アクション* は、サインイン カードだけでなく、Teams のすべてのカードで使用できます。 認証の詳細については、「[Microsoft Teams の Bot における認証フロー](~/bots/how-to/authentication/auth-flow-bot.md)」を参照してください。

### <a name="support-for-signin-cards"></a>サインイン カードでのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

### <a name="for-more-information-on-signin-cards"></a>サインイン カードの詳細

以下の Bot Framework リファレンスを参照してください。

* [サインイン カード ノード](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [サインイン カード C#](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a>サムネイル カード

通常、1 つのサムネイル画像、1 つまたは複数のボタン、テキストを含むカードです。

### <a name="support-for-thumbnail-cards"></a>サムネイル カードでのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

![サムネイル カードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>サムネイル カードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト | カードのタイトル。 最大 2 行。|
| サブタイトル | リッチ テキスト | カードのサブタイトル。 最大 2 行。|
| テキスト | リッチ テキスト | テキストはサブタイトルのすぐ下に表示されます。書式設定のオプションについては、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。 |
| images | 画像の配列 | カードの上部に表示される画像。 縦横比は 1:1 (正方形) です |
| buttons | Action オブジェクトの配列 | 現在のカードに適用できるアクション一式。 最大で 6 までサポートされています |
| tap | Action オブジェクト | このアクションは、ユーザーがカード自体をタップしたときにアクティブになります |
|

### <a name="example-thumbnail-card"></a>サムネイル カードの例

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

### <a name="for-more-information"></a>関連情報

以下の Bot Framework リファレンスを参照してください。

* [サムネイル カード ノード](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [サムネイル カード C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a>カード コレクション

カード コレクションは Teams でサポートされています。

`builder.AttachmentLayout.carousel` と `builder.AttachmentLayout.list` のカード コレクションが Bot Framework によって提供されています。 これらのコレクションには、アダプティブ、ヒーロー、サムネイルのカードを含めることができます。

## <a name="carousel-collection"></a>カルーセル コレクション

[カルーセルのレイアウト](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true)でカードのカルーセルが表示され、関連付けられたアクション ボタンがオプションで示されます。

### <a name="support-for-carousel-collections"></a>カルーセル コレクションでのサポート

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

> [!NOTE]
> カルーセルでは、メッセージごとに最大 10 枚のカードを表示することができます。

### <a name="example-carousel-collection"></a>カルーセル コレクションの例

![カードのカルーセルの例](~/assets/images/cards/carousel.png)

プロパティは、ヒーローやサムネイル カードの場合と同じです。

### <a name="syntax-for-carousel-collections"></a>カルーセル コレクションの構文

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a>リスト コレクション

### <a name="support-for-list-collections"></a>リスト コレクションでのサポート

リストのレイアウトでカードが縦方向に一覧表示され、関連付けられたアクション ボタンがオプションで示されます。

| Teams の Bot | メッセージング拡張機能  | コネクタ | Bot Framework |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-list-collection"></a>リスト コレクションの例

![カードのリストの例](~/assets/images/cards/list.png)

プロパティは、ヒーローやサムネイル カードの場合と同じです。

リストでは、メッセージごとに最大 10 枚のカードを表示することができます。

> [!NOTE]
> iOS および Android では、一部のリスト カードの組み合わせがまだサポートされていません。

### <a name="syntax-for-list-collections"></a>リスト コレクションの構文

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>Teams でサポートされていないカード

次のカードは Bot Framework によって実装されていますが、Teams ではサポートされていません。

* アニメーション カード
* オーディオ カード
* ビデオ カード
