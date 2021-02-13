---
title: タスク モジュールの送信アクションに応答する
author: clearab
description: メッセージング拡張機能アクション コマンドからタスク モジュール送信アクションに応答する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1fb2f2dc51d7de1208a5a913abf2d38cb80c401a
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231646"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="49802-103">タスク モジュールの送信アクションに応答する</span><span class="sxs-lookup"><span data-stu-id="49802-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="49802-104">ユーザーがタスク モジュールを送信すると、Web サービスはコマンド ID とパラメーター値を含む呼び出し `composeExtension/submitAction` メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="49802-104">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="49802-105">アプリが呼び出しに応答するまでに *5* 秒が必要です。それ以外の場合、ユーザーはアプリに到達できないというエラー メッセージを受け取り、呼び出しに対する返信は Teams クライアントによって無視されます。</span><span class="sxs-lookup"><span data-stu-id="49802-105">Your app has five seconds to respond to the invoke, otherwise the user receives an error message *Unable to reach the app*, and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="49802-106">応答するには、次のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="49802-106">You have the following options for responding:</span></span>

* <span data-ttu-id="49802-107">応答なし - 送信アクションを使用して外部システムのプロセスをトリガーし、ユーザーにフィードバックを提供しない方法を選択できます。</span><span class="sxs-lookup"><span data-stu-id="49802-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="49802-108">これは、長時間実行されるプロセスに役立つ可能性があります。また、別の方法でフィードバックを提供する (プロアクティブ メッセージを含むなど) [選択できます](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="49802-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="49802-109">[別のタスク モジュール](#respond-with-another-task-module) - 複数ステップの操作の一部として、追加のタスク モジュールで応答できます。</span><span class="sxs-lookup"><span data-stu-id="49802-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="49802-110">[カードの](#respond-with-a-card-inserted-into-the-compose-message-area) 応答 - ユーザーが操作したり、メッセージに挿入したりできるカードで応答できます。</span><span class="sxs-lookup"><span data-stu-id="49802-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="49802-111">[ボットからのアダプティブ カード](#bot-response-with-adaptive-card) - 会話に直接アダプティブ カードを挿入します。</span><span class="sxs-lookup"><span data-stu-id="49802-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="49802-112">ユーザー認証を要求する</span><span class="sxs-lookup"><span data-stu-id="49802-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="49802-113">ユーザーに追加の構成の提供を要求する</span><span class="sxs-lookup"><span data-stu-id="49802-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="49802-114">認証または構成の場合、ユーザーがフローを完了すると、元の呼び出しが Web サービスに再送信されます。</span><span class="sxs-lookup"><span data-stu-id="49802-114">For authentication or configuration, after the user completes the flow the original invoke is re-sent to your web service.</span></span> <span data-ttu-id="49802-115">次の表に、メッセージング拡張機能の呼び出し場所に基づいて使用可能な応答の `commandContext` 種類を示します。</span><span class="sxs-lookup"><span data-stu-id="49802-115">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="49802-116">応答の種類</span><span class="sxs-lookup"><span data-stu-id="49802-116">Response Type</span></span> | <span data-ttu-id="49802-117">compose</span><span class="sxs-lookup"><span data-stu-id="49802-117">compose</span></span> | <span data-ttu-id="49802-118">コマンド バー</span><span class="sxs-lookup"><span data-stu-id="49802-118">command bar</span></span> | <span data-ttu-id="49802-119">メッセージ​​</span><span class="sxs-lookup"><span data-stu-id="49802-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="49802-120">カードの応答</span><span class="sxs-lookup"><span data-stu-id="49802-120">Card response</span></span> | <span data-ttu-id="49802-121">x</span><span class="sxs-lookup"><span data-stu-id="49802-121">x</span></span> | <span data-ttu-id="49802-122">x</span><span class="sxs-lookup"><span data-stu-id="49802-122">x</span></span> | <span data-ttu-id="49802-123">x</span><span class="sxs-lookup"><span data-stu-id="49802-123">x</span></span> |
|<span data-ttu-id="49802-124">別のタスク モジュール</span><span class="sxs-lookup"><span data-stu-id="49802-124">Another task module</span></span> | <span data-ttu-id="49802-125">x</span><span class="sxs-lookup"><span data-stu-id="49802-125">x</span></span> | <span data-ttu-id="49802-126">x</span><span class="sxs-lookup"><span data-stu-id="49802-126">x</span></span> | <span data-ttu-id="49802-127">x</span><span class="sxs-lookup"><span data-stu-id="49802-127">x</span></span> |
|<span data-ttu-id="49802-128">アダプティブ カード付きボット</span><span class="sxs-lookup"><span data-stu-id="49802-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="49802-129">x</span><span class="sxs-lookup"><span data-stu-id="49802-129">x</span></span> |  | <span data-ttu-id="49802-130">x</span><span class="sxs-lookup"><span data-stu-id="49802-130">x</span></span> |
| <span data-ttu-id="49802-131">応答なし</span><span class="sxs-lookup"><span data-stu-id="49802-131">No response</span></span> | <span data-ttu-id="49802-132">x</span><span class="sxs-lookup"><span data-stu-id="49802-132">x</span></span> | <span data-ttu-id="49802-133">x</span><span class="sxs-lookup"><span data-stu-id="49802-133">x</span></span> | <span data-ttu-id="49802-134">x</span><span class="sxs-lookup"><span data-stu-id="49802-134">x</span></span> |

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="49802-135">submitAction 呼び出しイベント</span><span class="sxs-lookup"><span data-stu-id="49802-135">The submitAction invoke event</span></span>

<span data-ttu-id="49802-136">呼び出しメッセージを受信する例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="49802-136">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="49802-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="49802-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49802-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49802-138">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="49802-139">JSON</span><span class="sxs-lookup"><span data-stu-id="49802-139">JSON</span></span>](#tab/json)

<span data-ttu-id="49802-140">これは、受け取る JSON オブジェクトの例です。</span><span class="sxs-lookup"><span data-stu-id="49802-140">This is an example of the JSON object you receive.</span></span> <span data-ttu-id="49802-141">この `commandContext` パラメーターは、メッセージング拡張機能がトリガーされた場所を示します。</span><span class="sxs-lookup"><span data-stu-id="49802-141">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="49802-142">この `data` オブジェクトには、フォーム上のフィールドがパラメーターとして含まれます。また、ユーザーが送信した値も含まれます。</span><span class="sxs-lookup"><span data-stu-id="49802-142">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="49802-143">ここでの JSON オブジェクトは、最も関連性の高いフィールドを強調表示するために短縮されています。</span><span class="sxs-lookup"><span data-stu-id="49802-143">The JSON object here is shortened to highlight the most relevant fields.</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith",
  "serviceUrl": "https://smba.trafficmanager.net/amer/",
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "id": "submitButton",
      "formField1": "formField1_value",
      "formField2": "formField2_value",
      "formField3": "formField3_value"
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  }
}
```

* * *

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="49802-144">メッセージ作成領域に挿入されたカードで応答する</span><span class="sxs-lookup"><span data-stu-id="49802-144">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="49802-145">要求に応答する最も一般的な方法は、メッセージ作成領域にカード `composeExtension/submitAction` を挿入する方法です。</span><span class="sxs-lookup"><span data-stu-id="49802-145">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="49802-146">その後、ユーザーは会話にカードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="49802-146">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="49802-147">カードの使用の詳細については、「カードと [カードの操作」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="49802-147">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="49802-148">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="49802-148">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var createCardData = ((JObject)action.Data).ToObject<CreateCardData>();
var card = new HeroCard
{
     Title = createCardData.Title,
     Subtitle = createCardData.Subtitle,
     Text = createCardData.Text,
};
    var attachments = new List<MessagingExtensionAttachment>();
    attachments.Add(new MessagingExtensionAttachment
    {
        Content = card,
        ContentType = HeroCard.ContentType,
        Preview = card.ToAttachment(),
    });
    response.ComposeExtension.Attachments = attachments;
    return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49802-149">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49802-149">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const data = action.data;
    const heroCard = CardFactory.heroCard(data.title, data.text);
    heroCard.content.subtitle = data.subTitle;
    const attachment = { contentType: heroCard.contentType, content: heroCard.content, preview: heroCard };

    return {
      composeExtension: {
        type: 'result',
        attachmentLayout: 'list',
        attachments: [
          attachment
        ]
      }
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="49802-150">JSON</span><span class="sxs-lookup"><span data-stu-id="49802-150">JSON</span></span>](#tab/json)

```json
{
  "composeExtension": {
    "attachmentLayout": "list",
    "type": "result",
    "attachments": [
      {
        "preview": {
          "contentType": "application/vnd.microsoft.card.hero",
          "content": {
            "title": "formField1_value",
            "subtitle": "formField2_value",
            "text": "formField3_value"
          }
        },
        "contentType": "application/vnd.microsoft.card.hero",
        "content": {
          "title": "formField1_value",
          "subtitle": "formField2_value",
          "text": "formField3_value"
        }
      }
    ]
  }
}
```

* * *

## <a name="respond-with-another-task-module"></a><span data-ttu-id="49802-151">別のタスク モジュールで応答する</span><span class="sxs-lookup"><span data-stu-id="49802-151">Respond with another task module</span></span>

<span data-ttu-id="49802-152">追加のタスク モジュールを使用して `submitAction` イベントに応答できます。</span><span class="sxs-lookup"><span data-stu-id="49802-152">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="49802-153">これは、次の場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="49802-153">This can be useful when:</span></span>

* <span data-ttu-id="49802-154">大量の情報を収集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="49802-154">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="49802-155">ユーザー入力に基づいて収集する情報を動的に変更する必要がある場合</span><span class="sxs-lookup"><span data-stu-id="49802-155">If you need to dynamically change what information you are collecting based on user input</span></span>
* <span data-ttu-id="49802-156">ユーザーが送信した情報を検証し、問題が発生した場合はエラー メッセージを表示してフォームを再送信する必要がある場合。</span><span class="sxs-lookup"><span data-stu-id="49802-156">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="49802-157">応答のメソッドは、最初のイベント [に応答する方法と同 `fetchTask` じです](~/messaging-extensions/how-to/action-commands/create-task-module.md)。</span><span class="sxs-lookup"><span data-stu-id="49802-157">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="49802-158">Bot Framework SDK を使用している場合は、両方の送信アクションに対して同じイベント トリガーが発生します。</span><span class="sxs-lookup"><span data-stu-id="49802-158">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="49802-159">つまり、正しい応答を決定するロジックを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="49802-159">This means you must add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="49802-160">アダプティブ カードを使用したボットの応答</span><span class="sxs-lookup"><span data-stu-id="49802-160">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="49802-161">このフローでは、アプリ マニフェストにオブジェクトを追加し、ボットに必要なスコープ `bot` を定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="49802-161">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="49802-162">ボットのメッセージング拡張機能と同じ ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="49802-162">Use the same ID as your messaging extension for your bot.</span></span>

<span data-ttu-id="49802-163">アダプティブ カードを含むメッセージをボットを使用してチャネルに挿入することで、送信アクションに応答できます。</span><span class="sxs-lookup"><span data-stu-id="49802-163">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="49802-164">ユーザーは、送信する前にメッセージをプレビューしたり、メッセージを編集したり操作したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="49802-164">Your user can preview the message before submitting it, and potentially edit or interact with it as well.</span></span> <span data-ttu-id="49802-165">これは、アダプティブ カード応答を作成する前にユーザーから情報を収集する場合や、カードを操作した後にカードを更新する場合に非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="49802-165">This can be very useful in scenarios where you gather information from your users before creating an adaptive card response, or when you update the card after someone interacts with it.</span></span> <span data-ttu-id="49802-166">次のシナリオは、アプリ Polly でこのフローを使用して、チャネル会話に構成手順を含めずにポーリングを構成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="49802-166">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation:</span></span>

1. <span data-ttu-id="49802-167">ユーザーがメッセージング拡張機能を選択して、タスク モジュールをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="49802-167">The user selects the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="49802-168">ユーザーは、タスク モジュールを使用してポーリングを構成します。</span><span class="sxs-lookup"><span data-stu-id="49802-168">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="49802-169">タスク モジュールを提出した後、アプリは提供された情報を使用してポーリングをアダプティブ カードとして構築し、それをクライアントに応答 `botMessagePreview` として送信します。</span><span class="sxs-lookup"><span data-stu-id="49802-169">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="49802-170">ユーザーは、ボットがチャネルに挿入する前に、アダプティブ カード メッセージをプレビューできます。</span><span class="sxs-lookup"><span data-stu-id="49802-170">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="49802-171">アプリがチャネルのメンバーではない場合は、それを選択して `Send` 追加します。</span><span class="sxs-lookup"><span data-stu-id="49802-171">If the app is not already a member of the channel, selecting `Send` adds it.</span></span>
   1. <span data-ttu-id="49802-172">また、ユーザーはメッセージを選択して、元のタスク モジュール `Edit` に返します。</span><span class="sxs-lookup"><span data-stu-id="49802-172">The user can also choose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="49802-173">アダプティブ カードを操作すると、メッセージを送信する前に変更されます。</span><span class="sxs-lookup"><span data-stu-id="49802-173">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="49802-174">ユーザーがボットを選択 `Send` すると、チャネルにメッセージが投稿されます。</span><span class="sxs-lookup"><span data-stu-id="49802-174">After the user selects `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="49802-175">最初の送信アクションに応答する</span><span class="sxs-lookup"><span data-stu-id="49802-175">Respond to initial submit action</span></span>

