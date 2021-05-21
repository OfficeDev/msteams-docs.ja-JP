---
title: プロアクティブ メッセージ
description: ボットがチャットで会話を開始できるMicrosoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: Teams シナリオのプロアクティブ メッセージング会話ボット
ms.openlocfilehash: baf148d0f4d0a669de582dfca70ed5d5bed0274c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566790"
---
# <a name="proactive-messaging-for-bots"></a>ボットのプロアクティブ メッセージング

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

プロアクティブ メッセージとは、ボットが会話を開始するために送信するメッセージです。 ボットに会話を開始させる理由として、次のようなものがあります。

* 個人用ボットの会話に関するウェルカム メッセージ。
* ポーリング応答。
* 外部イベント通知。

新しい会話スレッドを開始するメッセージの送信は、既存の会話に応答してメッセージを送信する場合とは異なります。ボットが新しい会話を開始すると、メッセージを投稿する既存の会話はありません。 プロアクティブ メッセージを送信するには、次の必要があります。

1. [何を言うのかを決める](#best-practices-for-proactive-messaging)
1. [ユーザーの一意の ID とテナント ID を取得する](#obtain-necessary-user-information)
1. [メッセージを送信する](#examples)

プロアクティブ メッセージを作成する場合は、メッセージの送信に使用するメッセージを作成する前に、サービス URL を呼び出して渡 `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` す必要があります。 応答しない場合、アプリは応答を受信 `401: Unauthorized` します。 詳細については、以下の [サンプルを参照してください](#net-example-from-this-sample)。

## <a name="best-practices-for-proactive-messaging"></a>プロアクティブ メッセージングのベスト プラクティス

ユーザーにプロアクティブ メッセージを送信すると、ユーザーと通信する非常に効果的な方法になります。 ただし、このメッセージの観点から見ると、このメッセージは完全にプロンプトされていないものに見え、ウェルカム メッセージの場合はアプリを初めて操作します。 そのため、この機能を使用する (ユーザーに迷惑メールを送信しない) ので、メッセージが送信される理由を理解するのに十分な情報を提供することが非常に重要です。

プロアクティブ メッセージは、一般にウェルカム メッセージと通知の 2 つのカテゴリに分類されます。

### <a name="welcome-messages"></a>ウェルカム メッセージ

プロアクティブ メッセージングを使用してユーザーにウェルカム メッセージを送信する場合は、メッセージを受信するほとんどのユーザーに対して、メッセージを受信する理由に関するコンテキストが提供されません。 また、アプリを操作したのも初めてです。良い第一印象を作り出す機会です。 最適なウェルカム メッセージには、次のものが含まれます。

* **なぜこのメッセージを受け取るのですか。** ユーザーがメッセージを受信する理由は非常に明確である必要があります。 あなたのボットがチャネルにインストールされていて、すべてのユーザーにウェルカム メッセージを送信した場合は、どのチャネルにインストールされ、誰がインストールしたのかを通知する必要があります。
* **提示する内容。** ユーザーはあなたのアプリで何ができるのでしょうか? ユーザーはどのような価値を得られるのでしょうか?
* **ユーザーが次にするべきこと。** コマンドを試すように招待したり、何らかの方法でアプリと対話したりします。

### <a name="notification-messages"></a>通知メッセージ

プロアクティブ メッセージングを使用して通知を送信する場合は、ユーザーが通知に基づいて一般的なアクションを実行する明確なパスを持ち、通知が発生した理由を明確に理解する必要があります。 良好な通知メッセージには、通常、次のものが含まれます。

* **何が起こったのですか。** 何が原因で通知が発生したのかを明確に示しています。
* **何が起こったのか。** 通知を発生するために更新されたアイテム/物を明確にしてください。
* **Whoを行いました。** Whoが送信される原因となるアクションを実行しました。
* **彼らが何を行うのか。** ユーザーが通知に基づいてアクションを取ることを容易にします。
* **オプトアウトする方法。** ユーザーが追加の通知をオプトアウトするパスを指定する必要があります。

## <a name="obtain-necessary-user-information"></a>必要なユーザー情報を取得する

ボットは、ユーザーの一意の *ID* とテナント ID をMicrosoft Teamsして、個々のユーザーと新しい会話を *作成できます。* これらの値は、次のいずれかの方法で取得できます。

* アプリ [がインストールされているチャネル](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) からチーム名簿を取得します。
* ユーザーがチャネルでボットとやり取りするときにキャッシュ [します](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)。
* ユーザーがチャネル会話 [@mentioned、](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) ボットは一部です。
* アプリが個人用スコープにインストール[ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)されている場合、または新しいメンバーがチャネルまたはグループ チャットに追加された場合に、それらをキャッシュします。

### <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリをプロアクティブにインストール

> [!Note]
> Graph を使用してアプリを積極的にインストールする方法は、現在ベータ版です。

場合によっては、以前にアプリをインストールしていない、またはアプリと対話していないユーザーにプロアクティブにメッセージを送る必要があるかもしれません。 たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。 このシナリオでは、Graph API を使用してユーザー向けアプリをプロアクティブにインストールし、インストール時にアプリが受け取るイベントから必要な値を `conversationUpdate` キャッシュできます。

インストールできるのは、組織のアプリ カタログまたはアプリ ストアTeamsのみです。

詳細については[、「ユーザー向けアプリ](/graph/teams-proactive-messaging)のインストール」Graphドキュメントを参照してください。 .NET にも [サンプルがあります](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。

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

この ID は、個人チャットの一意の会話 ID です。 この値を保存し、ユーザーとの将来のやり取りのために再利用してください。

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

チームが追加したボットは、チャネルに投稿して新しい返信チェーンを作成できます。 この SDK を使用しているNode.js Teams、正しいアクティビティ ID と会話 ID を持つ完全に入力されたアドレス `startReplyChain()` を提供します。このツールを使用しているC#、以下の例を参照してください。

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