---
title: プロアクティブ メッセージ
description: ボットがチャットで会話を開始できるMicrosoft Teams
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Teams シナリオのプロアクティブ メッセージング会話ボット
ms.openlocfilehash: c84b504fc6dba84f33ecaf76a0ce0cdebea82255
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720065"
---
# <a name="proactive-messaging-for-bots"></a>ボットのプロアクティブ メッセージング

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

プロアクティブ メッセージとは、ボットが会話を開始するために送信するメッセージです。 ボットに会話を開始させる理由として、次のようなものがあります。

* 個人向けの会話におけるボットのウェルカム メッセージ
* 投票の回答
* 外部イベントの通知

新しい会話スレッドを開始するメッセージの送信は、既存の会話に応答してメッセージを送信する場合とは異なります。ボットが新しい会話を開始すると、メッセージを投稿する既存の会話はありません。 プロアクティブ メッセージを送信するには、次の必要があります。

1. [何を言うのかを決める](#best-practices-for-proactive-messaging)
1. [ユーザーの一意の ID とテナント ID を取得する](#obtain-necessary-user-information)
1. [メッセージを送信する](#examples)

プロアクティブ メッセージを作成 **する場合は** 、メッセージの送信に使用されるメッセージを作成する前に、サービス URL を呼び出して渡 `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` す必要があります。 応答を受信しない場合は `401: Unauthorized` 、アプリによって応答が受信されます。 詳細については、以下の [サンプルを参照してください](#net-example-from-this-sample)。

## <a name="best-practices-for-proactive-messaging"></a>プロアクティブ メッセージングのベスト プラクティス

プロアクティブ メッセージの送信は、ユーザーと通信する効果的な方法です。 ただし、ユーザーの観点から見ると、メッセージはプロンプトされていない表示されます。 ウェルカム メッセージがある場合、アプリを操作したのは初めてです。 この機能を使用し、このメッセージの目的を理解するためにユーザーに完全な情報を提供することが重要です。

プロアクティブ メッセージは、一般にウェルカム メッセージと通知の 2 つのカテゴリに分類されます。

### <a name="welcome-messages"></a>ウェルカム メッセージ

プロアクティブ メッセージングを使用してウェルカム メッセージをユーザーに送信する場合は、ユーザーの観点からメッセージがプロンプトされていないと表示されます。 ウェルカム メッセージがある場合、アプリを操作したのは初めてです。 最適なウェルカム メッセージには、次のものが含まれます。

* **このメッセージを受信する理由**: このメッセージを受信する理由をユーザーに明確に伝えるべきです。 あなたのボットがチャネルにインストールされていて、すべてのユーザーにウェルカム メッセージを送信した場合は、どのチャネルにインストールされ、誰がインストールしたのかを通知する必要があります。
* **何を提供しますか**: アプリで何ができますか? ユーザーはどのような価値を得られるのでしょうか?
* **次に何をする必要があります**: コマンドを試してみるか、何らかの方法でアプリを操作するために招待します。

### <a name="notification-messages"></a>通知メッセージ

プロアクティブ メッセージングを使用して通知を送信する場合は、ユーザーが通知に基づいて一般的なアクションを実行する明確なパスを持ち、通知が発生した理由を明確に理解する必要があります。 良好な通知メッセージには、通常、次のものが含まれます。

* **何が起こった** か: 通知の原因を明確に示します。
* **何が起こったか**: 通知を発生するために更新されたアイテム/物が明確である必要があります。
* **Whoしました:** Whoが送信される原因となるアクションを実行しましたか?
* **ユーザーが通知に基づいて** 簡単にアクションを実行できます。
* **ユーザーがオプトアウトする方法**: ユーザーが追加の通知をオプトアウトするパスを提供します。

## <a name="obtain-necessary-user-information"></a>必要なユーザー情報を取得する

ボットは、ユーザーの一意の *ID* とテナント ID をMicrosoft Teamsして、個々のユーザーと新しい会話を *作成できます。* これらの値は、次のいずれかの方法で取得できます。

* アプリ [がインストールされているチャネルから](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) チーム名簿を取得します。
* ユーザーがチャネルでボットとやり取りするときにキャッシュ [します](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)。
* ユーザーがチャネル会話 [@mentioned、](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) ボットは一部です。
* アプリが個人用スコープにインストール[ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)されている場合、または新しいメンバーがチャネルまたはグループ チャットに追加された場合に、それらをキャッシュします。

### <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリをプロアクティブにインストール

> [!Note]
> Graph を使用してアプリを積極的にインストールする方法は、現在ベータ版です。

以前にアプリをインストールまたは操作していないユーザーに事前にメッセージを送信する必要がある場合があります。 たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。 このシナリオでは、Graph API を使用してユーザー向けアプリをプロアクティブにインストールし、インストール時にアプリが受け取るイベントから必要な値を `conversationUpdate` キャッシュできます。

インストールできるのは、組織のアプリ カタログまたはアプリ ストアTeamsのみです。

詳細については[、「ユーザー向けアプリ](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)のインストール」Graphドキュメントを参照してください。 .NET にも [サンプルがあります](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。

## <a name="examples"></a>例

REST API を使用して新しい会話を作成する前に、ベアラー トークンを認証して持っている必要があります。

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

この ID は、個人チャットの一意の会話 ID です。 この値を保存し、ユーザーとの将来の対話のために再利用します。

### <a name="using-net"></a>.NET の使用

この例では[、Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)します。

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

## <a name="creating-a-channel-conversation"></a>チャネル会話の作成

チームが追加したボットは、チャネルに投稿して新しい返信チェーンを作成できます。 SDK に対して Node.js Teamsを使用している場合は、正しいアクティビティ ID と会話 ID を持つ完全に入力されたアドレス `startReplyChain()` を使用します。 このファイルを使用しているC#、以下の例を参照してください。

または、REST API を使用して、リソースに POST 要求を発行 [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) することもできます。

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

## <a name="see-also"></a>関連項目

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
