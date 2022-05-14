---
title: ボットを使用してメッセージを送受信します
description: Microsoft Teams でボットを使用してメッセージを送受信する方法について説明します
ms.topic: overview
ms.localizationpriority: medium
keywords: Teamsボットメッセージ
ms.date: 05/20/2019
ms.openlocfilehash: 0d4665d098e0e14fa3de5f2667c7e970b545b284
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2022
ms.locfileid: "65296974"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Microsoft Teams ボットと会話する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。 Teams には、次の 3 種類の会話 (スコープとも呼ばれる) があります。

* `teams`: チャネル会話とも呼ばれ、チャネルのすべてのメンバーに対して表示されます。
* `personal` ボットと 1 人のユーザーとの会話。
* `groupChat` ボットと 2 人以上のユーザーとの会話。

ボットの動作は、関係する会話の種類に応じて多少異なります:

* [チャネル内やグループ チャット内の会話の場合](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)、ユーザーはボットを @メンションしてチャネルに呼び出す必要があります。
* [単一ユーザー会話のボット](~/resources/bot-v3/bot-conversations/bots-conv-personal.md)には @mention -  は必要ありません。ユーザーは入力するだけで済みます。

ボットを特定のスコープで動作させるには、マニフェストでそのスコープをサポートするものとして一覧表示する必要があります。スコープは、[マニフェスト リファレンス](~/resources/schema/manifest-schema.md)で定義され、さらに詳しく説明されています。

## <a name="proactive-messages"></a>プロアクティブ メッセージ

ボットは会話に参加したり、会話を開始したりできます。 ほとんどの通信は、別のメッセージに応答しています。 ボットが会話を開始する場合は、*プロアクティブ メッセージ* と呼ばれます。 たとえば、次のような情報が含まれます。

* ウェルカム メッセージ
* イベント通知
* 投票メッセージ

## <a name="conversation-basics"></a>会話の基本

各メッセージは `messageType: message` 型の `Activity` オブジェクトです。 ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。 ボットはメッセージを調べて種類を判別し、種類に応じて応答します。

ボットはイベントスタイルのメッセージもサポートしています。 詳細については、「[Microsoft Teamsでのボット イベントの処理](~/resources/bot-v3/bots-notifications.md)」を参照してください。 音声は現在サポートされていません。

メッセージはほとんどの場合、すべてのスコープで同じですが、UI でボットにアクセスする方法と、バックグラウンドの違いについて知っておく必要があります。

基本的な会話は、ボットフレームワークコネクタという単一のREST APIを介して処理され、ボットがTeamsや他のチャネルと通信できるようになります。 Bot Builder SDK では、この API への簡単なアクセス、会話のフローと状態を管理するための追加機能、自然言語処理 (NLP) などのCognitive Servicesを組み込む簡単な方法が提供されます。

## <a name="message-content"></a>メッセージの内容

ボットは、リッチ テキスト、画像、カードを送信できます。 ユーザーは、リッチ テキストと画像をボットに送信できます。 ボットが処理できるコンテンツの種類は、ボットのMicrosoft Teams設定ページで指定できます。

| フォーマット | ユーザーからボットへ  | ボットからユーザーへ |  メモ |
| --- | :---: | :---: | --- |
| リッチ テキスト | ✔ | ✔ |  |
| ピクチャ | ✔ | ✔ | 最大 1024×1024 MB、1 MB の PNG、JPEG、GIF 形式、アニメーション GIF はサポートされていません。 |
| カード | ✖ | ✔ | サポートされているカードについては、[Teams カード リファレンスを参照](~/task-modules-and-cards/cards/cards-reference.md)してください。 |
| 絵文字 | ✖ | ✔ | Teamsは現在、ニヤリとした顔のU+1F600など、UTF-16による絵文字をサポートしています。 |
|

Bot Framework でサポートされているボット操作の種類の詳細については、Bot [Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) および Bot [Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)のドキュメントの[会話フロー](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true)と関連する概念に関する Bot Framework のドキュメントを参照してください。

## <a name="message-formatting"></a>メッセージの書式設定

