---
title: ボットを使用したチャネルとグループチャットの会話
description: Microsoft Teams のチャネルで bot との会話を行うエンドツーエンドのシナリオについて説明します。
keywords: teams シナリオチャネル会話 bot
ms.date: 06/25/2019
ms.openlocfilehash: 168abd1e3894b95983eec01541d470f1b5384a66
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674677"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Microsoft Teams bot によるチャネルおよびグループチャットの会話

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams を使用すると、ユーザーは自分のチャネルまたはグループのチャット会話に bot を提供できます。 チームまたはチャットに bot を追加することで、会話のすべてのユーザーは、会話の bot 機能を利用できるようになります。 チーム情報のクエリやユーザーの @mentioning など、ボット内の Teams 固有の機能にアクセスすることもできます。

チャネルおよびグループチャットでのチャットは、ユーザーが bot @mention する必要があるという点で、個人チャットとは異なります。 Bot が複数の範囲 (personal、groupchat または channel) で使用されている場合は、ボットメッセージの送信元のスコープを検出し、それに応じて処理する必要があります。

## <a name="designing-a-great-bot-for-channels-or-groups"></a>チャネルまたはグループ向けに優位な bot を設計する

チームに追加された bot は、他のチームメンバーとなり、会話の一部として @mentioned できます。 実際には、ボットは @mentioned ときにのみメッセージを受信するので、チャネルの他の会話は bot に送信されません。

> [!NOTE]
> チャネル内の bot メッセージに返信する際に便宜上、[新規作成] メッセージボックスに bot 名が自動的に付加されます。

グループまたはチャネル内の bot は、すべてのメンバーに関連する情報を提供する必要があります。 ボットは確かに、その環境に関連する情報をすべて提供できるようになりますが、すべてのユーザーが見ることができるように注意してください。 そのため、グループまたはチャネル内の大 bot は、すべてのユーザーに値を追加する必要があります。これにより、1対1の会話でより適切に情報を共有することは間違いありません。

