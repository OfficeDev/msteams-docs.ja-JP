---
title: カード内のテキストの書式設定
description: Microsoft Teamsでのカード テキストの書式設定について説明します。
keywords: チームボットカード形式
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 848656097f2c865705cc0d91dece93049d8c6790
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566584"
---
# <a name="format-cards-in-teams"></a>Teamsでカードをフォーマットする

カードの種類に応じて、マークダウンまたは HTML を使用して、リッチ テキスト形式を追加できます。

カードは、タイトルやサブタイトルのプロパティではなく、text プロパティの書式設定のみをサポートします。 フォーマットは、XML (HTML) フォーマットのサブセットを使用して指定することも、カードの種類に応じてマークダウンすることもできます。 現在および将来の開発のためにマークダウンフォーマットを使用してアダプティブカードをお勧めします。

フォーマットのサポートはカードの種類によって異なり、カードのレンダリングはデスクトップとモバイル Teamsクライアントの間で若干異なる場合があり、デスクトップ ブラウザーでTeamsします。

インライン画像は、任意のTeamsカードに含めることができます。 イメージは、 、または ファイルとしてフォーマットされ  `.png` `.jpg` `.gif` 、1024 × 1024 px または 1 MB を超えてはなりません。 アニメーション GIF は正式にはサポートされていません。 詳細については、 [カードリファレンス](./cards-reference.md#inline-card-images)を参照してください。

## <a name="formatting-cards-with-markdown"></a>マークダウンを使用したカードのフォーマット

Teamsでマークダウンをサポートするカードタイプは2つあります。

> [!div class="checklist"]
> * **アダプティブカード**: マークダウンはアダプティブカード `Textblock` フィールドおよび `Fact.Title` `Fact.Value` . アダプティブ カードでは、HTML はサポートされていません。
> * **O365 コネクタ カード**: マークダウンと制限付き HTML は、テキスト フィールドのコネクタ カードOffice 365でサポートされています。

# <a name="markdown-formatting-adaptive-cards"></a>[**マークダウンのフォーマット: アダプティブカード**](#tab/adaptive-md)

 でサポートされているスタイル `Textblock` `Fact.Title` は `Fact.Value` 、次のとおりです。

| Style | 例 | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| 順序なしリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 順序付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[Bing](https://www.bing.com/)| ```[Title](url)``` |

次のマークダウン タグはサポートされていません。

* ヘッダー
* テーブル
* 画像
* 書式設定済みのテキスト
* ブロッククォート

> [!IMPORTANT]
> アダプティブ カードは HTML 形式をサポートしていません。

### <a name="newlines-for-adaptive-cards"></a>アダプティブ カードの改行

リストでは、改行に対して、 `\r` または `\n` エスケープ シーケンスを使用できます。 `\n\n`リスト内で使用すると、リスト内の次の要素がインデントされます。 テキストブロック内の他の場所に改行が必要な場合は、 `\n\n` を使用します。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>アダプティブカードのモバイルとデスクトップの違い

フォーマットは、デスクトップとモバイル版のTeamsの間で若干異なります。

デスクトップでは、アダプティブ カード マークダウンの書式設定は、Web ブラウザとTeams クライアント アプリケーションの両方で次のように表示されます。

![デスクトップ クライアントでのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

iOS では、アダプティブ カード マークダウンの書式設定は次のように表示されます。

![iOS でのアダプティブ カード マークダウンの書式設定](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

Android では、アダプティブ カード マークダウンの書式設定は次のように表示されます。

![アンドロイドでアダプティブカードマークダウンフォーマット](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>アダプティブカードの詳細

[アダプティブ カードのテキスト機能](/adaptive-cards/create/textfeatures)このトピックで説明する日付およびローカライズ機能は、Teamsではサポートされていません。

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

### <a name="mention-support-within-adaptive-cards-v12"></a>アダプティブカードv1.2内でのサポートについて言及

カードベースのメンションは、ウェブ、デスクトップ、モバイルクライアントでサポートされています。 ボットおよびメッセージング拡張機能の応答に対して、アダプティブ カード本体内に @ メンションを追加できます。 カードに @ メンションを追加するには、 [チャネルやグループチャットの会話で](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)メッセージベースのメンションと同じ通知ロジックとレンダリングを実行します。

ボットとメッセージング拡張機能には [、TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 要素と [FactSet](https://adaptivecards.io/explorer/FactSet.html) 要素のカード コンテンツ内にメンションを含めることができます。

> [!NOTE]
> * [メディア要素](https://adaptivecards.io/explorer/Media.html)は、現在、Teamsプラットフォームのアダプティブ カード v1.2 ではサポートされていません。
> * チャンネル & チームのメンションは、ボット メッセージではサポートされていません。

#### <a name="constructing-mentions"></a>メンションの構築

アダプティブ カードにメンションを含めるには、アプリに次の要素を含める必要があります。

* `<at>username</at>` サポートされているアダプティブ カード要素で
* `mention` `msteams` カード Teams コンテンツ内のプロパティ内のオブジェクト。
* `userId`は、ボット ID と特定のユーザーに固有です。 特定のユーザーを@mentionするために使用できます。 `userId`ユーザー ID の[取得](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)に記載されているオプションの 1 つを使用して取得できます。

#### <a name="sample-adaptive-card-with-a-mention"></a>言及付きのサンプルアダプティブカード

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

### <a name="information-masking-in-adaptive-cards"></a>アダプティブカードでの情報マスキング
情報マスク プロパティを使用して、Adaptive カード入力要素内のユーザーからのパスワードや機密情報などの特定の情報をマスク [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) します。 

> [!NOTE]
> この機能はクライアント側の情報マスキングのみをサポートし、マスクされた入力テキストは [、ボットの設定](../../build-your-first-app/build-bot.md)中に指定された https エンドポイントアドレスにクリアテキストで送信されます。 

> [!NOTE]
> 情報マスク プロパティは、現在、開発者プレビューでのみ使用できます。

アダプティブ カードの情報をマスクするには、プロパティを `isMasked` **type** `Input.Text` に追加し、その値を *true* に設定します。

#### <a name="sample-adaptive-card-with-masking-property"></a>マスク プロパティを使用したサンプル アダプティブ カード

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

次の図は、アダプティブ カードのマスキング情報の例です。

![マスキング情報画像](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>全幅アダプティブカード
`msteams`このプロパティを使用して、アダプティブ カードの幅を広げ、追加のキャンバススペースを利用できます。 プロパティの使用方法については、次の例を参照してください。

#### <a name="constructing-full-width-cards"></a>全幅カードの作成
全幅アダプティブ カードを作成するには、 `width` `msteams` カード コンテンツのオブジェクトのプロパティを に設定する必要があります `Full` 。
また、アプリには次の要素を含める必要があります。

#### <a name="sample-adaptive-card-with-full-width"></a>全幅のサンプルアダプティブカード

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

全幅アダプティブ カードは次のように表示されます。 ![](../../assets/images/cards/full-width-adaptive-card.png)

プロパティを `width` *[完全]* に設定していない場合、アダプティブ カードの既定のビューは次のようになります。 ![](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>タイプ先行サポート

schema [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) 要素内で、ユーザーにフィルター処理を依頼し、多数の選択肢を選択すると、タスクの完了が大幅に遅くなる可能性があります。 アダプティブカード内での Typeahead サポートは、ユーザーが入力を入力する際に入力選択肢のセットを絞り込んだりフィルタリングしたりすることで、入力の選択を簡素化できます。 

#### <a name="enable-typeahead-in-adaptive-cards"></a>アダプティブ カードでの入力を有効にする

に設定されている typeahead を有効に `Input.Choiceset` `style` `filtered` し、確実 `isMultiSelect` に `false` に設定するには 

#### <a name="sample-adaptive-card-with-typeahead-support"></a>タイプ先行サポートを備えたサンプルアダプティブカード

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>アダプティブカード内の画像のステージビュー

> [!NOTE]
> この機能は、現在、開発者プレビューでのみ使用できます。
 
Adaptive カードでは、このプロパティを使用 `msteams` して、ステージ ビューでイメージを選択的に表示する機能を追加できます。 ユーザーが画像の上にマウスを置くと、展開アイコンが表示され、属性 `allowExpand` が に設定されます `true` 。 プロパティの使用方法については、次の例を参照してください。

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

ユーザーが画像の上にマウスを移動すると、画像の右上隅に展開アイコンが表示されます: ![ 展開可能な画像を持つアダプティブ カード](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

ユーザーが展開ボタンを選択すると、画像がステージビューに表示されます: ![ 画像はステージビューに展開されます。](../../assets/images/cards/adaptivecard-expand-image.png)

ステージビューでは、ユーザーは画像を拡大表示したりズームアウトしたりできます。 アダプティブ カード内の画像にこの機能を適用する必要がある画像を選択できます。

> [!NOTE]
> 拡大/縮小機能は、アダプティブ カードのイメージ エレメント(イメージ タイプ)にのみ適用されます。

> [!NOTE]
> Teamsモバイルアプリでは、アダプティブカードの画像のステージビュー機能はデフォルトで利用可能であり、ユーザーはアトリビュートが存在するかどうかに関係なく、画像をタップするだけで、ステージビューでアダプティブカード画像を表示できます `allowExpand` 。

# <a name="markdown-formatting-o365-connector-cards"></a>[**マークダウンのフォーマット: O365 コネクタ カード**](#tab/connector-md)

コネクタ カードは、限定的なマークダウンおよび HTML 形式をサポートします。 HTML サポートについては、最後のセクションで説明します。

| Style | 例 | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `### Text`|
| 取り消し線 | ~~text~~ | `~~text~~` |
| 順序なしリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 順序付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 書式設定済みのテキスト | `text` | ``preformatted text`` |
| blockquote | >ブロッククォートテキスト | `>blockquote text` |
| hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 画像リンク |![岩の上のアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

コネクタ カードでは、改行線は に対してレンダリング `\n\n` されますが、 または にはレンダリングされません `\n` `\r` 。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>マークダウンを使用したコネクタカードのモバイルとデスクトップの違い

デスクトップでは、コネクタ カードのマークダウンの書式は次のようになります。

![デスクトップ クライアントのコネクタ カードのマークダウンの書式設定](../../assets/images/cards/connector-desktop-markdown-combined.png)

iOS では、コネクタ カードのマークダウンの書式は次のようになります。

![iOS クライアントのコネクタ カードのマークダウン形式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

懸案事項:

* Teams用の iOS クライアントは、コネクタ カードにマークダウンまたは HTML インライン イメージをレンダリングしません。
* ブロック引用符はインデントとしてレンダリングされますが、背景はグレーで表示されません。

Android では、コネクタ カードのマークダウンの書式設定は次のようになります。

![Android クライアントのコネクタ カードのマークダウン形式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>マークダウン コネクタ カードの書式設定例

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

# <a name="html-formatting-o365-connector-cards"></a>[**HTML 形式: O365 コネクタ カード**](#tab/connector-html)

コネクタ カードは、限定的なマークダウンおよび HTML 形式をサポートします。 マークダウンについては、次のセクションで説明します。

| Style | 例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| 取り消し線 | ~~text~~ | `<strike>text</strike>` |
| 順序なしリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 順序付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 書式設定済みのテキスト | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>テキスト</blockquote> | `<blockquote>text</blockquote>` |
| hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

コネクタ カードでは、タグを使用して改行が HTML でレンダリングされます `<p>` 。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>HTML を使用するコネクタ カードのモバイルとデスクトップの違い

デスクトップでは、コネクタ カードの HTML 形式は次のようになります。

![デスクトップ クライアントのコネクタ カードの HTML 形式](../../assets/images/cards/Connector-desktop-html-combined.png)

iOS では、HTML 形式は次のようになります。

![iOS クライアントのコネクタ カードの HTML 形式](../../assets/images/cards/connector-iphone-html-combined-80.png)

懸案事項:

* インライン イメージは、コネクタ カードでマークダウンまたは HTML を使用して iOS ではレンダリングされません。
* 書式設定済みのテキストはレンダリングされますが、背景は灰色ではありません。

Android では、HTML 形式は次のようになります。

![Android クライアントのコネクタ カードの HTML 形式](../../assets/images/cards/connector-android-html-combined.png)

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**HTML フォーマット: ヒーローカードとサムネイルカード**](#tab/simple-html)

HTML タグは、ヒーロー カードやサムネイル カードなどの単純なカードでサポートされています。 マークダウンはサポートされていません。

| Style | 例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `<h3>Text</h3>` |
| 取り消し線 | ~~text~~ | `<strike>text</strike>` |
| 順序なしリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 順序付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 書式設定済みのテキスト | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>テキスト</blockquote> | `<blockquote>text</blockquote>` |
| hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>シンプルカードのモバイルとデスクトップの違い

デスクトッププラットフォームとモバイルプラットフォームの解像度が異なるため、フォーマットはデスクトップバージョンとモバイル版のTeamsの間で異なります。

デスクトップでは、HTML 形式は次のように表示されます。

![デスクトップ クライアントでの HTML 形式の書式設定](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

iOS では、HTML 形式は次のように表示されます。

![iOS クライアントでの HTML フォーマット](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

懸案事項:

* 太字や斜体などの文字書式は iOS ではレンダリングされません。

Android では、HTML 形式は次のように表示されます。

![アンドロイドクライアントでのHTMLフォーマット](../../assets/images/cards/card-formatting-xml-android-60.png)

太字や斜体などの文字書式は、Android 上で正しく表示されます。

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>シンプルカードでの HTML フォーマットのサンプルの書式設定

これらのスクリーンショットは、hero カードの text プロパティが次の文字列に設定されている AppStudio Teams使用して作成されました。 このコードを変更することで、独自のカードで書式設定をテストできます。

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
