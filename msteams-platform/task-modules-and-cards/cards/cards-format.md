---
title: カード内のテキストの書式設定
description: このモジュールでは、Microsoft Teams でのカード テキストの書式設定と、マークダウンを使用したカードの書式設定について説明します。
ms.localizationpriority: high
ms.topic: reference
ms.date: 06/25/2021
ms.openlocfilehash: e6cbccdb436b8d84f5d139b6a082765f22f373c6
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586960"
---
# <a name="format-cards-in-microsoft-teams"></a>Microsoft Teams のカードの書式設定

カードにリッチ テキストの書式設定を追加する 2 つの方法を次に示します。

* [markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

カードは、タイトル プロパティや字幕プロパティではなく、テキスト プロパティでのみ書式設定をサポートします。 カードの種類に応じて、XML または HTML のサブセット、または Markdown を使用して書式設定を指定できます。 アダプティブ カードの現在および将来の開発では、Markdown の書式設定をお勧めします。

書式設定のサポートはカードの種類によって異なります。カードのレンダリングは、デスクトップとモバイルの Microsoft Teams クライアント間、およびデスクトップ ブラウザーの Teams 間でわずかに異なる場合があります。

Teams カードにはインライン画像を含めることができます。 サポートされているイメージ形式は、.png、.jpg、または .gif 形式です。 サイズは 1024 x 1024 ピクセル以内、ファイル サイズは 1 MB 未満にしてください。 アニメーション .gif 画像はサポートされていません。 詳細については、「[カードの種類](./cards-reference.md#inline-card-images)」を参照してください。

サポートされている特定のスタイルを含む Markdown を使用して、アダプティブカードと Office 365 コネクタ カードを書式設定できます。  

## <a name="format-cards-with-markdown"></a>Markdown でカードを書式設定する

次のカードタイプは、Teams での Markdown 書式設定をサポートしています。

* アダプティブ カード: Markdown は、アダプティブ カード `Textblock` フィールド、および `Fact.Title` と `Fact.Value` でサポートされています。 HTML はアダプティブ カードではサポートされていません。
* Office 365 コネクタ カード: Markdown と制限付き HTML は、テキスト フィールドの Office 365 コネクタ カードでサポートされています。

リスト内の改行に `\r` または `\n` エスケープ シーケンスを使用して、アダプティブ カードに改行を使用できます。 書式設定は、デスクトップ版とモバイル版の アダプティブ カード用 Teams で異なります。 カード ベースのメンションは、Web、デスクトップ、およびモバイル クライアントでサポートされています。 情報マスキングプロパティを使用して、アダプティブ カード `Input.Text` 入力要素内のユーザーからのパスワードや機密情報などの特定の情報をマスクできます。 `width` オブジェクトを使用して、アダプティブ カードの幅を拡張できます。 アダプティブ カード内で先行入力サポートを有効にし、ユーザーが入力を入力するときに入力選択肢のセットをフィルタリングできます。 `msteams` プロパティを使用して、ステージ ビューで画像を選択的に表示する機能を追加できます。

書式設定は、アダプティブ カードおよびコネクタ カード用の Teams のデスクトップ バージョンとモバイル バージョンで異なります。 このセクションでは、アダプティブ カードとコネクタ カードの Markdown 書式の例を紹介します。

# <a name="markdown-format-for-adaptive-cards"></a>[アダプティブ カードの Markdown 書式](#tab/adaptive-md)

 次の表に、`Textblock`、`Fact.Title`、および `Fact.Value` でサポートされているスタイルを示します。

| Style | 例 | Markdown |
| --- | --- | --- |
| 太字 | **Bold** | ```**Bold**``` |
| 斜体 | _Italic_ | ```_Italic_``` |
| 記号付きリスト | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 番号付きリスト | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[Bing](https://www.bing.com/)| ```[Title](url)``` |

次の Markdown タグはサポートされていません。

* ヘッダー
* テーブル
* 画像
* 事前書式設定済みのテキスト
* Blockquotes

### <a name="newlines-for-adaptive-cards"></a>アダプティブ カードの改行

リスト内の改行には、`\r` または `\n` のエスケープ シーケンスを使用できます。 リストで `\n\n` を使用すると、リスト内の次の要素がインデントされます。 TextBlock の他の場所で改行が必要な場合は、`\n\n` を使用してください。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>アダプティブ カードのモバイルとデスクトップの違い

デスクトップでは、アダプティブ カードの Markdown 書式設定は、Web ブラウザーと Teams クライアント アプリケーションの両方で次の画像のように表示されます。

:::image type="content" source="../../assets/images/Cards/Adaptive-markdown-desktop-client.png" alt-text="アダプティブ markdown デスクトップ クライアント":::

iOS では、アダプティブ カード Markdown の書式設定が次の図のように表示されます。

:::image type="content" source="../../assets/images/Cards/Adaptive-markdown-iOS-75.png" alt-text="iOS でのアダプティブ カード Markdown の書式設定":::

Android では、アダプティブ カード Markdown の書式設定が次の図のように表示されます。

:::image type="content" source="../../assets/images/Cards/Adaptive-markdown-Android.png" alt-text="Android でのアダプティブ カード Markdown の書式設定":::

詳細については、[「アダプティブ カード」のテキスト機能](/adaptive-cards/create/textfeatures)を参照してください。

> [!NOTE]
> このセクションに記載されている日付とローカリゼーション機能は、Teams ではサポートされていません。

### <a name="adaptive-cards-format-sample"></a>アダプティブ カード書式のサンプル

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

アダプティブ カードは、絵文字をサポートします。次のコードは、絵文字を使用したアダプティブ カードの例を示しています。

``` json
{ "$schema": "http://adaptivecards.io/schemas/adaptive-card.json", "type": "AdaptiveCard", "version": "1.0", "body": [ { "type": "Container", "items": [ { "type": "TextBlock", "text": "Publish Adaptive Card with emojis 🥰 ", "weight": "bolder", "size": "medium" }, ] }, ], }
```

:::image type="content" source="../../assets/images/Cards/adaptive-card-emoji.png" alt-text="絵文字付きのアダプティブ カード":::

### <a name="mention-support-within-adaptive-cards"></a>アダプティブ カード内でのサポートのメンション

ボットとメッセージ拡張機能の応答のために、アダプティブ カード本体内に @メンションを追加できます。 カードに @メンションを追加するには、[チャネルおよびグループ チャットの会話でのメッセージ ベースのメンション](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)と同じ通知ロジックとレンダリングに従います。

ボットとメッセージ拡張機能には、カード コンテンツ内の [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 要素と [FactSet](https://adaptivecards.io/explorer/FactSet.html) 要素に言及を含めることができます。

> [!NOTE]
>
> * [メディア要素](https://adaptivecards.io/explorer/Media.html)は現在、Teams プラットフォームのアダプティブ カードではサポートされていません。
> * チャネルとチームのメンションはボット メッセージではサポートされていません。

アダプティブ カードにメンションを含めるには、アプリに次の要素を含める必要があります。

* サポートされているアダプティブカード要素の `<at>username</at>`。
* カード コンテンツの `msteams` プロパティ内の `mention` オブジェクトには、言及されているユーザーの Teams ユーザー ID が含まれています。
* `userId` は、ボット ID と特定のユーザーに固有です。 特定のユーザーに @メンションするために使用できます。 `userId` は、[ユーザー ID の取得](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id) で説明されているオプションの 1 つを使用して取得できます。

#### <a name="sample-adaptive-card-with-a-mention"></a>メンション付きアダプティブ カードのサンプル

次のコードは、アダプティブ カードとメンションの例を示しています。

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

### <a name="microsoft-azure-active-directory-azure-ad-object-id-and-upn-in-user-mention"></a>Microsoft Azure Active Directory (Azure AD) ユーザー メンションにおけるオブジェクト ID と UPN

Teams プラットフォームでは、既存の言及 ID に加えて、Azure AD オブジェクト ID とユーザー原則名 (UPN) を使用してユーザーに言及することができます。 アダプティブ カードを備えたボットと受信 Webhook を備えたコネクタは、2 つのユーザー メンション ID をサポートします。

次の表に、新しくサポートされたユーザー メンション ID を示します。

|ID  | サポート機能 | 説明 | 例 |
|----------|--------|---------------|---------|
| Azure AD オブジェクト ID | ボット、コネクタ |  Azure AD ユーザーのオブジェクト ID を指定する | 49c4641c-ab91-4248-aebb-6a7de286397b |
| UPN | ボット、コネクタ | Azure AD ユーザーの UPN | john.smith@microsoft.com |

#### <a name="user-mention-in-bots-with-adaptive-cards"></a>アダプティブ カードを使用したボットでのユーザー メンション

ボットは、既存の ID に加えて、Azure AD オブジェクト ID と UPN を使用したユーザーのメンションをサポートします。 2 つの新しい ID のサポートは、テキスト メッセージ、アダプティブ カード本体、およびメッセージ拡張応答のボットで利用できます。 ボットは、会話および `invoke` シナリオでの言及 ID をサポートします。 ユーザーは、ID で @メンションされると、アクティビティ フィード通知を受け取ります。

> [!NOTE]
> ボットのアダプティブ カードを使用したユーザー メンションには、スキーマの更新と UI/UX の変更は必要ありません。

##### <a name="example"></a>例

アダプティブ カードを使用するボットでのユーザー メンションの例は次のとおりです。

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.0",
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Hi <at>Adele UPN</at>, <at>Adele Azure AD</at>"
    }
  ],
  "msteams": {
    "entities": [
      {
        "type": "mention",
        "text": "<at>Adele UPN</at>",
        "mentioned": {
          "id": "AdeleV@contoso.onmicrosoft.com",
          "name": "Adele Vance"
        }
      },
      {
        "type": "mention",
        "text": "<at>Adele Azure AD</at>",
        "mentioned": {
          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
          "name": "Adele Vance"
        }
      }
    ]
  }
}
```

次の画像は、ボットのアダプティブ カードでのユーザー メンションを示しています。

:::image type="content" source="../../assets/images/authentication/user-mention-in-bot.png" alt-text="アダプティブ カードを使用したボットでのユーザー メンション":::

#### <a name="user-mention-in-incoming-webhook-with-adaptive-cards"></a>アダプティブ カードを使用した受信 Webhook でのユーザー メンション

受信 Webhook は、Azure AD オブジェクト ID と UPN を使用したアダプティブ カードでのユーザー メンションをサポートし始めます。

> [!NOTE]
>
> * 受信 Webhook のスキーマでユーザー メンションを有効にして、Azure AD オブジェクト ID と UPN をサポートします。
> * UI/UX の変更は、Azure AD オブジェクト ID および UPN を使用したユーザー メンションには必要ありません。

##### <a name="example"></a>例

受信 Webhook でのユーザー メンションの例を次に示します。

```json
{
    "type": "message",
    "attachments": [
        {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
            "type": "AdaptiveCard",
            "body": [
                {
                    "type": "TextBlock",
                    "size": "Medium",
                    "weight": "Bolder",
                    "text": "Sample Adaptive Card with User Mention"
                },
                {
                    "type": "TextBlock",
                    "text": "Hi <at>Adele UPN</at>, <at>Adele Azure AD</at>"
                }
            ],
            "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
            "version": "1.0",
            "msteams": {
                "entities": [
                    {
                        "type": "mention",
                        "text": "<at>Adele UPN</at>",
                        "mentioned": {
                          "id": "AdeleV@contoso.onmicrosoft.com",
                          "name": "Adele Vance"
                        }
                      },
                      {
                        "type": "mention",
                        "text": "<at>Adele Azure AD</at>",
                        "mentioned": {
                          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
                          "name": "Adele Vance"
                        }
                      }
                ]
            }
        }
    }]
}
```

次の図は、受信 Webhook でのユーザー メンションを示しています。

:::image type="content" source="../../assets/images/authentication/user-mention-in-incoming-webhook.png" alt-text="受信 Webhook でのユーザー メンション":::

### <a name="information-masking-in-adaptive-cards"></a>アダプティブ カードの情報マスキング

情報マスキングプロパティを使用して、アダプティブ カード [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) 入力要素内のユーザーからのパスワードや機密情報などの特定の情報をマスクします。

> [!NOTE]
> この機能は、クライアント側の情報マスキングのみをサポートします。マスキングされた入力テキストは、[ボット構成](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)中に指定された HTTPS エンドポイント アドレスにクリア テキストとして送信されます。

アダプティブ カードの情報をマスクするには、`style`プロパティを **型** `input.text` に追加し、その値を **Password** に設定します。

#### <a name="sample-adaptive-card-with-masking-property"></a>マスキング プロパティを備えたアダプティブ カードのサンプル

次のコードは、マスキング プロパティを持つアダプティブ カードの例を示しています。

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

次の画像は、アダプティブ カードのマスキング情報の例です。

:::image type="content" source="../../assets/images/Cards/masking-information-view.png" alt-text="マスキング情報ビュー":::

### <a name="full-width-adaptive-card"></a>全幅アダプティブ カード

`msteams` プロパティを使用して、アダプティブ カードの幅を拡張し、追加のキャンバス スペースを利用できます。 次のセクションでは、プロパティの使用方法について説明します。

> [!NOTE]
> モバイル パネルや会議サイド パネルなどの狭いフォーム 要素で全幅アダプティブ カードをテストし、コンテンツが切り捨てられていないことを確認します。

#### <a name="construct-full-width-cards"></a>全幅カードを作成する

全幅 アダプティブ カードを作成するには、カード コンテンツの `msteams` プロパティの `width` オブジェクトを `Full` に設定する必要があります。

#### <a name="sample-adaptive-card-with-full-width"></a>全幅 アダプティブ カードのサンプル

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

次の画像は、全幅アダプティブカードを示しています。

:::image type="content" source="../../assets/images/Cards/full-width-adaptive-card.png" alt-text="全幅アダプティブ カード ビュー":::

次の画像は、`width`プロパティを **Full** に設定していない場合のアダプティブ カードの既定ビューを示しています。

:::image type="content" source="../../assets/images/Cards/small-width-adaptive-card.png" alt-text="小幅アダプティブ カード ビュー":::

### <a name="typeahead-support"></a>先行入力のサポート

[`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) スキーマ要素内で、かなりの数の選択肢をフィルタリングして選択するようにユーザーに求めると、タスクの完了が大幅に遅くなる可能性があります。 アダプティブ カード内の先行入力サポートは、ユーザーが入力を入力するときに入力選択肢のセットを絞り込んだりフィルタリングしたりすることで、入力選択を簡素化できます。

`Input.Choiceset` 内で先行入力を有効にするには、`style` を `filtered` に設定し、`isMultiSelect` が `false` に設定されていることを確認します。

#### <a name="sample-adaptive-card-with-typeahead-support"></a>先行入力をサポートするサンプル アダプティブ カード

次のコードは、先行入力をサポートするアダプティブ カードの例を示しています。

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

アダプティブ カードでは、`msteams` プロパティを使用して、ステージ ビューで画像を選択的に表示する機能を追加できます。 ユーザーが画像にカーソルを合わせると、`allowExpand` 属性が `true` に設定されている拡張アイコンが表示されます。 プロパティの使用方法については、次の例を参照してください。

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
          }
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

