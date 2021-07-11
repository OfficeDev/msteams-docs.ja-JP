---
title: ボットにカード アクションを追加する
description: Microsoft Teams のカード アクションと、ボットでの使用方法について説明します。
localization_priority: Normal
ms.topic: conceptual
keywords: チーム ボット カード アクション
ms.openlocfilehash: 4af152f6179785687d4fd7371d202c56e1aee170
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254203"
---
# <a name="card-actions"></a><span data-ttu-id="de201-104">カード アクション</span><span class="sxs-lookup"><span data-stu-id="de201-104">Card actions</span></span>

<span data-ttu-id="de201-105">Teams のボットやメッセージング拡張機能で使用されるカードは、以下のアクティビティ [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) タイプをサポートします。</span><span class="sxs-lookup"><span data-stu-id="de201-105">Cards used by bots and messaging extensions in Teams support the following activity [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) types:</span></span>

> [!NOTE]
> <span data-ttu-id="de201-106">`CardAction` アクションは、コネクタから使用する場合、Office 365 コネクタ カード向けの `potentialActions` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="de201-106">The `CardAction` actions differ from `potentialActions` for Office 365 Connector cards when used from connectors.</span></span>

| <span data-ttu-id="de201-107">タイプ</span><span class="sxs-lookup"><span data-stu-id="de201-107">Type</span></span> | <span data-ttu-id="de201-108">操作</span><span class="sxs-lookup"><span data-stu-id="de201-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="de201-109">URL を既定のブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="de201-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="de201-110">ボタンを選択するか、またはカードをタップしたユーザーからのメッセージおよびペイロードをボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="de201-110">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="de201-111">別のメッセージをチャット ストリームに送信します。</span><span class="sxs-lookup"><span data-stu-id="de201-111">Sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="de201-112">ボタンを選択するか、またはカードをタップしたユーザーからのメッセージをボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="de201-112">Sends a message to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="de201-113">ユーザーからボットに送信されたこのメッセージは、すべての会話参加者に表示されます。</span><span class="sxs-lookup"><span data-stu-id="de201-113">This message from user to bot is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="de201-114">ボタンを選択するか、またはカードをタップしたユーザーからのメッセージおよびペイロードをボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="de201-114">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="de201-115">このメッセージは表示されません。</span><span class="sxs-lookup"><span data-stu-id="de201-115">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="de201-116">OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。</span><span class="sxs-lookup"><span data-stu-id="de201-116">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="de201-117">Teams は、前のテーブルに記載されていない `CardAction` タイプをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="de201-117">Teams does not support `CardAction` types not listed in the previous table.</span></span>
>* <span data-ttu-id="de201-118">Teams は `potentialActions` プロパティをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="de201-118">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="de201-119">カード アクションは、Bot Framework や Azure Bot Service の[おすすめの操作](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true)とは異なります。</span><span class="sxs-lookup"><span data-stu-id="de201-119">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework or Azure Bot Service.</span></span> <span data-ttu-id="de201-120">おすすめの操作は、Microsoft Teams ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="de201-120">Suggested actions are not supported in Microsoft Teams.</span></span> <span data-ttu-id="de201-121">Teams ボット メッセージにボタンを表示させる場合は、カードを使用します。</span><span class="sxs-lookup"><span data-stu-id="de201-121">If you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="de201-122">カード アクションをメッセージング拡張機能の一部として使用している場合、カードがチャネルに送信されるまでアクションは機能しません。</span><span class="sxs-lookup"><span data-stu-id="de201-122">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="de201-123">カードがメッセージの作成ボックスに入っている間は、アクションは機能しません。</span><span class="sxs-lookup"><span data-stu-id="de201-123">The actions do not work while the card is in the compose message box.</span></span>

## <a name="action-type-openurl"></a><span data-ttu-id="de201-124">アクション タイプ openUrl</span><span class="sxs-lookup"><span data-stu-id="de201-124">Action type openUrl</span></span>