<span data-ttu-id="49802-176">このフローを有効にするには、ボットがチャネルに送信するカードのプレビューを含む初期メッセージにタスク モジュール `composeExtension/submitAction` が応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="49802-176">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot send to the channel.</span></span> <span data-ttu-id="49802-177">これにより、ユーザーは送信前にカードを確認し、ボットがインストールされていない場合は会話にボットをインストールする機会を得る機会があります。</span><span class="sxs-lookup"><span data-stu-id="49802-177">This gives the user the opportunity to verify the card before sending, and also attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="49802-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="49802-178">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic createCardData = ((JObject) action.Data).ToObject(typeof(JObject));
  var response = new MessagingExtensionActionResponse
  {
    ComposeExtension = new MessagingExtensionResult
    {
      Type = "botMessagePreview",
      ActivityPreview = MessageFactory.Attachment(new Attachment
      {
        Content = new AdaptiveCard("1.0")
        {
          Body = new List<AdaptiveElement>()
          {
            new AdaptiveTextBlock() { Text = "FormField1 value was:", Size = AdaptiveTextSize.Large },
            new AdaptiveTextBlock() { Text = Data["FormField1"] as string }
          },
          Height = AdaptiveHeight.Auto,
          Actions = new List<AdaptiveAction>()
          {
            new AdaptiveSubmitAction
            {
              Type = AdaptiveSubmitAction.TypeName,
              Title = "Submit",
              Data = new JObject { { "submitLocation", "messagingExtensionFetchTask" } },
            },
          }
        },
        ContentType = AdaptiveCard.ContentType
      }) as Activity
    }
  };

  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49802-179">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49802-179">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const submittedData = action.data;
    const adaptiveCard = CardFactory.adaptiveCard({
      actions: [
        { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
      ],
      body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submittedData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
        {
          choices: [
            { title: submittedData.Option1, value: submittedData.Option1 },
            { title: submittedData.Option2, value: submittedData.Option2 },
            { title: submittedData.Option3, value: submittedData.Option3 }
          ],
          id: 'Choices',
          isMultiSelect: submittedData.MultiSelect,
          style: 'expanded',
          type: 'Input.ChoiceSet'
        }
      ],
      type: 'AdaptiveCard',
      version: '1.0'
    });
    return {
      composeExtension: {
        activityPreview: MessageFactory.attachment(adaptiveCard, null, null, InputHints.ExpectingInput),
        type: 'botMessagePreview'
      }
    };
  }
}
```

# <a name="json"></a>[<span data-ttu-id="49802-180">JSON</span><span class="sxs-lookup"><span data-stu-id="49802-180">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="49802-181">The `activityPreview` must contain a activity with `message` exactly 1 adaptive card attachment.</span><span class="sxs-lookup"><span data-stu-id="49802-181">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="49802-182">値 `<< Card Payload >>` は、送信するカードのプレースホルダーです。</span><span class="sxs-lookup"><span data-stu-id="49802-182">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

* * *

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="49802-183">botMessagePreview の送信イベントと編集イベント</span><span class="sxs-lookup"><span data-stu-id="49802-183">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="49802-184">メッセージ拡張機能は、2 つの新しい呼び出しの種類 (場所と `composeExtension/submitAction` `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="49802-184">Your message extension must respond now to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="49802-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="49802-185">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewEditAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49802-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49802-186">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionBotMessagePreviewEdit(context, action) {

    //handle the event
  }
  
  handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {

    //handle the event
  }
}

