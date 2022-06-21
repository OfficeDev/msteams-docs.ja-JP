---
title: ボットとのチャネルおよびグループ チャット会話
description: このモジュールでは、Microsoft Teamsのチャネルでボットと会話するエンドツーエンドのシナリオについて説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e93b6cc18e38da4f6307fda3d30968bfa709dbf1
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190181"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Microsoft Teams ボットとのチャネルおよびグループ チャット会話

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams でユーザーは、チャネルまたはグループ チャットの会話にボットを参加させることができます。 チームまたはチャットにボットを追加すると、会話のすべてのユーザーがボットの機能を会話内で利用できるようになります。 ボット内で、チーム情報のクエリの実行や、ユーザーの @メンションなど、Teams 固有の機能にアクセスすることもできます。

チャネルとグループ チャットでのチャットは、ユーザーがボットを@mentionする必要がある点で、個人用チャットとは異なります。 ボットが個人用、グループ チャット、チャネルなどの複数のスコープで使用されている場合は、ボット メッセージが送信されたスコープを検出し、それに応じて処理する必要があります。

## <a name="designing-a-great-bot-for-channels-or-groups"></a>チャネルまたはグループ用に優れたボットを設計する

チームに追加されたボットは、新たなチーム メンバーとなり、会話の一員として @メンションの対象になります。 実際、ボットはメッセージが@mentionedときにのみ受信されるため、チャネル上の他の会話はボットに送信されません。

グループまたはチャネル内のボットは、すべてのメンバーに関係する適切な情報を提供する必要があります。 ボットが、エクスペリエンスに関わるどんな情報でも提供できるのは確かですが、それとの会話がすべてのユーザーに表示される点に留意してください。 それで、グループまたはチャネル内の優れたボットは、すべてのユーザーに付加価値を提供するものであり、1 対 1 の会話に向いている情報を誤って共有することがないはずです。

ボットは、同様に、より多くの作業を必要とせずに、すべてのスコープで完全に関連している可能性があります。 Teamsでは、ボットがすべてのスコープで機能するとは思いませんが、サポートするスコープのうち、どのスコープでもボットがユーザーの価値を提供するようにする必要があります。 スコープの詳細については、[Microsoft Teams のアプリ](~/concepts/build-and-test/app-studio-overview.md)に関する記事を参照してください。

グループまたはチャネルで動作するボットの開発では、個人の会話と同じ機能の多くを使用します。 ペイロード内の追加のイベントとデータで、Teams のグループおよびチャネルの情報を提供します。 それらの相違点、および一般的な機能の主な相違点について、以下のセクションで説明します。

### <a name="creating-messages"></a>メッセージの作成

