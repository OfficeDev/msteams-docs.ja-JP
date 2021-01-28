---
title: ボットを使用してメッセージを送受信する
description: Microsoft Teams でボットを使用してメッセージを送受信する方法について説明します。
ms.topic: overview
keywords: チームボット メッセージ
ms.date: 05/20/2019
ms.openlocfilehash: 20c285a0cd06ac929d628edbc059b2a00b937eec
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014118"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Microsoft Teams ボットと会話する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。 Teams には、次の 3 種類の会話 (スコープとも呼ばれる) があります。

* `teams` チャネル会話とも呼ばれる、チャネルのすべてのメンバーに表示されます。
* `personal` ボットと 1 人のユーザーの会話。
* `groupChat` ボットと 2 人以上のユーザーの間でチャットします。

ボットの動作は、関連する会話の種類によって少し異なります。

* [チャネルとグループ チャットの会話の](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) ボットでは、ユーザーがチャネルでボットを呼び出す @ メンションをする必要があります。
* [単一ユーザーの会話のボットには](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) @ メンションは不要です。ユーザーは入力できます。

ボットが特定のスコープで動作するには、そのスコープをサポートするとしてマニフェストに一覧表示される必要があります。 スコープはマニフェスト リファレンスで定義され、詳 [しい説明を参照してください](~/resources/schema/manifest-schema.md)。

## <a name="proactive-messages"></a>プロアクティブ メッセージ

ボットは会話に参加するか、会話を開始できます。 ほとんどの通信は、別のメッセージに対する応答です。 ボットが会話を開始する場合は、プロアクティブ メッセージ *と呼ばれる。* たとえば、次のような情報が含まれます。

* ウェルカム メッセージ
* イベント通知
* メッセージのポーリング

## <a name="conversation-basics"></a>会話の基本

各メッセージは `messageType: message` 型の `Activity` オブジェクトです。 ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。 ボットがメッセージを調べて種類を特定し、それに応じて応答します。

ボットは、イベント スタイルのメッセージもサポートします。 詳細 [については、「Microsoft Teams でのボット イベントの処理](~/resources/bot-v3/bots-notifications.md) 」を参照してください。 現在、音声はサポートされていません。

メッセージの大部分は、すべてのスコープで同じですが、ボットが UI でアクセスされる方法と、知る必要がある背後での違いがあります。

基本的な会話は、ボットが Teams や他のチャネルと通信するための単一の REST API である Bot Framework Connector を通じて処理されます。 Bot Builder SDK は、この API への簡単なアクセス、会話のフローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法を提供します。

## <a name="message-content"></a>メッセージの内容

ボットは、リッチ テキスト、画像、カードを送信できます。 ユーザーは、リッチ テキストと画像をボットに送信できます。 ボットが処理できるコンテンツの種類は、ボットの Microsoft Teams 設定ページで指定できます。

| フォーマット | ユーザーからボットへ  | ボットからユーザーへ |  Notes |
| --- | :---: | :---: | --- |
| リッチ テキスト | ✔ | ✔ |  |
| ピクチャ | ✔ | ✔ | 最大 1024×1024 および 1 MB (PNG、JPEG、または GIF 形式)。アニメーション GIF はサポートされていません |
| カード | ✖ | ✔ | サポートされている [カードについては、Teams カード](~/task-modules-and-cards/cards/cards-reference.md) リファレンスを参照してください。 |
| Emojis | ✖ | ✔ | Teams は現在、UTF-16 を介して絵文字をサポートしています (顔のくびくびくをする U+1F600 など) |
|

Bot Framework でサポートされるボット操作の種類 (チーム内のボットの基に基づく) の詳細については、Bot Builder [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) [SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0)および bot Builder SDK for [Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0)のドキュメントの会話フローと関連概念に関する Bot Framework のドキュメントを参照してください。

## <a name="message-formatting"></a>メッセージの書式設定

