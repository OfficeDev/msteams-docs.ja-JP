---
title: ボットとのチャネルチャットとグループ チャットの会話
description: Microsoft Teams のチャネルでボットと会話するエンドツーエンドのシナリオについて説明します。
keywords: チーム のシナリオ チャネル会話ボット
ms.date: 06/25/2019
ms.openlocfilehash: e556eb006257a83ddf93adb62f79857201d6a9ad
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231632"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Microsoft Teams ボットとのチャネルおよびグループ チャット会話

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams を使用すると、ユーザーはチャネルやグループ チャットの会話にボットを取り込むこが可能です。 ボットをチームまたはチャットに追加することで、会話のすべてのユーザーが会話内のボット機能を利用できます。 チーム情報のクエリやユーザーへのアクセスなど、ボット内の Teams 固有の@mentioningすることもできます。

チャネルとグループ チャットでのチャットは、ユーザーがボットにアクセスする必要があるという点@mention異なります。 ボットが複数のスコープ (個人用、グループチャット、またはチャネル) で使用されている場合は、ボット メッセージの受信範囲を検出し、必要に応じてそれらを処理する必要があります。

## <a name="designing-a-great-bot-for-channels-or-groups"></a>チャネルまたはグループ用の最適なボットの設計

チームに追加されたボットは別のチーム メンバーになり@mentioned会話の一部として使用できます。 実際、ボットは自分がメッセージを受信@mentioned、チャネル上の他の会話はボットに送信されません。

グループまたはチャネル内のボットは、すべてのメンバーに関連する適切な情報を提供する必要があります。 ボットはエクスペリエンスに関連する情報を確実に提供することができますが、ボットとの会話はだれでも見えるので、ご安心ください。 したがって、グループまたはチャネルの優良ボットは、すべてのユーザーに価値を加え、1 対 1 の会話に適した情報を誤って共有し続けてしまう必要があります。

ボットは、その場合と同様に、追加の作業を必要とせずに、すべてのスコープで完全に関連している可能性があります。 Microsoft Teams では、ボットがすべてのスコープで機能する可能性はありません。ただし、ボットがサポートするスコープでユーザー値を提供する必要があります。 スコープの詳細については、「Microsoft Teams のアプリ [」を参照してください](~/concepts/build-and-test/app-studio-overview.md)。

グループまたはチャネルで動作するボットの開発では、個人の会話と同じ機能の多くを使用します。 ペイロード内の追加のイベントとデータは、Teams グループとチャネル情報を提供します。 これらの違い、および一般的な機能の主な違いについては、次のセクションで説明します。

### <a name="creating-messages"></a>メッセージの作成

チャネルでメッセージを作成するボットについて詳しくは、「ボットの [プロ](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)アクティブ メッセージング」、特にチャネル会話 [の作成に関するページをご覧ください](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)。

### <a name="receiving-messages"></a>メッセージの受信

