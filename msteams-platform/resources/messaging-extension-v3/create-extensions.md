---
title: メッセージング拡張機能を使用してアクションを開始する
description: アクション ベースのメッセージング拡張機能を作成して、ユーザーが外部サービスをトリガーできる
localization_priority: Normal
ms.topic: how-to
keywords: teams メッセージング拡張機能メッセージング拡張機能の検索
ms.openlocfilehash: 5604d86f05bad42bf3a00f611711afc34beedf42
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140370"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="dd17d-104">メッセージング拡張機能を使用してアクションを開始する</span><span class="sxs-lookup"><span data-stu-id="dd17d-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="dd17d-105">アクション ベースのメッセージング拡張機能を使用すると、ユーザーは外部サービスの内部でアクションをトリガー Teams。</span><span class="sxs-lookup"><span data-stu-id="dd17d-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![メッセージング拡張機能カードの例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="dd17d-107">次のセクションでは、これを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="dd17d-108">アクションの種類のメッセージ拡張機能</span><span class="sxs-lookup"><span data-stu-id="dd17d-108">Action type message extensions</span></span>

<span data-ttu-id="dd17d-109">メッセージング拡張機能からアクションを開始するには、パラメーターを `type` に設定します `action` 。</span><span class="sxs-lookup"><span data-stu-id="dd17d-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="dd17d-110">次に、検索と作成コマンドを含むマニフェストの例を示します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="dd17d-111">1 つのメッセージング拡張機能には、最大 10 の異なるコマンドを使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="dd17d-112">これには、複数の検索と複数のアクション ベースのコマンドの両方を含めできます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="dd17d-113">アプリ マニフェストの完全な例</span><span class="sxs-lookup"><span data-stu-id="dd17d-113">Complete app manifest example</span></span>

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

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="dd17d-114">メッセージからアクションを開始する</span><span class="sxs-lookup"><span data-stu-id="dd17d-114">Initiate actions from messages</span></span>

