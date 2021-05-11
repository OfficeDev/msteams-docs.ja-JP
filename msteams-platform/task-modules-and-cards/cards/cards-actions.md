---
title: ボットにカード アクションを追加する
description: ボットでのカード アクションMicrosoft Teams、ボットでカードを使用する方法について説明します。
localization_priority: Normal
ms.topic: conceptual
keywords: teams ボット カードアクション
ms.openlocfilehash: 75dcd6e1de1968f021a1ebe66c6770c4f641c94d
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088795"
---
# <a name="card-actions"></a><span data-ttu-id="d548e-104">カードアクション</span><span class="sxs-lookup"><span data-stu-id="d548e-104">Card actions</span></span>

<span data-ttu-id="d548e-105">ボットとメッセージング拡張機能で使用されるカードは、Teamsアクティビティ ( ) の種類 [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="d548e-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="d548e-106">これらのアクションは、Connectors `potentialActions` から使用Office 365コネクタ カードとは異なります。</span><span class="sxs-lookup"><span data-stu-id="d548e-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="d548e-107">型</span><span class="sxs-lookup"><span data-stu-id="d548e-107">Type</span></span> | <span data-ttu-id="d548e-108">アクション</span><span class="sxs-lookup"><span data-stu-id="d548e-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="d548e-109">既定のブラウザーで URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="d548e-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="d548e-110">ボットにメッセージとペイロードを送信し (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから) チャット ストリームに別のメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="d548e-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="d548e-111">ボットにメッセージを送信します (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから)。</span><span class="sxs-lookup"><span data-stu-id="d548e-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="d548e-112">このメッセージ (ユーザーからボットへ) は、すべての会話参加者に表示されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="d548e-113">ボットにメッセージとペイロードを送信します (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから)。</span><span class="sxs-lookup"><span data-stu-id="d548e-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="d548e-114">このメッセージは表示されません。</span><span class="sxs-lookup"><span data-stu-id="d548e-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="d548e-115">OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。</span><span class="sxs-lookup"><span data-stu-id="d548e-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="d548e-116">Teams前の表 `CardAction` にリストされていない型はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d548e-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="d548e-117">Teamsプロパティはサポート `potentialActions` されていません。</span><span class="sxs-lookup"><span data-stu-id="d548e-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="d548e-118">カードアクションは、Bot [](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) Framework/Azure Bot Service で推奨されるアクションとは異なります。</span><span class="sxs-lookup"><span data-stu-id="d548e-118">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="d548e-119">推奨されるアクションは、Microsoft Teamsボット メッセージにボタンを表示する場合Teamsカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="d548e-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="d548e-120">メッセージング拡張機能の一部としてカード アクションを使用している場合、カードがチャネルに送信されるまでアクションは機能しません (カードがメッセージの作成ボックスに入っている間は動作しません)。</span><span class="sxs-lookup"><span data-stu-id="d548e-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="d548e-121">Teamsアダプティブ カード[アクションもサポートしています](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)。これはアダプティブ カードでのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="d548e-122">これらのアクションは、この参照の最後にある独自のセクションに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="d548e-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="d548e-123">openUrl</span></span>

<span data-ttu-id="d548e-124">このアクションの種類は、既定のブラウザーで起動する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d548e-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="d548e-125">ボットは、クリックされたボタンに関する通知を受け取らない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="d548e-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="d548e-126">フィールド `value` には、完全で適切に形成された URL が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="d548e-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="d548e-127">messageBack</span><span class="sxs-lookup"><span data-stu-id="d548e-127">messageBack</span></span>

<span data-ttu-id="d548e-128">を `messageBack` 使用すると、次のプロパティを使用して完全にカスタマイズされたアクションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="d548e-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="d548e-129">プロパティ</span><span class="sxs-lookup"><span data-stu-id="d548e-129">Property</span></span> | <span data-ttu-id="d548e-130">説明</span><span class="sxs-lookup"><span data-stu-id="d548e-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="d548e-131">ボタン ラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="d548e-132">省略可能。</span><span class="sxs-lookup"><span data-stu-id="d548e-132">Optional.</span></span> <span data-ttu-id="d548e-133">アクションの実行時に、ユーザーがチャット ストリームにエコーします。</span><span class="sxs-lookup"><span data-stu-id="d548e-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="d548e-134">このテキストは *ボット* に送信されません。</span><span class="sxs-lookup"><span data-stu-id="d548e-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="d548e-135">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="d548e-136">アクションのコンテキスト (一意の識別子や JSON オブジェクトなど) をエンコードできます。</span><span class="sxs-lookup"><span data-stu-id="d548e-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="d548e-137">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="d548e-138">ボットの開発を簡略化するには、このプロパティを使用します。コードでは、ボット ロジックをディスパッチするために 1 つのトップ レベル プロパティをチェックできます。</span><span class="sxs-lookup"><span data-stu-id="d548e-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="d548e-139">柔軟性は、コードが単に使用しないだけで、表示されるユーザー メッセージを履歴に残すのを選択 `messageBack` できないという意味です `displayText` 。</span><span class="sxs-lookup"><span data-stu-id="d548e-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="d548e-140">プロパティ `value` には、シリアル化された JSON 文字列または JSON オブジェクトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="d548e-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="d548e-141">受信メッセージの例</span><span class="sxs-lookup"><span data-stu-id="d548e-141">Inbound message example</span></span>

<span data-ttu-id="d548e-142">`replyToId` には、カード アクションが送信されたメッセージの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="d548e-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="d548e-143">メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="d548e-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="d548e-144">imBack</span><span class="sxs-lookup"><span data-stu-id="d548e-144">imBack</span></span>

<span data-ttu-id="d548e-145">このアクションは、ユーザーが通常のチャット メッセージに入力した場合と同様に、ボットへの戻りメッセージをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="d548e-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="d548e-146">チャネル内のユーザーと他のすべてのユーザーには、そのボタンの応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="d548e-147">フィールド `value` には、チャットにエコーされたテキスト文字列が含まれている必要があります。そのため、ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="d548e-148">これは、目的のロジックを実行するためにボットで処理するメッセージ テキストです。</span><span class="sxs-lookup"><span data-stu-id="d548e-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="d548e-149">注: このフィールドは単純な文字列です。書式設定や非表示文字のサポートはありません。</span><span class="sxs-lookup"><span data-stu-id="d548e-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="d548e-150">invoke</span><span class="sxs-lookup"><span data-stu-id="d548e-150">invoke</span></span>

<span data-ttu-id="d548e-151">この `invoke` アクションは、タスク モジュールの呼び出 [しに使用されます](~/task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="d548e-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="d548e-152">アクション `invoke` には、次の 3 つのプロパティ `type` が `title` 含まれる。 `value`</span><span class="sxs-lookup"><span data-stu-id="d548e-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="d548e-153">この `value` プロパティには、文字列、文字列化された JSON オブジェクト、または JSON オブジェクトを含めできます。</span><span class="sxs-lookup"><span data-stu-id="d548e-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="d548e-154">ユーザーがボタンをクリックすると、ボットは追加の情報を `value` 含むオブジェクトを受信します。</span><span class="sxs-lookup"><span data-stu-id="d548e-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="d548e-155">アクティビティの種類は ( ) の `invoke` 代わりに使用されます `message` `activity.Type == "invoke"` 。</span><span class="sxs-lookup"><span data-stu-id="d548e-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="d548e-156">例: ボタン定義の呼び出し (.NET)</span><span class="sxs-lookup"><span data-stu-id="d548e-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="d548e-157">例: 受信呼び出しメッセージ</span><span class="sxs-lookup"><span data-stu-id="d548e-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="d548e-158">Top-level `replyToId` プロパティには、カードアクションが送信されたメッセージの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="d548e-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="d548e-159">メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="d548e-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="d548e-160">signin</span><span class="sxs-lookup"><span data-stu-id="d548e-160">signin</span></span>

<span data-ttu-id="d548e-161">OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。詳細については、ボットの認証フロー [を参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="d548e-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="d548e-162">アダプティブ カードのアクション</span><span class="sxs-lookup"><span data-stu-id="d548e-162">Adaptive Cards actions</span></span>

<span data-ttu-id="d548e-163">アダプティブ カードは、次の 4 種類のアクションをサポートします。</span><span class="sxs-lookup"><span data-stu-id="d548e-163">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="d548e-164">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="d548e-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="d548e-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="d548e-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="d548e-166">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="d548e-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="d548e-167">Action.Exeかわいい</span><span class="sxs-lookup"><span data-stu-id="d548e-167">Action.Execute</span></span>](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="d548e-168">上記のアクションに加えて、アダプティブ カード ペイロードを変更して、オブジェクトのプロパティを使用して既存の Bot Framework アクション `Action.Submit` `msteams` `data` をサポートできます `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="d548e-168">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="d548e-169">以下のセクションでは、アダプティブ カードで既存の Bot Framework アクションを使用する方法について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="d548e-169">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="d548e-170">Bot Framework アクションを使用してデータに追加しても、アダプティブ カード タスク `msteams` モジュールでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="d548e-170">Adding `msteams` to data, with a Bot Framework action, does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="d548e-171">messageBack アクションを含むアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="d548e-171">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="d548e-172">アダプティブ カードに `messageBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d548e-172">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="d548e-173">必要に応じて、オブジェクトに追加の非表示プロパティ `data` を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d548e-173">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="d548e-174">プロパティ</span><span class="sxs-lookup"><span data-stu-id="d548e-174">Property</span></span> | <span data-ttu-id="d548e-175">説明</span><span class="sxs-lookup"><span data-stu-id="d548e-175">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="d548e-176">に設定する `messageBack`</span><span class="sxs-lookup"><span data-stu-id="d548e-176">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="d548e-177">省略可能。</span><span class="sxs-lookup"><span data-stu-id="d548e-177">Optional.</span></span> <span data-ttu-id="d548e-178">アクションの実行時に、ユーザーがチャット ストリームにエコーします。</span><span class="sxs-lookup"><span data-stu-id="d548e-178">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="d548e-179">このテキストは *ボット* に送信されません。</span><span class="sxs-lookup"><span data-stu-id="d548e-179">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="d548e-180">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-180">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="d548e-181">アクションのコンテキスト (一意の識別子や JSON オブジェクトなど) をエンコードできます。</span><span class="sxs-lookup"><span data-stu-id="d548e-181">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="d548e-182">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="d548e-182">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="d548e-183">ボットの開発を簡略化するには、このプロパティを使用します。コードでは、ボット ロジックをディスパッチするために 1 つのトップ レベル プロパティをチェックできます。</span><span class="sxs-lookup"><span data-stu-id="d548e-183">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="d548e-184">例</span><span class="sxs-lookup"><span data-stu-id="d548e-184">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="d548e-185">imBack アクションを使用したアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="d548e-185">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="d548e-186">アダプティブ カードに `imBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d548e-186">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="d548e-187">必要に応じて、オブジェクトに追加の非表示プロパティ `data` を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d548e-187">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="d548e-188">プロパティ</span><span class="sxs-lookup"><span data-stu-id="d548e-188">Property</span></span> | <span data-ttu-id="d548e-189">説明</span><span class="sxs-lookup"><span data-stu-id="d548e-189">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="d548e-190">に設定する `imBack`</span><span class="sxs-lookup"><span data-stu-id="d548e-190">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="d548e-191">チャットでエコーバックする必要がある文字列</span><span class="sxs-lookup"><span data-stu-id="d548e-191">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="d548e-192">例</span><span class="sxs-lookup"><span data-stu-id="d548e-192">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="d548e-193">Signin アクションを使用したアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="d548e-193">Adaptive Cards with signin action</span></span>

<span data-ttu-id="d548e-194">アダプティブ カードに `signin` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d548e-194">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="d548e-195">必要に応じて、オブジェクトに追加の非表示プロパティ `data` を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d548e-195">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="d548e-196">プロパティ</span><span class="sxs-lookup"><span data-stu-id="d548e-196">Property</span></span> | <span data-ttu-id="d548e-197">説明</span><span class="sxs-lookup"><span data-stu-id="d548e-197">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="d548e-198">に設定する `signin`</span><span class="sxs-lookup"><span data-stu-id="d548e-198">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="d548e-199">リダイレクト先の URL に設定する</span><span class="sxs-lookup"><span data-stu-id="d548e-199">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="d548e-200">例</span><span class="sxs-lookup"><span data-stu-id="d548e-200">Example</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="d548e-201">アクションを呼び出すアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="d548e-201">Adaptive Cards with invoke action</span></span>
 
<span data-ttu-id="d548e-202">アダプティブ カードに `invoke` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d548e-202">To include a `invoke` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="d548e-203">必要に応じて、オブジェクトに追加の非表示プロパティ `data` を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d548e-203">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="d548e-204">プロパティ</span><span class="sxs-lookup"><span data-stu-id="d548e-204">Property</span></span> | <span data-ttu-id="d548e-205">説明</span><span class="sxs-lookup"><span data-stu-id="d548e-205">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="d548e-206">に設定する `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="d548e-206">Set to `task/fetch`</span></span> |
| `data` | <span data-ttu-id="d548e-207">値を設定する</span><span class="sxs-lookup"><span data-stu-id="d548e-207">Set the value</span></span>  |

#### <a name="example"></a><span data-ttu-id="d548e-208">例</span><span class="sxs-lookup"><span data-stu-id="d548e-208">Example</span></span>

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

#### <a name="example-2-with-additional-payload-data"></a><span data-ttu-id="d548e-209">例 2 (追加のペイロード データを含む)</span><span class="sxs-lookup"><span data-stu-id="d548e-209">Example 2 (with additional payload data)</span></span>

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
