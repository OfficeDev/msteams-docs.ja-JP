---
title: ボットにカード アクションを追加する
description: ボットでのカード アクションMicrosoft Teams、ボットでカードを使用する方法について説明します。
localization_priority: Normal
ms.topic: conceptual
keywords: teams ボット カードアクション
ms.openlocfilehash: 1b20ca8003ab74c5dd2860e754024ae64ff94527
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140090"
---
# <a name="card-actions"></a><span data-ttu-id="49af5-104">カードアクション</span><span class="sxs-lookup"><span data-stu-id="49af5-104">Card actions</span></span>

<span data-ttu-id="49af5-105">ボットとメッセージング拡張機能で使用されるカードは、Teamsアクティビティの種類をサポート [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) します。</span><span class="sxs-lookup"><span data-stu-id="49af5-105">Cards used by bots and messaging extensions in Teams support the following activity [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) types:</span></span>

> [!NOTE]
> <span data-ttu-id="49af5-106">コネクタ `CardAction` と使用する `potentialActions` 場合Office 365コネクタ カードのアクションは異なります。</span><span class="sxs-lookup"><span data-stu-id="49af5-106">The `CardAction` actions differ from `potentialActions` for Office 365 Connector cards when used from connectors.</span></span>

| <span data-ttu-id="49af5-107">型</span><span class="sxs-lookup"><span data-stu-id="49af5-107">Type</span></span> | <span data-ttu-id="49af5-108">アクション</span><span class="sxs-lookup"><span data-stu-id="49af5-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="49af5-109">既定のブラウザーで URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="49af5-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="49af5-110">ボタンを選択したユーザーまたはカードをタップしたユーザーから、ボットにメッセージとペイロードを送信します。</span><span class="sxs-lookup"><span data-stu-id="49af5-110">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="49af5-111">チャット ストリームに別のメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="49af5-111">Sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="49af5-112">ボタンを選択したユーザーまたはカードをタップしたユーザーからボットにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="49af5-112">Sends a message to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="49af5-113">ユーザーからボットへのこのメッセージは、すべての会話参加者に表示されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-113">This message from user to bot is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="49af5-114">ボタンを選択したユーザーまたはカードをタップしたユーザーから、ボットにメッセージとペイロードを送信します。</span><span class="sxs-lookup"><span data-stu-id="49af5-114">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="49af5-115">このメッセージは表示されません。</span><span class="sxs-lookup"><span data-stu-id="49af5-115">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="49af5-116">OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。</span><span class="sxs-lookup"><span data-stu-id="49af5-116">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="49af5-117">Teams前の表 `CardAction` にリストされていない型はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="49af5-117">Teams does not support `CardAction` types not listed in the previous table.</span></span>
>* <span data-ttu-id="49af5-118">Teamsプロパティはサポート `potentialActions` されていません。</span><span class="sxs-lookup"><span data-stu-id="49af5-118">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="49af5-119">カードアクションは、Bot Framework [または](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) Azure Bot Service で推奨されるアクションとは異なります。</span><span class="sxs-lookup"><span data-stu-id="49af5-119">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework or Azure Bot Service.</span></span> <span data-ttu-id="49af5-120">推奨されるアクションは、Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="49af5-120">Suggested actions are not supported in Microsoft Teams.</span></span> <span data-ttu-id="49af5-121">ボット メッセージにボタンを表示する場合Teamsカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="49af5-121">If you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="49af5-122">メッセージング拡張機能の一部としてカード アクションを使用している場合、カードがチャネルに送信されるまでアクションは機能しません。</span><span class="sxs-lookup"><span data-stu-id="49af5-122">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="49af5-123">カードがメッセージの作成ボックスにある間、アクションは機能しません。</span><span class="sxs-lookup"><span data-stu-id="49af5-123">The actions do not work while the card is in the compose message box.</span></span>

## <a name="action-type-openurl"></a><span data-ttu-id="49af5-124">アクションの種類 openUrl</span><span class="sxs-lookup"><span data-stu-id="49af5-124">Action type openUrl</span></span>

