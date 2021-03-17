---
title: タスク モジュールの送信アクションに応答する
author: clearab
description: メッセージング拡張機能アクション コマンドからタスク モジュール送信アクションに応答する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fecc0ace5f767da3764529a9e8a590b37e547bb0
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827943"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="2ac4e-103">タスク モジュールの送信アクションに応答する</span><span class="sxs-lookup"><span data-stu-id="2ac4e-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="2ac4e-104">ユーザーがタスク モジュールを送信すると、Web サービスはコマンド ID とパラメーター値を含む呼び出し `composeExtension/submitAction` メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-104">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="2ac4e-105">アプリは呼び出しに応答するために **5** 秒を持っています。それ以外の場合、ユーザーはエラー メッセージを受け取りますアプリに到達できず、呼び出しに対する返信は Teams クライアントによって無視されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-105">Your app has five seconds to respond to the invoke, otherwise the user receives an error message **Unable to reach the app** and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="2ac4e-106">応答するオプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-106">You have the following options for responding:</span></span>

* <span data-ttu-id="2ac4e-107">応答なし - 送信アクションを使用して外部システムのプロセスをトリガーし、ユーザーにフィードバックを提供しない選択できます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="2ac4e-108">これは長時間実行されるプロセスに役立ちます。また、別の方法 (プロアクティブ メッセージなど) でフィードバックを [提供する場合があります](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="2ac4e-109">[別のタスク モジュール](#respond-with-another-task-module) - 複数ステップの操作の一環として、追加のタスク モジュールで応答できます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="2ac4e-110">[カードの](#respond-with-a-card-inserted-into-the-compose-message-area) 応答 - ユーザーがメッセージを操作したり、メッセージに挿入したりできるカードで応答できます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="2ac4e-111">[ボットからのアダプティブ カード](#bot-response-with-adaptive-card) - アダプティブ カードを会話に直接挿入します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="2ac4e-112">ユーザーの認証を要求する</span><span class="sxs-lookup"><span data-stu-id="2ac4e-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="2ac4e-113">ユーザーに追加の構成の提供を要求する</span><span class="sxs-lookup"><span data-stu-id="2ac4e-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="2ac4e-114">認証または構成の場合、ユーザーがフローを完了すると、元の呼び出しが Web サービスに再送信されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-114">For authentication or configuration, after the user completes the flow the original invoke is re-sent to your web service.</span></span> <span data-ttu-id="2ac4e-115">次の表に、メッセージング拡張機能の呼び出し場所に基づいて使用できる応答 `commandContext` の種類を示します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-115">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="2ac4e-116">応答の種類</span><span class="sxs-lookup"><span data-stu-id="2ac4e-116">Response Type</span></span> | <span data-ttu-id="2ac4e-117">compose</span><span class="sxs-lookup"><span data-stu-id="2ac4e-117">compose</span></span> | <span data-ttu-id="2ac4e-118">コマンド バー</span><span class="sxs-lookup"><span data-stu-id="2ac4e-118">command bar</span></span> | <span data-ttu-id="2ac4e-119">message</span><span class="sxs-lookup"><span data-stu-id="2ac4e-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="2ac4e-120">カードの応答</span><span class="sxs-lookup"><span data-stu-id="2ac4e-120">Card response</span></span> | <span data-ttu-id="2ac4e-121">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-121">x</span></span> | <span data-ttu-id="2ac4e-122">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-122">x</span></span> | <span data-ttu-id="2ac4e-123">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-123">x</span></span> |
|<span data-ttu-id="2ac4e-124">別のタスク モジュール</span><span class="sxs-lookup"><span data-stu-id="2ac4e-124">Another task module</span></span> | <span data-ttu-id="2ac4e-125">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-125">x</span></span> | <span data-ttu-id="2ac4e-126">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-126">x</span></span> | <span data-ttu-id="2ac4e-127">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-127">x</span></span> |
|<span data-ttu-id="2ac4e-128">アダプティブ カードを使用したボット</span><span class="sxs-lookup"><span data-stu-id="2ac4e-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="2ac4e-129">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-129">x</span></span> |  | <span data-ttu-id="2ac4e-130">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-130">x</span></span> |
| <span data-ttu-id="2ac4e-131">応答なし</span><span class="sxs-lookup"><span data-stu-id="2ac4e-131">No response</span></span> | <span data-ttu-id="2ac4e-132">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-132">x</span></span> | <span data-ttu-id="2ac4e-133">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-133">x</span></span> | <span data-ttu-id="2ac4e-134">x</span><span class="sxs-lookup"><span data-stu-id="2ac4e-134">x</span></span> |

> [!NOTE]
> * <span data-ttu-id="2ac4e-135">**[Action.Submit** through ME] カードを選択すると、その値が通常のペイロードと等しい名前 **の composeExtension** を持つ呼び出しアクティビティが送信されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-135">When you select **Action.Submit** through ME cards, it sends invoke activity with the name **composeExtension**, where the value is equal to the usual payload.</span></span>
> * <span data-ttu-id="2ac4e-136">**[Action.Submit** through conversation] を選択すると、onCardButtonClicked という名前のメッセージ アクティビティが表示され、値は通常のペイロードと等しくなります。 </span><span class="sxs-lookup"><span data-stu-id="2ac4e-136">When you select **Action.Submit** through conversation, you receive message activity with the name **onCardButtonClicked**, where the value is equal to the usual payload.</span></span>

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="2ac4e-137">submitAction 呼び出しイベント</span><span class="sxs-lookup"><span data-stu-id="2ac4e-137">The submitAction invoke event</span></span>

<span data-ttu-id="2ac4e-138">呼び出しメッセージを受信する例は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-138">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2ac4e-139">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2ac4e-139">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="2ac4e-140">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="2ac4e-140">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="2ac4e-141">JSON</span><span class="sxs-lookup"><span data-stu-id="2ac4e-141">JSON</span></span>](#tab/json)

<span data-ttu-id="2ac4e-142">これは、受信する JSON オブジェクトの例です。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-142">This is an example of the JSON object you receive.</span></span> <span data-ttu-id="2ac4e-143">パラメーター `commandContext` は、メッセージング拡張機能がトリガーされた場所を示します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-143">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="2ac4e-144">オブジェクト `data` には、パラメーターとしてフォームのフィールドと、ユーザーが送信した値が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-144">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="2ac4e-145">ここでの JSON オブジェクトは、最も関連性の高いフィールドを強調表示するために短縮されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-145">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="2ac4e-146">作成メッセージ領域にカードを挿入して応答する</span><span class="sxs-lookup"><span data-stu-id="2ac4e-146">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="2ac4e-147">要求に応答する最も一般的な方法は、作成メッセージ領域にカード `composeExtension/submitAction` を挿入する方法です。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-147">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="2ac4e-148">その後、ユーザーは会話にカードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-148">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="2ac4e-149">カードの使用の詳細については、「カードと [カードのアクション」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-149">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2ac4e-150">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2ac4e-150">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="2ac4e-151">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="2ac4e-151">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="2ac4e-152">JSON</span><span class="sxs-lookup"><span data-stu-id="2ac4e-152">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="2ac4e-153">別のタスク モジュールで応答する</span><span class="sxs-lookup"><span data-stu-id="2ac4e-153">Respond with another task module</span></span>

<span data-ttu-id="2ac4e-154">追加のタスク モジュールを使用して `submitAction` イベントに応答できます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-154">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="2ac4e-155">これは、次の場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-155">This can be useful when:</span></span>

* <span data-ttu-id="2ac4e-156">大量の情報を収集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-156">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="2ac4e-157">ユーザー入力に基づいて収集する情報を動的に変更する必要がある場合</span><span class="sxs-lookup"><span data-stu-id="2ac4e-157">If you need to dynamically change what information you are collecting based on user input</span></span>
* <span data-ttu-id="2ac4e-158">ユーザーが送信した情報を検証し、何か問題が発生した場合にエラー メッセージを表示してフォームを再送信する必要がある場合。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-158">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="2ac4e-159">応答のメソッドは、最初のイベント [に応答する方法と同 `fetchTask` じです](~/messaging-extensions/how-to/action-commands/create-task-module.md)。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-159">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="2ac4e-160">Bot Framework SDK を使用している場合は、両方の送信アクションに対して同じイベント トリガーが発生します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-160">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="2ac4e-161">つまり、正しい応答を決定するロジックを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-161">This means you must add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="2ac4e-162">アダプティブ カードを使用したボットの応答</span><span class="sxs-lookup"><span data-stu-id="2ac4e-162">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="2ac4e-163">このフローでは、アプリ マニフェストにオブジェクトを追加し、ボットに必要なスコープを定義 `bot` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-163">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="2ac4e-164">ボットのメッセージング拡張機能と同じ ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-164">Use the same ID as your messaging extension for your bot.</span></span>

<span data-ttu-id="2ac4e-165">送信アクションに応答するには、アダプティブ カードを含むメッセージをボットを使用してチャネルに挿入します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-165">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="2ac4e-166">ユーザーは、メッセージを送信する前にプレビューし、メッセージを編集したり操作したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-166">Your user can preview the message before submitting it, and potentially edit or interact with it as well.</span></span> <span data-ttu-id="2ac4e-167">これは、アダプティブ カード応答を作成する前にユーザーから情報を収集するシナリオや、ユーザーがカードを操作した後にカードを更新する場合に非常に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-167">This can be very useful in scenarios where you gather information from your users before creating an adaptive card response, or when you update the card after someone interacts with it.</span></span> <span data-ttu-id="2ac4e-168">次のシナリオは、アプリ Polly がチャネル会話に構成手順を含めずに、このフローを使用してポーリングを構成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-168">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation:</span></span>

1. <span data-ttu-id="2ac4e-169">ユーザーがメッセージング拡張機能を選択して、タスク モジュールをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-169">The user selects the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="2ac4e-170">ユーザーは、タスク モジュールを使用してポーリングを構成します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-170">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="2ac4e-171">タスク モジュールを送信した後、アプリは提供された情報を使用して、アダプティブ カードとしてポーリングを構築し、それをクライアントに応答 `botMessagePreview` として送信します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-171">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="2ac4e-172">その後、ボットがチャネルに挿入する前に、アダプティブ カード メッセージをプレビューできます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-172">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="2ac4e-173">アプリがチャネルのメンバーではない場合は、選択すると追加 `Send` されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-173">If the app is not already a member of the channel, selecting `Send` adds it.</span></span>
   1. <span data-ttu-id="2ac4e-174">ユーザーはメッセージを選択して、元のタスク モジュール `Edit` に返します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-174">The user can also choose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="2ac4e-175">アダプティブ カードを操作すると、メッセージを送信する前に変更されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-175">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="2ac4e-176">ユーザーがボットを選択 `Send` すると、メッセージがチャネルに投稿されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-176">After the user selects `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="2ac4e-177">最初の送信アクションに応答する</span><span class="sxs-lookup"><span data-stu-id="2ac4e-177">Respond to initial submit action</span></span>

<span data-ttu-id="2ac4e-178">このフローを有効にするには、ボットがチャネルに送信するカードのプレビューを使用して、タスク モジュールが最初のメッセージ `composeExtension/submitAction` に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-178">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot send to the channel.</span></span> <span data-ttu-id="2ac4e-179">これにより、ユーザーは送信する前にカードを確認し、ボットがインストールされていない場合は会話にボットをインストールする機会も与えます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-179">This gives the user the opportunity to verify the card before sending, and also attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2ac4e-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2ac4e-180">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="2ac4e-181">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="2ac4e-181">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="2ac4e-182">JSON</span><span class="sxs-lookup"><span data-stu-id="2ac4e-182">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="2ac4e-183">アダプティブ `activityPreview` カードの添付ファイル `message` が 1 つのアクティビティを含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-183">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="2ac4e-184">この `<< Card Payload >>` 値は、送信するカードのプレースホルダーです。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-184">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="2ac4e-185">botMessagePreview 送信イベントと編集イベント</span><span class="sxs-lookup"><span data-stu-id="2ac4e-185">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="2ac4e-186">メッセージ拡張機能は、2 つの新しい種類の呼び出しに今すぐ応答する `composeExtension/submitAction` 必要があります。where と `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="2ac4e-186">Your message extension must respond now to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2ac4e-187">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2ac4e-187">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="2ac4e-188">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="2ac4e-188">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="2ac4e-189">JSON</span><span class="sxs-lookup"><span data-stu-id="2ac4e-189">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="2ac4e-190">botMessagePreview 編集に応答する</span><span class="sxs-lookup"><span data-stu-id="2ac4e-190">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="2ac4e-191">ユーザーが [編集] ボタンを選択して送信する前にカードを編集すると、で呼び出しを `composeExtension/submitAction` 受け取る `value.botMessagePreviewAction = edit` 。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-191">If the user edits the card before sending by selecting the **Edit** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="2ac4e-192">通常、対話を開始した最初の呼び出しに応答して送信したタスク モジュール `composeExtension/fetchTask` を返して応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-192">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="2ac4e-193">これにより、ユーザーは元の情報を再入力してプロセスを開始できます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-193">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="2ac4e-194">使用可能な情報を使用して、ユーザーがすべての情報を最初から入力する必要が生じないので、タスク モジュールに事前入力します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-194">Use the available information to pre-populate the task module so the user does not have to fill out all of the information from scratch.</span></span>

<span data-ttu-id="2ac4e-195">「 [初期イベントへの応答」を `fetchTask` 参照してください](~/messaging-extensions/how-to/action-commands/create-task-module.md)。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-195">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="2ac4e-196">botMessagePreview 送信に応答する</span><span class="sxs-lookup"><span data-stu-id="2ac4e-196">Respond to botMessagePreview send</span></span>

<span data-ttu-id="2ac4e-197">ユーザーが [送信] ボタンを **選択すると** 、呼び出しが `composeExtension/submitAction` 表示されます `value.botMessagePreviewAction = send` 。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-197">After the user selects the **Send** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="2ac4e-198">Web サービスでは、アダプティブ カードを含むプロアクティブ メッセージを作成して会話に送信し、呼び出しに返信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-198">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2ac4e-199">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2ac4e-199">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="2ac4e-200">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="2ac4e-200">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="2ac4e-201">JSON</span><span class="sxs-lookup"><span data-stu-id="2ac4e-201">JSON</span></span>](#tab/json)

<span data-ttu-id="2ac4e-202">次のような新しい `composeExtension/submitAction` メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-202">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="2ac4e-203">ボット メッセージのユーザー属性</span><span class="sxs-lookup"><span data-stu-id="2ac4e-203">User attribution for bots messages</span></span> 

<span data-ttu-id="2ac4e-204">ボットがユーザーに代わってメッセージを送信するシナリオでは、メッセージをそのユーザーに帰属すると、エンゲージメントに役立ち、より自然な対話フローを紹介できます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-204">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="2ac4e-205">この機能を使用すると、ボットから送信されたユーザーにメッセージを属性付けできます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-205">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="2ac4e-206">次の図では、左側はユーザー属性なしでボットから送信されたカードメッセージで、右側はユーザー属性を持つボット *によって送信された* カードです。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-206">In the following image, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![スクリーンショット](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="2ac4e-208">Teams でユーザー属性を使用するには、Teams に送信されるペイロードにメンション `OnBehalfOf` `ChannelData` `Activity` エンティティを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-208">To use the user attribution in teams, you must  add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2ac4e-209">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2ac4e-209">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="2ac4e-210">JSON</span><span class="sxs-lookup"><span data-stu-id="2ac4e-210">JSON</span></span>](#tab/json-1)

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

<span data-ttu-id="2ac4e-211">次のセクションでは、Array のエンティティの `OnBehalfOf` 説明を示します。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-211">The following section is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="2ac4e-212">エンティティ スキーマ  `OnBehalfOf` の詳細</span><span class="sxs-lookup"><span data-stu-id="2ac4e-212">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="2ac4e-213">Field</span><span class="sxs-lookup"><span data-stu-id="2ac4e-213">Field</span></span>|<span data-ttu-id="2ac4e-214">種類</span><span class="sxs-lookup"><span data-stu-id="2ac4e-214">Type</span></span>|<span data-ttu-id="2ac4e-215">説明</span><span class="sxs-lookup"><span data-stu-id="2ac4e-215">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="2ac4e-216">整数</span><span class="sxs-lookup"><span data-stu-id="2ac4e-216">Integer</span></span>|<span data-ttu-id="2ac4e-217">0 である必要があります</span><span class="sxs-lookup"><span data-stu-id="2ac4e-217">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="2ac4e-218">文字列</span><span class="sxs-lookup"><span data-stu-id="2ac4e-218">String</span></span>|<span data-ttu-id="2ac4e-219">"人" である必要があります</span><span class="sxs-lookup"><span data-stu-id="2ac4e-219">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="2ac4e-220">文字列</span><span class="sxs-lookup"><span data-stu-id="2ac4e-220">String</span></span>|<span data-ttu-id="2ac4e-221">メッセージが送信されたユーザーのメッセージ リソース識別子 (MRI)。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-221">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="2ac4e-222">メッセージ送信者名は "via" として \<user\> 表示 \<bot name\> されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-222">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="2ac4e-223">文字列</span><span class="sxs-lookup"><span data-stu-id="2ac4e-223">String</span></span>|<span data-ttu-id="2ac4e-224">ユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-224">Name of the person.</span></span> <span data-ttu-id="2ac4e-225">名前解決が使用できない場合にフォールバックとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="2ac4e-225">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="2ac4e-226">次の手順</span><span class="sxs-lookup"><span data-stu-id="2ac4e-226">Next Steps</span></span>

<span data-ttu-id="2ac4e-227">検索コマンドの追加</span><span class="sxs-lookup"><span data-stu-id="2ac4e-227">Add a search command</span></span>

* [<span data-ttu-id="2ac4e-228">検索コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="2ac4e-228">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
