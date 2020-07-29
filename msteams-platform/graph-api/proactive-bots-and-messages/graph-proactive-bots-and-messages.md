---
title: Microsoft Graph を使用して Teams での積極的なボットのインストールとメッセージングを有効にする
description: Teams における予防的なメッセージングと実装方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams の予防的なメッセージングチャットインストールグラフ
ms.openlocfilehash: 735dbfa39222f312b4f3714b5c009dfd1bf28b05
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434497"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>Microsoft Graph を使用した Teams での予防的なインストールと予防的なメッセージングを有効にする (パブリックプレビュー)

>[!IMPORTANT]
> Microsoft Graph のパブリックプレビューは、初めてアクセスしてフィードバックする際に使用できます。 このリリースは広範なテストを経ていますが、運用環境での使用は想定されていません。

## <a name="proactive-messaging-in-teams"></a>Teams での事前のメッセージング

事前メッセージは、ユーザーとの会話を開始する bot によって開始されます。 開始メッセージの送信、調査または投票の実行、組織全体にわたる通知の配信など、さまざまな目的に対応しています。  Teams の事前メッセージ**は、アドホックまたは****ダイアログベース**の会話として配信できます。

|メッセージ型 | 説明 |
|----------------|-------------- |
|アドホックの事前メッセージ| Bot は、会話フローを中断することなくメッセージを interjects します。|
|ダイアログベースの事前メッセージ | Bot は、新しいダイアログスレッドを作成し、会話の制御を取得し、事前メッセージを配信し、前のダイアログに制御を戻します。|

「[ユーザーに事前通知を送信する SDK V4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp) *」を参照してください*。

## <a name="proactive-app-installation-in-teams"></a>Teams での事前にアプリをインストールする

Bot がユーザーに対して予防的なメッセージを実行できるようにするには、ユーザーを個人のアプリとしてインストールするか、またはユーザーがメンバーになっているチームにインストールする必要があります。 インストールさ_れていない_、またはアプリに以前対話したことがない場合は、事前にメッセージを事前に作成しておく必要があります。 たとえば、組織内のすべてのユーザーにとって重要な情報をメッセージにする必要があります。 このようなシナリオでは、Microsoft Graph API を使用して、ユーザー向けに bot を事前にインストールすることができます。

## <a name="permissions"></a>アクセス許可

Microsoft Graph [teamsAppInstallation リソースの種類](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0)のアクセス許可を使用すると、microsoft Teams プラットフォーム内のすべてのユーザー (個人) スコープまたはチーム (チャネル) スコープのアプリのインストールライフサイクルを管理できます。

|アプリケーションのアクセス許可 | 説明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Teams アプリは、サインインまたは使用前に、**ユーザー**の読み取り、インストール、アップグレード、およびアンインストールを行うことができます。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Teams アプリは、サインインまたは使用前に、任意の**チーム**で自分自身を読み取り、インストール、アップグレード、およびアンインストールできます。|

