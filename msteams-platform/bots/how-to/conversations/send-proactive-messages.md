---
title: プロアクティブ メッセージを送信する
description: Microsoft Teams ボットでプロアクティブ メッセージを送信し、Microsoft Graph を使用してアプリをプロアクティブにインストールし、Bot Framework SDK v4 に基づいてコード サンプルを確認する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: high
Keywords: メッセージの送信、ユーザー ID の取得、チャネル ID の取得、会話 ID の取得
ms.openlocfilehash: 7b1227dd69e8245b6ad318eb5e7425893075d878
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757578"
---
# <a name="proactive-messages"></a>プロアクティブ メッセージ

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

プロアクティブ メッセージは、ユーザーからの要求に応答していないボットによって送信されるメッセージです。これには、次のようなメッセージを含めることができます。

* ウェルカム メッセージ
* 通知
* 予定されたメッセージ

> [!IMPORTANT]
> 現在、ボットは Government Community Cloud (GCC) と GCC-High で利用できますが、国防総省 (DOD) では利用できません。
>
> プロアクティブ メッセージの場合、ボットは政府機関のクラウド環境に対して次のエンドポイントを使用する必要があります。
>    * GCC: `https://smba.infra.gcc.teams.microsoft.com/gcc`。
>    * GCCH: `https://smba.infra.gov.teams.microsoft.us/gcch`。

