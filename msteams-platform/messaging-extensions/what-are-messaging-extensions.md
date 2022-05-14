---
title: メッセージの拡張機能
author: surbhigupta
description: Microsoft Teams プラットフォームでのメッセージング拡張機能の概要
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 54c0ce0139f6d70aca0c002edff2c60065c48b7b
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2022
ms.locfileid: "65297143"
---
# <a name="message-extensions"></a>メッセージの拡張機能

メッセージ拡張機能を使用すると、ユーザーは、Microsoft Teams クライアントのボタンとフォームを使用して Web サービスを操作することができます。 ユーザーは、外部システムのメッセージ作成領域、コマンド ボックスから、またはメッセージから直接、操作を検索したり、開始したりできます。 その操作の結果を、リッチに書式設定されたカードとして Microsoft Teams クライアントに送信できます。

このドキュメントでは、メッセージ拡張機能、さまざまなシナリオで実行されるタスク、メッセージ拡張機能の動作、操作コマンドと検索コマンド、リンク展開の概要について説明します。

次の画像は、メッセージ拡張機能が呼び出される場所を示しています。

:::image type="content" source="~/assets/images/messaging-extension-invoke-locations.png" alt-text="メッセージ拡張機能の呼び出し場所":::

> [!NOTE]
> @メンション メッセージ拡張機能は、作成ボックスではサポートされなくなりました。

## <a name="scenarios-where-message-extensions-are-used"></a>メッセージ拡張機能が使用されるシナリオ

| シナリオ | 例 |
|:-----------------|:-----------------|
|操作を行うために外部システムが必要で、その操作の結果を会話に送り返したい。|リソースの予約、予約されたタイム スロットをチャネルに知らせます。|
|外部システムで何かを見つける必要があり、その結果を会話で共有したい。|Azure DevOps で作業項目を検索し、アダプティブ カードとしてグループと共有します。|
|外部システムで複数の手順 または多くの情報を含む複雑なタスクを完了させる必要があり、その結果を会話で共有したい。|Teams のメッセージに基づいてトラッキング システムにバグを作成し、そのバグを Bob に割り当て、そのバグの詳細情報が記載されたカードを会話スレッドに送信します。|

## <a name="understand-how-message-extensions-work"></a>メッセージ拡張機能のしくみを理解する

メッセージ拡張機能は、ホストする Web サービスとアプリのマニフェストによって構成されています。このマニフェストによって、Microsoft Teams クライアント内のどこから Web サービスを呼び出すかが定義されます。 Web サービスは Bot Framework のメッセージング スキーマとセキュリティで保護された通信プロトコルを利用するので、Web サービスを Bot Framework でボットとして登録する必要があります。

