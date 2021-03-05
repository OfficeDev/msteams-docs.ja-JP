---
title: ボットから送信されたメッセージを更新および削除する
author: WashingtonKayaker
description: Microsoft Teams ボットから送信されたメッセージを更新および削除する方法
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 664bd531bdee0093c6766bc23e35d2bf10307eb4
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449501"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="13218-103">ボットから送信されたメッセージを更新および削除する</span><span class="sxs-lookup"><span data-stu-id="13218-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="update-messages"></a><span data-ttu-id="13218-104">メッセージを更新する</span><span class="sxs-lookup"><span data-stu-id="13218-104">Update messages</span></span>

<span data-ttu-id="13218-105">ボットは、送信後にメッセージを動的に更新できます。</span><span class="sxs-lookup"><span data-stu-id="13218-105">Your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="13218-106">ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオで、動的メッセージ更新を使用できます。</span><span class="sxs-lookup"><span data-stu-id="13218-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="13218-107">新しいメッセージは、型の元のメッセージと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="13218-107">The new message need not match the original in type.</span></span> <span data-ttu-id="13218-108">たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージには単純なテキスト メッセージを指定できます。</span><span class="sxs-lookup"><span data-stu-id="13218-108">For example, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="13218-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="13218-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="13218-110">既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをクラス `Activity` の `UpdateActivityAsync` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="13218-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="13218-111">[「TurnContextClass」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="13218-111">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="13218-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="13218-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="13218-113">既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをオブジェクトの `Activity` `updateActivity` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="13218-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="13218-114">updateActivity [を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="13218-114">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="13218-115">Python</span><span class="sxs-lookup"><span data-stu-id="13218-115">Python</span></span>](#tab/python)

<span data-ttu-id="13218-116">既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをクラス `Activity` の `update_activity` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="13218-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="13218-117">[「TurnContextClass」を参照してください](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest)。</span><span class="sxs-lookup"><span data-stu-id="13218-117">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="13218-118">REST API</span><span class="sxs-lookup"><span data-stu-id="13218-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="13218-119">任意の Web プログラミング テクノロジで Teams アプリを開発し、ボット コネクタ サービス [REST API を直接呼び出します](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="13218-119">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="13218-120">これを行うには、API 要求で [認証](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) セキュリティ手順を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="13218-120">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="13218-121">会話内の既存のアクティビティを更新するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="13218-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="13218-122">このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="13218-122">To complete this scenario, you must cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="13218-123">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="13218-123">**Request body**</span></span> | <span data-ttu-id="13218-124">[Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)オブジェクト</span><span class="sxs-lookup"><span data-stu-id="13218-124">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object</span></span> |
| <span data-ttu-id="13218-125">**返される値**</span><span class="sxs-lookup"><span data-stu-id="13218-125">**Returns**</span></span> | <span data-ttu-id="13218-126">[ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)オブジェクト</span><span class="sxs-lookup"><span data-stu-id="13218-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object</span></span> |

---

## <a name="update-cards"></a><span data-ttu-id="13218-127">カードの更新</span><span class="sxs-lookup"><span data-stu-id="13218-127">Update cards</span></span>

<span data-ttu-id="13218-128">ボタン選択時に既存のカードを更新するには、受信アクティビティ `ReplyToId` を使用できます。</span><span class="sxs-lookup"><span data-stu-id="13218-128">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="13218-129">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="13218-129">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="13218-130">ボタンクリックで既存のカードを更新するには、更新されたカードとアクティビティ ID を持つ新しいオブジェクトをクラスのメソッド `Activity` `ReplyToId` `UpdateActivityAsync` に渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="13218-130">To update existing card on a button click, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="13218-131">[「TurnContextClass」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="13218-131">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>
```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="13218-132">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="13218-132">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="13218-133">ボタンクリックで既存のカードを更新するには、更新されたカードとアクティビティ ID を持つ新しいオブジェクトをオブジェクトのメソッド `Activity` `replyToId` `updateActivity` に渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="13218-133">To update existing card on a button click, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="13218-134">updateActivity [を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="13218-134">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>
```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="13218-135">Python</span><span class="sxs-lookup"><span data-stu-id="13218-135">Python</span></span>](#tab/python)

<span data-ttu-id="13218-136">ボタンクリックで既存のカードを更新するには、更新されたカードとアクティビティ ID を持つ新しいオブジェクトをクラスのメソッド `Activity` `reply_to_id` `update_activity` に渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="13218-136">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="13218-137">[「TurnContextClass」を参照してください](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest)。</span><span class="sxs-lookup"><span data-stu-id="13218-137">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)

```

## <a name="delete-messages"></a><span data-ttu-id="13218-138">メッセージを削除する</span><span class="sxs-lookup"><span data-stu-id="13218-138">Delete messages</span></span>

<span data-ttu-id="13218-139">ボット フレームワークでは、すべてのメッセージに固有のアクティビティ識別子があります。</span><span class="sxs-lookup"><span data-stu-id="13218-139">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="13218-140">次に示すように、ボット フレームワークのメソッドを使用 `DeleteActivity` してメッセージを削除できます。</span><span class="sxs-lookup"><span data-stu-id="13218-140">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="13218-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="13218-141">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="13218-142">そのメッセージを削除するには、そのアクティビティの ID をクラス `DeleteActivityAsync` のメソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="13218-142">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="13218-143">[「TurnContext.DeleteActivityAsync メソッド」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="13218-143">See [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="13218-144">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="13218-144">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="13218-145">そのメッセージを削除するには、そのアクティビティの ID をオブジェクトの `deleteActivity` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="13218-145">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="13218-146">[「deleteActivity」を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="13218-146">See [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="13218-147">Python</span><span class="sxs-lookup"><span data-stu-id="13218-147">Python</span></span>](#tab/python)

<span data-ttu-id="13218-148">そのメッセージを削除するには、そのアクティビティの ID をオブジェクトの `delete_activity` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="13218-148">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="13218-149">[「activity-update-and-delete」を参照してください](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。</span><span class="sxs-lookup"><span data-stu-id="13218-149">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="13218-150">REST API</span><span class="sxs-lookup"><span data-stu-id="13218-150">REST API</span></span>](#tab/rest)

 <span data-ttu-id="13218-151">会話内の既存のアクティビティを削除するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="13218-151">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="13218-152">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="13218-152">**Request body**</span></span> | <span data-ttu-id="13218-153">該当なし</span><span class="sxs-lookup"><span data-stu-id="13218-153">n/a</span></span> |
| <span data-ttu-id="13218-154">**返される値**</span><span class="sxs-lookup"><span data-stu-id="13218-154">**Returns**</span></span> | <span data-ttu-id="13218-155">操作の結果を示す HTTP 状態コード。</span><span class="sxs-lookup"><span data-stu-id="13218-155">An HTTP Status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="13218-156">応答の本文には何も指定されていません。</span><span class="sxs-lookup"><span data-stu-id="13218-156">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-samples"></a><span data-ttu-id="13218-157">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="13218-157">Code samples</span></span>

<span data-ttu-id="13218-158">公式の会話の基本は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="13218-158">The official conversation basics are as follows:</span></span>

| <span data-ttu-id="13218-159">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="13218-159">Sample Name</span></span>           | <span data-ttu-id="13218-160">説明</span><span class="sxs-lookup"><span data-stu-id="13218-160">Description</span></span>                                                                      | <span data-ttu-id="13218-161">.NET</span><span class="sxs-lookup"><span data-stu-id="13218-161">.NET</span></span>    | <span data-ttu-id="13218-162">JavaScript</span><span class="sxs-lookup"><span data-stu-id="13218-162">JavaScript</span></span>   | <span data-ttu-id="13218-163">Python</span><span class="sxs-lookup"><span data-stu-id="13218-163">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="13218-164">Teams での会話の基本</span><span class="sxs-lookup"><span data-stu-id="13218-164">Teams Conversation Basics</span></span>  | <span data-ttu-id="13218-165">メッセージの更新や削除など、Teams での会話の基本を示します。</span><span class="sxs-lookup"><span data-stu-id="13218-165">Demonstrates basics of conversations in Teams, including message update and delete.</span></span>|[<span data-ttu-id="13218-166">.NET&nbsp;Core</span><span class="sxs-lookup"><span data-stu-id="13218-166">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="13218-167">JavaScript</span><span class="sxs-lookup"><span data-stu-id="13218-167">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="13218-168">Python</span><span class="sxs-lookup"><span data-stu-id="13218-168">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
