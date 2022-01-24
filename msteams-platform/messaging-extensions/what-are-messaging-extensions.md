---
title: メッセージング拡張機能
author: surbhigupta
description: Microsoft Teams プラットフォームでのメッセージング拡張機能の概要
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 975a51850e7e9d0049de46fc8d77016166ffedab
ms.sourcegitcommit: 55d4b4b721a33bacfe503bc646b412f0e3b0203e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2022
ms.locfileid: "62185450"
---
# <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージング拡張機能を使用すると、ユーザーはクライアント内のボタンとフォームを介して web サービスとMicrosoft Teamsできます。 ユーザーは、作成メッセージ領域、コマンド ボックス、またはメッセージから直接、外部システムでアクションを検索または開始できます。 その操作の結果を、リッチ形式のカードMicrosoft Teamsクライアントに返送できます。 このドキュメントでは、メッセージング拡張機能の概要、さまざまなシナリオで実行されるタスク、メッセージング拡張機能の作業、アクションと検索コマンド、リンク解除について説明します。

次の図は、メッセージング拡張機能が呼び出される場所を表示します。

![メッセージング拡張機能の呼び出し場所](~/assets/images/messaging-extension-invoke-locations.png)

> [!NOTE]
> @mentioning作成ボックスでは、メッセージ拡張機能がサポートされなくなりました。

## <a name="scenarios-where-messaging-extensions-are-used"></a>メッセージング拡張機能が使用されるシナリオ

| シナリオ | 例 |
|:-----------------|:-----------------|
|一部の外部システムでアクションを実行し、アクションの結果を会話に戻す必要があります。|リソースを予約し、チャネルが予約されたタイム スロットを知るのを許可します。|
|外部システムで何かを見つけて、その結果を会話と共有します。|グループ内の作業項目をAzure DevOps、アダプティブ カードとしてグループと共有します。|
|外部システムで複数の手順または多数の情報を含む複雑なタスクを完了し、その結果を会話と共有します。|Teams メッセージに基づいて追跡システムにバグを作成し、そのバグを Bob に割り当て、そのバグの詳細を示すカードをスレッドに送信します。|

## <a name="understand-how-messaging-extensions-work"></a>メッセージング拡張機能の動作を理解する

メッセージング拡張機能は、ホストする Web サービスとアプリ マニフェストで構成され、web サービスがクライアントで呼び出される場所をMicrosoft Teamsします。 Web サービスは、ボット フレームワークのメッセージング スキーマとセキュリティで保護された通信プロトコルを利用します。そのため、Web サービスをボット フレームワークにボットとして登録する必要があります。 

> [!NOTE]
> Web サービスを手動で作成することもできますが、 [ボット フレームワーク SDK を使用](https://github.com/microsoft/botframework-sdk) してプロトコルを操作します。

アプリのアプリ マニフェストMicrosoft Teams、最大 10 個の異なるコマンドで 1 つのメッセージング拡張機能が定義されます。 各コマンドは、アクションや検索などの種類と、呼び出されたクライアント内の場所を定義します。 呼び出し場所は、メッセージ領域、コマンド バー、およびメッセージを作成します。 呼び出し時に、Web サービスは、関連するすべての情報を含む JSON ペイロードを含む HTTPS メッセージを受信します。 JSON ペイロードを使用して応答し、Teamsが次の対話を有効にすることを知る。 

## <a name="types-of-messaging-extension-commands"></a>メッセージング拡張機能のコマンドの種類

メッセージング拡張機能コマンドには、アクション コマンドと検索コマンドの 2 種類があります。 メッセージング拡張機能コマンドの種類は、Web サービスで使用できる UI 要素と対話フローを定義します。 認証や構成などの一部の操作は、両方の種類のコマンドで使用できます。

### <a name="action-commands"></a>操作コマンド

アクション コマンドは、ユーザーにモーダル ポップアップを表示して情報を収集または表示するために使用します。 ユーザーがフォームを送信すると、Web サービスはメッセージを会話に直接挿入するか、メッセージを作成メッセージ領域に挿入して応答します。 その後、ユーザーはメッセージを送信できます。 複数のフォームを連鎖して、より複雑なワークフローを作成できます。

アクション コマンドは、作成メッセージ領域、コマンド ボックス、またはメッセージからトリガーされます。 コマンドがメッセージから呼び出されると、ボットに送信される最初の JSON ペイロードには、呼び出されたメッセージ全体が含まれます。 次の図は、メッセージング拡張機能アクション コマンド タスク モジュールを表示します。 ![ メッセージング拡張機能アクション コマンド タスク モジュール](~/assets/images/task-module.png)

### <a name="search-commands"></a>検索コマンド

検索コマンドを使用すると、ユーザーは、検索ボックスを介して手動で、または監視対象ドメインへのリンクを作成メッセージ領域に貼り付け、検索の結果をメッセージに挿入することで、外部システムを検索できます。 最も基本的な検索コマンド フローでは、最初の呼び出しメッセージには、ユーザーが送信した検索文字列が含まれます。 カードとカードのプレビューの一覧で応答します。 クライアントTeamsは、ユーザーのカード プレビューの一覧を表示します。 ユーザーがリストからカードを選択すると、フルサイズのカードが作成メッセージ領域に挿入されます。

カードは、メッセージの作成領域またはコマンド ボックスからトリガーされ、メッセージからトリガーされません。 メッセージからトリガーできない。
次の図は、メッセージング拡張機能の検索コマンド タスク モジュールを表示します。

![メッセージング拡張機能の検索コマンド](~/assets/images/search-extension.png)

> [!NOTE]
> カードの詳細については、「カードは [何か」を参照してください](../task-modules-and-cards/what-are-cards.md)。

## <a name="link-unfurling"></a>リンク展開

Web サービスは、作成メッセージ領域に URL を貼り付けするときに呼び出されます。 この機能は、リンク解除と呼ばれる機能です。 特定のドメインを含む URL を作成メッセージ領域に貼り付けるときに、呼び出しを受信するためにサブスクライブできます。 お客様の Web サービスは、URL を詳細情報が記載されたカードに "展開" することができ、そのカードでは標準的な Web サイトのプレビュー カードよりも多くの情報を提供できます。 ボタンを追加すると、ユーザーがクライアントから離れることなく、すぐにMicrosoft Teamsできます。
次の画像は、メッセージング拡張機能にリンクを貼り付けするときにリンクの分岐解除機能を表示します。
 
![unfurl リンク](../assets/images/messaging-extension/unfurl-link.png)

![リンクのリンク解除](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-snippets"></a>コード スニペット

次のコードは、メッセージング拡張機能に基づくアクションの例を示しています。

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

次のコードは、メッセージング拡張機能に基づく検索の例を示しています。

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
| アクションベースのコマンドを使用したメッセージング拡張機能 | このサンプルは、アクション ベースのメッセージング拡張機能を構築する方法を示しています。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| 検索ベースのコマンドを使用したメッセージング拡張機能 | このサンプルは、検索ベースのメッセージング拡張機能を構築する方法を示しています。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|タスクのスケジュールに関するメッセージング拡張機能アクション|このサンプルは、メッセージング拡張機能アクション コマンドからタスクをスケジュールし、スケジュールされた日時にリマインダー カードを取得する方法を示しています。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)|

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アクション メッセージング拡張機能のコマンドを定義する](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>関連項目

* [検索メッセージング拡張機能のコマンドを定義する](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [メッセージング拡張機能を作成する](../build-your-first-app/build-messaging-extension.md)