---
title: ボット用のプロアクティブ メッセージング
description: このモジュールでは、ボットにプロアクティブ メッセージングを使用する方法と、Microsoft Teamsでのプロアクティブ メッセージングのベスト プラクティスについて説明します
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: ee193cd7dfcfec20f501483eabc3a485cff0caab
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143131"
---
# <a name="proactive-messaging-for-bots"></a>ボット用のプロアクティブ メッセージング

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

プロアクティブ メッセージは、会話を開始するためにボットによって送信されるメッセージです。 ボットに会話を開始させる理由として、次のようなものがあります。

* 個人用ボットの会話のウェルカム メッセージ。
* 応答をポーリングします。
* 外部イベント通知。
新しい会話スレッドを開始するメッセージの送信は、既存の会話に応答してメッセージを送信する場合とは異なります。ボットが新しい会話を開始すると、メッセージを投稿する既存の会話はありません。 プロアクティブ メッセージを送信するには、次の手順を実行する必要があります。

1. [何を言うかを決める](#best-practices-for-proactive-messaging)
1. [ユーザーの一意の ID とテナント ID を取得する](#obtain-necessary-user-information)
1. [メッセージを送信する](#examples)

プロアクティブ メッセージを作成する場合は、メッセージの送信に使用するメッセージを作成`ConnectorClient`する前に、サービス URL を呼び出`MicrosoftAppCredentials.TrustServiceUrl`して渡す **必要があります**。 応答しない場合は、 `401: Unauthorized` アプリによって応答が受信されます。 詳細については、 [以下のサンプルを](#net-example-from-this-sample)参照してください。

## <a name="best-practices-for-proactive-messaging"></a>プロアクティブ メッセージングのベスト プラクティス

プロアクティブ メッセージを送信することは、ユーザーと通信するための効果的な方法です。 ただし、ユーザーの観点からは、メッセージはプロンプトなしで表示されます。 ウェルカム メッセージがある場合、アプリを操作するのは初めてです。 この機能を使用し、このメッセージの目的を理解するためにユーザーに完全な情報を提供することが重要です。

プロアクティブ メッセージは、一般にウェルカム メッセージと通知の 2 つのカテゴリに分類されます。

### <a name="welcome-messages"></a>ウェルカム メッセージ

プロアクティブ メッセージングを使用してウェルカム メッセージをユーザーに送信する場合は、ユーザーの観点から、メッセージがプロンプティングされていない状態で表示されることを確認します。 ウェルカム メッセージがある場合、アプリを操作するのは初めてです。 最適なウェルカム メッセージには、次のものが含まれます。

* **このメッセージを受け取る理由: このメッセージを受け取** る理由をユーザーに明確にする必要があります。 あなたのボットがチャネルにインストールされていて、すべてのユーザーにウェルカム メッセージを送信した場合は、どのチャネルにインストールされ、誰がインストールしたのかを通知する必要があります。
* **何を提供しますか**:アプリで何ができますか? ユーザーはどのような価値を得られるのでしょうか?
* **次に実行する必要がある操作**: コマンドを試すか、何らかの方法でアプリと対話するように招待します。

### <a name="notification-messages"></a>通知メッセージ

プロアクティブ メッセージングを使用して通知を送信する場合は、ユーザーが通知に基づいて一般的なアクションを実行するための明確なパスと、通知が発生した理由を明確に理解する必要があります。 通常、適切な通知メッセージには次のものが含まれます。

* **発生した内容**: 通知の原因を明確に示します。
* **発生した** 内容: 通知の原因として更新された項目/内容を明確にする必要があります。
* **Whoしました。** Who通知が送信される原因となったアクションを実行しましたか?
* **ユーザーができること**: ユーザーが通知に基づいて簡単にアクションを実行できるようにします。
* **オプトアウトする方法**: ユーザーが追加の通知をオプトアウトするためのパスを指定します。

## <a name="obtain-necessary-user-information"></a>必要なユーザー情報を取得する

ボットは、ユーザーの *一意の ID* と *テナント ID* を取得することで、個々のMicrosoft Teams ユーザーとの新しい会話を作成できます。 これらの値は、次のいずれかの方法で取得できます。

* アプリがインストールされているチャネルから [チーム名簿をフェッチ](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) します。
* ユーザーが [チャネルでボットと対話](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)するときにキャッシュします。
* ユーザーが [チャネル会話で@mentioned](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) 場合、ボットは一部です。
* アプリが個人用スコープにインストールされたとき、または新しいメンバーがチャネルまたはグループ チャットに追加されたときに、イベントを [受け取 `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) ったときにキャッシュします。

### <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリをプロアクティブにインストール

> [!Note]
> グラフを使用してアプリをプロアクティブにインストールすることは、現在ベータ版です。

場合によっては、以前にアプリをインストールまたは操作していないユーザーに対してプロアクティブにメッセージを送信することが必要になる場合があります。 たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。 このシナリオでは、Graph APIを使用してユーザーのアプリを事前にインストールし、インストール時にアプリが受け取るイベントから`conversationUpdate`必要な値をキャッシュできます。

インストールできるのは、組織のアプリ カタログまたはTeamsアプリ ストア内にあるアプリのみです。

詳細については、Graphドキュメントの「[ユーザー向けのアプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)」を参照してください。 [.NET にはサンプル](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)もあります。

## <a name="examples"></a>例

REST API を使用して新しい会話を作成する前に、必ず認証し、ベアラー トークンを持っていることを確認してください。

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

ユーザー ID とテナント ID を入力する必要があります。 呼び出しに成功した場合、API は以下の応答オブジェクトを返します。

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

この ID は、個人用チャットの一意の会話 ID です。 この値をMicrosoft Storeし、今後ユーザーとやり取りするために再利用します。

### <a name="using-net"></a>.NET の使用

この例では、[Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

### <a name="using-nodejs"></a>Node.jsの使用

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

## <a name="creating-a-channel-conversation"></a>チャネル会話の作成

チームが追加したボットは、チャネルに投稿して新しい返信チェーンを作成できます。 Node.js Teams SDK を使用している場合は、`startReplyChain()`正しいアクティビティ ID と会話 ID で完全に設定されたアドレスを指定します。 C# を使用している場合は、次の例を参照してください。

または、REST API を使用して、リソースに対して POST 要求を [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) 発行することもできます。

### <a name="net-example-from-this-sample"></a>.NET の例 ( [このサンプル](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)から)

```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```

## <a name="see-also"></a>関連項目

[Bot Framework Samples (Bot Framework のサンプル)](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
