---
title: Bot にカードアクションを追加する
description: Microsoft Teams でのカードアクションと、それらを bot で使用する方法について説明します。
keywords: teams のボットカードのアクション
ms.openlocfilehash: e0b050cde9adf5bd811d5d95ce1c6f1bf60546a1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674830"
---
# <a name="card-actions"></a><span data-ttu-id="ffa94-104">カードのアクション</span><span class="sxs-lookup"><span data-stu-id="ffa94-104">Card actions</span></span>

<span data-ttu-id="ffa94-105">Teams のボットおよびメッセージング拡張機能によって使用されるカード[`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)は、次のアクティビティ () の種類をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ffa94-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="ffa94-106">これらのアクションは、コネクタ`potentialActions`から使用された場合、Office 365 コネクタカードとは異なることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ffa94-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="ffa94-107">型</span><span class="sxs-lookup"><span data-stu-id="ffa94-107">Type</span></span> | <span data-ttu-id="ffa94-108">Action</span><span class="sxs-lookup"><span data-stu-id="ffa94-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="ffa94-109">既定のブラウザーで URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="ffa94-110">(ボタンをクリックしたユーザーまたはカードをタップしたユーザーから) メッセージとペイロードを bot に送信し、別のメッセージをチャットストリームに送信します。</span><span class="sxs-lookup"><span data-stu-id="ffa94-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="ffa94-111">Bot (ボタンをクリックしたユーザーまたはカードをタップしたユーザーから) にメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="ffa94-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="ffa94-112">このメッセージ (ユーザーから bot) は、すべての会話参加者に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="ffa94-113">Bot にメッセージとペイロードを送信します (ボタンをクリックしたユーザー、またはカードをタップしたユーザーから)。</span><span class="sxs-lookup"><span data-stu-id="ffa94-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="ffa94-114">このメッセージは表示されません。</span><span class="sxs-lookup"><span data-stu-id="ffa94-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="ffa94-115">OAuth フローを開始し、ボットがセキュリティ保護されたサービスで接続できるようにします。</span><span class="sxs-lookup"><span data-stu-id="ffa94-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="ffa94-116">Teams では、 `CardAction`上記の表に記載されていない種類はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ffa94-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="ffa94-117">Teams はプロパティを`potentialActions`サポートしていません。</span><span class="sxs-lookup"><span data-stu-id="ffa94-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="ffa94-118">カードアクションは、Bot フレームワーク/Azure Bot サービスの推奨される[アクション](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button)とは異なります。</span><span class="sxs-lookup"><span data-stu-id="ffa94-118">Card actions are different than [suggested actions](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="ffa94-119">Microsoft Teams では、推奨されるアクションはサポートされていません。 Teams の bot メッセージにボタンを表示する場合は、カードを使用します。</span><span class="sxs-lookup"><span data-stu-id="ffa94-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="ffa94-120">メッセージ拡張機能の一部としてカードアクションを使用している場合、カードがチャネルに送信されるまで、アクションは機能しません (カードが [新規作成] メッセージボックスにある間は機能しません)。</span><span class="sxs-lookup"><span data-stu-id="ffa94-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="ffa94-121">Teams は、アダプティブカードによってのみ使用される[アダプティブカードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)もサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ffa94-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="ffa94-122">これらの操作は、このリファレンスの最後にあるセクションに記載されています。</span><span class="sxs-lookup"><span data-stu-id="ffa94-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="ffa94-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="ffa94-123">openUrl</span></span>

<span data-ttu-id="ffa94-124">このアクションの種類では、既定のブラウザーで起動する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ffa94-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="ffa94-125">Bot がクリックされたボタンに関する通知を受け取っていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ffa94-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="ffa94-126">この`value`フィールドには、完全で正しい形式の URL が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ffa94-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="ffa94-127">messageBack</span><span class="sxs-lookup"><span data-stu-id="ffa94-127">messageBack</span></span>

<span data-ttu-id="ffa94-128">で`messageBack`は、次のプロパティを使用して、完全にカスタマイズされたアクションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="ffa94-129">プロパティ</span><span class="sxs-lookup"><span data-stu-id="ffa94-129">Property</span></span> | <span data-ttu-id="ffa94-130">説明</span><span class="sxs-lookup"><span data-stu-id="ffa94-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="ffa94-131">ボタンのラベルとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="ffa94-132">省略可能です。</span><span class="sxs-lookup"><span data-stu-id="ffa94-132">Optional.</span></span> <span data-ttu-id="ffa94-133">アクションの実行時にユーザーによってチャットストリームにエコーされます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="ffa94-134">このテキストは bot に送信され*ません*。</span><span class="sxs-lookup"><span data-stu-id="ffa94-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="ffa94-135">アクションが実行されたときに bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="ffa94-136">一意の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードできます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="ffa94-137">アクションが実行されたときに bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="ffa94-138">このプロパティを使用して、ボットの開発を簡素化します。コードでは、ボットロジックをディスパッチするために1つのトップレベルのプロパティをチェックできます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="ffa94-139">柔軟`messageBack`には、コードでは、を使用`displayText`しないで、表示されるユーザーメッセージを履歴に残すことを選択できます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="ffa94-140">この`value`プロパティには、シリアル化された json 文字列または json オブジェクトのいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="ffa94-141">受信メッセージの例</span><span class="sxs-lookup"><span data-stu-id="ffa94-141">Inbound message example</span></span>

<span data-ttu-id="ffa94-142">`replyToId`カードアクションの送信元のメッセージの ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="ffa94-143">メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="ffa94-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="ffa94-144">imBack</span><span class="sxs-lookup"><span data-stu-id="ffa94-144">imBack</span></span>

<span data-ttu-id="ffa94-145">この操作によって、ユーザーが通常のチャットメッセージに入力した場合と同じように、bot に返されるメッセージがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="ffa94-146">チャネルを使用している場合、ユーザーとその他のすべてのユーザーは、そのボタンの応答を確認できます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="ffa94-147">フィールド`value`にはチャットでのテキスト文字列が含まれている必要があります。そのため、bot に送り返されます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="ffa94-148">これは、ボットで処理して必要なロジックを実行するメッセージテキストです。</span><span class="sxs-lookup"><span data-stu-id="ffa94-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="ffa94-149">メモ: このフィールドは単純な文字列です。書式設定または隠し文字はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ffa94-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="ffa94-150">invoke</span><span class="sxs-lookup"><span data-stu-id="ffa94-150">invoke</span></span>

<span data-ttu-id="ffa94-151">アクション`invoke`は、[タスクモジュール](~/task-modules-and-cards/task-modules/task-modules-bots.md)を呼び出すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="ffa94-152">アクション`invoke`には、、 `type` `title`、および`value`の3つのプロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="ffa94-153">この`value`プロパティには、文字列、文字列 json オブジェクト、または json オブジェクトを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="ffa94-154">ユーザーがボタンをクリックすると、bot は、追加`value`情報を含むオブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="ffa94-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="ffa94-155">アクティビティの種類は ( `invoke` `message` `activity.Type == "invoke"`) の代わりになることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ffa94-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="ffa94-156">例: Invoke button definition (.NET)</span><span class="sxs-lookup"><span data-stu-id="ffa94-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="ffa94-157">例: 着信呼び出しメッセージ</span><span class="sxs-lookup"><span data-stu-id="ffa94-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="ffa94-158">トップレベル`replyToId`のプロパティには、カードアクションの送信元であるメッセージの ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="ffa94-159">メッセージを更新する場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="ffa94-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="ffa94-160">signin</span><span class="sxs-lookup"><span data-stu-id="ffa94-160">signin</span></span>

<span data-ttu-id="ffa94-161">OAuth フローを開始し、次の詳細に説明するように、ボットでセキュリティ保護されたサービスとの接続を許可します。 [bot での認証フロー](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="ffa94-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="ffa94-162">アダプティブカードのアクション</span><span class="sxs-lookup"><span data-stu-id="ffa94-162">Adaptive Cards actions</span></span>

<span data-ttu-id="ffa94-163">アダプティブカードは、次の3種類のアクションをサポートします。</span><span class="sxs-lookup"><span data-stu-id="ffa94-163">Adaptive Cards support three action types:</span></span>

* [<span data-ttu-id="ffa94-164">アクション (OpenUrl)</span><span class="sxs-lookup"><span data-stu-id="ffa94-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="ffa94-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="ffa94-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="ffa94-166">ShowCard</span><span class="sxs-lookup"><span data-stu-id="ffa94-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)

<span data-ttu-id="ffa94-167">前述の操作に加え`Action.Submit`て、の`msteams` `data` `Action.Submit`オブジェクトのプロパティを使用して、既存の Bot フレームワークアクションをサポートするようにアダプティブカードのペイロードを変更できます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-167">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="ffa94-168">次のセクションでは、既存の Bot フレームワークアクションをアダプティブカードで使用する方法について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="ffa94-168">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="ffa94-169">MessageBack アクションを備えたアダプティブカード</span><span class="sxs-lookup"><span data-stu-id="ffa94-169">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="ffa94-170">アダプティブカードに`messageBack`アクションを含めるには、 `msteams`オブジェクトに次の詳細情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ffa94-170">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="ffa94-171">必要に応じて、 `data`追加の非表示プロパティをオブジェクトに含めることができることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ffa94-171">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="ffa94-172">プロパティ</span><span class="sxs-lookup"><span data-stu-id="ffa94-172">Property</span></span> | <span data-ttu-id="ffa94-173">説明</span><span class="sxs-lookup"><span data-stu-id="ffa94-173">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="ffa94-174">に設定`messageBack`</span><span class="sxs-lookup"><span data-stu-id="ffa94-174">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="ffa94-175">省略可能です。</span><span class="sxs-lookup"><span data-stu-id="ffa94-175">Optional.</span></span> <span data-ttu-id="ffa94-176">アクションの実行時にユーザーによってチャットストリームにエコーされます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-176">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="ffa94-177">このテキストは bot に送信され*ません*。</span><span class="sxs-lookup"><span data-stu-id="ffa94-177">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="ffa94-178">アクションが実行されたときに bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-178">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="ffa94-179">一意の識別子や JSON オブジェクトなど、アクションのコンテキストをエンコードできます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-179">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="ffa94-180">アクションが実行されたときに bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-180">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="ffa94-181">このプロパティを使用して、ボットの開発を簡素化します。コードでは、ボットロジックをディスパッチするために1つのトップレベルのプロパティをチェックできます。</span><span class="sxs-lookup"><span data-stu-id="ffa94-181">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="ffa94-182">例</span><span class="sxs-lookup"><span data-stu-id="ffa94-182">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="ffa94-183">ImBack アクションを備えたアダプティブカード</span><span class="sxs-lookup"><span data-stu-id="ffa94-183">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="ffa94-184">アダプティブカードに`imBack`アクションを含めるには、 `msteams`オブジェクトに次の詳細情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ffa94-184">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="ffa94-185">必要に応じて、 `data`追加の非表示プロパティをオブジェクトに含めることができることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ffa94-185">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="ffa94-186">プロパティ</span><span class="sxs-lookup"><span data-stu-id="ffa94-186">Property</span></span> | <span data-ttu-id="ffa94-187">説明</span><span class="sxs-lookup"><span data-stu-id="ffa94-187">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="ffa94-188">に設定`imBack`</span><span class="sxs-lookup"><span data-stu-id="ffa94-188">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="ffa94-189">チャットでエコーバックする必要がある文字列</span><span class="sxs-lookup"><span data-stu-id="ffa94-189">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="ffa94-190">例</span><span class="sxs-lookup"><span data-stu-id="ffa94-190">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="ffa94-191">サインインカードとサインインアクション</span><span class="sxs-lookup"><span data-stu-id="ffa94-191">Adaptive Cards with signin action</span></span>

<span data-ttu-id="ffa94-192">アダプティブカードに`signin`アクションを含めるには、 `msteams`オブジェクトに次の詳細情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ffa94-192">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="ffa94-193">必要に応じて、 `data`追加の非表示プロパティをオブジェクトに含めることができることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ffa94-193">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="ffa94-194">プロパティ</span><span class="sxs-lookup"><span data-stu-id="ffa94-194">Property</span></span> | <span data-ttu-id="ffa94-195">説明</span><span class="sxs-lookup"><span data-stu-id="ffa94-195">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="ffa94-196">に設定`signin`</span><span class="sxs-lookup"><span data-stu-id="ffa94-196">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="ffa94-197">リダイレクト先の URL に設定します。</span><span class="sxs-lookup"><span data-stu-id="ffa94-197">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="ffa94-198">例</span><span class="sxs-lookup"><span data-stu-id="ffa94-198">Example</span></span>

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