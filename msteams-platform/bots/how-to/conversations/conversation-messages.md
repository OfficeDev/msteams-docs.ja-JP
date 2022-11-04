---
title: ボットの会話内のメッセージ
description: メッセージ、推奨されるアクション、通知、添付ファイル、画像、アダプティブ カード、状態エラー コードの応答を受信する方法について説明します。
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 16849a9e8ed97854e91934aef9de463eb355fec5
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833206"
---
# <a name="messages-in-bot-conversations"></a>ボットの会話内のメッセージ

会話内の各メッセージは、 `Activity` 型のオブジェクトです `messageType: message`。 ユーザーがメッセージを送信すると、Microsoft Teams によってボットにメッセージが投稿されます。 Teams は JSON オブジェクトをボットのメッセージング エンドポイントに送信し、Teams ではメッセージング用のエンドポイントを 1 つだけ許可します。 ボットはメッセージを調べて種類を判別し、種類に応じて応答します。

基本的な会話は、1 つの REST API である Bot Framework コネクタを介して処理されます。 この API を使用すると、ボットは Teams やその他のチャネルと通信できます。 Bot Builder SDK には、次の機能があります。

* Bot Framework コネクタに簡単にアクセスできます。
* 会話フローと状態を管理する機能。
* 自然言語処理 (NLP) などのコグニティブ サービスを組み込む簡単な方法。

ボットは、 プロパティを使用して Teams からメッセージを `Text` 受信し、1 つまたは複数のメッセージ応答をユーザーに送信します。

