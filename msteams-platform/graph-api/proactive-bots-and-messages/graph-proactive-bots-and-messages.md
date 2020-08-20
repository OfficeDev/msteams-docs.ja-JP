---
title: Microsoft Graph を使用して、Teams でプロアクティブ ボット インストールとメッセージングを有効にする
description: Teams のプロアクティブ メッセージングと実装方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams プロアクティブなメッセージング チャットのインストール Graph
ms.openlocfilehash: b601c5858e5141ce81985dca62968b1713e1d2ba
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819162"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>Microsoft Graph を使用して Teams のプロアクティブ ボットのインストールとプロアクティブなメッセージングを有効にする (パブリック プレビュー)

>[!IMPORTANT]
> Microsoft Graph と Microsoft Teams のパブリック プレビューは、すでにアクセスしてフィードバックを行います。 このリリースは、拡張的なテストを受けてきてきてきませんが、運用環境での使用を意図したものではありません。

## <a name="proactive-messaging-in-teams"></a>Teams でのプロアクティブ メッセージング

ユーザーとの会話を開始するために、プロアクティブ メッセージがボットによって開始されます。 ウェルカム メッセージの送信、アンケートや投資の実行、組織全体の通知のブロードキャストなど、多くの目的に使用できます。  Teams のプロアクティブ メッセージは、アドホックまたは**ダイアログ ベースの会話****として配信**できます。

|メッセージ型 | Description |
|----------------|-------------- |
|アドホックのプロアクティブ メッセージ| ボットは会話フローを中断することなくメッセージを挿入します。|
|ダイアログベースのプロアクティブ メッセージ | ボットは新しいダイアログ スレッドを作成し、会話の制御を取得し、プロアクティブ メッセージを配信し、コントロールを閉じて前のダイアログに制御を返します。|

*「ユーザー* [SDK v4 へのプロアクティブ通知の送信」をご覧ください。](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)

## <a name="proactive-app-installation-in-teams"></a>Teams でのアプリのプロアクティブなインストール

ボットがユーザーにプロアクティブにメッセージを送信するには、その前に、個人用アプリとして、またはユーザーがメンバーであるチームにインストールする必要があります。 場合によっては、インストールしていない、または以前にアプリを操作した _ユーザーにメッセージ_ を、表示しないように促す必要があります。 たとえば、組織内のすべてのユーザーに対して、必要な情報をメッセージで送信する必要があります。 そのようなシナリオでは、Microsoft Graph API を使用して、ユーザー用にボットをプロアクティブにインストールできます。

## <a name="permissions"></a>アクセス許可

Microsoft Graph [teamsAppInstallation リソースの種類の](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) アクセス許可を使用すると、Microsoft Teams プラットフォーム内のすべてのユーザー (個人) またはチーム (チャネル) スコープに対するアプリのインストール ライフサイクルを管理できます。

|アプリケーションのアクセス許可 | Description|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|以前のサインインや使用をすることなく、Teams アプリで、すべてのユーザーに対してそれ **自体の**読み取り、インストール、アップグレード、アンインストールを行うことができます。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Teams アプリで、以前のサインインや使用をせずに、任意のチームでそれ自体の読み **取**り、インストール、アップグレード、アンインストールを行うことができます。|

