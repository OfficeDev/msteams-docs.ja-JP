---
title: カードでのテキストの書式設定
description: Microsoft Teams でのカードテキストの書式設定について説明します。
keywords: teams の bot カード形式
ms.date: 03/29/2018
ms.openlocfilehash: 944e6a69c68d284b3a7309063587bd4b75319bc7
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587812"
---
# <a name="format-cards-in-teams"></a>Teams の書式設定カード

カードの種類に応じて、Markdown または HTML のどちらかを使用して、リッチテキスト形式をカードに追加できます。

カードは、title または副題のプロパティではなく、text プロパティのみの書式設定をサポートしています。 書式は、カードの種類に応じて、XML (HTML) 形式のサブセットまたは Markdown を使用して指定できます。 Markdown の書式設定を使用して、現在および今後の開発用のアダプティブカード用にお勧めします。

カードの種類に応じて書式設定のサポートが異なります。また、カードのレンダリングはデスクトップとモバイルチームの両方のクライアントとデスクトップブラウザーの Teams で少しずつ異なります。

任意の Teams カードを含むインライン画像を含めることができます。 画像は、、またはのファイルとして書式設定さ `.png` `.jpg` れ、 `.gif` 1024 × 1024 px または 1 MB を超えることはできません。 アニメーション GIF は正式にはサポートされていません。 *See* [カードリファレンス](./cards-reference.md#inline-card-images)を参照

## <a name="formatting-cards-with-markdown"></a>Markdown を使用したカードの書式設定

Teams で Markdown をサポートするカードには、次の2つの種類があります。

> [!div class="checklist"]
> * **アダプティブカード**: Markdown は、およびと同様に、アダプティブカードフィールドでサポートされています `Textblock` `Fact.Title` `Fact.Value` 。 HTML は、アダプティブカードではサポートされていません。
> * **O365 コネクタカード**: Markdown および制限付き HTML は、テキストフィールドの Office 365 コネクタカードでサポートされています。

# <a name="markdown-formatting-adaptive-cards"></a>[**Markdown の書式設定: アダプティブカード**](#tab/adaptive-md)

 とでサポートされているスタイル `Textblock` `Fact.Title` は、次のとおりです `Fact.Value` 。

| Style | 例 | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| 順序なしリスト | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 順序付きリスト | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[Bing](https://www.bing.com/)| ```[Title](url)``` |

次の Markdown タグはサポートされていません。

* ヘッダー
* テーブル
* 画像
* 書式設定済みのテキスト
* Blockquotes

> [!IMPORTANT]
> アダプティブカードは、HTML 形式をサポートしていません。

### <a name="newlines-for-adaptive-cards"></a>アダプティブカードの改行

リストで `\r` は、または `\n` エスケープシーケンスを使用して改行することができます。 `\n\n`リストでを使用すると、リスト内の次の要素がインデントされます。 Textblock の他の場所に改行が必要な場合は、を使用 `\n\n` します。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>アダプティブカードのモバイルとデスクトップの違い

デスクトップとモバイルバージョンの Teams では、書式設定が若干異なります。

デスクトップでは、アダプティブカードの Markdown 書式は、web ブラウザーと Teams クライアントアプリケーションの両方で次のように表示されます。

![デスクトップクライアントでのアダプティブカード Markdown の書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

IOS では、アダプティブカード Markdown 形式は次のように表示されます。

![IOS のアダプティブカード Markdown 形式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

Android では、アダプティブカードの Markdown 書式は次のように表示されます。

![Android のアダプティブカード Markdown 形式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>アダプティブカードの詳細情報

[アダプティブカードのテキスト機能](/adaptive-cards/create/textfeatures)このトピックで説明する日付とローカリゼーションの機能は、Teams ではサポートされていません。

### <a name="formatting-sample-for-adaptive-cards"></a>アダプティブカード用の書式設定のサンプル

``` json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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
            "text": "Check out [Adaptive Cards](http://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a>アダプティブカード v2.0 でのサポートを説明します。

カードベースのメンションは、Web、デスクトップ、モバイルクライアントでサポートされています。 ボットおよびメッセージング拡張機能の応答には、アダプティブカードの本文内に @ メンションを追加することができます。  カードに @ メンションを追加するには、同じ通知ロジックに従って、[チャネルおよびグループチャットの会話に](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions )あるメッセージに基づいたものとしてレンダリングします。

ボットおよびメッセージング拡張機能には、 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html)および[FactSet](https://adaptivecards.io/explorer/FactSet.html)要素のカードコンテンツ内のメンションを含めることができます。

> [!NOTE]
> * [Media 要素](https://adaptivecards.io/explorer/Media.html)は、現在 Teams プラットフォームのアダプティブカード v2.0 ではサポートされていません。
> * チャネル & チームメンションは bot メッセージではサポートされていません。

### <a name="constructing-mentions"></a>メンションの構築

アダプティブカードにメンションを含めるには、アプリに次の要素を含める必要があります。

* `<at>username</at>`サポートされているアダプティブカード要素
* `mention`カードコンテンツ内のプロパティの内部にあるオブジェクト。このオブジェクトは、 `msteams` 説明されているユーザーの Teams ユーザー id を含みます。

### <a name="sample-adaptive-card-with-a-mention"></a>アダプティブカードのサンプル

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
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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

# <a name="markdown-formatting-o365-connector-cards"></a>[**Markdown の形式: O365 コネクタカード**](#tab/connector-md)

コネクタカードは、制限付きの Markdown および HTML 形式をサポートしています。 HTML サポートについては、前のセクションで説明します。

| Style | 例 | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| ヘッダー (レベル 1 &ndash; 3) | **テキスト** | `### Text`|
| 打ち消し | ~~text~~ | `~~text~~` |
| 順序なしリスト | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 順序付きリスト | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 書式設定済みのテキスト | `text` | ``preformatted text`` |
| blockquote | >blockquote テキスト | `>blockquote text` |
| hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 画像リンク |![岩に関するアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

コネクタカードでは、改行はに対してレンダリングされますが、では表示され `\n\n` ません `\n` `\r` 。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Markdown を使用したコネクタカードのモバイルとデスクトップの相違点

デスクトップでは、Markdown のコネクタカードの書式は、次のようになります。

![デスクトップクライアントでのコネクタカードの Markdown の書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

IOS では、Markdown のコネクタカードの書式設定は次のようになります。

![IOS クライアントでのコネクタカードの Markdown の書式設定](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

懸案事項:

* Teams の iOS クライアントは、コネクタカードで Markdown または HTML インライン画像を表示しません。
* Blockquotes はインデント付きですが、灰色は表示されません。

Android では、Markdown のコネクタカードの書式設定は次のようになります。

![Android クライアントでのコネクタカードの Markdown の書式設定](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Markdown コネクタカードの書式設定の例

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
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
            "text": "embedded image link: ![Duck on a rock](http://aka.ms/Fo983c)"
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

## <a name="formatting-cards-with-html"></a>HTML を使用してカードを書式設定する

# <a name="html-formatting-o365-connector-cards"></a>[**HTML 形式: O365 コネクタカード**](#tab/connector-html)

コネクタカードは、制限付きの Markdown および HTML 形式をサポートしています。 Markdown については、次のセクションで説明します。

| Style | 例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| ヘッダー (レベル 1 &ndash; 3) | **テキスト** | `<h3>Text</h3>` |
| 打ち消し | ~~text~~ | `<strike>text</strike>` |
| 順序なしリスト | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 順序付きリスト | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 書式設定済みのテキスト | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

コネクタカードでは、改行はタグを使用して HTML でレンダリングされ `<p>` ます。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>HTML を使用するコネクタカードのモバイルとデスクトップの相違点

デスクトップでは、コネクタカードの HTML 書式設定は次のようになります。

![デスクトップクライアントのコネクタカードの HTML 形式](../../assets/images/cards/Connector-desktop-html-combined.png)

IOS では、HTML 形式は次のようになります。

![IOS クライアントでのコネクタカードの HTML 書式設定](../../assets/images/cards/connector-iphone-html-combined-80.png)

懸案事項:

* インライン画像は、コネクタカードで Markdown または HTML のどちらかを使用して iOS でレンダリングされることはありません。
* 書式設定済みのテキストは表示されますが、灰色の背景は表示されません。

Android では、HTML 形式は次のようになります。

![Android クライアントでのコネクタカードの HTML 書式設定](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>HTML コネクタカードの書式設定のサンプル

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
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
            "text": "embedded image <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**HTML 形式: 英雄とサムネイルカード**](#tab/simple-html)

HTML タグは、ヒーローやサムネイルカードなどの単純なカードでサポートされています。 Markdown はサポートされていません。

| Style | 例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| ヘッダー (レベル 1 &ndash; 3) | **テキスト** | `<h3>Text</h3>` |
| 打ち消し | ~~text~~ | `<strike>text</strike>` |
| 順序なしリスト | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 順序付きリスト | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 書式設定済みのテキスト | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>簡単なカードのモバイルとデスクトップの相違点

デスクトップとモバイルプラットフォームとの間には、解像度の違いがあるため、デスクトップとモバイルバージョンの Teams との間で書式設定が異なります。

デスクトップでは、HTML 形式は次のように表示されます。

![デスクトップクライアントの HTML 形式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

IOS では、HTML 形式は次のように表示されます。

![IOS クライアントでの HTML 形式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

懸案事項:

* 太字や斜体などの文字書式は、iOS では表示されません。

Android では、HTML 形式は次のように表示されます。

![Android クライアントでの HTML 形式](../../assets/images/cards/card-formatting-xml-android-60.png)

Android では、太字や斜体などの文字書式が正しく表示されます。

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>シンプルなカードにおける HTML 形式の書式設定のサンプル

これらのスクリーンショットは Teams AppStudio を使用して作成されています。これは、ヒーローカードの text プロパティが次の文字列に設定されています。 このコードを変更することにより、独自のカードで書式設定をテストできます。

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