Bot は、すべてのスコープにあるものと完全に関連している可能性があります。また、bot がそれらを越えて機能できるようにするための重要な特別な作業は必要ありません。 Microsoft Teams では、bot がすべてのスコープで機能することを想定していませんが、bot がサポートする範囲でユーザー値を提供できるようにする必要があります。 範囲の詳細については、「 [Microsoft Teams のアプリ](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。

グループまたはチャネルで機能する bot を開発すると、個人の会話と同じ機能が多く使用されます。 ペイロードの追加のイベントとデータは、Teams グループとチャネル情報を提供します。 次のセクションでは、これらの相違点と、共通機能の主な違いについて説明します。

### <a name="creating-messages"></a>メッセージを作成する

ボットの詳細については、「 [bot の](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)メッセージを作成する」および「特に[チャネル会話を作成](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)する」を参照してください。

### <a name="receiving-messages"></a>メッセージの受信

[通常のメッセージスキーマ](https://docs.botframework.com/core-concepts/reference/#activity)に加えて、グループまたはチャネル内の bot の場合、bot は次のプロパティも受け取ります。

* `channelData`「 [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)」を参照してください。 グループチャットには、そのチャットに固有の情報が含まれています。
* `conversation.id`応答チェーン ID。チャネル ID と、返信チェーン内の最初のメッセージの ID で構成されます。
* `conversation.isGroup`チャネル`true`またはグループチャットのボットメッセージ用
* `conversation.conversationType``groupChat`あるいは`channel`
* `entities`1つ以上のメンションを含めることができます ([メンション](#-mentions)を参照してください)

### <a name="replying-to-messages"></a>メッセージへの返信

既存のメッセージに返信するには[`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) 、.net また[`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler)は node.js で呼び出します。 Bot ビルダー SDK は、すべての詳細を処理します。

REST API の使用を選択する場合は、 [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply)エンドポイントを呼び出すこともできます。

チャネルでは、メッセージへの返信として、開始側の返信チェインへの返信として表示されます。 に`conversation.id`は、チャネルとトップレベルのメッセージ ID が含まれています。 Bot フレームワークは詳細を考慮していますが、必要に`conversation.id`応じて、その会話スレッドへの今後の返信のためにキャッシュすることができます。

### <a name="best-practice-welcome-messages-in-teams"></a>ベストプラクティス: Teams でのウェルカムメッセージ

Bot が初めてグループまたはチームに追加されると、すべてのユーザーに bot を紹介するウェルカムメッセージを送信すると便利です。 ウェルカムメッセージには、bot の機能とユーザーの利点についての説明が記載されています。 メッセージには、ユーザーがアプリを操作するためのコマンドも含めることが理想的です。 これを行うには、bot が`conversationUpdate`メッセージに応答して、 `teamsAddMembers` `channelData`オブジェクトに eventType があることを確認します。 ユーザーがチームに`memberAdded`追加されたときに同じイベントが送信されるので、ID が Bot のアプリ id 自体であることを確認してください。 詳細について[は、「Team member or bot の追加](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)」を参照してください。

Bot が追加されたときに、チームの各メンバーに個人メッセージを送信することもできます。 これを行うには、[チーム名簿を取得](~/resources/bot-v3/bots-context.md#fetching-the-team-roster)して、各ユーザーを[直接メッセージ](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)として送信することができます。

次の状況では、お客様がウェルカムメッセージを送信し*ない*ことをお勧めします。

* チームは大規模です (ただし、100メンバーよりも大きいなど)。 Bot が "spammy" と表示されている可能性があります。これを追加したユーザーは、ウェルカムメッセージが表示されるすべてのユーザーに bot の価値提案を明確に伝えない限り、苦情を受けることがあります。
* Bot は、最初にグループまたはチャネルで言及されます (チームに最初に追加されるものではありません)。
* グループまたはチャネルの名前が変更された
* チームメンバーがグループまたはチャネルに追加される

## <a name="-mentions"></a>@ メンション

グループまたはチャネル内のボットは、メッセージ内の bot ("@_botname_") に記述されている場合にのみ応答するため、グループチャネル内の bot が受信するすべてのメッセージには独自の名前が含まれており、メッセージ解析がそれを処理する必要があります。 また、bot は、前述の他のユーザーを分析し、ユーザーにメッセージの一部として言及することができます。

### <a name="retrieving-mentions"></a>メンションの取得

メンションは、 `entities`ペイロードのオブジェクトに返され、ユーザーの一意の ID と、通常はユーザーの名前の両方が含まれます。 メッセージ内のすべてのメンションを取得するに`GetMentions`は、BOT ビルダー SDK の関数を呼び出します。これは、 `Mentioned`オブジェクトの配列を返します。

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>.NET のコード例: @bot 言及していることを確認して削除する

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
> Teams 拡張機能`GetTextWithoutMentions`を使用して、bot を含むすべてのメンションをストリップすることもできます。

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js のコード例: @bot 言及してください。

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

Teams 拡張機能`getTextWithoutMentions`を使用して、bot を含むすべてのメンションをストリップすることもできます。

### <a name="constructing-mentions"></a>メンションの構築

Bot は、チャネルに投稿されたメッセージに他のユーザーを伝えます。 これを行うには、メッセージで次の操作を実行する必要があります。

* メッセージ`<at>@username</at>`テキストに含める
* オブジェクトを`mention` entities コレクション内に含める

#### <a name="net-example"></a>.NET の例

この例では、 [Microsoft の Bot](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。

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

このサンプルでは、 [botbuilder](https://www.npmjs.com/package/botbuilder-teams)の npm パッケージを使用します。

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>例: ユーザーが説明した送信メッセージ

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

## <a name="accessing-groupchat-or-channel-scope"></a>GroupChat またはチャネルスコープへのアクセス

Bot は、グループと teams でメッセージを送受信することができます。 たとえば、プロファイル情報やチャネルの一覧を含む、メンバーの一覧を取得することもできます。 詳細については[、「Microsoft Teams の bot のコンテキストを取得](~/resources/bot-v3/bots-context.md)する」を参照してください。
