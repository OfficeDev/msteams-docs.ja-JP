---
title: タスクモジュール送信アクションに応答する
author: clearab
description: メッセージング拡張機能のアクションコマンドからタスクモジュール送信アクションに応答する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 82dad570bac096a9b2fb0d1fbada4ee70ca2a662
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867112"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="f7bc4-103">タスクモジュール送信アクションに応答する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="f7bc4-104">ユーザーがタスクモジュールを送信すると、web サービスは `composeExtension/submitAction` コマンド id とパラメーター値が設定された invoke メッセージを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-104">Once a user submits the task module, your web service will receive a `composeExtension/submitAction` invoke message with the command id and parameter values set.</span></span> <span data-ttu-id="f7bc4-105">アプリには、呼び出しに応答するための5秒があります。それ以外の場合、ユーザーは "アプリに到達できません" というエラーメッセージを受け取り、呼び出しへの応答は Teams クライアントによって無視されます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-105">Your app will have five seconds to respond to the invoke, otherwise the user will receive an "Unable to reach the app" error message, and any reply to the invoke will be ignored by the Teams client.</span></span>

<span data-ttu-id="f7bc4-106">応答するには、次のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-106">You have the following options for responding.</span></span>

* <span data-ttu-id="f7bc4-107">応答なし-送信アクションを使用して外部システムでプロセスをトリガーし、ユーザーにフィードバックを提供しないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="f7bc4-108">これは長時間実行されているプロセスで便利な場合があり、別の方法でフィードバックを提供することもできます (たとえば、[予防的なメッセージ](~/bots/how-to/conversations/send-proactive-messages.md)を使用して)。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="f7bc4-109">[別のタスクモジュール](#respond-with-another-task-module)-複数ステップの操作の一部として、追加のタスクモジュールで応答できます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="f7bc4-110">[カード応答](#respond-with-a-card-inserted-into-the-compose-message-area)-ユーザーがメッセージに操作したり、メッセージに挿入したりすることができるカードで応答できます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="f7bc4-111">[Bot からのアダプティブカード](#bot-response-with-adaptive-card)。会話にアダプティブカードを直接挿入します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="f7bc4-112">ユーザーの認証を要求する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="f7bc4-113">ユーザーに追加の構成を提供するよう要求する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="f7bc4-114">次の表は、メッセージング拡張機能の呼び出し場所 () に基づいて、使用可能な応答の種類を示して `commandContext` います。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-114">The table below shows which types of responses are available based on the invoke location (`commandContext`) of the messaging extension.</span></span> <span data-ttu-id="f7bc4-115">認証または構成の場合、ユーザーがフローを完了すると、元の呼び出しが web サービスに再送信されます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-115">For authentication or configuration, once the user completes the flow the original invoke will be re-sent to your web service.</span></span>

|<span data-ttu-id="f7bc4-116">応答の種類</span><span class="sxs-lookup"><span data-stu-id="f7bc4-116">Response Type</span></span> | <span data-ttu-id="f7bc4-117">hotmail</span><span class="sxs-lookup"><span data-stu-id="f7bc4-117">compose</span></span> | <span data-ttu-id="f7bc4-118">コマンド バー</span><span class="sxs-lookup"><span data-stu-id="f7bc4-118">command bar</span></span> | <span data-ttu-id="f7bc4-119">メッセージ​​</span><span class="sxs-lookup"><span data-stu-id="f7bc4-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="f7bc4-120">カード応答</span><span class="sxs-lookup"><span data-stu-id="f7bc4-120">Card response</span></span> | <span data-ttu-id="f7bc4-121">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-121">x</span></span> | <span data-ttu-id="f7bc4-122">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-122">x</span></span> | <span data-ttu-id="f7bc4-123">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-123">x</span></span> |
|<span data-ttu-id="f7bc4-124">別のタスクモジュール</span><span class="sxs-lookup"><span data-stu-id="f7bc4-124">Another task module</span></span> | <span data-ttu-id="f7bc4-125">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-125">x</span></span> | <span data-ttu-id="f7bc4-126">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-126">x</span></span> | <span data-ttu-id="f7bc4-127">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-127">x</span></span> |
|<span data-ttu-id="f7bc4-128">Adaptive Card 搭載ボット</span><span class="sxs-lookup"><span data-stu-id="f7bc4-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="f7bc4-129">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-129">x</span></span> |  | <span data-ttu-id="f7bc4-130">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-130">x</span></span> |
| <span data-ttu-id="f7bc4-131">応答なし</span><span class="sxs-lookup"><span data-stu-id="f7bc4-131">No response</span></span> | <span data-ttu-id="f7bc4-132">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-132">x</span></span> | <span data-ttu-id="f7bc4-133">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-133">x</span></span> | <span data-ttu-id="f7bc4-134">x</span><span class="sxs-lookup"><span data-stu-id="f7bc4-134">x</span></span> |

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="f7bc4-135">SubmitAction invoke イベント</span><span class="sxs-lookup"><span data-stu-id="f7bc4-135">The submitAction invoke event</span></span>

<span data-ttu-id="f7bc4-136">次に、呼び出しメッセージを受信する例を示します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-136">Below are examples of receiving the invoke message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f7bc4-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f7bc4-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f7bc4-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f7bc4-138">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="f7bc4-139">JSON</span><span class="sxs-lookup"><span data-stu-id="f7bc4-139">JSON</span></span>](#tab/json)

<span data-ttu-id="f7bc4-140">受け取る JSON オブジェクトの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-140">This is an example of the JSON object you will receive.</span></span> <span data-ttu-id="f7bc4-141">パラメーターは、 `commandContext` メッセージング拡張機能がどこからトリガーされたかを示します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-141">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="f7bc4-142">オブジェクトには、 `data` パラメーターとしてフォーム上のフィールドと、ユーザーが送信した値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-142">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="f7bc4-143">ここでは、JSON オブジェクトを短縮して、最も関連のあるフィールドを強調表示します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-143">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="f7bc4-144">メッセージの作成領域に挿入されたカードで応答する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-144">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="f7bc4-145">要求に応答する最も一般的な方法 `composeExtension/submitAction` は、[メッセージの作成] 領域に挿入されたカードです。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-145">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="f7bc4-146">ユーザーは、このカードを会話に送信するかどうかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-146">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="f7bc4-147">カードの使用の詳細については[、「カードおよびカードのアクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-147">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f7bc4-148">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f7bc4-148">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    dynamic Data = JObject.Parse(action.Data.ToString());
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var card = new HeroCard
    {
        Title = Data["formField1"] as string,
        Subtitle = Data["formField2"]  as string,
        Text = Data["formField3"]  as string,
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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f7bc4-149">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f7bc4-149">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f7bc4-150">JSON</span><span class="sxs-lookup"><span data-stu-id="f7bc4-150">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="f7bc4-151">別のタスクモジュールで応答する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-151">Respond with another task module</span></span>

<span data-ttu-id="f7bc4-152">追加のタスクモジュールを使用してイベントに応答することもでき `submitAction` ます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-152">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="f7bc4-153">これは、次のような場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-153">This can be useful when:</span></span>

* <span data-ttu-id="f7bc4-154">大量の情報を収集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-154">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="f7bc4-155">ユーザーの入力に基づいて収集している情報を動的に変更する必要がある場合</span><span class="sxs-lookup"><span data-stu-id="f7bc4-155">If you need to dynamically change what information you're collecting based on user input</span></span>
* <span data-ttu-id="f7bc4-156">ユーザーによって送信された情報を検証する必要があり、何らかの問題が発生した場合に、フォームを再送信してエラーメッセージが表示される可能性がある場合。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-156">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="f7bc4-157">応答のメソッドは、[最初の `fetchTask` イベントに応答する](~/messaging-extensions/how-to/action-commands/create-task-module.md)のと同じです。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-157">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="f7bc4-158">Bot フレームワーク SDK を使用している場合は、両方の送信アクションに対して同じイベントがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-158">If you're using the Bot Framework SDK the same event will trigger for both submit actions.</span></span> <span data-ttu-id="f7bc4-159">これは、正しい応答を決定するロジックを追加する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-159">This mean you need to be sure to add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="f7bc4-160">アダプティブカードを使用したボット応答</span><span class="sxs-lookup"><span data-stu-id="f7bc4-160">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="f7bc4-161">このフローでは、 `bot` アプリケーションマニフェストにオブジェクトを追加し、bot に対して必要なスコープが定義されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-161">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="f7bc4-162">Bot のメッセージング拡張機能と同じ Id を使用します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-162">Use the same Id as your messaging extension for your bot.</span></span>

<span data-ttu-id="f7bc4-163">また、サブカード付きのメッセージをボット付きのチャネルに挿入することによって、送信アクションに応答することもできます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-163">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="f7bc4-164">ユーザーは、メッセージを送信する前にプレビューでき、必要に応じて編集や操作を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-164">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="f7bc4-165">これは、アダプティブカード応答を作成する前にユーザーから情報を収集する必要がある場合や、カードを操作した後にカードを更新する必要がある場合に、非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-165">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response, or when you're going to need to update the card after someone interacts with it.</span></span> <span data-ttu-id="f7bc4-166">次のシナリオでは、アプリがこのフローをかなり使用して、チャネル会話に構成手順を含めずにポーリングを構成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-166">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation.</span></span>

1. <span data-ttu-id="f7bc4-167">ユーザーが [メッセージング] 拡張をクリックして、タスクモジュールをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-167">The user clicks the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="f7bc4-168">ユーザーは、タスクモジュールを使用してポーリングを構成します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-168">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="f7bc4-169">タスクモジュールを送信した後、アプリは提供された情報を使用して、投票をアダプティブカードとして作成し、クライアントへの応答として送信し `botMessagePreview` ます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-169">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="f7bc4-170">ユーザーは、カードをチャネルに挿入する前に、アダプティブカードメッセージをプレビューできます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-170">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="f7bc4-171">アプリがまだチャネルのメンバーではない場合は、をクリックするとそのアプリが `Send` 追加されます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-171">If the app is not already a member of the channel, clicking `Send` will add the it.</span></span>
   1. <span data-ttu-id="f7bc4-172">ユーザーはメッセージを選択して `Edit` 、元のタスクモジュールに返すこともできます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-172">The user can also chose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="f7bc4-173">アダプティブカードとの対話は、メッセージを送信する前に変更します。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-173">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="f7bc4-174">ユーザーがクリックすると、 `Send` メッセージがチャネルに投稿されます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-174">Once the user clicks `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="f7bc4-175">最初の送信アクションに応答する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-175">Respond to initial submit action</span></span>

<span data-ttu-id="f7bc4-176">このフローを有効にするには、タスクモジュールは、 `composeExtension/submitAction` bot がチャネルに送信するカードのプレビューを使用して、最初のメッセージに応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-176">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot will send to the channel.</span></span> <span data-ttu-id="f7bc4-177">これにより、ユーザーは送信前にカードを確認することができます。また、インストールされていない場合は、お客様が会話に bot をインストールしようとします。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-177">This gives the user the opportunity to verify the card before sending, and also will attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f7bc4-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f7bc4-178">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic Data = JObject.Parse(action.Data.ToString());
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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f7bc4-179">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f7bc4-179">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f7bc4-180">JSON</span><span class="sxs-lookup"><span data-stu-id="f7bc4-180">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="f7bc4-181">には、 `activityPreview` `message` 完全に1つのアダプティブカード添付ファイルがあるアクティビティが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-181">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="f7bc4-182">`<< Card Payload >>`値は、送信するカードのプレースホルダーです。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-182">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="f7bc4-183">BotMessagePreview send および edit イベント</span><span class="sxs-lookup"><span data-stu-id="f7bc4-183">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="f7bc4-184">メッセージの内線番号は、次の2つの新しい種類の呼び出しに応答する必要があり `composeExtension/submitAction` `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` ます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-184">Your message extension will now need to respond to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f7bc4-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f7bc4-185">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f7bc4-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f7bc4-186">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f7bc4-187">JSON</span><span class="sxs-lookup"><span data-stu-id="f7bc4-187">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="f7bc4-188">BotMessagePreview 編集に応答する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-188">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="f7bc4-189">ユーザーが [**編集**] ボタンをクリックして送信する前にカードを編集する場合は、という呼び出しを受け取り `composeExtension/submitAction` `value.botMessagePreviewAction = edit` ます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-189">If the user decides to edit the card before sending by clicking the **Edit** button, you will receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="f7bc4-190">通常、対話を開始した最初の呼び出しに応答して送信したタスクモジュールを返すことによって応答する必要があり `composeExtension/fetchTask` ます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-190">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="f7bc4-191">これにより、ユーザーは元の情報を再入力することで、処理を開始することができます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-191">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="f7bc4-192">また、ユーザーがすべての情報を最初から入力していないように、タスクモジュールを事前入力するために、現在使用可能な情報を使用することも検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-192">You should also consider using the information you now have available to pre-populate the task module so the user doesn't have fill out all of the information from scratch.</span></span>

<span data-ttu-id="f7bc4-193">「[最初の `fetchTask` イベントへの対応」を](~/messaging-extensions/how-to/action-commands/create-task-module.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-193">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="f7bc4-194">BotMessagePreview send に応答する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-194">Respond to botMessagePreview send</span></span>

<span data-ttu-id="f7bc4-195">ユーザーが [**送信**] ボタンをクリックすると、invoke with が表示され `composeExtension/submitAction` `value.botMessagePreviewAction = send` ます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-195">Once the user clicks the **Send** button, you will receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="f7bc4-196">Web サービスは、アダプティブカードを使用した予防的なメッセージを作成して会話に送信する必要があります。また、呼び出しに応答することもできます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-196">Your web service will need to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f7bc4-197">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f7bc4-197">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f7bc4-198">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f7bc4-198">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f7bc4-199">JSON</span><span class="sxs-lookup"><span data-stu-id="f7bc4-199">JSON</span></span>](#tab/json)

<span data-ttu-id="f7bc4-200">`composeExtension/submitAction`次のような新しいメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7bc4-200">You will receive a new `composeExtension/submitAction` message similar to the one below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f7bc4-201">次の手順</span><span class="sxs-lookup"><span data-stu-id="f7bc4-201">Next Steps</span></span>

<span data-ttu-id="f7bc4-202">検索コマンドを追加する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-202">Add a search command</span></span>

* [<span data-ttu-id="f7bc4-203">検索コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="f7bc4-203">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
