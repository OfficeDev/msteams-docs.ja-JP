---
title: ボットとのチャネルとグループの会話
author: clearab
description: チャネルまたはグループ チャットでボットのメッセージを送信、受信、および処理する方法。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: cbc82471ce31edaf733bde6951648af86842ab62
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020934"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>ボットとのチャネルチャットとグループ チャットの会話

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

チームまたはグループ チャットに Microsoft Teams ボットをインストールするには、ボットに `teams` スコープ `groupchat` を追加します。 これにより、会話のすべてのメンバーがボットと対話できるようになります。 ボットをインストールすると、会話に関するメタデータ (会話メンバーの一覧など) にアクセスできます。 また、チームにインストールすると、ボットは、そのチームに関する詳細とチャネルの完全なリストにアクセスできます。

グループまたはチャネル内のボットは、メッセージが言及されている場合にのみメッセージを受信します `@botname` 。 会話に送信された他のメッセージは受信しません。

> [!NOTE]
> ボットは直接である必要 `@mentioned` があります。 チームまたはチャネルが言及された場合、またはボットからメッセージに返信しても、ボットはメッセージを受信@mentioningされません。

## <a name="design-guidelines"></a>デザインのガイドライン

個人用チャットとは異なり、グループ チャットやチャネルでは、ボットが簡単な概要を提供する必要があります。 これらのボットの設計ガイドラインに従う必要があります。 Teams でボットを設計する方法の詳細については、「チャネルとチャットでボットの会話を設計する方法」 [を参照してください](~/bots/design/bots.md)。

これで、新しい会話スレッドを作成し、チャネル内の異なる会話を簡単に管理できます。

## <a name="create-new-conversation-threads"></a>新しいスレッドの作成

ボットがチームにインストールされている場合は、既存のスレッドに返信するのではなく、新しいスレッドを作成する必要があります。 2 つの会話を区別することは困難な場合があります。 スレッド化された会話の場合は、チャネルでさまざまな会話を整理して管理する方が簡単です。 これは、プロアクティブ メッセージング [の形式です](~/bots/how-to/conversations/send-proactive-messages.md)。

次に、オブジェクトを使用してメンションを取得し、オブジェクトを使用して `entities` メッセージにメンションを追加 `Mention` できます。

## <a name="work-with-mentions"></a>メンションを使用する

グループまたはチャネルからボットに送信されるメッセージには、@mentionに名前が含まれているメッセージが含まれる。 メッセージの解析でメッセージが処理@mention。 ボットは、メッセージに記載されている他のユーザーを取得し、送信するメッセージにメンションを追加することもできます。

また、ボットが受信したメッセージ@mentionsコンテンツから削除する必要があります。

### <a name="retrieve-mentions"></a>メンションの取得

メンションはペイロード内のオブジェクトに返され、ユーザーの一意の ID と、指定したユーザーの `entities` 名前の両方が含まれます。 メッセージのテキストには、次のようなメンションも含まれます `<at>@John Smith<at>` 。 ただし、メッセージ内のテキストを使用して、ユーザーに関する情報を取得しない。 メッセージを送信するユーザーがメッセージを変更することができます。 したがって、オブジェクトを使用 `entities` します。

メッセージ内のすべてのメンションを取得するには、Bot Builder SDK で関数を呼び出し、オブジェクトの `GetMentions` 配列を返 `Mention` します。

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

ボットは、チャネルに投稿されたメッセージで他のユーザーに言及できます。

オブジェクト `Mention` には、次の 2 つのプロパティを使用して設定する必要があります。

* メッセージ <at>の@username</at> にデータを含める。
* エンティティ コレクション内にメンション オブジェクトを含める。

Bot Framework SDK には、メンションを作成するヘルパー メソッドとオブジェクトが含まれています。

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

配列 `text` 内のオブジェクトのフィールドは、メッセージ `entities` フィールドの一部と一致している必要 `text` があります。 指定しない場合、メンションは無視されます。

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

これで、ボットが最初にインストールまたはグループまたはチームに追加された場合に、概要メッセージを送信できます。

## <a name="send-a-message-on-installation"></a>インストール時にメッセージを送信する

ボットが最初にグループまたはチームに追加された場合は、紹介メッセージを送信する必要があります。 メッセージには、ボットの機能とボットの機能の使い方について簡単に説明する必要があります。 eventType を使用して `conversationUpdate` イベントをサブスクライブする `teamMemberAdded` 必要があります。  イベントは、新しいチーム メンバーが追加された場合に送信されます。 追加された新しいメンバーがボットか確認します。 詳細については、「ウェルカム [メッセージを新しいチーム メンバーに送信する」を参照してください](~/bots/how-to/conversations/send-proactive-messages.md)。

ボットが追加された場合、各チーム メンバーに個人メッセージを送信します。 これを行うには、チーム名簿を取得し、各ユーザーに直接メッセージを送信します。

次の場合は、メッセージを送信しない。

* チームは大きい (たとえば、100 人を超えるメンバー) です。 ボットはスパムと見なされ、追加したユーザーは苦情を受け取ることができます。 ウェルカム メッセージを見たすべてのユーザーに、ボットの価値提案を明確に伝える必要があります。
* ボットは、最初にチームに追加されるのではなく、グループまたはチャネルで最初に言及されます。
* グループまたはチャネルの名前が変更されます。
* チーム メンバーがグループまたはチャネルに追加されます。

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [チームのコンテキストを取得します](~/bots/how-to/get-teams-context.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会話イベントにサブスクライブする](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
