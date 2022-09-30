---
title: メッセージ拡張機能を使用した操作の開始
description: このモジュールでは、ユーザーが外部サービスをトリガーできるようにアクション ベースのメッセージ拡張機能を作成する方法について説明します
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: e72d4c5d7ca7ecaa0ced14f28cc321d0a93a19c3
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243571"
---
# <a name="initiate-actions-with-message-extensions"></a>メッセージ拡張機能を使用した操作の開始

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

アクション ベースのメッセージ拡張機能を使用すると、ユーザーは Teams 内で外部サービスでアクションをトリガーできます。

![メッセージ拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

次のセクションでは、これを行う方法について説明します。

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

## <a name="action-type-message-extensions"></a>アクションの種類のメッセージ拡張機能

メッセージ拡張機能からアクションを開始するには、パラメーター`action`を `type` . 検索と作成コマンドを含むマニフェストの例を次に示します。 1 つのメッセージ拡張機能には、最大 10 個の異なるコマンドを含めることができます。 これには、複数の検索コマンドと複数のアクション ベースのコマンドの両方を含めることができます。

 > [!NOTE]
 >`justInTimeInstall` は、アプリカタログにアプリをアップロードするときに機能しますが、アプリをサイドロードすると失敗します。

### <a name="complete-app-manifest-example"></a>完全なアプリ マニフェストの例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": false,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
              "inputType": "text"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

### <a name="initiate-actions-from-messages"></a>メッセージからアクションを開始する

メッセージ作成領域からアクションを開始するだけでなく、メッセージ拡張機能を使用してメッセージからアクションを開始することもできます。 これにより、処理のためにメッセージの内容をボットに送信し、必要に応じて、送信する応答に関するページで説明されているメソッドを使用して応答でそのメッセージ [に返信できます](#responding-to-submit)。 応答は、送信する前にユーザーが編集できるメッセージへの応答として挿入されます。 ユーザーはオーバーフロー `...` メニューからメッセージ拡張機能にアクセスし、次の図のように選択 `Take action` できます。

![メッセージからアクションを開始する例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

メッセージ拡張機能をメッセージから機能させるには、次の `context` 例のように、アプリ マニフェストでメッセージ拡張機能の `commands` オブジェクトにパラメーターを追加します。 配列の `context` 有効な文字列は `"message"`、、 `"commandBox"`、および `"compose"`. 既定値は `["compose", "commandBox"]` です。 パラメーターの詳細については、「 [コマンドの定義](#define-commands) 」セクションを `context` 参照してください。

```json
"composeExtensions": [
  {
    "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Create To Do",
        "type": "Action",
        "context": ["message"],
        "fetchTask": true
    }]
    ...

```

ボットに `value` 送信される要求の一部として送信されるメッセージの詳細を含むオブジェクトの `composeExtension` 例を次に示します。

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "this is the message"
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

### <a name="test-via-uploading"></a>アップロードによるテスト

アプリをアップロードすることで、メッセージ拡張機能をテストできます。 詳細については、「 [チームでのアプリのアップロード](~/concepts/deploy-and-publish/apps-upload.md)」を参照してください。

メッセージ拡張機能を開くには、任意のチャットまたはチャネルに移動します。 作成ボックスの **[その他のオプション** (**&#8943;**)] ボタンを選択し、メッセージ拡張機能を選択します。

## <a name="collecting-input-from-users"></a>ユーザーからの入力の収集

Teams のエンド ユーザーから情報を収集するには、3 つの方法があります。

### <a name="static-parameter-list"></a>静的パラメーターの一覧

このメソッドでは、"Create To Do" コマンドで上に示したように、マニフェスト内のパラメーターの静的なリストを定義するだけです。 このメソッドを使用するには、マニフェストでパラメーターが設定`false`されていることと、パラメーターを定義していることを確認`fetchTask`します。

ユーザーが静的パラメーターを持つコマンドを選択すると、Teams はマニフェストに定義されたパラメーターを含むフォームをタスク モジュールに生成します。 [送信] をクリックすると、a `composeExtension/submitAction` がボットに送信されます。 予想される応答のセットの詳細については、「 [送信への応答」を](#responding-to-submit)参照してください。

### <a name="dynamic-input-using-an-adaptive-card"></a>アダプティブ カードを使用した動的入力

この方法では、ユーザー入力を収集するカスタム アダプティブ カードをサービスで定義できます。 この方法では、マニフェストでパラメーターを`fetchTask``true`設定します。 設定した場合、 `fetchTask` コマンドに対して `true` 定義されているすべての静的パラメーターは無視されます。

このメソッドでは、サービスがイベントを `composeExtension/fetchTask` 受信し、アダプティブ カード ベースの [タスク モジュール応答で応答します](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。 アダプティブ カードを使用した応答の例を次に示します。

```json
{
    "task": {
        "type": "continue",
        "value": {
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": {
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Please enter the following information:"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Name"
                        },
                        {
                            "type": "Input.Text",
                            "spacing": "None",
                            "title": "New Input.Toggle",
                            "placeholder": "Placeholder text"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Date of birth"
                        },
                        {
                            "type": "Input.Date",
                            "spacing": "None",
                            "title": "New Input.Toggle"
                        }
                    ],
                    "type": "AdaptiveCard",
                    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                    "version": "1.0"
                }
            }
        }
    }
}
```

また、ユーザーがユーザー入力を取得する前に拡張機能を認証または構成する必要がある場合は、ボットは認証/構成応答で応答することもできます。

### <a name="dynamic-input-using-a-web-view"></a>Web ビューを使用した動的入力

このメソッドでは、サービスはベース ウィジェットを `<iframe>` 表示してカスタム UI を表示し、ユーザー入力を収集できます。 この方法では、マニフェストでパラメーターを`fetchTask``true`設定します。

アダプティブ カード フローと同様に、サービスはイベントを `fetchTask` 送信し、URL ベースの [タスク モジュール応答で応答します](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。 アダプティブ カードを使用した応答の例を次に示します。

```json
{
    "task": {
        "value": {
            "url": "http://mywebapp.com/input"
        },
        "type": "continue"
    }
}
```

### <a name="request-to-install-your-conversational-bot"></a>会話型ボットのインストールを要求する

アプリに会話ボットが含まれている場合は、タスク モジュールを読み込む前に、会話にインストールされていることを確認します。 これは、タスク モジュールの追加コンテキストを取得する必要がある場合に役立ちます。 たとえば、ユーザー選択コントロールを設定するために名簿をフェッチする必要がある場合や、チーム内のチャネルの一覧を取得する必要がある場合があります。

このフローを容易にするために、メッセージ拡張機能が最初に呼び出しを `composeExtension/fetchTask` 受け取ったときに、ボットが現在のコンテキストにインストールされているかどうかを確認します。 これを取得するには、名簿の取得呼び出しを試みます。 たとえば、ボットがインストールされていない場合は、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します。 ユーザーには、その場所にアプリをインストールするためのアクセス許可が必要です。 インストールできない場合は、管理者に問い合わせるメッセージが表示されます。

応答の例を次に示します。

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

ユーザーがインストールを完了すると、ボットは別の呼び出しメッセージ ( `name = composeExtension/submitAction`および `value.data.msteams.justInTimeInstall = true`.

呼び出しの例を次に示します。

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

ボットが既にインストールされている場合と同じタスク応答で呼び出しに応答します。

## <a name="responding-to-submit"></a>送信への応答

ユーザーが入力を完了すると、ボットはコマンド ID とパラメーター値が設定されたイベントを受け取ります `composeExtension/submitAction` 。

これらは、次に示す異なる予想される応答です `submitAction`。

### <a name="task-module-response"></a>タスク モジュールの応答

これは、拡張機能がダイアログを連結して詳細情報を取得する必要がある場合に使用されます。 応答は、前に説明したものとまったく同じです `fetchTask` 。

### <a name="compose-extension-authconfig-response"></a>拡張機能の認証/構成応答を作成する

これは、拡張機能を認証するか、続行するように構成する必要がある場合に使用されます。 詳細については、検索 [セクションの「認証」セクション](~/resources/messaging-extension-v3/search-extensions.md#authentication) を参照してください。

### <a name="compose-extension-result-response"></a>拡張機能の結果応答を作成する

これは、コマンドの結果として作成ボックスにカードを挿入するために使用されます。 検索コマンドで使用されるのと同じ応答ですが、配列内の 1 つのカードまたは 1 つの結果に制限されます。

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        },
    "attachments": [
      {  
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>ボットから送信されたアダプティブ カード メッセージで応答する

送信アクションに応答するには、アダプティブ カードを含むメッセージをボットを使用してチャネルに挿入します。 ユーザーはメッセージを送信する前にプレビューし、メッセージを編集/操作することもできます。 これは、アダプティブ カード応答を作成する前にユーザーから情報を収集する必要があるシナリオで役立ちます。 次のシナリオでは、このフローを使用して、チャネル メッセージに構成手順を含めずにポーリングを構成する方法を示します。

1. ユーザーがメッセージ拡張機能を選択して、タスク モジュールをトリガーします。
1. ユーザーは、タスク モジュールを使用してポーリングを構成します。
1. 構成タスク モジュールを送信した後、アプリはタスク モジュールで提供された情報を使用してアダプティブ カードを作成し、クライアントに応答として `botMessagePreview` 送信します。
1. その後、ボットがチャネルに挿入する前に、アダプティブ カード メッセージをプレビューできます。 ボットがまだチャネルのメンバーでない場合は、クリックすると `Send` ボットが追加されます。
1. アダプティブ カードを操作すると、メッセージを送信する前にメッセージが変更されます。
1. ユーザーが選択 `Send` すると、ボットはメッセージをチャネルに投稿します。

このフローを有効にするには、次の例のようにタスク モジュールが応答する必要があります。これにより、プレビュー メッセージがユーザーに表示されます。

> [!NOTE]
> には `activityPreview` 、 `message` アダプティブ カードの添付ファイルが 1 つだけ含まれるアクティビティが含まれている必要があります。


```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

これで、メッセージ拡張機能は 2 つの新しい種類の対話に応答する必要があります `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"`。 処理する必要があるオブジェクトの `value` 例を次に示します。

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send" | "edit",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

要求に応答するときは、ユーザーが既に `edit` 送信した情報が入力された値を含む応答で応答 `task` する必要があります。 要求に `send` 応答するときは、最終的なアダプティブ カードを含むチャネルにメッセージを送信する必要があります。

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
teamChatConnector.onComposeExtensionSubmitAction((
    event: builder.IEvent,
    request: teamBuilder.IComposeExtensionActionCommandRequest,
    callback: (err: Error, result: any, statusCode: number) => void) => {
        let invokeValue = (<any> event).value;

        if (invokeValue.botMessagePreviewAction ) {
            let attachment = invokeValue.botActivityPreview[0].attachments[0];

            if (invokeValue.botMessagePreviewAction === 'send') {
                let msg = new builder.Message()
                    .address(event.address)
                    .addAttachment(attachment);
                teamChatConnector.send([msg.toMessage()],
                    (error) => {
                        if(error){
                            //TODO: Handle error and callback
                        }
                        else {
                            callback(null, null, 200);
                        }
                    }
                );
            }

            else if (invokeValue.botMessagePreviewAction === 'edit') {
              // Create the card and populate with user-inputted information
              let card = { ... }

              let taskResponse = {
                task: {
                  type: "continue",
                  value: {
                    title: "Card Preview",
                    card: {
                      contentType: 'application/vnd.microsoft.card.adaptive',
                      content: card
                    }
                  }
                }
              }
              callback(null, taskResponse, 200);
            }

        else {
            let attachment = {
                  //create adaptive card
                };
            let activity = new builder.Message().addAttachment(attachment).toMessage();
            let response = teamBuilder.ComposeExtensionResponse.messagePreview()
                .preview(activity)
                .toResponse();
            callback(null, response, 200);
        }
    });
```

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

このサンプルでは、 [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) を使用してこのフローを示します。

```csharp
public class MessagesController : ApiController
{

    [BotAuthentication]
    public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
    {
        MicrosoftAppCredentials.TrustServiceUrl(activity.ServiceUrl, DateTime.MaxValue);
        ConnectorClient connectorClient = new ConnectorClient(
            new Uri(activity.ServiceUrl),
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppIdKey],
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppPasswordKey]);

        if (activity.Type == ActivityTypes.Invoke)
        {
            // Initial task module presented to the user
            if (activity.Name == "composeExtension/fetchTask")
            {
                string task = GetTaskModule();

                return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
            }
            else if (activity.Name == "composeExtension/submitAction")
            {
                dynamic activityValue = JObject.FromObject(activity.Value);
                string botMessagePreviewAction = activityValue["botMessagePreviewAction"];

                //This is the initial card response sent after the task module is submitted
                if (botMessagePreviewAction is null)
                {
                    string text = activityValue.data.cardMessage;

                    AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "This card will be inserted into the conversation by the bot.",
                        Size = AdaptiveTextSize.Large,
                        Wrap = true
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "The text below is what you provided."
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = text,
                    });

                    string cardJson = card.ToJson();

                    string cardMessage = $@"{{
                        'composeExtension': {{
                        'type': 'botMessagePreview',
                        'activityPreview': {{
                            'type': 'message',
                            'attachments': [{{
                                'contentType': 'application/vnd.microsoft.card.adaptive',
                                'content': {cardJson}
                            }}]
                        }}
                        }}
                    }}";

                    JObject res = JObject.Parse(cardMessage);
                    return Request.CreateResponse(HttpStatusCode.OK, res);

                }
                else
                {
                    //This is the "send the card to the channel" event
                    if (botMessagePreviewAction.Equals("send"))
                    {
                        string cardJson = JsonConvert.SerializeObject(activityValue.botActivityPreview[0].attachments[0].content);

                        AdaptiveCardParseResult cardResult = AdaptiveCard.FromJson(cardJson);
                        AdaptiveCard card = cardResult.Card;
                        Attachment cardAttachment = new Attachment
                        {
                            ContentType = AdaptiveCard.ContentType,
                            Content = card
                        };


                        Activity response = activity.CreateReply();
                        response.Attachments.Add(cardAttachment);

                        var result = await connectorClient.Conversations.SendToConversationAsync(response);
                    }
                    //This is fired if the user edits the card before sending it
                    else if (botMessagePreviewAction.Equals("edit"))
                    {
                        string task = GetTaskModule();

                        return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
                    }
                    else
                    {
                        return Request.CreateResponse(HttpStatusCode.NotImplemented);
                    }
                }
            }
        }

        return Request.CreateResponse(HttpStatusCode.NotImplemented);

    }

    private static string GetTaskModule()
    {
        AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Please enter the following information:",
            Size = AdaptiveTextSize.Large
        });
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Card Message:"
        });
        card.Body.Add(new AdaptiveTextInput()
        {
            Id = "cardMessage",
            Spacing = AdaptiveSpacing.None,
            Placeholder = "Card message goes here."
        });
        card.Actions.Add(new AdaptiveSubmitAction()
        {
            Title = "Submit"
        });

        string cardJson = card.ToJson();

        //Create the task module response
        string task = $@"{{
                            'task': {{
                                'type': 'continue',
                                'value': {{
                                    'card': {{
                                        'contentType': 'application/vnd.microsoft.card.adaptive',
                                        'content': {cardJson}
                                        }}
                                    }}
                                }}
                            }}";
        return task;
    }

}
```

## <a name="see-also"></a>関連項目

[Bot Framework Samples (Bot Framework のサンプル)](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
