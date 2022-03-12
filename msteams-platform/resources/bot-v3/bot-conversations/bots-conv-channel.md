---
title: ボットとのチャネルチャットとグループ チャットの会話
description: チャネル内のボットと会話を行うエンドツーエンドのシナリオについて説明Microsoft Teams
keywords: チームのシナリオ チャネルの会話ボット
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: 1b9d25b7ce6bc30c980634510b5fca7c60f155ef
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453811"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Microsoft Teams ボットとのチャネルおよびグループ チャット会話

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teamsは、ユーザーが自分のチャネルまたはグループ チャットの会話にボットを取り込むのを許可します。 チームまたはチャットにボットを追加すると、会話のすべてのユーザーが会話でボット機能を利用できます。 また、チーム情報のTeamsユーザーのクエリなど、ボット内の特定の機能@mentioningできます。

チャネルやグループ チャットでのチャットは、ユーザーがボットにアクセスする必要があるという点@mention異なります。 ボットが個人、グループチャット、チャネルなどの複数のスコープで使用されている場合は、ボット メッセージが送信されたスコープを検出し、必要に応じて処理する必要があります。

## <a name="designing-a-great-bot-for-channels-or-groups"></a>チャネルまたはグループに最適なボットを設計する

チームに追加されたボットは別のチーム メンバーになり、会話の@mentionedとして使用できます。 実際、ボットはメッセージを受信する@mentioned、チャネル上の他の会話はボットに送信されません。

グループまたはチャネルのボットは、すべてのメンバーに関連する適切な情報を提供する必要があります。 ボットはエクスペリエンスに関連する情報を確実に提供することができますが、ボットとの会話は誰にでも表示されます。 したがって、グループまたはチャネルの優良なボットは、すべてのユーザーに価値を追加し、1 対 1 の会話に適した情報を誤って共有する必要があります。

ボットは、同様に、追加の作業を必要とせずに、すべてのスコープで完全に関連している可能性があります。 このMicrosoft Teams、すべてのスコープでボットが機能するとは思いもよらありませんが、ボットがサポートするスコープでユーザー値を提供する必要があります。 スコープの詳細については、「アプリ」を参照[Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)。

グループまたはチャネルで動作するボットの開発では、個人の会話と同じ機能の多くを使用します。 ペイロード内の追加のイベントとデータは、グループTeamsチャネル情報を提供します。 これらの違い、および一般的な機能の主な違いについては、次のセクションで説明します。

### <a name="creating-messages"></a>メッセージの作成