これらのアクセス許可を使用するには、次の値 [を使用して、アプリ](../../resources/schema/manifest-schema.md#webapplicationinfo) マニフェストに webApplicationInfo キーを追加する必要があります。
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id**  — Azure AD アプリ ID。
> * **resource** — アプリのリソース URL。
>

>[!NOTE]
>
> * ボットのインストール_は、ユーザー__に代用するもの_ではありませんが、他のユーザーに対してはインストールされないため、アプリケーションには、ユーザーに委任されたアクセス許可が必要です。
>
> * テナント管理者が Azure ADは、アプリケーション [にアクセス許可を明示的に付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。 アプリケーションにアクセス許可が付与されると _、テナント_ テナントのすべてのメンバーにADアクセス許可が付与されます。

## <a name="enable-proactive-app-installation-and-messaging"></a>プロアクティブ アプリのインストールとメッセージングを有効にする

 > [!IMPORTANT]
>Microsoft Graph は、組織のアプリ カタログ内または AppSource 内に [公開された](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) アプリのみを [インストールします](https://appsource.microsoft.com/)。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ Teams のプロアクティブ メッセージング ボットを作成して公開する

開始するには、プロアクティブ メッセージング機能を使用し、[proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md)組織のアプリ カタログまたは[published](../../concepts/deploy-and-publish/overview.md)AppSource で公開[される Teams](../../bots/how-to/create-a-bot-for-teams.md) [用ボ](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)ットが[必要です](https://appsource.microsoft.com/)。

>[!TIP]
> 運用環境に適した [**会社のCommunicator、**](../..//samples/app-templates.md#company-communicator) ブロードキャスト メッセージングを有効にして、プロアクティブなボット アプリケーションを構築するための基盤になります。

### <a name="-get-the-teamsappid-for-your-app"></a>✔アプリを `teamsAppId` 取得する

**1.** 次の `teamsAppId`  手順に進んでください。

組織 `teamsAppId` のアプリ カタログから取得できます。

**Microsoft Graph ページ リファレンス:** [teamsApp リソース タイプ](/graph/api/resources/teamsapp?view=graph-rest-1.0)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

要求はオブジェクトを返 `teamsApp`  します。 返されたオブジェクトのカタログ `id`  は、アプリのカタログに生成されたアプリ ID で、Teams アプリ マニフェストに指定した "id:" とは異なります。

```json
{
  "value": [
    {
      "id": "b1c5353a-7aca-41b3-830f-27d5218fe0e5",
      "externalId": "f31b1263-ba99-435a-a679-911d24850d7c",
      "name": "Test App",
      "version": "1.0.1",
      "distributionMethod": "Organization"
    }
  ]
}
```

**2.**  個人用スコープでユーザーのアプリが既にアップロードまたはサイドローディングされている場合は、次のように `teamsAppId` して取得できます。

**Microsoft Graph ページ リファレンス: ユーザーにインストール**[されたアプリを一覧表示する](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** チームのスコープでチャネル用にアプリが既にアップロードまたはサイドロードされている場合は、次のように `teamsAppId` して取得できます。

**Microsoft Graph ページ リファレンス:** [チーム内のアプリを一覧表示する](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0)オブジェクトのいずれかのフィールドでフィルター処理して結果リストを絞り込むことができます。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔メッセージ受信者にボットが現在インストールされているかどうかを確認する

**Microsoft Graph ページ リファレンス: ユーザーにインストール**[されたアプリを一覧表示する](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

この要求は、アプリがインストールされていない場合は空の配列を返し、インストールされている [場合は、単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) オブジェクトの配列を返します。

### <a name="-install-your-app"></a>✔をインストールする

**Microsoft Graph リファレンス: ユーザー**[用アプリをインストールする](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP POST** 要求:

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

ユーザーが Microsoft Teams を実行している場合は、アプリのインストールがすぐに表示される可能性があります。 または、インストール済みアプリを表示するには、再起動が必要になる場合があります。

### <a name="-retrieve-the-conversation-chatid"></a>✔ **chatId を取得する**

アプリがユーザー用にインストールされると、ボットはイベント通知を受け取り、プロアクティブ メッセージを `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)送信するために必要な情報が含まれます。

`chatId`次のように取得できる。

**Microsoft Graph リファレンス:** [チャットを取得する](/graph/api/chat-get?view=graph-rest-beta&tabs=http)

**1.** アプリが必要になります `{teamsAppInstallationId}` 。 使用しない場合は、以下を使用します。

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

応答 **の id** プロパティは次の場所です `teamsAppInstallationId` 。

**2. 次** のような要求を行ってフェッチします `chatId` 。

**HTTP GET 要求** (アクセス許可 `TeamsAppInstallation.ReadWriteSelfForUser.All` —  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

応答 **の id** プロパティは次の場所です `chatId` 。

または、次の要求で `chatId`  取得できますが、より広範なアクセス許可が必要 `Chat.Read.All` になります。

**HTTP GET 要求** (アクセス許可 `Chat.Read.All` —

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔アクティブ メッセージを送信する

ユーザーまたはチームにボットが追加され、必要なユーザー情報を取得したら、プロアクティブ メッセージ [を送信できるようになります](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)。

# <a name="c--net"></a>[C# / .NET](#tab/csharp)

次のコード スニペットは [、Microsoft Bot Framework Samples for C# のサンプルのスニペットです。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

```csharp
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Bot.Builder;
using Microsoft.Bot.Schema;

namespace Microsoft.BotBuilderSamples
{
    public class ProactiveBot : ActivityHandler
    {
        // Message to send to users when the bot receives a Conversation Update event
        private const string WelcomeMessage = "Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.";

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

        public ProactiveBot(ConcurrentDictionary<string, ConversationReference> conversationReferences)
        {
            _conversationReferences = conversationReferences;
        }

        private void AddConversationReference(Activity activity)
        {
            var conversationReference = activity.GetConversationReference();
            _conversationReferences.AddOrUpdate(conversationReference.User.Id, conversationReference, (key, newValue) => conversationReference);
        }

        protected override Task OnConversationUpdateActivityAsync(ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            return base.OnConversationUpdateActivityAsync(turnContext, cancellationToken);
        }

        protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            foreach (var member in membersAdded)
            {
                // Greet anyone that was not the target (recipient) of this message.
                if (member.Id != turnContext.Activity.Recipient.Id)
                {
                    await turnContext.SendActivityAsync(MessageFactory.Text(WelcomeMessage), cancellationToken);
                }
            }
        }

        protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            // Echo back what the user said
            await turnContext.SendActivityAsync(MessageFactory.Text($"You sent '{turnContext.Activity.Text}'"), cancellationToken);
        }
    }
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

次のコード スニペットは [、JavaScript 用 Microsoft Bot Framework サンプルのものです](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。

```javascript
const { ActivityHandler, TurnContext } = require('botbuilder');

class ProactiveBot extends ActivityHandler {
    constructor(conversationReferences) {
        super();

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        this.conversationReferences = conversationReferences;

        this.onConversationUpdate(async (context, next) => {
            this.addConversationReference(context.activity);

            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (let cnt = 0; cnt < membersAdded.length; cnt++) {
                if (membersAdded[cnt].id !== context.activity.recipient.id) {
                    const welcomeMessage = 'Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.';
                    await context.sendActivity(welcomeMessage);
                }
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });

        this.onMessage(async (context, next) => {
            this.addConversationReference(context.activity);

            // Echo back what the user said
            await context.sendActivity(`You sent '${ context.activity.text }'`);
            await next();
        });
    }

    addConversationReference(activity) {
        const conversationReference = TurnContext.getConversationReference(activity);
        this.conversationReferences[conversationReference.conversation.id] = conversationReference;
    }
}

module.exports.ProactiveBot = ProactiveBot;

```
---

## <a name="related-topic-for-teams-administrators"></a>Teams 管理者向けの関連トピック
>
> [!div class="nextstepaction"]
> [**Microsoft Teams でアプリのセットアップ ポリシーを管理する**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>その他のコード サンプルを表示する
>
> [!div class="nextstepaction"]
> [**Teams のプロアクティブなメッセージング コード サンプル**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
