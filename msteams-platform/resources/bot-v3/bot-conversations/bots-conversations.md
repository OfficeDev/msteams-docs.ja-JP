---
title: Bot でメッセージを送受信する
description: Microsoft Teams でボットを使用してメッセージを送受信する方法について説明します。
keywords: teams の bot メッセージ
ms.date: 05/20/2019
ms.openlocfilehash: 864473c7f502d96987a48e5837840236c45f59c7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675113"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Microsoft Teams bot との会話

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

会話とは、ボットと1人以上のユーザーとの間で送信される一連のメッセージのことです。 Teams には、次の3種類の会話 (スコープとも呼ばれる) があります。

* `teams`チャネルの会話とも呼ばれ、チャネルのすべてのメンバーに表示されます。
* `personal`ボットと1人のユーザーとの会話。
* `groupChat`ボットと2人以上のユーザーとの間でチャットを行います。

Bot は、関係する会話の種類に応じて、微妙に動作が異なります。

* [チャネルおよびグループチャットの会話に含まれる bot](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)は、ユーザーがチャネルで bot を呼び出すようにボットに言及する必要があります。
* [単一のユーザー会話のボットで](~/resources/bot-v3/bot-conversations/bots-conv-personal.md)は、@ メンションは必要ありません。ユーザーは単に入力できます。

Bot が特定のスコープで機能するためには、マニフェストでその範囲をサポートするようにリストされている必要があります。 スコープは[マニフェストの参照](~/resources/schema/manifest-schema.md)で定義され、さらに詳しく説明されています。

## <a name="proactive-messages"></a>事前メッセージ

Bot は、会話に参加したり、1つ開始したりできます。 ほとんどの通信は、別のメッセージに応答します。 Bot が会話を開始した場合は、"*予防的メッセージ*" と呼ばれます。 例:

* ウェルカムメッセージ
* イベント通知
* ポーリングメッセージ

## <a name="conversation-basics"></a>会話の基礎

各メッセージは、 `Activity`型`messageType: message`のオブジェクトです。 ユーザーがメッセージを送信すると、Teams がメッセージを bot に投稿します。具体的には、ユーザーは bot のメッセージングエンドポイントに JSON オブジェクトを送信します。 Bot は、メッセージを調べて、その種類を特定し、それに応じて応答します。

Bot は、イベントスタイルのメッセージもサポートします。 詳細については、「 [Microsoft Teams のハンドル bot イベント](~/resources/bot-v3/bots-notifications.md)」を参照してください。 音声認識は現在サポートされていません。

メッセージは、すべてのスコープ間で同じようにほとんど同じですが、UI での bot へのアクセス方法と、その背後で知っておく必要がある相違点には違いがあります。

基本的な会話は Bot フレームワークコネクタを介して処理されます。これは、ボットが Teams やその他のチャネルと通信できるようにするための1つの REST API です。 Bot ビルダー SDK は、この API への簡単なアクセス、会話フローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを簡単に組み込むための簡単な方法を提供します。

## <a name="message-content"></a>メッセージの内容

Bot は、リッチテキスト、画像、およびカードを送信できます。 ユーザーは bot にリッチテキストと画像を送信できます。 Bot が [Microsoft Teams の設定] ページで処理できるコンテンツの種類を指定できます。

| Format | ユーザーから bot  | Bot からユーザー |  メモ |
| --- | :---: | :---: | --- |
| リッチ テキスト  | ✔ | ✔ |  |
| ピクチャ | ✔ | ✔ | 最高1024×1024、1 MB (PNG、JPEG、または GIF 形式)アニメーション GIF はサポートされていません |
| Lcc | ✖ | ✔ | サポートされているカードについては、 [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)を参照してください。 |
| 絵文字 | ✖ | ✔ | 現在、Teams は utf-16 を介して絵文字をサポートしています (grinning フェイスの U + 1f600 など) |
|

Bot フレームワークによってサポートされる bot の相互作用の種類 (teams の基礎となる bot) の詳細については、bot[ビルダー sdk for .net](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0)および[ボット builder sdk for node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0)のドキュメントの bot フレームワークのドキュメントを[参照して](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0)ください。

## <a name="message-formatting"></a>メッセージの書式設定