チャネルでメッセージを作成するボットの詳細については、「 [Proactive Messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」および「特にチャネル会話を作成 [する」を参照してください](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)。

### <a name="receiving-messages"></a>メッセージの受信

グループまたはチャネル内のボットの場合、通常のメッセージ スキーマ[](https://docs.botframework.com/core-concepts/reference/#activity)に加えて、ボットは次のプロパティも受け取ります。

* `channelData`「チャネル [Teams」を参照してください](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)。 グループ チャットには、そのチャットに固有の情報が含まれる。
* `conversation.id` チャネル ID と返信チェーン内の最初のメッセージの ID で構成される応答チェーン ID。
* `conversation.isGroup` チャネル `true` またはグループ チャットのボット メッセージ用です。
* `conversation.conversationType` どちらか `groupChat` または `channel`.
* `entities` 1 つ以上のメンションを含めできます。 詳細については、「メンション」 [を参照してください](#-mentions)。

### <a name="replying-to-messages"></a>メッセージへの返信

既存のメッセージに返信するには、 [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .NET [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) を呼び出すか、Node.js。 ボット ビルダー SDK は、すべての詳細を処理します。

REST API を使用する場合は、エンドポイントを呼び出することもできます [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) 。

チャネルでは、メッセージに返信すると、開始する返信チェーンへの返信として表示されます。 チャネル `conversation.id` とトップ レベルのメッセージ ID が含まれる。 ボット フレームワークは詳細を処理しますが `conversation.id` 、必要に応じて、その会話スレッドに対する今後の返信のためにキャッシュできます。

### <a name="best-practice-welcome-messages-in-teams"></a>ベスト プラクティス: ウェルカム メッセージ (Teams

ボットが最初にグループまたはチームに追加される場合は、通常、ボットを紹介するウェルカム メッセージをすべてのユーザーに送信すると便利です。 ウェルカム メッセージには、ボットの機能とユーザーの利点の説明が記載されている必要があります。 理想的には、メッセージには、ユーザーがアプリを操作するためのコマンドも含める必要があります。 これを行うには、ボットがメッセージ`conversationUpdate``teamsAddMembers`に応答し、オブジェクトに eventType が含まれることを確認`channelData`します。 ユーザーがチームに `memberAdded` 追加された場合に同じイベントが送信されるので、ID がボットのアプリ ID 自体である必要があります。 詳細については [、「チーム メンバーまたはボットの追加」](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) を参照してください。

ボットを追加するときに、チームの各メンバーに個人用メッセージを送信する場合があります。 これを行うには、チーム名 [簿を](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) 取得し、各ユーザーに直接メッセージを [送信します](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

次の状況では *、ボットが* ウェルカム メッセージを送信しなかすることをお勧めします。

* チームは大きい (明らかに主観的です。たとえば、100 人を超えるメンバー)。 ボットは "spammy" と見なされ、追加したユーザーは、ウェルカム メッセージを見たすべてのユーザーにボットの価値提案を明確に伝えない限り、苦情を受け取る可能性があります。
* ボットは最初にグループまたはチャネルで言及され、最初にチームに追加されます。
* グループまたはチャネルの名前が変更されます。
* チーム メンバーがグループまたはチャネルに追加されます。

## <a name="-mentions"></a>@ メンション

グループまたはチャネル内のボットは、メッセージに ("@*botname*") と記載されている場合にのみ応答しますので、グループ チャネル内のボットによって受信されるメッセージには、その名前が含まれているため、メッセージ解析で処理を行う必要があります。 さらに、ボットは、メッセージの一部として言及された他のユーザーを解析し、ユーザーに言及することもできます。

### <a name="retrieving-mentions"></a>メンションの取得

メンションはペイロード内の `entities` オブジェクトで返され、ユーザーの一意の ID と、ほとんどの場合、言及されたユーザーの名前の両方が含まれます。 メッセージ内のすべてのメンションを `GetMentions` 取得するには、オブジェクトの配列を返す .NET 用ボット ビルダー SDK で関数を呼び出 `Mentioned` します。

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>.NET サンプル コード: メンションの確認と@botする

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
> ボットを含むすべてのTeams`GetTextWithoutMentions`を取り除く拡張機能を使用することもできます。

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.jsコードの例: メンションの確認と@botする

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

ボットを含むすべてのTeams`getTextWithoutMentions`を取り除く拡張機能を使用することもできます。

### <a name="constructing-mentions"></a>メンションの作成

ボットは、チャネルに投稿されたメッセージで他のユーザーに言及できます。 これを行うには、メッセージで次の操作を行う必要があります。

* メッセージ `<at>@username</at>` テキストに含める。
* エンティティ コレクション内 `mention` にオブジェクトを含める。

#### <a name="net-example"></a>.NET の例

この例では[、Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)します。

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Node.js例

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>例: ユーザーが言及した送信メッセージ

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

## <a name="accessing-groupchat-or-channel-scope"></a>groupChat またはチャネル スコープへのアクセス

ボットは、グループやチームでメッセージを送受信する以上の操作を実行できます。 たとえば、メンバーのリスト (プロファイル情報を含む) とチャネルのリストをフェッチすることもできます。 詳細については、「Get [context for your Microsoft Teamsボット」を参照してください](~/resources/bot-v3/bots-context.md)。

## <a name="see-also"></a>関連項目

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