```

# <a name="json"></a>[<span data-ttu-id="49802-187">JSON</span><span class="sxs-lookup"><span data-stu-id="49802-187">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "edit | send",
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

* * *

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="49802-188">botMessagePreview 編集に応答する</span><span class="sxs-lookup"><span data-stu-id="49802-188">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="49802-189">If the user edits the card before sending by selecting the **Edit** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="49802-189">If the user edits the card before sending by selecting the **Edit** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="49802-190">通常は、対話を開始した最初の呼び出しに応じて送信したタスク モジュール `composeExtension/fetchTask` を返して応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="49802-190">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="49802-191">これにより、ユーザーは元の情報を再入力してプロセスを最初から開始できます。</span><span class="sxs-lookup"><span data-stu-id="49802-191">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="49802-192">利用可能な情報を使用して、ユーザーがすべての情報を最初から入力する必要が生じないので、タスク モジュールに事前に入力します。</span><span class="sxs-lookup"><span data-stu-id="49802-192">Use the available information to pre-populate the task module so the user does not have to fill out all of the information from scratch.</span></span>

<span data-ttu-id="49802-193">最初 [のイベントへの応答を参照 `fetchTask` してください](~/messaging-extensions/how-to/action-commands/create-task-module.md)。</span><span class="sxs-lookup"><span data-stu-id="49802-193">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="49802-194">botMessagePreview 送信に応答する</span><span class="sxs-lookup"><span data-stu-id="49802-194">Respond to botMessagePreview send</span></span>

<span data-ttu-id="49802-195">ユーザーが [送信] ボタンを選択 **すると** 、次の呼び出しを `composeExtension/submitAction` 受け取る `value.botMessagePreviewAction = send` 。</span><span class="sxs-lookup"><span data-stu-id="49802-195">After the user selects the **Send** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="49802-196">Web サービスは、アダプティブ カードを含むプロアクティブ メッセージを作成して会話に送信し、呼び出しに応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="49802-196">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="49802-197">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="49802-197">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var activityPreview = action.BotActivityPreview[0];
  var attachmentContent = activityPreview.Attachments[0].Content;
  var previewedCard = JsonConvert.DeserializeObject<AdaptiveCard>(attachmentContent.ToString(),
          new JsonSerializerSettings { NullValueHandling = NullValueHandling.Ignore });
  
  previewedCard.Version = "1.0";

  var responseActivity = Activity.CreateMessageActivity();
  Attachment attachment = new Attachment()
  {
    ContentType = AdaptiveCard.ContentType,
    Content = previewedCard
  };
  responseActivity.Attachments.Add(attachment);
  
  // Attribute the message to the user on whose behalf the bot is posting
  responseActivity.ChannelData = new {
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }
  };
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49802-198">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49802-198">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {
      // The data has been returned to the bot in the action structure.
      const activityPreview = action.botActivityPreview[0];
      const attachmentContent = activityPreview.attachments[0].content;
      const userText = attachmentContent.body[1].text;
      const choiceSet = attachmentContent.body[3];

      const submitData = {
        MultiSelect: choiceSet.isMultiSelect ? 'true' : 'false',
        Option1: choiceSet.choices[0].title,
        Option2: choiceSet.choices[1].title,
        Option3: choiceSet.choices[2].title,
        Question: userText
      };

      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [
          { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
        ],
        body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submitData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
          {
            choices: [
                { title: submitData.Option1, value: submitData.Option1 },
                { title: submitData.Option2, value: submitData.Option2 },
                { title: submitData.Option3, value: submitData.Option3 }
            ],
            id: 'Choices',
            isMultiSelect: submitData.MultiSelect,
            style: 'expanded',
            type: 'Input.ChoiceSet'
          }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });
      const responseActivity = { type: 'message', attachments: [adaptiveCard], channelData: {
          onBehalfOf: [
              { itemId: 0, mentionType: 'person', mri: context.activity.from.id, displayname: context.activity.from.name }
          ]
      }};

      await context.sendActivity(responseActivity);
    }
}
```