> [!NOTE]
> Web サービスは手動で作成できますが、[Bot Framework SDK](https://github.com/microsoft/botframework-sdk) を使用してプロトコルを操作してください。

Microsoft Teams アプリのアプリ マニフェストでは、最大 10 個の異なるコマンドを使用して 1 つのメッセージ拡張機能が定義されます。 各コマンドは、操作や検索などの種類と、呼び出されたクライアント内の場所を定義します。 呼び出し場所は、メッセージ作成領域、コマンド バー、およびメッセージです。 呼び出し時に、Web サービスは、すべての関連情報を持つ JSON ペイロードを含む HTTPS メッセージを受信します。 JSON ペイロードを使用して応答し、有効にする次の対話を Teams クライアントが認識できるようにします。

## <a name="types-of-message-extension-commands"></a>メッセージ拡張機能のコマンドの種類

メッセージ拡張機能のコマンドには、操作コマンドと検索コマンドの 2 種類があります。 メッセージ拡張機能のコマンドの種類は、Web サービスで利用可能な UI 要素と操作フローを定義します。 認証や構成などの一部の操作は、どちらの種類のコマンドでも利用可能です。

### <a name="action-commands"></a>操作コマンド

操作コマンドは、情報を収集または表示するためのモーダル ポップアップをユーザーに表示するために使用されます。 ユーザーがフォームを送信すると、Web サービスはメッセージを会話に直接挿入するか、またはメッセージ作成領域にメッセージを挿入することで応答します。 その後、ユーザーはメッセージを送信できます。 複数のフォームをチェーン化して、より複雑なワークフローを実現することができます。

操作コマンドは、メッセージの作成領域、コマンド ボックス、またはメッセージからトリガーされます。 コマンドがメッセージから呼び出される場合、ボットに送信される最初の JSON ペイロードには、呼び出されたメッセージ全体が含まれます。 次の画像は、メッセージ拡張機能アクション コマンド タスク モジュールを示しています。

:::image type="content" source="~/assets/images/task-module.png" alt-text="メッセージ拡張機能アクション コマンド タスク モジュール":::

### <a name="search-commands"></a>検索コマンド

検索コマンドを使用すると、ユーザーは検索ボックスを使用して手動で、または監視対象ドメインへのリンクをメッセージの作成領域に貼り付けて外部システムの情報を検索し、検索結果をメッセージに挿入できます。 最も基本的な検索コマンドのフローでは、ユーザーが送信した検索文字列が最初の呼び出しメッセージに含まれています。 カードのリストとカードのプレビューで応答します。 Teams クライアントは、ユーザーのカード プレビューのリストをレンダリングします。 ユーザーがリストからカードを選択すると、フルサイズのカードがメッセージ作成領域に挿入されます。

カードは、メッセージ作成領域、コマンド ボックス、またはメッセージからトリガーされ、メッセージからはトリガーされません。 メッセージからトリガーすることはできません。
次の画像は、メッセージ拡張機能検索コマンド タスク モジュールを示しています。

:::image type="content" source="~/assets/images/search-extension.png" alt-text="メッセージ拡張機能検索コマンド":::

> [!NOTE]
> カードの詳細については、「[カードとは](../task-modules-and-cards/what-are-cards.md)」を参照してください。

## <a name="link-unfurling"></a>リンク展開

Web サービスは、メッセージ作成領域に URL が貼り付けられたときに呼び出されます。 この機能は、リンク展開として知られています。 特定のドメインを含む URL がメッセージ作成領域に貼り付けられたときに、呼び出しを受け取るよう登録することができます。 お客様の Web サービスは、URL を詳細情報が記載されたカードに "展開" することができ、そのカードでは標準的な Web サイトのプレビュー カードよりも多くの情報を提供できます。 また、ボタンを追加して、ユーザーが Microsoft Teams クライアントから離脱することなくすぐにアクションを起こせるようにすることができます。
次の画像は、リンクがメッセージ拡張機能に貼り付けられたときのリンク展開機能を示しています。

:::image type="content" source="../assets/images/messaging-extension/unfurl-link.png" alt-text="リンクを展開する":::

![リンク展開](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-snippets"></a>コード スニペット

次のコードは、メッセージ拡張機能に基づく操作の例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

 protected override Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
        {
            // Handle different actions using switch
            switch (action.CommandId)
            {
                case "HTML":
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Height = 200,
                                Width = 400,
                                Title = "Task Module HTML Page",
                                Url = baseUrl + "/htmlpage.html",
                            },
                        },
                    };
                // return TaskModuleHTMLPage(turnContext, action);
                default:
                    string memberName = "";
                    var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
                    memberName = member.Name;
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Card = <<AdaptiveAction card json>>,
                                Height = 200,
                                Width = 400,
                                Title = $"Welcome {memberName}",
                            },
                        },
                    };
            }
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

    async handleTeamsMessagingExtensionFetchTask(context, action) {
        switch (action.commandId) {
            case 'Static HTML':
                return staticHtmlPage();
        }
    }

    staticHtmlPage(){
        return {
            task: {
                type: 'continue',
                value: {
                    width: 450,
                    height: 125,
                    title: 'Task module Static HTML',
                    url: `${baseurl}/StaticPage.html`
                }
            }
        };
    }

```

---

次のコードは、メッセージ拡張機能に基づく検索の例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
        {
            var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

            var packages = new[] {
            new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
            new { title = "Fluent UI Library", value = "FluentUI" }};

            // We take every row of the results and wrap them in cards wrapped in MessagingExtensionAttachment objects.
            // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
            var attachments = packages.Select(package =>
            {
                var previewCard = new ThumbnailCard { Title = package.title, Tap = new CardAction { Type = "invoke", Value = package } };
                if (!string.IsNullOrEmpty(package.title))
                {
                    previewCard.Images = new List<CardImage>() { new CardImage(package.title, "Icon") };
                }

                var attachment = new MessagingExtensionAttachment
                {
                    ContentType = HeroCard.ContentType,
                    Content = new HeroCard { Title = package.title },
                    Preview = previewCard.ToAttachment()
                };

                return attachment;
            }).ToList();

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

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;     
        const attachments = [];
                const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);
                
                response.data.objects.forEach(obj => {
                        const heroCard = CardFactory.heroCard(obj.package.name);
                        const preview = CardFactory.heroCard(obj.package.name);
                        preview.content.tap = { type: 'invoke', value: { description: obj.package.description } };
                        const attachment = { ...heroCard, preview };
                        attachments.push(attachment);
                });
    
                return {
                    composeExtension:  {
                           type: 'result',
                           attachmentLayout: 'list',
                           attachments: attachments
                    }
                };
            }       
        }
```

---

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|------------|-------------|----------------|------------|------------|
| 操作ベースのコマンドを使用したメッセージ拡張機能 | このサンプルは、操作ベースのメッセージ拡張機能を構築する方法を示しています。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| 検索ベースのコマンドを使用したメッセージ拡張機能 | このサンプルは、検索ベースのメッセージ拡張機能を構築する方法を示しています。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|タスク スケジュール用のメッセージ拡張機能操作|このサンプルは、メッセージ拡張機能操作コマンドからタスクをスケジュールし、スケジュールされた日時にリマインダー カードを取得する方法を示しています。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [メッセージ拡張機能の操作コマンドを定義する](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>関連項目

* [メッセージ拡張機能の検索コマンドを定義する](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [メッセージ拡張機能を作成する](../build-your-first-app/build-messaging-extension.md)
