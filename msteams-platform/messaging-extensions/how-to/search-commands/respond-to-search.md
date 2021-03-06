---
title: 検索コマンドに応答する
author: surbhigupta
description: アプリ内のメッセージング拡張機能から検索コマンドに応答するMicrosoft Teamsします。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 3d82c7be0a0bbe5cf0ef991a90b277de38fcf4d5
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068941"
---
# <a name="respond-to-search-command"></a>検索コマンドに応答する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

ユーザーが検索コマンドを送信すると、Web サービスは、検索パラメーターを持つオブジェクトを含む呼び出し `composeExtension/query` `value` メッセージを受信します。 この呼び出しは、次の条件でトリガーされます。

* 検索ボックスに文字が入力されます。
* `initialRun` がアプリ マニフェストで true に設定されている場合、検索コマンドが呼び出されるとすぐに呼び出しメッセージが表示されます。 詳細については、「既定のクエリ [」を参照してください](#default-query)。

このドキュメントでは、カードとプレビューの形式でユーザー要求に応答する方法と、ユーザーが既定のクエリを発行する条件Microsoft Teams説明します。

要求パラメーターは、次の `value` プロパティを含む要求内のオブジェクトに含まれています。

| プロパティ名 | 用途 |
|---|---|
| `commandId` | アプリ マニフェストで宣言されているコマンドの 1 つと一致する、ユーザーによって呼び出されるコマンドの名前。 |
| `parameters` | パラメーターの配列。 各パラメーター オブジェクトには、ユーザーが指定したパラメーター値と共に、パラメーター名が含まれる。 |
| `queryOptions` | ページネーション パラメーター: <br>`skip`: このクエリのスキップ カウント <br>`count`: 返す要素の数。 |

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

以下の JSON は、最も関連性の高いセクションを強調表示するために短縮されています。

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

ユーザーがクエリを実行すると、Microsoft Teamsに同期 HTTP 要求が発行されます。 その時点で、要求に対する `5` HTTP 応答を提供する秒がコードに設定されています。 この間、サービスは追加の参照、または要求を処理するために必要なその他のビジネス ロジックを実行できます。

サービスは、ユーザー クエリに一致する結果で応答する必要があります。 応答は、HTTP 状態コードと、次のプロパティを持 `200 OK` つ有効なアプリケーションまたは JSON オブジェクトを示す必要があります。

|プロパティ名|用途|
|---|---|
|`composeExtension`|トップ レベルの応答エンベロープ。|
|`composeExtension.type`|応答の種類。 次の種類がサポートされています。 <br>`result`: 検索結果の一覧を表示します。 <br>`auth`: ユーザーに認証を求める <br>`config`: メッセージング拡張機能のセットアップをユーザーに求める <br>`message`: テキスト形式のメッセージを表示します。 |
|`composeExtension.attachmentLayout`|添付ファイルのレイアウトを指定します。 型の応答に使用されます `result` 。 <br>現在、次の種類がサポートされています。 <br>`list`: サムネイル、タイトル、テキスト フィールドを含むカード オブジェクトの一覧 <br>`grid`: サムネイル画像のグリッド |
|`composeExtension.attachments`|有効な添付ファイル オブジェクトの配列。 型の応答に使用されます `result` 。 <br>現在、次の種類がサポートされています。 <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|推奨されるアクション。 型または . の応答に `auth` 使用 `config` されます。 |
|`composeExtension.text`|表示するメッセージ。 型の応答に使用されます `message` 。 |

### <a name="response-card-types-and-previews"></a>応答カードの種類とプレビュー

Teamsは、次のカードの種類をサポートしています。

* [サムネイル カード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [ヒーロー カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

カードの理解と概要を把握するには、カード [の概要を参照してください](~/task-modules-and-cards/what-are-cards.md)。

サムネイルカードとヒーロー カードの種類を使用する方法については、「Add [card and card actions」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。

コネクタ カードの詳細については、「Office 365 コネクタ カードの使用[」Office 365参照してください](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。

結果リストは、各アイテムのプレビュー Microsoft Teams UI に表示されます。 プレビューは、次の 2 つの方法で生成されます。

* オブジェクト内 `preview` のプロパティを使用 `attachment` する。 添付 `preview` ファイルには、ヒーロー カードまたはサムネイル カードのみを指定できます。
* 添付ファイルの基本 `title` 、 `text` および `image` プロパティから抽出されます。 これらは、プロパティが設定されていない `preview` 場合にのみ使用され、これらのプロパティを使用できます。
* [ヒーロー] または [サムネイル] カードボタンとタップアクション (呼び出しを除く) は、プレビュー カードではサポートされません。

プレビュー プロパティを使用して、アダプティブ カードまたは Office 365 コネクタ カードのプレビューを結果リストに表示できます。 結果が既にヒーロー カードまたはサムネイル カードである場合、preview プロパティは必要ありません。 プレビュー添付ファイルを使用する場合は、ヒーロー カードまたはサムネイル カードである必要があります。 preview プロパティを指定しない場合、カードのプレビューは失敗し、何も表示されません。

### <a name="response-example"></a>応答の例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="json"></a>[JSON](#tab/json)

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

マニフェストで設定した場合、Microsoft Teamsが最初にメッセージング拡張機能を開くと、既定のクエリ `initialRun` `true` が発行されます。  サービスは、事前に設定された結果のセットでこのクエリに応答できます。 これは、検索コマンドで認証または構成が必要な場合、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。

既定のクエリは、通常のユーザー クエリと同じ構造を持ち、フィールドを次のオブジェクトに示すように設定 `name` `initialRun` `value` `true` します。

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

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams拡張アクション| アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams拡張機能の検索   |  検索コマンドを定義し、検索に応答する方法について説明します。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a>関連項目

[メッセージング拡張機能に構成を追加する](~/get-started/first-message-extension.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [メッセージング拡張機能に認証を追加する](~/messaging-extensions/how-to/add-authentication.md)



