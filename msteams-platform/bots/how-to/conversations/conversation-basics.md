---
title: 会話の基礎
author: clearab
description: Microsoft Teams bot との会話を行う方法
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2d241ad04509c596e97647138bab2a749fa0f74c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674768"
---
# <a name="conversation-basics"></a>会話の基礎

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

会話とは、ボットと1人以上のユーザーとの間で送信される一連のメッセージのことです。 Teams には、次の3種類の会話 (スコープとも呼ばれる) があります。

* `teams`チャネルの会話とも呼ばれ、チャネルのすべてのメンバーに表示されます。
* `personal`ボットと1人のユーザーとの会話。
* `groupChat`ボットと2人以上のユーザーとの間でチャットを行います。 また、会議チャットでボットを有効にします。

Bot は、関係する会話の種類に応じて、微妙に動作が異なります。

* チャネルおよびグループチャットの会話に含まれる bot は、ユーザーがチャネルで bot を呼び出すようにボットに言及する必要があります。
* 一対一の会話の bot には、@ メンションは必要ありません。 ユーザーによって送信されるすべてのメッセージは bot にルーティングされます。

特定のスコープでボットを有効にするには、そのスコープを[アプリのマニフェスト](~/resources/schema/manifest-schema.md)に追加します。

## <a name="activities"></a>アクティビティ

各メッセージは、 `Activity`型`messageType: message`のオブジェクトです。 ユーザーがメッセージを送信すると、Teams がメッセージを bot に投稿します。具体的には、ユーザーは bot のメッセージングエンドポイントに JSON オブジェクトを送信します。 Bot は、メッセージを調べて、その種類を特定し、それに応じて応答します。

基本的な会話は Bot フレームワークコネクタを介して処理されます。これは、ボットが Teams やその他のチャネルと通信できるようにするための1つの REST API です。 Bot ビルダー SDK は、この API への簡単なアクセス、会話フローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを簡単に組み込むための簡単な方法を提供します。

## <a name="receive-a-message"></a>メッセージを受信する

テキストメッセージを受信するには、 `Text` `Activity`オブジェクトのプロパティを使用します。 Bot のアクティビティハンドラーで、turn コンテキストオブジェクト`Activity`を使用して1つのメッセージ要求を読み取ります。

次のコードは例を示しています。

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# <a name="pythontabpython"></a>[Python](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

---

## <a name="send-a-message"></a>メッセージの送信

