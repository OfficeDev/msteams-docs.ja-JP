---
title: プロアクティブ メッセージを送信する
description: ボットでプロアクティブ メッセージを送信するMicrosoft Teamsします。
ms.topic: conceptual
ms.author: anclear
localization_priority: Normal
Keywords: メッセージの送信、ユーザー ID の取得、チャネル ID の取得、会話 ID の取得
ms.openlocfilehash: ae651ac94b1b092374f6fae284b67070036b561f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020920"
---
# <a name="send-proactive-messages"></a>プロアクティブ メッセージを送信する

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

プロアクティブ メッセージとは、ユーザーからの要求に応答しないボットから送信されるメッセージです。 これには、次のようなメッセージが含まれます。

* ウェルカム メッセージ
* 通知
* 予定されたメッセージ

ボットがユーザー、グループ チャット、またはチームにプロアクティブ メッセージを送信するには、そのボットにメッセージを送信するアクセス権が必要です。 グループ チャットまたはチームの場合、ボットを含むアプリを最初にその場所にインストールする必要があります。 必要に[応じて、チーム](#proactively-install-your-app-using-graph)内の Microsoft Graph を使用してアプリをプロアクティブにインストールするか[](/microsoftteams/teams-custom-app-policies-and-settings)、アプリ ポリシーを使用してアプリをテナントのチームとユーザーにプッシュできます。 ユーザーの場合、自分でアプリをインストールしているか、アプリがインストールされているチームのメンバーである必要があります。

プロアクティブ メッセージの送信は、通常のメッセージの送信とは異なります。 返信に使用 `turnContext` するアクティブはありません。 メッセージを送信する前に、会話を作成する必要があります。 たとえば、新しい 1 対 1 のチャットやチャネル内の新しい会話スレッドなどです。 プロアクティブ メッセージングでは、新しいグループ チャットやチーム内の新しいチャネルを作成することはできません。

**プロアクティブ メッセージを送信するには**

1. [必要に応じて、ユーザー ID、チーム ID、またはチャネル ID](#get-the-user-id-team-id-or-channel-id)を取得します。
1. [必要に応じて、](#create-the-conversation)会話を作成します。
1. [会話ID を取得します](#get-the-conversation-id)。
1. [メッセージを送信します](#send-the-message)。

サンプル セクションのコード スニペット [は](#samples) 、1 対 1 の会話を作成するためのコード スニペットです。 1 対 1 の会話とグループまたはチャネルの両方の作業サンプルを完了するリンクについては、コード サンプルを [参照してください](#code-sample)。

プロアクティブ メッセージを効果的に使用するには、「プロアクティブ [メッセージングのベスト プラクティス」を参照してください](#best-practices-for-proactive-messaging)。 特定のシナリオでは、アプリを使用してアプリを事前にインストールする[必要Graph。](#proactively-install-your-app-using-graph) サンプル セクションのコード スニペット [は](#samples) 、1 対 1 の会話を作成するためのコード スニペットです。 1 対 1 の会話とグループまたはチャネルの両方の完全な作業サンプルについては、コード サンプルを [参照してください](#code-sample)。

## <a name="get-the-user-id-team-id-or-channel-id"></a>ユーザー ID、チーム ID、またはチャネル ID を取得する

チャネルに新しいスレッドまたは会話スレッドを作成するには、正しい ID が必要です。 次の ID を使用して、この ID を受信または取得できます。

* アプリが特定のコンテキストにインストールされている場合は、アクティビティを受信[ `onMembersAdded` します](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* アプリがインストールされているコンテキストに新しいユーザーを追加すると、アクティビティが表示[ `onMembersAdded` されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* アプリがインストール [されているチーム内](~/bots/how-to/get-teams-context.md) のチャネルの一覧を取得できます。
* アプリがインストール [されているチームの](~/bots/how-to/get-teams-context.md) メンバーの一覧を取得できます。
* ボットが受け取るすべてのアクティビティには、必要な情報が含まれている必要があります。

情報の取得方法に関係なく、新しい会話を作成するか、またはを保存 `tenantId` `userId` `channelId` する必要があります。 `teamId` を使って、チームの一般チャネルや既定のチャネルに新しい会話スレッドを作成することもできます。

これは `userId` 、ボット ID と特定のユーザーに固有です。 間のボット `userId` を再利用することはできません。 は `channelId` グローバルです。 ただし、チャネルにプロアクティブ メッセージを送信するには、ボットをチームにインストールする必要があります。

ユーザーまたはチャネル情報を取得した後、会話を作成する必要があります。

## <a name="create-the-conversation"></a>会話を作成する

会話が存在しない場合、または会話が存在しない場合は、会話を作成する必要があります `conversationId` 。 会話は 1 回だけ作成し、値または `conversationId` オブジェクトを格納する必要 `conversationReference` があります。

会話が作成された後、会話 ID を取得する必要があります。

## <a name="get-the-conversation-id"></a>会話 ID を取得する

オブジェクトを使用 `conversationReference` するか、 `conversationId` メッセージ `tenantId` を送信します。 この ID は、会話を作成するか、そのコンテキストから送信された任意のアクティビティから保存することで取得できます。 参照用にこの ID を格納します。

適切なアドレス情報を取得した後、メッセージを送信できます。

## <a name="send-the-message"></a>メッセージを送信する

正しいアドレス情報を取得したので、メッセージを送信することができます。 SDK を使用している場合は `continueConversation` メソッドを使用し、直接 API を呼び出すには `conversationId` と `tenantId` を使用します。 メッセージを正常に送信するには、`conversationParameters` を正しく設定する必要があります。 サンプル セクション [を参照](#samples) するか、コード サンプル セクションに記載されているサンプル [のいずれかを使用](#code-sample) します。

SDK を使用している場合は、メソッドを使用し、メッセージを送信するために直接 API 呼び出しを行 `continueConversation` `conversationId` `tenantId` う必要があります。 メッセージを正常に送信するには、`conversationParameters` を正しく設定する必要があります。

プロアクティブ メッセージを送信したので、ユーザーとボット間の情報交換を向上するために、プロアクティブ メッセージを送信しながら、次のベスト プラクティスに従う必要があります。

## <a name="best-practices-for-proactive-messaging"></a>プロアクティブ メッセージングのベスト プラクティス

ユーザーにプロアクティブ メッセージを送信するのは、ユーザーと効果的なコミュニケーションを行うのに役立ちます。 しかし、ユーザーの視点から、このメッセージはプロンプトが表示されないまま表示されることがあり、ウェルカム メッセージの場合、ユーザーがあなたのアプリと対話するのは初めてのことです。 そのため、ユーザーに迷惑メールを送信するのではなく、プロアクティブ メッセージングを使用し、ユーザーがメッセージを受信する理由を理解するのに十分な情報を提供することが非常に重要です。

### <a name="welcome-messages"></a>ウェルカム メッセージ

プロアクティブ メッセージングを使用してウェルカム メッセージをユーザーに送信する場合、ユーザーがメッセージを受信する理由に関するコンテキストはありません。 また、ユーザーがアプリを操作するのも初めてです。 良い第一印象を生み出す機会です。 最高のウェルカム メッセージには、次のことが必ず含まれている必要があります。

* ユーザーがメッセージを受信する理由: メッセージを受信する理由は、ユーザーに明確である必要があります。 ボットがチャネルにインストールされ、すべてのユーザーにウェルカム メッセージを送信した場合は、そのボットがインストールされたチャネルとインストールしたユーザーを通知します。
* 提供する機能: ユーザーは、アプリで実行できる操作と、アプリにどのような値を提供できるのかを特定できる必要があります。
* 次に実行する操作: ユーザーにコマンドの試用やアプリの操作を招待します。

ウェルカム メッセージが不十分な場合、ユーザーがボットをブロックする可能性があります。 ポイントに書き込み、ウェルカム メッセージをクリアします。 ウェルカム メッセージが目的の効果を持たない場合は、メッセージを反復処理します。

### <a name="notification-messages"></a>通知メッセージ

プロアクティブ メッセージングを使用して通知を送信するには、ユーザーが通知に基づいて一般的なアクションを実行するための明確なパスを持っている必要があります。 ユーザーが通知を受け取った理由を明確に理解してください。 良好な通知メッセージには、通常、次のものが含まれます。

* 何が起こったか: 通知の原因を明確に示します。
* 結果は何でした: 通知を発生するために更新されたアイテムを明確にする必要があります。
* Whoトリガーされたイベント:Who通知の送信を引き起こしたアクションを指定します。
* ユーザーが応答で実行できる操作: 通知に基づいてユーザーが簡単にアクションを実行できます。
* ユーザーがオプトアウトする方法: ユーザーが追加の通知をオプトアウトするパスを指定する必要があります。

大規模なグループのユーザー (組織など) にメッセージを送信するには、アプリを事前にインストールGraph。

### <a name="scheduled-messages"></a>予定されたメッセージ

プロアクティブ メッセージングを使用してスケジュールされたメッセージをユーザーに送信する場合は、タイム ゾーンがタイム ゾーンに更新されるのを確認します。 これにより、メッセージが関連する時刻にユーザーに配信されます。 通常、スケジュール メッセージには次のものが含まれます。

* ユーザーがメッセージを受信する理由: ユーザーがメッセージを受け取る理由を簡単に理解できます。
* ユーザーが次に実行できる操作: ユーザーは、メッセージの内容に基づいて必要なアクションを実行できます。

## <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリをプロアクティブにインストール

> [!Note]
> アプリを使用してアプリをプロアクティブにGraph現在ベータ版です。

アプリを以前にインストールまたは操作していないユーザーにプロアクティブにメッセージを送信します。 たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。 この場合、アプリ API を使用Graphユーザー向けアプリをプロアクティブにインストールできます。 インストール時にアプリが受け `conversationUpdate` 取ったイベントから必要な値をキャッシュします。

組織のアプリ カタログまたはアプリ ストア内のアプリTeamsインストールできます。

詳細[については、Graph](/graph/api/userteamwork-post-installedapps)ドキュメントのユーザー向けアプリのインストールと、TeamsでのプロアクティブボットGraphを[参照してください](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。 GitHub プラットフォームには[Microsoft .NET framework サンプル](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)もあります。

## <a name="samples"></a>サンプル

次のコードは、アプリを使用してアプリを事前にインストールする簡単なコード サンプルをGraph。

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

ユーザー ID とテナント ID を入力する必要があります。 呼び出しが成功すると、API は次の応答オブジェクトを返します。

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a>コード サンプル

次の表は、基本的な会話フローを Teams アプリケーションに組み込む簡単なコード サンプルと、Teams のチャネルで新しい会話スレッドを作成する方法を示Teams。

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Teams での会話の基本  | 1 対 1 のプロアクティブ メッセージの送信など、Teams での会話の基本をご紹介します。| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| チャネルで新しいスレッドを開始する | チャネルで新しいスレッドを作成する方法をご紹介します。 | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a>追加のコード サンプル

> [!div class="nextstepaction"]
> [Teams のプロアクティブ メッセージング コード サンプル](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [**Teamsメッセージング コードのサンプルを確認する**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp) 
> [ボット メッセージの書式設定](~/bots/how-to/format-your-bot-messages.md)