<span data-ttu-id="dd17d-115">メッセージの作成領域からアクションを開始する以外に、メッセージング拡張機能を使用してメッセージからアクションを開始することもできます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="dd17d-116">これにより、メッセージの内容をボットに送信して処理し、必要に応じて送信の応答で説明されているメソッドを使用して、そのメッセージに返信 [できます](#responding-to-submit)。</span><span class="sxs-lookup"><span data-stu-id="dd17d-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="dd17d-117">返信は、ユーザーが送信する前に編集できるメッセージへの返信として挿入されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="dd17d-118">ユーザーは、オーバーフロー メニューからメッセージング拡張機能にアクセスし、次の `...` 図のように `Take action` 選択できます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the following image:</span></span>

![メッセージからアクションを開始する例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="dd17d-120">メッセージからメッセージング拡張機能を機能するには、次の例のように、アプリ マニフェスト内のメッセージング拡張機能のオブジェクトにパラメーターを追加 `context` `commands` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd17d-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="dd17d-121">配列の有効な `context` 文字列は `"message"` 、、 `"commandBox"` 、および `"compose"` です。</span><span class="sxs-lookup"><span data-stu-id="dd17d-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="dd17d-122">既定値は `["compose", "commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="dd17d-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="dd17d-123">パラメーターの [詳細については、「コマンド](#define-commands) の定義」セクションを参照 `context` してください。</span><span class="sxs-lookup"><span data-stu-id="dd17d-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

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

<span data-ttu-id="dd17d-124">以下は、ボットに送信される要求の一部として送信されるメッセージの詳細を含む `value` `composeExtension` オブジェクトの例です。</span><span class="sxs-lookup"><span data-stu-id="dd17d-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

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

### <a name="test-via-uploading"></a><span data-ttu-id="dd17d-125">アップロードによるテスト</span><span class="sxs-lookup"><span data-stu-id="dd17d-125">Test via uploading</span></span>

<span data-ttu-id="dd17d-126">メッセージング拡張機能をテストするには、アプリをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="dd17d-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="dd17d-127">詳細については、「チームでの [アプリのアップロード」を参照してください](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="dd17d-127">For more information, see [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

<span data-ttu-id="dd17d-128">メッセージング拡張機能を開くには、チャットまたはチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="dd17d-129">作成ボックス **で** [**その** 他の&#8943;] ボタンを選択し、メッセージング拡張機能を選択します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="dd17d-130">ユーザーからの入力の収集</span><span class="sxs-lookup"><span data-stu-id="dd17d-130">Collecting input from users</span></span>

<span data-ttu-id="dd17d-131">エンド ユーザーから情報を収集するには、次の 3 つのTeams。</span><span class="sxs-lookup"><span data-stu-id="dd17d-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="dd17d-132">静的パラメーター リスト</span><span class="sxs-lookup"><span data-stu-id="dd17d-132">Static parameter list</span></span>

<span data-ttu-id="dd17d-133">このメソッドでは、上記の "Create To Do" コマンドに示すように、マニフェスト内のパラメーターの静的な一覧を定義To Doです。</span><span class="sxs-lookup"><span data-stu-id="dd17d-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="dd17d-134">このメソッドを使用するには、 `fetchTask` マニフェストにパラメーターを設定し `false` 、パラメーターを定義します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="dd17d-135">ユーザーが静的パラメーターを含むコマンドを選択すると、Teamsで定義されたパラメーターを持つフォームがタスク モジュールに生成されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="dd17d-136">送信時にボット `composeExtension/submitAction` に送信されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="dd17d-137">予想される応答のセットの詳細については、「送信への応答 [」を参照してください](#responding-to-submit)。</span><span class="sxs-lookup"><span data-stu-id="dd17d-137">For more information on the expected set of responses, see [Responding to submit](#responding-to-submit).</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="dd17d-138">アダプティブ カードを使用した動的入力</span><span class="sxs-lookup"><span data-stu-id="dd17d-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="dd17d-139">このメソッドでは、サービスは、エンド ユーザー入力を収集するカスタムアダプティブ カードを定義できます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="dd17d-140">この方法では、マニフェスト `fetchTask` でパラメーター `true` を設定します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="dd17d-141">コマンドに対して定義 `fetchTask` されている `true` 静的パラメーターに設定すると、無視されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="dd17d-142">このメソッドでは、サービスはイベントを受信し、アダプティブ カード ベースのタスク モジュール応答 `composeExtension/fetchTask` [で応答します](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="dd17d-142">In this method your service receives a `composeExtension/fetchTask` event and responds with an adaptive card based [task module response](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="dd17d-143">アダプティブ カードを使用した応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-143">Following is a sample response with an adaptive card:</span></span>

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

<span data-ttu-id="dd17d-144">ユーザーがユーザー入力を取得する前に拡張機能を認証または構成する必要がある場合、ボットは認証/構成応答で応答することもできます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="dd17d-145">Web ビューを使用した動的入力</span><span class="sxs-lookup"><span data-stu-id="dd17d-145">Dynamic input using a web view</span></span>

<span data-ttu-id="dd17d-146">このメソッドでは、サービスに基づくウィジェットを表示して、カスタム UI を表示し、 `<iframe>` ユーザー入力を収集できます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="dd17d-147">この方法では、マニフェスト `fetchTask` でパラメーター `true` を設定します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="dd17d-148">アダプティブ カード フローと同様に、サービスはイベントを送信し、URL ベースのタスク モジュール `fetchTask` 応答 [で応答します](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="dd17d-148">Just like in the adaptive card flow your service sends a `fetchTask` event and responds with a URL based [task module response](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="dd17d-149">アダプティブ カードを使用した応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-149">Following is a sample response with an Adaptive card:</span></span>

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="dd17d-150">会話型ボットのインストールを要求する</span><span class="sxs-lookup"><span data-stu-id="dd17d-150">Request to install your conversational bot</span></span>

<span data-ttu-id="dd17d-151">アプリに会話型ボットも含まれている場合は、タスク モジュールを読み込む前にボットが会話にインストールされていることを確認する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="dd17d-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="dd17d-152">これは、タスク モジュールの追加コンテキストを取得する必要がある状況で役立ちます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="dd17d-153">たとえば、ユーザー選択コントロール、またはチーム内のチャネルの一覧を設定するために、名簿をフェッチする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="dd17d-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="dd17d-154">このフローを容易にするために、メッセージング拡張機能が最初に呼び出しチェックを受け取り、ボットが現在のコンテキスト `composeExtension/fetchTask` にインストールされていないか確認します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context.</span></span> <span data-ttu-id="dd17d-155">これを実現するには、名簿の取得呼び出しを試みることができます。たとえば、ボットがインストールされていない場合は、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します。以下の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dd17d-155">You could accomplish this by attempting the get roster call, for example, If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="dd17d-156">この場合、ユーザーは、その場所にアプリをインストールするアクセス許可を持っている必要があります。できない場合は、管理者に連絡を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="dd17d-157">応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-157">Here's an example of the response:</span></span>

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

<span data-ttu-id="dd17d-158">ユーザーがインストールを完了すると、ボットは別の呼び出しメッセージを受け `name = composeExtension/submitAction` 取ります `value.data.msteams.justInTimeInstall = true` 。</span><span class="sxs-lookup"><span data-stu-id="dd17d-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="dd17d-159">呼び出しの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-159">Here's an example of the invoke:</span></span>

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

<span data-ttu-id="dd17d-160">ボットが既にインストールされている場合と同じタスク応答で、この呼び出しに応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd17d-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="dd17d-161">送信への応答</span><span class="sxs-lookup"><span data-stu-id="dd17d-161">Responding to submit</span></span>

<span data-ttu-id="dd17d-162">ユーザーが入力を完了すると、ボットはコマンド ID とパラメーター値が設定されたイベント `composeExtension/submitAction` を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="dd17d-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="dd17d-163">これらは、 に対する異なる期待される応答です `submitAction` 。</span><span class="sxs-lookup"><span data-stu-id="dd17d-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="dd17d-164">タスク モジュールの応答</span><span class="sxs-lookup"><span data-stu-id="dd17d-164">Task Module response</span></span>

<span data-ttu-id="dd17d-165">これは、拡張機能が詳細を取得するためにダイアログを連鎖する必要がある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="dd17d-166">応答は、前述とまったく `fetchTask` 同じです。</span><span class="sxs-lookup"><span data-stu-id="dd17d-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="dd17d-167">拡張機能の auth/config 応答の作成</span><span class="sxs-lookup"><span data-stu-id="dd17d-167">Compose extension auth/config response</span></span>

<span data-ttu-id="dd17d-168">これは、拡張機能を続行するために認証または構成する必要がある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="dd17d-169">詳細については、「検索」 [セクションの「認証](~/resources/messaging-extension-v3/search-extensions.md#authentication) 」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="dd17d-169">For more information, see [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="dd17d-170">拡張機能の結果の応答を作成する</span><span class="sxs-lookup"><span data-stu-id="dd17d-170">Compose extension result response</span></span>

<span data-ttu-id="dd17d-171">これは、コマンドの結果として、カードを作成ボックスに挿入するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="dd17d-172">これは、検索コマンドで使用される応答と同じですが、配列内のカードまたは 1 つの結果に制限されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="dd17d-173">ボットから送信されたアダプティブ カード メッセージで応答する</span><span class="sxs-lookup"><span data-stu-id="dd17d-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="dd17d-174">送信アクションに応答するには、アダプティブ カードを含むメッセージをボットを使用してチャネルに挿入します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="dd17d-175">ユーザーは、メッセージを送信する前にプレビューしたり、メッセージを編集したり操作したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="dd17d-176">これは、アダプティブ カード応答を作成する前にユーザーから情報を収集する必要があるシナリオで非常に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="dd17d-177">次のシナリオは、チャネル メッセージに構成手順を含めずに、このフローを使用してポーリングを構成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="dd17d-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="dd17d-178">ユーザーがメッセージング拡張機能をクリックしてタスク モジュールをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="dd17d-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="dd17d-179">ユーザーはタスク モジュールを使用してポーリングを構成します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="dd17d-180">構成タスク モジュールを送信した後、アプリはタスク モジュールで提供された情報を使用してアダプティブ カードを作成し、クライアントに応答 `botMessagePreview` として送信します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="dd17d-181">その後、ボットがチャネルに挿入する前に、アダプティブ カード メッセージをプレビューできます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="dd17d-182">ボットがチャネルのメンバーではない場合は、クリックすると `Send` ボットが追加されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="dd17d-183">アダプティブ カードを操作すると、メッセージを送信する前に変更されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="dd17d-184">ユーザーがクリックすると `Send` 、ボットはメッセージをチャネルに投稿します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="dd17d-185">このフローを有効にするには、タスク モジュールは次の例のように応答する必要があります。これにより、プレビュー メッセージがユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="dd17d-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="dd17d-186">アダプティブ `activityPreview` カードの添付ファイル `message` が 1 つのアクティビティを含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd17d-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

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

<span data-ttu-id="dd17d-187">これで、メッセージ拡張機能は 2 種類の新しい種類の操作に応答する必要 `value.botMessagePreviewAction = "send"` があります `value.botMessagePreviewAction = "edit"` 。</span><span class="sxs-lookup"><span data-stu-id="dd17d-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="dd17d-188">次に、処理する必要 `value` があるオブジェクトの例を示します。</span><span class="sxs-lookup"><span data-stu-id="dd17d-188">Below is an example of the `value` object you will need to process:</span></span>

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

<span data-ttu-id="dd17d-189">要求に応答する場合は、ユーザーが既に送信した情報が入力された値で応答 `edit` `task` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd17d-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="dd17d-190">要求に応答する場合は、確定したアダプティブ カードを含むチャネルに `send` メッセージを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd17d-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="dd17d-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="dd17d-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="cnet"></a>[<span data-ttu-id="dd17d-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="dd17d-192">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="dd17d-193">このサンプルでは[、Microsoft.Bot.Connector.Teams SDK (v3) を使用してこのフローを示します](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)。</span><span class="sxs-lookup"><span data-stu-id="dd17d-193">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

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

## <a name="see-also"></a><span data-ttu-id="dd17d-194">関連項目</span><span class="sxs-lookup"><span data-stu-id="dd17d-194">See also</span></span>

[<span data-ttu-id="dd17d-195">ボット フレームワークのサンプル</span><span class="sxs-lookup"><span data-stu-id="dd17d-195">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)