ユーザーが画像にカーソルを合わせると、次の画像に示すように、右上隅に拡張アイコンが表示されます。

:::image type="content" source="../../assets/images/Cards/adaptivecard-hover-expand-icon.png" alt-text="拡張可能な画像を備えたアダプティブ カード":::

次の画像に示すように、ユーザーが拡張アイコンを選択すると、画像がステージ ビューに表示されます。

:::image type="content" source="../../assets/images/Cards/adaptivecard-expand-image.png" alt-text="ステージ ビューに拡張された画像":::

ステージ ビューでは、ユーザーは画像を拡大および縮小できます。 この機能が必要なアダプティブ カードの画像を選択できます。

> [!NOTE]
>
> * 拡大および縮小機能は、アダプティブ カードの画像の種類である画像要素にのみ適用されます。
> * Teams モバイルア プリの場合、アダプティブ カードの画像のステージ ビュー機能が既定で利用できます。 ユーザーは、`allowExpand` 属性が存在するかどうかに関係なく、画像をタップするだけでアダプティブ カードの画像をステージ ビューで表示できます。

# <a name="markdown-format-for-office-365-connector-cards"></a>[Office 365 コネクタ カードの Markdown 書式](#tab/connector-md)

コネクタ カードでは、Markdown と HTML の書式設定が制限されています。

