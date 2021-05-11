---
title: ボットから送信されたメッセージを更新および削除する
author: WashingtonKayaker
description: ボットから送信されたメッセージを更新およびMicrosoft Teamsする方法
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 90dc50fd2ec153813457f199ac029e17a0157502
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101535"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="f9115-103">ボットから送信されたメッセージを更新および削除する</span><span class="sxs-lookup"><span data-stu-id="f9115-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="f9115-104">ボットは、メッセージをデータの静的スナップショットとしてではなく、送信後に動的に更新できます。</span><span class="sxs-lookup"><span data-stu-id="f9115-104">Your bot can dynamically update messages after sending them instead of having them as static snapshots of data.</span></span> <span data-ttu-id="f9115-105">ボット フレームワークのメソッドを使用してメッセージを削除 `DeleteActivity` することもできます。</span><span class="sxs-lookup"><span data-stu-id="f9115-105">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="update-messages"></a><span data-ttu-id="f9115-106">メッセージを更新する</span><span class="sxs-lookup"><span data-stu-id="f9115-106">Update messages</span></span>

<span data-ttu-id="f9115-107">ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更など、シナリオに対して動的なメッセージ更新を使用できます。</span><span class="sxs-lookup"><span data-stu-id="f9115-107">You can use dynamic message updates for scenarios, such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="f9115-108">新しいメッセージが元の種類と一致する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f9115-108">It is not necessary for the new message to match the original in type.</span></span> <span data-ttu-id="f9115-109">たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージには単純なテキスト メッセージを指定できます。</span><span class="sxs-lookup"><span data-stu-id="f9115-109">For example, if the original message contains an attachment, the new message can be a simple text message.</span></span>

# <a name="c"></a>[<span data-ttu-id="f9115-110">C#</span><span class="sxs-lookup"><span data-stu-id="f9115-110">C#</span></span>](#tab/dotnet)

