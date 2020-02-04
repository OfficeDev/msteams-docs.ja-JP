---
title: タスクモジュールを作成して送信する
author: clearab
description: '[方法] 最初の呼び出しアクションを処理し、アクションメッセージング拡張コマンドからタスクモジュールで応答する方法'
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f5f96e71517d45f52d17d2d70c583ec1eec3babd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674941"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="e11c4-103">タスクモジュールを作成して送信する</span><span class="sxs-lookup"><span data-stu-id="e11c4-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="e11c4-104">アプリマニフェストで定義されたパラメーターを使用してタスクモジュールを設定していない場合は、ユーザーに表示するタスクモジュールを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-104">If you are not populating your task module with parameters defined in your app manifest, you'll need to create the task module to be presented to your users.</span></span> <span data-ttu-id="e11c4-105">アダプティブカードまたは埋め込まれた web ビューのいずれかを使用できます。</span><span class="sxs-lookup"><span data-stu-id="e11c4-105">You can use either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="e11c4-106">最初の呼び出し要求</span><span class="sxs-lookup"><span data-stu-id="e11c4-106">The initial invoke request</span></span>

<span data-ttu-id="e11c4-107">このメソッドを使用すると、サービス`Activity`は型`composeExtension/fetchTask`のオブジェクトを受け取ります。また、アダプティブカード`task`を含むオブジェクト、または埋め込み web ビューへの URL のいずれかを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-107">Using this method you service will receive an `Activity` object of type `composeExtension/fetchTask`, and you'll need to respond with a `task` object containing either the adaptive card or a URL to the embedded web view.</span></span> <span data-ttu-id="e11c4-108">標準の bot アクティビティプロパティに加えて、最初の呼び出しペイロードには次の要求メタデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e11c4-108">In addition to the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="e11c4-109">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="e11c4-109">Property name</span></span>|<span data-ttu-id="e11c4-110">用途</span><span class="sxs-lookup"><span data-stu-id="e11c4-110">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="e11c4-111">要求の種類。で`invoke`ある必要があります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-111">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="e11c4-112">サービスに対して発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="e11c4-112">Type of command that is issued to your service.</span></span> <span data-ttu-id="e11c4-113">はに`composeExtension/fetchTask`なります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-113">Will be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="e11c4-114">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="e11c4-114">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="e11c4-115">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="e11c4-115">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="e11c4-116">要求を送信したユーザーの Azure Active Directory オブジェクト id。</span><span class="sxs-lookup"><span data-stu-id="e11c4-116">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="e11c4-117">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="e11c4-117">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="e11c4-118">チャネル ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="e11c4-118">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="e11c4-119">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="e11c4-119">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="e11c4-120">呼び出されたコマンドの Id が含まれています。</span><span class="sxs-lookup"><span data-stu-id="e11c4-120">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="e11c4-121">イベントを発生させたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="e11c4-121">The context that triggered the event.</span></span> <span data-ttu-id="e11c4-122">はに`compose`なります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-122">Will be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="e11c4-123">埋め込み web ビューの書式設定に役立つ、ユーザーのクライアントテーマ。</span><span class="sxs-lookup"><span data-stu-id="e11c4-123">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="e11c4-124">は`default`、また`contrast`は`dark`になります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-124">Will be `default`, `contrast` or `dark`.</span></span> |

### <a name="example-fetchtask-request"></a><span data-ttu-id="e11c4-125">FetchTask 要求の例</span><span class="sxs-lookup"><span data-stu-id="e11c4-125">Example fetchTask request</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="e11c4-126">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e11c4-126">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="e11c4-127">JavaScript/node.js</span><span class="sxs-lookup"><span data-stu-id="e11c4-127">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="e11c4-128">JSON</span><span class="sxs-lookup"><span data-stu-id="e11c4-128">JSON</span></span>](#tab/json)

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

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="e11c4-129">メッセージからの最初の呼び出し要求</span><span class="sxs-lookup"><span data-stu-id="e11c4-129">Initial invoke request from a message</span></span>

<span data-ttu-id="e11c4-130">Bot が [新規作成] エリアまたはコマンドバーではなくメッセージから呼び出された`value`場合、最初の要求のオブジェクトには、メッセージングの内線番号から呼び出されたメッセージの詳細が含まれます。</span><span class="sxs-lookup"><span data-stu-id="e11c4-130">When your bot is invoked from a message rather than the compose area or the command bar, the `value` object in the initial request will contain the details of the message your messaging extension was invoked from.</span></span> <span data-ttu-id="e11c4-131">このオブジェクトの例を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="e11c4-131">An example of this object is below.</span></span> <span data-ttu-id="e11c4-132">および`reactions` `mentions`の配列はオプションであり、元のメッセージに反応またはメンションが存在しない場合は表示されません。</span><span class="sxs-lookup"><span data-stu-id="e11c4-132">The `reactions` and `mentions` arrays are optional, and will not be present if there are no reactions or mentions in the original message.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="e11c4-133">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e11c4-133">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="e11c4-134">JavaScript/node.js</span><span class="sxs-lookup"><span data-stu-id="e11c4-134">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="e11c4-135">JSON</span><span class="sxs-lookup"><span data-stu-id="e11c4-135">JSON</span></span>](#tab/json)

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

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="e11c4-136">FetchTask に応答する</span><span class="sxs-lookup"><span data-stu-id="e11c4-136">Respond to the fetchTask</span></span>

