---
title: カードリファレンス
description: Teams のボットで利用可能なすべてのカードおよびカードアクションについて説明します。
keywords: bot カードリファレンス
ms.openlocfilehash: 76b9cb7e2508d300deb2e3cd4f392fdb9850062d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674829"
---
# <a name="cards-reference"></a>カードリファレンス

このセクションに記載されているカードは、Teams の bot でサポートされています。 Bot フレームワークによって定義されたカードに基づいていますが、Teams はすべての Bot フレームワークカードをサポートしておらず、一部を追加しています。 相違点については、以下の参考資料を参照してください。

## <a name="card-examples"></a>カードの例

カードの使用方法の詳細については、Bot ビルダー SDK (v3) のドキュメントを参照してください。 GitHub の Microsoft/BotBuilder リポジトリで使用可能なコードサンプルもあります。

* .NET
  * [メッセージに添付ファイルとしてカードを追加する](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [カードサンプルコード (Bot ビルダー v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [メッセージに添付ファイルとしてカードを追加する](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [カードサンプルコード (Bot ビルダー v3)](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>カードの種類

次の表に、使用できるカードの種類を示します。

| カードの種類 | 説明 |
| --- | --- |
| [アダプティブカード](#adaptive-card) | テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含むことができる高度にカスタマイズ可能なカード。 |
| [英雄カード](#hero-card) | 通常は1つの大きな画像、1つまたは複数のボタン、および少量のテキストが含まれています。 |
| [カードの一覧表示](#list-card) | アイテムのスクロールリスト。 |
| [Office 365 コネクタカード](#office-365-connector-card) | 複数のセクション、フィールド、画像、アクションを持つ柔軟なレイアウト。 |
| [レシートカード](#receipt-card) | ユーザーに受信確認を提供します。 |
| [サインインカード](#signin-card) | Bot がユーザーのサインインを要求できるようにします。 |
| [サムネイルカード](#thumbnail-card) | 通常は、1つのサムネイル画像、短いテキスト、1つまたは複数のボタンが含まれています。 |
| [カードコレクション](#card-collections) | 単一の応答で複数のアイテムを返すために使用されます。 |

## <a name="common-properties-for-all-cards"></a>すべてのカードの共通プロパティ

### <a name="inline-card-images"></a>インラインカードの画像

カードには、公的の使用可能な画像へのリンクを含めることで、インライン画像を含めることができます。 パフォーマンス上の理由から、公開されたコンテンツ配信ネットワーク (CDN) で画像をホストすることを強くお勧めします。

画像を拡大または縮小して、画像領域をカバーしてから、カードの適切な縦横比を達成するために、画像の縦横比を維持しながら、サイズを拡大または縮小します。

画像は最大1024×1024で、PNG、JPEG、または GIF 形式では 1 MB でなければなりません。アニメーション GIF は正式にはサポートされていません。

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| url | URL | 画像への HTTPS URL |
| alt | String | 画像のアクセス可能な説明 |

### <a name="buttons"></a>ボタン

ボタンは、カードの下部に積み重ねて表示されます。 ボタンのテキストは常に1行になり、テキストがボタンの幅を超えた場合は切り捨てられます。 カードでサポートされている最大数を超える追加のボタンは表示されません。

詳細については、「[カードアクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。

### <a name="card-formatting"></a>カードの書式設定

カードのテキストの書式設定の詳細については、「[カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。

## <a name="adaptive-card"></a>アダプティブカード

> [!NOTE]
> すべてのユーザーに対して、アダプティブカードのバージョン1.0 のみがサポートされています。 現在、バージョン1.2 は開発者向けプレビューでのみ利用可能です。

テキスト、音声、画像、ボタン、入力フィールドの任意の組み合わせを含むことができるカスタマイズ可能なカード。

### <a name="support-for-adaptive-cards"></a>アダプティブカードのサポート

| Teams のボット | メッセージング拡張機能  | コネクタ | Bot フレームワーク |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-adaptive-card"></a>アダプティブカードの例

![アダプティブカードカードの例](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a>アダプティブカードの詳細については、

* [アダプティブカードの概要](/adaptive-cards/)
* [Teams でのアダプティブカードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>英雄カード

通常1つの大きな画像、1つまたは複数のボタンとテキストを含むカード。

### <a name="support-for-hero-cards"></a>英雄カードのサポート

| Teams のボット | メッセージング拡張機能  | コネクタ | Bot フレームワーク |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="properties-of-a-hero-card"></a>英雄カードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト  | カードのタイトル。 最大2行現在サポートされていない書式設定 |
| サブタイトル | リッチ テキスト  | カードのサブタイトル。 最大2行現在サポートされていない書式設定 |
| text | リッチ テキスト  | テキストは、サブタイトルのすぐ下に表示されます。書式設定オプションの[カード書式](~/task-modules-and-cards/cards/cards-format.md)を表示する |
| images | 画像の配列 | カードの上部に表示される画像。 縦横比16:9 |
| リモコン | Action オブジェクトの配列 | 現在のカードに適用できるアクションのセット。 最大6 |
| 搭載 | Action オブジェクト | このアクションは、ユーザーがカード自体をタップしたときにアクティブになります。 |
|

### <a name="example-hero-card"></a>英雄カードの例

![英雄カードの例](~/assets/images/cards/hero.png)

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

### <a name="for-more-information-on-hero-cards"></a>英雄カードの詳細については、

Bot フレームワークリファレンス:

* [英雄カードノード](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [英雄カード C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a>カードの一覧表示

リストカードは Teams によって追加されており、リストコレクションが提供する機能を超える機能を提供します。 リストカードは、アイテムのスクロールリストを提供します。

### <a name="support-for-list-cards"></a>リストカードのサポート

| Teams のボット | メッセージング拡張機能  | コネクタ | Bot フレームワーク |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |
|

### <a name="properties-of-a-list-card"></a>リストカードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト  | カードのタイトル。 最大2行現在サポートされていない書式設定 |
| items | リストアイテムの配列  ||
| リモコン | Action オブジェクトの配列 | 現在のカードに適用できるアクションのセット。 最大6。 モバイルでは表示されません。 |
|

### <a name="example-list-card"></a>リストカードの例

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

## <a name="office-365-connector-card"></a>Office 365 コネクタカード

Teams ではサポートされていません。 Bot フレームワークではサポートされません。

Office 365 コネクタカードには、複数のセクション、フィールド、画像、およびアクションを備えた柔軟なレイアウトが用意されています。 このカードは、コネクタカードをカプセル化して、bot がそれを使用できるようにします。 コネクタカードと O365 カードの違いについては、「メモ」セクションを参照してください。

### <a name="support-for-office-365-connector-cards"></a>Office 365 コネクタカードのサポート

| Teams のボット | メッセージング拡張機能  | コネクタ | Bot フレームワーク |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |
|

### <a name="properties-of-the-office-365-connector-card"></a>Office 365 コネクタカードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト  | カードのタイトル。 最大2行現在サポートされていない書式設定 |
| summary | リッチ テキスト  | カードの概要。 最大2行現在サポートされていない書式設定 |
| text | リッチ テキスト  | テキストは、サブタイトルのすぐ下に表示されます。書式設定オプションの[カード書式](~/task-modules-and-cards/cards/cards-format.md)を表示する |
| themeColor | 16進文字列 | アプリケーションマニフェストで提供される、表示色をオーバーライドする色 |

### <a name="notes-on-the-office-365-connector-card"></a>Office 365 コネクタカードのメモ

Office 365 のコネクタカードは、 [Actioncard アクション](/outlook/actionable-messages/card-reference#actioncard-action)を含む Microsoft Teams では正しく機能します。

コネクタからコネクタカードを使用することと、ボットでコネクタカードを使用することの重要な違いは、カードアクションの処理です。

* コネクタの場合、エンドポイントは HTTP POST 経由でカードのペイロードを受信します。
* Bot の場合、アクション`HttpPOST`は、アクション`invoke` ID と本文のみを bot に送信するアクティビティをトリガーします。

各コネクタカードには最大10個のセクションを表示でき、各セクションには最大5つの画像と5つのアクションを含めることができます。

> [!NOTE]
> メッセージ内の追加のセクション、画像、アクションは表示されません。

すべてのテキストフィールドは、Markdown と HTML をサポートしています。 Markdown または HTML を使用するセクションは、 `markdown`メッセージでプロパティを設定することによって制御できます。 既定では`markdown` 、はに`true`設定されています。代わりに HTML を使用する場合は、を`markdown`に`false`設定します。

`themeColor`プロパティを指定すると、そのプロパティは`accentColor`アプリマニフェストのプロパティより優先されます。

のレンダリングスタイルを指定する`activityImage`には、次`activityImageType`のように設定します。

| 値 | 説明 |
| --- | --- |
| `avatar` | 限り`activityImage`円としてトリミングされます。 |
| `article` | `activityImage`四角形として表示され、その縦横比を保持します。 |

コネクタカードのプロパティに関するその他の詳細については、「操作可能な[メッセージカードリファレンス](/outlook/actionable-messages/card-reference)」を参照してください。 Microsoft Teams が現在サポートしていないコネクタカードのプロパティは、次のとおりです。

* `heroImage`
* `hideOriginalBody`
* `startGroup`(常に Teams `true`で扱います)
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a>Office 365 コネクタカードの例

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

## <a name="receipt-card"></a>レシートカード

Teams でサポートされています。

Bot がユーザーにレシートを提供できるようにするカード。 通常、レシート、税金、およびその他のテキストに含めるアイテムの一覧が含まれます。

### <a name="support-for-receipts-cards"></a>領収書カードのサポート

| Teams のボット | メッセージング拡張機能  | コネクタ | Bot フレームワーク |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="for-more-information-on-receipt-cards"></a>受信カードの詳細については、

Bot フレームワークリファレンス:

* [レシートカードノード](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [レシートカード C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a>サインインカード

Bot がユーザーのサインインを要求することを可能にするカード。 Bot フレームワークで見つかったものとは異なる形式の Teams でサポートされています。 Teams のサインインカードは bot フレームワークのサインインカードに似ていますが、Teams のサインインカードでは、 `signin`との2つのアクション`openUrl`のみがサポートされるという例外があります。

*サインインアクション*は、サインインカードだけでなく、Teams のすべてのカードから使用できます。 認証の詳細については、「 [bot の Microsoft Teams 認証フロー](~/bots/how-to/authentication/auth-flow-bot.md) 」を参照してください。

### <a name="support-for-signin-cards"></a>サインインカードのサポート

| Teams のボット | メッセージング拡張機能  | コネクタ | Bot フレームワーク |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

### <a name="for-more-information-on-signin-cards"></a>サインインカードの詳細については、

Bot フレームワークリファレンス:

* [サインインカードのノード](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [サインインカード C#](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a>サムネイルカード

通常は1つのサムネイル画像、1つまたは複数のボタン、テキストを含むカード。

### <a name="support-for-thumbnail-cards"></a>サムネイルカードのサポート

| Teams のボット | メッセージング拡張機能  | コネクタ | Bot フレームワーク |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

![サムネイルカードの例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>サムネイルカードのプロパティ

| プロパティ | 型  | 説明 |
| --- | --- | --- |
| title | リッチ テキスト  | カードのタイトル。 最大2行現在サポートされていない書式設定 |
| サブタイトル | リッチ テキスト  | カードのサブタイトル。 最大2行現在サポートされていない書式設定 |
| text | リッチ テキスト  | テキストは、サブタイトルのすぐ下に表示されます。書式設定オプションの[カード書式](~/task-modules-and-cards/cards/cards-format.md)を表示する |
| images | 画像の配列 | カードの上部に表示される画像。 縦横比 1:1 (正方形) |
| リモコン | Action オブジェクトの配列 | 現在のカードに適用できるアクションのセット。 最大6 |
| 搭載 | Action オブジェクト | このアクションは、ユーザーがカード自体をタップしたときにアクティブになります。 |
|

### <a name="example-thumbnail-card"></a>サムネイルカードの例

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

Bot フレームワークリファレンス:

* [サムネイルカードノード](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [サムネイルカード C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a>カードコレクション

カードコレクションは Teams でサポートされています。

カードコレクションは Bot フレームワークによって提供`builder.AttachmentLayout.carousel`さ`builder.AttachmentLayout.list`れます。 これらのコレクションには、アダプティブ、英雄、またはサムネイルカードを含めることができます。

## <a name="carousel-collection"></a>カルーセルコレクション

[カルーセルのレイアウト](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0)は、オプションで、関連付けられたアクションボタンを表示するカルーセルのカードを示しています。

### <a name="support-for-carousel-collections"></a>カルーセルコレクションのサポート

| Teams のボット | メッセージング拡張機能  | コネクタ | Bot フレームワーク |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

> [!NOTE]
> カルーセルは、メッセージごとに最大10枚のカードを表示できます。

### <a name="example-carousel-collection"></a>カルーセルのコレクションの例

![カードのカルーセルの例](~/assets/images/cards/carousel.png)

プロパティは、英雄またはサムネイルカードの場合と同じです。

### <a name="syntax-for-carousel-collections"></a>カルーセルコレクションの構文

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a>List コレクション

### <a name="support-for-list-collections"></a>リストコレクションのサポート

リストレイアウトは、カードの縦に積み上げたリストを表示します。オプションで、関連付けられたアクションボタンを表示します。

| Teams のボット | メッセージング拡張機能  | コネクタ | Bot フレームワーク |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-list-collection"></a>List コレクションの例

![カードリストの例](~/assets/images/cards/list.png)

プロパティは、英雄またはサムネイルカードの場合と同じです。

リストでは、メッセージごとに最大10個のカードを表示できます。

> [!NOTE]
> IOS および Android では、リストカードの一部の組み合わせはまだサポートされていません。

### <a name="syntax-for-list-collections"></a>リストコレクションの構文

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>Teams でサポートされていないカード

次のカードは Bot フレームワークによって実装されていますが、Teams ではサポートされていません。

* アニメーションカード
* オーディオカード
* ビデオカード