<span data-ttu-id="49af5-125">`openUrl` action type は、既定のブラウザーで起動する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="49af5-125">`openUrl` action type specifies a URL to launch in the default browser.</span></span>

> [!NOTE]
> <span data-ttu-id="49af5-126">ボットは、どのボタンが選択されたのか通知を受け取らない。</span><span class="sxs-lookup"><span data-stu-id="49af5-126">Your bot does not receive any notice on which button was selected.</span></span>

<span data-ttu-id="49af5-127">を `openUrl` 使用すると、次のプロパティを使用してアクションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="49af5-127">With `openUrl`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="49af5-128">プロパティ</span><span class="sxs-lookup"><span data-stu-id="49af5-128">Property</span></span> | <span data-ttu-id="49af5-129">説明</span><span class="sxs-lookup"><span data-stu-id="49af5-129">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="49af5-130">ボタン ラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-130">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="49af5-131">このフィールドには、完全で適切に形成された URL が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="49af5-131">This field must contain a full and properly formed URL.</span></span> |

# <a name="json"></a>[<span data-ttu-id="49af5-132">JSON</span><span class="sxs-lookup"><span data-stu-id="49af5-132">JSON</span></span>](#tab/json)

<span data-ttu-id="49af5-133">次のコードは、JSON のアクション `openUrl` の種類の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-133">The following code shows an example of `openUrl` action type in JSON:</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[<span data-ttu-id="49af5-134">C#</span><span class="sxs-lookup"><span data-stu-id="49af5-134">C#</span></span>](#tab/csharp)

<span data-ttu-id="49af5-135">次のコードは、アクションの種類の `openUrl` 例を示C#。</span><span class="sxs-lookup"><span data-stu-id="49af5-135">The following code shows an example of `openUrl` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49af5-136">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49af5-136">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="49af5-137">次のコードは `openUrl` 、JavaScript のアクションの種類の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-137">The following code shows an example of `openUrl` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a><span data-ttu-id="49af5-138">アクションの種類 messageBack</span><span class="sxs-lookup"><span data-stu-id="49af5-138">Action type messageBack</span></span>

<span data-ttu-id="49af5-139">を `messageBack` 使用すると、次のプロパティを使用して完全にカスタマイズされたアクションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="49af5-139">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="49af5-140">プロパティ</span><span class="sxs-lookup"><span data-stu-id="49af5-140">Property</span></span> | <span data-ttu-id="49af5-141">説明</span><span class="sxs-lookup"><span data-stu-id="49af5-141">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="49af5-142">ボタン ラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-142">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="49af5-143">省略可能。</span><span class="sxs-lookup"><span data-stu-id="49af5-143">Optional.</span></span> <span data-ttu-id="49af5-144">アクションの実行時にチャット ストリーム内のユーザーが使用します。</span><span class="sxs-lookup"><span data-stu-id="49af5-144">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="49af5-145">このテキストはボットに送信されません。</span><span class="sxs-lookup"><span data-stu-id="49af5-145">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="49af5-146">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-146">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="49af5-147">アクションのコンテキスト (一意の識別子や JSON オブジェクトなど) をエンコードできます。</span><span class="sxs-lookup"><span data-stu-id="49af5-147">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="49af5-148">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-148">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="49af5-149">ボットの開発を簡略化するには、このプロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="49af5-149">Use this property to simplify bot development.</span></span> <span data-ttu-id="49af5-150">コードは、ボット ロジックをディスパッチするために、1 つのトップ レベル プロパティをチェックできます。</span><span class="sxs-lookup"><span data-stu-id="49af5-150">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="49af5-151">柔軟性は、コードが使用しないだけで、表示されるユーザー メッセージを履歴 `messageBack` に残せないという意味です `displayText` 。</span><span class="sxs-lookup"><span data-stu-id="49af5-151">The flexibility of `messageBack` means that your code cannot leave a visible user message in the history simply by not using `displayText`.</span></span>

# <a name="json"></a>[<span data-ttu-id="49af5-152">JSON</span><span class="sxs-lookup"><span data-stu-id="49af5-152">JSON</span></span>](#tab/json)