メッセージのテキスト コンテンツのレンダリング方法を制御するには、a `message` のオプションの[`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true)プロパティを設定できます。 ボット メッセージでサポートされている書式設定の詳細については、[「メッセージの書式設定」](~/resources/bot-v3/bots-message-format.md)を参照してください。
オプション [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) のプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法を制御できます。

Teamsがチームでテキストの書式設定をサポートする方法の詳細については、「 [ボット メッセージのテキスト書式設定](~/resources/bot-v3/bots-text-formats.md)」を参照してください。

メッセージ内のカードの書式設定の詳細については、「 [カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。

## <a name="picture-messages"></a>画像メッセージ

画像は、メッセージに添付ファイルを追加して送信されます。 添付ファイルの詳細については、 [Bot Framework のドキュメント](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)を参照してください。

画像は最大 1024×1024 MB および 1 MB の PNG、JPEG、または GIF 形式にすることができます。アニメーション GIF はサポートされていません。

XML を使用して、各イメージの高さと幅を指定することをお勧めします。 Markdown を使用する場合、イメージ サイズの既定値は 256×256 です。 次に例を示します。

* `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` を使う
* `![Duck on a rock](http://aka.ms/Fo983c)` を使用しないでください

## <a name="receiving-messages"></a>メッセージの受信

どのスコープが宣言されているかに応じて、ボットは次のコンテキストでメッセージを受信できます。

* **個人用チャット** ユーザーは、チャット履歴で追加されたボットを選択するか、新しいチャットの [To: ] ボックスに名前またはアプリ ID を入力することにより、ボットとプライベート会話ができます。
* **チャンネル** ボットがチームに追加されている場合は、チャネルでボット ("@*botname*") を指定できます。 チャネル内のボットに対する追加の返信には、ボットについて言及する必要があることに注意してください。 メンションされていない返信には応答しません。

受信メッセージの場合、ボットは`messageType: message`タイプの[アクティビティ](../../../bots/how-to/conversations/conversation-messages.md)オブジェクトを受け取ります。`Activity` オブジェクトには、ボットに送信される[チャンネル更新](~/resources/bot-v3/bots-notifications.md#channel-updates)など、他の種類の情報を含めることができますが、`message` の種類はボットとユーザー間の通信を表します。

ボットは、ユーザー メッセージ`Text`と、ユーザーに関するその他の情報、メッセージのソース、およびTeams情報を含むペイロードを受け取ります。注意:

* `timestamp`世界協定時刻 (UTC) でのメッセージの日付と時刻。
* `localTimestamp` 送信者のタイム ゾーン内のメッセージの日付と時刻。
* `channelId` は常に "msteams" です。これは、チーム チャネルではなく、ボット フレームワーク チャネルを指します。
* `from.id` ボットのユーザーのユニークで暗号化された ID; アプリでユーザー データを格納する必要がある場合は、キーとして適しています。 ボットに対して固有であり、そのユーザーを識別する意味のある方法でボット インスタンスの外部で直接使用することはできません。
* `channelData.tenant.id` - ユーザーの テナント ID。

> [!NOTE]
> `from.id` はボットに対して固有であり、そのユーザーを識別する意味のある方法でボット インスタンスの外部で直接使用することはできません。

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>チャネルとプライベートの対話をボットで結合させる

チャネルで対話する場合、ボットはユーザーとの特定の会話をオフラインにすることについてスマートにする必要があります。 たとえば、ユーザーが一連のチーム メンバーとのスケジュール設定など、複雑なタスクを調整しようとしているとします。 チャネルに対して一連の対話全体を表示するのではなく、ユーザーに個人用チャット メッセージを送信することを検討してください。 ボットは、状態を失うことなく、ユーザーを個人会話とチャネル会話の間で簡単に切り替えることができる必要があります。

> [!NOTE]
>操作が完了したら、チャネルを更新して他のメンバーに通知することを忘れないでください。

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
> 受信メッセージのテキスト フィールドにメンションが含まれている場合があります。 これらを正しく確認して取り除きます。 詳細については、「[メンション](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)」をご覧ください。

## <a name="teams-channel-data"></a>Teamsチャネルデータ

`channelData`オブジェクトにはTeams固有の情報が含まれており、チーム ID とチャネル ID の決定的なソースです。 これらの ID をキャッシュし、ローカル ストレージのキーとして使用する必要があります。

ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれています:

* `eventType`Teamsイベントの種類; [チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。
* `tenant.id`Microsoft Azure Active Directory (Azure AD) テナント ID; すべてのコンテキストで渡されます。
* `team` 個人用チャットではなく、チャネル コンテキストでのみ渡されます。
  * `id` チャネルの GUID。
  * `name` チームの名前; [は、チーム名変更イベント](~/resources/bot-v3/bots-notifications.md#team-name-updates)の場合にのみ渡されます。
* `channel` ボットが言及されたとき、またはボットが追加されたチームのチャネル内のイベントに対してのみ、チャネル コンテキストで渡されます。
  * `id` チャネルの GUID。
  * `name` チャネル名; [チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。
* `channelData.teamsTeamId` は非推奨です。このプロパティは、後方互換性のためにのみ含まれます。
* `channelData.teamsChannelId` は非推奨です。このプロパティは、後方互換性のためにのみ含まれます。

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

[Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージは、 Teams 固有の情報にアクセスするためのプロパティを公開する特殊な `TeamsChannelData` オブジェクト を提供します。

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>メッセージへの返信の送信

既存のメッセージに返信するには、.NET では [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true)、Node.js では [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) を呼び出します。 Bot Builder SDK で、すべての詳細が処理されます。

REST API を使用する場合は、[`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) エンドポイントを呼び出すこともできます。

メッセージ コンテンツ自体には、単純なテキストまたは Bot フレームワーク によって提供された [カードとカードアクション](~/task-modules-and-cards/cards/cards-actions.md)の一部を含めることができます。

送信スキーマでは、受信したスキーマと常に同じ `serviceUrl` を使用する必要があることに注意してください。 `serviceUrl` の値は安定する傾向がありますが、変更される可能性があることに注意してください。 新しいメッセージが届いたら、ボットは格納されている `serviceUrl`の値を確認する必要があります。

## <a name="updating-messages"></a>メッセージを更新しています

メッセージをデータの静的スナップショットにするのではなく、送信後にメッセージをインラインで動的に更新できます。 ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオでは、動的メッセージ更新を使用できます。

新しいメッセージは、種類の元のメッセージと一致する必要はありません。 たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージはテキスト メッセージにすることができます。

> [!NOTE]
> 単一の添付ファイル メッセージとカルーセル レイアウトで送信されたコンテンツのみを更新できます。 リスト レイアウト内の複数の添付ファイルを含むメッセージへの更新の投稿はサポートされていません。

### <a name="rest-api"></a>REST API

メッセージ更新プログラムを発行するには、特定のアクティビティ ID を使用して `/v3/conversations/<conversationId>/activities/<activityId>/` エンドポイントに対して PUT 要求を実行するだけです。 このシナリオを完了するには、元の POST 呼び出しによって返されたアクティビティ ID をキャッシュする必要があります。

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>.NET の例

Bot Builder SDK の `UpdateActivityAsync` メソッドを使用して、既存のメッセージを更新できます。

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

### <a name="nodejs-example"></a>Node.js の例

Bot Builder SDK の `session.connector.update` メソッドを使用して、既存のメッセージを更新できます。

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

ユーザーとの個人的な会話を作成したり、チーム ボットのチャネルで新しい返信チェーンを開始したりできます。 これにより、ユーザーが最初にボットとの連絡を開始しなくても、メッセージを送信できます。 詳細については、次の記事を参照してください。

ボットによって開始される会話の一般的な情報については、「 [ボットのプロアクティブ メッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 」を参照してください。

## <a name="deleting-messages"></a>メッセージの削除

メッセージは [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted)のコネクタ[`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html)メソッドを使用して削除できます。

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
