---
title: ボットの会話内のメッセージ
description: ボットと会話する方法についてMicrosoft Teamsします。 コード サンプルをTeamsチャネル データ、メッセージへの通知、ピクチャ メッセージ、アダプティブ カードについて学習します。
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: b78ca5b46442f30db3adfe314d627d3fc95682be
ms.sourcegitcommit: 25a33b31cc56c05169fc52c65d44c65c601aefef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2022
ms.locfileid: "62043232"
---
# <a name="messages-in-bot-conversations"></a>ボットの会話内のメッセージ

会話内の各メッセージは、 `Activity` 型のオブジェクトです `messageType: message` 。 ユーザーがメッセージを送信すると、Teamsボットにメッセージが投稿されます。 Teamsボットのメッセージング エンドポイントに JSON オブジェクトを送信します。 ボットはメッセージを調べて、その種類を特定し、それに応じて応答します。

基本的な会話は、単一の REST API である Bot Framework コネクタを介して処理されます。 この API を使用すると、ボットは他のチャネルTeams通信できます。 ボット ビルダー SDK には、次の機能があります。

* Bot Framework コネクタに簡単にアクセスできます。
* 会話のフローと状態を管理するための追加機能。
* 自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法。

ボットはプロパティを使用Teamsメッセージを受信し、ユーザーに単一または複数のメッセージ `Text` 応答を送信します。

## <a name="receive-a-message"></a>メッセージを受信する

テキスト メッセージを受信するには、`Activity` オブジェクトの `Text` プロパティを使用します。 ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `Activity` を使用して、1 つのメッセージ要求を読み取ります。

次のコードは、メッセージを受信する例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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
    "text": "Hello Teams TestBot.Sending bold-italic rich text",
    "attachments": [
      {
            "contentType": "text/html",
            "content": "<div><div>Hello Teams TestBot. Sending <strong>bold</strong>-<em>italic</em> rich text.</div>\n</div>"
      } 
    ],
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

テキスト メッセージを送信するには、送信する文字列をアクティビティとして指定します。 ボットのアクティビティ ハンドラーで、turn context オブジェクトのメソッドを使用して 1 つの `SendActivityAsync` メッセージ応答を送信します。 オブジェクトのメソッドを使用して `SendActivitiesAsync` 、複数の応答を一度に送信します。

次のコードは、ユーザーが会話に追加された場合にメッセージを送信する例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript

    this.onMembersAddedActivity(async (context, next) => {
        await Promise.all((context.activity.membersAdded || []).map(async (member) => {
            if (member.id !== context.activity.recipient.id) {
                await context.sendActivity(
                    `Welcome to the team ${member.givenName} ${member.surname}`
                );
            }
        }));

        await next();
    });
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
    "type": "message",
    "from": {
        "id": "28:c9e8c047-2a34-40a1-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "conversation": {
        "id": "a:17I0kl8EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-",
        "name": "Convo1"
   },
   "recipient": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB25ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen"
    },
    "text": "My bot's reply",
    "replyToId": "1632474074231"
}

