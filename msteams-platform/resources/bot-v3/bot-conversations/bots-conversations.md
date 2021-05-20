---
title: ボットを使用したメッセージの送受信
description: Microsoft Teamsでボットを使用してメッセージを送受信する方法について説明Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: チームボットメッセージ
ms.date: 05/20/2019
ms.openlocfilehash: e1926afe42bca45eda5f39be1be8342452b3aa24
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566496"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Microsoft Teamsボットと会話する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。 Teams には、次の 3 種類の会話 (スコープとも呼ばれる) があります。

* `teams` チャネル会話とも呼ばれ、チャネルのすべてのメンバーに表示されます。
* `personal` ボットと単一ユーザー間の会話。
* `groupChat` ボットと複数のユーザーの間でチャットします。

ボットは、どのような会話に関係するかによって、少し異なる動作をします。

* [チャネルチャットとグループチャットの会話のボット](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) では、ユーザーがチャネルで呼び出すためにボットを@mentionする必要があります。
* [単一ユーザー会話のボット](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) は@mentionを必要としません - ユーザーは入力するだけで済みます。

ボットが特定のスコープで動作するためには、そのスコープをサポートするマニフェストとしてリストする必要があります。 スコープは、 [マニフェスト リファレンス](~/resources/schema/manifest-schema.md)で定義および説明します。

## <a name="proactive-messages"></a>プロアクティブ メッセージ

ボットは、会話に参加したり、会話を開始したりできます。 ほとんどの通信は、別のメッセージに応答しています。 ボットが会話を開始した場合は、 *プロアクティブ メッセージ* と呼ばれます。 たとえば、次のような情報が含まれます。

* ウェルカム メッセージ
* イベント通知
* メッセージのポーリング

## <a name="conversation-basics"></a>会話の基本

各メッセージは `messageType: message` 型の `Activity` オブジェクトです。 ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。 ボットはメッセージを調べて、その種類を判断し、それに応じて応答します。

ボットはイベント形式のメッセージもサポートしています。 詳細については[、「Microsoft Teamsでのボット イベントの処理」を](~/resources/bot-v3/bots-notifications.md)参照してください。 現在、音声はサポートされていません。

メッセージは、ほとんどの場合、すべてのスコープで同じですが、UI でボットにアクセスする方法と、知る必要がある舞台裏の違いには違いがあります。

基本的な会話は、ボットがTeamsやその他のチャネルと通信できるようにするための単一の REST API である Bot Framework コネクタを通じて処理されます。 Bot Builder SDK は、この API へのアクセスが簡単で、会話フローと状態を管理するための追加機能、および自然言語処理 (NLP) などのコグニティブ サービスを組み込む簡単な方法を提供します。

## <a name="message-content"></a>メッセージの内容

ボットはリッチ テキスト、画像、およびカードを送信できます。 ユーザーは、ボットにリッチ テキストや画像を送信できます。 ボットのMicrosoft Teams設定ページで、ボットが処理できるコンテンツの種類を指定できます。

| Format | ユーザーからボットへ  | ボットからユーザーへ |  備考 |
| --- | :---: | :---: | --- |
| リッチ テキスト | ✔ | ✔ |  |
| ピクチャ | ✔ | ✔ | PNG、JPEG、または GIF 形式の最大 1024×1024 および 1 MB。アニメーション GIF はサポートされていません。 |
| カード | ✖ | ✔ | サポートされている[カードについては、Teamsカードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)を参照してください。 |
| 絵文字 | ✖ | ✔ | Teamsは現在、顔をニヤニヤするためのU + 1F600などのUTF-16経由で絵文字をサポートしています。 |
|

チーム内のボットが基づいているボット フレームワークでサポートされるボットの相互作用の種類の詳細については、ボット[ビルダー SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true)およびボット ビルダー SDK for Node.jsのドキュメントの[会話フロー](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true)と関連概念に関する Bot Framework のドキュメント[を](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)参照してください。

## <a name="message-formatting"></a>メッセージの書式設定

