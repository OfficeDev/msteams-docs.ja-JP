---
title: プロアクティブ メッセージを送信する
description: Microsoft Teams ボットを使用して、プロアクティブメッセージを送信する方法について説明します。
ms.topic: overview
ms.author: anclear
Keywords: メッセージの送信、ユーザー ID の取得、チャネル ID の取得、会話 ID の取得
ms.openlocfilehash: 2d7ff10469a181bb06fda5029c8f6b2725b0402d
ms.sourcegitcommit: 7db6eabe3ef128ac7f14b32d07e9e86c995d187f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2021
ms.locfileid: "50103606"
---
# <a name="send-proactive-messages"></a>プロアクティブ メッセージを送信する

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

プロアクティブ メッセージとは、ユーザーからのリクエストに直接応答しないボットによって送信されるメッセージのことです。 これには、次のようなメッセージを含むことができます。

* ウェルカム メッセージ
* 通知
* 予定されたメッセージ

ボットがプロアクティブ メッセージを送信するには、メッセージを送信したいユーザー、グループ チャット、またはチームにアクセスできる必要があります。 グループ チャットやチームの場合は、最初にボットを含むアプリをその場所にインストールする必要があります。 必要に応じて、チーム内で [Graph を使用してアプリをプロアクティブにインストール](#proactively-install-your-app-using-graph)したり、[アプリ ポリシー](/microsoftteams/teams-custom-app-policies-and-settings)を使用して、テナント内のチームやユーザーにアプリをプッシュしたりすることができます。 ユーザーの場合、自分でアプリをインストールしているか、アプリがインストールされているチームのメンバーである必要があります。

プロアクティブ メッセージを送ることは、通常のメッセージを送ることとは異なります。 その中で、返信に使うアクティブな `turnContext` はありません。 また、メッセージを送信する前に会話を作成する必要がある場合もあります。 たとえば、新しい 1 対 1 のチャットやチャネル内の新しい会話スレッドなどです。 プロアクティブ メッセージングでは、新しいグループ チャットやチーム内の新しいチャネルを作成することはできません。

大局的には、プロアクティブ メッセージを送信するために完了する必要がある手順は次のとおりです。

1. [ユーザー ID またはチーム/チャネル ID を取得します](#get-the-user-id-or-teamchannel-id) (必要な場合)。
1. [会話または会話スレッドを作成します](#create-the-conversation) (必要な場合)。
1. [会話ID を取得します](#get-the-conversation-id)。
1. [メッセージを送信します](#send-the-message)。

[サンプル](#examples)セクションのコード スニペットは、1 対 1 の会話を作成するためのものです。 1 対 1 の会話とグループやチャネルの両方に向けた完全な作業サンプルへのリンクについては、[コード サンプル](#code-samples)を参照してください。

## <a name="get-the-user-id-or-teamchannel-id"></a>ユーザー ID またはチーム/チャネル ID を取得する

チャネルで新しい会話や会話スレッドを作成するには、適切な ID が必要です。 この ID は複数の方法で受信または取得することができます。

1. アプリが特定のコンテキストでインストールされると、[`onMembersAdded`アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)を受信します。
1. アプリがインストールされているコンテキストに新しいユーザーが追加されると、[`onMembersAdded`アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)を受信します。
1. アプリがインストールされているチームで[チャネルのリスト](~/bots/how-to/get-teams-context.md)を取得することができます。
1. アプリがインストールされているチームで[メンバー リスト](~/bots/how-to/get-teams-context.md)を取得することができます。
1. ボットが受け取るすべてのアクティビティには、必要な情報が含まれている必要があります。

情報を取得する方法に関わらず、`tenantId`、`userId`、`channelId` のいずれかを保存しておかないと、新たな会話が作成されません。 `teamId` を使って、チームの一般チャネルや既定のチャネルに新しい会話スレッドを作成することもできます。

`userId` はあなたのボット ID と特定のユーザーに固有のもので、ボット間で再利用することはできません。 `channelId` はグローバルですが、チャネルにプロアクティブ メッセージを送信するには、お使いのボットがチームにインストールされている必要があります。

## <a name="create-the-conversation"></a>会話を作成する

ユーザーやチャネルの情報を取得した後、既に存在していない場合や `conversationId` が不明である場合は会話を作成する必要があります。 会話は一度だけ作成し、今後使用する `conversationId` の値または `conversationReference` のオブジェクトを保存するようにしておく必要があります。

## <a name="get-the-conversation-id"></a>会話 ID を取得する

会話が作成されたら、`conversationReference` オブジェクト、または `conversationId` と `tenantId` を使用してメッセージを送信します。 この ID は、会話を作成するか、そのコンテキストから送信されたアクティビティから保存することで取得することができます。 この ID を必ず保存してください。

## <a name="send-the-message"></a>メッセージを送信する

正しいアドレス情報を取得したので、メッセージを送信することができます。 SDK を使用している場合は `continueConversation` メソッドを使用し、直接 API を呼び出すには `conversationId` と `tenantId` を使用します。 メッセージを正常に送信するには、`conversationParameters` を正しく設定する必要があります。 [サンプル](#examples)セクションを参照するか、[コード サンプル](#code-samples)セクションに記載されているサンプルの 1 つを使用してください。

## <a name="best-practices-for-proactive-messaging"></a>プロアクティブ メッセージングのベスト プラクティス

ユーザーにプロアクティブ メッセージを送信するのは、ユーザーと効果的なコミュニケーションを行うのに役立ちます。 しかし、ユーザーの視点から、このメッセージはプロンプトが表示されないまま表示されることがあり、ウェルカム メッセージの場合、ユーザーがあなたのアプリと対話するのは初めてのことです。 したがって、この機能は頻繁に使用せず、ユーザーにスパムを送らないようにし、ユーザーがメッセージを送信する理由を理解するために十分な情報を提供することが非常に重要です。

### <a name="welcome-messages"></a>ウェルカム メッセージ

プロアクティブ メッセージを使用してユーザーにウェルカム メッセージを送信する場合は、メッセージを受信する多くのユーザーにとってメッセージを受信する理由のコンテキストがないことに注意する必要があります。 ユーザーがあなたのアプリと対話するのは初めてであることにも注意してください。 あなたの第一印象を良くするチャンスです。 最高のウェルカム メッセージには、次のことが必ず含まれている必要があります。

* **ユーザがメッセージを受信する理由。** メッセージを受信する理由が、ユーザーにとって非常に明確でなければなりません。 あなたのボットがチャネルにインストールされていて、すべてのユーザーにウェルカム メッセージを送信した場合は、どのチャネルにインストールされ、誰がインストールしたのかを通知する必要があります。
* **提示する内容。** ユーザーはあなたのアプリで何ができるのでしょうか? ユーザーはどのような価値を得られるのでしょうか?
* **ユーザーが次にするべきこと。** コマンドを試すように招待したり、何らかの方法でアプリと対話したりします。

ウェルカム メッセージが不十分な場合、ユーザーはあなたのボットをブロックする可能性があることに注意してください。 ウェルカム メッセージを作成するのに時間をかけ、望ましい効果が得られない場合は、それを繰り返します。

### <a name="notification-messages"></a>通知メッセージ

プロアクティブ メッセージを使用して通知を送信するときは、ユーザーが通知に基づいて一般的な操作を行うための明確な道筋を示し、通知が発生した理由をユーザーに明確に理解させなければなりません。 優れた通知メッセージには、一般的に以下のようなものがあります。

* **何が起こったのですか。** 何が原因で通知が発生したのかを明確に示しています。
* **結果はどうでしたか。** どのような項目や物事が更新されて通知が発生したのかを明確にしなければなりません。
* **誰が/何がトリガーになったのですか。** 誰が、または何をして、通知を送信されることになったのか。
* **ユーザーが対応できることは何ですか。** ユーザーが通知に基づいてアクションを取ることを容易にします。
* **ユーザーがオプトアウトするにはどうすればいいですか。** ユーザーが追加の通知をオプトアウトするためのパスを提供する必要があります。

## <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリをプロアクティブにインストール

> [!Note]
> Microsoft Graph を使用したアプリのプロアクティブ インストールは、現在ベータ版です。

場合によっては、以前にアプリをインストールしていない、またはアプリと対話していないユーザーにプロアクティブにメッセージを送る必要があるかもしれません。 たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。 このシナリオでは、Graph API を使用してアプリをユーザーにプロアクティブにインストールし、インストール時にアプリが受信する `conversationUpdate` イベントから必要な値をキャッシュすることができます。

組織のアプリ カタログまたは Teams アプリ ストアにあるアプリのみインストールできます。

Graph ドキュメントの「[ユーザー向けアプリのインストール](/graph/api/userteamwork-post-installedapps)」および「[Microsoft Graph を使用した Teams でのプロアクティブ　ボットのインストールとメッセージング](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)」を参照してください。 GitHub プラットフォームには[Microsoft .NET framework サンプル](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)もあります。

## <a name="examples"></a>例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
[Route("api/notify")]
[ApiController]
public class NotifyController : ControllerBase
{
    private readonly IBotFrameworkHttpAdapter _adapter;
    private readonly string _appId;
    private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

    public NotifyController(IBotFrameworkHttpAdapter adapter, IConfiguration configuration, ConcurrentDictionary<string, ConversationReference> conversationReferences)
    {
        _adapter = adapter;
        _conversationReferences = conversationReferences;
        _appId = configuration["MicrosoftAppId"] ?? string.Empty;
    }

    public async Task<IActionResult> Get()
    {
        foreach (var conversationReference in _conversationReferences.Values)
        {
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, conversationReference, BotCallback, default(CancellationToken));
        }
        
        // Let the caller know proactive messages have been sent
        return new ContentResult()
        {
            Content = "<html><body><h1>Proactive messages have been sent.</h1></body></html>",
            ContentType = "text/html",
            StatusCode = (int)HttpStatusCode.OK,
        };
    }

    private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
    {
        // If you encounter permission-related errors when sending this message, see
        // https://aka.ms/BotTrustServiceUrl
        await turnContext.SendActivityAsync("proactive hello");
    }
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

ユーザー ID とテナント ID を入力する必要があります。 呼び出しに成功した場合、API は以下の応答オブジェクトを返します。

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a>コード サンプル

公式プロアクティブ メッセージングのサンプルは以下のとおりです。

| サンプルの名前           | 説明                                                                      | .NET    | JavaScript   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Teams での会話の基本  | 1 対 1 のプロアクティブ メッセージの送信など、Teams での会話の基本をご紹介します。|[.NET&nbsp;Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|チャネルで新しいスレッドを開始する     | チャネルで新しいスレッドを作成する方法をご紹介します。 |[.NET&nbsp;Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a>その他のコード サンプルを見る
>
> [!div class="nextstepaction"]
> [**Teams のプロアクティブ メッセージング コード サンプル**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
