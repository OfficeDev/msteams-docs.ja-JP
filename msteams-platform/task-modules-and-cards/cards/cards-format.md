---
title: カード内のテキストの書式設定
description: カードテキストの書式設定について説明Microsoft Teams
keywords: teams ボット カードの形式
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 877a16f884e91138dc656434438a5fe1dd2ffd6e
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140640"
---
# <a name="format-cards-in-microsoft-teams"></a>カードの書式を設定Microsoft Teams

カードにリッチ テキストの書式設定を追加する 2 つの方法を次に示します。
* [Markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

カードは、タイトルプロパティや字幕プロパティではなく、text プロパティでのみ書式設定をサポートします。 書式設定は、カードの種類に応じて、XML または HTML の書式設定または Markdown のサブセットを使用して指定できます。 アダプティブ カードの現在および将来の開発では、Markdown の書式設定をお勧めします。

書式設定のサポートは、カードの種類によって異なります。 カードのレンダリングは、デスクトップ とモバイル クライアントの間で、Microsoft Teamsとデスクトップ ブラウザー Teams若干異なる場合があります。

インライン イメージは、任意のカードにTeamsできます。 イメージは、、、またはファイルとして書式設定できますし `.png` `.jpg` `.gif` 、1024 ピクセルまたは 1024 px または 1 MB を超え×する必要があります。 アニメーション GIF はサポートされていません。 詳細については、「カードの [種類」を参照してください](./cards-reference.md#inline-card-images)。

サポートされている特定のスタイルを含む markdown Office 365アダプティブ カードとコネクタ カードの書式を設定できます。

## <a name="format-cards-with-markdown"></a>Markdown でカードを書式設定する

次のカードの種類では、マークダウンの書式設定がサポートTeams。

* アダプティブ カード: Markdown はアダプティブ カード フィールドおよび `Textblock` `Fact.Title` `Fact.Value` . アダプティブ カードでは HTML はサポートされていません。
* O365 コネクタ カード: テキスト フィールドの O365 コネクタ カードでは、マークダウンと制限付き HTML がサポートされています。

リスト内の改行に対して、アダプティブ カードの改行を使用するか、エスケープ `\r` `\n` シーケンスを使用できます。 アダプティブ カード用のデスクトップとモバイル バージョンの書式Teams異なります。 カード ベースのメンションは、Web クライアント、デスクトップ クライアント、モバイル クライアントでサポートされています。 information masking プロパティを使用すると、アダプティブ カード入力要素内のユーザーからのパスワードや機密情報などの特定の情報を `Input.Text` マスクできます。 アダプティブ カードの幅は、オブジェクトを使用して展開 `width` できます。 アダプティブ カード内で typeahead サポートを有効にし、ユーザーが入力を入力すると、入力の選択肢のセットをフィルター処理できます。 このプロパティを使用 `msteams` して、ステージ ビューに画像を選択的に表示する機能を追加できます。

アダプティブ カードとコネクタ カードのデスクトップとモバイル バージョンのTeamsは異なります。 このセクションでは、アダプティブ カードとコネクタ カードの Markdown 形式の例を参照できます。

# <a name="markdown-format-for-adaptive-cards"></a>[アダプティブ カードのマークダウン形式](#tab/adaptive-md)

 次の表に、、 、およびのサポート `Textblock` されているスタイル `Fact.Title` を示します `Fact.Value` 。

| Style | 例 | Markdown |
| --- | --- | --- |
| 太字 | **Bold** | ```**Bold**``` |
| 斜体 | _Italic_ | ```_Italic_``` |
| 記号付きリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 番号付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[Bing](https://www.bing.com/)| ```[Title](url)``` |

次の Markdown タグはサポートされていません。

* ヘッダー
* テーブル
* 画像
* 書式設定済みのテキスト
* Blockquotes

### <a name="newlines-for-adaptive-cards"></a>アダプティブ カードの改行

リスト内の改行 `\r` には、エスケープ `\n` シーケンスまたはエスケープ シーケンスを使用できます。 リスト `\n\n` で使用すると、リスト内の次の要素がインデントされます。 TextBlock の他の場所で改行が必要な場合は、 を使用します `\n\n` 。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>アダプティブ カードのモバイルとデスクトップの違い

デスクトップでは、アダプティブ カード マークダウンの書式設定は、Web ブラウザーとクライアント アプリケーションの両方の次のTeams表示されます。

![デスクトップ クライアントでのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

iOS では、アダプティブ カード マークダウンの書式設定が次の図のように表示されます。

![iOS でのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

Android では、アダプティブ カード マークダウンの書式設定が次の図のように表示されます。

![Android でのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-Android.png)

詳細については、「アダプティブ カード」 [のテキスト機能を参照してください](/adaptive-cards/create/textfeatures)。

> [!NOTE]
> このセクションで説明する日付とローカライズ機能は、このセクションではTeams。

### <a name="adaptive-cards-format-sample"></a>アダプティブ カード形式のサンプル

次のコードは、アダプティブ カードの書式設定の例を示しています。

``` json
{
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "This is some **bold** text"
        },
        {
            "type": "TextBlock",
            "text": "This is some _italic_ text"
        },
        {
            "type": "TextBlock",
            "text": "- Bullet \r- List \r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "1. Numbered\r2. List\r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Check out [Adaptive Cards](https://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a>アダプティブ カード v1.2 内でのサポートのメンション

ボットおよびメッセージング拡張機能@mentionsアダプティブ カード本文内に追加できます。 カードに@mentionsするには、チャネルおよびグループ チャットの会話でメッセージ ベースのメンションと同じ通知ロジックとレンダリング [に従います](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)。

ボットとメッセージング拡張機能には [、TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 要素と FactSet 要素のカード コンテンツ内にメンション [を含](https://adaptivecards.io/explorer/FactSet.html) めることはできません。

> [!NOTE]
> * [メディア要素](https://adaptivecards.io/explorer/Media.html)は、現在、プラットフォーム上のアダプティブ カード v1.2 ではTeamsされていません。
> * チャネルとチームのメンションはボット メッセージではサポートされていません。

アダプティブ カードにメンションを含めるには、アプリに次の要素を含める必要があります。

* `<at>username</at>` は、サポートされているアダプティブ カード要素に含まれます。
* カード `mention` コンテンツ内のプロパティ内のオブジェクトには、Teams `msteams` のユーザー ID が含まれます。
* これは `userId` 、ボット ID と特定のユーザーに固有です。 特定のユーザーを@mention使用できます。 ユーザー `userId` ID の取得に記載されているオプションのいずれかを使用して [取得できます](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)。

#### <a name="sample-adaptive-card-with-a-mention"></a>メンション付きアダプティブ カードのサンプル

次のコードは、メンションを持つアダプティブ カードの例を示しています。

``` json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "type": "AdaptiveCard",
    "body": [
      {
        "type": "TextBlock",
        "text": "Hi <at>John Doe</at>"
      }
    ],
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.0",
    "msteams": {
      "entities": [
        {
          "type": "mention",
          "text": "<at>John Doe</at>",
          "mentioned": {
            "id": "29:123124124124",
            "name": "John Doe"
          }
        }
      ]
    }
  }
}
```

### <a name="information-masking-in-adaptive-cards"></a>アダプティブ カードの情報マスキング

Information masking プロパティを使用して、アダプティブ カード入力要素内のユーザーからのパスワードや機密情報などの特定の情報を [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) マスクします。

> [!NOTE]
> この機能は、クライアント側の情報マスキングのみをサポートします。 マスクされた入力テキストは、ボットの構成中に指定された HTTPS エンドポイント アドレスにクリア テキスト [として送信されます](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)。

アダプティブ カードで情報をマスクするには、型に `isMasked` プロパティを追加 **し** `Input.Text` 、その値を true に設定 **します**。

#### <a name="sample-adaptive-card-with-masking-property"></a>マスキング プロパティを持つアダプティブ カードのサンプル

次のコードは、マスキング プロパティを持つアダプティブ カードの例を示しています。

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

次の図は、アダプティブ カードのマスキング情報の例です。

![マスキング情報イメージ](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>全幅アダプティブ カード

このプロパティを使用 `msteams` すると、アダプティブ カードの幅を拡大し、追加のキャンバス領域を利用できます。 次のセクションでは、プロパティの使い方について説明します。

#### <a name="construct-full-width-cards"></a>全幅カードを作成する

全幅アダプティブ カードを作成するには、カード コンテンツの `width` `msteams` プロパティのオブジェクトをに設定する必要があります `Full` 。

#### <a name="sample-adaptive-card-with-full-width"></a>全幅のアダプティブ カードのサンプル

全幅アダプティブ カードを作成するには、アプリに次のコード サンプルの要素を含める必要があります。

``` json
{
    "type": "AdaptiveCard",
    "body": [{
        "type": "Container",
        "items": [{
            "type": "TextBlock",
            "text": "Digest card",
            "size": "Large",
            "weight": "Bolder"
        }]
    }],

    "msteams": {
        "width": "Full"
    },
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

次の図は、全幅アダプティブ カードを示しています。

![全幅アダプティブ カード ビュー](../../assets/images/cards/full-width-adaptive-card.png)

次の図は、プロパティを Full に設定していない場合のアダプティブ カードの既定 `width` のビューを **示しています**。

![小幅アダプティブ カード ビュー](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Typeahead のサポート

schema 要素内で、ユーザーにフィルター処理を求め、サイズの大きい数の選択肢を選択すると、タスクの完了が大幅 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) に遅くなる可能性があります。 アダプティブ カード内の Typeahead サポートは、ユーザーが入力を入力する場合に、入力の選択肢のセットを絞り込むかフィルター処理することで、入力の選択を簡略化できます。

で typeahead を有効にするには `Input.Choiceset` 、に設定 `style` し、 `filtered` 必ずに `isMultiSelect` 設定します `false` 。

#### <a name="sample-adaptive-card-with-typeahead-support"></a>Typeahead サポートを備えるアダプティブ カードのサンプル

次のコードは、typeahead サポートを備えるアダプティブ カードの例を示しています。

``` json
{
   "type": "Input.ChoiceSet",
   "label": "Select a user",
   "isMultiSelect": false,
   "choices":  [
      { "title": "User 1", "value": "User1" },
      { "title": "User 2", "value": "User2" }
    ],
   "style": "filtered"
}
```

### <a name="stage-view-for-images-in-adaptive-cards"></a>アダプティブ カードの画像のステージ ビュー

アダプティブ カードでは、このプロパティを使用して、ステージ ビューで画像を選択的 `msteams` に表示する機能を追加できます。 ユーザーが画像にカーソルを合わせると、展開アイコンが表示され、属性が `allowExpand` に設定されます `true` 。 プロパティの使用方法については、次の例を参照してください。

``` json
{
    "type": "AdaptiveCard",
     "body": [
          {
            "type": "Image",
            "url": "https://picsum.photos/200/200?image=110",
            "msTeams": {
              "allowExpand": true
            }
          },
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

ユーザーが画像の上にマウス ポインターを置くと、次の図に示すように、右上隅に展開アイコンが表示されます。

![展開可能なイメージを持つアダプティブ カード](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

次の図に示すように、ユーザーが展開アイコンを選択すると、イメージがステージ ビューに表示されます。

![ステージ ビューに展開されたイメージ](../../assets/images/cards/adaptivecard-expand-image.png)

ステージ ビューでは、ユーザーは画像を拡大および縮小できます。 この機能が必要なアダプティブ カードの画像を選択できます。

> [!NOTE]
> * 拡大および縮小機能は、アダプティブ カードの画像の種類である画像要素にのみ適用されます。
> * モバイル Teamsでは、アダプティブ カードの画像のステージ ビュー機能が既定で使用できます。 ユーザーは、属性が存在するかどうかに関係なく、画像をタップするだけでステージ ビューでアダプティブ カードイメージ `allowExpand` を表示できます。

# <a name="markdown-format-for-o365-connector-cards"></a>[O365 コネクタ カードのマークダウン形式](#tab/connector-md)

コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。

| Style | 例 | Markdown |
| --- | --- | --- |
| 太字 | **text** | `**text**` |
| 斜体 | *text* | `*text*` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `### Text`|
| 取り消し線 | ~~text~~ | `~~text~~` |
| 記号付きリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 番号付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 書式設定済みのテキスト | `text` | ``preformatted text`` |
| Blockquote | >をブロッククォートする | `>blockquote text` |
| Hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 画像リンク |![岩の上のアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

コネクタ カードでは、改行はのためにレンダリングされますが `\n\n` 、for または `\n` `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>コネクタ カードのモバイルとデスクトップの違い

デスクトップでは、次の図に示すように、コネクタ カードの Markdown 書式設定が表示されます。

![デスクトップ クライアントでのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

iOS では、次の図に示すように、コネクタ カードの Markdown 書式設定が表示されます。

![iOS クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

iOS 用 Markdown を使用するコネクタ カードには、次の問題があります。

* コネクタ カードの iOS クライアントTeamsマークダウンまたは HTML インライン イメージはレンダリングされません。
* ブロッククォートはインデントされますが、灰色の背景なしでレンダリングされます。

Android では、次の図に示すように、コネクタ カードのマークダウンの書式設定が表示されます。

![Android クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a>Markdown コネクタ カードの形式の例

次のコードは、Markdown コネクタ カードの書式設定の例を示しています。

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card Markdown formatting",
    "sections": [
        {
            "text": "This is some **bold** text"
        },
        {
            "text": "This is some _italic_ text"
        },
        {
            "text": "# Header 1\r## Header 2\r### Header 3"
        },
        {
            "text": "- Bullet \r- List \r"
        },
        {
            "text": "1. Numbered\r1. List \r"
        },
        {
            "text": "Link: [Bing](https://www.bing.com)"
        },
        {
            "text": "embedded image link: ![Duck on a rock](https://aka.ms/Fo983c)"
        },
        {
            "text": "`preformatted text`"
        },
        {
            "text": "Newlines (backslash n, backslash n):\n\nline a\n\nline b\n\nline c"
        },
        {
            "text": ">This is a blockquote"
        }
     ]
  }
}

```

---

## <a name="format-cards-with-html"></a>HTML を使用してカードを書式設定する

次のカードの種類は、HTML 形式をサポートTeams。

* O365 コネクタ カード: 制限付きマークダウンと HTML の書式設定は、コネクタ カードOffice 365サポートされています。
* ヒーロー カードとサムネイル カード: HTML タグは、ヒーロー カードやサムネイル カードなどの単純なカードでサポートされます。

O365 Connector カードと簡易カードの場合、Teamsとモバイル バージョンの書式は異なります。 このセクションでは、コネクタ カードと簡易カードの HTML 形式の例を参照できます。

# <a name="html-format-for-o365-connector-cards"></a>[O365 コネクタ カードの HTML 形式](#tab/connector-html)

コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。

| Style | 例 | HTML |
| --- | --- | --- |
| 太字 | **text** | `<strong>text</strong>` |
| 斜体 | *text* | `<em>text</em>` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| 取り消し線 | ~~text~~ | `<strike>text</strike>` |
| 記号付きリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 番号付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 書式設定済みのテキスト | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>テキスト</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

コネクタ カードでは、タグを使用して改行が HTML でレンダリング `<p>` されます。

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>コネクタ カードのモバイルとデスクトップの違い

デスクトップでは、次の図に示すように、コネクタ カードの HTML 書式が表示されます。

![デスクトップ クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/Connector-desktop-html-combined.png)

iOS では、次の図に示すように HTML 書式が表示されます。

![iOS クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-iphone-html-combined-80.png)

iOS 用 HTML を使用するコネクタ カードには、次の問題があります。

* インライン イメージは、コネクタ カードの Markdown または HTML を使用して iOS ではレンダリングされません。
* 書式設定済みのテキストはレンダリングされますが、背景が灰色ではありません。

Android では、次の図に示すように HTML 書式が表示されます。

![Android クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a>HTML コネクタ カードの形式のサンプル

次のコードは、HTML コネクタ カードの書式設定の例を示しています。

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card HTML formatting",
    "sections": [
        {
            "text": "This is some <strong>bold</strong> text"
        },
        {
            "text": "This is some <em>italic</em> text"
        },
        {
            "text": "This is some <strike>strikethrough</strike> text"
        },
        {
            "text": "<h1>Header 1</h1>\r<h2>Header 2</h2>\r <h3>Header 3</h3>"
        },
        {
            "text": "bullet list <ul><li>text</li><li>text</li></ul>"
        },
        {
            "text": "ordered list <ol><li>text</li><li>text</li></ol>"
        },
        {
            "text": "hyperlink <a href=\"https://www.bing.com/\">Bing</a>"
        },
        {
            "text": "embedded image <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
        },
        {
            "text": "preformatted text <pre>text</pre>"
        },
        {
            "text": "Paragraphs <p>Line a</p><p>Line b</p>"
        },
        {
            "text": "<blockquote>Blockquote text</blockquote>"
        }
     ]
  }
}

```

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[ヒーロー カードとサムネイル カードの HTML 形式](#tab/simple-html)

HTML タグは、ヒーロー カードやサムネイル カードなどの単純なカードでサポートされます。 Markdown はサポートされていません。

| Style | 例 | HTML |
| --- | --- | --- |
| 太字 | **text** | `<strong>text</strong>` |
| 斜体 | *text* | `<em>text</em>` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| 取り消し線 | ~~text~~ | `<strike>text</strike>` |
| 記号付きリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 番号付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 書式設定済みのテキスト | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>テキスト</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>単純なカードのモバイルとデスクトップの違い

デスクトップ プラットフォームとモバイル プラットフォームの解像度の違いがある場合、デスクトップとモバイル バージョンのモバイル プラットフォームでは書式設定が異Teams。

デスクトップでは、次の図に示すように HTML 書式が表示されます。

![デスクトップ クライアントでの HTML 書式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

iOS では、次の図に示すように HTML 書式が表示されます。

![iOS クライアントの HTML 書式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

太字や斜体などの文字の書式設定は、iOS ではレンダリングされません。

Android では、次の図に示すように HTML 書式が表示されます。

![Android クライアントでの HTML 書式](../../assets/images/cards/card-formatting-xml-android-60.png)

Android で太字や斜体などの文字の書式設定が正しく表示されます。

### <a name="format-example-for-simple-cards"></a>単純なカードの形式の例

前のセクションのイメージは、Teams **App Studio** を使用して作成され、ヒーロー カードの text プロパティは次の文字列に設定されます。

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

このコードを変更することで、独自のカードの書式設定をテストできます。

---

## <a name="see-also"></a>関連項目

* [カードアクション](./cards-actions.md)
* [タスク モジュール](~/task-modules-and-cards/cards/cards-format.md)
