---
title: メッセージング拡張機能を使用してアクションを開始する
description: アクション ベースのメッセージング拡張機能を作成して、ユーザーが外部サービスをトリガーできる
localization_priority: Normal
ms.topic: how-to
keywords: teams メッセージング拡張機能メッセージング拡張機能の検索
ms.openlocfilehash: bfb3295726c355164f080c15e3759ea36a99d914
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566741"
---
# <a name="initiate-actions-with-messaging-extensions"></a>メッセージング拡張機能を使用してアクションを開始する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

アクション ベースのメッセージング拡張機能を使用すると、ユーザーは外部サービスの内部でアクションをトリガー Teams。

![メッセージング拡張機能カードの例](~/assets/images/compose-extensions/ceexample.png)

次のセクションでは、これを行う方法について説明します。

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>アクションの種類のメッセージ拡張機能

メッセージング拡張機能からアクションを開始するには、パラメーターを `type` に設定します `action` 。 次に、検索と作成コマンドを含むマニフェストの例を示します。 1 つのメッセージング拡張機能には、最大 10 の異なるコマンドを使用できます。 これには、複数の検索と複数のアクション ベースのコマンドの両方を含めできます。

#### <a name="complete-app-manifest-example"></a>アプリ マニフェストの完全な例

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

メッセージの作成領域からアクションを開始する以外に、メッセージング拡張機能を使用してメッセージからアクションを開始することもできます。 これにより、メッセージの内容をボットに送信して処理し、必要に応じて送信の応答で説明されているメソッドを使用して、そのメッセージに返信 [できます](#responding-to-submit)。 返信は、ユーザーが送信する前に編集できるメッセージへの返信として挿入されます。 ユーザーは、オーバーフロー メニューからメッセージング拡張機能にアクセスし、次の `...` 図のように `Take action` 選択できます。

![メッセージからアクションを開始する例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

メッセージからメッセージング拡張機能を機能するには、次の例のように、アプリ マニフェスト内のメッセージング拡張機能のオブジェクトにパラメーターを追加 `context` `commands` する必要があります。 配列の有効な `context` 文字列は `"message"` 、、 `"commandBox"` 、および `"compose"` です。 既定値は `["compose", "commandBox"]` です。 パラメーターの [詳細については、「コマンド](#define-commands) の定義」セクションを参照 `context` してください。

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

以下は、ボットに送信される要求の一部として送信されるメッセージの詳細を含む `value` `composeExtension` オブジェクトの例です。

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

メッセージング拡張機能をテストするには、アプリをアップロードします。 詳細については、「チームでの [アプリのアップロード」を参照してください](~/concepts/deploy-and-publish/apps-upload.md)。

メッセージング拡張機能を開くには、チャットまたはチャネルに移動します。 作成ボックス **で** [**その** 他の&#8943;] ボタンを選択し、メッセージング拡張機能を選択します。

## <a name="collecting-input-from-users"></a>ユーザーからの入力の収集

エンド ユーザーから情報を収集するには、次の 3 つのTeams。

### <a name="static-parameter-list"></a>静的パラメーター リスト

このメソッドでは、上記の "Create To Do" コマンドに示すように、マニフェスト内のパラメーターの静的な一覧を定義To Doです。 このメソッドを使用するには、 `fetchTask` マニフェストにパラメーターを設定し `false` 、パラメーターを定義します。

ユーザーが静的パラメーターを含むコマンドを選択すると、Teamsで定義されたパラメーターを持つフォームがタスク モジュールに生成されます。 送信時にボット `composeExtension/submitAction` に送信されます。 予想される応答のセットの詳細については、「送信への応答 [」を参照してください](#responding-to-submit)。

### <a name="dynamic-input-using-an-adaptive-card"></a>アダプティブ カードを使用した動的入力

このメソッドでは、サービスは、エンド ユーザー入力を収集するカスタムアダプティブ カードを定義できます。 この方法では、マニフェスト `fetchTask` でパラメーター `true` を設定します。 コマンドに対して定義 `fetchTask` されている `true` 静的パラメーターに設定すると、無視されます。

この方法では、サービスはイベントを受け取り、アダプティブ カード ベースのタスク モジュール応答で `composeExtension/fetchTask` [応答する必要があります](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)。 アダプティブ カードを使用した応答の例を次に示します。

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

ユーザーがユーザー入力を取得する前に拡張機能を認証または構成する必要がある場合、ボットは認証/構成応答で応答することもできます。

### <a name="dynamic-input-using-a-web-view"></a>Web ビューを使用した動的入力

このメソッドでは、サービスに基づくウィジェットを表示して、カスタム UI を表示し、 `<iframe>` ユーザー入力を収集できます。 この方法では、マニフェスト `fetchTask` でパラメーター `true` を設定します。

アダプティブ カード フローと同様に、サービスはイベントを送信し、URL ベースのタスク モジュール応答で応答 `fetchTask` [する必要があります](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)。 アダプティブ カードを使用した応答の例を次に示します。

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

アプリに会話型ボットも含まれている場合は、タスク モジュールを読み込む前にボットが会話にインストールされていることを確認する必要がある場合があります。 これは、タスク モジュールの追加コンテキストを取得する必要がある状況で役立ちます。 たとえば、ユーザー選択コントロール、またはチーム内のチャネルの一覧を設定するために、名簿をフェッチする必要がある場合があります。

このフローを容易にするために、メッセージング拡張機能が最初に呼び出しチェックを受け取り、ボットが現在のコンテキスト `composeExtension/fetchTask` にインストールされていないか確認します。 これを実現するには、名簿の取得呼び出しを試みることができます。たとえば、ボットがインストールされていない場合は、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します。以下の例を参照してください。 この場合、ユーザーは、その場所にアプリをインストールするアクセス許可を持っている必要があります。できない場合は、管理者に連絡を求めるメッセージが表示されます。

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

ユーザーがインストールを完了すると、ボットは別の呼び出しメッセージを受け `name = composeExtension/submitAction` 取ります `value.data.msteams.justInTimeInstall = true` 。

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

ボットが既にインストールされている場合と同じタスク応答で、この呼び出しに応答する必要があります。

## <a name="responding-to-submit"></a>送信への応答

ユーザーが入力を完了すると、ボットはコマンド ID とパラメーター値が設定されたイベント `composeExtension/submitAction` を受け取ります。

これらは、 に対する異なる期待される応答です `submitAction` 。

### <a name="task-module-response"></a>タスク モジュールの応答

これは、拡張機能が詳細を取得するためにダイアログを連鎖する必要がある場合に使用されます。 応答は、前述とまったく `fetchTask` 同じです。

### <a name="compose-extension-authconfig-response"></a>拡張機能の auth/config 応答の作成

これは、拡張機能を続行するために認証または構成する必要がある場合に使用されます。 詳細については、「検索」 [セクションの「認証](~/resources/messaging-extension-v3/search-extensions.md#authentication) 」セクションを参照してください。

### <a name="compose-extension-result-response"></a>拡張機能の結果の応答を作成する

これは、コマンドの結果として、カードを作成ボックスに挿入するために使用されます。 これは、検索コマンドで使用される応答と同じですが、配列内のカードまたは 1 つの結果に制限されます。

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

送信アクションに応答するには、アダプティブ カードを含むメッセージをボットを使用してチャネルに挿入します。 ユーザーは、メッセージを送信する前にプレビューしたり、メッセージを編集したり操作したりすることもできます。 これは、アダプティブ カード応答を作成する前にユーザーから情報を収集する必要があるシナリオで非常に役立ちます。 次のシナリオは、チャネル メッセージに構成手順を含めずに、このフローを使用してポーリングを構成する方法を示しています。

1. ユーザーがメッセージング拡張機能をクリックしてタスク モジュールをトリガーします。
1. ユーザーはタスク モジュールを使用してポーリングを構成します。
1. 構成タスク モジュールを送信した後、アプリはタスク モジュールで提供された情報を使用してアダプティブ カードを作成し、クライアントに応答 `botMessagePreview` として送信します。
1. その後、ボットがチャネルに挿入する前に、アダプティブ カード メッセージをプレビューできます。 ボットがチャネルのメンバーではない場合は、クリックすると `Send` ボットが追加されます。
1. アダプティブ カードを操作すると、メッセージを送信する前に変更されます。
1. ユーザーがクリックすると `Send` 、ボットはメッセージをチャネルに投稿します。

このフローを有効にするには、タスク モジュールは次の例のように応答する必要があります。これにより、プレビュー メッセージがユーザーに表示されます。

>[!Note]
>アダプティブ `activityPreview` カードの添付ファイル `message` が 1 つのアクティビティを含む必要があります。

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

これで、メッセージ拡張機能は 2 種類の新しい種類の操作に応答する必要 `value.botMessagePreviewAction = "send"` があります `value.botMessagePreviewAction = "edit"` 。 次に、処理する必要 `value` があるオブジェクトの例を示します。

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

要求に応答する場合は、ユーザーが既に送信した情報が入力された値で応答 `edit` `task` する必要があります。 要求に応答する場合は、確定したアダプティブ カードを含むチャネルに `send` メッセージを送信する必要があります。

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

このサンプルでは[、Microsoft.Bot.Connector.Teams SDK (v3) を使用してこのフローを示します](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)。

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