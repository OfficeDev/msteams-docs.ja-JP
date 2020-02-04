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
# <a name="respond-to-the-search-command"></a><span data-ttu-id="10b92-103">[検索] コマンドに応答する</span><span class="sxs-lookup"><span data-stu-id="10b92-103">Respond to the search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="10b92-104">Web サービスは、検索パラメーター `composeExtension/query`を持つオブジェクトを`value`含む呼び出しメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="10b92-104">Your web service will receive a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="10b92-105">この呼び出しはトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="10b92-105">This invoke is triggered:</span></span>

* <span data-ttu-id="10b92-106">文字は検索ボックスに入力されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="10b92-107">が`initialRun`アプリマニフェストで true に設定されている場合は、検索コマンドが呼び出された直後に invoke メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="10b92-107">If `initialRun` is set to true in your app manifest, you'll receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="10b92-108">[既定のクエリ](#default-query)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10b92-108">See [default query](#default-query).</span></span>

<span data-ttu-id="10b92-109">要求のパラメーター自体は、要求の`value`オブジェクト内にあります。これには、次のプロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="10b92-109">The request parameters itself are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="10b92-110">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="10b92-110">Property name</span></span> | <span data-ttu-id="10b92-111">用途</span><span class="sxs-lookup"><span data-stu-id="10b92-111">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="10b92-112">アプリマニフェストで宣言されているコマンドのいずれかと一致する、ユーザーによって起動されたコマンドの名前。</span><span class="sxs-lookup"><span data-stu-id="10b92-112">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="10b92-113">パラメーターの配列。</span><span class="sxs-lookup"><span data-stu-id="10b92-113">Array of parameters.</span></span> <span data-ttu-id="10b92-114">各 parameter オブジェクトには、ユーザーによって提供されるパラメータ値とともにパラメータ名が含まれています。</span><span class="sxs-lookup"><span data-stu-id="10b92-114">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="10b92-115">改ページのパラメーター:</span><span class="sxs-lookup"><span data-stu-id="10b92-115">Pagination parameters:</span></span> <br><span data-ttu-id="10b92-116">`skip`: このクエリの skip count</span><span class="sxs-lookup"><span data-stu-id="10b92-116">`skip`: skip count for this query</span></span> <br><span data-ttu-id="10b92-117">`count`: 返される要素の数</span><span class="sxs-lookup"><span data-stu-id="10b92-117">`count`: number of elements to return</span></span> |

# <a name="cnettabdotnet"></a>[<span data-ttu-id="10b92-118">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="10b92-118">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="10b92-119">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="10b92-119">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="10b92-120">JSON</span><span class="sxs-lookup"><span data-stu-id="10b92-120">JSON</span></span>](#tab/json)

<span data-ttu-id="10b92-121">次の JSON は、最も関連のあるセクションを強調するために短縮されています。</span><span class="sxs-lookup"><span data-stu-id="10b92-121">The JSON below is shortened to highlight the most relevant sections.</span></span>

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

## <a name="respond-to-user-requests"></a><span data-ttu-id="10b92-122">ユーザー要求に応答する</span><span class="sxs-lookup"><span data-stu-id="10b92-122">Respond to user requests</span></span>

<span data-ttu-id="10b92-123">ユーザーがクエリを実行すると、Microsoft Teams はサービスに対して同期 HTTP 要求を発行します。</span><span class="sxs-lookup"><span data-stu-id="10b92-123">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="10b92-124">その時点で、コードには、要求に対する HTTP 応答を提供する5秒の時間があります。</span><span class="sxs-lookup"><span data-stu-id="10b92-124">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="10b92-125">この間、サービスは、追加の参照、または要求の提供に必要なその他のビジネスロジックを実行できます。</span><span class="sxs-lookup"><span data-stu-id="10b92-125">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="10b92-126">サービスは、ユーザークエリに一致する結果で応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10b92-126">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="10b92-127">応答は、HTTP 状態コード`200 OK`と、次の本文を含む有効な application/json オブジェクトを示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="10b92-127">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="10b92-128">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="10b92-128">Property name</span></span>|<span data-ttu-id="10b92-129">用途</span><span class="sxs-lookup"><span data-stu-id="10b92-129">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="10b92-130">最上位レベルの応答封筒。</span><span class="sxs-lookup"><span data-stu-id="10b92-130">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="10b92-131">応答の種類。</span><span class="sxs-lookup"><span data-stu-id="10b92-131">Type of response.</span></span> <span data-ttu-id="10b92-132">次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="10b92-132">The following types are supported:</span></span> <br><span data-ttu-id="10b92-133">`result`: 検索結果の一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="10b92-133">`result`: displays a list of search results</span></span> <br><span data-ttu-id="10b92-134">`auth`: ユーザーに認証を要求する</span><span class="sxs-lookup"><span data-stu-id="10b92-134">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="10b92-135">`config`: メッセージング拡張機能をセットアップするようにユーザーに要求します。</span><span class="sxs-lookup"><span data-stu-id="10b92-135">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="10b92-136">`message`: テキスト形式のメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-136">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="10b92-137">添付ファイルのレイアウトを指定します。</span><span class="sxs-lookup"><span data-stu-id="10b92-137">Specifies the layout of the attachments.</span></span> <span data-ttu-id="10b92-138">種類`result`の応答に使用されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-138">Used for responses of type `result`.</span></span> <br><span data-ttu-id="10b92-139">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="10b92-139">Currently the following types are supported:</span></span> <br><span data-ttu-id="10b92-140">`list`: サムネイル、タイトル、テキストフィールドを含む card オブジェクトのリスト</span><span class="sxs-lookup"><span data-stu-id="10b92-140">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="10b92-141">`grid`: サムネイル画像のグリッド</span><span class="sxs-lookup"><span data-stu-id="10b92-141">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="10b92-142">有効な attachment オブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="10b92-142">Array of valid attachment objects.</span></span> <span data-ttu-id="10b92-143">種類`result`の応答に使用されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-143">Used for responses of type `result`.</span></span> <br><span data-ttu-id="10b92-144">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="10b92-144">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="10b92-145">推奨されるアクション。</span><span class="sxs-lookup"><span data-stu-id="10b92-145">Suggested actions.</span></span> <span data-ttu-id="10b92-146">種類`auth`または`config`の応答に使用されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-146">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="10b92-147">表示するメッセージ。</span><span class="sxs-lookup"><span data-stu-id="10b92-147">Message to display.</span></span> <span data-ttu-id="10b92-148">種類`message`の応答に使用されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-148">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="10b92-149">応答カードの種類とプレビュー</span><span class="sxs-lookup"><span data-stu-id="10b92-149">Response card types and previews</span></span>

