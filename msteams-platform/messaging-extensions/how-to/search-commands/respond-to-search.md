---
title: 検索コマンドに応答する
author: clearab
description: Microsoft Teams アプリのメッセージング拡張機能から検索コマンドに応答する方法。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 2cc53796deddb47e8dbce86a5b02f4d80a1b91e0
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696193"
---
# <a name="respond-to-search-command"></a><span data-ttu-id="d2959-103">検索コマンドに応答する</span><span class="sxs-lookup"><span data-stu-id="d2959-103">Respond to search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="d2959-104">ユーザーが検索コマンドを送信すると、Web サービスは、検索パラメーターを持つオブジェクトを含む呼び出し `composeExtension/query` `value` メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="d2959-104">After the user submits the search command, your web service receives a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="d2959-105">この呼び出しは、次の条件でトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="d2959-105">This invoke is triggered with the following conditions:</span></span>

* <span data-ttu-id="d2959-106">検索ボックスに文字が入力されます。</span><span class="sxs-lookup"><span data-stu-id="d2959-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="d2959-107">`initialRun` がアプリ マニフェストで true に設定されている場合、検索コマンドが呼び出されるとすぐに呼び出しメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d2959-107">`initialRun` is set to true in your app manifest, you receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="d2959-108">詳細については、「既定のクエリ [」を参照してください](#default-query)。</span><span class="sxs-lookup"><span data-stu-id="d2959-108">For more information, see [default query](#default-query).</span></span>

<span data-ttu-id="d2959-109">このドキュメントでは、カードとプレビューの形式でユーザー要求に応答する方法と、Microsoft Teams が既定のクエリを発行する条件について説明します。</span><span class="sxs-lookup"><span data-stu-id="d2959-109">This document guides you on how to respond to user requests in the form of cards and previews, and the conditions under which Microsoft Teams issues a default query.</span></span>

<span data-ttu-id="d2959-110">要求パラメーターは、次の `value` プロパティを含む要求内のオブジェクトに含まれています。</span><span class="sxs-lookup"><span data-stu-id="d2959-110">The request parameters are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="d2959-111">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="d2959-111">Property name</span></span> | <span data-ttu-id="d2959-112">用途</span><span class="sxs-lookup"><span data-stu-id="d2959-112">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="d2959-113">アプリ マニフェストで宣言されているコマンドの 1 つと一致する、ユーザーによって呼び出されるコマンドの名前。</span><span class="sxs-lookup"><span data-stu-id="d2959-113">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="d2959-114">パラメーターの配列。</span><span class="sxs-lookup"><span data-stu-id="d2959-114">Array of parameters.</span></span> <span data-ttu-id="d2959-115">各パラメーター オブジェクトには、ユーザーが指定したパラメーター値と共に、パラメーター名が含まれる。</span><span class="sxs-lookup"><span data-stu-id="d2959-115">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="d2959-116">ページネーション パラメーター:</span><span class="sxs-lookup"><span data-stu-id="d2959-116">Pagination parameters:</span></span> <br><span data-ttu-id="d2959-117">`skip`: このクエリのスキップ カウント</span><span class="sxs-lookup"><span data-stu-id="d2959-117">`skip`: Skip count for this query</span></span> <br><span data-ttu-id="d2959-118">`count`: 返す要素の数。</span><span class="sxs-lookup"><span data-stu-id="d2959-118">`count`: Number of elements to return.</span></span> |

# <a name="cnet"></a>[<span data-ttu-id="d2959-119">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d2959-119">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="d2959-120">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="d2959-120">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[<span data-ttu-id="d2959-121">JSON</span><span class="sxs-lookup"><span data-stu-id="d2959-121">JSON</span></span>](#tab/json)

<span data-ttu-id="d2959-122">以下の JSON は、最も関連性の高いセクションを強調表示するために短縮されています。</span><span class="sxs-lookup"><span data-stu-id="d2959-122">The JSON below is shortened to highlight the most relevant sections.</span></span>

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

## <a name="respond-to-user-requests"></a><span data-ttu-id="d2959-123">ユーザー要求に応答する</span><span class="sxs-lookup"><span data-stu-id="d2959-123">Respond to user requests</span></span>

<span data-ttu-id="d2959-124">ユーザーがクエリを実行すると、Microsoft Teams はサービスに同期 HTTP 要求を発行します。</span><span class="sxs-lookup"><span data-stu-id="d2959-124">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="d2959-125">その時点で、要求に対する `5` HTTP 応答を提供する秒がコードに設定されています。</span><span class="sxs-lookup"><span data-stu-id="d2959-125">At that point, your code has `5` seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="d2959-126">この間、サービスは追加の参照、または要求を処理するために必要なその他のビジネス ロジックを実行できます。</span><span class="sxs-lookup"><span data-stu-id="d2959-126">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="d2959-127">サービスは、ユーザー クエリに一致する結果で応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d2959-127">Your service must respond with the results matching the user query.</span></span> <span data-ttu-id="d2959-128">応答は、HTTP 状態コードと、次のプロパティを持 `200 OK` つ有効なアプリケーションまたは JSON オブジェクトを示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d2959-128">The response must indicate an HTTP status code of `200 OK` and a valid application or JSON object with the following properties:</span></span>

|<span data-ttu-id="d2959-129">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="d2959-129">Property name</span></span>|<span data-ttu-id="d2959-130">用途</span><span class="sxs-lookup"><span data-stu-id="d2959-130">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="d2959-131">トップ レベルの応答エンベロープ。</span><span class="sxs-lookup"><span data-stu-id="d2959-131">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="d2959-132">応答の種類。</span><span class="sxs-lookup"><span data-stu-id="d2959-132">Type of response.</span></span> <span data-ttu-id="d2959-133">次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d2959-133">The following types are supported:</span></span> <br><span data-ttu-id="d2959-134">`result`: 検索結果の一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="d2959-134">`result`: Displays a list of search results</span></span> <br><span data-ttu-id="d2959-135">`auth`: ユーザーに認証を求める</span><span class="sxs-lookup"><span data-stu-id="d2959-135">`auth`: Asks the user to authenticate</span></span> <br><span data-ttu-id="d2959-136">`config`: メッセージング拡張機能のセットアップをユーザーに求める</span><span class="sxs-lookup"><span data-stu-id="d2959-136">`config`: Asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="d2959-137">`message`: テキスト形式のメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="d2959-137">`message`: Displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="d2959-138">添付ファイルのレイアウトを指定します。</span><span class="sxs-lookup"><span data-stu-id="d2959-138">Specifies the layout of the attachments.</span></span> <span data-ttu-id="d2959-139">型の応答に使用されます `result` 。</span><span class="sxs-lookup"><span data-stu-id="d2959-139">Used for responses of type `result`.</span></span> <br><span data-ttu-id="d2959-140">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d2959-140">Currently, the following types are supported:</span></span> <br><span data-ttu-id="d2959-141">`list`: サムネイル、タイトル、テキスト フィールドを含むカード オブジェクトの一覧</span><span class="sxs-lookup"><span data-stu-id="d2959-141">`list`: A list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="d2959-142">`grid`: サムネイル画像のグリッド</span><span class="sxs-lookup"><span data-stu-id="d2959-142">`grid`: A grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="d2959-143">有効な添付ファイル オブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="d2959-143">Array of valid attachment objects.</span></span> <span data-ttu-id="d2959-144">型の応答に使用されます `result` 。</span><span class="sxs-lookup"><span data-stu-id="d2959-144">Used for responses of type `result`.</span></span> <br><span data-ttu-id="d2959-145">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d2959-145">Currently, the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="d2959-146">推奨されるアクション。</span><span class="sxs-lookup"><span data-stu-id="d2959-146">Suggested actions.</span></span> <span data-ttu-id="d2959-147">型または . の応答に `auth` 使用 `config` されます。</span><span class="sxs-lookup"><span data-stu-id="d2959-147">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="d2959-148">表示するメッセージ。</span><span class="sxs-lookup"><span data-stu-id="d2959-148">Message to display.</span></span> <span data-ttu-id="d2959-149">型の応答に使用されます `message` 。</span><span class="sxs-lookup"><span data-stu-id="d2959-149">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="d2959-150">応答カードの種類とプレビュー</span><span class="sxs-lookup"><span data-stu-id="d2959-150">Response card types and previews</span></span>

<span data-ttu-id="d2959-151">Teams では、次のカードの種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d2959-151">Teams supports the following card types:</span></span>

* [<span data-ttu-id="d2959-152">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="d2959-152">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="d2959-153">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="d2959-153">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="d2959-154">Office 365 コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="d2959-154">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="d2959-155">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="d2959-155">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="d2959-156">カードの理解と概要を把握するには、カード [の概要を参照してください](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="d2959-156">To have a better understanding and overview on cards, see [what are cards](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="d2959-157">サムネイルカードとヒーロー カードの種類を使用する方法については、「Add [card and card actions」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="d2959-157">To learn how to use the thumbnail and hero card types, see [add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="d2959-158">365 コネクタ カードの詳細Office 365 コネクタ カードの使用Office [を参照してください](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="d2959-158">For additional information regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="d2959-159">結果の一覧が Microsoft Teams UI に表示され、各アイテムのプレビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d2959-159">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="d2959-160">プレビューは、次の 2 つの方法で生成されます。</span><span class="sxs-lookup"><span data-stu-id="d2959-160">The preview is generated in one of the two ways:</span></span>

* <span data-ttu-id="d2959-161">オブジェクト内 `preview` のプロパティを使用 `attachment` する。</span><span class="sxs-lookup"><span data-stu-id="d2959-161">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="d2959-162">添付 `preview` ファイルには、ヒーロー カードまたはサムネイル カードのみを指定できます。</span><span class="sxs-lookup"><span data-stu-id="d2959-162">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="d2959-163">添付ファイルの基本 `title` 、 `text` および `image` プロパティから抽出されます。</span><span class="sxs-lookup"><span data-stu-id="d2959-163">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="d2959-164">これらは、プロパティが設定されていない `preview` 場合にのみ使用され、これらのプロパティを使用できます。</span><span class="sxs-lookup"><span data-stu-id="d2959-164">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="d2959-165">アダプティブ カードまたは 365 コネクタ カードOfficeプレビュー プロパティを使用して、結果リストに表示できます。</span><span class="sxs-lookup"><span data-stu-id="d2959-165">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list using its preview property.</span></span> <span data-ttu-id="d2959-166">結果が既にヒーロー カードまたはサムネイル カードである場合、preview プロパティは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="d2959-166">The preview property is not necessary if the results are already Hero or Thumbnail cards.</span></span> <span data-ttu-id="d2959-167">プレビュー添付ファイルを使用する場合は、ヒーロー カードまたはサムネイル カードである必要があります。</span><span class="sxs-lookup"><span data-stu-id="d2959-167">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="d2959-168">preview プロパティを指定しない場合、カードのプレビューは失敗し、何も表示されません。</span><span class="sxs-lookup"><span data-stu-id="d2959-168">If no preview property is specified, the preview of the card fails and nothing is displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="d2959-169">応答の例</span><span class="sxs-lookup"><span data-stu-id="d2959-169">Response example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="d2959-170">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d2959-170">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="d2959-171">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="d2959-171">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="d2959-172">JSON</span><span class="sxs-lookup"><span data-stu-id="d2959-172">JSON</span></span>](#tab/json)

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

## <a name="default-query"></a><span data-ttu-id="d2959-173">既定のクエリ</span><span class="sxs-lookup"><span data-stu-id="d2959-173">Default query</span></span>

<span data-ttu-id="d2959-174">マニフェストで設定した場合、Microsoft Teams は、ユーザーが最初にメッセージング拡張機能を開くと既定 `initialRun` `true` のクエリを発行します。 </span><span class="sxs-lookup"><span data-stu-id="d2959-174">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a **default** query when the user first opens the messaging extension.</span></span> <span data-ttu-id="d2959-175">サービスは、事前に設定された結果のセットでこのクエリに応答できます。</span><span class="sxs-lookup"><span data-stu-id="d2959-175">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="d2959-176">これは、検索コマンドで認証または構成が必要な場合、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="d2959-176">This is useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="d2959-177">既定のクエリは、通常のユーザー クエリと同じ構造を持ち、フィールドを次のオブジェクトに示すように設定 `name` `initialRun` `value` `true` します。</span><span class="sxs-lookup"><span data-stu-id="d2959-177">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as shown in the following object:</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="d2959-178">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="d2959-178">Code sample</span></span>

| <span data-ttu-id="d2959-179">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="d2959-179">Sample Name</span></span>           | <span data-ttu-id="d2959-180">説明</span><span class="sxs-lookup"><span data-stu-id="d2959-180">Description</span></span> | <span data-ttu-id="d2959-181">.NET</span><span class="sxs-lookup"><span data-stu-id="d2959-181">.NET</span></span>    | <span data-ttu-id="d2959-182">Node.js</span><span class="sxs-lookup"><span data-stu-id="d2959-182">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="d2959-183">Teams メッセージング拡張機能アクション</span><span class="sxs-lookup"><span data-stu-id="d2959-183">Teams messaging extension action</span></span>| <span data-ttu-id="d2959-184">アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d2959-184">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="d2959-185">View</span><span class="sxs-lookup"><span data-stu-id="d2959-185">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="d2959-186">View</span><span class="sxs-lookup"><span data-stu-id="d2959-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="d2959-187">Teams メッセージング拡張機能の検索</span><span class="sxs-lookup"><span data-stu-id="d2959-187">Teams messaging extension search</span></span>   |  <span data-ttu-id="d2959-188">検索コマンドを定義し、検索に応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d2959-188">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="d2959-189">View</span><span class="sxs-lookup"><span data-stu-id="d2959-189">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="d2959-190">View</span><span class="sxs-lookup"><span data-stu-id="d2959-190">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="d2959-191">関連項目</span><span class="sxs-lookup"><span data-stu-id="d2959-191">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2959-192">メッセージング拡張機能に構成を追加する</span><span class="sxs-lookup"><span data-stu-id="d2959-192">Add configuration to a messaging extension</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)
 
## <a name="next-step"></a><span data-ttu-id="d2959-193">次の手順</span><span class="sxs-lookup"><span data-stu-id="d2959-193">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2959-194">メッセージング拡張機能に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="d2959-194">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)



