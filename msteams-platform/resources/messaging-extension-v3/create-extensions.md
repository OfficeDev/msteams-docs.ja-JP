---
title: メッセージング拡張機能を使用したアクションの開始
description: アクションベースのメッセージング拡張機能を作成して、ユーザーが外部サービスを起動できるようにする
keywords: teams メッセージング拡張メッセージング拡張検索
ms.openlocfilehash: 1a38b4f7bfb413defd28950ca9b97f7411cf9c09
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228032"
---
# <a name="initiate-actions-with-messaging-extensions"></a>メッセージング拡張機能を使用したアクションの開始

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

アクションベースのメッセージング拡張機能を使用すると、ユーザーは Teams 内で外部サービスのアクションを開始できます。

![メッセージング拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

次のセクションでは、これを行う方法について説明します。

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>アクションタイプメッセージ拡張子

メッセージング拡張機能からアクションを開始するに`type`は、 `action`パラメーターをに設定します。 次に、検索と create コマンドを使用したマニフェストの例を示します。 1つのメッセージング拡張機能は、最大10個の異なるコマンドを持つことができます。 これには、複数の検索と複数のアクションベースのコマンドの両方を含めることができます。

#### <a name="complete-app-manifest-example"></a>完全なアプリマニフェストの例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

[メッセージの作成] 領域からアクションを開始するだけでなく、メッセージング拡張機能を使用して、メッセージからアクションを開始することもできます。 これにより、メッセージの内容を bot に送信して処理することができます。また、必要に応じて、「 [submit to submit](#responding-to-submit)」で説明されている方法を使用して、そのメッセージに応答を返信します。 応答は、送信前にユーザーが編集できるメッセージへの返信として挿入されます。 ユーザーは、[オーバーフロー `...` ] メニューからメッセージング拡張機能にアクセスし`Take action`て、次の図のように選択することができます。

![メッセージからアクションを開始する例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

メッセージからメッセージング拡張機能を有効にするには、次の例に`context`示すように、アプリマニフェスト`commands`のメッセージング拡張機能のオブジェクトにパラメーターを追加する必要があります。 `context`配列の有効な文字列は`"message"`、 `"commandBox"`、、 `"compose"`です。 既定値は `["compose", "commandBox"]` です。 パラメーターの詳細については、「コマンドの定義」セクションを参照してください。 [](#define-commands) `context`

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

要求の一部として`value`送信されるメッセージの詳細を含むオブジェクトの例を、bot に送信します。 `composeExtension`

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

アプリをアップロードすることで、メッセージング拡張機能をテストできます。 詳細について[は、「チームでアプリをアップロード](~/concepts/deploy-and-publish/apps-upload.md)する」を参照してください。

メッセージング拡張機能を開くには、いずれかのチャットまたはチャネルに移動します。 [新規作成] ボックスの [**その他のオプション**(**&#8943;**)] ボタンをクリックして、メッセージング拡張機能を選択します。

## <a name="collecting-input-from-users"></a>ユーザーからの入力を収集する

Teams でエンドユーザーから情報を収集するには、3つの方法があります。

### <a name="static-parameter-list"></a>静的パラメーターリスト

この方法では、上記の「Create To Do」に示すように、マニフェスト内でパラメーターの静的な一覧を定義するだけです。 このメソッドを使用する`fetchTask`には、 `false`がに設定されており、マニフェストでパラメーターを定義していることを確認します。

ユーザーが静的パラメーターを使用してコマンドを選択すると、Teams はマニフェストで定義されたパラメーターを使用して、タスクモジュール内にフォームを生成します。 [投稿を送信`composeExtension/submitAction`すると、a は bot に送信されます。 予想される応答のセットの詳細については、「 [submit to submit](#responding-to-submit) 」を参照してください。

### <a name="dynamic-input-using-an-adaptive-card"></a>アダプティブカードを使用した動的入力

この方法では、サービスでカスタムのアダプティブカードを定義して、エンドユーザーの入力を収集できます。 この方法では、マニフェスト`fetchTask`内の`true`パラメーターをに設定します。 コマンドに対して定義`fetchTask`さ`true`れている静的パラメーターが設定されている場合は無視されることに注意してください。

このメソッドでは、サービスはイベント`composeExtension/fetchTask`を受け取り、アダプティブカードベースの[タスクモジュール応答](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)と共に応答する必要があります。 アダプティブカードを使用した応答の例を次に示します。

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

Bot は、ユーザーの入力を受け取る前に、ユーザーが拡張機能を認証または構成する必要がある場合に、auth/config 応答で応答することもできます。

### <a name="dynamic-input-using-a-web-view"></a>Web ビューを使用した動的入力

このメソッドでは、カスタム UI を`<iframe>`表示してユーザー入力を収集するためのベースのウィジェットをサービスで表示できます。 この方法では、マニフェスト`fetchTask`内の`true`パラメーターをに設定します。

アダプティブカードフローと同じように、サービスはイベントを`fetchTask`送信し、URL ベースの[タスクモジュール応答](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)で応答する必要があります。 アダプティブカードを使用した応答の例を次に示します。

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

### <a name="request-to-install-your-conversational-bot"></a>会話 bot をインストールする要求

アプリに会話 bot が含まれている場合は、タスクモジュールを読み込む前に、その bot が会話にインストールされていることを確認する必要があります。 これは、タスクモジュールの追加のコンテキストを取得する必要がある場合に便利です。 たとえば、名簿を取得してユーザー選択コントロールに設定する必要がある場合や、チーム内のチャネルのリストに含まれている場合があります。

このフローを円滑にするために、メッセージング拡張機能`composeExtension/fetchTask`が最初に呼び出しチェックを受信して、現在のコンテキストに bot がインストールされているかどうかを確認します (これを行うには、get 名簿呼び出しを試みます)。 Bot がインストールされていない場合は、ユーザーにボットをインストールするよう要求するアクションを含むアダプティブカードを返します。次の例を参照してください。 このためには、ユーザーがその場所にアプリをインストールするためのアクセス許可を持っている必要があることに注意してください。それができない場合は、管理者に連絡するように求めるメッセージが表示されます。

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

ユーザーがインストールを完了すると、ボットはとと`name = composeExtension/submitAction` `value.data.msteams.justInTimeInstall = true`いう別の起動メッセージを受け取ります。

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

この呼び出しには、bot が既にインストールされている場合と同じタスク応答で応答する必要があります。

## <a name="responding-to-submit"></a>送信への応答

ユーザーが入力の入力を完了すると、ボットは`composeExtension/submitAction`コマンド id とパラメーター値が設定されたイベントを受け取ります。

に対するさまざまな予想応答`submitAction`。

### <a name="task-module-response"></a>タスクモジュールの応答

これは、拡張機能がダイアログを結合して詳細情報を取得する必要がある場合に使用されます。 応答は、前述したもの`fetchTask`とまったく同じです。

### <a name="compose-extension-authconfig-response"></a>新規作成拡張機能の認証/構成応答

これは、拡張機能が続行するために認証または構成を必要とする場合に使用されます。 詳細については、「検索」セクションの「[認証」セクション](~/resources/messaging-extension-v3/search-extensions.md#authentication)を参照してください。

### <a name="compose-extension-result-response"></a>拡張結果の作成の応答

コマンドの結果として、カードを新規作成ボックスに挿入するために使用されます。 これは、検索コマンドで使用されるのと同じ応答ですが、1つのカードまたは配列内の1つの結果に制限されます。

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
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>Bot から送信されたアダプティブカードメッセージで応答する

また、サブカード付きのメッセージをボット付きのチャネルに挿入することによって、送信アクションに応答することもできます。 ユーザーは、メッセージを送信する前にプレビューでき、必要に応じて編集や操作を行うこともできます。 これは、アダプティブカード応答を作成する前にユーザーから情報を収集する必要がある場合に非常に役立ちます。 次のシナリオは、このフローを使用して、チャネルメッセージに構成手順を含めずにポーリングを構成する方法を示しています。

1. ユーザーが [メッセージング] 拡張をクリックして、タスクモジュールをトリガーします。
1. ユーザーは、タスクモジュールを使用して投票を構成します。
1. 構成タスクモジュールを送信した後、アプリはタスクモジュールで提供されている情報を使用して、アダプティブ`botMessagePreview`カードを用意し、クライアントへの応答として送信します。
1. ユーザーは、ドーターカードがチャネルに挿入される前に、アダプティブカードメッセージをプレビューすることができます。 Bot がまだチャネルのメンバーではない場合は、を`Send`クリックすると bot が追加されます。
1. アダプティブカードと対話すると、メッセージを送信する前に変更されます。
1. ユーザーが bot を`Send`クリックすると、メッセージがチャネルに送信されます。

このフローを有効にするには、タスクモジュールが次の例のように応答する必要があります。これにより、プレビューメッセージがユーザーに表示されます。

>[!Note]
>に`activityPreview`は、完全`message`に1つのアダプティブカード添付ファイルがあるアクティビティが含まれている必要があります。

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

メッセージ拡張機能は、次の2つの新しい種類の対話`value.botMessagePreviewAction = "send"`に応答`value.botMessagePreviewAction = "edit"`する必要があります。 処理する必要がある`value`オブジェクトの例を次に示します。

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

`edit`要求に応答する場合は、ユーザーが既`task`に送信した情報で値が入力された応答と共に応答を返す必要があります。 `send`要求に応答する場合は、ファイナライズされたアダプティブカードを含むチャネルにメッセージを送信する必要があります。

# <a name="typescriptnodejs"></a>[TypeScript/node.js](#tab/typescript)

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

[Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください*。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

このサンプルでは、このフローを示します。このフローは、 [TEAMS SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)を使用しています。

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