ボットがプロアクティブなメッセージをユーザー、グループ チャット、またはチームに送信するには、ボットがメッセージを送信するためのアクセス権を持っている必要があります。 グループ チャットまたはチームの場合、ボットを含むアプリを最初にその場所にインストールする必要があります。
必要に応じて、チーム内で [Microsoft Graph を使用してアプリをプロアクティブにインストール](#proactively-install-your-app-using-graph)したり、[アプリ ポリシー](/microsoftteams/teams-custom-app-policies-and-settings)を使用して、テナント内のチームやユーザーにアプリをプッシュしたりすることができます。 ユーザーの場合、自分でアプリをインストールしているか、アプリがインストールされているチームのメンバーである必要があります。

プロアクティブ メッセージの送信は、通常のメッセージの送信とは異なります。 返信に使うアクティブな `turnContext` はありません。 また、メッセージを送信する前に会話を作成する必要があります。 たとえば、新しい 1 対 1 のチャットやチャネル内の新しい会話スレッドなどです。 プロアクティブ メッセージングでは、新しいグループ チャットやチーム内の新しいチャネルを作成することはできません。

プロアクティブ メッセージを送信するには、次の手順に従います。

1. 必要に応じて、[ユーザー ID、チーム ID、またはチャネル ID](#get-the-user-id-team-id-or-channel-id) を取得します。
1. 必要に応じて[会話を作成します](#create-the-conversation)。
1. [会話ID を取得します](#get-the-conversation-id)。
1. [メッセージを送信します](#send-the-message)。

[サンプル](#samples)セクションのコード スニペットは、1 対 1 の会話を作成するためのものです。 1 対 1 の会話とグループやチャネルの両方に向けた完全な作業サンプルへのリンクについては、「[コード サンプル](#code-sample)」を参照してください。

プロアクティブメッセージを効果的に使用するには、「[プロアクティブ メッセージングのベスト プラクティス](#best-practices-for-proactive-messaging)」を参照してください。 特定のシナリオでは、[Graph を使用してアプリをプロアクティブにインストールする](#proactively-install-your-app-using-graph)必要があります。 [サンプル](#samples)セクションのコード スニペットは、1 対 1 の会話を作成するためのものです。 1 対 1 の会話とグループやチャネルの両方に向けた完全な作業サンプルについては、「[コード サンプル](#code-sample)」を参照してください。

## <a name="get-the-user-id-team-id-or-channel-id"></a>ユーザー ID、チーム ID、またはチャネル ID を取得する

チャネルで新しい会話や会話スレッドを作成するには、適切な ID がなくてはいけません。 次のいずれかを使用して、この ID を受信または取得できます。

* アプリが特定のコンテキストでインストールされると、[`onMembersAdded`アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)を受信します。
* アプリがインストールされているコンテキストに新しいユーザーが追加されると、[`onMembersAdded`アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)を受信します。
* アプリがインストールされているチームで[チャネルのリスト](~/bots/how-to/get-teams-context.md)を取得することができます。
* アプリがインストールされているチームで[メンバー リスト](~/bots/how-to/get-teams-context.md)を取得することができます。
* ボットが受け取るすべてのアクティビティには、必要な情報が含まれている必要があります。

情報を取得する方法に関わらず、`tenantId`、`userId`、`channelId` のいずれかを保存しないと、新たな会話が作成されません。 `teamId` を使って、チームの一般チャネルや既定のチャネルに新しい会話スレッドを作成することもできます。

`userId` は、ボット ID と特定のユーザーに固有です。 ボット間で `userId` を再利用することはできません。 `channelId` はグローバルです。 ただし、チャネルにプロアクティブ メッセージを送信するには、お使いのボットがチームにインストールされている必要があります。

ユーザーまたはチャネル情報を取得したら、会話を作成する必要があります。

## <a name="create-the-conversation"></a>会話を作成する

会話が存在しない場合、または `conversationId` がわからない場合は、会話を作成する必要があります。 会話は 1 回だけ作成し、`conversationId` 値または `conversationReference` オブジェクトを保存する必要があります。

会話が作成されたら、会話 ID を取得する必要があります。

## <a name="get-the-conversation-id"></a>会話 ID を取得する

メッセージを送信するには、`conversationReference` オブジェクトまたは `conversationId` か `tenantId` のいずれかを使用します。 この ID は、会話を作成するか、そのコンテキストから送信されたアクティビティから保存することで取得することができます。 参照用にこの ID を格納します。

適切なアドレス情報を取得したら、メッセージを送信できます。

## <a name="send-the-message"></a>メッセージを送信する

正しいアドレス情報を取得したので、メッセージを送信することができます。 SDK を使用している場合は、メソッドを使用し、直接 API 呼び出しを行う `continueConversation` `conversationId` `tenantId` 必要があります。 メッセージを正常に送信するには、`conversationParameters` を正しく設定する必要があります。 [サンプル](#samples)セクションを参照するか、[コード サンプル](#code-sample)セクションに記載されているサンプルの 1 つを使用してください。

プロアクティブなメッセージを送信したので、ユーザーとボットの間の情報交換を改善するために、プロアクティブなメッセージを送信する間、これらのベスト プラクティスに従う必要があります。

## <a name="best-practices-for-proactive-messaging"></a>プロアクティブ メッセージングのベスト プラクティス

ユーザーにプロアクティブ メッセージを送信するのは、ユーザーと効果的なコミュニケーションを行うのに役立ちます。 ただし、ユーザーの観点からは、メッセージはプロンプトなしで表示されます。 ウェルカム メッセージがある場合、アプリを操作するのは初めてです。 この機能を使用し、このメッセージの目的を理解するためにユーザーに完全な情報を提供することが重要です。

### <a name="welcome-messages"></a>ウェルカム メッセージ

プロアクティブ メッセージングを使用してウェルカム メッセージをユーザーに送信する場合、ユーザーがメッセージを受信する理由についてのコンテキストはありません。 また、ユーザーがアプリを操作するのはこれが初めてです。 第一印象を良くするチャンスです。 最高のウェルカム メッセージには、次のことが必ず含まれている必要があります。

* ユーザがメッセージを受信する理由。 メッセージを受信する理由が、ユーザーにとって明確でなければなりません。 あなたのボットがチャネルにインストールされていて、すべてのユーザーにウェルカム メッセージを送信した場合は、どのチャネルにインストールされ、誰がインストールしたのかを通知する必要があります。

* 提示する内容。 ユーザーは、アプリで何ができるか、そしてユーザーにどのような価値をもたらすことができるかを識別できなければなりません。

* ユーザーが次にするべきこと。 コマンドを試すか、アプリを操作するようにユーザーを招待します。
ウェルカム メッセージが不十分だと、ユーザーがボットをブロックする可能性があります。 要点を書いて、ウェルカム メッセージを明確にします。 ウェルカム メッセージが目的の効果を発揮していない場合は、ウェルカム メッセージを繰り返します。

### <a name="notification-messages"></a>通知メッセージ

プロアクティブ メッセージングを使用して通知を送信するには、通知に基づいて一般的なアクションを実行するための明確なパスがユーザーにあることを確認してください。 ユーザーが通知を受け取った理由を明確に理解していることを確認してください。 良好な通知メッセージには、通常、以下のものが含まれます。

* 何が起こったのでしょうか? 何が原因で通知が発生したのかを明確に示しています。

* 結果はどうでしたか? 通知を受け取るためにどのアイテムが更新されているかを明確にする必要があります。

* 誰が/何がトリガーになったのですか? 誰が、または何をして、通知を送信されることになったのか。

* ユーザーが対応できることは何ですか? ユーザーが通知に基づいてアクションを取ることを容易にします。

* ユーザーはどのようにオプトアウトできますか? ユーザーが追加の通知をオプトアウトするためのパスを提供する必要があります。

組織などの大規模なユーザー グループにメッセージを送信するには、 Graph を使用してアプリをプロアクティブにインストールします。

### <a name="scheduled-messages"></a>予定されたメッセージ

プロアクティブ メッセージングを使用してスケジュールされたメッセージをユーザーに送信する場合は、タイム ゾーンがユーザーのタイム ゾーンに更新されていることを確認してください。 これにより、メッセージが適切な時間にユーザーに確実に配信されます。 スケジュール メッセージには通常、次のものが含まれます。

* ユーザがメッセージを受信する理由。 ユーザーがメッセージを受信する理由を簡単に理解できるようにします。

* ユーザーは次に何ができますか? ユーザーは、メッセージの内容に基づいて必要なアクションを実行できます。

## <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリをプロアクティブにインストール

以前アプリをインストールしたり操作したりしていないユーザーにプロアクティブにメッセージを送信します。 たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。 この場合、Graph API を使用して、ユーザー向けにアプリをプロアクティブにインストールできます。 インストール時にアプリが受け取る `conversationUpdate` イベントから必要な値をキャッシュします。

組織のアプリ カタログまたは Teams アプリ ストアにあるアプリのみインストールできます。

Graph ドキュメントの「[ユーザー向けアプリのインストール](/graph/api/userteamwork-post-installedapps)」および「[Graph を使用した Teams でのプロアクティブ ボットのインストールとメッセージング](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)」を参照してください。 GitHub プラットフォームには [Microsoft .NET framework サンプル](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)もあります。

## <a name="samples"></a>サンプル

次のコードは、プロアクティブなメッセージを送信する方法を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

## <a name="code-sample"></a>コード サンプル

次の表は、基本的な会話フローを Teams アプリケーションに組み込んだ簡単なコード サンプルと、Teams のチャネルで新しい会話スレッドを作成する方法を示しています。

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Teams での会話の基本  | 1 対 1 のプロアクティブ メッセージの送信など、Teams での会話の基本をご紹介します。| [表示](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| チャネルで新しいスレッドを開始する | チャネルで新しいスレッドを作成する方法をご紹介します。 | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |
| アプリのプロアクティブ インストールとプロアクティブ通知の送信 | このサンプルは、ユーザー向けのアプリのプロアクティブなインストールを使用し、Microsoft Graph API を呼び出してプロアクティブな通知を送信する方法を示しています。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) | |

### <a name="additional-code-sample"></a>追加のコード サンプル

> [!div class="nextstepaction"]
> [Teams のプロアクティブ メッセージング コード サンプル](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

ボットからプロアクティブなメッセージを送信するのに役立つ[ステップ バイ ステップ ガイド](../../../sbs-send-proactive.yml)に従ってください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ボット メッセージの書式を設定する](~/bots/how-to/format-your-bot-messages.md)

## <a name="see-also"></a>関連項目

* [**Teams のプロアクティブ メッセージング コード サンプル**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
* [ボットとのチャネルおよびグループ チャットの会話](~/bots/how-to/conversations/channel-and-group-conversations.md)
* [タスク モジュールの送信アクションに応答する](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [ユーザーにプロアクティブ通知を送信する](/azure/bot-service/bot-builder-howto-proactive-message)