<span data-ttu-id="de201-125">`openUrl` アクション タイプでは、既定のブラウザーで起動する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="de201-125">`openUrl` action type specifies a URL to launch in the default browser.</span></span>

> [!NOTE]
> <span data-ttu-id="de201-126">どのボタンが選択されたかの通知は、ボットでは受信しません。</span><span class="sxs-lookup"><span data-stu-id="de201-126">Your bot does not receive any notice on which button was selected.</span></span>

<span data-ttu-id="de201-127">`openUrl` を使用すると、以下のプロパティを含むアクションを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="de201-127">With `openUrl`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="de201-128">プロパティ</span><span class="sxs-lookup"><span data-stu-id="de201-128">Property</span></span> | <span data-ttu-id="de201-129">説明</span><span class="sxs-lookup"><span data-stu-id="de201-129">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="de201-130">ボタンのラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="de201-130">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="de201-131">このフィールドには、完全でかつ適切に形成された URL が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="de201-131">This field must contain a full and properly formed URL.</span></span> |

# <a name="json"></a>[<span data-ttu-id="de201-132">JSON</span><span class="sxs-lookup"><span data-stu-id="de201-132">JSON</span></span>](#tab/json)

<span data-ttu-id="de201-133">次のコードは JSON での `openUrl` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-133">The following code shows an example of `openUrl` action type in JSON:</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[<span data-ttu-id="de201-134">C#</span><span class="sxs-lookup"><span data-stu-id="de201-134">C#</span></span>](#tab/csharp)

<span data-ttu-id="de201-135">次のコードは C# での `openUrl` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-135">The following code shows an example of `openUrl` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="de201-136">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="de201-136">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="de201-137">次のコードは JavaScript での `openUrl` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-137">The following code shows an example of `openUrl` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a><span data-ttu-id="de201-138">アクション タイプ messageBack</span><span class="sxs-lookup"><span data-stu-id="de201-138">Action type messageBack</span></span>

<span data-ttu-id="de201-139">`messageBack` を使用すると、以下のプロパティを含む完全にカスタマイズされたアクションを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="de201-139">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="de201-140">プロパティ</span><span class="sxs-lookup"><span data-stu-id="de201-140">Property</span></span> | <span data-ttu-id="de201-141">説明</span><span class="sxs-lookup"><span data-stu-id="de201-141">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="de201-142">ボタンのラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="de201-142">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="de201-143">省略可能。</span><span class="sxs-lookup"><span data-stu-id="de201-143">Optional.</span></span> <span data-ttu-id="de201-144">アクションが実行されたときに、チャット ストリームでユーザーが使用します。</span><span class="sxs-lookup"><span data-stu-id="de201-144">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="de201-145">このテキストは、お使いのボットには送信されません。</span><span class="sxs-lookup"><span data-stu-id="de201-145">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="de201-146">アクションが実行された場合に、ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="de201-146">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="de201-147">固有の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードすることができます。</span><span class="sxs-lookup"><span data-stu-id="de201-147">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="de201-148">アクションが実行された場合に、ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="de201-148">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="de201-149">このプロパティを使用して、ボット開発を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="de201-149">Use this property to simplify bot development.</span></span> <span data-ttu-id="de201-150">コードでは、トップレベルのプロパティをチェックして、ボット ロジックをディスパッチすることができます。</span><span class="sxs-lookup"><span data-stu-id="de201-150">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="de201-151">`messageBack` の柔軟性は、`displayText` を使用しないだけでは、コードが視覚的なユーザー メッセージを履歴に残すことができないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="de201-151">The flexibility of `messageBack` means that your code cannot leave a visible user message in the history simply by not using `displayText`.</span></span>

# <a name="json"></a>[<span data-ttu-id="de201-152">JSON</span><span class="sxs-lookup"><span data-stu-id="de201-152">JSON</span></span>](#tab/json)

<span data-ttu-id="de201-153">次のコードは JSON での `messageBack` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-153">The following code shows an example of `messageBack` action type in JSON:</span></span>