<span data-ttu-id="10b92-150">次の種類の添付ファイルがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="10b92-150">We support the following attachment types:</span></span>

* [<span data-ttu-id="10b92-151">サムネイルカード</span><span class="sxs-lookup"><span data-stu-id="10b92-151">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="10b92-152">英雄カード</span><span class="sxs-lookup"><span data-stu-id="10b92-152">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="10b92-153">Office 365 コネクタカード</span><span class="sxs-lookup"><span data-stu-id="10b92-153">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="10b92-154">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="10b92-154">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="10b92-155">概要については、「[カードとは](~/task-modules-and-cards/what-are-cards.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10b92-155">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="10b92-156">サムネイルおよびヒーローカードの種類を使用する方法については、「[カードおよびカードのアクションを追加](~/task-modules-and-cards/cards/cards-actions.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10b92-156">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="10b92-157">Office 365 コネクタカードに関するその他のドキュメントについては、「 [office 365 コネクタカードの使用](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10b92-157">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="10b92-158">結果リストは、Microsoft Teams UI に各アイテムのプレビューと共に表示されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-158">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="10b92-159">プレビューは、次の2つの方法のいずれかで生成されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-159">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="10b92-160">`attachment`オブジェクト内で`preview`プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="10b92-160">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="10b92-161">添付`preview`ファイルには、ヒーローまたはサムネイルカードのみを指定できます。</span><span class="sxs-lookup"><span data-stu-id="10b92-161">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="10b92-162">添付ファイルの基本`title`、 `text`、および`image`プロパティから抽出されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-162">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="10b92-163">これらのプロパティは、 `preview`プロパティが設定されておらず、これらのプロパティを使用できる場合にのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="10b92-163">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="10b92-164">そのプレビュープロパティを使用して、アダプティブカードまたは Office 365 のコネクタカードのプレビューを結果リストに表示することができます。</span><span class="sxs-lookup"><span data-stu-id="10b92-164">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list simply by its preview property.</span></span> <span data-ttu-id="10b92-165">結果が既にヒーローまたはサムネイルカードである場合は、この手順は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="10b92-165">This is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="10b92-166">プレビューの添付ファイルを使用する場合は、ヒーローまたは Thumbnail カードである必要があります。</span><span class="sxs-lookup"><span data-stu-id="10b92-166">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="10b92-167">Preview プロパティが指定されていない場合、カードのプレビューは失敗し、何も表示されません。</span><span class="sxs-lookup"><span data-stu-id="10b92-167">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="10b92-168">応答の例</span><span class="sxs-lookup"><span data-stu-id="10b92-168">Response example</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="10b92-169">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="10b92-169">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="10b92-170">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="10b92-170">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="10b92-171">JSON</span><span class="sxs-lookup"><span data-stu-id="10b92-171">JSON</span></span>](#tab/json)

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

## <a name="default-query"></a><span data-ttu-id="10b92-172">既定のクエリ</span><span class="sxs-lookup"><span data-stu-id="10b92-172">Default query</span></span>

<span data-ttu-id="10b92-173">マニフェスト内に`initialRun`が`true`設定されている場合、Microsoft Teams は、ユーザーが最初にメッセージング拡張機能を開いたときに "既定" クエリを発行します。</span><span class="sxs-lookup"><span data-stu-id="10b92-173">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="10b92-174">サービスは、このクエリに対して事前に設定された一連の結果で応答できます。</span><span class="sxs-lookup"><span data-stu-id="10b92-174">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="10b92-175">これは、検索コマンドが認証または構成を必要とし、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="10b92-175">This can be useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="10b92-176">既定のクエリは、通常のユーザークエリと同じ構造を持って`name`おり`initialRun` `value` 、フィールドはに設定`true`され、以下のオブジェクトと同様に設定されています。</span><span class="sxs-lookup"><span data-stu-id="10b92-176">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as in the object below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="10b92-177">次のステップ</span><span class="sxs-lookup"><span data-stu-id="10b92-177">Next Steps</span></span>

<span data-ttu-id="10b92-178">認証または構成を追加する</span><span class="sxs-lookup"><span data-stu-id="10b92-178">Add authentication and/or configuration</span></span>

* [<span data-ttu-id="10b92-179">メッセージング拡張機能に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="10b92-179">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="10b92-180">メッセージング拡張機能に構成を追加する</span><span class="sxs-lookup"><span data-stu-id="10b92-180">Add configuration to a messaging extension</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="10b92-181">構成の展開</span><span class="sxs-lookup"><span data-stu-id="10b92-181">Deploy configuration</span></span>

* [<span data-ttu-id="10b92-182">アプリパッケージを展開する</span><span class="sxs-lookup"><span data-stu-id="10b92-182">Deploy your app package</span></span>](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