<span data-ttu-id="f9115-111">既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをクラス `Activity` の `UpdateActivityAsync` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="f9115-111">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="f9115-112">詳細については [、「TurnContextClass」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-112">For more information, see [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="f9115-113">TypeScript</span><span class="sxs-lookup"><span data-stu-id="f9115-113">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="f9115-114">既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをオブジェクトの `Activity` `updateActivity` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="f9115-114">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f9115-115">詳細については [、「updateActivity 」を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-115">For more information, see [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="f9115-116">Python</span><span class="sxs-lookup"><span data-stu-id="f9115-116">Python</span></span>](#tab/python)

<span data-ttu-id="f9115-117">既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをクラス `Activity` の `update_activity` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="f9115-117">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="f9115-118">[「TurnContextClass」を参照してください](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-118">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="f9115-119">REST API</span><span class="sxs-lookup"><span data-stu-id="f9115-119">REST API</span></span>](#tab/rest)

> [!NOTE]

> <span data-ttu-id="f9115-120">Web プログラミング テクノロジTeamsアプリを開発し、ボット コネクタ サービス REST [API を直接呼び出します](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-120">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="f9115-121">これを行うには、API 要求で [認証](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) セキュリティ手順を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9115-121">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="f9115-122">会話内の既存のアクティビティを更新するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9115-122">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="f9115-123">このシナリオを完了するには、元の通話後に返されたアクティビティ ID をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9115-123">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="f9115-124">要求</span><span class="sxs-lookup"><span data-stu-id="f9115-124">Request</span></span> |<span data-ttu-id="f9115-125">応答</span><span class="sxs-lookup"><span data-stu-id="f9115-125">Response</span></span> |
|----|----|
| <span data-ttu-id="f9115-126">[Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="f9115-126">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object.</span></span> | <span data-ttu-id="f9115-127">[ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="f9115-127">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object.</span></span> |

---
* * *

<span data-ttu-id="f9115-128">メッセージが更新されたので、受信アクティビティのボタン選択の既存のカードを更新します。</span><span class="sxs-lookup"><span data-stu-id="f9115-128">Now that you have updated messages, update the existing card on button selection for incoming activities.</span></span>

## <a name="update-cards"></a><span data-ttu-id="f9115-129">カードの更新</span><span class="sxs-lookup"><span data-stu-id="f9115-129">Update cards</span></span>

<span data-ttu-id="f9115-130">ボタン選択時に既存のカードを更新するには、受信アクティビティ `ReplyToId` を使用できます。</span><span class="sxs-lookup"><span data-stu-id="f9115-130">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f9115-131">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f9115-131">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f9115-132">ボタン選択の既存のカードを更新するには、更新されたカードとアクティビティ ID を持つ新しいオブジェクトをクラスのメソッド `Activity` `ReplyToId` `UpdateActivityAsync` に渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="f9115-132">To update existing card on a button selection, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="f9115-133">[「TurnContextClass」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-133">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="f9115-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="f9115-134">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="f9115-135">ボタン選択の既存のカードを更新するには、新しいオブジェクトに更新されたカードとアクティビティ ID をオブジェクトのメソッド `Activity` `replyToId` `updateActivity` に渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="f9115-135">To update existing card on a button selection, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f9115-136">updateActivity [を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-136">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="f9115-137">Python</span><span class="sxs-lookup"><span data-stu-id="f9115-137">Python</span></span>](#tab/python)

<span data-ttu-id="f9115-138">ボタンクリックで既存のカードを更新するには、更新されたカードとアクティビティ ID を持つ新しいオブジェクトをクラスのメソッド `Activity` `reply_to_id` `update_activity` に渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="f9115-138">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="f9115-139">[「TurnContextClass」を参照してください](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-139">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="f9115-140">REST API</span><span class="sxs-lookup"><span data-stu-id="f9115-140">REST API</span></span>](#tab/rest)

> [!NOTE]
> <span data-ttu-id="f9115-141">任意の web プログラミング Teamsアプリを開発し、ボット コネクタ サービス[REST API を直接呼び出します](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-141">You can develop Teams apps in any web programming technology and directly call the [bot connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="f9115-142">これを行うには、API 要求 [で認証](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) セキュリティ手順を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9115-142">To do this, you must implement [authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="f9115-143">会話内の既存のアクティビティを更新するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9115-143">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="f9115-144">このシナリオを完了するには、元の通話後に返されたアクティビティ ID をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9115-144">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="f9115-145">要求</span><span class="sxs-lookup"><span data-stu-id="f9115-145">Request</span></span> |<span data-ttu-id="f9115-146">応答</span><span class="sxs-lookup"><span data-stu-id="f9115-146">Response</span></span> |
|----|----|
| <span data-ttu-id="f9115-147">アクティビティ [オブジェクト](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) 。</span><span class="sxs-lookup"><span data-stu-id="f9115-147">An [activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object.</span></span> | <span data-ttu-id="f9115-148">[ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="f9115-148">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object.</span></span> |

* * *

<span data-ttu-id="f9115-149">カードを更新したので、ボット フレームワークを使用してメッセージを削除できます。</span><span class="sxs-lookup"><span data-stu-id="f9115-149">Now that you have updated cards, you can delete messages using the Bot Framework.</span></span>

## <a name="delete-messages"></a><span data-ttu-id="f9115-150">メッセージを削除する</span><span class="sxs-lookup"><span data-stu-id="f9115-150">Delete messages</span></span>

<span data-ttu-id="f9115-151">ボット フレームワークでは、すべてのメッセージに固有のアクティビティ識別子があります。</span><span class="sxs-lookup"><span data-stu-id="f9115-151">In the Bot Framework, every message has its unique activity identifier.</span></span> <span data-ttu-id="f9115-152">メッセージは、ボット フレームワークのメソッドを使用して削除 `DeleteActivity` できます。</span><span class="sxs-lookup"><span data-stu-id="f9115-152">Messages can be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

# <a name="c"></a>[<span data-ttu-id="f9115-153">C#</span><span class="sxs-lookup"><span data-stu-id="f9115-153">C#</span></span>](#tab/dotnet)

<span data-ttu-id="f9115-154">メッセージを削除するには、そのアクティビティの ID をクラスの `DeleteActivityAsync` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="f9115-154">To delete a message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="f9115-155">詳細については [、「TurnContext.DeleteActivityAsync メソッド」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-155">For more information, see [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="f9115-156">TypeScript</span><span class="sxs-lookup"><span data-stu-id="f9115-156">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="f9115-157">メッセージを削除するには、そのアクティビティの ID をオブジェクトの `deleteActivity` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="f9115-157">To delete a message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f9115-158">詳細については [、「deleteActivity」を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f9115-158">For more information, see [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="f9115-159">Python</span><span class="sxs-lookup"><span data-stu-id="f9115-159">Python</span></span>](#tab/python)

<span data-ttu-id="f9115-160">そのメッセージを削除するには、そのアクティビティの ID をオブジェクトの `delete_activity` メソッドに渡 `TurnContext` します。</span><span class="sxs-lookup"><span data-stu-id="f9115-160">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f9115-161">詳細については [、「activity-update-and-delete」を参照してください](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。</span><span class="sxs-lookup"><span data-stu-id="f9115-161">For more information, see [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="f9115-162">REST API</span><span class="sxs-lookup"><span data-stu-id="f9115-162">REST API</span></span>](#tab/rest)

<span data-ttu-id="f9115-163">会話内の既存のアクティビティを削除するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9115-163">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| <span data-ttu-id="f9115-164">**要求と応答**</span><span class="sxs-lookup"><span data-stu-id="f9115-164">**Request and response**</span></span> | <span data-ttu-id="f9115-165">**説明**</span><span class="sxs-lookup"><span data-stu-id="f9115-165">**Description**</span></span> |
|----|----|
| <span data-ttu-id="f9115-166">該当なし</span><span class="sxs-lookup"><span data-stu-id="f9115-166">N/A</span></span> | <span data-ttu-id="f9115-167">操作の結果を示す HTTP 状態コード。</span><span class="sxs-lookup"><span data-stu-id="f9115-167">An HTTP status code indicating the outcome of the operation.</span></span> <span data-ttu-id="f9115-168">応答の本文には何も指定されていません。</span><span class="sxs-lookup"><span data-stu-id="f9115-168">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-sample"></a><span data-ttu-id="f9115-169">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="f9115-169">Code sample</span></span>

<span data-ttu-id="f9115-170">次のコード サンプルは、会話の基本を示しています。</span><span class="sxs-lookup"><span data-stu-id="f9115-170">The following code sample demonstrates basics of conversations:</span></span>

| <span data-ttu-id="f9115-171">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="f9115-171">**Sample name**</span></span> | <span data-ttu-id="f9115-172">**説明**</span><span class="sxs-lookup"><span data-stu-id="f9115-172">**Description**</span></span> | <span data-ttu-id="f9115-173">**.NET**</span><span class="sxs-lookup"><span data-stu-id="f9115-173">**.NET**</span></span> | <span data-ttu-id="f9115-174">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="f9115-174">**Node.js**</span></span> | <span data-ttu-id="f9115-175">**Python**</span><span class="sxs-lookup"><span data-stu-id="f9115-175">**Python**</span></span> |
|----------------------|-----------------|--------|-------------|--------|
| <span data-ttu-id="f9115-176">Teams での会話の基本</span><span class="sxs-lookup"><span data-stu-id="f9115-176">Teams Conversation Basics</span></span>  | <span data-ttu-id="f9115-177">メッセージの更新と削除を含むTeamsの基本を示します。</span><span class="sxs-lookup"><span data-stu-id="f9115-177">Demonstrates basics of conversations in Teams including message update and delete.</span></span> | [<span data-ttu-id="f9115-178">View</span><span class="sxs-lookup"><span data-stu-id="f9115-178">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="f9115-179">View</span><span class="sxs-lookup"><span data-stu-id="f9115-179">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="f9115-180">View</span><span class="sxs-lookup"><span data-stu-id="f9115-180">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a><span data-ttu-id="f9115-181">次の手順</span><span class="sxs-lookup"><span data-stu-id="f9115-181">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9115-182">コンテキストTeams取得</span><span class="sxs-lookup"><span data-stu-id="f9115-182">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)