```json
{
  "buttons": [
    {
    "type": "messageBack",
    "title": "My MessageBack button",
    "displayText": "I clicked this button",
    "text": "User just clicked the MessageBack button",
    "value": "{\"property\": \"propertyValue\" }"
    }
  ]
}
```

<span data-ttu-id="de201-154">`value` プロパティには、シリアル化された JSON 文字列または JSON オブジェクトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="de201-154">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

# <a name="c"></a>[<span data-ttu-id="de201-155">C#</span><span class="sxs-lookup"><span data-stu-id="de201-155">C#</span></span>](#tab/csharp)

<span data-ttu-id="de201-156">次のコードは C# での `messageBack` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-156">The following code shows an example of `messageBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.MessageBack,
    Title = "My MessageBack button",
    DisplayText = "I clicked this button",
    Text = "User just clicked the MessageBack button",
    Value = "{\"property\": \"propertyValue\" }"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="de201-157">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="de201-157">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="de201-158">次のコードは JavaScript での `messageBack` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-158">The following code shows an example of `messageBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'messageBack',
    title: "My MessageBack button",
    displayText: "I clicked this button",
    text: "User just clicked the MessageBack button",
    value: {property: "propertyValue" }
}])
```

---

### <a name="inbound-message-example"></a><span data-ttu-id="de201-159">受信メッセージの例</span><span class="sxs-lookup"><span data-stu-id="de201-159">Inbound message example</span></span>

<span data-ttu-id="de201-160">`replyToId` には、カード アクションの発信元であるメッセージ ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="de201-160">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="de201-161">これは、メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="de201-161">Use it if you want to update the message.</span></span>

<span data-ttu-id="de201-162">以下のコードは、受信メッセージの一例を示しています。</span><span class="sxs-lookup"><span data-stu-id="de201-162">The following code shows an example of inbound message:</span></span>

```json
{
   "text":"User just clicked the MessageBack button",
   "value":{
      "property":"propertyValue"
   },
   "type":"message",
   "timestamp":"2017-06-22T22:38:47.407Z",
   "id":"f:5261769396935243054",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:102jd210jd010icsoaeclaejcoa9ue09u",
      "name":"John Smith"
   },
   "conversation":{
      "id":"19:malejcou081i20ojmlcau0@thread.skype;messageid=1498171086622"
   },
   "recipient":{
      "id":"28:76096e45-119f-4736-859c-6dfff54395f7",
      "name":"MyBot"
   },
   "entities":[
      {
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo" 
      }
   ],
   "channelData":{
      "channel":{
         "id":"19:malejcou081i20ojmlcau0@thread.skype"
      },
      "team":{
         "id":"19:12d021jdoijsaeoaue0u@thread.skype"
      },
      "tenant":{
         "id":"bec8e231-67ad-484e-87f4-3e5438390a77"
      }
   },
        "replyToId": "1575667808184",
}
```

## <a name="action-type-imback"></a><span data-ttu-id="de201-163">アクション タイプ imBack</span><span class="sxs-lookup"><span data-stu-id="de201-163">Action type imBack</span></span>

<span data-ttu-id="de201-164">`imBack` アクションは、ユーザーが通常のチャット メッセージで入力した場合のように、ボットへの返信メッセージをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="de201-164">The `imBack` action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="de201-165">ユーザーおよびチャネル内の他のすべてのユーザーがボタンの応答を確認することができます。</span><span class="sxs-lookup"><span data-stu-id="de201-165">Your user and all other users in a channel can see the button response.</span></span>

<span data-ttu-id="de201-166">`imBack` を使用すると、以下のプロパティを含むアクションを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="de201-166">With `imBack`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="de201-167">プロパティ</span><span class="sxs-lookup"><span data-stu-id="de201-167">Property</span></span> | <span data-ttu-id="de201-168">説明</span><span class="sxs-lookup"><span data-stu-id="de201-168">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="de201-169">ボタンのラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="de201-169">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="de201-170">このフィールドには、チャットで使用されるテキスト文字列が含まれている必要があるため、ボットに送り返されます。</span><span class="sxs-lookup"><span data-stu-id="de201-170">This field must contain the text string used in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="de201-171">これは、ボットで目的のロジックを実行するために処理するメッセージ テキストです。</span><span class="sxs-lookup"><span data-stu-id="de201-171">This is the message text you process in your bot to perform the desired logic.</span></span> |

> [!NOTE]
> <span data-ttu-id="de201-172">`value` フィールドはシンプルな文字列です。</span><span class="sxs-lookup"><span data-stu-id="de201-172">The `value` field is a simple string.</span></span> <span data-ttu-id="de201-173">書式設定や隠し文字のサポートはありません。</span><span class="sxs-lookup"><span data-stu-id="de201-173">There is no support for formatting or hidden characters.</span></span>

# <a name="json"></a>[<span data-ttu-id="de201-174">JSON</span><span class="sxs-lookup"><span data-stu-id="de201-174">JSON</span></span>](#tab/json)

<span data-ttu-id="de201-175">次のコードは JSON での `imBack` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-175">The following code shows an example of `imBack` action type in JSON:</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[<span data-ttu-id="de201-176">C#</span><span class="sxs-lookup"><span data-stu-id="de201-176">C#</span></span>](#tab/csharp)

<span data-ttu-id="de201-177">次のコードは C# での `imBack` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-177">The following code shows an example of `imBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="de201-178">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="de201-178">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="de201-179">次のコードは JavaScript での `imBack` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-179">The following code shows an example of `imBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a><span data-ttu-id="de201-180">アクション タイプ invoke</span><span class="sxs-lookup"><span data-stu-id="de201-180">Action type invoke</span></span>

