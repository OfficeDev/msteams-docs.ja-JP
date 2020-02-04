---
title: チャネルとグループの会話
author: clearab
description: チャネルまたはグループのチャットで bot 宛てのメッセージを送信、受信、処理する方法について説明します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ada2839ba41e4004b5f48449f4e057830dd841b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675025"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Microsoft Teams bot によるチャネルおよびグループチャットの会話

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Bot に`teams` or `groupchat`スコープを追加することで、チームまたはグループのチャットにインストールできるようになります。 これにより、会話のすべてのメンバーが bot と対話することができます。 インストールされた後は、会話メンバーのリストと同様に会話に関するメタデータにアクセスできます。また、チームの詳細と、そのチームに関する詳細なチャネルリストがインストールされている場合。

グループまたはチャネル内のボットは、メッセージが記載されている場合にのみメッセージを受信します ("@botname")、会話に送信された他のメッセージは受信しません。

> [!NOTE]
> Bot は直接 @mentioned する必要があります。 チームまたはチャネルが言及されたとき、またはユーザーが bot からメッセージに返信したときに @mentioning せずに、そのメッセージが bot に表示されることはありません。

## <a name="design-considerations"></a>設計上の考慮事項

Bot は、グループまたはチャネル内のすべてのメンバーについて適切かつ関連性のある情報を提供する必要があります。 この会話は、グループまたはチャネルの一部であるすべてのユーザーに表示されます。 適切に設計された bot は、すべてのユーザーに値を追加することができますが、1対1の会話でより適切な情報を誤って共有することはありません。 ダイアログのようなマルチターン会話は回避する必要があります。代わりに、カードやタスクモジュールを使用して情報を収集します。

## <a name="creating-new-conversation-threads"></a>新しい会話スレッドを作成する

Bot がチームにインストールされている場合、既存のスレッドに返信するのではなく、新しい会話スレッドを作成する必要が生じることがあります。 これは、[事前メッセージ](~/bots/how-to/conversations/send-proactive-messages.md)の形式です。

## <a name="working-with--mentions"></a>@ メンションの使用

グループまたはチャネルから bot へのすべてのメッセージには、メッセージテキストに独自の名前を持つ @mention が含まれているため、メッセージ解析でそのことを確実に処理する必要があります。 Bot は、メッセージに記載されている他のユーザーを取得し、そのユーザーが送信するメッセージにメンションを追加することもできます。

### <a name="stripping-mentions-from-message-text"></a>メッセージテキストからメンションを除去する

Bot が受信するメッセージのテキストから @mentions を削除する必要がある場合があります。

### <a name="retrieving-mentions"></a>メンションの取得

メンションは、 `entities`ペイロードのオブジェクトに返され、ユーザーの一意の ID と、通常はユーザーの名前の両方が含まれます。 メッセージのテキストには、同様`<at>@John Smith<at>`の説明も含まれます。 ただし、ユーザーに関する情報を取得するために、メッセージ内のテキストに依存しないようにしてください。メッセージを送信するユーザーが変更を行うことができます。 代わりに、 `entities`オブジェクトを使用します。

メッセージ内のすべてのメンションを取得するに`GetMentions`は、オブジェクトの`Mention`配列を返す Bot ビルダー SDK の関数を呼び出します。

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

# <a name="pythontabpython"></a>[Python](#tab/python)

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

### <a name="adding-mentions-to-your-messages"></a>メッセージにメンションを追加する

Bot は、チャネルに投稿されたメッセージに他のユーザーを伝えます。 これを行うには、メッセージで次の操作を実行する必要があります。

オブジェクト`Mention`には、次の2つのプロパティを設定する必要があります。

* メッセージテキストに<at>@username</at>を含める
* エンティティのコレクション内に、メンションオブジェクトを含めます。

Bot フレームワーク SDK は、ヘルパーメソッドとオブジェクトを提供して、メンションを簡単に作成できるようにします。

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

配列内のオブジェクトのフィールドは、 `text`メッセージ** `text`フィールドの一部に正確に一致している必要があります。 `entities` そうでない場合、メンションは無視されます。

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

# <a name="pythontabpython"></a>[Python](#tab/python)

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

Bot がグループまたはチームに最初に追加されたときに、それを紹介するメッセージを送信すると便利な場合があります。 このメッセージには、bot の機能の簡単な説明とその使用方法が記載されています。 `conversationUpdate`イベントをイベントにサブスクライブするには`teamMemberAdded` 、eventType を使用します。  新しいチームメンバーが追加されたときにイベントが送信されるため、追加された新しいメンバーが bot であるかどうかを確認する必要があります。 詳細については、「[新しいチームメンバーへのウェルカムメッセージの送信](~/bots/how-to/conversations/send-proactive-messages.md)」を参照してください。

Bot が追加されたときに、チームの各メンバーに個人メッセージを送信することもできます。 これを行うには、チーム名簿を取得して、各ユーザーに直接メッセージを送信することができます。

次の状況では、メッセージを送信することはお勧めしません。

* チームは大規模です (ただし、100メンバーよりも大きいなど)。 Bot が "spammy" と表示されている可能性があります。これを追加したユーザーは、ウェルカムメッセージが表示されるすべてのユーザーに bot の価値提案を明確に伝えない限り、苦情を受けることがあります。
* Bot は、最初にグループまたはチャネルで言及されます (チームに最初に追加されるものではありません)。
* グループまたはチャネルの名前が変更された
* チームメンバーがグループまたはチャネルに追加される

## <a name="learn-more"></a>詳細情報

Bot は、インストールされているグループチャットまたはチームに関する追加情報にアクセスできます。 Bot で利用できるその他の Api については、「 [teams コンテキストを取得](~/bots/how-to/get-teams-context.md)する」を参照してください。

Bot がサブスクライブして応答できる追加のイベントもあります。 詳細については、「[会話イベントを購読](~/bots/how-to/conversations/subscribe-to-conversation-events.md)する」を参照してください。

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
