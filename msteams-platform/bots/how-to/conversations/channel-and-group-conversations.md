---
title: ボットを使用したチャネルとグループの会話
author: surbhigupta
description: チャネルまたはグループ チャットでボットのメッセージを送信、受信、処理する方法。 コード サンプルを使用して@mentionsを使用して、設計ガイドライン、会話スレッドを作成する方法について説明します
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 6b3adf491ccfed2401308f0b6d283047f24f91e2
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757179"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>ボットとのチャネルおよびグループ チャットの会話

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Microsoft Teams ボットをチームまたはグループ チャットにインストールするには、ボットに`teams`スコープを追加します`groupchat`。 これにより、会話のすべてのメンバーがボットと対話できるようになります。 ボットがインストールされると、会話メンバーの一覧など、会話に関するメタデータにアクセスできます。 また、チームにインストールされると、ボットはそのチームに関する詳細とチャネルの完全なリストにアクセスできます。

グループまたはチャネル内のボットは、@botnameに言及された場合にのみメッセージを受信します。 会話に送信された他のメッセージは受信しません。 ボットは直接 @メンションされる必要があります。 チームまたはチャネルがメンションされたとき、またはボットからメッセージに返信したときにボットがメッセージを@mentioningしない場合、ボットはメッセージを受け取りません。

> [!NOTE]
> この機能は現在、 [パブリック開発者向けプレビュー](../../../resources/dev-preview/developer-preview-intro.md) でのみ使用できます。
>
> リソース固有の同意 (RSC) を使用すると、ボットは、インストールされているチーム内のすべてのチャネル メッセージを@mentionedせずに受信できます。 詳細については、「 [RSC を使用してすべてのチャネル メッセージを受信する](channel-messages-with-rsc.md)」を参照してください。
>
> メッセージまたはアダプティブ カードをプライベート チャネルに投稿することは現在サポートされていません。

## <a name="design-guidelines"></a>デザインのガイドライン

個人用チャットとは異なり、グループ チャットやチャネルでは、ボットで簡単な概要を提供する必要があります。 以上のボット設計ガイドラインに従う必要があります。 Teamsでボットを設計する方法の詳細については、[チャネルとチャットでボットの会話を設計する方法](~/bots/design/bots.md)を参照してください。

これで、新しい会話スレッドを作成し、チャネル内のさまざまな会話を簡単に管理できます。

## <a name="create-new-conversation-threads"></a>新しい会話スレッドを作成する

ボットがチームにインストールされている場合は、既存のスレッドに返信するのではなく、新しい会話スレッドを作成する必要があります。 2 つの会話を区別するのは困難な場合があります。 会話がスレッド化されている場合は、チャネル内のさまざまな会話を整理および管理する方が簡単です。 これは [プロアクティブ メッセージング](~/bots/how-to/conversations/send-proactive-messages.md)の形式です。

次に、オブジェクトを使用してメンションを `entities` 取得し、そのオブジェクトを使用してメッセージにメンションを `Mention` 追加できます。

## <a name="work-with-mentions"></a>メンションを操作する

グループまたはチャネルからボットに送信されるすべてのメッセージには、メッセージ テキストにその名前を持つ@mentionが含まれています。 ボットは、メッセージで言及されている他のユーザーを取得し、送信するすべてのメッセージにメンションを追加することもできます。

また、ボットが受信するメッセージのコンテンツから@mentionsを取り除く必要もあります。

### <a name="retrieve-mentions"></a>メンションを取得する

メンションはペイロード内のオブジェクトに `entities` 返され、ユーザーの一意の ID と、言及されたユーザーの名前の両方が含まれます。 メッセージのテキストには、次のような `<at>@John Smith<at>`メンションも含まれます。 ただし、メッセージ内のテキストに依存してユーザーに関する情報を取得しないでください。 メッセージを送信するユーザーが変更する可能性があります。 そのため、オブジェクトを使用します `entities` 。

メッセージ内のすべてのメンションを取得するには、オブジェクトの配列`Mention`を`GetMentions`返す Bot Builder SDK で関数を呼び出します。