<span data-ttu-id="de201-181">`invoke` アクションは、[タスク モジュール](~/task-modules-and-cards/task-modules/task-modules-bots.md)を起動するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="de201-181">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="de201-182">`invoke` アクションには、`type`、`title`、`value` の 3 つのプロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="de201-182">The `invoke` action contains three properties, `type`, `title`, and `value`.</span></span>

<span data-ttu-id="de201-183">`invoke` を使用すると、以下のプロパティを含むアクションを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="de201-183">With `invoke`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="de201-184">プロパティ</span><span class="sxs-lookup"><span data-stu-id="de201-184">Property</span></span> | <span data-ttu-id="de201-185">説明</span><span class="sxs-lookup"><span data-stu-id="de201-185">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="de201-186">ボタンのラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="de201-186">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="de201-187">このプロパティには、文字列、文字列化された JSON オブジェクト、または JSON オブジェクトを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="de201-187">This property can contain a string, a stringified JSON object, or a JSON object.</span></span> |

# <a name="json"></a>[<span data-ttu-id="de201-188">JSON</span><span class="sxs-lookup"><span data-stu-id="de201-188">JSON</span></span>](#tab/json)

<span data-ttu-id="de201-189">次のコードは JSON での `invoke` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-189">The following code shows an example of `invoke` action type in JSON:</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="de201-190">ユーザーがボタンを選択した場合、ボットはいくつかの追加情報を含む `value` オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="de201-190">When a user selects the button, your bot receives the `value` object with some additional information.</span></span>

> [!NOTE]
> <span data-ttu-id="de201-191">アクティビティ タイプは、`activity.Type == "invoke"` である `message` の代わりに `invoke` です。</span><span class="sxs-lookup"><span data-stu-id="de201-191">The activity type is `invoke` instead of `message` that is `activity.Type == "invoke"`.</span></span>

# <a name="c"></a>[<span data-ttu-id="de201-192">C#</span><span class="sxs-lookup"><span data-stu-id="de201-192">C#</span></span>](#tab/csharp)

