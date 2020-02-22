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
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="600af-104">メッセージング拡張機能を使用したアクションの開始</span><span class="sxs-lookup"><span data-stu-id="600af-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="600af-105">アクションベースのメッセージング拡張機能を使用すると、ユーザーは Teams 内で外部サービスのアクションを開始できます。</span><span class="sxs-lookup"><span data-stu-id="600af-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![メッセージング拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="600af-107">次のセクションでは、これを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="600af-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="600af-108">アクションタイプメッセージ拡張子</span><span class="sxs-lookup"><span data-stu-id="600af-108">Action type message extensions</span></span>

<span data-ttu-id="600af-109">メッセージング拡張機能からアクションを開始するに`type`は、 `action`パラメーターをに設定します。</span><span class="sxs-lookup"><span data-stu-id="600af-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="600af-110">次に、検索と create コマンドを使用したマニフェストの例を示します。</span><span class="sxs-lookup"><span data-stu-id="600af-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="600af-111">1つのメッセージング拡張機能は、最大10個の異なるコマンドを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="600af-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="600af-112">これには、複数の検索と複数のアクションベースのコマンドの両方を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="600af-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="600af-113">完全なアプリマニフェストの例</span><span class="sxs-lookup"><span data-stu-id="600af-113">Complete app manifest example</span></span>

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

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="600af-114">メッセージからアクションを開始する</span><span class="sxs-lookup"><span data-stu-id="600af-114">Initiate actions from messages</span></span>

<span data-ttu-id="600af-115">[メッセージの作成] 領域からアクションを開始するだけでなく、メッセージング拡張機能を使用して、メッセージからアクションを開始することもできます。</span><span class="sxs-lookup"><span data-stu-id="600af-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="600af-116">これにより、メッセージの内容を bot に送信して処理することができます。また、必要に応じて、「 [submit to submit](#responding-to-submit)」で説明されている方法を使用して、そのメッセージに応答を返信します。</span><span class="sxs-lookup"><span data-stu-id="600af-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="600af-117">応答は、送信前にユーザーが編集できるメッセージへの返信として挿入されます。</span><span class="sxs-lookup"><span data-stu-id="600af-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="600af-118">ユーザーは、[オーバーフロー `...` ] メニューからメッセージング拡張機能にアクセスし`Take action`て、次の図のように選択することができます。</span><span class="sxs-lookup"><span data-stu-id="600af-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the image below.</span></span>

![メッセージからアクションを開始する例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="600af-120">メッセージからメッセージング拡張機能を有効にするには、次の例に`context`示すように、アプリマニフェスト`commands`のメッセージング拡張機能のオブジェクトにパラメーターを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="600af-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="600af-121">`context`配列の有効な文字列は`"message"`、 `"commandBox"`、、 `"compose"`です。</span><span class="sxs-lookup"><span data-stu-id="600af-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="600af-122">既定値は `["compose", "commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="600af-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="600af-123">パラメーターの詳細については、「コマンドの定義」セクションを参照してください。 [](#define-commands) `context`</span><span class="sxs-lookup"><span data-stu-id="600af-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

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

<span data-ttu-id="600af-124">要求の一部として`value`送信されるメッセージの詳細を含むオブジェクトの例を、bot に送信します。 `composeExtension`</span><span class="sxs-lookup"><span data-stu-id="600af-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

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

### <a name="test-via-uploading"></a><span data-ttu-id="600af-125">アップロードによるテスト</span><span class="sxs-lookup"><span data-stu-id="600af-125">Test via uploading</span></span>

<span data-ttu-id="600af-126">アプリをアップロードすることで、メッセージング拡張機能をテストできます。</span><span class="sxs-lookup"><span data-stu-id="600af-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="600af-127">詳細について[は、「チームでアプリをアップロード](~/concepts/deploy-and-publish/apps-upload.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="600af-127">See [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for details.</span></span>

<span data-ttu-id="600af-128">メッセージング拡張機能を開くには、いずれかのチャットまたはチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="600af-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="600af-129">[新規作成] ボックスの [**その他のオプション**(**&#8943;**)] ボタンをクリックして、メッセージング拡張機能を選択します。</span><span class="sxs-lookup"><span data-stu-id="600af-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="600af-130">ユーザーからの入力を収集する</span><span class="sxs-lookup"><span data-stu-id="600af-130">Collecting input from users</span></span>

<span data-ttu-id="600af-131">Teams でエンドユーザーから情報を収集するには、3つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="600af-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="600af-132">静的パラメーターリスト</span><span class="sxs-lookup"><span data-stu-id="600af-132">Static parameter list</span></span>

<span data-ttu-id="600af-133">この方法では、上記の「Create To Do」に示すように、マニフェスト内でパラメーターの静的な一覧を定義するだけです。</span><span class="sxs-lookup"><span data-stu-id="600af-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="600af-134">このメソッドを使用する`fetchTask`には、 `false`がに設定されており、マニフェストでパラメーターを定義していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="600af-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="600af-135">ユーザーが静的パラメーターを使用してコマンドを選択すると、Teams はマニフェストで定義されたパラメーターを使用して、タスクモジュール内にフォームを生成します。</span><span class="sxs-lookup"><span data-stu-id="600af-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="600af-136">[投稿を送信`composeExtension/submitAction`すると、a は bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="600af-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="600af-137">予想される応答のセットの詳細については、「 [submit to submit](#responding-to-submit) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="600af-137">See the topic [Responding to submit](#responding-to-submit) for more information on the expected set of responses.</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="600af-138">アダプティブカードを使用した動的入力</span><span class="sxs-lookup"><span data-stu-id="600af-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="600af-139">この方法では、サービスでカスタムのアダプティブカードを定義して、エンドユーザーの入力を収集できます。</span><span class="sxs-lookup"><span data-stu-id="600af-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="600af-140">この方法では、マニフェスト`fetchTask`内の`true`パラメーターをに設定します。</span><span class="sxs-lookup"><span data-stu-id="600af-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="600af-141">コマンドに対して定義`fetchTask`さ`true`れている静的パラメーターが設定されている場合は無視されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="600af-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="600af-142">このメソッドでは、サービスはイベント`composeExtension/fetchTask`を受け取り、アダプティブカードベースの[タスクモジュール応答](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)と共に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="600af-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="600af-143">アダプティブカードを使用した応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="600af-143">Below is an sample response with an adaptive card:</span></span>

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

<span data-ttu-id="600af-144">Bot は、ユーザーの入力を受け取る前に、ユーザーが拡張機能を認証または構成する必要がある場合に、auth/config 応答で応答することもできます。</span><span class="sxs-lookup"><span data-stu-id="600af-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="600af-145">Web ビューを使用した動的入力</span><span class="sxs-lookup"><span data-stu-id="600af-145">Dynamic input using a web view</span></span>

<span data-ttu-id="600af-146">このメソッドでは、カスタム UI を`<iframe>`表示してユーザー入力を収集するためのベースのウィジェットをサービスで表示できます。</span><span class="sxs-lookup"><span data-stu-id="600af-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="600af-147">この方法では、マニフェスト`fetchTask`内の`true`パラメーターをに設定します。</span><span class="sxs-lookup"><span data-stu-id="600af-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="600af-148">アダプティブカードフローと同じように、サービスはイベントを`fetchTask`送信し、URL ベースの[タスクモジュール応答](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)で応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="600af-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="600af-149">アダプティブカードを使用した応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="600af-149">Below is an sample response with an Adaptive card:</span></span>

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="600af-150">会話 bot をインストールする要求</span><span class="sxs-lookup"><span data-stu-id="600af-150">Request to install your conversational bot</span></span>

<span data-ttu-id="600af-151">アプリに会話 bot が含まれている場合は、タスクモジュールを読み込む前に、その bot が会話にインストールされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="600af-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="600af-152">これは、タスクモジュールの追加のコンテキストを取得する必要がある場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="600af-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="600af-153">たとえば、名簿を取得してユーザー選択コントロールに設定する必要がある場合や、チーム内のチャネルのリストに含まれている場合があります。</span><span class="sxs-lookup"><span data-stu-id="600af-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="600af-154">このフローを円滑にするために、メッセージング拡張機能`composeExtension/fetchTask`が最初に呼び出しチェックを受信して、現在のコンテキストに bot がインストールされているかどうかを確認します (これを行うには、get 名簿呼び出しを試みます)。</span><span class="sxs-lookup"><span data-stu-id="600af-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context (you could accomplish this by attempting the get roster call, for example).</span></span> <span data-ttu-id="600af-155">Bot がインストールされていない場合は、ユーザーにボットをインストールするよう要求するアクションを含むアダプティブカードを返します。次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="600af-155">If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="600af-156">このためには、ユーザーがその場所にアプリをインストールするためのアクセス許可を持っている必要があることに注意してください。それができない場合は、管理者に連絡するように求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="600af-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="600af-157">応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="600af-157">Here's an example of the response:</span></span>

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

<span data-ttu-id="600af-158">ユーザーがインストールを完了すると、ボットはとと`name = composeExtension/submitAction` `value.data.msteams.justInTimeInstall = true`いう別の起動メッセージを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="600af-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="600af-159">呼び出しの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="600af-159">Here's an example of the invoke:</span></span>

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

<span data-ttu-id="600af-160">この呼び出しには、bot が既にインストールされている場合と同じタスク応答で応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="600af-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="600af-161">送信への応答</span><span class="sxs-lookup"><span data-stu-id="600af-161">Responding to submit</span></span>

<span data-ttu-id="600af-162">ユーザーが入力の入力を完了すると、ボットは`composeExtension/submitAction`コマンド id とパラメーター値が設定されたイベントを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="600af-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="600af-163">に対するさまざまな予想応答`submitAction`。</span><span class="sxs-lookup"><span data-stu-id="600af-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="600af-164">タスクモジュールの応答</span><span class="sxs-lookup"><span data-stu-id="600af-164">Task Module response</span></span>

<span data-ttu-id="600af-165">これは、拡張機能がダイアログを結合して詳細情報を取得する必要がある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="600af-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="600af-166">応答は、前述したもの`fetchTask`とまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="600af-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="600af-167">新規作成拡張機能の認証/構成応答</span><span class="sxs-lookup"><span data-stu-id="600af-167">Compose extension auth/config response</span></span>

<span data-ttu-id="600af-168">これは、拡張機能が続行するために認証または構成を必要とする場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="600af-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="600af-169">詳細については、「検索」セクションの「[認証」セクション](~/resources/messaging-extension-v3/search-extensions.md#authentication)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="600af-169">See [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section for more details.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="600af-170">拡張結果の作成の応答</span><span class="sxs-lookup"><span data-stu-id="600af-170">Compose extension result response</span></span>

<span data-ttu-id="600af-171">コマンドの結果として、カードを新規作成ボックスに挿入するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="600af-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="600af-172">これは、検索コマンドで使用されるのと同じ応答ですが、1つのカードまたは配列内の1つの結果に制限されます。</span><span class="sxs-lookup"><span data-stu-id="600af-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="600af-173">Bot から送信されたアダプティブカードメッセージで応答する</span><span class="sxs-lookup"><span data-stu-id="600af-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="600af-174">また、サブカード付きのメッセージをボット付きのチャネルに挿入することによって、送信アクションに応答することもできます。</span><span class="sxs-lookup"><span data-stu-id="600af-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="600af-175">ユーザーは、メッセージを送信する前にプレビューでき、必要に応じて編集や操作を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="600af-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="600af-176">これは、アダプティブカード応答を作成する前にユーザーから情報を収集する必要がある場合に非常に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="600af-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="600af-177">次のシナリオは、このフローを使用して、チャネルメッセージに構成手順を含めずにポーリングを構成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="600af-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="600af-178">ユーザーが [メッセージング] 拡張をクリックして、タスクモジュールをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="600af-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="600af-179">ユーザーは、タスクモジュールを使用して投票を構成します。</span><span class="sxs-lookup"><span data-stu-id="600af-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="600af-180">構成タスクモジュールを送信した後、アプリはタスクモジュールで提供されている情報を使用して、アダプティブ`botMessagePreview`カードを用意し、クライアントへの応答として送信します。</span><span class="sxs-lookup"><span data-stu-id="600af-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="600af-181">ユーザーは、ドーターカードがチャネルに挿入される前に、アダプティブカードメッセージをプレビューすることができます。</span><span class="sxs-lookup"><span data-stu-id="600af-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="600af-182">Bot がまだチャネルのメンバーではない場合は、を`Send`クリックすると bot が追加されます。</span><span class="sxs-lookup"><span data-stu-id="600af-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="600af-183">アダプティブカードと対話すると、メッセージを送信する前に変更されます。</span><span class="sxs-lookup"><span data-stu-id="600af-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="600af-184">ユーザーが bot を`Send`クリックすると、メッセージがチャネルに送信されます。</span><span class="sxs-lookup"><span data-stu-id="600af-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="600af-185">このフローを有効にするには、タスクモジュールが次の例のように応答する必要があります。これにより、プレビューメッセージがユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="600af-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="600af-186">に`activityPreview`は、完全`message`に1つのアダプティブカード添付ファイルがあるアクティビティが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="600af-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

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

<span data-ttu-id="600af-187">メッセージ拡張機能は、次の2つの新しい種類の対話`value.botMessagePreviewAction = "send"`に応答`value.botMessagePreviewAction = "edit"`する必要があります。</span><span class="sxs-lookup"><span data-stu-id="600af-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="600af-188">処理する必要がある`value`オブジェクトの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="600af-188">Below is an example of the `value` object you will need to process:</span></span>

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

<span data-ttu-id="600af-189">`edit`要求に応答する場合は、ユーザーが既`task`に送信した情報で値が入力された応答と共に応答を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="600af-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="600af-190">`send`要求に応答する場合は、ファイナライズされたアダプティブカードを含むチャネルにメッセージを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="600af-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="600af-191">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="600af-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

<span data-ttu-id="600af-192">[Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください*。</span><span class="sxs-lookup"><span data-stu-id="600af-192">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="600af-193">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="600af-193">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="600af-194">このサンプルでは、このフローを示します。このフローは、 [TEAMS SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)を使用しています。</span><span class="sxs-lookup"><span data-stu-id="600af-194">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

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
