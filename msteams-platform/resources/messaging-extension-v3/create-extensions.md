---
title: メッセージング拡張機能を使用してアクションを開始する
description: アクションベースのメッセージング拡張機能を作成して、ユーザーが外部サービスをトリガーできるようにする
localization_priority: Normal
ms.topic: how-to
keywords: チーム メッセージング拡張機能のメッセージング拡張機能の検索
ms.openlocfilehash: bfb3295726c355164f080c15e3759ea36a99d914
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566741"
---
# <a name="initiate-actions-with-messaging-extensions"></a>メッセージング拡張機能を使用してアクションを開始する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

アクションベースのメッセージング拡張機能を使用すると、ユーザーはTeams内部で外部サービスでアクションをトリガーできます。

![メッセージング拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

次のセクションでは、この方法について説明します。

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>アクションの種類のメッセージ拡張

メッセージング拡張機能からアクションを開始するには、パラメーターを `type` `action` に設定します。 以下は、検索と作成コマンドを含むマニフェストの例です。 1 つのメッセージング拡張機能には、最大 10 種類のコマンドを使用できます。 これには、複数の検索と複数のアクション ベースのコマンドの両方を含めることができます。

#### <a name="complete-app-manifest-example"></a>完全なアプリ マニフェストの例

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
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
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

メッセージ作成領域からアクションを開始するだけでなく、メッセージング拡張機能を使用してメッセージからアクションを開始することもできます。 これにより、処理のためにボットにメッセージの内容を送信し、必要に応じて、「 [送信の応答](#responding-to-submit)」で説明されている方法を使用して応答を返してそのメッセージに返信できます。 返信は、送信前にユーザーが編集できるメッセージへの返信として挿入されます。 ユーザーは、オーバーフロー メニューからメッセージング拡張機能にアクセス `...` し、 `Take action` 次の図のように選択できます。

![メッセージからアクションを起こす例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

メッセージからメッセージング拡張機能を機能させるには、 `context` `commands` 次の例のように、アプリ マニフェストでメッセージング拡張機能のオブジェクトにパラメーターを追加する必要があります。 配列に有効な文字列 `context` は `"message"` `"commandBox"` 、 、および `"compose"` です。 既定値は `["compose", "commandBox"]` です。 パラメーターの詳細については、 [コマンドの定義](#define-commands) セクションを参照 `context` してください。

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

以下は、 `value` リクエストの一部として送信されるメッセージの詳細を含むオブジェクトの `composeExtension` 例をボットに送信します。

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

アプリをアップロードして、メッセージング拡張機能をテストできます。 詳しくは、 [チームでのアプリのアップロードを](~/concepts/deploy-and-publish/apps-upload.md)参照してください。

メッセージング拡張機能を開くには、チャットまたはチャネルのいずれかに移動します。 作成ボックスの [ **その他のオプション** ] (**&#8943;**) を選択し、メッセージング拡張機能を選択します。

## <a name="collecting-input-from-users"></a>ユーザーからの入力の収集

Teamsでエンド ユーザーから情報を収集する方法は 3 つあります。

### <a name="static-parameter-list"></a>静的パラメータリスト

このメソッドでは、上記の「To Do作成」コマンドに示すように、マニフェスト内のパラメーターの静的なリストを定義するだけです。 このメソッドを使用するには `fetchTask` 、必ずにマニフェスト `false` にパラメーターを定義するように設定します。

ユーザーが静的パラメーターを持つコマンドを選択すると、マニフェストで定義されたパラメーターを使用して、タスク モジュールにフォームが生成Teams。 [Submit] を押すと `composeExtension/submitAction` 、ボットに送信されます。 予想される応答のセットの詳細については、「 [送信への応答」を](#responding-to-submit)参照してください。

### <a name="dynamic-input-using-an-adaptive-card"></a>アダプティブカードを使用したダイナミック入力

このメソッドでは、サービスはカスタム アダプティブ カードを定義してエンド ユーザー入力を収集できます。 この方法では、パラメーターを `fetchTask` `true` マニフェストに設定します。 `fetchTask` `true` コマンドに対して定義された静的パラメーターを設定すると、無視されることに注意してください。

このメソッドでは、サービスはイベントを受信 `composeExtension/fetchTask` し、アダプティブ カード ベース [のタスク モジュール応答](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)で応答する必要があります。 アダプティブ カードの応答例を次に示します。

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

ボットは、ユーザーがユーザー入力を取得する前に、ユーザーが拡張機能を認証または構成する必要がある場合に、auth/config 応答で応答することもできます。

### <a name="dynamic-input-using-a-web-view"></a>Web ビューを使用した動的入力

このメソッドでは、サービスは `<iframe>` 、任意のカスタム UI を表示し、ユーザー入力を収集するベースのウィジェットを表示できます。 この方法では、パラメーターを `fetchTask` `true` マニフェストに設定します。

アダプティブ カード フローと同様に、サービスはイベントを送信 `fetchTask` し、URL ベースの [タスク モジュール応答](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)で応答する必要があります。 次に、アダプティブ カードを使用した応答の例を示します。

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

### <a name="request-to-install-your-conversational-bot"></a>会話型ボットのインストールをリクエストする

アプリに会話型ボットも含まれている場合は、タスク モジュールを読み込む前に、ボットがスレッドにインストールされていることを確認する必要があります。 これは、タスクモジュールの追加コンテキストを取得する必要がある場合に役立ちます。 たとえば、ユーザー選択コントロールやチーム内のチャネルのリストを設定するために、名簿を取得する必要がある場合があります。

このフローを容易にするために、メッセージング拡張機能が最初に `composeExtension/fetchTask` 呼び出しチェックを受けたときに、ボットが現在のコンテキストにインストールされているかどうかを確認します。 たとえば、getroster 呼び出しを試みることでこれを実現できます( たとえば、ボットがインストールされていない場合は、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します以下の例を参照してください)。 この場合、ユーザーはその場所にアプリをインストールする権限を持っている必要があります。管理者に連絡するように求めるメッセージが表示されます。

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

ユーザーがインストールを完了すると、ボットは、 および と共に別の呼び出しメッセージを受け取ります `name = composeExtension/submitAction` `value.data.msteams.justInTimeInstall = true` 。

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

ボットが既にインストールされている場合は、応答したタスクと同じタスク応答を使用して、この呼び出しに応答する必要があります。

## <a name="responding-to-submit"></a>送信への応答

ユーザーが入力を入力すると、ボットは `composeExtension/submitAction` コマンド ID とパラメーター値が設定されたイベントを受け取ります。

これらは、 に対する予想される応答の違いです `submitAction` 。

### <a name="task-module-response"></a>タスク モジュールの応答

これは、拡張機能がダイアログをチェーンして詳細情報を取得する必要がある場合に使用されます。 応答は、前述のとおりです `fetchTask` 。

### <a name="compose-extension-authconfig-response"></a>拡張認証/構成応答の作成

この機能は、拡張機能が認証または設定を続行する必要がある場合に使用されます。 詳細については、検索 [セクションの「認証」セクション](~/resources/messaging-extension-v3/search-extensions.md#authentication) を参照してください。

### <a name="compose-extension-result-response"></a>拡張結果応答の作成

これは、コマンドの結果として、作成ボックスにカードを挿入するために使用されます。 これは検索コマンドで使用される応答と同じですが、配列内の 1 つのカードまたは 1 つの結果に制限されています。

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

また、アダプティブ カードを含むメッセージをボットでチャネルに挿入することで、送信アクションに応答することもできます。 ユーザーは、送信する前にメッセージをプレビューし、メッセージを編集/操作することもできます。 これは、アダプティブ カード応答を作成する前にユーザーから情報を収集する必要があるシナリオで非常に便利です。 次のシナリオでは、このフローを使用して、チャネル メッセージに構成ステップを含めずにポーリングを構成する方法を示します。

1. ユーザーは、タスク モジュールをトリガーするメッセージング拡張機能をクリックします。
1. ユーザーは、タスク モジュールを使用してポーリングを構成します。
1. 構成タスク モジュールを送信した後、アプリはタスク モジュールで提供される情報を使用してアダプティブ カードを作成し、 `botMessagePreview` クライアントに応答として送信します。
1. ユーザーは、アダプティブ カード メッセージをプレビューしてから、ボットがチャネルに挿入します。 ボットがチャネルのメンバーでない場合は、クリック `Send` するとボットが追加されます。
1. アダプティブ カードとやり取りすると、送信前にメッセージが変更されます。
1. ユーザーがクリックすると `Send` 、ボットはメッセージをチャネルに投稿します。

このフローを有効にするには、タスク モジュールは、次の例のように応答する必要があります。

>[!Note]
>には `activityPreview` 、 `message` アダプティブ カードアタッチメントが 1 つ含まれているアクティビティが含まれている必要があります。

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

メッセージ拡張機能は、2 つの新しい種類の対話に応答する必要 `value.botMessagePreviewAction = "send"` があります `value.botMessagePreviewAction = "edit"` 。 以下は、 `value` 処理する必要があるオブジェクトの例です。

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

要求に応答 `edit` する場合は、 `task` ユーザーが既に送信した情報が入力された値を含む応答を返す必要があります。 要求に応答する `send` 場合は、最終的なアダプティブ カードを含むチャネルにメッセージを送信する必要があります。

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

このサンプルでは、このフローを[使用して、SDK (v3) を使用してTeams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)を示します。

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

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)