<span data-ttu-id="de201-193">次のコードは C# での `invoke` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-193">The following code shows an example of `invoke` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="de201-194">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="de201-194">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="de201-195">次のコードは Node.js での `invoke` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-195">The following code shows an example of `invoke` action type in Node.js:</span></span>

```javascript
CardFactory.actions([
{
    type: "invoke",
    title: "Option 1",
    value: {
        option: "opt1"
    }
}])
```

---

### <a name="example-of-incoming-invoke-message"></a><span data-ttu-id="de201-196">受信した起動メッセージの例</span><span class="sxs-lookup"><span data-stu-id="de201-196">Example of incoming invoke message</span></span>

<span data-ttu-id="de201-197">上位の `replyToId` プロパティには、カード アクションの発信元であるメッセージ ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="de201-197">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="de201-198">これは、メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="de201-198">Use it if you want to update the message.</span></span>

<span data-ttu-id="de201-199">以下のコードは、受信する起動メッセージの一例を示しています。</span><span class="sxs-lookup"><span data-stu-id="de201-199">The following code shows an example of incoming invoke message:</span></span>

```json
{
    "type": "invoke",
    "value": {
        "option": "opt1"
    },
    "timestamp": "2017-02-10T04:11:19.614Z",
    "localTimestamp": "2017-02-09T21:11:19.614-07:00",
    "id": "f:6894910862892785420",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1Eniglq0-uVL83xNB9GU6w_G5a4SZF0gcJLprZzhtEbel21G_5h-
    NgoprRw45mP0AXUIZVeqrsIHSYV4ntgfVJQ",
        "name": "John Doe"
    },
    "conversation": {
        "id": "19:97b1ec61-45bf-453c-9059-6e8984e0cef4_8d88f59b-ae61-4300-bec0-caace7d28446@unq.gbl.spaces"
    },
    "recipient": {
        "id": "28:8d88f59b-ae61-4300-bec0-caace7d28446",
        "name": "MyBot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Web",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "channel": {
            "id": "19:dc5ba12695be4eb7bf457cad6b4709eb@thread.skype"
        },
        "team": {
            "id": "19:712c61d0ef384e5fa681ba90ca943398@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

## <a name="action-type-signin"></a><span data-ttu-id="de201-200">アクション タイプ signin</span><span class="sxs-lookup"><span data-stu-id="de201-200">Action type signin</span></span>

<span data-ttu-id="de201-201">`signin`アクション タイプは、ボットがセキュリティで保護されたサービスに接続することを許可する OAuth フローを開始します。</span><span class="sxs-lookup"><span data-stu-id="de201-201">`signin` action type initiates an OAuth flow that permits bots to connect with secure services.</span></span> <span data-ttu-id="de201-202">詳細については、「[ボットでの認証フロー](~/bots/how-to/authentication/auth-flow-bot.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="de201-202">For more information, see [authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="de201-203">また、Teams は、アダプティブ カードでのみ使用される[アダプティブ カード アクション](#adaptive-cards-actions)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="de201-203">Teams also supports [Adaptive Cards actions](#adaptive-cards-actions) that are only used by Adaptive Cards.</span></span>

# <a name="json"></a>[<span data-ttu-id="de201-204">JSON</span><span class="sxs-lookup"><span data-stu-id="de201-204">JSON</span></span>](#tab/json)

<span data-ttu-id="de201-205">次のコードは JSON での `signin` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-205">The following code shows an example of `signin` action type in JSON:</span></span>

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[<span data-ttu-id="de201-206">C#</span><span class="sxs-lookup"><span data-stu-id="de201-206">C#</span></span>](#tab/csharp)

<span data-ttu-id="de201-207">次のコードは C# での `signin` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-207">The following code shows an example of `signin` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="de201-208">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="de201-208">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="de201-209">次のコードは JavaScript での `signin` アクション タイプの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-209">The following code shows an example of `signin` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a><span data-ttu-id="de201-210">アダプティブ カード アクション</span><span class="sxs-lookup"><span data-stu-id="de201-210">Adaptive Cards actions</span></span>

<span data-ttu-id="de201-211">アダプティブ カードは、次の 4 つのアクション タイプをサポートします。</span><span class="sxs-lookup"><span data-stu-id="de201-211">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="de201-212">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="de201-212">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="de201-213">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="de201-213">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="de201-214">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="de201-214">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="de201-215">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="de201-215">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="de201-216">アダプティブ カード `Action.Submit`のペイロードを変更して、`Action.Submit` の `data` オブジェクトで `msteams` プロパティを使用して、既存の Bot Framework アクションをサポートすることもできます。</span><span class="sxs-lookup"><span data-stu-id="de201-216">You can also modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using an `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="de201-217">次のセクションでは、既存の Bot Framework アクションをアダプティブ カードで使用する方法について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="de201-217">The next section provide details on how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="de201-218">Bot Framework アクションを含むデータに `msteams` を追加しても、アダプティブ カード タスク モジュールでは動作しません。</span><span class="sxs-lookup"><span data-stu-id="de201-218">Adding `msteams` to data with a Bot Framework action does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="de201-219">messageBack アクションを備えたアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="de201-219">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="de201-220">`msteams` オブジェクトに次の詳細を含むアダプティブ カードに `messageBack` アクションを含めるには、以下の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="de201-220">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="de201-221">必要に応じて、`data` オブジェクトに追加の隠しプロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="de201-221">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="de201-222">プロパティ</span><span class="sxs-lookup"><span data-stu-id="de201-222">Property</span></span> | <span data-ttu-id="de201-223">説明</span><span class="sxs-lookup"><span data-stu-id="de201-223">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="de201-224">`messageBack` に設定します。</span><span class="sxs-lookup"><span data-stu-id="de201-224">Set to `messageBack`.</span></span> |
| `displayText` | <span data-ttu-id="de201-225">省略可能。</span><span class="sxs-lookup"><span data-stu-id="de201-225">Optional.</span></span> <span data-ttu-id="de201-226">アクションが実行されたときに、チャット ストリームでユーザーが使用します。</span><span class="sxs-lookup"><span data-stu-id="de201-226">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="de201-227">このテキストは、お使いのボットには送信されません。</span><span class="sxs-lookup"><span data-stu-id="de201-227">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="de201-228">アクションが実行された場合に、ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="de201-228">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="de201-229">固有の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードすることができます。</span><span class="sxs-lookup"><span data-stu-id="de201-229">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="de201-230">アクションが実行された場合に、ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="de201-230">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="de201-231">このプロパティを使用して、ボット開発を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="de201-231">Use this property to simplify bot development.</span></span> <span data-ttu-id="de201-232">コードでは、トップレベルのプロパティをチェックして、ボット ロジックをディスパッチすることができます。</span><span class="sxs-lookup"><span data-stu-id="de201-232">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="de201-233">次のコードは `messageBack` アクションを備えたアダプティブ カードの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-233">The following code shows an example of Adaptive Cards with `messageBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for messageBack",
  "data": {
    "msteams": {
        "type": "messageBack",
        "displayText": "I clicked this button",
        "text": "text to bots",
        "value": "{\"bfKey\": \"bfVal\", \"conflictKey\": \"from value\"}"
    }
  }
}
```

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="de201-234">imBack アクションを備えたアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="de201-234">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="de201-235">`msteams` オブジェクトに次の詳細を含むアダプティブ カードに `imBack` アクションを含めるには、以下の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="de201-235">To include an `imBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="de201-236">必要に応じて、`data` オブジェクトに追加の隠しプロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="de201-236">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="de201-237">プロパティ</span><span class="sxs-lookup"><span data-stu-id="de201-237">Property</span></span> | <span data-ttu-id="de201-238">説明</span><span class="sxs-lookup"><span data-stu-id="de201-238">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="de201-239">`imBack` に設定します。</span><span class="sxs-lookup"><span data-stu-id="de201-239">Set to `imBack`.</span></span> |
| `value` | <span data-ttu-id="de201-240">チャットでエコー バックされる必要のある文字列。</span><span class="sxs-lookup"><span data-stu-id="de201-240">String that needs to be echoed back in the chat.</span></span> |

