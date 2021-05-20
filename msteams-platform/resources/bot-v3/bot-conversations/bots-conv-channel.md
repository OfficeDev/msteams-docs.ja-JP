---
title: ボットとのチャンネルチャットとグループチャットの会話
description: チャネル内のボットと会話するエンド ツー エンドのシナリオを説明Microsoft Teams
keywords: チーム シナリオ チャネル会話ボット
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e254302271cf101638c897e1a1952d302705d6a4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566797"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Microsoft Teams ボットとのチャネルおよびグループ チャット会話

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teamsを使用すると、ユーザーは自分のチャンネルやグループチャットの会話にボットを持ち込むことができるようになります。 チームまたはチャットにボットを追加することで、会話のすべてのユーザーが、会話のボット機能を利用できます。 チーム情報の照会やユーザーの@mentioningなど、ボット内のTeams固有の機能にアクセスすることもできます。

チャンネルチャットやグループチャットは、ユーザーがボットを@mentionする必要があるという点で、個人チャットとは異なります。 ボットが個人、グループチャット、チャネルなどの複数のスコープで使用されている場合は、ボット メッセージがどのスコープから来たかを検出し、それに応じて処理する必要があります。

## <a name="designing-a-great-bot-for-channels-or-groups"></a>チャネルまたはグループ用の優れたボットの設計

チームに追加されたボットは別のチーム メンバーになり、会話の一部として@mentionedできます。 実際、ボットは@mentionedされたときにのみメッセージを受信するため、チャネル上の他の会話はボットに送信されません。

グループまたはチャネル内のボットは、すべてのメンバーに関連し、適切な情報を提供する必要があります。 ボットは、エクスペリエンスに関連する情報を提供できますが、そのボットとの会話は誰でも見ることができます。 したがって、グループやチャネルの優れたボットは、すべてのユーザーに価値を追加し、1 対 1 の会話に適した情報を誤って共有する必要があります。