<span data-ttu-id="e11c4-137">アダプティブカードまたは web URL を`task`持つ`taskInfo`オブジェクトまたは単純な文字列メッセージを含むオブジェクトを使用して、呼び出し要求に応答します。</span><span class="sxs-lookup"><span data-stu-id="e11c4-137">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the adaptive card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="e11c4-138">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="e11c4-138">Property name</span></span>|<span data-ttu-id="e11c4-139">用途</span><span class="sxs-lookup"><span data-stu-id="e11c4-139">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="e11c4-140">フォームを表示`continue`するか、または`message`簡単なポップアップ用にすることができます。</span><span class="sxs-lookup"><span data-stu-id="e11c4-140">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="e11c4-141">フォームの`taskInfo`オブジェクト、またはのメッセージ`string`のいずれか。</span><span class="sxs-lookup"><span data-stu-id="e11c4-141">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="e11c4-142">TaskInfo オブジェクトのスキーマは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e11c4-142">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="e11c4-143">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="e11c4-143">Property name</span></span>|<span data-ttu-id="e11c4-144">用途</span><span class="sxs-lookup"><span data-stu-id="e11c4-144">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="e11c4-145">タスクモジュールのタイトルを示します。</span><span class="sxs-lookup"><span data-stu-id="e11c4-145">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="e11c4-146">整数 (ピクセル単位)、または`small` `medium`、のいずれかを`large`することができます。</span><span class="sxs-lookup"><span data-stu-id="e11c4-146">Can be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="e11c4-147">整数 (ピクセル単位)、または`small` `medium`、のいずれかを`large`することができます。</span><span class="sxs-lookup"><span data-stu-id="e11c4-147">Can be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="e11c4-148">フォームを定義するアダプティブカード (使用している場合)。</span><span class="sxs-lookup"><span data-stu-id="e11c4-148">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="e11c4-149">埋め込み web ビューとしてタスクモジュールの内部に開く URL。</span><span class="sxs-lookup"><span data-stu-id="e11c4-149">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="e11c4-150">クライアントがタスクモジュール機能をサポートしていない場合、この URL はブラウザタブで開かれます。</span><span class="sxs-lookup"><span data-stu-id="e11c4-150">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="with-an-adaptive-card"></a><span data-ttu-id="e11c4-151">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="e11c4-151">With an adaptive card</span></span>

<span data-ttu-id="e11c4-152">アダプティブカードを使用する場合は、アダプティブカードを含むオブジェクト`task`を使用し`value`て、オブジェクトで応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-152">When using an adaptive card, you'll need to respond with a `task` object with the `value` object containing an adaptive card.</span></span>

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a><span data-ttu-id="e11c4-153">アダプティブカードによるタスク応答のフェッチの例</span><span class="sxs-lookup"><span data-stu-id="e11c4-153">Example fetchTask response with an adaptive card</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="e11c4-154">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e11c4-154">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="e11c4-155">このサンプルでは、Bot フレームワーク SDK に加えて[AdaptiveCards NuGet パッケージ](https://www.nuget.org/packages/AdaptiveCards)を使用します。</span><span class="sxs-lookup"><span data-stu-id="e11c4-155">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

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

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="e11c4-156">JavaScript/node.js</span><span class="sxs-lookup"><span data-stu-id="e11c4-156">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="e11c4-157">JSON</span><span class="sxs-lookup"><span data-stu-id="e11c4-157">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "card":
      {
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
        ],
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json"
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a><span data-ttu-id="e11c4-158">埋め込み web ビュー付き</span><span class="sxs-lookup"><span data-stu-id="e11c4-158">With an embedded web view</span></span>

<span data-ttu-id="e11c4-159">埋め込み web ビューを使用する場合は、読み込む web フォームへ`task`の URL を`value`含むオブジェクトを使用してオブジェクトで応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-159">When using an embedded web view, you'll need to respond with a `task` object with the `value` object containing the URL to the web form you'd like to load.</span></span> <span data-ttu-id="e11c4-160">読み込む必要のある URL のドメインは、アプリのマニフェストの`validDomains`配列に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-160">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="e11c4-161">埋め込み web ビューの作成に関する詳細については、「[タスクモジュールのドキュメント](~/task-modules-and-cards/what-are-task-modules.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e11c4-161">See the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md) for complete information on building your embedded web view.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="e11c4-162">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e11c4-162">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="e11c4-163">JavaScript/node.js</span><span class="sxs-lookup"><span data-stu-id="e11c4-163">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="e11c4-164">JSON</span><span class="sxs-lookup"><span data-stu-id="e11c4-164">JSON</span></span>](#tab/json)

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

## <a name="next-steps"></a><span data-ttu-id="e11c4-165">次のステップ</span><span class="sxs-lookup"><span data-stu-id="e11c4-165">Next steps</span></span>

<span data-ttu-id="e11c4-166">ユーザーがタスクモジュールから応答を返信できるようにするには、送信アクションを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e11c4-166">If you allow your users to send a response back from the task module, you'll need to handle the submit action.</span></span>

* [<span data-ttu-id="e11c4-167">タスクモジュールを作成して応答する</span><span class="sxs-lookup"><span data-stu-id="e11c4-167">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