a のオプション [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) のプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 `message` を制御できます。 ボット [メッセージでサポート](~/resources/bot-v3/bots-message-format.md) されている書式設定の詳細については、「メッセージの書式設定」を参照してください。
オプションのプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) を制御できます。

Teams がチームでテキストの書式設定をサポートする方法の詳細については、「ボット メッセージのテキスト [の書式設定」を参照してください](~/resources/bot-v3/bots-text-formats.md)。

メッセージ内のカードの書式設定の詳細については、「カードの書式設定」 [を参照してください](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="picture-messages"></a>画像メッセージ

画像は、メッセージに添付ファイルを追加することで送信されます。 添付ファイルの詳細については、Bot Framework のドキュメント [を参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)。

画像は、PNG、JPEG、GIF 形式で最大 1024×1024 および 1 MB です。アニメーション GIF はサポートされていません。

XML を使用して各イメージの高さと幅を指定することをお勧めします。 Markdown を使用する場合、画像サイズの既定値は 256×256 です。 以下に例を示します。

* `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` を使う
* 使用しない `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>メッセージの受信

宣言されているスコープに応じて、ボットは次のコンテキストでメッセージを受信できます。

* **個人用チャット** ユーザーは、チャット履歴で追加されたボットを選択するか、新しいチャットの [To:] ボックスに名前またはアプリ ID を入力するだけで、ボットとのプライベート会話で対話できます。
* **チャネル** ボットがチームに追加されている場合は、チャネルでボットを言及 ("@_botname_") できます。 チャネル内のボットに対する追加の返信には、ボットのメンションが必要です。 記載されていない返信には応答しない。

受信メッセージの場合、ボットは種類の [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) オブジェクトを受信します `messageType: message` 。 オブジェクトには、ボットに送信されるチャネルの更新など、他の種類の情報を含めすることもできますが、この型はボットとユーザーの間の `Activity` [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` 通信を表します。

ボットは、ユーザー メッセージと、ユーザーに関するその他の情報、メッセージのソース、および Teams 情報を含むペイロード `Text` を受信します。 次の点に注意してください。

* `timestamp` 協定世界時 (UTC) でのメッセージの日時
* `localTimestamp` 送信者のタイム ゾーンでのメッセージの日時
* `channelId` 常に "msteams" です。 これは、チーム チャネルではなくボット フレームワーク チャネルを指します。
* `from.id` ボットのそのユーザーの一意で暗号化された ID。アプリでユーザー データを保存する必要がある場合にキーとして適しています。 ボットに固有の機能であり、そのユーザーを識別するための意味のある方法でボット インスタンスの外部で直接使用することはできません。
* `channelData.tenant.id` ユーザーのテナント ID。

> [!NOTE]
> `from.id` はボットに固有であり、そのユーザーを識別するための意味のある方法でボット インスタンスの外部で直接使用することはできません。

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>チャネルとプライベート操作をボットと組み合わせる

チャネルで操作する場合、ボットは、ユーザーとの特定の会話をオフラインにした方が良い必要があります。 たとえば、ユーザーがチーム メンバーのセットとのスケジュール設定などの複雑なタスクを調整しようとしているとします。 一連の操作全体がチャネルに表示されるのではなく、ユーザーに個人用チャット メッセージを送信する方法を検討してください。 ボットは、状態を失わずに、個人会話とチャネル会話の間でユーザーを簡単に移行できる必要があります。

> [!NOTE]
>他のチーム メンバーに通知する操作が完了したら、チャネルを更新することを忘れないでください。

## <a name="full-inbound-schema-example"></a>完全な受信スキーマの例

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

> [!NOTE]
> 受信メッセージのテキスト フィールドにメンションが含まれる場合があります。 それらのチェックと取り除きを正しく行ってください。 詳細については、「メンション [」を参照してください](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)。

## <a name="teams-channel-data"></a>Teams チャネル データ

オブジェクトには Teams 固有の情報が含まれているので、チームとチャネルの ID の確定的 `channelData` なソースです。 これらの ID をキャッシュし、ローカル ストレージのキーとして使用する必要があります。

オブジェクトはチャネルの外部で行うので、個人の会話の `channelData` メッセージには含まれません。

ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれます。

* `eventType` Teams イベントの種類:チャネル変更イベントの場合 [にのみ渡されます。](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `tenant.id` Azure Active Directory テナント ID;すべてのコンテキストで渡される
* `team` チャネル コンテキストでのみ渡されます。個人用チャットでは渡されます。
  * `id` チャネルの GUID
  * `name` チームの名前。チームの名前変更イベントの場合 [にのみ渡されます](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel` ボットが言及されている場合、またはボットが追加されたチームのチャネルのイベントに対して、チャネル コンテキストでのみ渡されます。
  * `id` チャネルの GUID
  * `name` チャネル名チャネル変更イベントの場合 [にのみ渡されます](~/resources/bot-v3/bots-notifications.md#channel-updates)。
* `channelData.teamsTeamId` 非推奨。 このプロパティは、下位互換性のためにのみ含まれています。
* `channelData.teamsChannelId` 非推奨。 このプロパティは、下位互換性のためにのみ含まれています。

### <a name="example-channeldata-object-channelcreated-event"></a>channelData オブジェクトの例 (channelCreated イベント)

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

### <a name="net-example"></a>.NET の例

[Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージは、Teams 固有の情報にアクセスするプロパティを公開する特殊 `TeamsChannelData` なオブジェクトを提供します。

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>メッセージへの返信の送信

既存のメッセージに返信するには、.NET または既存のメッセージを呼び [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) 出Node.js。 Bot Builder SDK は、すべての詳細を処理します。

REST API を使用する場合は、エンドポイントを呼び出 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) す方法も可能です。

メッセージコンテンツ自体には、単純なテキストや Bot Framework で提供されるカードとカード [アクションの一部を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。

送信スキーマでは、受信したスキーマと常に同じ値 `serviceUrl` を使用する必要があります。 値は安定する `serviceUrl` 傾向がありますが、変化する可能性があります。 新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl` 。

## <a name="updating-messages"></a>メッセージの更新

メッセージをデータの静的スナップショットにするのではなく、ボットは送信後にインラインでメッセージを動的に更新できます。 ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオで、動的メッセージの更新を使用できます。

新しいメッセージは、種類が元のメッセージと一致する必要があります。 たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージは単純なテキスト メッセージになります。

> [!NOTE]
> 単一添付メッセージとカルーセル レイアウトで送信されたコンテンツのみを更新できます。 リスト レイアウトで複数の添付ファイルを持つメッセージへの更新の投稿はサポートされていません。

### <a name="rest-api"></a>REST API

メッセージ更新を発行するには、特定のアクティビティ ID を使用してエンドポイントに対して PUT `/v3/conversations/<conversationId>/activities/<activityId>/` 要求を実行します。 このシナリオを完了するには、元の POST 呼び出しによって返されたアクティビティ ID をキャッシュする必要があります。

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>.NET の例

Bot Builder `UpdateActivityAsync` SDK のメソッドを使用して、既存のメッセージを更新できます。

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a>Node.js例

Bot Builder `session.connector.update` SDK のメソッドを使用して、既存のメッセージを更新できます。

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a>会話を開始する (プロアクティブ メッセージング)

ユーザーとの個人的な会話を作成したり、チーム ボットのチャネルで新しい返信チェーンを開始することができます。 これにより、最初にボットとの連絡を開始することなく、ユーザーにメッセージを送信できます。 詳細については、次のトピックをご覧ください。

ボット [によって開始される会話の詳細については、「](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) ボットのプロアクティブ メッセージング」を参照してください。

## <a name="deleting-messages"></a>メッセージの削除

メッセージは BotBuilder SDK のコネクタ [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) メソッドを使用 [して削除できます](/bot-framework/bot-builder-overview-getstarted)。

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```
