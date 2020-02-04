---
title: 検索コマンドに応答する
author: clearab
description: Microsoft Teams アプリのメッセージング拡張機能から [検索] コマンドに応答する方法。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e8b40dd8f422ffbd2537e8fa76a38c15eb6208de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675121"
---
# <a name="respond-to-the-search-command"></a>[検索] コマンドに応答する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Web サービスは、検索パラメーター `composeExtension/query`を持つオブジェクトを`value`含む呼び出しメッセージを受信します。 この呼び出しはトリガーされます。

* 文字は検索ボックスに入力されます。
* が`initialRun`アプリマニフェストで true に設定されている場合は、検索コマンドが呼び出された直後に invoke メッセージを受信します。 [既定のクエリ](#default-query)を参照してください。

要求のパラメーター自体は、要求の`value`オブジェクト内にあります。これには、次のプロパティが含まれます。

| プロパティ名 | 用途 |
|---|---|
| `commandId` | アプリマニフェストで宣言されているコマンドのいずれかと一致する、ユーザーによって起動されたコマンドの名前。 |
| `parameters` | パラメーターの配列。 各 parameter オブジェクトには、ユーザーによって提供されるパラメータ値とともにパラメータ名が含まれています。 |
| `queryOptions` | 改ページのパラメーター: <br>`skip`: このクエリの skip count <br>`count`: 返される要素の数 |

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

次の JSON は、最も関連のあるセクションを強調するために短縮されています。

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
...
}
```

* * *

## <a name="respond-to-user-requests"></a>ユーザー要求に応答する

ユーザーがクエリを実行すると、Microsoft Teams はサービスに対して同期 HTTP 要求を発行します。 その時点で、コードには、要求に対する HTTP 応答を提供する5秒の時間があります。 この間、サービスは、追加の参照、または要求の提供に必要なその他のビジネスロジックを実行できます。

サービスは、ユーザークエリに一致する結果で応答する必要があります。 応答は、HTTP 状態コード`200 OK`と、次の本文を含む有効な application/json オブジェクトを示す必要があります。

|プロパティ名|用途|
|---|---|
|`composeExtension`|最上位レベルの応答封筒。|
|`composeExtension.type`|応答の種類。 次の種類がサポートされています。 <br>`result`: 検索結果の一覧を表示します。 <br>`auth`: ユーザーに認証を要求する <br>`config`: メッセージング拡張機能をセットアップするようにユーザーに要求します。 <br>`message`: テキスト形式のメッセージが表示されます。 |
|`composeExtension.attachmentLayout`|添付ファイルのレイアウトを指定します。 種類`result`の応答に使用されます。 <br>現在、次の種類がサポートされています。 <br>`list`: サムネイル、タイトル、テキストフィールドを含む card オブジェクトのリスト <br>`grid`: サムネイル画像のグリッド |
|`composeExtension.attachments`|有効な attachment オブジェクトの配列。 種類`result`の応答に使用されます。 <br>現在、次の種類がサポートされています。 <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|推奨されるアクション。 種類`auth`または`config`の応答に使用されます。 |
|`composeExtension.text`|表示するメッセージ。 種類`message`の応答に使用されます。 |

### <a name="response-card-types-and-previews"></a>応答カードの種類とプレビュー

次の種類の添付ファイルがサポートされています。

* [サムネイルカード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [英雄カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタカード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブカード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

概要については、「[カードとは](~/task-modules-and-cards/what-are-cards.md)」を参照してください。

サムネイルおよびヒーローカードの種類を使用する方法については、「[カードおよびカードのアクションを追加](~/task-modules-and-cards/cards/cards-actions.md)する」を参照してください。

Office 365 コネクタカードに関するその他のドキュメントについては、「 [office 365 コネクタカードの使用](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)」を参照してください。

結果リストは、Microsoft Teams UI に各アイテムのプレビューと共に表示されます。 プレビューは、次の2つの方法のいずれかで生成されます。

* `attachment`オブジェクト内で`preview`プロパティを使用します。 添付`preview`ファイルには、ヒーローまたはサムネイルカードのみを指定できます。
* 添付ファイルの基本`title`、 `text`、および`image`プロパティから抽出されます。 これらのプロパティは、 `preview`プロパティが設定されておらず、これらのプロパティを使用できる場合にのみ使用されます。

そのプレビュープロパティを使用して、アダプティブカードまたは Office 365 のコネクタカードのプレビューを結果リストに表示することができます。 結果が既にヒーローまたはサムネイルカードである場合は、この手順は必要ありません。 プレビューの添付ファイルを使用する場合は、ヒーローまたは Thumbnail カードである必要があります。 Preview プロパティが指定されていない場合、カードのプレビューは失敗し、何も表示されません。

### <a name="response-example"></a>応答の例

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken) 
{
  var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

  //searches NuGet for a package
  var obj = JObject.Parse(await (new HttpClient()).GetStringAsync($"https://azuresearch-usnc.nuget.org/query?q=id:{text}&prerelease=true"));
  var packages = obj["data"].Select(item => (item["id"].ToString(), item["version"].ToString(), item["description"].ToString()));

  // We take every row of the results and wrap them in cards wrapped in in MessagingExtensionAttachment objects.
  // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
  var attachments = packages.Select(package => new MessagingExtensionAttachment
      {
          ContentType = HeroCard.ContentType,
          Content = new HeroCard { Title = package.Item1 },
          Preview = new HeroCard { Title = package.Item1, Tap = new CardAction { Type = "invoke", Value = package } }.ToAttachment()
      })
      .ToList();

  // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
  return new MessagingExtensionResponse
  {
      ComposeExtension = new MessagingExtensionResult
      {
          Type = "result",
          AttachmentLayout = "list",
          Attachments = attachments
      }
  };
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearchBot extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;
        const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);

        const attachments = [];
        response.data.objects.forEach(obj => {
            const heroCard = CardFactory.heroCard(obj.package.name);
            const preview = CardFactory.heroCard(obj.package.name);
            const attachment = { ...heroCard, preview };
            attachments.push(attachment);
        });

        return {
            composeExtension: {
                type: 'result',
                attachmentLayout: 'list',
                attachments: attachments
            }
        };
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

* * *

## <a name="default-query"></a>既定のクエリ

マニフェスト内に`initialRun`が`true`設定されている場合、Microsoft Teams は、ユーザーが最初にメッセージング拡張機能を開いたときに "既定" クエリを発行します。 サービスは、このクエリに対して事前に設定された一連の結果で応答できます。 これは、検索コマンドが認証または構成を必要とし、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。

既定のクエリは、通常のユーザークエリと同じ構造を持って`name`おり`initialRun` `value` 、フィールドはに設定`true`され、以下のオブジェクトと同様に設定されています。

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="next-steps"></a>次のステップ

認証または構成を追加する

* [メッセージング拡張機能に認証を追加する](~/messaging-extensions/how-to/add-authentication.md)
* [メッセージング拡張機能に構成を追加する](~/messaging-extensions/how-to/add-configuration-page.md)

構成の展開

* [アプリパッケージを展開する](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
