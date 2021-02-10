---
title: Microsoft Graph を使用して Teams で事前ボットのインストールとメッセージングを有効にする
description: Teams でのプロアクティブ メッセージングと実装方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams のプロアクティブ メッセージング チャットのインストールのグラフ
ms.openlocfilehash: 4f26b4d2f4e82fcf50b7a35c46bcd07e5afecf19
ms.sourcegitcommit: b99ed616db734371e4af4594b7e895c5b05737c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2021
ms.locfileid: "50162895"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>Microsoft Graph を使用して Teams でプロアクティブ ボットのインストールとプロアクティブ メッセージングを有効にする (パブリック プレビュー)

>[!IMPORTANT]
> Microsoft Graph と Microsoft Teams のパブリック プレビューは、早期アクセスとフィードバックに利用できます。 このリリースでは広範なテストが実施されましたが、実稼働環境での使用を意図した方法ではありません。

## <a name="proactive-messaging-in-teams"></a>Teams でのプロアクティブ メッセージング

プロアクティブ メッセージは、ユーザーとの会話を開始するためにボットによって開始されます。 ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に対応します。  Teams のプロアクティブ メッセージは、アドホックまたはダイアログ ベースの **会話として配信** できます。

|メッセージ型 | 説明 |
|----------------|-------------- |
|臨時のプロアクティブ メッセージ| ボットは、会話フローを中断せずにメッセージを対話します。|
|ダイアログ ベースのプロアクティブ メッセージ | ボットは、新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じ、前のダイアログにコントロールを返します。|

*See* [,Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="proactive-app-installation-in-teams"></a>Teams でのアプリのプロアクティブ インストール

ボットが事前にユーザーにメッセージを送信するには、事前に個人用アプリとして、またはユーザーがメンバーであるチームにインストールする必要があります。 場合によっては、アプリをインストールしていないユーザーや以前にアプリとやり取りしていないユーザーに事前にメッセージを送信する必要があります。 たとえば、組織内のすべてのユーザーに重要な情報をメッセージ送信する必要があります。 このようなシナリオでは、Microsoft Graph API を使用して、ユーザーのボットを事前にインストールできます。

## <a name="permissions"></a>許可

Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) リソースの種類のアクセス許可を使用すると、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) スコープまたはチーム (チャネル) スコープに対するアプリのインストール ライフサイクルを管理できます。

|アプリケーションのアクセス許可 | 説明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Teams アプリは、事前サインインや使用なしで、任意のユーザーの読み取り、インストール、アップグレード、アンインストールを実行できます。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Teams アプリは、事前にサインインしたり使用したりすることなく、任意のチームで自身を読み取り、インストール、アップグレード、アンインストールできます。|

これらのアクセス許可を使用するには、次の値を使用して [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id**  — Azure ADアプリ ID。
> * **resource** — アプリのリソース URL。
>

>[!NOTE]
>
> * ボットでは、 _アプリケーションは_ ユーザー _によって委任_ されたアクセス許可を必要とします。これは、インストールは自分用ではなく、他のユーザー向けのためです。
>
> * Azure ADテナント管理者は、アプリケーションにアクセス [許可を明示的に付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。 アプリケーションにアクセス許可が付与された後、Azure AD テナントのすべてのメンバーに付与されたアクセス許可が付与されます。 

## <a name="enable-proactive-app-installation-and-messaging"></a>予防的なアプリのインストールとメッセージングを有効にする

 > [!IMPORTANT]
>Microsoft Graph は、組織のアプリ カタログ内または AppSource 内で [公開されている](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) アプリのみを [インストールします](https://appsource.microsoft.com/)。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ Teams 用のプロアクティブ メッセージング ボットを作成して発行する

To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with proactive [messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [in AppSource](https://appsource.microsoft.com/).

>[!TIP]
> 実稼働対応の [**Company Communicator**](../..//samples/app-templates.md#company-communicator) アプリ テンプレートは、ブロードキャスト メッセージングを有効にし、プロアクティブ ボット アプリケーションを構築する良い基盤です。

### <a name="-get-the-teamsappid-for-your-app"></a>✔アプリを `teamsAppId` 取得する

**1.** 次の手順 `teamsAppId`  が必要です。

組織 `teamsAppId` のアプリ カタログから取得できます。

**Microsoft Graph ページ リファレンス:** [teamsApp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

要求はオブジェクトを返 `teamsApp`  します。 返されるオブジェクトは、アプリのカタログによって生成されたアプリ ID であり、Teams アプリ マニフェストで指定した `id`  "id:" とは異なります。

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

**2.**  個人用スコープのユーザーに対してアプリが既にアップロードまたはサイドロードされている場合は、次の情報を `teamsAppId` 取得できます。

**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされたアプリを一覧表示する](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** チーム スコープのチャネルに対してアプリが既にアップロードまたはサイドロードされている場合は、次のように `teamsAppId` 取得できます。

**Microsoft Graph ページ リファレンス:** [チーム内のアプリを一覧表示する](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)オブジェクトの任意のフィールドにフィルターを適用して、結果の一覧を絞り込む。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔メッセージ受信者用にボットが現在インストールされているかどうかを確認する

**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされたアプリを一覧表示する](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

この要求は、アプリがインストールされていない場合は空の配列を返し、インストールされている場合は [単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列を返します。

### <a name="-install-your-app"></a>✔をインストールする

**Microsoft Graph ページ リファレンス:** [ユーザー用アプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** 要求:

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

ユーザーが Microsoft Teams を実行している場合、アプリがすぐにインストールされる可能性があります。 または、インストールされているアプリを表示するために再起動が必要になる場合があります。

### <a name="-retrieve-the-conversation-chatid"></a>✔ **chatId を取得する**

ユーザー用にアプリがインストールされている場合、ボットはプロアクティブ メッセージを送信するために必要な情報を含むイベント `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)通知を受け取ります。

次 `chatId` のように取得することもできます。

**Microsoft Graph ページ リファレンス:** [チャットを取得する](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** アプリが必要です `{teamsAppInstallationId}` 。 お持ちでない場合は、次のコマンドを使用します。

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

応答 **の id** プロパティは次の値です `teamsAppInstallationId` 。

**2. 次** の要求を行って、次の要求をフェッチします `chatId` 。

**HTTP GET** 要求 (アクセス許可 — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

応答 **の id** プロパティは次の値です `chatId` 。

または、以下の要求を使用して取得できますが、 `chatId`  より広範なアクセス許可が必要 `Chat.Read.All` になります。

**HTTP GET** 要求 (アクセス許可 — `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔メッセージを送信する

ボットがユーザーまたはチームに追加され、必要なユーザー情報を取得したら、プロアクティブ メッセージの送信 [を開始できます](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。

# <a name="c--net"></a>[C# / .NET](#tab/csharp)

次のコード スニペットは [、C# 用 Microsoft Bot Framework サンプルの抜粋です。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

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

次のコード スニペットは [、Microsoft Bot Framework Samples for JavaScript の抜粋です](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。

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

## <a name="related-topic-for-teams-administrators"></a>Teams 管理者向け関連トピック
>
> [!div class="nextstepaction"]
> [**Microsoft Teams のアプリのセットアップ ポリシーを管理する**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>その他のコード サンプルを表示する
>
> [!div class="nextstepaction"]
> [**Teams プロアクティブ メッセージングのコード サンプル**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