| Style | 例 | Markdown |
| --- | --- | --- |
| 太字 | **text** | `**text**` |
| 斜体 | _text_ | `*text*` |
| ヘッダー (レベル 1&ndash;3) | **Text** | `### Text`|
| 取り消し線 | ~~text~~ | `~~text~~` |
| 記号付きリスト | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 番号付きリスト | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 事前書式設定済みのテキスト | `text` | ``preformatted text`` |
| Blockquote | >テキストを引用する | `>blockquote text` |
| Hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 画像リンク |![岩の上のアヒル](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

コネクタ カードでは、改行は `\n\n` に対してレンダリングされますが、`\n` または `\r` に対してはレンダリングされません。

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>コネクタ カードのモバイルとデスクトップの違い

デスクトップでは、次の図に示すように、コネクタ カードの Markdown 書式設定が表示されます。

:::image type="content" source="../../assets/images/Cards/connector-desktop-markdown-combined.png" alt-text="コネクタ カードの Markdown 書式設定":::

iOS では、次の図に示すように、コネクタ カードの Markdown 書式設定が表示されます。

:::image type="content" source="../../assets/images/Cards/connector-iphone-html-combined-80.png" alt-text="iOS クライアントのコネクタ カードの Markdown 書式設定":::

iOS 用 Markdown を使用するコネクタ カードには、次の問題があります。

* Teams 用の iOS クライアントは、コネクタ カードで Markdown または HTML インライン画像をレンダリングしません。
* ブロック クォートはインデントされてレンダリングされますが、背景は灰色ではありません。

Android では、次の図に示すように、コネクタ カードの Markdown の書式設定が表示されます。

:::image type="content" source="../../assets/images/Cards/connector-android-markdown-combined.png" alt-text="Android クライアントのコネクタ カードの Markdown の書式設定":::

### <a name="format-example-for-markdown-connector-cards"></a>Markdown コネクタ カードの書式の例

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

次のカード タイプは、Teams での HTML 書式設定をサポートしています。

* Office 365 コネクタ カード: 制限付き Markdown と HTML 書式設定は、Office 365 コネクタ カードでサポートされています。
* ヒーロー カードとサムネイル カード: HTML タグは、ヒーロー カードやサムネイル カードなどの簡易カードでサポートされています。

デスクトップ版とモバイル版の Teams for Office 365 コネクタ カードと簡易カードでは、書式設定が異なります。 このセクションでは、コネクタ カードと簡易カードの HTML 書式の例を参照できます。

# <a name="html-format-for-office-365-connector-cards"></a>[Office 365 コネクタ カードの HTML 書式](#tab/connector-html)

コネクタ カードでは、Markdown と HTML の書式設定が制限されています。

| Style | 例 | HTML |
| --- | --- | --- |
| 太字 | **text** | `<strong>text</strong>` |
| 斜体 | _text_ | `<em>text</em>` |
| ヘッダー (レベル 1&ndash;3) | **Text** | `<h3>Text</h3>` |
| 取り消し線 | ~~text~~ | `<strike>text</strike>` |
| 記号付きリスト | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 番号付きリスト | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 事前書式設定済みのテキスト | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

コネクタ カードでは、改行は `<p>` タグを使用して HTML でレンダリングされます。

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>コネクタ カードのモバイルとデスクトップの違い

デスクトップでは、次の画像に示すように、コネクタ カードの HTML 書式設定が表示されます。

:::image type="content" source="../../assets/images/Cards/Connector-desktop-html-combined.png" alt-text="デスクトップ クライアントのコネクタ カードの HTML 書式設定":::

iOS では、次の図に示すように HTML 書式設定が表示されます。

:::image type="content" source="../../assets/images/Cards/connector-iphone-html-combined-80.png" alt-text="iOS クライアントのコネクタ カードの HTML 書式設定":::

iOS 用 HTML を使用するコネクタ カードには、次の問題があります。

* インライン イメージは、コネクタ カードの Markdown または HTML を使用して iOS ではレンダリングされません。
* 書式設定済みのテキストはレンダリングされますが、背景が灰色ではありません。

Android では、次の図に示すように HTML 書式設定が表示されます。

:::image type="content" source="../../assets/images/Cards/connector-android-html-combined.png" alt-text="Android クライアントのコネクタ カードの HTML 書式設定":::

### <a name="format-sample-for-html-connector-cards"></a>HTML コネクタ カードの書式のサンプル

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[ヒーロー カードとサムネイル カードの HTML 書式](#tab/simple-html)

HTML タグは、ヒーロー カードやサムネイル カードなどの簡易カードでサポートされています。マークダウンはサポートされていません。

| Style | 例 | HTML |
| --- | --- | --- |
| 太字 | **text** | `<strong>text</strong>` |
| 斜体 | _text_ | `<em>text</em>` |
| ヘッダー (レベル 1&ndash;3) | **Text** | `<h3>Text</h3>` |
| 取り消し線 | ~~text~~ | `<strike>text</strike>` |
| 記号付きリスト | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 番号付きリスト | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 事前書式設定済みのテキスト | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [Bing](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>簡易カードのモバイルとデスクトップの違い

デスクトップとモバイル プラットフォームの間には解像度の違いがあるため、書式設定はデスクトップ バージョンとモバイル バージョンの Teams の間で異なります。

デスクトップでは、次の図に示すように HTML 書式設定が表示されます。

:::image type="content" source="../../assets/images/Cards/card-formatting-xml-desktop-v2.png" alt-text="デスクトップ クライアントでの HTML 書式設定":::

iOS では、次の図に示すように HTML 書式設定が表示されます。

:::image type="content" source="../../assets/images/Cards/card-formatting-xml-mobile-v2.png" alt-text="iOS クライアントの HTML 書式設定":::

太字や斜体などの文字の書式設定は、iOS ではレンダリングされません。

Android では、次の図に示すように HTML 書式設定が表示されます。

:::image type="content" source="../../assets/images/Cards/card-formatting-xml-android-60.png" alt-text="Android クライアントでの HTML 書式設定":::

Android で太字や斜体などの文字の書式設定が正しく表示されます。

### <a name="format-example-for-simple-cards"></a>簡易カードの書式の例

前のセクションの画像は、Teams **App Studio** を使用して作成されました。ここで、ヒーロー カードのテキスト プロパティは次の文字列に設定されています。

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

このコードを変更することで、独自のカードの書式設定をテストできます。

---

## <a name="see-also"></a>関連項目

* [カード アクション](./cards-actions.md)
* [ボットでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [タスク モジュール](~/task-modules-and-cards/cards/cards-format.md)
* [ボット メッセージの書式を設定する](~/bots/how-to/format-your-bot-messages.md)
* [アダプティブ カードのスキーマ エクスプローラー](https://adaptivecards.io/explorer/TextBlock.html)
