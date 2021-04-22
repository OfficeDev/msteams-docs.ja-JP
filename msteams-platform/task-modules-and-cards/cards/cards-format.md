---
title: カード内のテキストの書式設定
description: Microsoft Teams のカード テキストの書式設定について説明します。
keywords: teams ボット カードの形式
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: b50109ad664bda2fc130e08c53dd7fca2a3d54ef
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922518"
---
# <a name="format-cards-in-teams"></a>Teams でカードを書式設定する

カードの種類に応じて、Markdown または HTML を使用してリッチ テキスト書式をカードに追加できます。

カードは、タイトルプロパティや字幕プロパティではなく、text プロパティでのみ書式設定をサポートします。 書式設定は、カードの種類に応じて XML (HTML) 書式のサブセットまたは Markdown を使用して指定できます。 現在および将来の開発では、Markdown 書式設定を使用したアダプティブ カードをお勧めします。

書式設定のサポートはカードの種類によって異なりますが、カードのレンダリングはデスクトップとモバイル Teams クライアント、およびデスクトップ ブラウザーの Teams で若干異なる場合があります。

任意の Teams カードにインライン イメージを含めできます。 イメージは、、、またはファイルとして書式設定され  `.png` `.jpg` `.gif` 、1024 px または 1 MB を超え×する必要があります。 アニメーション GIF は公式にはサポートされていません。 *「カード*[リファレンス」を参照してください。](./cards-reference.md#inline-card-images)

## <a name="formatting-cards-with-markdown"></a>Markdown を使用したカードの書式設定

Teams で Markdown をサポートするカードの種類は次の 2 種類です。

> [!div class="checklist"]
> * **アダプティブ カード**: Markdown はアダプティブ カード フィールドおよび . `Textblock` `Fact.Title` `Fact.Value` アダプティブ カードでは HTML はサポートされていません。
> * **O365 コネクタ カード**: マークダウンと制限付き HTML は、テキスト フィールドOffice 365 コネクタ カードでサポートされます。

# <a name="markdown-formatting-adaptive-cards"></a>[**Markdown の書式設定: アダプティブ カード**](#tab/adaptive-md)

 サポートされているスタイルは `Textblock` 、次 `Fact.Title` `Fact.Value` のとおりです。

| Style | 例 | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| 順序なしリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 順序付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[Bing](https://www.bing.com/)| ```[Title](url)``` |

次の Markdown タグはサポートされていません。

* ヘッダー
* テーブル
* 画像
* 書式設定済みのテキスト
* Blockquotes

> [!IMPORTANT]
> アダプティブ カードは HTML の書式設定をサポートしていない。

### <a name="newlines-for-adaptive-cards"></a>アダプティブ カードの改行

リストでは、改行に対 `\r` してエスケープ シーケンス `\n` またはエスケープ シーケンスを使用できます。 リスト `\n\n` で使用すると、リスト内の次の要素がインデントされます。 テキスト ブロック内の他の場所に改行が必要な場合は、 を使用します `\n\n` 。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>アダプティブ カードのモバイルとデスクトップの違い

書式設定は、デスクトップとモバイル バージョンの Teams では少し異なります。

デスクトップでは、アダプティブ カードの Markdown 書式は、Web ブラウザーと Teams クライアント アプリケーションの両方で次のように表示されます。

![デスクトップ クライアントでのアダプティブ カードマークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

iOS では、アダプティブ カードのマークダウンの書式設定は次のように表示されます。

![iOS でのアダプティブ カードマークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

Android では、アダプティブ カード マークダウンの書式設定は次のように表示されます。

![Android のアダプティブ カード Markdown 書式設定](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>アダプティブ カードの詳細

[アダプティブ カードのテキスト機能](/adaptive-cards/create/textfeatures) このトピックで説明されている日付とローカライズ機能は、Teams ではサポートされていません。

### <a name="formatting-sample-for-adaptive-cards"></a>アダプティブ カードの書式設定サンプル

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

カード ベースのメンションは、Web、デスクトップ、モバイル クライアントでサポートされています。 ボットおよびメッセージング拡張機能の応答に対して、アダプティブ カード本文内に @ メンションを追加できます。 カードに @ メンションを追加するには、チャネルとグループ チャットの会話でメッセージ ベースのメンションと同じ通知ロジックとレンダリングに [従います](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)。

ボットとメッセージング拡張機能には [、TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 要素と FactSet 要素のカード コンテンツ内にメンション [を含](https://adaptivecards.io/explorer/FactSet.html) めることはできません。

> [!NOTE]
> * [メディア要素](https://adaptivecards.io/explorer/Media.html) は、Teams プラットフォームのアダプティブ カード v1.2 では現在サポートされていません。
> * チャネル &チームのメンションはボット メッセージではサポートされていません。

#### <a name="constructing-mentions"></a>メンションの作成

アダプティブ カードにメンションを含めるには、アプリに次の要素を含める必要があります。

* `<at>username</at>` は、サポートされているアダプティブ カード要素に含まれます。
* カード コンテンツ内のプロパティ内のオブジェクト 。このオブジェクトには、言及されているユーザーの Teams ユーザー `mention` `msteams` ID が含まれます。
* これは `userId` 、ボット ID と特定のユーザーに固有です。 特定のユーザーを@mention使用できます。 ユーザー `userId` ID の取得に記載されているオプションのいずれかを使用して [取得できます](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)。

#### <a name="sample-adaptive-card-with-a-mention"></a>メンション付きアダプティブ カードのサンプル

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
> この機能はクライアント側の情報マスキングのみをサポートします。マスクされた入力テキストは、ボットの構成中に指定された https エンドポイント アドレスにクリア テキスト [として送信されます](../../build-your-first-app/build-bot.md#4-configure-your-bot)。 

> [!NOTE]
> information masking プロパティは現在、開発者プレビューでのみ使用できます。

アダプティブ カードで情報をマスクするには、型に `isMasked` プロパティを追加 **し** `Input.Text` 、その値を true に設定 *します*。

#### <a name="sample-adaptive-card-with-masking-property"></a>マスキング プロパティを持つアダプティブ カードのサンプル

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

次の図は、アダプティブ カードのマスキング情報の例です。

![マスキング情報イメージ](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>全幅アダプティブ カード
このプロパティを使用 `msteams` すると、アダプティブ カードの幅を拡大し、追加のキャンバス領域を利用できます。 プロパティの使用方法については、次の例を参照してください。

#### <a name="constructing-full-width-cards"></a>全幅カードの作成
全幅アダプティブ カードを作成するには、 `width` カード コンテンツのプロパティのオブジェクトをに `msteams` 設定する必要があります `Full` 。
さらに、アプリには次の要素が含まれる必要があります。

#### <a name="sample-adaptive-card-with-full-width"></a>全幅のアダプティブ カードのサンプル

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

全幅アダプティブ カードは、次のように表示されます。 ![ 全幅アダプティブ カード ビュー](../../assets/images/cards/full-width-adaptive-card.png)

プロパティを Full に設定していない場合、アダプティブ カードの既定のビューは次のとおりです。小幅アダプティブ カード `width`  ![ ビュー](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Typeahead のサポート

schema 要素内で、ユーザーにフィルター処理を求め、多数の選択肢を選択すると、タスクの完了が大幅 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) に遅くなる可能性があります。 アダプティブ カード内の Typeahead サポートは、ユーザーが入力を入力する場合に入力の選択肢のセットを絞り込むかフィルター処理することで、入力の選択を簡略化できます。 

#### <a name="enable-typeahead-in-adaptive-cards"></a>アダプティブ カードで typeahead を有効にする

セット内で typeahead を有効 `Input.Choiceset` にし `style` 、 `filtered` 必ずに `isMultiSelect` に設定します `false` 。 

#### <a name="sample-adaptive-card-with-typeahead-support"></a>typeahead サポートを備えるアダプティブ カードのサンプル

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

> [!NOTE]
> この機能は現在、開発者プレビューでのみ利用できます。
 
アダプティブ カードでは、このプロパティを使用して、ステージ ビューに画像を選択的 `msteams` に表示する機能を追加できます。 ユーザーが画像にカーソルを合わせると、展開アイコンが表示され、属性が `allowExpand` に設定されます `true` 。 プロパティの使用方法については、次の例を参照してください。

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

ユーザーが画像の上にマウス ポインターを置くと、画像の右上隅に展開アイコンが表示されます。展開可能なイメージを持つ ![ アダプティブ カード](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

ユーザーが展開ボタンを選択すると、イメージがステージ ビューに表示されます。 ![ イメージはステージ ビューに展開されます。](../../assets/images/cards/adaptivecard-expand-image.png)

ステージ ビューでは、ユーザーは画像を拡大および縮小できます。 アダプティブ カードでこの機能を使用する必要があるイメージを選択できます。

> [!NOTE]
> 拡大および縮小機能は、アダプティブ カード内のイメージ要素 (画像の種類) にのみ適用されます。

> [!NOTE]
> Teams モバイル アプリの場合、アダプティブ カードの画像のステージ ビュー機能は既定で利用できます。ユーザーは、属性が存在するかどうかに関係なく、画像をタップするだけでステージ ビューでアダプティブ カードイメージを表示できます。 `allowExpand`

# <a name="markdown-formatting-o365-connector-cards"></a>[**Markdown の書式設定: O365 コネクタ カード**](#tab/connector-md)

コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。 HTML サポートについては、最後のセクションで説明します。

| Style | 例 | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `### Text`|
| 取り消し線 | ~~text~~ | `~~text~~` |
| 順序なしリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 順序付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 事前に書式設定されたテキスト | `text` | ``preformatted text`` |
| blockquote | >をブロッククォートする | `>blockquote text` |
| hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 画像リンク |![岩の上のアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

コネクタ カードでは、改行はのためにレンダリングされますが `\n\n` 、for または `\n` `\r` .

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>Markdown を使用したコネクタ カードのモバイルとデスクトップの違い

デスクトップでは、コネクタ カードの Markdown 書式は次のように表示されます。

![デスクトップ クライアントでのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

iOS では、コネクタ カードの Markdown 書式は次のように表示されます。

![iOS クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

懸案事項:

* Teams の iOS クライアントは、コネクタ カードで Markdown または HTML インライン イメージをレンダリングしない。
* ブロッククォートはインデントされますが、灰色の背景なしでレンダリングされます。

Android では、コネクタ カードの Markdown 書式は次のように表示されます。

![Android クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Markdown コネクタ カードの書式設定の例

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

## <a name="formatting-cards-with-html"></a>HTML を使用したカードの書式設定

# <a name="html-formatting-o365-connector-cards"></a>[**HTML の書式設定: O365 コネクタ カード**](#tab/connector-html)

コネクタ カードでは、マークダウンと HTML の書式設定が制限されています。 マークダウンについては、次のセクションで説明します。

| Style | 例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| 取り消し線 | ~~text~~ | `<strike>text</strike>` |
| 順序なしリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 順序付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 事前に書式設定されたテキスト | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>テキスト</blockquote> | `<blockquote>text</blockquote>` |
| hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

コネクタ カードでは、タグを使用して改行が HTML でレンダリング `<p>` されます。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>HTML を使用したコネクタ カードのモバイルとデスクトップの違い

デスクトップでは、コネクタ カードの HTML 書式は次のように表示されます。

![デスクトップ クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/Connector-desktop-html-combined.png)

iOS では、HTML の書式設定は次のように表示されます。

![iOS クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-iphone-html-combined-80.png)

懸案事項:

* インライン イメージは、コネクタ カードの Markdown または HTML を使用して iOS ではレンダリングされません。
* 書式設定済みのテキストはレンダリングされますが、背景が灰色ではありません。

Android では、HTML の書式設定は次のように表示されます。

![Android クライアントのコネクタ カードの HTML 書式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>HTML コネクタ カードの書式設定サンプル

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**HTML の書式設定: ヒーローカードとサムネイル カード**](#tab/simple-html)

HTML タグは、ヒーロー カードやサムネイル カードなどの単純なカードでサポートされています。 Markdown はサポートされていません。

| Style | 例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| 取り消し線 | ~~text~~ | `<strike>text</strike>` |
| 順序なしリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 順序付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 事前に書式設定されたテキスト | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>テキスト</blockquote> | `<blockquote>text</blockquote>` |
| hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>単純なカードのモバイルとデスクトップの違い

デスクトップ プラットフォームとモバイル プラットフォームの解像度の違いにより、デスクトップとモバイル バージョンの Teams では書式設定が異なります。

デスクトップでは、HTML の書式設定は次のように表示されます。

![デスクトップ クライアントの HTML 書式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

iOS では、HTML 書式は次のように表示されます。

![iOS クライアントの HTML 書式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

懸案事項:

* 太字や斜体のような文字の書式設定は、iOS ではレンダリングされません。

Android では、HTML の書式設定は次のように表示されます。

![Android クライアントでの HTML 書式](../../assets/images/cards/card-formatting-xml-android-60.png)

Android では太字や斜体のような文字の書式設定が正しく表示されます。

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>単純なカードの HTML 書式の書式設定サンプル

これらのスクリーンショットは Teams AppStudio を使用して作成され、ヒーロー カードの text プロパティは次の文字列に設定されています。 このコードを変更することで、独自のカードの書式設定をテストできます。

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
