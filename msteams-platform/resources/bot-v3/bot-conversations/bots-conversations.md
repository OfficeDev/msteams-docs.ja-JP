---
title: ボットを使用してメッセージを送受信する
description: Microsoft Teams でボットを使用してメッセージを送受信する方法について説明します。
ms.topic: overview
localization_priority: Normal
keywords: teams ボット メッセージ
ms.date: 05/20/2019
ms.openlocfilehash: 67dae46d0d34ff842d3fe6717f51e00ad4b8c80a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020668"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Microsoft Teams ボットと会話する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。 Teams には、次の 3 種類の会話 (スコープとも呼ばれる) があります。

* `teams` チャネル会話とも呼ばれる、チャネルのすべてのメンバーに表示されます。
* `personal` ボットと 1 人のユーザーの会話。
* `groupChat` ボットと 2 人以上のユーザーとのチャット。

ボットの動作は、関係する会話の種類に応じて少し異なります。

* [チャネルチャットとグループ チャット会話](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) のボットでは、チャネルでボットを呼び出す場合は、ユーザーがボットに @メンションする必要があります。
* [単一ユーザーの会話のボット](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) では@メンションは必要としません。ユーザーは入力できます。

ボットが特定のスコープで動作するには、マニフェスト内のそのスコープをサポートするとして一覧表示する必要があります。 スコープはマニフェストリファレンスで定義され、さらに [説明されています](~/resources/schema/manifest-schema.md)。

## <a name="proactive-messages"></a>プロアクティブ メッセージ

ボットは、会話に参加するか、会話を開始できます。 ほとんどの通信は、別のメッセージに応答します。 ボットが会話を開始した場合は、プロアクティブ メッセージと *呼ばれる。* たとえば、次のような情報が含まれます。

* ウェルカム メッセージ
* イベント通知
* ポーリング メッセージ

## <a name="conversation-basics"></a>会話の基本

各メッセージは `messageType: message` 型の `Activity` オブジェクトです。 ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。 ボットはメッセージを調べて、その種類を特定し、それに応じて応答します。

ボットは、イベント スタイルのメッセージもサポートします。 詳細については [、「Microsoft Teams でのボット イベントの処理](~/resources/bot-v3/bots-notifications.md) 」を参照してください。 音声は現在サポートされていません。

メッセージはほとんどの場合、すべてのスコープで同じですが、ボットが UI でアクセスされる方法と、知る必要があるシーンの背後での違いがあります。

基本的な会話は、ボットが Teams や他のチャネルと通信するための単一の REST API である Bot Framework Connector を介して処理されます。 ボット ビルダー SDK は、この API への簡単なアクセス、会話のフローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法を提供します。

## <a name="message-content"></a>メッセージの内容

ボットはリッチ テキスト、画像、カードを送信できます。 ユーザーは、リッチ テキストと画像をボットに送信できます。 ボットで処理できるコンテンツの種類は、ボットの [Microsoft Teams の設定] ページで指定できます。

| フォーマット | ユーザーからボットへ  | ボットからユーザーへ |  メモ |
| --- | :---: | :---: | --- |
| リッチ テキスト | ✔ | ✔ |  |
| ピクチャ | ✔ | ✔ | 最大 1024× 1024 および 1 MB (PNG、JPEG、または GIF 形式)。アニメーション GIF はサポートされていません |
| カード | ✖ | ✔ | サポートされている [カードについては、「Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md) 」を参照してください。 |
| 絵文字 | ✖ | ✔ | Teams は現在、UTF-16 を介して絵文字をサポートしています (顔を笑う場合は U+1F600 など) |
|

ボット フレームワークでサポートされるボット操作の種類 (チーム内のボットが基づく) の詳細については、ボット ビルダー SDK [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) [for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true)およびボット ビルダー SDK for Node.jsのドキュメントの会話フローと関連する概念に関するボット フレームワーク[のドキュメントを参照](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)してください。

## <a name="message-formatting"></a>メッセージの書式設定

a の省略可能なプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) `message` を制御できます。 ボット [メッセージでサポートされている](~/resources/bot-v3/bots-message-format.md) 書式設定の詳細については、「メッセージの書式設定」を参照してください。
省略可能なプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) を制御できます。

Teams がチームでテキストの書式設定をサポートする方法の詳細については、「ボット メッセージの [テキストの書式設定」を参照してください](~/resources/bot-v3/bots-text-formats.md)。

