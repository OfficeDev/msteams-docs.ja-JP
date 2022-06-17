---
title: ボットの会話内のメッセージ
description: コード サンプルを使用して、Teams ボットとTeams チャネル データ、メッセージへの通知、画像メッセージ、アダプティブ カードとの会話を行う方法について説明します
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 7e71e6ce6c70967de9c9f086251772df8d758f4a
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142452"
---
# <a name="messages-in-bot-conversations"></a>ボットの会話内のメッセージ

会話内の各メッセージは、型`messageType: message`の`Activity`オブジェクトです。 ユーザーがメッセージを送信すると、Teamsメッセージがボットに投稿されます。 Teamsボットのメッセージング エンドポイントに JSON オブジェクトを送信します。 ボットはメッセージを調べて種類を判別し、種類に応じて応答します。

基本的な会話は、Bot Framework コネクタ (単一の REST API) を介して処理されます。 この API を使用すると、ボットはTeamsやその他のチャネルと通信できます。 Bot Builder SDK には、次の機能が用意されています。

* Bot Framework コネクタに簡単にアクセスできます。
* 会話のフローと状態を管理するための追加機能。
* 自然言語処理 (NLP) などのコグニティブ サービスを組み込む簡単な方法。

ボットは、プロパティを使用してTeamsからメッセージを`Text`受信し、1 つまたは複数のメッセージ応答をユーザーに送信します。

