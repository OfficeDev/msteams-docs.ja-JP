---
title: アダプティブ カードの先行入力検索
author: Rajeshwari-v
description: このモジュールでは、Input.ChoiceSet コントロールを使用したアダプティブ カードでの先行入力検索について説明し、先行入力検索を実装します
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 205da5ca0171182047ccd06f7f2926f731ceb94d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143894"
---
# <a name="typeahead-search-in-adaptive-cards"></a>アダプティブ カードの先行入力検索

アダプティブ カードの先行入力検索機能により、コンポーネントの `input.choiceset` 検索機能が強化されます。 検索フィールドにテキストを入力するための選択肢の一覧が表示されます。 アダプティブ カードに先行入力検索を組み込んで、データを検索および選択できます。

次の検索には先行入力検索を使用できます。

* [静的検索](#static-typeahead-search)
* [動的検索](#dynamic-typeahead-search)

## <a name="static-typeahead-search"></a>静的先行型検索

静的な先行入力検索を使用すると、ユーザーはアダプティブ カード ペイロード内 `input.choiceset` で指定された値から検索できます。 静的な先行入力検索を使用して、ユーザーに複数の選択肢を表示できます。 静的検索のペイロード サイズは、ペイロードで指定された選択肢の数と共に増加します。
ユーザーがテキストの入力を開始すると、入力と部分的に一致する選択肢がフィルター処理されます。 ドロップダウン リストでは、検索に一致する入力文字が強調表示されます。

次の図は、静的な先行型検索を示しています。

![静的先行型検索](~/assets/images/Cards/static-typeahead-search.gif)

## <a name="dynamic-typeahead-search"></a>動的な先行入力検索

動的な先行入力検索は、大規模なデータ セットからデータを検索して選択する場合に便利です。 データ セットは、カード ペイロードで指定されたデータセットから動的に読み込まれます。 先行入力機能は、ユーザーの種類に応じて選択肢を除外するのに役立ちます。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop.png" alt-text="動的な先行入力検索":::

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop-2.png" alt-text="動的な先行入力検索 2":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

AndroidおよびiOSモバイル クライアントでは、アダプティブ カードでの先行入力検索がサポートされます。

**シナリオ**

John は、Xbox リテール ストアで働く店員です。 ストアはボットを使用して、顧客からの新しい購入要求を受け取ります。 顧客は、使用可能な数千のゲームから検索できます。 アダプティブ カードの先行入力検索は、顧客の選択肢を検索および選択するために使用されます。

**アダプティブ カードで先行入力検索を使用するには**

1. ユーザー A がストア ボットを開きます。
1. ユーザー A は、 **新しい顧客要求** のコマンドをボットに送信します。 ボットは、コンポーネントを持 `Input.ChoiceSet` つアダプティブ カードで応答します。
1. ユーザー A は、先行入力検索を使用して、顧客の選択に基づいて情報を検索して選択します。

次の図は、先行入力検索のモバイル エクスペリエンスを示しています。

![静的先行型検索](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> クエリ ベースのメッセージ拡張機能など、動的検索ではリッチ カード エクスペリエンスを得ることはできません。

## <a name="implement-typeahead-search"></a>先行入力検索を実装する

`Input.ChoiceSet` は、アダプティブ カードの重要な入力コンポーネントの 1 つです。 先行入力検索コントロールをコンポーネントに追加して `Input.ChoiceSet` 、先行入力検索を実装できます。 次の選択を使用して、必要な情報を検索して選択できます。

* 展開された選択などのドロップダウン。
* ラジオ ボタン (単一の選択など)。
* 複数の選択など、チェック ボックス。

> [!NOTE]
> コントロールは `Input.ChoiceSet` 、スタイルと `isMultiSelect` プロパティに基づいています。

### <a name="schema-properties"></a>スキーマのプロパティ

次のプロパティは、事前入力検索を有効にするための [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) スキーマへの新しい追加です。

| プロパティ| 型 | 必須 | 説明 |
|-----------|------|----------|-------------|
| style | Compact <br/> Expanded <br/> Filtered | 不要 | 静的な先行入力でサポートされている検証の一覧にフィルター処理されたスタイルを追加します。|
| choices.data | Data.Query | いいえ | バックエンドから選択肢のリモート セットをフェッチすることで、ユーザーの種類として動的な先行入力を有効にします。 |

### <a name="dataquery-definition"></a>Data.Query 定義

| プロパティ| 型 | 必須 | 説明 |
|-----------|------|----------|-------------|
| type | Data.Query | はい | Data.Query オブジェクトであることを指定します。|
| データセット | String | はい | 動的にフェッチされるデータの種類を指定します。 |
| value | String | いいえ | ユーザーがボットに指定 `ChoiceSet`した入力をボットに呼び出し要求を入力します。 |
| count | 番号 | 不要 | 返す必要がある要素の数を指定するために、ボットへの呼び出し要求を設定します。 ユーザーが別の金額を送信する場合、ボットはそれを無視します。 |
| skip | 番号 | いいえ | 呼び出し要求をボットに設定して、ユーザーがページ分割してリスト内で先に移動することを示します。 |

### <a name="example"></a>例

次に示すように、単一の&複数選択オプションを含む静的および動的な先行型検索を含むペイロードの例を示します。

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

## <a name="code-snippets-for-invoke-request-and-response"></a>呼び出し要求と応答のコード スニペット

### <a name="invoke-request"></a>要求の呼び出し

```json
{
    "name": "application/search",
    "type": "invoke",
    "value": {
        "queryText": "fluentui",
        "queryOptions": {
            "skip": 0,
            "top": 15
        },
        "dataset": "npm"
    },
    "locale": "en-US",
    "localTimezone": "America/Los_Angeles",
    // …. other fields
}
```

### <a name="response"></a>応答

#### <a name="c"></a>[C#](#tab/csharp)

```csharp
protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Name == "application/search")
    {
 var packages = new[] {
   new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
   new { title = "Fluent UI Library", value = "FluentUI" }};

 var searchResponseData = new
 {
     type = "application/vnd.microsoft.search.searchResponse",
     value = new
     {
  results = packages
     }
 };
 var jsonString = JsonConvert.SerializeObject(searchResponseData);
 JObject jsonData = JObject.Parse(jsonString);
 return new InvokeResponse()
 {
     Status = 200,
     Body = jsonData
 };
    }

    return null;
}
```

#### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```nodejs
  async onInvokeActivity(context) {
    if (context._activity.name == 'application/search') {
      // let searchQuery = context._activity.value.queryText;  // This can be used to filter the results
      var successResult = {
        status: 200,
        body: {
          "type": "application/vnd.microsoft.search.searchResponse",
          "value": {
            "results": [
              {
                "value": "FluentAssertions",
                "title": "A very extensive set of extension methods"
              },
              {
                "value": "FluentUI",
                "title": "Fluent UI Library"
              }
            ]
          }
        }
      }

      return successResult;

    }
  }
```

#### <a name="json"></a>[JSON](#tab/json)

```json
{
    "status": 200,
    "body" : {
        "type": "application/vnd.microsoft.search.searchResponse",
        "value": {
           "results": [
                {
                    "value": "FluentAssertions",
                    "title": "A very extensive set of extension methods."
                },
                {
                    "value": "FluentUI",
                    "title": "Fluent UI Library"
                }
            ]
        }
    }
}
```

---

## <a name="code-sample"></a>コード サンプル

|**サンプルの名前** | **説明** | **C#** | **Node.js** |
|----------------|-----------------|--------------|----------------|
| アダプティブ カードの先行入力検索コントロール | このサンプルは、アダプティブ カードの静的および動的な先行型検索コントロールの機能を示しています。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [アダプティブ カードのユニバーサル アクション](Universal-actions-for-adaptive-cards/Overview.md)
* [タスク モジュール](../what-are-task-modules.md)