<span data-ttu-id="de201-241">次のコードは `imBack` アクションを備えたアダプティブ カードの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-241">The following code shows an example of Adaptive Cards with `imBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for imBack",
  "data": {
    "msteams": {
        "type": "imBack",
        "value": "Text to reply in chat"
    }
  }
}
```

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="de201-242">signin アクションを備えたアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="de201-242">Adaptive Cards with signin action</span></span>

<span data-ttu-id="de201-243">`msteams` オブジェクトに次の詳細を含むアダプティブ カードに `signin` アクションを含めるには、以下の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="de201-243">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="de201-244">必要に応じて、`data` オブジェクトに追加の隠しプロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="de201-244">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="de201-245">プロパティ</span><span class="sxs-lookup"><span data-stu-id="de201-245">Property</span></span> | <span data-ttu-id="de201-246">説明</span><span class="sxs-lookup"><span data-stu-id="de201-246">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="de201-247">`signin` に設定します。</span><span class="sxs-lookup"><span data-stu-id="de201-247">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="de201-248">リダイレクトさせる URL に設定します。</span><span class="sxs-lookup"><span data-stu-id="de201-248">Set to the URL where you want to redirect.</span></span>  |

<span data-ttu-id="de201-249">次のコードは `signin` アクションを備えたアダプティブ カードの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-249">The following code shows an example of Adaptive Cards with `signin` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for signin",
  "data": {
    "msteams": {
        "type": "signin",
        "value": "https://signin.com"
    }
  }
}
```

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="de201-250">invoke アクションを備えたアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="de201-250">Adaptive Cards with invoke action</span></span>