次のコードは、メンションを取得する例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    Mention[] mentions = turnContext.Activity.GetMentions();
    if(mentions != null)
    {
        ChannelAccount firstMention = mentions[0].Mentioned;
        await turnContext.SendActivityAsync($"Hello {firstMention.Name}");
    }
    else
    {
        await turnContext.SendActivityAsync("Aw, no one was mentioned.");
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mentions = TurnContext.getMentions(turnContext.activity);
    if (mentions){
        const firstMention = mentions[0].mentioned;
        await turnContext.sendActivity(`Hello ${firstMention.name}.`);
    } else {
        await turnContext.sendActivity(`Aw, no one was mentioned.`);
    }

    await next();
});
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[Python](#tab/python)

```python
@staticmethod
def get_mentions(activity: Activity) -> List[Mention]:
    result: List[Mention] = []
    if activity.entities is not None:
        for entity in activity.entities:
            if entity.type.lower() == "mention":
                    result.append(entity)
     return result
```

* * *

### <a name="add-mentions-to-your-messages"></a>メッセージにメンションを追加する

ボットは、チャネルに投稿されるメッセージで他のユーザーをメンションできます。

`Mention`オブジェクトには、次のプロパティを使用して設定する必要がある 2 つのプロパティがあります。

* メッセージ テキスト *に@username* を含めます。
* エンティティ コレクション内にメンション オブジェクトを含めます。

Bot Framework SDK には、メンションを作成するためのヘルパー メソッドとオブジェクトが用意されています。

次のコードは、メッセージにメンションを追加する例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="json"></a>[JSON](#tab/json)

配列内のオブジェクト内のフィールドは `text` 、 `entities` メッセージ `text` フィールドの一部と一致する必要があります。 そうでない場合、メンションは無視されます。

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _mention_activity(self, turn_context: TurnContext):
        mention = Mention(
            mentioned=turn_context.activity.from_property,
            text=f"<at>{turn_context.activity.from_property.name}</at>",
            type="mention"
        )

        reply_activity = MessageFactory.text(f"Hello {mention.text}")
        reply_activity.entities = [Mention().deserialize(mention.serialize())]
        await turn_context.send_activity(reply_activity)
```

* * *

これで、ボットが最初にインストールまたはグループまたはチームに追加されたときに、概要メッセージを送信できるようになりました。

## <a name="send-a-message-on-installation"></a>インストール時にメッセージを送信する

ボットが最初にグループまたはチームに追加されたら、概要メッセージを送信する必要があります。 メッセージには、ボットの機能とその使用方法について簡単に説明する必要があります。 eventType を使用してイベントを `conversationUpdate` サブスクライブする `teamMemberAdded` 必要があります。  イベントは、新しいチーム メンバーが追加されたときに送信されます。 追加された新しいメンバーがボットであるかどうかを確認します。 詳細については、 [新しいチーム メンバーにウェルカム メッセージを送信する方法に関するページを](~/bots/how-to/conversations/send-proactive-messages.md)参照してください。

ボットが追加されたときに、各チーム メンバーに個人用メッセージを送信します。 これを行うには、チーム名簿を取得し、各ユーザーにダイレクト メッセージを送信します。

次の場合は、メッセージを送信しないでください。

* チームは大きく、たとえば 100 人を超えるメンバーです。 ボットはスパムと見なされ、それを追加したユーザーは苦情を受け取ることができます。 ウェルカム メッセージを表示するすべてのユーザーに、ボットの価値提案を明確に伝える必要があります。
* ボットは、最初にチームに追加されるのではなく、グループまたはチャネルで最初に言及されます。
* グループまたはチャネルの名前が変更される。
* チーム メンバーがグループまたはチャネルに追加される。

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

[ステップ バイ ステップ ガイド](../../../sbs-teams-conversation-bot.yml)に従って、会話型ボットTeams作成します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [会話イベントにサブスクライブする](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="see-also"></a>関連項目

[Teams のコンテキストを取得する](~/bots/how-to/get-teams-context.md)