詳細については、「[ボット メッセージのユーザー属性」を](/microsoftteams/platform/messaging-extensions/how-to/action-commands/respond-to-task-module-submit?tabs=dotnet%2Cdotnet-1&branch=pr-en-us-5926#user-attribution-for-bots-messages)参照してください。

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

テキスト メッセージを送信するには、送信する文字列をアクティビティとして指定します。 ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `SendActivityAsync` メソッドを使用して、1 つのメッセージ応答を送信します。 オブジェクトの `SendActivitiesAsync` メソッドを使用して、一度に複数の応答を送信します。

次のコードは、ユーザーが会話に追加されたときにメッセージを送信する例を示しています。

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
> メッセージ分割は、テキスト メッセージと添付ファイルが同じアクティビティ ペイロードで送信されるときに発生します。 このアクティビティは、Microsoft Teams別に別のアクティビティに分割されます。1 つはテキスト メッセージ、もう 1 つは添付ファイルを含みます。 アクティビティが分割されると、メッセージ ID は応答で受け取りません。これは、メッセージをプロアクティブに [更新または削除](~/bots/how-to/update-and-delete-bot-messages.md) するために使用されます。 メッセージ分割に応じて、別のアクティビティを送信することをお勧めします。

ユーザーとボットの間で送信されるメッセージには、メッセージ内の内部チャネル データが含まれます。 このデータを使用すると、ボットはそのチャネルで適切に通信できます。 Bot Builder SDK を使用すると、メッセージ構造を変更できます。

## <a name="teams-channel-data"></a>Teamsチャネルデータ

オブジェクトには`channelData`Teams固有の情報が含まれており、チーム ID とチャネル ID の決定的なソースです。 必要に応じて、これらの ID をキャッシュし、ローカル ストレージのキーとして使用できます。 `TeamsActivityHandler` SDK では、オブジェクトから重要な情報を`channelData`取り出して、簡単にアクセスできるようにします。 ただし、オブジェクトから `turnContext` 元のデータにいつでもアクセスできます。

オブジェクトは `channelData` 、チャネルの外部で行われるので、個人の会話のメッセージには含まれません。

ボットに送信されるアクティビティの一般的な `channelData` オブジェクトには、次の情報が含まれています。

* `eventType`: [チャネル変更](~/bots/how-to/conversations/subscribe-to-conversation-events.md)イベントの場合にのみ渡されるイベントの種類をTeamsします。
* `tenant.id`: すべてのコンテキストで渡されるMicrosoft Azure Active Directory (Azure AD) テナント ID。
* `team`: 個人用チャットではなく、チャネル コンテキストでのみ渡されます。
  * `id`: チャネルの GUID。
  * `name`: チーム名の [変更イベント](subscribe-to-conversation-events.md#team-renamed)の場合にのみ渡されたチームの名前。
* `channel`: チャネル コンテキストでのみ渡されます。ボットが言及されたとき、またはボットが追加されたチーム内のチャネル内のイベントに対してのみ渡されます。
  * `id`: チャネルの GUID。
  * `name`: チャネル [変更イベント](~/bots/how-to/conversations/subscribe-to-conversation-events.md)の場合にのみ渡されるチャネル名。
* `channelData.teamsTeamId`: 非推奨です。 このプロパティは、下位互換性のためにのみ含まれます。
* `channelData.teamsChannelId`: 非推奨です。 このプロパティは、下位互換性のためにのみ含まれます。

### <a name="example-channeldata-object-channelcreated-event"></a>channelData オブジェクトの例 (channelCreated イベント)

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

## <a name="message-content"></a>メッセージの内容

ボットとの間で送受信されるメッセージには、さまざまな種類のメッセージ コンテンツを含めることができます。

| フォーマット    | ユーザーからボットへ | ボットからユーザーへ | メモ                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| リッチ テキスト | ✔️                | ✔️                | ボットは、リッチ テキスト、画像、カードを送信できます。 ユーザーは、リッチ テキストと画像をボットに送信できます。                                                                                        |
| ピクチャ  | ✔️                | ✔️                | 最大 1024 ×1024 MB、PNG、JPEG、または GIF 形式で 1 MB。 アニメーション GIF はサポートされていません。  |
| カード     | ❌                | ✔️                | サポートされているカードについては、[Teams カードリファレンスを参照](~/task-modules-and-cards/cards/cards-reference.md)してください。 |
| 絵文字    | ✔️                | ✔️                | Teamsは現在、顔を笑う U+1F600 など、UTF-16 を介した絵文字をサポートしています。 |

## <a name="notifications-to-your-message"></a>メッセージへの通知

このプロパティを使用して、メッセージに通知を `Notification.Alert` 追加することもできます。 通知は、新しいタスク、メンション、コメントについてユーザーに通知します。 これらのアラートは、ユーザーが作業している内容や、アクティビティ フィードに通知を挿入して確認する必要がある内容に関連します。 ボット メッセージから通知をトリガーするには、objects `Notification.Alert` プロパティを `TeamsChannelData` true に設定 *します*。 通知が発生するかどうかは、個々のユーザーのTeams設定によって異なり、これらの設定をオーバーライドすることはできません。 通知の種類はバナーか、バナーとメールの両方です。

> [!NOTE]
> [ **概要]** フィールドには、フィード内の通知メッセージとしてユーザーからのテキストが表示されます。

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

メッセージを強化するために、そのメッセージの添付ファイルとして画像を含めることができます。

## <a name="picture-messages"></a>画像メッセージ

画像は、メッセージに添付ファイルを追加して送信されます。 添付ファイルの詳細については、「 [メッセージにメディア添付ファイルを追加する」を](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)参照してください。

画像は最大 1024 ×1024 MB、PNG、JPEG、または GIF 形式で 1 MB です。 アニメーション GIF はサポートされていません。

XML を使用して、各イメージの高さと幅を指定します。 マークダウンでは、イメージ サイズの既定値は 256×256 です。 以下に例を示します。

* 使用: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.
* 使用しないでください: `![Duck on a rock](http://aka.ms/Fo983c)`.

会話型ボットには、ビジネス ワークフローを簡略化するアダプティブ カードを含めることができます。 アダプティブ カードは、豊富なカスタマイズ可能なテキスト、音声、画像、ボタン、入力フィールドを提供します。

## <a name="adaptive-cards"></a>アダプティブ カード

アダプティブ カードはボットで作成し、Teams、Web サイトなどの複数のアプリで表示できます。 詳細については「[アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)」を参照してください。

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

### <a name="form-completion-feedback"></a>フォームの完了に関するフィードバック

フォーム入力候補メッセージは、ボットに応答を送信するときにアダプティブ カードに表示されます。 メッセージには、エラーと成功の 2 種類があります。

* **エラー**: ボットに送信された応答が失敗すると、 **問題が発生しました。もう一度やり直してください** というメッセージが表示されます。

     :::image type="content" source="../../../assets/images/Cards/error-message.png" alt-text="エラー メッセージ"border="true":::

* **成功**: ボットに送信された応答が成功すると、 **アプリに送信された応答** メッセージが表示されます。

     :::image type="content" source="../../../assets/images/Cards/success.PNG" alt-text="成功メッセージ"border="true":::

     [ **閉じる** ] または [チャットの切り替え] を選択して、メッセージを閉じます。

     成功メッセージを表示しない場合は、プロパティで`msTeams``feedback`属性`hide`を`true`設定します。 次に例を示します。

     ```json
        "content": {
            "type": "AdaptiveCard",
            "title": "Card with hidden footer messages",
            "version": "1.0",
            "actions": [
            {
                "type": "Action.Submit",
                "title": "Submit",
                "msTeams": {
                    "feedback": {
                    "hide": true
                    }
                }
            }
            ]
        } 
     ```

ボット内のカードとカードの詳細については、カードの [ドキュメントを参照してください](~/task-modules-and-cards/what-are-cards.md)。

## <a name="status-code-responses"></a>状態コードの応答

状態コードとそのエラー コードとメッセージ値を次に示します。

| 状態コード | エラー コードとメッセージの値 | 説明 |
|----------------|-----------------|-----------------|
| 403 | **コード**: `ConversationBlockedByUser` <br/> **メッセージ**: ユーザーがボットとの会話をブロックしました。 | ユーザーは、モデレーション設定を使用して、1:1 チャットまたはチャネルでボットをブロックしました。 |
| 403 | **コード**: `BotNotInConversationRoster` <br/> **メッセージ**: ボットは会話名簿の一部ではありません。 | ボットは会話の一部ではありません。 |
| 403 | **コード**: `BotDisabledByAdmin` <br/> **メッセージ**: テナント管理者がこのボットを無効にしました。 | テナントがボットをブロックしました。 |
| 401 | **コード**: `BotNotRegistered` <br/> **メッセージ**: このボットの登録が見つかりません。 | このボットの登録が見つかりませんでした。 |
| 412 | **コード**: `PreconditionFailed` <br/> **メッセージ**: 前提条件に失敗しました。もう一度やり直してください。 | 同じ会話に対する複数の同時操作が原因で、依存関係の 1 つに前提条件が失敗しました。 |
| 404 | **コード**: `ConversationNotFound` <br/> **メッセージ**: 会話が見つかりません。 | 会話が見つかりませんでした。 |
| 413 | **コード**: `MessageSizeTooBig` <br/> **メッセージ**: メッセージ サイズが大きすぎます。 | 受信要求のサイズが大きすぎます。 |
| 429 | **コード**: `Throttled` <br/> **メッセージ**: 要求が多すぎます。 後で再試行するタイミングも返されます。 | ボットから送信された要求が多すぎます。 詳細については、 [レート制限](~/bots/how-to/rate-limit.md)に関するページを参照してください。 |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|-----------|
| Teams 会話ボット | メッセージングと会話イベントの処理。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Bot コマンド メニュー](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>関連項目

* [プロアクティブ メッセージを送信する](~/bots/how-to/conversations/send-proactive-messages.md)
* [会話イベントにサブスクライブする](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [ボットを介してファイルを送受信する方法](~/bots/how-to/bots-filesv4.md)
* [ボットの要求ヘッダーにテナント ID と会話 ID を送信する](~/bots/how-to/conversations/request-headers-of-the-bot.md)