# <a name="json"></a>[<span data-ttu-id="49802-199">JSON</span><span class="sxs-lookup"><span data-stu-id="49802-199">JSON</span></span>](#tab/json)

<span data-ttu-id="49802-200">次のような新 `composeExtension/submitAction` しいメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="49802-200">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send",
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

* * *

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="49802-201">ボット メッセージのユーザー属性</span><span class="sxs-lookup"><span data-stu-id="49802-201">User attribution for bots messages</span></span> 

<span data-ttu-id="49802-202">ボットがユーザーの代わりにメッセージを送信するシナリオでは、そのユーザーにメッセージを割り当て、エンゲージメントを支援し、より自然な対話フローを示します。</span><span class="sxs-lookup"><span data-stu-id="49802-202">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="49802-203">この機能を使用すると、ボットからのメッセージを、そのメッセージが送信されたユーザーに属性付けできます。</span><span class="sxs-lookup"><span data-stu-id="49802-203">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="49802-204">次の図では、左側はユーザー属性のないボットによって送信されたカードメッセージで、右側はユーザー属性を持つボットによって送信された *カードです*。</span><span class="sxs-lookup"><span data-stu-id="49802-204">In the following image, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![スクリーンショット](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="49802-206">チームでユーザー属性を使用するには、Teams に送信されるペイロードにメンション エンティティ `OnBehalfOf` `ChannelData` `Activity` を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="49802-206">To use the user attribution in teams, you must  add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="49802-207">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="49802-207">C#/.NET</span></span>](#tab/dotnet-1)

```csharp
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }

```

# <a name="json"></a>[<span data-ttu-id="49802-208">JSON</span><span class="sxs-lookup"><span data-stu-id="49802-208">JSON</span></span>](#tab/json-1)

```json
{
    "text": "Hello World!",
    "ChannelData": {
        "OnBehalfOf": [{
            "itemid": 0,
            "mentionType": "person",
            "mri": "29:orgid:89e6508d-6c0f-4ffe-9f6a-b58416d965ae",
            "displayName": "Sowrabh N R S"
        }]
    }
}
```

* * *

<span data-ttu-id="49802-209">次のセクションでは、配列のエンティティについて `OnBehalfOf` 説明します。</span><span class="sxs-lookup"><span data-stu-id="49802-209">The following section is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="49802-210">エンティティ スキーマ  `OnBehalfOf` の詳細</span><span class="sxs-lookup"><span data-stu-id="49802-210">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="49802-211">フィールド</span><span class="sxs-lookup"><span data-stu-id="49802-211">Field</span></span>|<span data-ttu-id="49802-212">種類</span><span class="sxs-lookup"><span data-stu-id="49802-212">Type</span></span>|<span data-ttu-id="49802-213">説明</span><span class="sxs-lookup"><span data-stu-id="49802-213">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="49802-214">整数</span><span class="sxs-lookup"><span data-stu-id="49802-214">Integer</span></span>|<span data-ttu-id="49802-215">0 である必要があります。</span><span class="sxs-lookup"><span data-stu-id="49802-215">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="49802-216">String</span><span class="sxs-lookup"><span data-stu-id="49802-216">String</span></span>|<span data-ttu-id="49802-217">"person" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="49802-217">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="49802-218">String</span><span class="sxs-lookup"><span data-stu-id="49802-218">String</span></span>|<span data-ttu-id="49802-219">メッセージの代理としてメッセージが送信される人物のメッセージ リソース識別子 (KM)。</span><span class="sxs-lookup"><span data-stu-id="49802-219">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="49802-220">メッセージの送信者名は"via" として \<user\> 表示 \<bot name\> されます。</span><span class="sxs-lookup"><span data-stu-id="49802-220">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="49802-221">String</span><span class="sxs-lookup"><span data-stu-id="49802-221">String</span></span>|<span data-ttu-id="49802-222">人物の名前。</span><span class="sxs-lookup"><span data-stu-id="49802-222">Name of the person.</span></span> <span data-ttu-id="49802-223">名前解決が使用できない場合にフォールバックとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="49802-223">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="49802-224">次の手順</span><span class="sxs-lookup"><span data-stu-id="49802-224">Next Steps</span></span>

<span data-ttu-id="49802-225">検索コマンドを追加する</span><span class="sxs-lookup"><span data-stu-id="49802-225">Add a search command</span></span>

* [<span data-ttu-id="49802-226">検索コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="49802-226">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