<span data-ttu-id="49af5-153">次のコードは、JSON のアクション `messageBack` の種類の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-153">The following code shows an example of `messageBack` action type in JSON:</span></span>

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

<span data-ttu-id="49af5-154">プロパティ `value` には、シリアル化された JSON 文字列または JSON オブジェクトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="49af5-154">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

# <a name="c"></a>[<span data-ttu-id="49af5-155">C#</span><span class="sxs-lookup"><span data-stu-id="49af5-155">C#</span></span>](#tab/csharp)

<span data-ttu-id="49af5-156">次のコードは、アクションの種類の `messageBack` 例を示C#。</span><span class="sxs-lookup"><span data-stu-id="49af5-156">The following code shows an example of `messageBack` action type in C#:</span></span>

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49af5-157">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49af5-157">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="49af5-158">次のコードは `messageBack` 、JavaScript のアクションの種類の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-158">The following code shows an example of `messageBack` action type in JavaScript:</span></span>

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

### <a name="inbound-message-example"></a><span data-ttu-id="49af5-159">受信メッセージの例</span><span class="sxs-lookup"><span data-stu-id="49af5-159">Inbound message example</span></span>

<span data-ttu-id="49af5-160">`replyToId` には、カード アクションが送信されたメッセージの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="49af5-160">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="49af5-161">メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="49af5-161">Use it if you want to update the message.</span></span>

<span data-ttu-id="49af5-162">次のコードは、受信メッセージの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-162">The following code shows an example of inbound message:</span></span>

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

## <a name="action-type-imback"></a><span data-ttu-id="49af5-163">アクションの種類 imBack</span><span class="sxs-lookup"><span data-stu-id="49af5-163">Action type imBack</span></span>

<span data-ttu-id="49af5-164">アクションは、ユーザーが通常のチャット メッセージに入力した場合と同様に、ボットへの戻り `imBack` メッセージをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="49af5-164">The `imBack` action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="49af5-165">ユーザーとチャネル内の他のすべてのユーザーは、ボタンの応答を確認できます。</span><span class="sxs-lookup"><span data-stu-id="49af5-165">Your user and all other users in a channel can see the button response.</span></span>

<span data-ttu-id="49af5-166">を `imBack` 使用すると、次のプロパティを使用してアクションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="49af5-166">With `imBack`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="49af5-167">プロパティ</span><span class="sxs-lookup"><span data-stu-id="49af5-167">Property</span></span> | <span data-ttu-id="49af5-168">説明</span><span class="sxs-lookup"><span data-stu-id="49af5-168">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="49af5-169">ボタン ラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-169">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="49af5-170">このフィールドには、チャットで使用されるテキスト文字列が含まれている必要があります。そのため、ボットに返送されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-170">This field must contain the text string used in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="49af5-171">これは、必要なロジックを実行するためにボットで処理するメッセージ テキストです。</span><span class="sxs-lookup"><span data-stu-id="49af5-171">This is the message text you process in your bot to perform the desired logic.</span></span> |

> [!NOTE]
> <span data-ttu-id="49af5-172">フィールド `value` は単純な文字列です。</span><span class="sxs-lookup"><span data-stu-id="49af5-172">The `value` field is a simple string.</span></span> <span data-ttu-id="49af5-173">書式設定や非表示の文字はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="49af5-173">There is no support for formatting or hidden characters.</span></span>

# <a name="json"></a>[<span data-ttu-id="49af5-174">JSON</span><span class="sxs-lookup"><span data-stu-id="49af5-174">JSON</span></span>](#tab/json)

<span data-ttu-id="49af5-175">次のコードは、JSON のアクション `imBack` の種類の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-175">The following code shows an example of `imBack` action type in JSON:</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[<span data-ttu-id="49af5-176">C#</span><span class="sxs-lookup"><span data-stu-id="49af5-176">C#</span></span>](#tab/csharp)

<span data-ttu-id="49af5-177">次のコードは、アクションの種類の `imBack` 例を示C#。</span><span class="sxs-lookup"><span data-stu-id="49af5-177">The following code shows an example of `imBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49af5-178">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49af5-178">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="49af5-179">次のコードは `imBack` 、JavaScript のアクションの種類の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-179">The following code shows an example of `imBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a><span data-ttu-id="49af5-180">アクションの種類の呼び出し</span><span class="sxs-lookup"><span data-stu-id="49af5-180">Action type invoke</span></span>