これらのアクセス許可を使用するには、次の値を使用して、 [Webapplicationinfo](../../resources/schema/manifest-schema.md#webapplicationinfo)キーをアプリのマニフェストに追加する必要があります。
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id** : Azure AD アプリ id。
> * **resource** —アプリのリソース URL。
>

>[!NOTE]
>
> * Bot には、ユーザーにはインストールされませんが、それ以外の場合は、_アプリケーション_による_委任_されたアクセス許可が必要です。
>
> * Azure AD テナント管理者は、[アプリケーションに対するアクセス許可を明示的に付与](/graph/security-authorization#grant-permissions-to-an-application)する必要があります。 アプリケーションにアクセス許可が付与されると、Azure AD テナントの_すべて_のメンバーが付与されたアクセス許可を取得します。

## <a name="enable-proactive-app-installation-and-messaging"></a>事前にアプリのインストールとメッセージングを有効にする

 > [!IMPORTANT]
>Microsoft Graph では、組織の[アプリカタログ](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)または[appsource](https://appsource.microsoft.com/)に発行されたアプリのみがインストールされます。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>チームのために予防的なメッセージングボットを作成して発行する✔

作業を開始するには、[積極的なメッセージング](../../concepts/bots/bot-conversations/bots-conv-proactive.md)機能を備え、組織の[アプリカタログ](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)または[appsource](https://appsource.microsoft.com/)に[公開](../../concepts/deploy-and-publish/overview.md)されている[Teams 用の bot](../../bots/how-to/create-a-bot-for-teams.md)が必要です。

>[!TIP]
> 運用に対応した[**会社の Communicator**](../..//samples/app-templates.md#company-communicator)アプリテンプレートでは、ブロードキャストメッセージングが有効になり、予防的な bot アプリケーションを構築するための基礎となります。

### <a name="-get-the-teamsappid-for-your-app"></a>`teamsAppId`アプリのを取得✔

**1.** 次の手順では、が必要になります。 `teamsAppId`

は、 `teamsAppId` 組織のアプリカタログから取得できます。

**Microsoft Graph ページリファレンス:** [teamsapp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0)

**HTTP GET**要求:

```http
GET https://graph.microsoft.com/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

要求はオブジェクトを返し `teamsApp` ます。 返されるオブジェクトは、アプリのカタログ生成されたアプリ id であり、 `id` Teams アプリマニフェストで指定した "id:" とは異なります。

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

**2.** 個人スコープ内のユーザーに対してアプリが既にアップロードされている場合は、次のようにサイドロードを取得できます。 `teamsAppId`

**Microsoft Graph ページリファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP GET**要求:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

**3.** アプリがチームスコープ内のチャネルに対して既にアップロードまたはサイドロードされている場合は、次のようにを取得できます `teamsAppId` 。

**Microsoft Graph ページリファレンス:** teams[のアプリの一覧](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)

**HTTP GET**要求:

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{manifestId}'
```

>[!TIP]
> [**Teamsapp**](/graph/api/resources/teamsapp?view=graph-rest-1.0)オブジェクトの任意のフィールドをフィルター処理して、結果の一覧を絞り込むことができます。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ Bot がメッセージの受信者に現在インストールされているかどうかを判断するには

**Microsoft Graph ページリファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP GET**要求:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

この要求は、アプリがインストールされていない場合は空の配列を返し、インストールされている場合は1つの[teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta)オブジェクトを持つ配列を返します。

### <a name="-install-your-app"></a>アプリをインストール✔には

**Microsoft Graph リファレンス:** [ユーザーのアプリをインストールする](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP POST**要求:

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

ユーザーが Microsoft Teams を実行している場合は、直ちにアプリのインストールが表示されることがあります。 または、インストールされているアプリを表示するために再起動が必要な場合があります。

### <a name="-retrieve-the-conversation-chatid"></a>会話**chatId**を取得✔には

アプリがユーザー用にインストールされている場合、bot は、 `conversationUpdate` 事前メッセージを送信するために必要な情報が含まれた[イベント通知](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)を受け取ります。

は、次のように `chatId` 取得することもできます。

**Microsoft Graph リファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-beta&tabs=http)

**1.** アプリがインストールされていない場合は、次のように使用します。 `{teamsAppInstallationId}`

**HTTP GET**要求:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

応答の**id**プロパティは、 `teamsAppInstallationId` です。

**2.** 次のものをフェッチするための要求を行います。 `chatId`

**HTTP GET**要求 (アクセス許可— `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

応答の**id**プロパティは、 `chatId` です。

または、以下の要求でを取得することもでき `chatId` ますが、より広範なアクセス許可が必要になり `Chat.Read.All` ます。

**HTTP GET**要求 (アクセス許可— `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>積極的なメッセージを送信✔には

ユーザーまたはチームに bot が追加され、必要なユーザー情報を取得している場合は、[事前メッセージの送信](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)を開始できます。

# <a name="c--net"></a>[C#/.NET](#tab/csharp)

次のコードスニペットは、 [C# の Microsoft Bot フレームワークサンプル](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)からのものです。

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

次のコードスニペットは、 [JavaScript の Microsoft Bot フレームワークサンプル](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)からのものです。

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
> [**Microsoft Teams でアプリのセットアップポリシーを管理する**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>追加のコードサンプルを表示する
>
> [!div class="nextstepaction"]
> [**Teams の予防的なメッセージングコードサンプル**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>