詳細については、「 [ボット メッセージのユーザー属性」を](/microsoftteams/platform/messaging-extensions/how-to/action-commands/respond-to-task-module-submit?tabs=dotnet%2Cdotnet-1&branch=pr-en-us-5926#user-attribution-for-bots-messages)参照してください。

## <a name="receive-a-message"></a>メッセージを受信する

テキスト メッセージを受信するには、オブジェクトの `Text` プロパティを `Activity` 使用します。 ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `Activity` を使用して、1 つのメッセージ要求を読み取ります。

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

テキスト メッセージを送信するには、アクティビティとして送信する文字列を指定します。 ボットのアクティビティ ハンドラーで、ターン コンテキスト オブジェクトの `SendActivityAsync` メソッドを使用して、1 つのメッセージ応答を送信します。 オブジェクトのメソッドを使用して、複数の `SendActivitiesAsync` 応答を送信します。

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
>
>* メッセージ分割は、テキスト メッセージと添付ファイルが同じアクティビティ ペイロードで送信されるときに発生します。 Teams では、このアクティビティを 2 つの別々のアクティビティに分割します。1 つはテキスト メッセージで、もう 1 つは添付ファイルを含みます。 アクティビティが分割されると、応答としてメッセージ ID は受信されません。これは、メッセージを事前に [更新または削除](~/bots/how-to/update-and-delete-bot-messages.md) するために使用されます。 メッセージ分割に応じてではなく、個別のアクティビティを送信することをお勧めします。
>* 送信されたメッセージは、パーソナル化を提供するためにローカライズできます。 詳細については、「 [アプリのローカライズ](../../../concepts/build-and-test/apps-localization.md)」を参照してください。

ユーザーとボットの間で送信されるメッセージには、メッセージ内の内部チャネル データが含まれます。 このデータを使用すると、ボットはそのチャネルで適切に通信できます。 Bot Builder SDK を使用すると、メッセージ構造を変更できます。

## <a name="send-suggested-actions"></a>推奨されるアクションを送信する

推奨されるアクションを使用すると、ボットは、ユーザーが入力を提供するために選択できるボタンを表示できます。 推奨されるアクションは、ユーザーがキーボードで応答を入力するのではなく、質問に回答したり、ボタンを選択したりできるようにすることで、ユーザー エクスペリエンスを向上させます。
ユーザーがボタンを選択すると、リッチ カードでは表示され、アクセス可能なままになりますが、推奨されるアクションにはアクセスできません。 これにより、ユーザーが会話内の古いボタンを選択できなくなります。

推奨されるアクションをメッセージに追加するには、[アクティビティ](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference) オブジェクトの プロパティを`suggestedActions`設定して、ユーザーに表示するボタンを表す[カード アクション](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference) オブジェクトの一覧を指定します。 詳細については、[`sugestedActions`](/dotnet/api/microsoft.bot.builder.messagefactory.suggestedactions) を参照してください。

推奨されるアクションの実装とエクスペリエンスの例を次に示します。

``` json
"suggestedActions": {
    "actions": [
      {
        "type": "imBack",
        "title": "Action 1",
        "value": "Action 1"
      },
      {
        "type": "imBack",
        "title": "Action 2",
        "value": "Action 2"
      }
    ],
    "to": [<list of recepientIds>]
  }
```

次に、推奨されるアクションの例を示します。

:::image type="content" source="~/assets/images/Cards/suggested-actions.png" alt-text="ボットが推奨するアクション" border="true":::

> [!NOTE]
>
> * `SuggestedActions` は、1 対 1 のチャット ボットとテキスト ベースのメッセージでのみサポートされ、アダプティブ カードや添付ファイルではサポートされません。
> * `imBack` はサポートされている唯一のアクションの種類であり、Teams には最大 3 つの推奨アクションが表示されます。

## <a name="teams-channel-data"></a>Teamsチャネルデータ

オブジェクトには `channelData` Teams 固有の情報が含まれており、チーム ID とチャネル ID の決定的なソースです。 必要に応じて、これらの ID をキャッシュし、ローカル ストレージのキーとして使用できます。 SDK の は `TeamsActivityHandler` 、オブジェクトから重要な情報を `channelData` 取り出してアクセスできるようにします。 ただし、オブジェクトから `turnContext` 元のデータにいつでもアクセスできます。

オブジェクトは `channelData` 、チャネルの外部で行われるので、個人的な会話のメッセージには含まれません。

ボットに送信されるアクティビティの一般的な `channelData` オブジェクトには、次の情報が含まれています。

* `eventType`: [チャネル変更](~/bots/how-to/conversations/subscribe-to-conversation-events.md)イベントの場合にのみ、Teams イベントの種類が渡されます。
* `tenant.id`: すべてのコンテキストで渡されたMicrosoft Azure Active Directory (Azure AD) テナント ID。
* `team`: 個人用チャットではなく、チャネル コンテキストでのみ渡されます。
  * `id`: チャネルの GUID。
  * `name`: チーム名が [イベントの名前変更](subscribe-to-conversation-events.md#team-renamed)の場合にのみ渡されたチームの名前。
* `channel`: ボットがメンションされたとき、またはボットが追加されたチームのチャネルのイベントに対してのみ、チャネル コンテキストで渡されます。
  * `id`: チャネルの GUID。
  * `name`: チャネル [変更イベント](~/bots/how-to/conversations/subscribe-to-conversation-events.md)の場合にのみ渡されるチャネル名。
* `channelData.teamsTeamId`：廃止。 このプロパティは、下位互換性のためにのみ含まれています。
* `channelData.teamsChannelId`：廃止。 このプロパティは、下位互換性のためにのみ含まれています。

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

ボットから受信またはボットに送信されるメッセージには、さまざまな種類のメッセージ コンテンツを含めることができます。

| フォーマット    | ユーザーからボットへ | ボットからユーザーへ | メモ                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| リッチ テキスト | ✔️                | ✔️                | ボットは、リッチ テキスト、画像、カードを送信できます。 ユーザーは、リッチ テキストと画像をボットに送信できます。                                                                                        |
| ピクチャ  | ✔️                | ✔️                | 最大 1024 × 1024 ピクセル、PNG、JPEG、GIF 形式で 1 MB。 アニメーション GIF はサポートされていません。 |
| カード     | ❌                | ✔️                | サポートされているカードについては、「 [Teams カードリファレンス」を参照](~/task-modules-and-cards/cards/cards-reference.md) してください。 |
| 絵文字    | ✔️                | ✔️                | Teams では現在、顔を笑う U+1F600 など、UTF-16 を介した絵文字がサポートされています。 |

### <a name="picture-messages"></a>画像メッセージ

メッセージを強化するために、そのメッセージの添付ファイルとして画像を含めることができます。 添付ファイルの詳細については、「メッセージに [メディア添付ファイルを追加する」を](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)参照してください。

画像は、最大 1024 × 1024 ピクセル、PNG、JPEG、GIF 形式で 1 MB にすることができます。 アニメーション GIF はサポートされていません。

XML を使用して、各イメージの高さと幅を指定します。 Markdown では、イメージ サイズの既定値は 256×256 です。 以下に例を示します。

* 使用: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`。
* を使用しないでください。 `![Duck on a rock](http://aka.ms/Fo983c)`

会話型ボットには、ビジネス ワークフローを簡略化するアダプティブ カードを含めることができます。 アダプティブ カードは、カスタマイズ可能な豊富なテキスト、音声、画像、ボタン、入力フィールドを提供します。

### <a name="adaptive-cards"></a>アダプティブ カード

アダプティブ カードはボットで作成し、Teams や Web サイトなどの複数のアプリに表示できます。 詳細については「[アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)」を参照してください。

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

#### <a name="form-completion-feedback"></a>フォームの完了に関するフィードバック

アダプティブ カードを使用してフォーム入力候補のフィードバックを作成できます。 ボットへの応答の送信中に、アダプティブ カードにフォーム入力候補メッセージが表示されます。 メッセージには、エラーまたは成功の 2 種類があります。

* **エラー**: ボットに送信された応答が失敗すると、 **問題が発生し、[再試行]** というメッセージが表示されます。

     :::image type="content" source="../../../assets/images/Cards/error-message.png" alt-text="エラー メッセージ"border="true":::

* **成功**: ボットに送信された応答が成功すると、 **アプリ に送信された応答** メッセージが表示されます。

     :::image type="content" source="../../../assets/images/Cards/success.PNG" alt-text="成功メッセージ"border="true":::

     [ **閉じる** ] を選択するか、チャットを切り替えてメッセージを無視できます。

     成功メッセージを表示しない場合は、 プロパティで `msTeams` `feedback` 属性`hide`を に`true`設定します。 次に例を示します。

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

ボットのカードとカードの詳細については、 [カードのドキュメントを参照してください](~/task-modules-and-cards/what-are-cards.md)。

## <a name="add-notifications-to-your-message"></a>メッセージに通知を追加する

アプリケーションから通知を送信するには、次の 2 つの方法があります。

* ボット メッセージで プロパティを `Notification.Alert` 設定します。
* Graph APIを使用してアクティビティ フィード通知を送信する。

プロパティを使用して、メッセージに通知を `Notification.Alert` 追加できます。 通知は、新しいタスク、メンション、コメントなど、アプリケーション内のイベントに対してユーザーに警告します。 これらのアラートは、ユーザーが作業している内容や、アクティビティ フィードに通知を挿入して確認する必要がある内容に関連しています。 ボット メッセージからトリガーする通知の場合は、objects `Notification.Alert` プロパティを `TeamsChannelData` true に設定 *します*。 通知が発生する場合は、個々のユーザーの Teams 設定に依存し、これらの設定をオーバーライドすることはできません。

ユーザーにメッセージを送信せずに任意の通知を生成する場合は、Graph APIを使用できます。 詳細については、[Graph APIとベスト プラクティス](/graph/teams-activity-feed-notifications-best-practices)[を使用してアクティビティ フィード通知を送信する方法](/graph/teams-send-activityfeednotifications)に関するページを参照してください。

> [!NOTE]
> [ **概要** ] フィールドには、フィード内の通知メッセージとしてユーザーからのテキストが表示されます。

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

## <a name="status-codes-from-bot-conversational-apis"></a>ボットの会話型 API からの状態コード

Teams アプリでこれらのエラーを適切に処理してください。 次の表に、エラー コードと、エラーが生成される説明を示します。

| 状態コード | エラー コードとメッセージ値 | 説明 | 再試行要求 | 開発者アクション |
|----------------|-----------------|-----------------|----------------|----------------|
| 400 | **コード**: `Bad Argument` <br/> **メッセージ**: *シナリオ固有 | ボットによって提供される要求ペイロードが無効です。 詳細については、「エラー メッセージ」を参照してください。 | いいえ | エラーの要求ペイロードを再評価します。 詳細については、返されたエラー メッセージを確認してください。 |
| 401 | **コード**: `BotNotRegistered` <br/> **メッセージ**: このボットの登録が見つかりません。 | このボットの登録が見つかりませんでした。 | いいえ | ボット ID とパスワードを確認します。 ボット ID (AAD ID) が Teams 開発者ポータルに登録されているか、Azure の Azure ボット チャネル登録を介して "Teams" チャネルが有効になっていることを確認します。|
| 403 | **コード**: `BotDisabledByAdmin` <br/> **メッセージ**: テナント管理者がこのボットを無効にしました | テナント管理者は、ユーザーとボット アプリ間の相互作用をブロックしました。 テナント管理者は、アプリ ポリシー内のユーザーのアプリを許可する必要があります。 詳細については、「 [アプリ ポリシー](/microsoftteams/app-policies)」を参照してください。 | いいえ | ボットとの対話が、ボットがブロックされなくなったことを示す会話内のユーザーによって明示的に開始されるまで、会話への投稿を停止します。 |
| 403 | **コード**: `BotNotInConversationRoster` <br/> **メッセージ**: ボットは会話名簿の一部ではありません。 | ボットは会話の一部ではありません。 会話でアプリを再インストールする必要があります。 | いいえ | 別の会話要求を送信する前に、ボットが再追加されたことを示すイベントを待 [`installationUpdate`](~/bots/how-to/conversations/subscribe-to-conversation-events.md#install-update-event) ちます。|
| 403 | **コード**: `ConversationBlockedByUser` <br/> **メッセージ**: ユーザーはボットとの会話をブロックしました。 | ユーザーは、モデレート設定を使用して、個人用チャットまたはチャネルでボットをブロックしました。 | いいえ | キャッシュから会話を削除します。 ボットとの対話が会話内のユーザーによって明示的に開始され、ボットがブロックされなくなったことを示すまで、会話への投稿を停止します。 |
| 403 |**コード**: `InvalidBotApiHost` <br/> **メッセージ**: ボット API ホストが無効です。 GCC テナントの場合は、 を呼び出 `https://smba.infra.gcc.teams.microsoft.com`してください。|GCC テナントに属する会話のパブリック API エンドポイントと呼ばれるボット。| いいえ | 会話のサービス URL を に `https://smba.infra.gcc.teams.microsoft.com` 更新し、要求を再試行します。|
| 403 | **コード**: `NotEnoughPermissions` <br/> **メッセージ**: *シナリオ固有 | ボットには、要求されたアクションを実行するための必要なアクセス許可がありません。 | いいえ | エラー メッセージから必要なアクションを決定します。 |
| 404 | **コード**: `ActivityNotFoundInConversation` <br/> **メッセージ**: 会話が見つかりません。 | 指定されたメッセージ ID が会話で見つかりませんでした。 メッセージが存在しないか、削除されています。 | いいえ | 送信されるメッセージ ID が予期される値であるかどうかを確認します。 キャッシュされた場合は、ID を削除します。 |
| 404 | **コード**: `ConversationNotFound` <br/> **メッセージ**: 会話が見つかりません。 | 会話が存在しないか削除されているため、見つかりませんでした。 | いいえ | 送信された会話 ID が予期される値であるかどうかを確認します。 キャッシュされた場合は、ID を削除します。 |
| 412 | **コード**: `PreconditionFailed` <br/> **メッセージ**: 前提条件に失敗しました。もう一度お試しください。 | 同じ会話に対する複数の同時実行操作が原因で、いずれかの依存関係で前提条件が失敗しました。 | はい | 指数バックオフを使用して再試行します。 |
| 413 | **コード**: `MessageSizeTooBig` <br/> **メッセージ**: メッセージ サイズが大きすぎます。 | 受信要求のサイズが大きすぎます。 詳細については、「 [ボット メッセージの書式設定](/microsoftteams/platform/bots/how-to/format-your-bot-messages)」を参照してください。 | いいえ | ペイロード サイズを小さくします。 |
| 429 | **コード**: `Throttled` <br/> **メッセージ**: 要求が多すぎます。 また、後で再試行するタイミングも返します。 | ボットから送信された要求が多すぎます。 詳細については、「 [レート制限](/microsoftteams/platform/bots/how-to/rate-limit)」を参照してください。 | はい | ヘッダーを使用して `Retry-After` バックオフ時間を確認して再試行します。 |
| 500 | **コード**: `ServiceError` <br/> **メッセージ**: *各種 | 内部サーバー エラー。 | いいえ | [開発者コミュニティ](~/feedback.md#developer-community-help)で問題を報告します。 |
| 502 | **コード**: `ServiceError` <br/> **メッセージ**: *各種 | サービス依存関係の問題。 | はい | 指数バックオフを使用して再試行します。 問題が解決しない場合は、 [開発者コミュニティ](~/feedback.md#developer-community-help)で問題を報告してください。 |
| 503 | | サービスは使用できません。 | はい | 指数バックオフを使用して再試行します。 問題が解決しない場合は、 [開発者コミュニティ](~/feedback.md#developer-community-help)で問題を報告してください。 |
| 504 | | ゲートウェイのタイムアウト。 | はい | 指数バックオフを使用して再試行します。 問題が解決しない場合は、 [開発者コミュニティ](~/feedback.md#developer-community-help)で問題を報告してください。 |

### <a name="status-codes-retry-guidance"></a>状態コードの再試行ガイダンス

各状態コードの一般的な再試行ガイダンスを次の表に示します。ボットは、指定されていない状態コードの再試行を避ける必要があります。

|状態コード | 再試行戦略 |
|----------------|-----------------|
| 403 | の `InvalidBotApiHost`GCC API `https://smba.infra.gcc.teams.microsoft.com` を呼び出して再試行します。|
| 412 | 指数バックオフを使用して再試行します。 |
| 429 | ヘッダーを使用して再試行して `Retry-After` 、要求の間の待機時間 (使用可能な場合) を秒単位で判断します。 それ以外の場合は、可能であれば、スレッド ID を使用して指数バックオフを使用して再試行してください。 |
| 502 | 指数バックオフを使用して再試行します。 |
| 503 | 指数バックオフを使用して再試行します。 |
| 504 | 指数バックオフを使用して再試行します。 |

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | Node.js | .NETCore | Python | .NET |
|----------------|-----------------|--------------|----------------|-----------|-----|
| Teams 会話ボット | メッセージングと会話イベントの処理。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) | 該当なし |
| Teams アプリのローカライズ | ボットとタブを使用した Teams アプリのローカライズ。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) | 該当なし | 該当なし | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Bot コマンド メニュー](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>関連項目

* [プロアクティブ メッセージを送信する](~/bots/how-to/conversations/send-proactive-messages.md)
* [会話イベントにサブスクライブする](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [ボットを介してファイルを送受信する方法](~/bots/how-to/bots-filesv4.md)
* [ボットの要求ヘッダーにテナント ID と会話 ID を送信する](~/bots/how-to/conversations/request-headers-of-the-bot.md)
* [アプリをローカライズする](../../../concepts/build-and-test/apps-localization.md)
