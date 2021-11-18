---
title: アダプティブ カードの Typeahead 検索
author: Rajeshwari-v
description: アダプティブ カードの Input.ChoiceSet コントロールを使用した typeahead 検索について説明します。
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 95041b1a24ac083329a809b8a5989d77e2430e26
ms.sourcegitcommit: e45742fd2aa2ff5e5c15e8f7c20cc14fbef6d441
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2021
ms.locfileid: "61075584"
---
# <a name="typeahead-search-in-adaptive-cards"></a>アダプティブ カードの Typeahead 検索

アダプティブ カードの Typeahead 検索機能により、コンポーネントでの検索エクスペリエンスが強化 `input.choiceset` されます。 検索フィールドにテキストを入力する選択肢の一覧を提供します。 Typeahead 検索とアダプティブ カードを組み込み、データを検索および選択できます。

次の検索に対して typeahead 検索を使用できます。

* [静的検索](#static-typeahead-search)
* [動的検索](#dynamic-typeahead-search)

## <a name="static-typeahead-search"></a>静的型検索

静的な typeahead 検索を使用すると、アダプティブ カード ペイロード内で指定された値 `input.choiceset` から検索できます。 静的型検索を使用すると、ユーザーに複数の選択肢を表示できます。 静的検索のペイロード サイズは、ペイロードで指定された選択肢の数と一緒に増加します。
ユーザーがテキストの入力を開始すると、選択肢がフィルター処理され、入力に部分的に一致します。 ドロップダウン リストは、検索に一致する入力文字を強調表示します。

次の図は、静的な typeahead 検索を示しています。

![静的型検索](~/assets/images/Cards/static-typeahead-search.gif)

## <a name="dynamic-typeahead-search"></a>動的な型検索

動的型検索は、大きなデータ セットからデータを検索して選択する場合に便利です。 データ セットは、カード ペイロードで指定されたデータセットから動的に読み込まれます。 先行型機能は、ユーザーの種類として選択肢をフィルター処理するのに役立ちます。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

![動的な型検索](~/assets/images/Cards/dynamic-typeahead-search-desktop.png)

![動的タイプアヘッド検索イメージ 2](~/assets/images/Cards/dynamic-typeahead-search-desktop-2.png)

# <a name="mobile"></a>[モバイル](#tab/mobile)

Android および iOS モバイル クライアントは、アダプティブ カードでの typeahead 検索をサポートします。

**シナリオ**

John は、Xbox 小売店で働くストアの従業員です。 ストアはボットを使用して、顧客からの新しい購入要求を受け取ります。 顧客は、利用可能な数千のゲームから検索できます。 アダプティブ カードの Typeahead 検索は、顧客の選択肢を検索および選択するために使用されます。

**アダプティブ カードで typeahead 検索を使用するには**

1. ユーザー A がストア ボットを開きます。
1. ユーザー A は、新しい顧客要求のコマンドを **ボットに送信します**。 ボットは、コンポーネントを持つアダプティブ カードで応答 `Input.ChoiceSet` します。
1. ユーザー A は typeahead 検索を使用して、顧客の選択に基づいて情報を検索および選択します。

次の図は、typeahead 検索のモバイル エクスペリエンスを示しています。

![静的型検索](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> クエリ ベースのメッセージング拡張機能など、動的検索でリッチ カード エクスペリエンスを取得できない。

## <a name="implement-typeahead-search"></a>typeahead 検索の実装

`Input.ChoiceSet` はアダプティブ カードの重要な入力コンポーネントの 1 つです。 typeahead 検索コントロールをコンポーネントに追加して `Input.ChoiceSet` 、typeahead 検索を実装できます。 次の項目を選択して、必要な情報を検索して選択できます。

* 展開された選択範囲などのドロップダウン。
* ラジオ ボタン (単一選択など)。
* 複数の選択範囲などのチェック ボックスをオンにします。

> [!NOTE]
> コントロール `Input.ChoiceSet` は、スタイルとプロパティに基 `isMultiSelect` づいて設定されます。

### <a name="schema-properties"></a>スキーマ のプロパティ

次のプロパティは、typeahead 検索を有効 [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) にするスキーマへの新しい追加です。

| プロパティ| 型 | 必須 | 説明 |
|-----------|------|----------|-------------|
| style | Compact <br/> Expanded <br/> Filtered | 不要 | 静的型先行のサポートされている検証の一覧にフィルター処理されたスタイルを追加します。|
| choices.data | Data.Query | 不要 | バックエンドからリモートの選択肢セットをフェッチすることで、ユーザーの種類として動的な先行型を有効にできます。 |

### <a name="dataquery-definition"></a>Data.Query 定義

| プロパティ| 型 | 必須 | 説明 |
|-----------|------|----------|-------------|
| type | Data.Query | はい | Data.Query オブジェクトを指定します。|
| データセット | 文字列 | はい | 動的にフェッチされるデータの種類を指定します。 |
| value | 文字列 | いいえ | ボットへの呼び出し要求に対して、ユーザーが指定した入力を設定します `ChoiceSet` 。 |
| count | 番号 | 不要 | ボットへの呼び出し要求を設定して、返す必要がある要素の数を指定します。 ユーザーが別の金額を送信する場合、ボットはそれを無視します。 | 
| skip | 番号 | 不要 | ボットへの呼び出し要求を設定して、ユーザーがページ分割してリスト内を移動する必要があるかどうかを示します。 |

### <a name="example"></a>例

次に示す複数の選択オプションを使用して、静的および動的な typeahead 検索を&ペイロードの例を示します。

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "columns": [
        {
          "width": "1",
          "items": [
            {
              "size": null,
              "url": "https://urlp.asm.skype.com/v1/url/content?url=https%3a%2f%2fi.imgur.com%2fhdOYxT8.png",
              "height": "auto",
              "type": "Image"
            }
          ],
          "type": "Column"
        },
        {
          "width": "2",
          "items": [
            {
              "size": "extraLarge",
              "text": "Game Purchase",
              "weight": "bolder",
              "wrap": true,
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Please fill out the below form to send a game purchase request.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Call of Duty",
                  "value": "call_of_duty"
                },
                {
                  "title": "Death's Door",
                  "value": "deaths_door"
                },
                {
                  "title": "Grand Theft Auto V",
                  "value": "grand_theft"
                },
                {
                  "title": "Minecraft",
                  "value": "minecraft"
                }
              ],
              "style": "filtered",
              "placeholder": "Search for a game",
              "id": "choiceGameSingle",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Multi-Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Static Option 1",
                  "value": "static_option_1"
                },
                {
                  "title": "Static Option 2",
                  "value": "static_option_2"
                },
                {
                  "title": "Static Option 3",
                  "value": "static_option_3"
                }
              ],
              "isMultiSelect": true,
              "style": "filtered",
              "choices.data": {
                "type": "Data.Query",
                "dataset": "xbox"
              },
              "id": "choiceGameMulti",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Needed by: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        },
        {
          "width": "stretch",
          "items": [
            {
              "id": "choiceDate",
              "type": "Input.Date"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Buy and download digital games and content directly from your Xbox console, Windows 10 PC, or at Xbox.com.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "text": "Earn points for what you already do on Xbox, then redeem your points on real rewards. Play more, get rewarded. Start earning today.",
      "wrap": true,
      "type": "TextBlock"
    }
  ],
  "actions": [
    {
      "data": {
        "msteams": {
          "type": "invoke",
          "value": {
            "type": "task/submit"
          }
        }
      },
      "title": "Request Purchase",
      "type": "Action.Submit"
    }
  ],
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.2"
}
```

## <a name="see-also"></a>関連項目

* [アダプティブ カードのユニバーサル アクション](Universal-actions-for-adaptive-cards/Overview.md)
* [タスク モジュール](../what-are-task-modules.md)