メッセージ内のカードの書式設定の詳細については、「カードの書式設定」 [を参照してください](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="picture-messages"></a>ピクチャ メッセージ

画像は、メッセージに添付ファイルを追加して送信されます。 添付ファイルの詳細については、Bot Framework のドキュメント [を参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)。

画像は、PNG、JPEG、または GIF 形式× 1024、1024、1 MB 以下の値を使用できます。アニメーション GIF はサポートされていません。

XML を使用して、各イメージの高さと幅を指定することをお勧めします。 Markdown を使用する場合、画像サイズの既定値は 256 ×256 です。 例:

* `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` を使う
* 使用しない `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages&quot;></a>メッセージの受信

宣言されているスコープに応じて、ボットは次のコンテキストでメッセージを受信できます。

* **個人用チャット** ユーザーは、チャット履歴で追加されたボットを選択するか、新しいチャットの [To:] ボックスに名前またはアプリ ID を入力するだけで、ボットとのプライベート会話で対話できます。
* **チャネル** ボットがチームに追加されている場合は、チャネルにボット (&quot;@_botname_") を指定できます。 チャネル内のボットに対する追加の返信には、ボットのメンションが必要です。 これは、記載されていない返信には応答しない。

受信メッセージの場合、ボットは型の [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) オブジェクトを受け取ります `messageType: message` 。 オブジェクトには、ボットに送信されるチャネル更新など、他の種類の情報を含めすることもできますが、この型はボットとユーザーの間 `Activity` [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` の通信を表します。

ボットは、ユーザー メッセージ、ユーザー、メッセージのソース、Teams 情報に関するその他の情報を含むペイロード `Text` を受け取ります。 注:

* `timestamp` 協定世界時 (UTC) のメッセージの日付と時刻
* `localTimestamp` 送信者のタイム ゾーン内のメッセージの日付と時刻
* `channelId` 常に "msteams" 。 これは、チーム チャネルではなく、ボット フレームワーク チャネルを指します。
* `from.id` ボットのユーザーの一意で暗号化された ID。アプリがユーザー データを保存する必要がある場合は、キーとして適しています。 ボットにとって一意であり、そのユーザーを識別する意味のある方法でボット インスタンスの外部で直接使用することはできません。
* `channelData.tenant.id` ユーザーのテナント ID。

> [!NOTE]
> `from.id` はボットにとって一意であり、そのユーザーを識別する意味のある方法でボット インスタンスの外部で直接使用することはできません。

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>チャネルとプライベート操作をボットと組み合わせる

チャネルで操作する場合、ボットはユーザーとの特定の会話をオフラインにした方が良い必要があります。 たとえば、ユーザーがチーム メンバーのセットとのスケジュール設定など、複雑なタスクを調整しようとしているとします。 一連の操作全体をチャネルに表示するのではなく、ユーザーに個人的なチャット メッセージを送信する方法を検討してください。 ボットは、状態を失わずに、個人とチャネルの会話の間でユーザーを簡単に移行できる必要があります。

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
> 受信メッセージのテキスト フィールドにメンションが含まれる場合があります。 適切にチェックして、それらのファイルを取り除く必要があります。 詳細については、「メンション」 [を参照してください](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)。

## <a name="teams-channel-data"></a>Teams チャネル データ

オブジェクト `channelData` には Teams 固有の情報が含まれているので、チームとチャネルの ID の決定的なソースです。 これらの ID をキャッシュし、ローカル ストレージのキーとして使用する必要があります。

オブジェクトは、チャネルの外部で行なうので、個人の会話 `channelData` のメッセージには含まれません。

ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれます。

* `eventType` Teams イベントの種類。チャネル変更イベントの場合 [にのみ渡される](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `tenant.id` Azure Active Directory テナント ID。すべてのコンテキストで渡される
* `team` 個人チャットではなく、チャネル コンテキストでのみ渡されます。
  * `id` チャネルの GUID
  * `name` チームの名前。チームの名前変更イベントの場合 [にのみ渡されます](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel` ボットが言及されている場合、またはボットが追加されたチームのチャネル内のイベントに対して、チャネル コンテキストでのみ渡されます。
  * `id` チャネルの GUID
  * `name` チャネル名。チャネル変更イベントの場合 [にのみ渡されます](~/resources/bot-v3/bots-notifications.md#channel-updates)。
* `channelData.teamsTeamId` 非推奨です。 このプロパティは、下位互換性の場合にのみ含まれます。
* `channelData.teamsChannelId` 非推奨です。 このプロパティは、下位互換性の場合にのみ含まれます。

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

[Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージは、Teams 固有の情報にアクセスするプロパティを公開する特殊な `TeamsChannelData` オブジェクトを提供します。

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>メッセージへの返信の送信

既存のメッセージに返信するには [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) 、.NET を呼び出すか、Node.js。 [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) ボット ビルダー SDK は、すべての詳細を処理します。

REST API を使用する場合は、エンドポイントを呼び出 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) することもできます。

メッセージ コンテンツ自体には、単純なテキストや、Bot Framework が提供するカードとカード [アクションの一部を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。

送信スキーマでは、受信したスキーマと常に同じ `serviceUrl` 値を使用する必要があります。 値は安定している傾向がありますが、変更 `serviceUrl` される可能性があります。 新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl` 。

## <a name="updating-messages"></a>メッセージの更新

メッセージをデータの静的スナップショットにするのではなく、ボットはメッセージを送信した後、インラインで動的にメッセージを更新できます。 ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオで、動的メッセージ更新を使用できます。

新しいメッセージは、型の元のメッセージと一致する必要があります。 たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージは単純なテキスト メッセージになります。

> [!NOTE]
> 単一添付メッセージとカルーセル レイアウトで送信されるコンテンツのみを更新できます。 リスト レイアウトで複数の添付ファイルを含むメッセージへの更新の投稿はサポートされていません。

### <a name="rest-api"></a>REST API

メッセージ更新を発行するには、特定のアクティビティ ID を使用してエンドポイントに対して PUT 要求 `/v3/conversations/<conversationId>/activities/<activityId>/` を実行します。 このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>.NET の例

ボット ビルダー SDK の `UpdateActivityAsync` メソッドを使用して、既存のメッセージを更新できます。

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

ボット ビルダー SDK の `session.connector.update` メソッドを使用して、既存のメッセージを更新できます。

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

## <a name="starting-a-conversation-proactive-messaging"></a>会話の開始 (プロアクティブ メッセージング)

ユーザーとの個人的な会話を作成するか、チーム ボットのチャネルで新しい返信チェーンを開始できます。 これにより、ユーザーまたはユーザーに最初にボットとの接触を開始せずにメッセージを送信できます。 詳細については、次のトピックをご覧ください。

ボット [によって開始される会話の詳細については、「](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) ボットのプロアクティブ メッセージング」を参照してください。

## <a name="deleting-messages"></a>メッセージの削除

メッセージは、BotBuilder SDK の connectors メソッドを使用 [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) [して削除できます](/bot-framework/bot-builder-overview-getstarted)。

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