<span data-ttu-id="49af5-181">この `invoke` アクションは、タスク モジュールの呼び出 [しに使用されます](~/task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="49af5-181">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="49af5-182">アクション `invoke` には、3 つのプロパティ `type` 、、 `title` およびが含まれる `value` 。</span><span class="sxs-lookup"><span data-stu-id="49af5-182">The `invoke` action contains three properties, `type`, `title`, and `value`.</span></span>

<span data-ttu-id="49af5-183">を `invoke` 使用すると、次のプロパティを使用してアクションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="49af5-183">With `invoke`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="49af5-184">プロパティ</span><span class="sxs-lookup"><span data-stu-id="49af5-184">Property</span></span> | <span data-ttu-id="49af5-185">説明</span><span class="sxs-lookup"><span data-stu-id="49af5-185">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="49af5-186">ボタン ラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-186">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="49af5-187">このプロパティには、文字列、文字列化された JSON オブジェクト、または JSON オブジェクトを含めできます。</span><span class="sxs-lookup"><span data-stu-id="49af5-187">This property can contain a string, a stringified JSON object, or a JSON object.</span></span> |

# <a name="json"></a>[<span data-ttu-id="49af5-188">JSON</span><span class="sxs-lookup"><span data-stu-id="49af5-188">JSON</span></span>](#tab/json)

<span data-ttu-id="49af5-189">次のコードは、JSON のアクション `invoke` の種類の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-189">The following code shows an example of `invoke` action type in JSON:</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="49af5-190">ユーザーがボタンを選択すると、ボットは追加の情報 `value` を含むオブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="49af5-190">When a user selects the button, your bot receives the `value` object with some additional information.</span></span>

> [!NOTE]
> <span data-ttu-id="49af5-191">アクティビティの種類は `invoke` 、 の代 `message` わりにです `activity.Type == "invoke"` 。</span><span class="sxs-lookup"><span data-stu-id="49af5-191">The activity type is `invoke` instead of `message` that is `activity.Type == "invoke"`.</span></span>

# <a name="c"></a>[<span data-ttu-id="49af5-192">C#</span><span class="sxs-lookup"><span data-stu-id="49af5-192">C#</span></span>](#tab/csharp)

<span data-ttu-id="49af5-193">次のコードは、アクションの種類の `invoke` 例を示C#。</span><span class="sxs-lookup"><span data-stu-id="49af5-193">The following code shows an example of `invoke` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49af5-194">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49af5-194">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="49af5-195">次のコードは、アクションの種類の例 `invoke` を示Node.js。</span><span class="sxs-lookup"><span data-stu-id="49af5-195">The following code shows an example of `invoke` action type in Node.js:</span></span>

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

### <a name="example-of-incoming-invoke-message"></a><span data-ttu-id="49af5-196">受信呼び出しメッセージの例</span><span class="sxs-lookup"><span data-stu-id="49af5-196">Example of incoming invoke message</span></span>

<span data-ttu-id="49af5-197">Top-level `replyToId` プロパティには、カードアクションが送信されたメッセージの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="49af5-197">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="49af5-198">メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="49af5-198">Use it if you want to update the message.</span></span>

<span data-ttu-id="49af5-199">次のコードは、受信呼び出しメッセージの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-199">The following code shows an example of incoming invoke message:</span></span>

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

## <a name="action-type-signin"></a><span data-ttu-id="49af5-200">アクションの種類の signin</span><span class="sxs-lookup"><span data-stu-id="49af5-200">Action type signin</span></span>

<span data-ttu-id="49af5-201">`signin` アクションの種類は、ボットがセキュリティで保護されたサービスに接続できる OAuth フローを開始します。</span><span class="sxs-lookup"><span data-stu-id="49af5-201">`signin` action type initiates an OAuth flow that permits bots to connect with secure services.</span></span> <span data-ttu-id="49af5-202">詳細については、「ボットの [認証フロー」を参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="49af5-202">For more information, see [authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="49af5-203">Teamsアダプティブ カード[でのみ使用されるアダプティブ](#adaptive-cards-actions)カード アクションもサポートしています。</span><span class="sxs-lookup"><span data-stu-id="49af5-203">Teams also supports [Adaptive Cards actions](#adaptive-cards-actions) that are only used by Adaptive Cards.</span></span>

# <a name="json"></a>[<span data-ttu-id="49af5-204">JSON</span><span class="sxs-lookup"><span data-stu-id="49af5-204">JSON</span></span>](#tab/json)

<span data-ttu-id="49af5-205">次のコードは、JSON のアクション `signin` の種類の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-205">The following code shows an example of `signin` action type in JSON:</span></span>

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[<span data-ttu-id="49af5-206">C#</span><span class="sxs-lookup"><span data-stu-id="49af5-206">C#</span></span>](#tab/csharp)

<span data-ttu-id="49af5-207">次のコードは、アクションの種類の `signin` 例を示C#。</span><span class="sxs-lookup"><span data-stu-id="49af5-207">The following code shows an example of `signin` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="49af5-208">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="49af5-208">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="49af5-209">次のコードは `signin` 、JavaScript のアクションの種類の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-209">The following code shows an example of `signin` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a><span data-ttu-id="49af5-210">アダプティブ カードのアクション</span><span class="sxs-lookup"><span data-stu-id="49af5-210">Adaptive Cards actions</span></span>

<span data-ttu-id="49af5-211">アダプティブ カードは、次の 4 種類のアクションをサポートします。</span><span class="sxs-lookup"><span data-stu-id="49af5-211">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="49af5-212">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="49af5-212">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="49af5-213">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="49af5-213">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="49af5-214">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="49af5-214">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="49af5-215">Action.Exeかわいい</span><span class="sxs-lookup"><span data-stu-id="49af5-215">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="49af5-216">アダプティブ カードペイロードを変更して、オブジェクトのプロパティを使用して既存の Bot Framework アクション `Action.Submit` `msteams` を `data` サポートすることができます `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="49af5-216">You can also modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using an `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="49af5-217">次のセクションでは、アダプティブ カードで既存の Bot Framework アクションを使用する方法の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="49af5-217">The next section provide details on how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="49af5-218">`msteams`Bot Framework アクションを使用してデータに追加しても、アダプティブ カード タスク モジュールでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="49af5-218">Adding `msteams` to data with a Bot Framework action does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="49af5-219">messageBack アクションを含むアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="49af5-219">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="49af5-220">アダプティブ カードに `messageBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="49af5-220">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="49af5-221">必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="49af5-221">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="49af5-222">プロパティ</span><span class="sxs-lookup"><span data-stu-id="49af5-222">Property</span></span> | <span data-ttu-id="49af5-223">説明</span><span class="sxs-lookup"><span data-stu-id="49af5-223">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="49af5-224">に設定します `messageBack` 。</span><span class="sxs-lookup"><span data-stu-id="49af5-224">Set to `messageBack`.</span></span> |
| `displayText` | <span data-ttu-id="49af5-225">省略可能。</span><span class="sxs-lookup"><span data-stu-id="49af5-225">Optional.</span></span> <span data-ttu-id="49af5-226">アクションの実行時にチャット ストリーム内のユーザーが使用します。</span><span class="sxs-lookup"><span data-stu-id="49af5-226">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="49af5-227">このテキストはボットに送信されません。</span><span class="sxs-lookup"><span data-stu-id="49af5-227">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="49af5-228">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-228">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="49af5-229">アクションのコンテキスト (一意の識別子や JSON オブジェクトなど) をエンコードできます。</span><span class="sxs-lookup"><span data-stu-id="49af5-229">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="49af5-230">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="49af5-230">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="49af5-231">ボットの開発を簡略化するには、このプロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="49af5-231">Use this property to simplify bot development.</span></span> <span data-ttu-id="49af5-232">コードは、ボット ロジックをディスパッチするために、1 つのトップ レベル プロパティをチェックできます。</span><span class="sxs-lookup"><span data-stu-id="49af5-232">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="49af5-233">次のコードは、アクションを含むアダプティブ カードの例を示 `messageBack` しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-233">The following code shows an example of Adaptive Cards with `messageBack` action:</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="49af5-234">imBack アクションを使用したアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="49af5-234">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="49af5-235">アダプティブ カードで `imBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="49af5-235">To include an `imBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="49af5-236">必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="49af5-236">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="49af5-237">プロパティ</span><span class="sxs-lookup"><span data-stu-id="49af5-237">Property</span></span> | <span data-ttu-id="49af5-238">説明</span><span class="sxs-lookup"><span data-stu-id="49af5-238">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="49af5-239">に設定します `imBack` 。</span><span class="sxs-lookup"><span data-stu-id="49af5-239">Set to `imBack`.</span></span> |
| `value` | <span data-ttu-id="49af5-240">チャットでエコーバックする必要がある文字列。</span><span class="sxs-lookup"><span data-stu-id="49af5-240">String that needs to be echoed back in the chat.</span></span> |

<span data-ttu-id="49af5-241">次のコードは、アクションを含むアダプティブ カードの例を示 `imBack` しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-241">The following code shows an example of Adaptive Cards with `imBack` action:</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="49af5-242">Signin アクションを使用したアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="49af5-242">Adaptive Cards with signin action</span></span>

<span data-ttu-id="49af5-243">アダプティブ カードに `signin` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="49af5-243">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="49af5-244">必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="49af5-244">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="49af5-245">プロパティ</span><span class="sxs-lookup"><span data-stu-id="49af5-245">Property</span></span> | <span data-ttu-id="49af5-246">説明</span><span class="sxs-lookup"><span data-stu-id="49af5-246">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="49af5-247">に設定します `signin` 。</span><span class="sxs-lookup"><span data-stu-id="49af5-247">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="49af5-248">リダイレクトする URL に設定します。</span><span class="sxs-lookup"><span data-stu-id="49af5-248">Set to the URL where you want to redirect.</span></span>  |

<span data-ttu-id="49af5-249">次のコードは、アクションを含むアダプティブ カードの例を示 `signin` しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-249">The following code shows an example of Adaptive Cards with `signin` action:</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="49af5-250">アクションを呼び出すアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="49af5-250">Adaptive Cards with invoke action</span></span>

<span data-ttu-id="49af5-251">アダプティブ カードで `invoke` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="49af5-251">To include an `invoke` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="49af5-252">必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="49af5-252">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="49af5-253">プロパティ</span><span class="sxs-lookup"><span data-stu-id="49af5-253">Property</span></span> | <span data-ttu-id="49af5-254">説明</span><span class="sxs-lookup"><span data-stu-id="49af5-254">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="49af5-255">に設定します `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="49af5-255">Set to `task/fetch`.</span></span> |
| `data` | <span data-ttu-id="49af5-256">値を設定します。</span><span class="sxs-lookup"><span data-stu-id="49af5-256">Set the value.</span></span>  |

<span data-ttu-id="49af5-257">次のコードは、アクションを含むアダプティブ カードの例を示 `invoke` しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-257">The following code shows an example of Adaptive Cards with `invoke` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

<span data-ttu-id="49af5-258">次のコードは、追加のペイロード データを含むアクションを含むアダプティブ `invoke` カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="49af5-258">The following code shows an example of Adaptive Cards with `invoke` action with additional payload data:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="49af5-259">関連項目</span><span class="sxs-lookup"><span data-stu-id="49af5-259">See also</span></span>

[<span data-ttu-id="49af5-260">カード リファレンス</span><span class="sxs-lookup"><span data-stu-id="49af5-260">Cards reference</span></span>](./cards-reference.md)

## <a name="next-step"></a><span data-ttu-id="49af5-261">次の手順</span><span class="sxs-lookup"><span data-stu-id="49af5-261">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49af5-262">アダプティブ カードのユニバーサル アクション</span><span class="sxs-lookup"><span data-stu-id="49af5-262">Universal Actions for Adaptive Cards</span></span>](../cards/Universal-actions-for-adaptive-cards/Overview.md)