ボットは、このままでも、追加の作業を必要とせずに、すべてのスコープで完全に関連している可能性があります。 Microsoft Teamsでは、すべてのスコープでボットが機能するとは考えられませんが、サポートするスコープでボットがユーザー値を提供することを確認する必要があります。 スコープの詳細については[、「Microsoft Teamsのアプリ](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。

グループやチャンネルで機能するボットを開発するには、個人的な会話と同じ機能を使用します。 ペイロード内の追加のイベントとデータは、グループ情報とチャネル情報Teams提供します。 これらの相違点と共通機能の主な相違点については、以下のセクションで説明します。

### <a name="creating-messages"></a>メッセージの作成

チャネルでメッセージを作成するボットの詳細については、「 [ボットのプロアクティブなメッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」、特に [チャネル会話の作成 を](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)参照してください。

### <a name="receiving-messages"></a>メッセージの受信

グループまたはチャネルのボットの場合、 [通常のメッセージ スキーマ](https://docs.botframework.com/core-concepts/reference/#activity)に加えて、ボットは次のプロパティも受け取ります。

* `channelData`[チャネル データTeams](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)参照してください。 グループ チャットには、そのチャットに固有の情報が含まれます。
* `conversation.id` チャネル ID と応答チェーン内の最初のメッセージの ID から成る応答チェーン ID。
* `conversation.isGroup``true`チャネルまたはグループ チャットのボット メッセージ用です。
* `conversation.conversationType``groupChat`または のいずれか `channel` 。
* `entities` 1 つまたは複数のメンションを含めることができます。 詳細については、「 [メンション](#-mentions)」を参照してください。

### <a name="replying-to-messages"></a>メッセージへの返信

既存のメッセージに返信するには [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) 、.NET または [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) Node.jsで呼び出します。 ボット ビルダー SDK では、すべての詳細を処理します。

REST API を使用する場合は、エンドポイントを呼び出すこともできます [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) 。

チャネルでは、メッセージに返信すると、その応答チェーンへの応答として表示されます。 `conversation.id`には、チャネルと最上位レベルのメッセージ ID が含まれます。 Bot Framework は詳細を処理しますが、必要に応じてその `conversation.id` 会話スレッドに対する今後の返信にキャッシュできます。

### <a name="best-practice-welcome-messages-in-teams"></a>ベスト プラクティス: Teamsのウェルカム メッセージ

ボットを最初にグループまたはチームに追加した場合、一般的に、ボットを紹介するウェルカム メッセージをすべてのユーザーに送信すると便利です。 ウェルカム メッセージには、ボットの機能とユーザーの利点の説明が記載されている必要があります。 メッセージには、ユーザーがアプリを操作するためのコマンドも含めるのが理想的です。 これを行うには、オブジェクト内の eventType を使用して `conversationUpdate` 、ボットがメッセージに応答することを確認 `teamsAddMembers` `channelData` します。 `memberAdded`ユーザーがチームに追加されたときに同じイベントが送信されるため、ID がボットのアプリ ID であることを確認してください。 詳細については [、チーム メンバーまたはボットの追加](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) を参照してください。

ボットが追加されたときに、チームの各メンバーに個人用メッセージを送信することもできます。 これを行うには、 [チームの名簿を取得](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) し、各ユーザーに [ダイレクトメッセージ](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)を送信します。

次の状況では、ボットからウェルカム メッセージを送信 *しないことを* お勧めします。

* チームは大きい(明らかに、100人以上のメンバー)。 ボットは「スパム」と見なされ、ボットを追加した人は、ウェルカムメッセージを見たすべての人にボットの価値提案を明確に伝えない限り、苦情を受け取る可能性があります。
* ボットは、最初にグループまたはチャネルで言及され、最初にチームに追加されます。
* グループまたはチャネルの名前が変更されます。
* チーム メンバーがグループまたはチャネルに追加されます。

## <a name="-mentions"></a>@言及

グループまたはチャネル内のボットはメッセージに記述されている場合にのみ応答するため _("@botname")、_ グループチャネル内のボットが受信するすべてのメッセージには独自の名前が含まれているため、メッセージの解析はそれを処理する必要があります。 さらに、ボットは、メッセージの一部として、ユーザーに言及されている他のユーザーを解析し、言及することができます。

### <a name="retrieving-mentions"></a>メンションの取得

メンションは `entities` ペイロードのオブジェクトに返され、ユーザーの一意の ID と、ほとんどの場合、言及されたユーザーの名前の両方が含まれています。 オブジェクトの配列を返す `GetMentions` Bot Builder SDK for .NET の関数を呼び出すことで、メッセージ内のすべてのメンションを取得できます `Mentioned` 。

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>.NET のコード例: @bot参照を確認し、削除します。

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
> また、 `GetTextWithoutMentions` ボットを含むすべてのメンションを取り除くTeams拡張機能を使用することもできます。

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js例のコード: @bot参照を確認して削除する

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

また、 `getTextWithoutMentions` ボットを含むすべてのメンションを取り除くTeams拡張機能を使用することもできます。

### <a name="constructing-mentions"></a>メンションの構築

ボットは、チャンネルに投稿されたメッセージで他のユーザーに言及できます。 これを行うには、メッセージで次の操作を行う必要があります。

* `<at>@username</at>`メッセージ テキストに含めます。
* エンティティ `mention` コレクション内にオブジェクトを含めます。

#### <a name="net-example"></a>.NET の例

この例では[、NuGet パッケージを使用Teams。](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

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

## <a name="accessing-groupchat-or-channel-scope"></a>グループチャットまたはチャネルスコープへのアクセス

ボットは、グループやチームでメッセージを送受信する以外の操作も実行できます。 たとえば、プロファイル情報やチャネルのリストを含むメンバーのリストを取得することもできます。 詳細については、「 [Microsoft Teams ボットのコンテキストを取得する](~/resources/bot-v3/bots-context.md)」を参照してください。

## <a name="see-also"></a>関連項目

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