```

---

> [!NOTE]
> メッセージの分割は、テキスト メッセージと添付ファイルが同じアクティビティ ペイロードで送信される場合に発生します。 このアクティビティは、テキスト メッセージMicrosoft Teams添付ファイルを持つ別のアクティビティに分割されます。 アクティビティが分割されている間、メッセージ ID は応答で受信されません。これは、メッセージを事前に更新または [削除するために使用](~/bots/how-to/update-and-delete-bot-messages.md) されます。 メッセージの分割に応じてではなく、個別のアクティビティを送信する方法をお勧めします。

ユーザーとボットの間で送信されるメッセージには、メッセージ内の内部チャネル データが含まれます。 このデータを使用すると、ボットはチャネルで適切に通信できます。 ボット ビルダー SDK を使用すると、メッセージ構造を変更できます。

## <a name="teams-channel-data"></a>Teamsチャネル データ

この `channelData` オブジェクトには、Teams固有の情報が含まれているので、チームとチャネルの ID の決定的なソースです。 必要に応じて、これらの ID をローカル ストレージのキーとしてキャッシュして使用できます。 `TeamsActivityHandler`SDK では、オブジェクトから重要な情報を取り出して、簡単 `channelData` にアクセスできます。 ただし、オブジェクトから元のデータにいつでもアクセス `turnContext` できます。

オブジェクトは、チャネルの外部で行なうので、個人的な会話の `channelData` メッセージには含まれません。

ボットに `channelData` 送信されるアクティビティの一般的なオブジェクトには、次の情報が含まれます。

* `eventType`: Teams変更イベントの場合にのみ渡されるイベント[の種類を指定します](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* `tenant.id`: Azure Active Directoryで渡されるテナント ID を指定します。
* `team`: チャネル コンテキストでのみ渡されます。個人チャットでは渡されない。
  * `id`: チャネルの GUID。
  * `name`: チーム名の変更イベントの場合にのみ渡された [チームの名前](~/bots/how-to/conversations/subscribe-to-conversation-events.md)です。
* `channel`: ボットが言及されている場合、またはボットが追加されたチーム内のチャネルのイベントに対して、チャネル コンテキストでのみ渡されます。
  * `id`: チャネルの GUID。
  * `name`: チャネル変更イベントの場合にのみ渡 [されるチャネル名](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* `channelData.teamsTeamId`: 非推奨です。 このプロパティは、下位互換性のためにのみ含まれます。
* `channelData.teamsChannelId`: 非推奨です。 このプロパティは、下位互換性のためにのみ含まれます。

### <a name="example-channeldata-object-or-channelcreated-event"></a>channelData オブジェクトまたは channelCreated イベントの例

次のコードは、channelData オブジェクトの例を示しています。

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

ボットから受信またはボットに送信されるメッセージには、さまざまな種類のメッセージ コンテンツを含めできます。

## <a name="message-content"></a>メッセージの内容

| フォーマット    | ユーザーからボットへ | ボットからユーザーへ | Notes                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| リッチ テキスト | ✔                | ✔                | ボットはリッチ テキスト、画像、カードを送信できます。 ユーザーは、リッチ テキストと画像をボットに送信できます。                                                                                        |
| ピクチャ  | ✔                | ✔                | 最大 1024 × 1024 および 1 MB (PNG、JPEG、または GIF 形式)。 アニメーション GIF はサポートされていません。  |
| カード     | ✖                | ✔                | サポートされているカード[についてはTeamsカード](~/task-modules-and-cards/cards/cards-reference.md)リファレンスを参照してください。 |
| 絵文字    | ✖                | ✔                | Teams、顔にニヤリと笑う U+1F600 など、UTF-16 による絵文字がサポートされています。 |

プロパティを使用してメッセージに通知を追加 `Notification.Alert` することもできます。

## <a name="notifications-to-your-message"></a>メッセージへの通知

通知は、新しいタスク、メンション、コメントについてユーザーに通知します。 これらのアラートは、ユーザーが作業している情報や、アクティビティ フィードに通知を挿入して表示する必要があるものに関連しています。 ボット メッセージから通知をトリガーするには、objects プロパティを `TeamsChannelData` true `Notification.Alert` に設定 *します*。 通知が発生するかどうかは、個々のユーザーの設定によって異Teams、これらの設定を上書きすることはできません。 通知の種類は、バナー、またはバナーとメールの両方です。

> [!NOTE]
> [ **概要] フィールド** には、ユーザーからのテキストがフィードに通知メッセージとして表示されます。

次のコードは、メッセージに通知を追加する例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

メッセージを強化するために、画像をそのメッセージの添付ファイルとして含めることができます。

## <a name="picture-messages"></a>ピクチャ メッセージ

画像は、メッセージに添付ファイルを追加して送信されます。 添付ファイルの詳細については [、Bot Framework のドキュメントを参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。

画像は、PNG、JPEG、または GIF 形式× 1024、1024、1 MB までです。 アニメーション GIF はサポートされていません。

XML を使用して各イメージの高さと幅を指定します。 markdown では、イメージ サイズの既定値は 256 ×256 です。 次に例を示します。

* 使用: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .
* 使用 `![Duck on a rock](http://aka.ms/Fo983c)` しない:

会話型ボットには、ビジネス ワークフローを簡素化するアダプティブ カードを含めできます。 アダプティブ カードは、豊富なカスタマイズ可能なテキスト、音声、画像、ボタン、および入力フィールドを提供します。

## <a name="adaptive-cards"></a>アダプティブ カード

アダプティブ カードはボットで作成し、Teams、Web サイトなど、複数のアプリに表示できます。 詳細については、「アダプティブ カード」 [を参照してください](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)。

次のコードは、単純なアダプティブ カードを送信する例を示しています。

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

ボット内のカードとカードの詳細については、カードのドキュメント [を参照してください](~/task-modules-and-cards/what-are-cards.md)。

## <a name="status-code-responses"></a>状態コードの応答

状態コードとエラー コードとメッセージ値を次に示します。

| 状態コード | エラー コードとメッセージ値 | 説明 |
|----------------|-----------------|-----------------|
| 403 | **コード**: `ConversationBlockedByUser` <br/> **メッセージ**: ユーザーがボットとの会話をブロックしました。 | ユーザーは、モデレート設定を使用して、1:1 チャットまたはチャネルでボットをブロックしました。 |
| 403 | **コード**: `BotNotInConversationRoster` <br/> **メッセージ**: ボットは会話名簿の一部ではありません。 | ボットは会話の一部ではありません。 |
| 403 | **コード**: `BotDisabledByAdmin` <br/> **メッセージ**: テナント管理者は、このボットを無効にしました。 | テナントがボットをブロックしました。 |
| 401 | **コード**: `BotNotRegistered` <br/> **メッセージ**: このボットの登録が見つかりません。 | このボットの登録が見つかりませんでした。 |
| 412 | **コード**: `PreconditionFailed` <br/> **メッセージ**: 事前条件に失敗しました。もう一度お試しください。 | 同じ会話に対する複数の同時操作が原因で、依存関係の 1 つでプレコンディションが失敗しました。 |
| 404 | **コード**: `ConversationNotFound` <br/> **メッセージ**: 会話が見つかりません。 | 会話が見つかりませんでした。 |
| 413 | **コード**: `MessageSizeTooBig` <br/> **メッセージ**: メッセージ サイズが大きすぎます。 | 受信要求のサイズが大きすぎました。 |
| 429 | **コード**: `Throttled` <br/> **メッセージ**: 要求が多すぎます。 後で再試行する場合も返します。 | ボットから送信された要求が多すぎます。 詳細については、「レート制限 [」を参照してください](~/bots/how-to/rate-limit.md)。 |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|-----------|
| Teams 会話ボット | メッセージングおよび会話イベントの処理。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ボット コマンド メニュー](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>関連項目

* [プロアクティブ メッセージを送信する](~/bots/how-to/conversations/send-proactive-messages.md)
* [会話イベントにサブスクライブする](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [ボットを介してファイルを送受信する](~/bots/how-to/bots-filesv4.md)
* [ボットの要求ヘッダーにテナント ID と会話 ID を送信する](~/bots/how-to/conversations/request-headers-of-the-bot.md)
