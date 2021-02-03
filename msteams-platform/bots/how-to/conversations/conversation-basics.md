---
title: 会話の基本
author: clearab
description: Microsoft Teams ボットと会話する方法
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6f7e7a4d1be08126c96dff07ddbc3e1156700a90
ms.sourcegitcommit: 94ad961ecd002805b4e0424601d1c0ec191ff376
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "50075694"
---
# <a name="conversation-basics"></a>会話の基本

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。 Teams には、次の 3 種類の会話 (スコープとも呼ばれる) があります。

* `teams` チャネル会話とも呼ばれる、チャネルのすべてのメンバーに表示されます。
* `personal` ボットと 1 人のユーザーの会話。
* `groupChat` ボットと 2 人以上のユーザーの間でチャットします。 また、会議チャットでボットを有効にできます。

ボットの動作は、関連する会話の種類によって少し異なります。

* チャネルとグループ チャットの会話のボットでは、ユーザーがボットを @メンションしてチャネルで呼び出す必要があります。
* 1 対 1 の会話のボットには@ メンションは必要ではありません。 ユーザーによって送信されたすべてのメッセージがボットにルーティングされます。

特定のスコープでボットを有効にするには、そのスコープをアプリ マニフェストに [追加します](~/resources/schema/manifest-schema.md)。

## <a name="activities"></a>アクティビティ

各メッセージは `messageType: message` 型の `Activity` オブジェクトです。 ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。 ボットがメッセージを調べて種類を特定し、それに応じて応答します。

基本的な会話は、ボットが Teams や他のチャネルと通信するための単一の REST API である Bot Framework Connector を通じて処理されます。 Bot Builder SDK は、この API への簡単なアクセス、会話のフローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法を提供します。

## <a name="receive-a-message"></a>メッセージを受信する

テキスト メッセージを受信するには、`Activity` オブジェクトの `Text` プロパティを使用します。 ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `Activity` を使用して、1 つのメッセージ要求を読み取ります。

次のコードは例を示しています。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[JSON](#tab/json)

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

## <a name="send-a-message"></a>メッセージを送信する

テキスト メッセージを送信するには、送信する文字列をアクティビティとして指定します。 ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `SendActivityAsync` メソッドを使用して、1 つのメッセージ応答を送信します。 オブジェクトのメソッドを使用して、一 `SendActivitiesAsync` 度に複数の応答を送信できます。 次のコードは、誰かが会話に追加されたときにメッセージを送信する例を示しています  

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[JSON](#tab/json)

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

## <a name="teams-channel-data"></a>Teams チャネル データ

オブジェクトには Teams 固有の情報が含まれているので、チームとチャネルの ID の確定的 `channelData` なソースです。 ローカル ストレージのキーとしてこれらの ID をキャッシュして使用する必要がある場合があります。 SDK では通常、オブジェクトから重要な情報を取り出してアクセスしやすくしますが、いつでもオブジェクトの元の情報に `TeamsActivityHandler` `channelData` アクセス `turnContext` できます。

オブジェクトはチャネルの外部で行うので、個人の会話の `channelData` メッセージには含まれません。

ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれます。

* `eventType` Teams イベントの種類:チャネル変更イベントの場合 [にのみ渡されます。](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `tenant.id` Azure Active Directory テナント ID;すべてのコンテキストで渡される
* `team` チャネル コンテキストでのみ渡されます。個人用チャットでは渡されます。
  * `id` チャネルの GUID
  * `name` チームの名前。チームの名前変更イベントの場合 [にのみ渡されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channel` ボットが言及されている場合、またはボットが追加されたチームのチャネルのイベントに対して、チャネル コンテキストでのみ渡されます。
  * `id` チャネルの GUID
  * `name` チャネル名チャネル変更イベントの場合 [にのみ渡されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
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

## <a name="message-content"></a>メッセージの内容

ボットは、リッチ テキスト、画像、カードを送信できます。 ユーザーは、リッチ テキストと画像をボットに送信できます。

| フォーマット    | ユーザーからボットへ | ボットからユーザーへ | Notes                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| リッチ テキスト | ✔                | ✔                |                                                                                         |
| ピクチャ  | ✔                | ✔                | 最大 1024×1024 および 1 MB (PNG、JPEG、または GIF 形式)。アニメーション GIF はサポートされていません  |
| カード     | ✖                | ✔                | サポートされている [カードについては、「Teams カード リファレンス](~/task-modules-and-cards/cards/cards-reference.md) 」を参照してください。 |
| Emojis    | ✖                | ✔                | Teams は現在 UTF-16 を介して絵文字をサポートしています (顔のくびくびくをする U+1F600 など)          |

## <a name="adding-notifications-to-your-message"></a>メッセージへの通知の追加

通知は、作業している作業に関連する新しいタスク、メンション、コメント、またはアクティビティ フィードに通知を挿入して確認する必要があるタスク、メンション、コメントについてユーザーに警告します。 objects プロパティを true に設定することで、ボット メッセージからトリガーする `TeamsChannelData` `Notification.Alert` 通知を設定できます。 通知が発生するかどうかは、最終的には個々のユーザーの Teams 設定に依存し、これらの設定をプログラムで上書きすることはできません。 通知の種類は、バナー、またはバナーとメールの両方です。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[Python](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[JSON](#tab/json)

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

画像は、メッセージに添付ファイルを追加することで送信されます。 添付ファイルの詳細については、Bot Framework のドキュメント [を参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)。

画像は、PNG、JPEG、GIF 形式で最大 1024×1024 および 1 MB です。アニメーション GIF はサポートされていません。

XML を使用して各イメージの高さと幅を指定することをお勧めします。 Markdown を使用する場合、画像サイズの既定値は 256×256 です。 例:

* Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* 使用しない - `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="code-sample"></a>コード サンプル
|**サンプルの名前** | **説明** | **.NETCore** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| Teams 会話ボット | メッセージングと会話イベントの処理。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a>次の手順

* [プロアクティブ メッセージの送信](~/bots/how-to/conversations/send-proactive-messages.md)
* [会話イベントにサブスクライブする](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