通常のメッセージ スキーマに加えて、グループまたはチャネル内[](https://docs.botframework.com/core-concepts/reference/#activity)のボットの場合、ボットは次のプロパティも受け取ります。

* `channelData` Teams の [チャネル データを参照してください](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)。 グループ チャットには、そのチャットに固有の情報が含まれている。
* `conversation.id` 応答チェーン ID。チャネル ID と、返信チェーン内の最初のメッセージの ID で構成されます。
* `conversation.isGroup` チャネル `true` またはグループ チャット内のボット メッセージ用
* `conversation.conversationType` どちらか `groupChat` または `channel`
* `entities` 1 つ以上のメンションを含む (「 [メンション」を参照](#-mentions))

### <a name="replying-to-messages"></a>メッセージに返信する

既存のメッセージに返信するには、.NET または既存のメッセージを呼び [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) 出Node.js。 Bot Builder SDK は、すべての詳細を処理します。

REST API を使用する場合は、エンドポイントを呼び出 [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) す方法も可能です。

チャネルでは、メッセージに返信すると、開始する返信チェーンへの返信として表示されます。 チャネル `conversation.id` とトップ レベルのメッセージ ID が含まれている。 Bot Framework は詳細を処理しますが、必要に応じて、その会話スレッドに対する将来の返信用 `conversation.id` にキャッシュできます。

### <a name="best-practice-welcome-messages-in-teams"></a>ベスト プラクティス: Teams でのウェルカム メッセージ

ボットが最初にグループまたはチームに追加される場合、通常、ボットを紹介するウェルカム メッセージをすべてのユーザーに送信すると便利です。 ウェルカム メッセージには、ボットの機能とユーザーの利点の説明が記載されている必要があります。 メッセージには、ユーザーがアプリを操作するためのコマンドも含めるのが理想的です。 これを行うには、オブジェクトに eventType を含むメッセージにボット `conversationUpdate` `teamsAddMembers` が応答します `channelData` 。 ユーザーがチームに追加された場合も同じイベントが送信されるので、ID がボットのアプリ ID 自体 `memberAdded` である必要があります。 詳細 [については、チーム メンバーまたはボットの追加](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) を参照してください。

ボットを追加するときに、チームの各メンバーに個人用メッセージを送信する必要がある場合があります。 これを行うには、チーム名 [簿を取得](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) し、各ユーザーに直接メッセージを [送信します](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

次の状況では *、ボットが* ウェルカム メッセージを送信しなにすることをお勧めします。

* チームは大規模です (明らかに主観的ですが、たとえば 100 人を超えるメンバー)。 ボットは "spammy" と見なされ、ボットを追加したユーザーは、ウェルカム メッセージを見たすべてのユーザーにボットの価値提案を明確に伝えられない限り、苦情を受け取る可能性があります。
* ボットは最初にグループまたはチャネルで言及されます (最初にチームに追加されるのとは比較して)
* グループまたはチャネルの名前が変更される
* チーム メンバーがグループまたはチャネルに追加される

## <a name="-mentions"></a>@ メンション

グループまたはチャネル内のボットは、メッセージに記載されている場合 ("@_botname_") にのみ応答します。グループ チャネル内のボットが受信するメッセージには、その名前が含まれているため、メッセージ解析で処理を行う必要があります。 さらに、ボットは、メッセージの一部としてメンションおよびメンションされた他のユーザーを解析できます。

### <a name="retrieving-mentions"></a>メンションの取得

メンションはペイロード内のオブジェクトで返され、ユーザーの一意の ID と、ほとんどの場合、メンションされたユーザーの名前の両方 `entities` が含まれます。 オブジェクトの配列を返す Bot Builder SDK for .NET の関数を呼び出すことによって、メッセージ内のすべてのメンション `GetMentions` を取得 `Mentioned` できます。

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>.NET のコード例: メンションをチェックして@botします

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
> Teams 拡張機能を使用して、ボットを含むすべてのメンション `GetTextWithoutMentions` を削除することもできます。

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.jsコード例: メンションの確認と@bot取り除く

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

Teams 拡張機能を使用して、ボットを含むすべてのメンション `getTextWithoutMentions` を削除することもできます。

### <a name="constructing-mentions"></a>メンションの作成

ボットは、チャネルに投稿されたメッセージで他のユーザーをメンションできます。 これを行うには、メッセージで次の操作を行う必要があります。

* メッセージ `<at>@username</at>` テキストに含める
* エンティティ コレクション `mention` 内にオブジェクトを含める

#### <a name="net-example"></a>.NET の例

この例では [、Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>例: ユーザーが記載された送信メッセージ

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

ボットは、グループやチームでメッセージを送受信する以上の操作を実行できます。 たとえば、メンバーのリスト (プロファイル情報を含む) とチャネルのリストをフェッチすることもできます。 詳細 [については、「Microsoft Teams ボットのコンテキストを取得する](~/resources/bot-v3/bots-context.md) 」を参照してください。

*Bot* Framework の [サンプルも参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
