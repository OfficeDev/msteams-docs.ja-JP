---
title: プロアクティブ メッセージ
description: ボットが会話を開始できるMicrosoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: チーム シナリオプロアクティブ メッセージング会話ボット
ms.openlocfilehash: baf148d0f4d0a669de582dfca70ed5d5bed0274c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566790"
---
# <a name="proactive-messaging-for-bots"></a>ボットのプロアクティブなメッセージング

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

プロアクティブ メッセージとは、ボットが会話を開始するために送信するメッセージです。 ボットに会話を開始させる理由として、次のようなものがあります。

* 個人的なボットの会話のウェルカムメッセージ。
* ポーリングの回答。
* 外部イベント通知。

新しい会話スレッドを開始するメッセージの送信は、既存の会話に応答してメッセージを送信することとは異なります: ボットが新しい会話を開始したときに、メッセージを投稿する既存の会話はありません。 プロアクティブ メッセージを送信するには、次の手順を実行する必要があります。

1. [何を言うか決める](#best-practices-for-proactive-messaging)
1. [ユーザーの一意の ID とテナント ID を取得します。](#obtain-necessary-user-information)
1. [メッセージを送信する](#examples)

プロアクティブ メッセージを作成するときは、 を呼び出 `MicrosoftAppCredentials.TrustServiceUrl` し、サービス URL を渡してから、 `ConnectorClient` メッセージの送信に使用する必要があります。 そうしない場合、アプリは応答を受け取ります `401: Unauthorized` 。 詳細については、 [以下のサンプルを参照してください](#net-example-from-this-sample)。

## <a name="best-practices-for-proactive-messaging"></a>プロアクティブ メッセージングのベスト プラクティス

ユーザーにプロアクティブ メッセージを送信することは、ユーザーとのコミュニケーションを効果的に行う方法です。 しかし、彼らの視点から見ると、このメッセージは完全に即座に表示され、ウェルカムメッセージの場合は初めてアプリとやり取りします。 そのため、この機能を控えめに使用し (ユーザーに迷惑を与えない)、メッセージが送信される理由を理解するのに十分な情報を提供することが非常に重要です。

プロアクティブ メッセージは、一般にウェルカム メッセージと通知の 2 つのカテゴリに分類されます。

### <a name="welcome-messages"></a>ウェルカム メッセージ

ユーザーにメッセージを送信するためにプロアクティブ メッセージを使用する場合、メッセージを受信するほとんどのユーザーは、メッセージを受信する理由に関するコンテキストを持たないことを覚えておいてください。 また、アプリとやり取りするのは初めてです。良い第一印象を作るチャンスです。 最高のウェルカムメッセージは次のとおりです。

* **なぜ彼らはこのメッセージを受け取っているのですか?** ユーザーがメッセージを受信する理由は、ユーザーにとって非常に明確に示されるはずです。 あなたのボットがチャネルにインストールされていて、すべてのユーザーにウェルカム メッセージを送信した場合は、どのチャネルにインストールされ、誰がインストールしたのかを通知する必要があります。
* **提示する内容。** ユーザーはあなたのアプリで何ができるのでしょうか? ユーザーはどのような価値を得られるのでしょうか?
* **ユーザーが次にするべきこと。** コマンドを試すように招待したり、何らかの方法でアプリと対話したりします。

### <a name="notification-messages"></a>通知メッセージ

プロアクティブ メッセージを使用して通知を送信する場合は、通知に基づいて共通のアクションを実行するための明確なパスをユーザーに確認し、通知が発生した理由を明確に理解する必要があります。 良い通知メッセージは、一般的に次のとおりです。

* **何が起こったのですか。** 何が原因で通知が発生したのかを明確に示しています。
* **それが何に起こったのか。** 通知を発生させるために更新されたアイテム/アイテムは明確にする必要があります。
* **Whoそれをやった。** Whoは、通知の送信の原因となったアクションを実行しました。
* **彼らはそれについて何ができるか。** ユーザーが通知に基づいてアクションを取ることを容易にします。
* **オプトアウトする方法。** ユーザーが追加の通知をオプトアウトするためのパスを指定する必要があります。

## <a name="obtain-necessary-user-information"></a>必要なユーザー情報を取得する

ボットは、ユーザーの *一意* の ID と *テナント ID* を取得することで、個々のMicrosoft Teamsユーザーとの新しい会話を作成できます。 これらの値は、次のいずれかの方法で取得できます。

* チャンネルから [チームの名簿を取得](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) することで、アプリがインストールされます。
* ユーザーが [チャネルでボットとやり取りするときにキャッシュ](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)する方法 。
* ユーザーが [チャネル会話で@mentioned](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) 場合、ボットはの一部です。
* アプリが個人用スコープにインストールされた場合、または新しいメンバーがチャネルまたはグループ チャットに追加されたときにイベントを[受信 `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)したときにキャッシュします。

### <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリをプロアクティブにインストール

> [!Note]
> グラフを使用してアプリをプロアクティブにインストールすることは、現在ベータ版です。

場合によっては、以前にアプリをインストールしていない、またはアプリと対話していないユーザーにプロアクティブにメッセージを送る必要があるかもしれません。 たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。 このシナリオでは、Graph API を使用してユーザー用にアプリを事前にインストールし、 `conversationUpdate` インストール時にアプリが受け取るイベントから必要な値をキャッシュします。

インストールできるのは、組織のアプリ カタログまたはTeams アプリ ストアに含まれるアプリのみです。

詳細については、Graphのドキュメントの[「ユーザー向けアプリのインストール](/graph/teams-proactive-messaging)」を参照してください。 [.NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)にはサンプルもあります。

## <a name="examples"></a>例

REST API を使用して新しい会話を作成する前に、認証を行い、ベアラー トークンを持っていることを確認してください。

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

この ID は、パーソナル チャットの一意の会話 ID です。 この値を保存し、ユーザーとの今後の対話のために再利用してください。

### <a name="using-net"></a>NET の使用

この例では[、NuGet パッケージを使用Teams。](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

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

チームが追加したボットは、チャネルに投稿して新しい返信チェーンを作成できます。 Node.js Teams SDK を使用している場合は、 `startReplyChain()` 適切なアクティビティ ID と会話 ID を持つ完全に入力されたアドレスを提供するを使用します。C# を使用している場合は、次の例を参照してください。

または、REST API を使用してリソースに POST 要求を発行することもできます [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) 。

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

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)