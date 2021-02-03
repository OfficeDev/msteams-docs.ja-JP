---
title: タスク モジュールの作成と送信
author: clearab
description: 最初の呼び出しアクションを処理し、アクション メッセージング拡張機能コマンドからタスク モジュールで応答する方法
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58fb7e1ff5690b33c2e23f68529f05869afa9016
ms.sourcegitcommit: ce74f821660b1258c72b3c3f71c1cf177e7e92ef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "50072876"
---
# <a name="create-and-send-the-task-module"></a>タスク モジュールの作成と送信

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

アプリ マニフェストで定義されたパラメーターを使ってタスク モジュールにデータを入力しない場合は、ユーザー用のタスク モジュールを作成する必要があります。 アダプティブ カードまたは埋め込み Web ビューのいずれかを使用します。

## <a name="the-initial-invoke-request"></a>最初の呼び出し要求

このメソッドを使用すると、サービスは型のオブジェクトを受け取り、アダプティブ カードまたは埋め込み Web ビューへの URL を含むオブジェクトで応答 `Activity` `composeExtension/fetchTask` `task` する必要があります。 標準のボット アクティビティ プロパティと共に、最初の呼び出しペイロードには次の要求メタデータが含まれます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は次の値である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は次の値である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (要求がチャネルで行われた場合)。 |
|`channelData.team.id`| チーム ID (チャネルで要求が行われた場合)。 |
|`value.commandId` | 呼び出されたコマンドの ID を格納します。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は次の値である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。 この値は `default` 、次の値 `contrast` である必要があります `dark` 。 |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-11-chat-are-listed-in-the-following-section"></a>1 対 1 のチャットからタスク モジュールが呼び出された場合のペイロード アクティビティのプロパティは、次のセクションに一覧表示されます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は、次の値である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は次の値である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信であるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID を格納します。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は次の値である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。 この値は `default` 、次の値 `contrast` である必要があります `dark` 。 |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-group-chat-are-listed-in-the-following-section"></a>グループ チャットからタスク モジュールを呼び出した場合のペイロード アクティビティプロパティは、次のセクションに示されています。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は次の値である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は、次の値である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信であるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID を格納します。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は次の値である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。 この値は 、または `default` `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-new-post-are-listed-in-the-following-section"></a>チャネルからタスク モジュールを呼び出した場合のペイロード アクティビティ プロパティ (新しい投稿) は、次のセクションに一覧表示されます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は次の値である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は、次の値である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (要求がチャネルで行われた場合)。 |
|`channelData.team.id`| チーム ID (チャネルで要求が行われた場合)。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信であるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID を格納します。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は、次の値である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。 この値は `default` 、次の値 `contrast` である必要があります `dark` 。 |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-reply-to-thread-are-listed-in-the-following-section"></a>チャネルからタスク モジュールを呼び出した場合のペイロード アクティビティ プロパティ (スレッドに返信) を次のセクションに示します。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は、次の値である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は次の値である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (要求がチャネルで行われた場合)。 |
|`channelData.team.id`| チーム ID (チャネルで要求が行われた場合)。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信であるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID を格納します。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は次の値である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。 この値は 、または `default` `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-command-box-are-listed-in-the-following-section"></a>コマンド ボックスからタスク モジュールを呼び出した場合のペイロード アクティビティ のプロパティは、次のセクションに示します。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は、次の値である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は次の値である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`value.commandId` | 呼び出されたコマンドの ID を格納します。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は、次の値である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。 この値は 、または `default` `contrast` `dark` . |

### <a name="example-fetchtask-request"></a>fetchTask 要求の例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
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
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a>メッセージからの最初の呼び出し要求

ボットが作成領域またはコマンド バーではなくメッセージから呼び出された場合、最初の要求のオブジェクトには、メッセージング拡張機能が呼び出されるメッセージの詳細が含まれている `value` 必要があります。 このオブジェクトの例については、次のセクションを参照してください。 The `reactions` and arrays are `mentions` optional, and they are not present if there are no reactions or mentions in the original message.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

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
        "content": "This is the message the messaging extension was invoked from."
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

* * *

## <a name="respond-to-the-fetchtask"></a>fetchTask に応答する

アダプティブ カードまたは Web URL を持つオブジェクト、または単純な文字列メッセージを含むオブジェクトを使用して、呼び出し要求 `task` `taskInfo` に応答します。

|プロパティ名|用途|
|---|---|
|`type`| フォームを `continue` 表示するか、単純な `message` ポップアップを表示することができます。 |
|`value`| フォーム `taskInfo` のオブジェクト、またはメッセージ `string` の a。 |

taskInfo オブジェクトのスキーマは次の例です。

|プロパティ名|用途|
|---|---|
|`title`| タスク モジュールのタイトル。|
|`height`| 整数 (ピクセル単位) または , `small` `medium` , . `large`|
|`width`| 整数 (ピクセル単位) または , `small` `medium` , . `large`|
|`card`| フォームを定義するアダプティブ カード (使用している場合)。
|`url`| 埋め込み Web ビューとしてタスク モジュール内で開く URL。|
|`fallbackUrl`| クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開きます。 |

### <a name="with-an-adaptive-card"></a>アダプティブ カードを使用する

アダプティブ カードを使用する場合は、アダプティブ カードを含むオブジェクトを持つ `task` `value` オブジェクトに応答する必要があります。

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a>アダプティブ カードを使用した fetchTask 応答の例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

このサンプルでは、Bot Framework SDK [に加えて AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) パッケージを使用します。

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a>埋め込み Web ビューを使用する

埋め込み Web ビューを使用する場合は、読み込む Web フォームの URL を含むオブジェクトを持つオブジェクトに応答 `task` `value` する必要があります。 読み込む URL のドメインは、アプリのマニフェストの配列に含 `validDomains` める必要があります。 埋め [込み Web ビューの構築](~/task-modules-and-cards/what-are-task-modules.md) に関する詳細については、タスク モジュールのドキュメントを参照してください。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a>会話ボットのインストール要求

アプリに会話ボットが含まれている場合は、タスク モジュールを読み込む前に会話にボットをインストールします。 タスク モジュールの追加のコンテキストを取得すると便利です。 このシナリオの一般的な例は、名簿をフェッチして、ユーザー選択コントロールまたはチーム内のチャネルの一覧を設定します。

メッセージング拡張機能が呼び出しを受信したら、ボットが現在のコンテキストにインストールされていることを確認して、フロー `composeExtension/fetchTask` を容易にしてください。 たとえば、名簿呼び出しを取得してフローを確認します。 ボットがインストールされていない場合は、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します。 次の例のアクションを参照してください。 ユーザーには、その場所にアプリをインストールして確認するためのアクセス許可が必要です。 アプリのインストールが失敗した場合、ユーザーは管理者に連絡するメッセージを受け取ります。

#### <a name="example-of-the-response"></a>応答の例:

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

インストール後、ボットは別の呼び出しメッセージを `name = composeExtension/submitAction` 受け取ります `value.data.msteams.justInTimeInstall = true` 。

#### <a name="example-of-the-invoke"></a>呼び出しの例:

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

呼び出しに対するタスクの応答は、インストールされているボットの応答と似ている必要があります。

#### <a name="example-of-just-in-time-installation-of-app-with-adaptive-card"></a>アダプティブ カードを含むアプリの just-in Time インストールの例: 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="next-steps"></a>次の手順

ユーザーがタスク モジュールから応答を返送できる場合は、送信アクションを処理する必要があります。

* [タスク モジュールを作成して応答する](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