メッセージのテキストコンテンツの[`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message)表示方法を`message`制御するには、のオプションのプロパティを設定できます。 Bot メッセージでサポートされている書式の詳細な説明については、「[メッセージ形式](~/resources/bot-v3/bots-message-format.md)」を参照してください。
オプション[`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message)のプロパティを設定して、メッセージのテキストコンテンツの表示方法を制御することができます。

Teams におけるテキストの書式設定のサポートの詳細については、 [bot メッセージのテキスト形式](~/resources/bot-v3/bots-text-formats.md)を参照してください。

メッセージ内のカードの書式設定の詳細については、「[カードの書式](~/task-modules-and-cards/cards/cards-format.md)設定」を参照してください。

## <a name="picture-messages"></a>画像メッセージ

画像は、メッセージに添付ファイルを追加することによって送信されます。 添付ファイルの詳細については、[ボットフレームワークのドキュメント](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)を参照してください。

画像は最大1024×1024で、PNG、JPEG、または GIF 形式の 1 MB にすることができます。アニメーション GIF はサポートされていません。

XML を使用して、各画像の高さと幅を指定することをお勧めします。 Markdown を使用する場合、画像のサイズは既定で256×256に設定されています。 例:

* 使え`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* 使用しない `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>メッセージの受信

どのスコープが宣言されているかに応じて、bot は次のコンテキストでメッセージを受信できます。

* **個人チャット**ユーザーは、チャット履歴で追加された bot を選択するか、新しいチャットの [宛先] ボックスにその名前またはアプリ ID を入力するだけで、自分のボットでプライベートな会話を操作できます。
* **チャネル**チームに追加された bot ("@_botname_") はチャネルで言及できます。 チャネル内の bot への追加の応答には、bot に言及する必要があることに注意してください。 記載されていない場合、返信には応答しません。

