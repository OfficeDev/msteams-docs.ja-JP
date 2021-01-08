---
title: ボットにカード アクションを追加する
description: Microsoft Teams でのカード アクションと、ボットでのカード アクションの使い方について説明します。
keywords: teams bots cards actions
ms.openlocfilehash: 2bee1072405d91cd29d1aa227884516a87d10bde
ms.sourcegitcommit: b9771f8f4be9ac1ff8c85c2d7bd8d5c5408bc653
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/06/2021
ms.locfileid: "49768075"
---
# <a name="card-actions"></a><span data-ttu-id="64aef-104">カードアクション</span><span class="sxs-lookup"><span data-stu-id="64aef-104">Card actions</span></span>

<span data-ttu-id="64aef-105">Teams のボットとメッセージング拡張機能で使用されるカードは、次の種類のアクティビティ ( [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="64aef-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="64aef-106">これらのアクションは、コネクタと使用 `potentialActions` Office 365 コネクタ カードとは異なります。</span><span class="sxs-lookup"><span data-stu-id="64aef-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="64aef-107">種類</span><span class="sxs-lookup"><span data-stu-id="64aef-107">Type</span></span> | <span data-ttu-id="64aef-108">アクション</span><span class="sxs-lookup"><span data-stu-id="64aef-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="64aef-109">既定のブラウザーで URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="64aef-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="64aef-110">ボットにメッセージとペイロードを送信し (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから)、チャット ストリームに別のメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="64aef-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="64aef-111">ボットにメッセージを送信します (ボタンをクリックまたはカードをタップしたユーザーからのメッセージ)。</span><span class="sxs-lookup"><span data-stu-id="64aef-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="64aef-112">このメッセージ (ユーザーからボットへ) は、すべての会話参加者に表示されます。</span><span class="sxs-lookup"><span data-stu-id="64aef-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="64aef-113">ボットにメッセージとペイロードを送信します (ボタンをクリックまたはカードをタップしたユーザーから)。</span><span class="sxs-lookup"><span data-stu-id="64aef-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="64aef-114">このメッセージは表示されません。</span><span class="sxs-lookup"><span data-stu-id="64aef-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="64aef-115">OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。</span><span class="sxs-lookup"><span data-stu-id="64aef-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="64aef-116">Teams では、前 `CardAction` の表に記載されていない種類はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="64aef-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="64aef-117">Teams では、このプロパティはサポート `potentialActions` されていません。</span><span class="sxs-lookup"><span data-stu-id="64aef-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="64aef-118">カード アクションは、Bot Framework/Azure Bot Service の推奨アクションとは異なります。 [](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="64aef-118">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="64aef-119">推奨されるアクションは Microsoft Teams ではサポートされていません。Teams ボット メッセージにボタンを表示する場合は、カードを使用します。</span><span class="sxs-lookup"><span data-stu-id="64aef-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="64aef-120">メッセージング拡張機能の一部としてカード アクションを使用している場合、そのアクションは、カードがチャネルに送信されるまで機能しません (カードがメッセージ作成ボックスにある間は機能しません)。</span><span class="sxs-lookup"><span data-stu-id="64aef-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="64aef-121">Teams は、 [アダプティブ カードでのみ使用](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)されるアダプティブ カード アクションもサポートしています。</span><span class="sxs-lookup"><span data-stu-id="64aef-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="64aef-122">これらのアクションは、このリファレンスの最後にある独自のセクションに記載されています。</span><span class="sxs-lookup"><span data-stu-id="64aef-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="64aef-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="64aef-123">openUrl</span></span>

<span data-ttu-id="64aef-124">このアクションの種類は、既定のブラウザーで起動する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="64aef-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="64aef-125">ボットは、クリックされたボタンに関する通知を受け取らない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="64aef-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="64aef-126">フィールド `value` には、完全で適切な形式の URL が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="64aef-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="64aef-127">messageBack</span><span class="sxs-lookup"><span data-stu-id="64aef-127">messageBack</span></span>

<span data-ttu-id="64aef-128">次 `messageBack` のプロパティを使用して、完全にカスタマイズされたアクションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="64aef-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="64aef-129">プロパティ</span><span class="sxs-lookup"><span data-stu-id="64aef-129">Property</span></span> | <span data-ttu-id="64aef-130">説明</span><span class="sxs-lookup"><span data-stu-id="64aef-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="64aef-131">ボタン ラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="64aef-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="64aef-132">省略可能です。</span><span class="sxs-lookup"><span data-stu-id="64aef-132">Optional.</span></span> <span data-ttu-id="64aef-133">アクションの実行時に、ユーザーによってチャット ストリームにエコーされます。</span><span class="sxs-lookup"><span data-stu-id="64aef-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="64aef-134">このテキスト *はボット* に送信されません。</span><span class="sxs-lookup"><span data-stu-id="64aef-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="64aef-135">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="64aef-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="64aef-136">アクションのコンテキスト (一意識別子や JSON オブジェクトなど) をエンコードできます。</span><span class="sxs-lookup"><span data-stu-id="64aef-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="64aef-137">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="64aef-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="64aef-138">ボットの開発を簡略化するには、このプロパティを使用します。コードでは、ボット ロジックをディスパッチする単一のトップ レベル プロパティをチェックできます。</span><span class="sxs-lookup"><span data-stu-id="64aef-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="64aef-139">柔軟性の高い方法は、コードで、単に使用しないだけで、表示されているユーザー メッセージを履歴に `messageBack` 残せない方法を選択できるという意味です `displayText` 。</span><span class="sxs-lookup"><span data-stu-id="64aef-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="64aef-140">この `value` プロパティには、シリアル化された JSON 文字列または JSON オブジェクトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="64aef-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="64aef-141">受信メッセージの例</span><span class="sxs-lookup"><span data-stu-id="64aef-141">Inbound message example</span></span>

<span data-ttu-id="64aef-142">`replyToId` には、カードアクションが送信されたメッセージの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="64aef-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="64aef-143">メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="64aef-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="64aef-144">imBack</span><span class="sxs-lookup"><span data-stu-id="64aef-144">imBack</span></span>

<span data-ttu-id="64aef-145">このアクションは、ユーザーが通常のチャット メッセージに入力した場合と同様に、ボットへの戻りメッセージをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="64aef-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="64aef-146">チャネル内のユーザーと他のすべてのユーザーには、そのボタンの応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="64aef-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="64aef-147">フィールドには、チャットでエコーされたテキスト文字列が含まれている必要があります。そのため、 `value` ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="64aef-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="64aef-148">これは、目的のロジックを実行するためにボットで処理するメッセージ テキストです。</span><span class="sxs-lookup"><span data-stu-id="64aef-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="64aef-149">注: このフィールドは単純な文字列です。書式設定や非表示文字はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="64aef-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="64aef-150">invoke</span><span class="sxs-lookup"><span data-stu-id="64aef-150">invoke</span></span>

<span data-ttu-id="64aef-151">この `invoke` アクションは、タスク モジュールの呼び出 [しに使用されます](~/task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="64aef-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="64aef-152">アクション `invoke` には、次の 3 つのプロパティ `type` `title` が含まれる: , , `value` and .</span><span class="sxs-lookup"><span data-stu-id="64aef-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="64aef-153">プロパティ `value` には、文字列、文字列に変換された JSON オブジェクト、または JSON オブジェクトを含めできます。</span><span class="sxs-lookup"><span data-stu-id="64aef-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="64aef-154">ユーザーがボタンをクリックすると、ボットは追加情報を含む `value` オブジェクトを受信します。</span><span class="sxs-lookup"><span data-stu-id="64aef-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="64aef-155">アクティビティの種類は ( ) の `invoke` 代わりに使用されます `message` `activity.Type == "invoke"` 。</span><span class="sxs-lookup"><span data-stu-id="64aef-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="64aef-156">例: 起動ボタン定義 (.NET)</span><span class="sxs-lookup"><span data-stu-id="64aef-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="64aef-157">例: 着信呼び出しメッセージ</span><span class="sxs-lookup"><span data-stu-id="64aef-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="64aef-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span><span class="sxs-lookup"><span data-stu-id="64aef-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="64aef-159">メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="64aef-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="64aef-160">signin</span><span class="sxs-lookup"><span data-stu-id="64aef-160">signin</span></span>

<span data-ttu-id="64aef-161">OAuth フローを開始し、ボットがセキュリティで保護されたサービスに接続できるようにします。詳細については、「ボットの認証フロー」を [参照してください](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="64aef-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="64aef-162">アダプティブ カード アクション</span><span class="sxs-lookup"><span data-stu-id="64aef-162">Adaptive Cards actions</span></span>

<span data-ttu-id="64aef-163">アダプティブ カードは、次の 3 種類のアクションをサポートします。</span><span class="sxs-lookup"><span data-stu-id="64aef-163">Adaptive Cards support three action types:</span></span>

* [<span data-ttu-id="64aef-164">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="64aef-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="64aef-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="64aef-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="64aef-166">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="64aef-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)

<span data-ttu-id="64aef-167">上記のアクションに加えて、オブジェクトのプロパティを使用して、既存の Bot Framework アクションをサポートするためにアダプティブ カードのペイロード `Action.Submit` `msteams` を `data` 変更できます `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="64aef-167">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="64aef-168">以下のセクションでは、アダプティブ カードで既存の Bot Framework アクションを使用する方法について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="64aef-168">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="64aef-169">Bot Framework アクションを使用したデータへの追加は、アダプティブ カード タスク `msteams` モジュールでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="64aef-169">Adding `msteams` to data, with a Bot Framework action, does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="64aef-170">messageBack アクションを含むアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="64aef-170">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="64aef-171">アダプティブ カードに `messageBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="64aef-171">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="64aef-172">必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="64aef-172">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="64aef-173">プロパティ</span><span class="sxs-lookup"><span data-stu-id="64aef-173">Property</span></span> | <span data-ttu-id="64aef-174">説明</span><span class="sxs-lookup"><span data-stu-id="64aef-174">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="64aef-175">設定 `messageBack`</span><span class="sxs-lookup"><span data-stu-id="64aef-175">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="64aef-176">省略可能です。</span><span class="sxs-lookup"><span data-stu-id="64aef-176">Optional.</span></span> <span data-ttu-id="64aef-177">アクションの実行時に、ユーザーによってチャット ストリームにエコーされます。</span><span class="sxs-lookup"><span data-stu-id="64aef-177">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="64aef-178">このテキスト *はボット* に送信されません。</span><span class="sxs-lookup"><span data-stu-id="64aef-178">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="64aef-179">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="64aef-179">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="64aef-180">アクションのコンテキスト (一意識別子や JSON オブジェクトなど) をエンコードできます。</span><span class="sxs-lookup"><span data-stu-id="64aef-180">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="64aef-181">アクションの実行時にボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="64aef-181">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="64aef-182">ボットの開発を簡略化するには、このプロパティを使用します。コードでは、ボット ロジックをディスパッチする単一のトップ レベル プロパティをチェックできます。</span><span class="sxs-lookup"><span data-stu-id="64aef-182">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="64aef-183">例</span><span class="sxs-lookup"><span data-stu-id="64aef-183">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="64aef-184">imBack アクションを含むアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="64aef-184">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="64aef-185">アダプティブ カードに `imBack` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="64aef-185">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="64aef-186">必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="64aef-186">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="64aef-187">プロパティ</span><span class="sxs-lookup"><span data-stu-id="64aef-187">Property</span></span> | <span data-ttu-id="64aef-188">説明</span><span class="sxs-lookup"><span data-stu-id="64aef-188">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="64aef-189">設定 `imBack`</span><span class="sxs-lookup"><span data-stu-id="64aef-189">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="64aef-190">チャットでエコーバックする必要がある文字列</span><span class="sxs-lookup"><span data-stu-id="64aef-190">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="64aef-191">例</span><span class="sxs-lookup"><span data-stu-id="64aef-191">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="64aef-192">サインイン アクションを使ったアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="64aef-192">Adaptive Cards with signin action</span></span>

<span data-ttu-id="64aef-193">アダプティブ カードに `signin` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="64aef-193">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="64aef-194">必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="64aef-194">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="64aef-195">プロパティ</span><span class="sxs-lookup"><span data-stu-id="64aef-195">Property</span></span> | <span data-ttu-id="64aef-196">説明</span><span class="sxs-lookup"><span data-stu-id="64aef-196">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="64aef-197">設定 `signin`</span><span class="sxs-lookup"><span data-stu-id="64aef-197">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="64aef-198">リダイレクト先の URL に設定します。</span><span class="sxs-lookup"><span data-stu-id="64aef-198">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="64aef-199">例</span><span class="sxs-lookup"><span data-stu-id="64aef-199">Example</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="64aef-200">呼び出しアクションを含むアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="64aef-200">Adaptive Cards with invoke action</span></span>
 
<span data-ttu-id="64aef-201">アダプティブ カードに `invoke` アクションを含めるには、オブジェクトに次の詳細を含 `msteams` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="64aef-201">To include a `invoke` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="64aef-202">必要に応じて、オブジェクトに追加の非表示 `data` プロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="64aef-202">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="64aef-203">プロパティ</span><span class="sxs-lookup"><span data-stu-id="64aef-203">Property</span></span> | <span data-ttu-id="64aef-204">説明</span><span class="sxs-lookup"><span data-stu-id="64aef-204">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="64aef-205">設定 `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="64aef-205">Set to `task/fetch`</span></span> |
| `data` | <span data-ttu-id="64aef-206">値を設定する</span><span class="sxs-lookup"><span data-stu-id="64aef-206">Set the value</span></span>  |

#### <a name="example"></a><span data-ttu-id="64aef-207">例</span><span class="sxs-lookup"><span data-stu-id="64aef-207">Example</span></span>

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

#### <a name="example-2-with-additional-payload-data"></a><span data-ttu-id="64aef-208">例 2 (追加のペイロード データを含む)</span><span class="sxs-lookup"><span data-stu-id="64aef-208">Example 2 (with additional payload data)</span></span>

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
