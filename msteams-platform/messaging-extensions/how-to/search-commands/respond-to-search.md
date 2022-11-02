---
title: 検索コマンドに応答する
author: surbhigupta
description: Microsoft Teams アプリのメッセージ拡張機能から検索コマンドに応答する方法について説明します。 ユーザー要求に応答する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 97fe20097e98a015759ba030004fb8c0b3b5e3f9
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819948"
---
# <a name="respond-to-search-command"></a>検索コマンドに応答する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

ユーザーが検索コマンドを送信すると、Web サービスは、検索パラメーターを `composeExtension/query` 持つオブジェクトを `value` 含む呼び出しメッセージを受け取ります。 この呼び出しは、次の条件でトリガーされます。

* 検索ボックスに文字が入力されます。
* `initialRun` がアプリ マニフェストで true に設定されている場合、検索コマンドが呼び出されるとすぐに呼び出しメッセージが表示されます。 詳細については、「既定の [クエリ](#default-query)」を参照してください。

このドキュメントでは、カードとプレビューの形式でユーザーの要求に応答する方法と、Microsoft Teams が既定のクエリを発行する条件について説明します。

要求パラメーターは、次のプロパティを `value` 含む要求内の オブジェクトにあります。

| プロパティ名 | 用途 |
|---|---|
| `commandId` | ユーザーによって呼び出されるコマンドの名前。アプリ マニフェストで宣言されているコマンドのいずれかと一致します。 |
| `parameters` | パラメーターの配列。 各パラメーター オブジェクトには、パラメーター名と、ユーザーによって提供されるパラメーター値が含まれます。 |
| `queryOptions` | 改ページ パラメーター: <br>`skip`: このクエリのカウントをスキップする <br>`count`: 返す要素の数。 |

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

## <a name="respond-to-user-requests"></a>ユーザーの要求に応答する

ユーザーがクエリを実行すると、Microsoft Teams はサービスに同期 HTTP 要求を発行します。 その時点で、コードには `5` 、要求に対する HTTP 応答を提供する秒数があります。 この間、サービスは追加の参照、または要求を処理するために必要なその他のビジネス ロジックを実行できます。

サービスは、ユーザー クエリと一致する結果で応答する必要があります。 応答は、 の HTTP 状態コードと、次の `200 OK` プロパティを持つ有効なアプリケーションまたは JSON オブジェクトを示す必要があります。

|プロパティ名|用途|
|---|---|
|`composeExtension`|最上位レベルの応答エンベロープ。|
|`composeExtension.type`|応答の種類。 次の種類がサポートされています。 <br>`result`: 検索結果の一覧を表示します <br>`auth`: ユーザーに認証を求めるメッセージ <br>`config`: メッセージ拡張機能の設定をユーザーに求めるメッセージ <br>`message`: プレーン テキスト メッセージを表示します |
|`composeExtension.attachmentLayout`|添付ファイルのレイアウトを指定します。 型 `result`の応答に使用されます。 <br>現在、次の種類がサポートされています。 <br>`list`: サムネイル、タイトル、テキスト フィールドを含むカード オブジェクトの一覧 <br>`grid`: サムネイル画像のグリッド |
|`composeExtension.attachments`|有効な添付ファイル オブジェクトの配列。 型 `result`の応答に使用されます。 <br>現在、次の種類がサポートされています。 <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|推奨されるアクション。 型 `auth` または `config`の応答に使用されます。 |
|`composeExtension.text`|表示するメッセージ。 型 `message`の応答に使用されます。 |

### <a name="response-card-types-and-previews"></a>応答カードの種類とプレビュー

Teams では、次のカードの種類がサポートされています。

* [サムネイル カード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [ヒーロー カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

カードについて理解を深め、概要を確認するには、カード [とは何かを](~/task-modules-and-cards/what-are-cards.md)参照してください。

サムネイルとヒーロー カードの種類を使用する方法については、「 [カードとカードアクションを追加](~/task-modules-and-cards/cards/cards-actions.md)する」を参照してください。

Office 365 コネクタ カードの詳細については、「Office 365 [コネクタ カードの使用](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)」を参照してください。

結果の一覧が Microsoft Teams UI に表示され、各項目のプレビューが表示されます。 プレビューは、次の 2 つの方法のいずれかで生成されます。

* オブジェクト内で `preview` プロパティを `attachment` 使用する。 添付ファイルには `preview` ヒーローカードまたはサムネイルカードのみを使用できます。
* オブジェクトの基本的な `title`、、 `text`および `image` プロパティ `attachment` から抽出します。 基本プロパティは、 プロパティが `preview` 指定されていない場合にのみ使用されます。

ヒーローまたはサムネイル カードの場合、ボタンやタップなどの他のアクションを呼び出す操作を除き、プレビュー カードではサポートされていません。

アダプティブ カードまたは Office 365 コネクタ カードを送信するには、プレビューを含める必要があります。 プロパティは `preview` ヒーローまたはサムネイル カードである必要があります。 オブジェクトに `attachment` preview プロパティを指定しない場合、プレビューは生成されません。

ヒーロー カードとサムネイル カードの場合、プレビュー プロパティを指定する必要はありません。プレビューは既定で生成されます。

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

### <a name="enable-and-handle-tap-actions"></a>タップ アクションを有効にして処理する

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
{
    // The Preview card's Tap should have a Value property assigned, this will be returned to the bot in this event. 
    var (packageId, version, description, projectUrl, iconUrl) = query.ToObject<(string, string, string, string, string)>();

    var card = new ThumbnailCard
    {
        Title = "Card Select Item",
        Subtitle = description
    };

    var attachment = new MessagingExtensionAttachment
    {
        ContentType = ThumbnailCard.ContentType,
        Content = card,
    };

    return Task.FromResult(new MessagingExtensionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            Type = "result",
            AttachmentLayout = "list",
            Attachments = new List<MessagingExtensionAttachment> { attachment }
        }
    });
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
async handleTeamsMessagingExtensionSelectItem(context, obj) {
        return {
            composeExtension: {
                  type: 'result',
                  attachmentLayout: 'list',
                  attachments: [CardFactory.thumbnailCard(obj.Item3)]
            }
        };
    } 
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "name": "composeExtension/selectItem",
    "type": "invoke",
    "value": {
        "Item1": "Package_Name",
        "Item2": "Version",
        "Item3": "Package Description"
    },
    .
    .
    .
}
```

* * *

> [!NOTE]
> `OnTeamsMessagingExtensionSelectItemAsync` はモバイル チーム アプリケーションではトリガーされません。

## <a name="default-query"></a>既定のクエリ

マニフェストで を に`true`設定`initialRun`した場合、Microsoft Teams は、ユーザーが最初にメッセージ拡張機能を開いたときに **既定** のクエリを発行します。 サービスは、事前に設定された一連の結果を使用して、このクエリに応答できます。 これは、検索コマンドで認証または構成が必要な場合、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。

既定のクエリは、通常のユーザー クエリと同じ構造を持ち、次の `name` オブジェクトに示すように フィールドを に `initialRun` 設定し `value` 、 に `true` 設定します。

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
|Teams メッセージ拡張機能アクション| アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Teams メッセージ拡張機能検索   |  検索コマンドを定義し、検索に応答する方法について説明します。        |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [メッセージ拡張機能に認証を追加する](~/messaging-extensions/how-to/add-authentication.md)

## <a name="see-also"></a>関連項目

* [メッセージの拡張機能](../../what-are-messaging-extensions.md)
* [JavaScript を使用して初めてのタブ アプリを構築する](../../../sbs-gs-javascript.yml)
* [composeExtensions](../../../resources/schema/manifest-schema.md#composeextensions)