チャネルでメッセージを作成するボットの詳細については、「 [ボットのプロアクティブ メッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」と「チャネル会話の [作成](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)」を参照してください。

### <a name="receiving-messages"></a>メッセージの受信

グループまたはチャネル内のボットの場合、[通常のメッセージ スキーマ](https://docs.botframework.com/core-concepts/reference/#activity)に加えて、ボットは次のプロパティも受け取ります。

* `channelData` 「[Teams チャネル データ](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)」を参照してください。 グループ チャットには、そのチャットに固有の情報が含まれます。
* `conversation.id` チャネル ID と、返信チェーン内の最初のメッセージの ID で構成される返信チェーン ID です。
* `conversation.isGroup` チャネルまたはグループ チャットでのボット メッセージの場合に `true` となります。
* `conversation.conversationType` `groupChat` または `channel` のどちらかです。
* `entities` 1 つ以上のメンションを含めることができます。 詳細については、「[メンション](#-mentions)」を参照してください。

### <a name="replying-to-messages"></a>メッセージへの返信

既存のメッセージに返信するには、.NET では [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply)、Node.js では [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) を呼び出します。 Bot Builder SDK で、すべての詳細が処理されます。

REST API を使用する場合は、[`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) エンドポイントを呼び出すこともできます。

チャネルでは、メッセージへの返信は、開始された返信チェーンへの返信として示されます。 `conversation.id` には、チャネルと最上位メッセージ ID が含まれます。 Bot Framework によって詳細が処理されますが、必要に応じて、その会話スレッドへの今後の返信のために `conversation.id` をキャッシュすることができます。

### <a name="best-practice-welcome-messages-in-teams"></a>ベスト プラクティス: Teams でのウェルカム メッセージ

ボットが最初にグループまたはチームに追加されたときは、ボットを紹介するウェルカム メッセージをすべてのユーザーに送信すると便利です。 ウェルカム メッセージで、ボットの機能と、ユーザーへのメリットについて説明する必要があります。 理想的には、ユーザーがアプリとやり取りするためのコマンドもメッセージに含める必要があります。 これを行うには、`channelData` オブジェクトで `teamsAddMembers` eventType を使用して、ボットが `conversationUpdate` メッセージに応答するようにします。 ユーザーがチームに追加されるときにも同じイベントが送信されるため、必ず、`memberAdded` ID をボットのアプリ ID そのものにしてください。 詳細については、 [チーム メンバーまたはボットの追加](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) に関するページを参照してください。

ボットが追加されたときに、チームの各メンバーに個人用メッセージを送信することもできます。 これを行うには、[チーム名簿を取得](~/resources/bot-v3/bots-context.md#fetch-the-team-roster)し、各ユーザーに[ダイレクト メッセージ](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)を送信することができます。

次の状況では、ボットからウェルカム メッセージを送信 *しない* ことをお勧めします。

* チームが大規模である (主観的に、たとえば 100 人以上のメンバーなど)。 ウェルカム メッセージを見るすべてのユーザーにボットの価値提案を明確に伝えないなら、ボットは "スパム" と見なされ、追加したユーザーに苦情が寄せられる可能性があります。
* ボットは、チームにまず追加されるのではなく、グループまたはチャネルでまずメンションされる。
* グループまたはチャネルの名前が変更される。
* チーム メンバーがグループまたはチャネルに追加される。

## <a name="-mentions"></a>@メンション

グループまたはチャネル内のボットは、メッセージ内で言及されたときにのみ ("@*botname*") 応答するため、グループ チャネル内のボットによって受信されたすべてのメッセージには独自の名前が含まれており、メッセージの解析によって処理されることを確認する必要があります。 さらにボットは、メンションされた他のユーザーを解析したり、メッセージの一部としてユーザーをメンションしたりすることができます。

### <a name="retrieving-mentions"></a>メンションの取得

メンションは、ペイロードの `entities` オブジェクトで返され、ユーザーの一意の ID と、ほとんどの場合、メンションされたユーザーの名前を含みます。 メッセージ内のすべてのメンションを取得するには、.NET の場合、Bot Builder SDK で `GetMentions` 関数を呼び出します。これにより、`Mentioned` オブジェクトの配列が返されます。

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>.NET のコード例: @ボット メンションの確認と取り出し

```csharp
Mention[] m = sourceMessage.GetMentions();
var messageText = sourceMessage.Text;

for (int i = 0;i < m.Length;i++)
{
    if (m[i].Mentioned.Id == sourceMessage.Recipient.Id)
    {
        //Bot is in the @mention list.
        //The below example will strip the bot name out of the message, so you can parse it as if it wasn't included. Note that the Text object will contain the full bot name, if applicable.
        if (m[i].Text != null)
            messageText = messageText.Replace(m[i].Text, "");
    }
}
```

> [!NOTE]
> ボットを含むすべてのメンションを取り出す、Teams 拡張関数 `GetTextWithoutMentions` を使用することもできます。

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js のコード例: @ボット メンションの確認と取り出し

```javascript
var text = message.text;
if (message.entities) {
    message.entities
        .filter(entity => ((entity.type === "mention") && (entity.mentioned.id.toLowerCase() === botId)))
        .forEach(entity => {
            text = text.replace(entity.text, "");
        });
    text = text.trim();
}
```

ボットを含むすべてのメンションを取り出す、Teams 拡張関数 `getTextWithoutMentions` を使用することもできます。

### <a name="constructing-mentions"></a>メンションの作成

ボットは、チャネルに投稿されるメッセージで他のユーザーをメンションできます。 これを行うには、メッセージで次を行う必要があります。

* メッセージ テキストに `<at>@username</at>` を含めます。
* エンティティ コレクション内に `mention` オブジェクトを含めます。

#### <a name="net-example"></a>.NET の例

この例では、[Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Node.js の例

```javascript
// User to mention
var toMention: builder.IIdentity = {
    name: 'John Doe',
    id: userId
};

// Create a message and add mention to it
var msg = new teams.TeamsMessage(session).text(teams.TeamsMessage.getTenantId(session.message));
var mentionedMsg = msg.addMentionToText(toMention);

// Post the message
var generalMessage = mentionedMsg.routeReplyToGeneralChannel();
session.send(generalMessage);
```

#### <a name="example-outgoing-message-with-user-mentioned"></a>例: ユーザーがメンションされた送信メッセージ

```json
{
    "type": "message", 
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "28:9e52142b-5e5e-4d7b-bb3e- e82dcf620000",
        "name": "SchemaTestBot"
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

## <a name="accessing-groupchat-or-channel-scope"></a>groupChat または channel スコープへのアクセス

ボットは、グループおよびチームでのメッセージの送受信以上の操作を行うことができます。 たとえば、チャネルの一覧や、プロフィール情報を含むメンバーの一覧をフェッチすることもできます。 詳細については、「[Microsoft Teams ボットのためにコンテキストを取得する](~/resources/bot-v3/bots-context.md)」を参照してください。

## <a name="see-also"></a>関連項目

[Bot Framework Samples (Bot Framework のサンプル)](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