の省略可能 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) なプロパティ `message` を設定して、メッセージのテキスト コンテンツの表示方法を制御できます。 ボット メッセージでサポートされる書式設定の詳細については、「 [メッセージの書式設定](~/resources/bot-v3/bots-message-format.md) 」を参照してください。
オプションの [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) プロパティを設定して、メッセージのテキスト コンテンツの表示方法を制御できます。

チームでのテキストの書式設定Teamsサポートする方法の詳細については[、「bot メッセージでのテキストの書式設定](~/resources/bot-v3/bots-text-formats.md)」を参照してください。

メッセージのカードの書式設定の詳細については、「 [カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。

## <a name="picture-messages"></a>画像メッセージ

画像は、メッセージに添付ファイルを追加することによって送信されます。 添付ファイルの詳細については [、Bot Framework のドキュメントを参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)。

画像は、PNG、JPEG、または GIF 形式で、1024×1024 および 1 MB 以上にすることができます。アニメーション GIF はサポートされていません。

各画像の高さと幅は、XML を使用して指定することをお勧めします。 マークダウンを使用する場合、イメージサイズはデフォルトで 256×256 になります。 例:

* `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` を使う
* 使用しない `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>メッセージの受信

宣言されているスコープに応じて、ボットは次のコンテキストでメッセージを受信できます。

* **パーソナルチャット** ユーザーは、チャット履歴で追加されたボットを選択するか、新しいチャットの [To: ] ボックスにその名前またはアプリ ID を入力するだけで、ボットとのプライベートな会話をやり取りできます。
* **チャンネル** ボットがチームに追加されている場合、ボットはチャンネルで言及できます _(「@botname」)。_ チャネル内のボットに対する追加の返信には、ボットに言及する必要があります。 言及されていない場合は返信されません。

受信メッセージの場合、ボットは [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) type 型のオブジェクトを受け取ります `messageType: message` 。 オブジェクトには `Activity` 、ボットに送信される [チャネルの更新](~/resources/bot-v3/bots-notifications.md#channel-updates) など、他の種類の情報を含めることができますが、この `message` 型はボットとユーザー間の通信を表します。

ボットは、ユーザー メッセージ、ユーザー、メッセージの `Text` ソース、およびTeams情報に関するその他の情報を含むペイロードを受信します。 注意:

* `timestamp` 世界協定時刻 (UTC) でのメッセージの日付と時刻。
* `localTimestamp` 送信者のタイム ゾーン内のメッセージの日時。
* `channelId` 常に"msteams"。 これは、チーム チャネルではなく、ボット フレームワーク チャネルを指します。
* `from.id` ボットのそのユーザーの一意の暗号化 ID。アプリがユーザー データを格納する必要がある場合は、キーとして適しています。 この ID はボットに固有であり、そのユーザーを識別するために意味のある方法でボットインスタンスの外部で直接使用することはできません。
* `channelData.tenant.id` ユーザーのテナント ID。

> [!NOTE]
> `from.id` はボットに固有であり、そのユーザーを識別するために意味のある方法でボットインスタンスの外部で直接使用することはできません。

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>ボットとチャンネルとプライベートの相互作用を組み合わせる

チャネルで対話する場合、ボットはユーザーとの特定の会話をオフラインにすることに賢明である必要があります。 たとえば、ユーザーがチーム メンバーのセットを使用してスケジュールを設定するなど、複雑なタスクを調整しようとしているとします。 チャネルに対して対話のシーケンス全体を表示するのではなく、ユーザーに個人用のチャット メッセージを送信することを検討してください。 ボットは、状態を失うことなく、ユーザーの会話を簡単に個人会話とチャンネル会話に移行できる必要があります。

> [!NOTE]
>他のチーム メンバーに通知するために、対話が完了したときにチャネルを更新することを忘れないでください。

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
> 受信メッセージのテキスト フィールドには、メンションが含まれることがあります。 それらを正しくチェックして取り除くようにしてください。 詳細については、「 [メンション](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)」を参照してください。

## <a name="teams-channel-data"></a>チャネル データTeams

`channelData`このオブジェクトにはTeams固有の情報が含まれ、チーム ID とチャネル ID の決定的なソースです。 これらの ID をキャッシュし、ローカルストレージのキーとして使用する必要があります。

`channelData`オブジェクトは、チャネル外で行われるため、個人的な会話のメッセージには含まれません。

ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれています。

* `eventType`Teamsイベントの種類。[チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。
* `tenant.id`Azure Active Directoryテナント ID。すべてのコンテキストで渡されます。
* `team` チャンネルコンテキストでのみ渡され、パーソナルチャットでは渡されません。
  * `id` チャネルの GUID。
  * `name` チームの名前。 [チーム名変更イベント](~/resources/bot-v3/bots-notifications.md#team-name-updates)の場合にのみ渡されます。
* `channel` ボットが言及されている場合、またはボットが追加されたチームのチャネルのイベントに対してのみ、チャネル コンテキストで渡されます。
  * `id` チャネルの GUID。
  * `name` チャネル名。 [チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。
* `channelData.teamsTeamId` 廃止。 このプロパティは、下位互換性を保つためにのみ含まれています。
* `channelData.teamsChannelId` 廃止。 このプロパティは、下位互換性を保つためにのみ含まれています。

### <a name="example-channeldata-object-channelcreated-event"></a>チャネルデータ オブジェクトの例 (チャネル作成イベント)

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

[Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)パッケージには `TeamsChannelData` 、Teams固有の情報にアクセスするためのプロパティを公開する特殊なオブジェクトが用意されています。

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>メッセージへの返信

既存のメッセージに返信するには [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) 、.NET または [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) Node.jsで呼び出します。 ボット ビルダー SDK では、すべての詳細を処理します。

REST API を使用する場合は、エンドポイントを呼び出すこともできます [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) 。

メッセージの内容自体には、単純なテキストを含めることも、Bot Framework が提供する [カードやカード アクション](~/task-modules-and-cards/cards/cards-actions.md)を含めることができます。

送信スキーマでは、 `serviceUrl` 常に受信したものと同じものを使用する必要があります。 の値は `serviceUrl` 安定する傾向がありますが、変化する可能性があることに注意してください。 新しいメッセージが到着すると、ボットは保存された値を `serviceUrl` 確認する必要があります。

## <a name="updating-messages"></a>メッセージの更新

メッセージをデータの静的なスナップショットにするのではなく、送信後にメッセージをインラインで動的に更新できます。 動的メッセージ更新は、ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオに使用できます。

新しいメッセージは、元のメッセージの種類と一致する必要はありません。 たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージは単純なテキスト メッセージになります。

> [!NOTE]
> 単一添付ファイル メッセージおよびカルーセル レイアウトで送信されたコンテンツのみを更新できます。 リスト レイアウトで複数の添付ファイルを含むメッセージへの更新の投稿はサポートされていません。

### <a name="rest-api"></a>REST API

メッセージ更新を発行するには、 `/v3/conversations/<conversationId>/activities/<activityId>/` 指定されたアクティビティ ID を使用してエンドポイントに対して PUT 要求を実行するだけです。 このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>.NET の例

ボット ビルダー `UpdateActivityAsync` SDK のメソッドを使用して、既存のメッセージを更新できます。

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

ボット ビルダー `session.connector.update` SDK のメソッドを使用して、既存のメッセージを更新できます。

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

## <a name="starting-a-conversation-proactive-messaging"></a>会話の開始 (プロアクティブなメッセージング)

ユーザーとの個人的な会話を作成したり、チームボットのチャネルで新しい返信チェーンを開始したりできます。 これにより、ユーザーが最初にボットとの接触を開始することなく、ユーザーにメッセージを送信できます。 詳細については、次のトピックをご覧ください。

ボットが開始した会話の一般的な情報については [、「ボットのプロアクティブなメッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 」をご覧ください。

## <a name="deleting-messages"></a>メッセージの削除

BotBuilder SDK のコネクタ メソッドを使用してメッセージを削除できます [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) 。 [](/bot-framework/bot-builder-overview-getstarted)

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
