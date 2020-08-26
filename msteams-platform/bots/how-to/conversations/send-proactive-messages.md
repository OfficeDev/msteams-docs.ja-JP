---
title: プロアクティブ メッセージを送信する
author: clearab
description: Microsoft Teams bot で予防的なメッセージを送信する方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874850"
---
# <a name="send-proactive-messages"></a>プロアクティブ メッセージを送信する

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

予防的なメッセージとは、ユーザーからの要求に直接応答していない bot によって送信されるメッセージのことです。 これには、次のようなメッセージが含まれます。

* ウェルカム メッセージ
* 通知
* スケジュールされたメッセージ

Bot が積極的なメッセージを送信するためには、メッセージの送信先のユーザー、グループチャット、またはチームにアクセスできる必要があります。 グループチャットまたはチームの場合は、ボットを含むアプリを最初にその場所にインストールする必要があります。 必要に応じて、チームで [グラフを使用してアプリを予防的にインストール](#proactively-install-your-app-using-graph) するか、 [アプリポリシー](/microsoftteams/teams-custom-app-policies-and-settings) を使用してテナント内の teams とユーザーにアプリをプッシュすることができます。 ユーザーの場合は、アプリをそのユーザー用にインストールするか、アプリがインストールされているチームの一部である必要があります。

積極的なメッセージを送信することは、返信に使用するアクティブがない場合に、通常のメッセージを送信することとは異なり `turnContext` ます。 メッセージを送信する前に、会話 (新しいワンツーワンチャット、チャネル内の新しい会話スレッドなど) を作成する必要がある場合もあります。 事前メッセージを使用してチームに新しいグループチャットまたは新しいチャネルを作成することはできません。

プロアクティブなメッセージを送信するには、次の手順を実行する必要があります。

1. [ユーザー id またはチーム/チャネル ID を取得](#get-the-user-id-or-teamchannel-id) します (必要な場合)。
1. [会話スレッドまたは会話スレッドを作成](#create-the-conversation) します (必要な場合)。
1. [会話 ID を取得](#get-the-conversation-id)します。
1. [メッセージを送信](#send-the-message)します。

1対1の会話を作成するには、以下の「 [例](#examples) 」セクションのコードスニペットを参照してください。1対1の会話とグループ/チャネルの両方に対して作業用のサンプルを完全に実行するには、「 [参照](#references) 」セクションを参照してください。

## <a name="get-the-user-id-or-teamchannel-id"></a>ユーザー ID またはチーム/チャネル ID を取得する

チャネルで新しい会話スレッドまたは会話スレッドを作成する必要がある場合は、最初に会話を作成するための適切な ID が必要です。 この ID を取得または取得するには、複数の方法があります。

1. アプリが特定のコンテキストでインストールされている場合は、 [ `onMembersAdded` アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)が表示されます。
1. アプリがインストールされているコンテキストに新しいユーザーが追加されると、 [ `onMembersAdded` アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)が表示されます。
1. アプリがインストールされているチーム内の [チャネルの一覧](~/bots/how-to/get-teams-context.md) を取得できます。
1. アプリがインストールされているチームの [メンバーの一覧](~/bots/how-to/get-teams-context.md) を取得できます。
1. お客様が受け取るすべてのアクティビティに必要な情報が含まれています。

情報を取得する方法に関係なく、 `tenantId` `userId` 新しい会話を作成するために、とのどちらか一方またはを格納する必要があり `channelId` ます。 を使用して、 `teamId` チームの一般または既定のチャネルに新しい会話スレッドを作成することもできます。

は `userId` Bot Id と特定のユーザーに固有のものであり、ボット間で使用することはできません。 `channelId`はグローバルですが、積極的なメッセージをチャネルに送信する前に、その bot をチームにインストールする_必要があり_ます。

## <a name="create-the-conversation"></a>会話を作成する

ユーザー/チャネル情報を取得したら、会話を作成する必要があります (または、不明な場合 `conversationId` )。 会話を作成するのは1回だけにしてください。 `conversationId` 今後使用する値またはオブジェクトを保存してください `conversationReference` 。

## <a name="get-the-conversation-id"></a>会話 ID を取得する

会話が作成されたら、オブジェクトまたはを使用して `conversationReference` `conversationId` メッセージを送信し `tenantId` ます。 この Id は、会話を作成するか、そのコンテキストから送信されたすべてのアクティビティから保存することによって取得できます。 この Id が格納されていることを確認してください。

## <a name="send-the-message"></a>メッセージを送信する

これで、適切な住所情報が得られたので、メッセージを送信することができます。 SDK を使用している場合は、メソッドを使用して、 `continueConversation` およびを `conversationId` 直接 API 呼び出しを行うようにし `tenantId` ます。  メッセージを正常に送信するには、適切に設定する必要があり `conversationParameters` ます。以下の [例](#examples) を参照するか、「 [参照](#references) 」セクションに記載されているサンプルのいずれかを使用してください。

## <a name="best-practices-for-proactive-messaging"></a>事前メッセージのベストプラクティス

事前にメッセージをユーザーに送信することは、ユーザーとの通信に非常に効果的な方法となります。 ただし、このメッセージは完全に表示されないように表示されるため、ウェルカムメッセージの場合はアプリを初めて操作したときになります。 そのため、この機能を多用しない (ユーザーにスパムを行わない) ことと、ユーザーが伝達されている理由をユーザーが理解できる情報を提供することが非常に重要です。

### <a name="welcome-messages"></a>ウェルカム メッセージ

事前メッセージを使用して、ユーザーにウェルカムメッセージを送信する場合は、メッセージを受信する多くのユーザーにとって、そのメッセージを受信する理由のコンテキストはないことに注意してください。 これは、アプリを初めて使用したときにも使用されます。最初の印象を得ることをお勧めします。 推奨されるウェルカムメッセージは次のとおりです。

* **ユーザーがメッセージを受信する理由。** ユーザーがメッセージを受信する理由を明確にする必要があります。 Bot がチャネルにインストールされていて、すべてのユーザーにウェルカムメッセージを送信した場合は、インストールされているチャネルと、インストールされている可能性のあるチャネルを知らせます。
* **何を提供するか。** アプリでできること どのような値にすることができますか。
* **次の手順を実行します。** コマンドを試したり、何らかの方法でアプリを操作したりするように招待します。

重要ではないウェルカムメッセージは、ユーザーが bot をブロックする可能性があることに注意してください。 ウェルカムメッセージの作成には、十分な時間を費やす必要があります。また、必要な効果を持っていない場合は、それらに対して反復処理を行う必要があります。

### <a name="notification-messages"></a>通知メッセージ

事前メッセージを使用して通知を送信する場合は、ユーザーが通知に基づいて一般的な操作を実行するための明確なパスを持っていることと、通知が発生した理由を明確に理解していることを確認する必要があります。 適切な通知メッセージには、通常次のものが含まれます。

* **どうしたのですか。** 通知を発生させた理由を明確に示します。
* **結果は何ですか。** 通知を発生させるためにアイテムまたはアイテムが更新されたことを明確にする必要があります。
* **誰がトリガーしたか。** 通知が送信された原因となった操作を実行したユーザーまたは対象。
* **ユーザーが応答で実行できること。** ユーザーが通知に基づいて操作を簡単に実行できるようにします。
* **ユーザーはどのようにして脱退できますか。** ユーザーが追加の通知をオプトアウトするためのパスを指定する必要があります。

## <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリを事前にインストールする

> [!Note]
> Microsoft Graph を使用してアプリを事前にインストールするのは、現在ベータ版です。

場合によっては、既にインストールされていない、またはアプリと対話していないメッセージユーザーを予防的に行う必要があります。 たとえば、 [会社の communicator](~/samples/app-templates.md#company-communicator) を使用して組織全体にメッセージを送信するとします。 このシナリオでは、Graph API を使用して、ユーザー用のアプリを事前にインストールし、 `conversationUpdate` インストール時にアプリが受け取るイベントから必要な値をキャッシュすることができます。

組織のアプリカタログまたは Teams アプリストアにあるアプリのみをインストールできます。

[Microsoft graph を使用する Teams で](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)は、graph のドキュメントの「[ユーザー用アプリのインストール](/graph/teams-proactive-messaging)」および「事前のボットのインストールとメッセージング」を参照してください。 GitHub プラットフォームには、 [Microsoft .net framework サンプル](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  もあります。

## <a name="examples"></a>例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```javascript

async messageAllMembersAsync(context) {
    const members = await this.getPagedMembers(context);

    members.forEach(async (teamMember) => {
        const message = MessageFactory.text('Hello ${ teamMember.givenName } ${ teamMember.surname }. I\'m a Teams conversation bot.');

        var ref = TurnContext.getConversationReference(context.activity);
        ref.user = teamMember;

        await context.adapter.createConversation(ref,
            async (t1) => {
                const ref2 = TurnContext.getConversationReference(t1.activity);
                await t1.adapter.continueConversation(ref2, async (t2) => {
                    await t2.sendActivity(message);
                });
            });
    });

    await context.sendActivity(MessageFactory.text('All messages have been sent.'));
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _message_all_members(self, turn_context: TurnContext):
    team_members = await self._get_paged_members(turn_context)

    for member in team_members:
        conversation_reference = TurnContext.get_conversation_reference(
            turn_context.activity
        )

        conversation_parameters = ConversationParameters(
            is_group=False,
            bot=turn_context.activity.recipient,
            members=[member],
            tenant_id=turn_context.activity.conversation.tenant_id,
        )

        async def get_ref(tc1):
            conversation_reference_inner = TurnContext.get_conversation_reference(
                tc1.activity
            )
            return await tc1.adapter.continue_conversation(
                conversation_reference_inner, send_message, self._app_id
            )

        async def send_message(tc2: TurnContext):
            return await tc2.send_activity(
                f"Hello {member.name}. I'm a Teams conversation bot."
            )

        await turn_context.adapter.create_conversation(
            conversation_reference, get_ref, conversation_parameters
        )

    await turn_context.send_activity(
        MessageFactory.text("All messages have been sent")
    )

```

# <a name="json"></a>[JSON](#tab/json)

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

---

## <a name="references"></a>関連情報

以下に、公式な予防的なメッセージングサンプルを示します。

|  いいえ。  | サンプル名           | 説明                                                                      | .NET    | JavaScript   | Python  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|57|Teams の会話の基礎  | 1対1の事前メッセージを送信するなど、Teams での会話の基本を示します。|[.NET &nbsp; コア](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|58|チャネルで新しいスレッドを開始する     | チャネルに新しいスレッドを作成する方法について説明します。 |[.NET &nbsp; コア](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

次の例は、(オブジェクトを使用せずに) 事前にメッセージを送信するために必要な最小限の情報を示して `conversationReference` います。 このサンプルは、REST API 呼び出しを直接使用している場合や、完全なオブジェクトが格納されていない場合に役立ち `conversationReference` ます。

* [Teams の予防的なメッセージング](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a>その他のコードを表示する
>
> [!div class="nextstepaction"]
> [**Teams の予防的なメッセージングコードサンプル**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>