テキストメッセージを送信するには、アクティビティとして送信する文字列を指定します。 Bot のアクティビティハンドラーで、turn コンテキストオブジェクトの`SendActivityAsync`メソッドを使用して、1つのメッセージ応答を送信します。 オブジェクトのメソッドを使用して`SendActivitiesAsync` 、一度に複数の応答を送信することもできます。 次のコードは、会話に他のユーザーが追加されたときにメッセージを送信する例を示しています。  

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity('Hello and welcome!');
            await next();
        });
    }
}
```

# <a name="pythontabpython"></a>[Python](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="jsontabjson"></a>[JSON](#tab/json)

```json
{
    "text": "hi",
    "textFormat": "plain",
    "type": "message",
    "timestamp": "2019-10-31T20:57:27.2347285Z",
    "localTimestamp": "2019-10-31T13:57:27.2347285-07:00",
    "id": "1572555447214",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1Xv-kvy4dKirR0rZfSF_kAVUzotoT1SXuEzkC9XGkuZng8YBw8qyu5uh4128fQRjlGgvEiRLx-0XP4KYMwcgdZw",
        "name": "Jane Doe",
        "aadObjectId": "df486eae-88fd-42a5-b45e-c581588186db"
    },
    "conversation": {
        "conversationType": "personal",
        "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "id": "a:1oAmWTVBBe9E0JrpGxauqNyx4CCE_iQf2ZuWon9D42722Fon3wYIpbhgbRChE3wgVS1Gwl9zS1pZy4FSu6-x1vGEq5KBQK-EbBgyPyeP_C-lbLBY3vxnGk9m9D_282jbg"
    },
    "recipient": {
        "id": "28:5baea8d1-d4ea-43a1-b101-882f4c8d9cb4",
        "name": "Imported Bot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Windows",
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

---

## <a name="teams-channel-data"></a>Teams チャネルデータ

この`channelData`オブジェクトには Teams 固有の情報が含まれており、チームおよびチャネル id の最終ソースとなります。 これらの id をローカルストレージのキーとしてキャッシュして使用する必要がある場合があります。 通常`TeamsActivityHandler` 、SDK のでは、 `channelData`オブジェクトから重要な情報を取得して、アクセスしやすいようにします。ただし、 `turnContext`オブジェクトから元の情報にいつでもアクセスできます。

この`channelData`オブジェクトは、チャネルの外側で行われるため、個人の会話のメッセージには含まれません。

Bot に送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれています。

* `eventType`Teams イベントの種類。[チャネル変更イベント](~/bots/how-to/conversations/subscribe-to-conversation-events.md)の場合にのみ渡されます。
* `tenant.id`Azure Active Directory テナント ID。すべてのコンテキストで渡される
* `team`チャネルコンテキストでのみ渡され、個人用チャットには渡されません。
  * `id`チャネルの GUID
  * `name`チームの名前。[チームの名前変更イベント](~/bots/how-to/conversations/subscribe-to-conversation-events.md)の場合にのみ渡される
* `channel`Bot が言及された場合、または bot が追加されている teams のチャネルでイベントが発生した場合に、チャネルコンテキストでのみ渡されます。
  * `id`チャネルの GUID
  * `name`チャネル名。[チャネル変更イベント](~/bots/how-to/conversations/subscribe-to-conversation-events.md)の場合にのみ渡されます。
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

## <a name="message-content"></a>メッセージの内容

Bot は、リッチテキスト、画像、およびカードを送信できます。 ユーザーは bot にリッチテキストと画像を送信できます。

| Format    | ユーザーから bot | Bot からユーザー | メモ                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| リッチ テキスト  | ✔                | ✔                |                                                                                         |
| ピクチャ  | ✔                | ✔                | 最高1024×1024、1 MB (PNG、JPEG、または GIF 形式)アニメーション GIF はサポートされていません  |
| Lcc     | ✖                | ✔                | サポートされているカードについては、 [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)を参照してください。 |
| 絵文字    | ✖                | ✔                | 現在、Teams は utf-16 を介して絵文字をサポートしています (grinning フェイスの U + 1f600 など)          |

## <a name="adding-notifications-to-your-message"></a>メッセージに通知を追加する

通知ユーザーが作業していることに関連する新しいタスク、メンション、コメントについてユーザーに警告するか、アクティビティフィードに通知を挿入して確認する必要があります。 " `TeamsChannelData` Objects/オブジェクト`Notification.Alert` " プロパティを true に設定することによって、ボットメッセージからトリガに対する通知を設定することができます。 通知が発生するかどうかは、最終的に個々のユーザーの Teams 設定に依存し、これらの設定をプログラムで上書きすることはできません。 通知の種類は、バナーまたはバナーと電子メールの両方のいずれかになります。

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="pythontabpython"></a>[Python](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="jsontabjson"></a>[JSON](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

## <a name="picture-messages"></a>画像メッセージ

画像は、メッセージに添付ファイルを追加することによって送信されます。 添付ファイルの詳細については、[ボットフレームワークのドキュメント](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)を参照してください。

画像は最大1024×1024で、PNG、JPEG、または GIF 形式の 1 MB にすることができます。アニメーション GIF はサポートされていません。

XML を使用して、各画像の高さと幅を指定することをお勧めします。 Markdown を使用する場合、画像のサイズは既定で256×256に設定されています。 例:

* 使え`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* を使用しない-`![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="next-steps"></a>次のステップ

* [事前メッセージの送信](~/bots/how-to/conversations/send-proactive-messages.md)
* [会話イベントにサブスクライブする](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
