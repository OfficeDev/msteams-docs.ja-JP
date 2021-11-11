---
title: アプリのアダプティブ カードのデザイン
description: Teams のアダプティブ カードをデザインして、Microsoft Teams UI Kit を取得するする方法を説明します。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b016df98d57b9a3f5fe03e6cf26b31ad2d7b8db9
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887965"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Microsoft Teams のアプリのアダプティブ カードの設計

アダプティブ カードには、カード要素のフリーフォーム本体とオプションのアクション セットが含まれています。 アダプティブ カードは、ボットまたはメッセージングの拡張機能を介してスレッドに追加できる、アクション可能なコンテンツのスニペットです。 これらのカードは、テキスト、グラフィック、ボタンを使用して、対象ユーザーにリッチなコミュニケーションを提供します。

アダプティブ カード フレームワークは、Teams を含む多くの Microsoft 製品で使用されています。 メッセージ内のカードは、ボットまたはメッセージングの拡張機能を介してユーザーに送信できます。 ユーザーは、カードが存在する場合、カードに対してアクションを実行することもできます。

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="アダプティブ カードの概要の例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI Kit には、必要に応じて変更できる要素を含む、Teams のアダプティブ カードに関するより包括的なデザイン ガイドラインが掲載されています。 UI キットには、テーマ、アクセシビリティ、応答性の高いサイズ設定などの重要なトピックも含まれています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>アダプティブ カード デザイナー。

ブラウザーで直接アダプティブ カードのデザインを開始することもできます。