受信メッセージの場合、bot は型[`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) `messageType: message`のオブジェクトを受け取ります。 このオブジェクト`Activity`には、bot に送信される[チャネルの更新](~/resources/bot-v3/bots-notifications.md#channel-updates)など、他の種類の`message`情報を含めることができますが、この型は bot とユーザーの間の通信を表します。

Bot は、ユーザーメッセージ`Text`だけでなく、ユーザーに関するその他の情報、メッセージの送信元、Teams 情報を含むペイロードを受け取ります。 注:

* `timestamp`協定世界時 (UTC) でのメッセージの日付と時刻
* `localTimestamp`送信者のタイムゾーンにおけるメッセージの日付と時刻
* `channelId`常に "msteams"。 これは、teams チャネルではなく bot フレームワークチャネルを参照します。
* `from.id`Bot に対して、そのユーザーの一意で暗号化された ID。アプリでユーザーデータを格納する必要がある場合は、キーとして適しています。 Bot に対して一意であり、ボットインスタンス外では、そのユーザーを特定するために任意の方法で直接使用することはできません。
* `channelData.tenant.id`ユーザーのテナント ID。

> [!NOTE]
> `from.id`は bot に対して一意であり、bot インスタンス外では、そのユーザーを特定するために任意の方法で直接使用することはできません。

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>チャネルとプライベートな相互作用を bot と組み合わせる

チャネルを操作する場合、ユーザーとの特定の会話をオフラインにすることをお勧めします。 たとえば、ユーザーが一連のチームメンバーとのスケジュール設定など、複雑なタスクをコーディネートしようとしているとします。 一連の対話がチャネルに表示されるのではなく、ユーザーに個人用チャットメッセージを送信することを検討してください。 Bot は、状態を失わずに、個人会話とチャネル会話間でユーザーを簡単に移行できるようにする必要があります。

> [!NOTE]
>他のチームメンバーに通知するために、相互作用の完了時にチャネルを更新することを忘れないでください。

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
> 受信メッセージのテキストフィールドには、メンションが含まれる場合があります。 適切に確認して、ストリップする必要があります。 詳細については、「[メンション](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)」を参照してください。

## <a name="teams-channel-data"></a>Teams チャネルデータ

この`channelData`オブジェクトには Teams 固有の情報が含まれており、チームおよびチャネル id の最終ソースとなります。 これらの id は、ローカルストレージのキーとしてキャッシュして使用する必要があります。

この`channelData`オブジェクトは、チャネルの外側で行われるため、個人の会話のメッセージには含まれません。

Bot に送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれています。

* `eventType`Teams イベントの種類。[チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。
* `tenant.id`Azure Active Directory テナント ID。すべてのコンテキストで渡される
* `team`チャネルコンテキストでのみ渡され、個人用チャットには渡されません。
  * `id`チャネルの GUID
  * `name`チームの名前。[チームの名前変更イベント](~/resources/bot-v3/bots-notifications.md#team-name-updates)の場合にのみ渡される
* `channel`Bot が言及された場合、または bot が追加されている teams のチャネルでイベントが発生した場合に、チャネルコンテキストでのみ渡されます。
  * `id`チャネルの GUID
  * `name`チャネル名。[チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。
* `channelData.teamsTeamId`予定. このプロパティは、下位互換性のためにのみ含まれています。
* `channelData.teamsChannelId`予定. このプロパティは、下位互換性のためにのみ含まれています。

### <a name="example-channeldata-object-channelcreated-event"></a>ChannelData オブジェクトの例 (Channeldata イベント)

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

Teams[の NuGet パッケージ](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)には、teams 固有の情報にアクセス`TeamsChannelData`するためのプロパティを公開する特別なオブジェクトが用意されています。

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>メッセージへの返信の送信

既存のメッセージに返信するには[`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) 、.net また[`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities)は node.js で呼び出します。 Bot ビルダー SDK は、すべての詳細を処理します。

REST API の使用を選択する場合は、 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0)エンドポイントを呼び出すこともできます。

メッセージコンテンツ自体には、単純なテキスト、または Bot フレームワーク提供の[カードおよびカードアクション](~/task-modules-and-cards/cards/cards-actions.md)を含めることができます。

送信スキーマでは、受信したものと同じ`serviceUrl`を常に使用する必要があることに注意してください。 の`serviceUrl`値は安定していますが、変更される可能性があることに注意してください。 新しいメッセージが到着すると、ボットはに格納されて`serviceUrl`いる値を確認する必要があります。

## <a name="updating-messages"></a>メッセージを更新する

Bot は、メッセージを送信した後、メッセージをデータの静的なスナップショットにするのではなく、メッセージを送信した後にメッセージを動的に更新することができます。 動的メッセージ更新は、投票の更新、ボタンの押した後の使用可能なアクションの変更、またはその他の非同期状態の変更などのシナリオで使用できます。

新しいメッセージは、元の種類と一致する必要はありません。 たとえば、元のメッセージに添付ファイルが含まれていた場合、新しいメッセージは単純なテキストメッセージにすることができます。

> [!NOTE]
> 単一添付ファイルメッセージおよびカルーセルレイアウトで送信されたコンテンツのみを更新できます。 リストレイアウトに複数の添付ファイルがあるメッセージへの更新の送信はサポートされていません。

### <a name="rest-api"></a>REST API

メッセージ更新を発行するには、特定のアクティビティ ID を`/v3/conversations/<conversationId>/activities/<activityId>/`使用して、エンドポイントに対する PUT 要求を実行するだけです。 このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>.NET の例

Bot ビルダー SDK の`UpdateActivityAsync`メソッドを使用して、既存のメッセージを更新することができます。

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

Bot ビルダー SDK の`session.connector.update`メソッドを使用して、既存のメッセージを更新することができます。

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

## <a name="starting-a-conversation-proactive-messaging"></a>会話の開始 (事前メッセージ)

ユーザーとの間で個人の会話を作成したり、チームの bot のチャネルで新しい返信チェーンを開始したりすることができます。 これにより、ユーザーに対して、最初に bot との連絡を開始させずに、ユーザーにメッセージを表示することができます。 詳細については、次のトピックをご覧ください。

Bot が開始した会話に関する一般的な情報については、「[予防的なメッセージング」を](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)参照してください。

## <a name="deleting-messages"></a>メッセージの削除

メッセージは、 [BOTBUILDER SDK](/bot-framework/bot-builder-overview-getstarted)のコネクタ[`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete)メソッドを使用して削除できます。

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
