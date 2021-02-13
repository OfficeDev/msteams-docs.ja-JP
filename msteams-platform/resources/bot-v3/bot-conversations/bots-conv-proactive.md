---
title: プロアクティブ メッセージ
description: ボットが Microsoft Teams で会話を開始できる方法について説明します
keywords: Teams のシナリオプロアクティブ メッセージング会話ボット
ms.openlocfilehash: 8c93696f79b5d99c32162a7374c7d9adccacb984
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231625"
---
# <a name="proactive-messaging-for-bots"></a>ボットのプロアクティブ メッセージング

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

プロアクティブ メッセージは、会話を開始するためにボットによって送信されるメッセージです。 ボットに会話を開始させる理由として、次のようなものがあります。

* 個人向けの会話におけるボットのウェルカム メッセージ
* 投票の回答
* 外部イベントの通知

新しい会話スレッドを開始するメッセージの送信は、既存の会話への応答でメッセージを送信する場合とは異なります。ボットが新しい会話を開始すると、メッセージを投稿する既存の会話はありません。 プロアクティブ メッセージを送信するには、次の必要があります。

1. [話す言葉を決める](#best-practices-for-proactive-messaging)
1. [ユーザーの一意の ID とテナント ID を取得する](#obtain-necessary-user-information)
1. [メッセージを送信する](#examples)

プロアクティブ メッセージを作成する場合は、メッセージの送信に使用するメッセージを作成する前に、サービス URL を呼び出して渡 `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` す必要があります。 そうしない場合、アプリは応答を受信 `401: Unauthorized` します。 以下 [のサンプルを参照してください](#net-example-from-this-sample)。

## <a name="best-practices-for-proactive-messaging"></a>プロアクティブ メッセージングのベスト プラクティス

プロアクティブ メッセージをユーザーに送信すると、ユーザーと通信する非常に効果的な方法になります。 ただし、ユーザーの観点からは、このメッセージは完全にプロンプトされていないと思える可能性があります。ウェルカム メッセージの場合は、アプリを初めて操作する場合です。 そのため、この機能を少しでも使用し (ユーザーに迷惑メールを送信しない)、メッセージが送信される理由を理解するのに十分な情報を提供することが非常に重要です。

プロアクティブ メッセージは、一般にウェルカム メッセージと通知の 2 つのカテゴリに分類されます。

### <a name="welcome-messages"></a>ウェルカム メッセージ

プロアクティブ メッセージングを使用してユーザーにウェルカム メッセージを送信する場合は、メッセージを受信するほとんどのユーザーに対して、メッセージを受信する理由に関するコンテキストがないという念頭に置く必要があります。 これは、アプリを操作する最初の機会です。第一印象を良くする機会です。 最適なウェルカム メッセージには、次のものが含まれます。

* **このメッセージを受信する理由。** ユーザーがメッセージを受信する理由は非常に明確である必要があります。 ボットがチャネルにインストールされ、すべてのユーザーにウェルカム メッセージを送信した場合は、ボットがインストールされているチャネルと、インストールされている可能性のあるユーザーを知らせる必要があります。
* **何を提供します。** アプリで何ができるか。 どのような価値を持ち込むか。
* **次に何を行う必要があります。** コマンドを試したり、何らかの方法でアプリを操作したりします。

### <a name="notification-messages"></a>通知メッセージ

プロアクティブ メッセージングを使用して通知を送信する場合は、通知に基づいて共通のアクションを実行する明確なパスと、通知が発生した理由を明確に理解する必要があります。 良好な通知メッセージには、通常、次のものが含まれます。

* **どうしたのですか。** 通知の原因を明確に示します。
* **何が起こったか。** 通知を発生するために更新されたアイテム/アイテムが明確である必要があります。
* **誰がそれを行ったか。** 通知の送信を引き起こしたアクションを実行したユーザー。
* **ユーザーが実行できる操作。** 通知に基づいてユーザーが簡単にアクションを実行できます。
* **ユーザーがオプトアウトする方法。** 追加の通知をオプトアウトするパスをユーザーに提供する必要があります。

## <a name="obtain-necessary-user-information"></a>必要なユーザー情報を取得する

ボットは、ユーザーの一意の ID とテナント *ID* を取得することで、個々の Microsoft Teams ユーザーとの新しい会話 *を作成できます。* これらの値は、次のいずれかの方法で取得できます。

* アプリ [がインストールされているチャネル](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) からチーム名簿を取得します。
* ユーザーがチャネルでボットを [操作するときにキャッシュします](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)。
* ユーザーがチャネル会話 [@mentioned、ボット](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) は一部です。
* アプリが個人用スコープで[ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)インストールされた場合、または新しいメンバーがチャネルまたはグループ チャットに追加された場合にイベントを受信するときにキャッシュする

### <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリを事前にインストールする

> [!Note]
> Graph を使用してアプリを事前にインストールする機能は、現在ベータ版です。

以前にアプリをインストールまたは操作していないユーザーに事前にメッセージを送信する必要がある場合があります。 たとえば、会社のコミュニケーター [を使用](~/samples/app-templates.md#company-communicator) して組織全体にメッセージを送信する場合です。 このシナリオでは、Graph API を使用してユーザー用のアプリを事前にインストールし、インストール時にアプリが受け取るイベントから必要な値を `conversationUpdate` キャッシュできます。

インストールできるのは、組織のアプリ カタログまたは Teams アプリ ストアにあるアプリのみです。

詳細 [については、Graph ドキュメントの「](/graph/teams-proactive-messaging) ユーザー向けアプリのインストール」を参照してください。 .NET には [サンプルがあります](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。

## <a name="examples"></a>例

REST API を使用して新しい会話を作成する前に、必ず認証し、ベアラー トークンを持っている必要があります。

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

この ID は、個人用チャットの一意の会話 ID です。 この値を保存し、ユーザーとの今後のやり取りのために再利用してください。

### <a name="using-net"></a>.NET の使用

この例では [、Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。

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

### <a name="using-nodejs"></a>ユーザー設定Node.js

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

*Bot* Framework の [サンプルも参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

## <a name="creating-a-channel-conversation"></a>チャネル会話の作成

チームが追加したボットは、チャネルに投稿して新しい返信チェーンを作成できます。 Node.js Teams SDK を使用している場合は、適切なアクティビティ ID と会話 ID が完全に入力されたアドレス `startReplyChain()` を使用します。C# を使用している場合は、以下の例を参照してください。

または、REST API を使用して、リソースに POST 要求を発行 [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) することもできます。

### <a name="net-example-from-this-sample"></a>.NET の例 (この [サンプルから](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))

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