<span data-ttu-id="de201-251">`msteams` オブジェクトに次の詳細を含むアダプティブ カードに `invoke` アクションを含めるには、以下の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="de201-251">To include an `invoke` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="de201-252">必要に応じて、`data` オブジェクトに追加の隠しプロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="de201-252">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="de201-253">プロパティ</span><span class="sxs-lookup"><span data-stu-id="de201-253">Property</span></span> | <span data-ttu-id="de201-254">説明</span><span class="sxs-lookup"><span data-stu-id="de201-254">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="de201-255">`task/fetch` に設定します。</span><span class="sxs-lookup"><span data-stu-id="de201-255">Set to `task/fetch`.</span></span> |
| `data` | <span data-ttu-id="de201-256">値を設定します。</span><span class="sxs-lookup"><span data-stu-id="de201-256">Set the value.</span></span>  |

<span data-ttu-id="de201-257">次のコードは `invoke` アクションを備えたアダプティブ カードの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-257">The following code shows an example of Adaptive Cards with `invoke` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit",
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

<span data-ttu-id="de201-258">次のコードは、追加のペイロードデータを含む `invoke` アクションを備えたアダプティブ カードの一例を示します。</span><span class="sxs-lookup"><span data-stu-id="de201-258">The following code shows an example of Adaptive Cards with `invoke` action with additional payload data:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    },
    "Value1": "some value"
  }
}
```

## <a name="see-also"></a><span data-ttu-id="de201-259">関連項目</span><span class="sxs-lookup"><span data-stu-id="de201-259">See also</span></span>

[<span data-ttu-id="de201-260">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="de201-260">Cards reference</span></span>](./cards-reference.md)

## <a name="next-step"></a><span data-ttu-id="de201-261">次の手順</span><span class="sxs-lookup"><span data-stu-id="de201-261">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="de201-262">アダプティブ カードのユニバーサル アクション</span><span class="sxs-lookup"><span data-stu-id="de201-262">Universal Actions for Adaptive Cards</span></span>](../cards/Universal-actions-for-adaptive-cards/Overview.md)