> [!div class="nextstepaction"]
> [アダプティブ カード デザイナーを試す](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>アダプティブ カードの種類

### <a name="hero"></a>ヒーロー

私たちの最大のカードです。画像がストーリーのほぼ全容を伝える記事やシナリオの共有に使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="モバイルでのアダプティブ カード ヒーロー カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="アダプティブ カードのヒーロー カードの例を示します。" border="false":::

### <a name="thumbnail"></a>サムネイル

単純な、アクション可能なメッセージを送信するために使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="モバイルでのアダプティブ カードのサムネイル カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="アダプティブ カードのサムネイル カードの例を示します。" border="false":::

### <a name="list"></a>リスト

ユーザーにリストから項目を選択してもらいたいが、項目に多くの説明は必要ないシナリオで使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="モバイルでのアダプティブ カードのリスト カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="アダプティブ カードのリスト カードの例を示します。" border="false":::

### <a name="digest"></a>Digest

ニュース ダイジェストと切り上げ投稿に使用します。 注: 単一の更新またはニュース アイテムに使用するサムネイル カードをお勧めします。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="モバイルでのアダプティブ カードのダイジェスト カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="アダプティブ カードのダイジェスト カードの例を示します。" border="false":::

### <a name="media"></a>メディア

オーディオやビデオなどのテキストとメディアを組み合わせたい場合に使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="モバイルでのアダプティブ カードのメディア カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="アダプティブ カードのメディア カードの例を示します。" border="false":::

### <a name="people"></a>連絡先

タスクに関係するユーザーを効率的に伝える場合に最適です。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="モバイルでのアダプティブ カードの連絡先カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="アダプティブ カードの連絡先カードの例を示します。" border="false":::

### <a name="request-ticket"></a>要求チケット

ユーザーから簡単な入力を取得して、タスクまたはチケットを自動的に作成するために使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="モバイルでのアダプティブ カードの要求チケット カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="アダプティブ カードの要求チケット カードの例を示します。" border="false":::

### <a name="imageset"></a>ImageSet

複数の画像サムネイルを送信するために使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="モバイルでのアダプティブ カードの画像セット カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="アダプティブ カードの画像セット カードの例を示します。" border="false":::

### <a name="actionset"></a>ActionSet

ユーザーにボタンを選択してもらい、同じカードから追加のユーザー入力を収集する場合に使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="モバイルでのアダプティブ カードのアクション セット カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="アダプティブ カードのアクション セット カードの例を示します。" border="false":::

### <a name="choiceset"></a>ChoiceSet

ユーザーから複数の入力を収集するために使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="モバイルでのアダプティブ カードの選択肢セット カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="アダプティブ カードの選択肢セット カードの例を示します。" border="false":::

## <a name="anatomy"></a>構造

アダプティブ カードの柔軟性は高いです。 ただし、少なくとも、すべてのカードに次のコンポーネントを含めることをお勧めします。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="モバイルでのアダプティブ カードの構造の例を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**ヘッダー**: ヘッダーを明確かつ簡潔にします。|
|B|**本文のコピー**: ヘッダーに含めるには長すぎるか、ヘッダーに含めるほど重要ではない詳細を伝えます。|
|C|**プライマリ アクション**: ベスト プラクティスとして、1 ~ 3 個のプライマリ アクションを含めます。 グループには最大 6 個のコントロールを指定できます。|

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="アダプティブ カードの構造の例を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**ヘッダー**: ヘッダーを明確かつ簡潔にします。|
|B|**本文のコピー**: ヘッダーに含めるには長すぎるか、ヘッダーに含めるほど重要ではない詳細を伝えます。|
|C|**プライマリ アクション**: ベスト プラクティスとして、1 ~ 3 個のプライマリ アクションを含めます。 グループには最大 6 個のコントロールを指定できます。|

## <a name="best-practices"></a>ベスト プラクティス

狭い画面用に設計されたカードは、広い画面でも適切に拡大縮小します（逆は当てはまりません）。 また、ユーザーがデスクトップ上でのみカードを表示しない場合も想定する必要があります。

### <a name="column-layouts"></a>列レイアウト

[`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html) を使用して、カードのコンテンツをテーブルまたはグリッドにフォーマットします。 列の幅の書式設定には、いくつかのオプションがあります。 これらのガイドラインは、各ガイドラインをいつ使用するのか理解するのに役立ちます。

* `"width": "auto"`: `ColumnSet` の各列のサイズを変更して、その列に含めるアプリのコンテンツに合わせます。
   * **Do**: 幅が異なるコンテンツがあり、特定の列に優先順位を付ける必要がない場合に使用します。
   * **Do**: 既定ではテキストは折り返されないため、`TextBlock` ごとに `"wrap": true`を設定します。
   * **Don't**: すべての列コンテナに `"width": "auto"` を設定します。 たとえば、入力とボタンが並んでいる場合、一部の画面でボタンが途切れる可能性があります。 代わりに、常に完全に表示する必要があるボタンやその他のコンテンツを含む列に `auto` を設定します。
* `"width": "stretch"`: 使用可能な `ColumnSet` 幅に基づいて列のサイズを変更します。 複数の列が `"stretch"` の値を使用する場合、それらは使用可能な幅を等しく共有します。
   * **Do**: 他のすべての列の幅が静的な場合は、1 つの列で使用します。 たとえば、1 つの列にすべて 50 ピクセル幅のサムネイル画像があるとします。
* `"width": "<number>"`: 使用可能な `ColumnSet` 幅の比率を使用して列のサイズを変更します。 たとえば、3 つの列を `"width": "1"`、`"width": "4"`、および `"width": "5"` で設定した場合、列は使用可能な幅の 10、40、および 50 パーセントを占めます。
* `"width": "<number>px"`: 特定のピクセル幅に列のサイズを設定します。 この方法は、テーブルを作成するときに役立ちます。
   * **Do**: 表示しているものの幅を変更する必要がない場合に使用します (たとえば、数値やパーセンテージ)。
   * **Don't**: 誤ってカードが表示できる幅を超えています。 使用可能な画面幅はデバイスによって異なることに注意してください。 また、Teams mobile では、Teams デスクトップのような水平スクロールはサポートしていません。

#### <a name="example-knowing-when-to-stretch-columns"></a>例: 列を拡大するタイミングを知る

# <a name="design"></a>[デザイン](#tab/design)

**Do**: この画面では、カードの下部に 2 つの列があります。 入力コンポーネントの幅は `stretch` に設定され、**[選択]** ボタンの幅は `auto` に設定されています。 これにより、ボタンが完全に表示されたままになります。

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="画像は、アダプティブ カードで列の幅を設定する方法を示しています。":::

**Don't**: この画面では、両方の列で `width` が `auto` に設定されています。 これにより、右側の **[選択]** ボタンが入力と比較してわずかに切り取られます。

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-dont.png" alt-text="画像は、アダプティブ カードで列幅を設定しない方法を示しています。":::

# <a name="code"></a>[コード](#tab/code)

従うべき設計例を実装するためのコードは次のとおりです。

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.2",
  "body": [
    {
      "type": "TextBlock",
      "text": "I wasn't able to identify the type of expense. Select from the list:",
      "wrap": true,
      "id": "typePrompt",
      "spacing": "Medium",
      "size": "Medium"
    },
    {
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Submit",
          "title": "Phone Bill",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Phone Bill",
              "action": "Phone Bill"
            },
            "action": "Phone Bill"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Taxi and Other Transportation",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Taxi and Other Transportation",
              "action": "Taxi and Other Transportation"
            },
            "action": "Taxi and Other Transportation"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Entertainment_misc",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Entertainment_misc",
              "action": "Entertainment_misc"
            },
            "action": "Entertainment_misc"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Car Rental",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Car Rental",
              "action": "Car Rental"
            },
            "action": "Car Rental"
          }
        },
        {
          "type": "Action.Submit",
          "title": "Airfare",
          "data": {
            "msteams": {
              "type": "messageBack",
              "displayText": "Airfare",
              "action": "Airfare"
            },
            "action": "Airfare"
          }
        }
      ],
      "spacing": "Medium"
    },
    {
      "type": "TextBlock",
      "text": "     ",
      "wrap": true
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "Input.ChoiceSet",
              "choices": [
                {
                  "title": "Meals",
                  "value": "Meals"
                },
                {
                  "title": "Parking/Tolls",
                  "value": "Parking/Tolls"
                },
                {
                  "title": "Accomodation",
                  "value": "Accomodation"
                },
                {
                  "title": "Fuel-Gas/Petrol/Diesel",
                  "value": "Fuel-Gas/Petrol/Diesel"
                },
                {
                  "title": "Hotel",
                  "value": "Hotel"
                },
                {
                  "title": "Meals - Employees Only",
                  "value": "Meals - Employees Only"
                },
                {
                  "title": "Accomodations",
                  "value": "Accomodations"
                },
                {
                  "title": "Misc.Expenses",
                  "value": "Misc.Expenses"
                },
                {
                  "title": "Please Categorize",
                  "value": "Please Categorize"
                }
              ],
              "placeholder": "All",
              "id": "expenseTypes",
              "value": "Meals - Employees Only"
            }
          ]
        },
        {
          "type": "Column",
          "width": "auto",
          "items": [
            {
              "type": "ActionSet",
              "actions": [
                {
                  "type": "Action.Submit",
                  "title": "Select",
                  "data": {
                    "msteams": {
                      "type": "messageBack",
                      "displayText": "Select",
                      "action": "applyType"
                    },
                    "action": "applyType"
                  }
                }
              ]
            }
          ]
        }
      ],
      "spacing": "ExtraLarge"
    }
  ]
}
```

---

#### <a name="example-using-fewer-columns"></a>例: 使用する列の数を減らす

**Do**: レイアウトは、列数が少ないモバイルでより適切に表示される傾向があります。

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-do.png" alt-text="画像は、アダプティブ カードの適切な列数を示しています。":::

**Don't**: 使用する列が多すぎると、モバイルでカードのコンテンツが乱雑になる可能性があります。

:::image type="content" source="~/assets/images/adaptive-cards/column-amount-dont.png" alt-text="画像は、列が多すぎるとアダプティブ カードのレイアウトに悪影響を与える可能性があることを示しています。":::

#### <a name="example-fixed-width-has-its-place"></a>例: 固定幅を使用した方が良い場合もあります。

# <a name="design"></a>[デザイン](#tab/design)

表示しているサイズを変更する必要がない場合は、列を特定のピクセル幅に設定します。 この例では、50 ピクセルのサイズの左側の列を示していますが、サムネイルの横の説明ではカードの長さを伸ばしています

:::image type="content" source="~/assets/images/adaptive-cards/width-auto-do.png" alt-text="画像は、アダプティブ カードで列幅を設定する方法を示しています。":::

# <a name="code"></a>[コード](#tab/code)

設計例を実装するためのコードは次のとおりです。

```json
{
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "Pick up where you left off?",
      "weight": "bolder"
    },
    {
      "type": "ColumnSet",
      "spacing": "medium",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1083",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "Silver Star Mountain Range"
            },
            {
              "type": "TextBlock",
              "text": "Maps",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.msn.com"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1082",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "style": "emphasis",
          "items": [
            {
              "type": "TextBlock",
              "text": "Kitchen Remodel for Homes"
            },
            {
              "type": "TextBlock",
              "text": "With EMPHASIS",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.AdaptiveCards.io"
      }
    },
    {
      "type": "ColumnSet",
      "columns": [
        {
          "type": "Column",
          "width": "50px",
          "items": [
            {
              "type": "Image",
              "url": "https://unsplash.it/80?image=1080",
              "size": "medium"
            }
          ]
        },
        {
          "type": "Column",
          "width": "stretch",
          "items": [
            {
              "type": "TextBlock",
              "text": "The Witcher: A Series"
            },
            {
              "type": "TextBlock",
              "text": "Netflix",
              "isSubtle": true,
              "spacing": "none"
            }
          ]
        }
      ],
      "selectAction": {
        "type": "Action.OpenUrl",
        "url": "https://www.outlook.com"
      }
    }
  ],
  "actions": [
    {
      "type": "Action.OpenUrl",
      "title": "Resume all",
      "url": "ms-cortana:resume-all"
    },
    {
      "type": "Action.OpenUrl",
      "title": "More activities",
      "url": "ms-cortana:more-activities"
    }
  ]
}
```

---

### <a name="text"></a>テキスト

[`TextBlock`](https://adaptivecards.io/explorer/TextBlock.html)、[`ColumnSet`](https://adaptivecards.io/explorer/ColumnSet.html)、または [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) のいずれを使用している場合でも、`wrap` プロパティを `true` に設定して、モバイルでカードのテキストが切り捨てられないようにします。

#### <a name="example-making-sure-text-doesnt-truncate"></a>例: テキストが切り捨てられないことを確認する

# <a name="design"></a>[デザイン](#tab/design)

**Do**: この画面では、カードの `wrap` プロパティが `true` に設定されています。 これにより、テキストを任意の画面サイズに合わせることができます。

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-true.png" alt-text="画像は、アダプティブ カードでテキストを折り返す方法を示しています。":::

**Don't**: この画面では、カードは `wrap` プロパティを使用していないため、モバイル画面ではテキストが途切れます。

:::image type="content" source="~/assets/images/adaptive-cards/text-wrap-false.png" alt-text="画像は、アダプティブ カードでテキストを折り返さないとどうなるかを示しています。":::

# <a name="code"></a>[コード](#tab/code)

従うべき設計例を実装するためのコードは次のとおりです。

```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "text": "What cuisine do you want?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor",
      "style": "compact",
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Chineese",
          "value": "1"
        },
        {
          "title": "Indian",
          "value": "2"
        },
        {
          "title": "Italian",
          "value": "3"
        }
      ]
    },
    {
      "type": "TextBlock",
      "text": "Select the dishes that you like?"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "myColor2",
      "style": "expanded",
      "wrap" : true,
      "isMultiSelect": false,
      "value": "1",
      "choices": [
        {
          "title": "Cauliflower with potatoes sautéed with garam masala",
          "wrap" : true,
          "value": "1"
        },
        {
          "title": "Patties of potato mixed with some vegetables fried",
          "wrap" : true,
          "value": "2"
        },
        {
          "title": "Green capsicum with potatoes sautéed with cumin seeds",
          "wrap" : true,
          "value": "3"
        }
      ]
    }
  ]
}
```

---

### <a name="containers"></a>Containers

`Container` を使用すると、関連する要素のセットをグループ化できます。

* **Do**: `style` プロパティを使用してコンテナを強調します。
* **Do**: `selectAction` プロパティを使用して、アクションをコンテナ内の他の要素に関連付けます。
* **Do**: `Action.ToggleVisibility` プロパティを使用して、要素のグループを折りたたみ可能にします。
* **Don't**: 前述以外の理由でコンテナを使用しないでください。

### <a name="images"></a>画像

カードに画像を含めるときは、これらのガイドラインに従ってください。

* **Do**: ピクセル化を回避するために高 DPI 画面の画像を設計します。 100 x100 ピクセルの画像を 50 x 50 ピクセルで表示する方が、その逆よりも良い方法です。
* **Do**: 画像の正確なサイズを制御する必要がある場合は、`width` プロパティと `height` プロパティを使用します。
* **Don't**: 画像にパディングを含めないでください。 これは通常、望ましくない間隔とレイアウトの問題を引き起こします。
* 背景色について:
   * **Do**: 透明な背景を使用して、画像が Teams のテーマに適応するようにします。 
   * **Don't**: 特定の色をユーザーに表示する必要がない限り、固定の背景色を含めないでください。
   * **Don't**: 読みやすさを損なう背景色を `TextBlock` に追加しないでください。 たとえば、背景が暗い場合は明るいテキスト カラーを使用します。その逆も同様です。

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブ カードに少数のアクションのみを含める方法に関するベスト プラクティス。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Do: 最大 6 つの主要なアクションを使用します

アダプティブ カードは 6 つの主要なアクションをサポートできますが、ほとんどのカードではそれを必要としません。 アクションは明確で簡潔で率直なものである必要があります。 少なければ少ない方がいいです。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブ カードに対するアクションが多すぎてユーザーに負荷をかけないようにする方法についてのベスト プラクティスです。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>Don't: 6 つ以上のプライマリ アクションを使用しないでください

アダプティブ カードは、迅速で実用的なコンテンツを提示する必要があります。 アクションが多すぎると、ユーザーの負担になる可能性があります。

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>頻度

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブ カードの頻度に関するベスト プラクティス。" border="false":::

#### <a name="do-be-concise"></a>Do: 簡潔にしてください

スレッドに複数のカードを送信するのは簡単ですが、スクロールしてカードが見えなくなると、役に立たなくなります。 必須項目にのみ制限するようにしてください。 これは、ユーザーが "ノイズ" と認識する内容に対する許容度が低いチャネルでは特に当てはまります。

## <a name="see-also"></a>関連項目

* [カードとタスク モジュール](~/task-modules-and-cards/cards-and-task-modules.md)
* [カードとタスク モジュールは、Teams ボットでサポートされています](~/task-modules-and-cards/what-are-task-modules.md)
* [アダプティブ カードのユニバーサル アクションの操作](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/work-with-universal-actions-for-adaptive-cards.md)
* [タスク モジュールの送信アクションに応答する](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [ユーザー固有のビュー](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/user-specific-views.md)
