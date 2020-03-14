---
title: 事前メッセージ
description: Bot が Microsoft Teams で会話を開始できることについて説明します。
keywords: teams シナリオの予防的なメッセージング会話 bot
ms.openlocfilehash: 30a21a15126e489ec50f8d3b7307880921d6062b
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "42635320"
---
# <a name="proactive-messaging-for-bots"></a>Bot のための事前のメッセージング

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

"予防的なメッセージ" とは、bot が会話を開始するために送信するメッセージです。 次のようなさまざまな理由により、ボットで会話を開始することが必要になる場合があります。

* 個人ボット会話のウェルカムメッセージ
* 投票応答
* 外部イベント通知

メッセージを送信して新しい会話スレッドを開始する方法は、既存の会話に対してメッセージを送信することとは異なります。 bot が新しい会話を開始すると、メッセージを投稿する既存の会話はありません。 事前メッセージを送信するには、次のことを行う必要があります。

1. [発言対象を決定する](#best-practices-for-proactive-messaging)
1. [ユーザーの一意の Id とテナント Id を取得する](#obtain-necessary-user-information)
1. [メッセージを送信する](#examples)

事前メッセージを作成するときは`MicrosoftAppCredentials.TrustServiceUrl`、を呼び出してサービス URL を作成して`ConnectorClient`から、メッセージの送信に使用するを作成する**必要があり**ます。 そうしないと、アプリは応答を`401: Unauthorized`受信します。 [以下のサンプルを](#net-example-from-this-sample)参照してください。

## <a name="best-practices-for-proactive-messaging"></a>事前メッセージのベストプラクティス

事前にメッセージをユーザーに送信することは、ユーザーとの通信に非常に効果的な方法となります。 ただし、このメッセージは完全に表示されないことがわかります。また、ウェルカムメッセージがアプリを初めて操作したときには、このメッセージが完全に非表示になっているように見えます。 そのため、この機能を多用しない (ユーザーにスパムを行わない) こと、および伝達の理由を理解するのに十分な情報を提供することが非常に重要です。

予防的なメッセージは、通常、ウェルカムメッセージまたは通知の2つのカテゴリに分類されます。

### <a name="welcome-messages"></a>ウェルカムメッセージ

事前メッセージを使用して、ユーザーにウェルカムメッセージを送信する場合は、メッセージを受信する多くのユーザーが受信する理由についてのコンテキストがないことに注意する必要があります。 これは、アプリを初めて使用したときにも使用されます。最初の印象を得ることをお勧めします。 推奨されるウェルカムメッセージは次のとおりです。

* **なぜこのメッセージを受信するのですか。** ユーザーがメッセージを受信する理由を明確にする必要があります。 Bot がチャネルにインストールされていて、すべてのユーザーにウェルカムメッセージを送信した場合は、インストールされているチャネルと、インストールされている可能性のあるチャネルを知らせます。
* **何を提供するか。** アプリでできること どのような値にすることができますか。
* **次の手順を実行します。** コマンドを試したり、何らかの方法でアプリを操作したりするように招待します。

### <a name="notification-messages"></a>通知メッセージ

事前メッセージを使用して通知を送信する場合は、ユーザーが通知に基づいて一般的な操作を実行するための明確なパスを持っていることを確認し、通知が発生した理由を明確に理解しておく必要があります。 適切な通知メッセージには、通常次のものが含まれます。

* **どうしたのですか。** 通知を発生させた理由を明確に示します。
* **何が起こったのか。** 通知を発生させるためにアイテムまたはアイテムが更新されたことを明確にする必要があります。
* **だれがやったか。** 通知が送信された原因となった操作を行ったユーザー。
* **そのためにできること。** ユーザーが通知に基づいて操作を簡単に実行できるようにします。
* **どのようにオプトアウトできるか。** ユーザーが追加の通知をオプトアウトするためのパスを指定する必要があります。

## <a name="obtain-necessary-user-information"></a>必要なユーザー情報を取得する

Bot は、ユーザーの*一意の id*とテナント id を取得することによって、個々の Microsoft Teams ユーザーとの新しい会話を作成でき*ます。* これらの値は、次のいずれかの方法を使用して取得できます。

* アプリがインストールされているチャネルから[チーム名簿を取得](~/resources/bot-v3/bots-context.md#fetching-the-team-roster)します。
* ユーザーが[チャネル内の bot と対話](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)するときにキャッシュする。
* ユーザーが[チャネル会話で @mentioned](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)すると、bot はの一部になります。
* アプリが個人スコープにインストールされたときにイベントを[受け取っ`conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)たときにキャッシュするか、新しいメンバーをチャネルまたはグループのチャットに追加します。

### <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリを事前にインストールする

> [!Note]
> Graph を使用してアプリを事前にインストールするのは、現在ベータ版です。

場合によっては、既にインストールされていない、またはアプリと対話していないメッセージユーザーを予防的に行う必要があります。 たとえば、[会社の communicator](~/samples/app-templates.md#company-communicator-app)を使用して組織全体にメッセージを送信するとします。 このシナリオでは、Graph API を使用して、ユーザー用のアプリを事前にインストールし、インストール時に`conversationUpdate`アプリが受け取るイベントから必要な値をキャッシュすることができます。

組織のアプリカタログまたは Teams アプリストアにあるアプリのみをインストールできます。

詳細については、グラフのドキュメントの「[ユーザー用アプリのインストール](/graph/teams-proactive-messaging)」を参照してください。 [.Net に](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)は、サンプルもあります。

## <a name="examples"></a>例

REST API を使用して新しい会話を作成する前に、必ず事前認証を行い、ベアラートークンを用意してください。

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

ユーザー ID とテナント ID を指定する必要があります。 呼び出しが成功すると、API は次の応答オブジェクトを返します。

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

この ID は、パーソナルチャットの一意の会話 ID です。 この値を保存して、後でユーザーとの対話のために再利用してください。

### <a name="using-net"></a>.NET の使用

この例では、 [Microsoft の Bot](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。

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

### <a name="using-nodejs"></a>Node.js の使用

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

[Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください*。

## <a name="creating-a-channel-conversation"></a>チャネル会話の作成

チームが追加した bot は、チャネルに投稿して新しい返信チェーンを作成できます。 Node.js Teams SDK を使用している場合は、を`startReplyChain()`使用して、適切なアクティビティ id と会話 id を持つ完全に入力されたアドレスを付与します。C# を使用している場合は、次の例を参照してください。

または、REST API を使用して、POST 要求を resource [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation)に発行することもできます。

### <a name="net-example-from-this-sample"></a>.NET の例 ([このサンプル](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)から)

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
