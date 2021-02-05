---
title: プロアクティブ メッセージを送信する
description: は、Microsoft Teams ボットでプロアクティブ メッセージを送信する方法について説明します。
ms.topic: overview
ms.author: anclear
Keywords: ユーザー ID チャネル ID 会話 ID を取得するメッセージを送信する
ms.openlocfilehash: 2d7ff10469a181bb06fda5029c8f6b2725b0402d
ms.sourcegitcommit: 7db6eabe3ef128ac7f14b32d07e9e86c995d187f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2021
ms.locfileid: "50103606"
---
# <a name="send-proactive-messages"></a>プロアクティブ メッセージを送信する

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

プロアクティブ メッセージとは、ユーザーからの要求に直接応答しないボットによって送信されるメッセージです。 これには、次のようなメッセージが含まれます。

* ウェルカム メッセージ
* 通知
* スケジュールされたメッセージ

ボットがプロアクティブ メッセージを送信するには、メッセージを送信するユーザー、グループ チャット、またはチームにアクセスできる必要があります。 グループ チャットまたはチームの場合は、ボットを含むアプリを最初にその場所にインストールする必要があります。 必要に[応じて、Graph](#proactively-install-your-app-using-graph)を使用してアプリを事前にチームにインストールするか[](/microsoftteams/teams-custom-app-policies-and-settings)、アプリ ポリシーを使用してテナント内のチームとユーザーにアプリをプッシュできます。 ユーザーの場合は、ユーザー用にアプリをインストールするか、アプリがインストールされているチームの一部である必要があります。

プロアクティブ メッセージの送信は、通常のメッセージの送信とは異なります。 その場合、返信に使用 `turnContext` するアクティブはありません。 メッセージを送信する前に会話を作成する必要がある場合があります。 たとえば、新しい 1 対 1 のチャットやチャネル内の新しい会話スレッドなどです。 プロアクティブ メッセージングを使用するチームで、新しいグループ チャットや新しいチャネルを作成することはできません。

プロアクティブ メッセージを送信するために完了する必要がある手順の大きなレベルは次のとおりです。

1. [ユーザー ID またはチーム/チャネル ID を取得します](#get-the-user-id-or-teamchannel-id) (必要な場合)。
1. [会話または会話スレッドを作成します](#create-the-conversation) (必要な場合)。
1. [会話 ID を取得します](#get-the-conversation-id)。
1. [メッセージを送信します](#send-the-message)。

例セクションのコード [スニペットは](#examples) 、1 対 1 の会話を作成するためのスニペットです。 1 対 1 の会話とグループまたはチャネルの両方の作業サンプルを完了するリンクについては、コード サンプルを [参照してください](#code-samples)。

## <a name="get-the-user-id-or-teamchannel-id"></a>ユーザー ID またはチーム/チャネル ID を取得する

チャネルで新しい会話または会話スレッドを作成するには、正しい ID が必要です。 この ID は、次の複数の方法で受信または取得できます。

1. アプリが特定のコンテキストでインストールされている場合、アクティビティを受信[ `onMembersAdded` します](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
1. アプリがインストールされているコンテキストに新しいユーザーが追加された場合、アクティビティを受信[ `onMembersAdded` します](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
1. アプリがインストール [されているチーム内の](~/bots/how-to/get-teams-context.md) チャネルの一覧を取得できます。
1. アプリがインストール [されているチームの](~/bots/how-to/get-teams-context.md) メンバーの一覧を取得できます。
1. ボットが受け取るすべてのアクティビティには、必要な情報が含まれている必要があります。

情報を取得する方法に関係なく、新しい会話を保存するか、新しい会話を作成 `tenantId` `userId` `channelId` する必要があります。 また、チームの一 `teamId` 般的なチャネルまたは既定のチャネルで新しい会話スレッドを作成するためにも使用できます。

ボット ID と特定のユーザーに対して一意であり、ボット間 `userId` で再使用することはできません。 グローバルですが、チャネルにプロアクティブ メッセージを送信する前に、ボットをチームに `channelId` インストールする必要があります。

## <a name="create-the-conversation"></a>会話を作成する

After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId` . 会話は 1 回だけ作成し、将来使用する値またはオブジェクト `conversationId` `conversationReference` を保存する必要があります。

## <a name="get-the-conversation-id"></a>会話 ID を取得する

会話が作成された後、オブジェクトを使用 `conversationReference` するか、メッセージ `conversationId` を `tenantId` 送信します。 この ID は、会話を作成するか、そのコンテキストから送信されたアクティビティから保存することで取得できます。 この ID を保存してください。

## <a name="send-the-message"></a>メッセージを送信する

適切なアドレス情報が得たので、メッセージを送信できます。 SDK を使用している場合は、メソッドを使用して直接 API 呼び出しを行 `continueConversation` `conversationId` `tenantId` います。 メッセージを正常に `conversationParameters` 送信するには、正しく設定する必要があります。 例の [セクションを参照](#examples) するか、コード サンプル セクションに記載されているサンプル [のいずれかを使用](#code-samples) してください。

## <a name="best-practices-for-proactive-messaging"></a>プロアクティブ メッセージングのベスト プラクティス

プロアクティブ メッセージをユーザーに送信する方法は、ユーザーと通信するための非常に効果的な方法です。 ただし、ユーザーの観点からは、このメッセージは完全に処理されていないと表示される可能性があります。ウェルカム メッセージの場合は、アプリを初めて操作します。 したがって、この機能は、ユーザーに迷惑メールを送信し、メッセージが送信される理由をユーザーが理解するのに十分な情報を提供するために、この機能を使用することが非常に重要です。

### <a name="welcome-messages"></a>ウェルカム メッセージ

プロアクティブ メッセージングを使用してユーザーにウェルカム メッセージを送信する場合、メッセージを受信するほとんどのユーザーに対して、メッセージを受信する理由に関するコンテキストがないという念頭に置く必要があります。 これは、ユーザーがアプリを初めて操作する場合にも行います。 第一印象を良くする機会です。 最適なウェルカム メッセージには、次のものが含まれる必要があります。

* **ユーザーがメッセージを受信する理由。** ユーザーがメッセージを受信する理由は非常に明確である必要があります。 ボットがチャネルにインストールされ、すべてのユーザーにウェルカム メッセージを送信した場合は、ボットがインストールされているチャネルと、インストールされている可能性のあるユーザーを知らせる必要があります。
* **何を提供します。** アプリで何ができるか。 どのような価値を持ち込むか。
* **次に何を行う必要があります。** コマンドを試したり、何らかの方法でアプリを操作したりします。

ウェルカム メッセージが不十分な場合は、ユーザーがボットをブロックする可能性があります。 ウェルカム メッセージの作成に十分な時間を費やし、望ましい効果が得ない場合は繰り返します。

### <a name="notification-messages"></a>通知メッセージ

プロアクティブ メッセージングを使用して通知を送信する場合は、通知に基づいて共通のアクションを実行するための明確なパスと、通知が発生した理由を明確に理解する必要があります。 通常、良好な通知メッセージには次のものが含まれます。

* **どうしたのですか。** 通知の原因を明確に示します。
* **結果は何でしたか。** 通知を発生するために更新されたアイテムまたはアイテムを明確に設定する必要があります。
* **誰が何をトリガーしたのか。** 通知の送信を引き起こしたアクションを実行したユーザーまたはアクション。
* **ユーザーが応答で実行できる操作。** 通知に基づいてユーザーが簡単にアクションを実行できます。
* **ユーザーがオプトアウトする方法。** ユーザーが追加の通知をオプトアウトするパスを指定する必要があります。

## <a name="proactively-install-your-app-using-graph"></a>Graph を使用してアプリを事前にインストールする

> [!Note]
> Microsoft Graph を使用してアプリを事前にインストールする機能は、現在ベータ版です。

以前にアプリをインストールまたは操作していないユーザーに事前にメッセージを送信する必要がある場合があります。 たとえば、会社のコミュニケーター [を使用](~/samples/app-templates.md#company-communicator) して組織全体にメッセージを送信する場合です。 このシナリオでは、Graph API を使用してユーザー用のアプリを事前にインストールし、インストール時にアプリが受け取ったイベントから必要な値を `conversationUpdate` キャッシュできます。

組織のアプリ カタログまたは Teams アプリ ストアにあるアプリのみをインストールできます。

Graph [ドキュメントのユーザー向けアプリの](/graph/api/userteamwork-post-installedapps) インストールと、Microsoft Graph を使用した Teams でのプロアクティブ ボットのインストール [とメッセージングに関するページをご覧ください](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。 GitHub プラットフォーム [には、Microsoft .NET フレームワーク](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) のサンプルも用意されています。

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

ユーザー ID とテナント ID を指定する必要があります。 呼び出しが成功すると、API は次の応答オブジェクトを返します。

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a>コード サンプル

公式のプロアクティブ メッセージングのサンプルは次のとおりです。

| サンプル名           | 説明                                                                      | .NET    | JavaScript   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Teams 会話の基本  | 1 対 1 のプロアクティブ メッセージの送信など、Teams での会話の基本を示します。|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|チャネルで新しいスレッドを開始する     | チャネルで新しいスレッドを作成する方法を示します。 |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a>その他のコード サンプルを表示する
>
> [!div class="nextstepaction"]
> [**Teams プロアクティブ メッセージングのコード サンプル**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
