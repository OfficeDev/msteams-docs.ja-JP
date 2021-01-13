---
title: ボットとのチャネル会話とグループ会話
author: clearab
description: チャネルまたはグループ チャットでボットのメッセージを送信、受信、処理する方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8a9a58208fff5cc2fe376fcb9932bad6ac2bf36f
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797842"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Microsoft Teams ボットとのチャネルとグループ チャットの会話

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

ボットに `teams` スコープを追加することで、チームチャットまたはグループ チャットにインストール `groupchat` できます。 これにより、会話のすべてのメンバーがボットと対話できるようになります。 インストールされたボットは、会話メンバーのリストなど、会話に関するメタデータにもアクセスできるようになります。チームにインストールされた場合、そのチームに関する詳細とチャネルの完全な一覧にアクセスできるようになります。

グループまたはチャネル内のボットは、メッセージが記載されている場合 (@botname) にのみメッセージを受信します。会話に送信された他のメッセージは受信しません。

> [!NOTE]
> ボットは直接 @メンションされる必要があります。 チームまたはチャネルが言及されている場合や、ボットからのメッセージに返信したユーザーがメッセージに応答しない場合、ボットはメッセージ@mentioningされません。

## <a name="design-guidelines"></a>デザインのガイドライン

チャネルとチャットで [ボットの会話を設計する方法を参照してください](~/bots/design/bots.md)。

## <a name="creating-new-conversation-threads"></a>新しい会話スレッドの作成

ボットがチームにインストールされている場合、既存の会話スレッドに返信するのではなく、新しい会話スレッドを作成する必要がある場合があります。 これはプロアクティブ メッセージング [の 1 つの形式です](~/bots/how-to/conversations/send-proactive-messages.md)。

## <a name="working-with-mentions"></a>メンションの操作

グループやチャネルからボットに送信されるすべてのメッセージには、メッセージのテキストにボット自身の名前の付いた @メンションが含まれているため、メッセージ解析でメンションが確実に処理されるようにする必要があります。 ボットは、メッセージ内でメンションされている他のユーザーを取得したり、ボットが送信するすべてのメッセージにメンションを追加したりすることもできます。

### <a name="stripping-mentions-from-message-text"></a>メッセージ テキストからメンションを削除する

ボットが受け取ったメッセージのテキストから @メンションを取り除く必要がある場合があります。

### <a name="retrieving-mentions"></a>メンションの取得

メンションはペイロード内のオブジェクトで返され、ユーザーの一意の ID と、ほとんどの場合、メンションされたユーザーの名前の両方 `entities` が含まれます。 メッセージのテキストには、`<at>@John Smith<at>` のようなメンションも含まれます。 ただし、メッセージ内のテキストを使用してユーザーに関する情報を取得する必要があります。メッセージを送信したユーザーがメッセージを変更する可能性があります。 代わりに、オブジェクトを使用 `entities` します。

オブジェクトの配列を返す Bot Builder SDK の関数を呼び出すことによって、メッセージ内のすべてのメンション `GetMentions` を取得 `Mention` できます。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

### <a name="adding-mentions-to-your-messages"></a>メッセージへのメンションの追加

ボットは、チャネルに投稿されたメッセージで他のユーザーをメンションできます。 これを行うには、メッセージで次の操作を行う必要があります。

この `Mention` オブジェクトには、次の 2 つのプロパティを設定する必要があります。

* メッセージ <at>@username</at> にメッセージを含める
* entities コレクション内に mention オブジェクトを含める

Bot Framework SDK には、メンションを簡単に構築するためのヘルパー メソッドとオブジェクトが含まれています。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

配列 `text` 内のオブジェクトのフィールド `entities` は、メッセージ *フィールドの一* 部と完全に一致している必要 `text` があります。 指定しない場合、メンションは無視されます。

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

## <a name="sending-a-message-on-installation"></a>インストール時にメッセージを送信する

ボットが最初にグループまたはチームに追加された場合、ボットを紹介するメッセージを送信すると便利な場合があります。 メッセージには、ボットの機能の簡単な説明と、その使い方が記載されている必要があります。 eventType を使用して `conversationUpdate` イベントをサブスクライブ `teamMemberAdded` する必要があります。  イベントは新しいチーム メンバーが追加された際に送信されます。このイベントは、追加された新しいメンバーがボットかどうかを確認する必要があります。 詳細 [については、「新しいチーム メンバーへのウェルカム メッセージ](~/bots/how-to/conversations/send-proactive-messages.md) の送信」を参照してください。

ボットを追加するときに、チームの各メンバーに個人用メッセージを送信する必要がある場合があります。 これを行うには、チーム名簿を取得し、各ユーザーに直接メッセージを送信します。

次の状況では、メッセージを送信する方法は推奨されません。

* チームは大規模です (明らかに主観的ですが、たとえば 100 人を超えるメンバー)。 ボットは "spammy" と見なされ、ボットを追加したユーザーは、ウェルカム メッセージを見たすべてのユーザーにボットの価値提案を明確に伝えられない限り、苦情を受け取る可能性があります。
* ボットは最初にグループまたはチャネルで言及されます (最初にチームに追加されるのとは比較して)
* グループまたはチャネルの名前が変更される
* チーム メンバーがグループまたはチャネルに追加される

## <a name="learn-more"></a>詳細情報

ボットは、インストールされているグループ チャットまたはチームに関する追加情報にアクセスできます。 ボット [で利用できる追加の](~/bots/how-to/get-teams-context.md) API については、チームのコンテキストの取得に関するページをご覧ください。

ボットがサブスクライブして応答できる追加のイベントも用意されています。 その [方法については、会話イベントのサブスクライブ](~/bots/how-to/conversations/subscribe-to-conversation-events.md) に関するページをご覧ください。

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
