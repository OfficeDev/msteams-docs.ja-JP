---
title: Bot から送信されたメッセージの更新と削除
author: WashingtonKayaker
description: Microsoft Teams bot から送信されたメッセージを更新および削除する方法
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 46994c6810197002ef1c108af4f725426395b37f
ms.sourcegitcommit: 2b1fd50466d807869fd173371ba7dfd82a0064ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2020
ms.locfileid: "43957188"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="bc987-103">Bot から送信されたメッセージの更新と削除</span><span class="sxs-lookup"><span data-stu-id="bc987-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="bc987-104">メッセージを更新する</span><span class="sxs-lookup"><span data-stu-id="bc987-104">Updating messages</span></span>

<span data-ttu-id="bc987-105">メッセージをデータの静的なスナップショットにするのではなく、bot がメッセージを送信した後にメッセージを動的に更新することができます。</span><span class="sxs-lookup"><span data-stu-id="bc987-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="bc987-106">動的メッセージ更新は、投票の更新、ボタンの押した後の使用可能なアクションの変更、またはその他の非同期状態の変更などのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="bc987-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="bc987-107">新しいメッセージは、元の種類と一致する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="bc987-107">The new message need not match the original in type.</span></span> <span data-ttu-id="bc987-108">たとえば、元のメッセージに添付ファイルが含まれていた場合、新しいメッセージは単純なテキストメッセージにすることができます。</span><span class="sxs-lookup"><span data-stu-id="bc987-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="bc987-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="bc987-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="bc987-110">既存のメッセージを更新するには、 `Activity`既存のアクティビティ ID を持つ新しいオブジェクト`UpdateActivityAsync`を`TurnContext`クラスのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="bc987-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="bc987-111">[TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="bc987-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="bc987-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="bc987-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="bc987-113">既存のメッセージを更新するには、 `Activity`既存のアクティビティ ID を持つ新しいオブジェクト`updateActivity`を`TurnContext`オブジェクトのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="bc987-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="bc987-114">*「* [Updateactivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--) 」を参照</span><span class="sxs-lookup"><span data-stu-id="bc987-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="bc987-115">Python</span><span class="sxs-lookup"><span data-stu-id="bc987-115">Python</span></span>](#tab/python)

<span data-ttu-id="bc987-116">既存のメッセージを更新するには、 `Activity`既存のアクティビティ ID を持つ新しいオブジェクト`update_activity`を`TurnContext`クラスのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="bc987-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="bc987-117">[TurnContextClass](link to Python API ref docs)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bc987-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="bc987-118">REST API</span><span class="sxs-lookup"><span data-stu-id="bc987-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="bc987-119">任意の web プログラミングテクノロジで Teams アプリを開発し、 [Bot コネクタサービス REST api](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0)を直接呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="bc987-119">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0).</span></span> <span data-ttu-id="bc987-120">これを行うには、API 要求に[認証](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0)セキュリティ手順を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bc987-120">To do so, you'll need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) security procedures with your API requests.</span></span>

<span data-ttu-id="bc987-121">会話内の既存のアクティビティを更新するには`conversationId` 、 `activityId`とを要求エンドポイントに含めます。</span><span class="sxs-lookup"><span data-stu-id="bc987-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="bc987-122">このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bc987-122">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="bc987-123">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="bc987-123">**Request body**</span></span> | <span data-ttu-id="bc987-124">[Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object)オブジェクト</span><span class="sxs-lookup"><span data-stu-id="bc987-124">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object) object</span></span> |
| <span data-ttu-id="bc987-125">**返される値**</span><span class="sxs-lookup"><span data-stu-id="bc987-125">**Returns**</span></span> | <span data-ttu-id="bc987-126">[ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object)オブジェクト</span><span class="sxs-lookup"><span data-stu-id="bc987-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object) object</span></span> |

---

## <a name="deleting-messages"></a><span data-ttu-id="bc987-127">メッセージの削除</span><span class="sxs-lookup"><span data-stu-id="bc987-127">Deleting messages</span></span>

<span data-ttu-id="bc987-128">Bot フレームワークでは、すべてのメッセージに固有のアクティビティ識別子があります。</span><span class="sxs-lookup"><span data-stu-id="bc987-128">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="bc987-129">次に示すように、Bot フレームワークの`DeleteActivity`メソッドを使用してメッセージを削除できます。</span><span class="sxs-lookup"><span data-stu-id="bc987-129">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="bc987-130">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="bc987-130">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="bc987-131">そのメッセージを削除するには、そのアクティビティの ID `DeleteActivityAsync`を`TurnContext`クラスのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="bc987-131">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="bc987-132">*「TurnContext」を参照してください* [。](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="bc987-132">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="bc987-133">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="bc987-133">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="bc987-134">そのメッセージを削除するには、そのアクティビティの ID `deleteActivity`を`TurnContext`オブジェクトのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="bc987-134">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="bc987-135">*「* [Deleteactivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--) 」を参照</span><span class="sxs-lookup"><span data-stu-id="bc987-135">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="bc987-136">Python</span><span class="sxs-lookup"><span data-stu-id="bc987-136">Python</span></span>](#tab/python)

<span data-ttu-id="bc987-137">そのメッセージを削除するには、そのアクティビティの ID `delete_activity`を`TurnContext`オブジェクトのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="bc987-137">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="bc987-138">「 [Activity-update and delete」を](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)参照してください。</span><span class="sxs-lookup"><span data-stu-id="bc987-138">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="bc987-139">REST API</span><span class="sxs-lookup"><span data-stu-id="bc987-139">REST API</span></span>](#tab/rest)

 <span data-ttu-id="bc987-140">会話内の既存のアクティビティを削除するには`conversationId` 、 `activityId`とを要求エンドポイントに含めます。</span><span class="sxs-lookup"><span data-stu-id="bc987-140">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="bc987-141">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="bc987-141">**Request body**</span></span> | <span data-ttu-id="bc987-142">該当なし</span><span class="sxs-lookup"><span data-stu-id="bc987-142">n/a</span></span> |
| <span data-ttu-id="bc987-143">**返される値**</span><span class="sxs-lookup"><span data-stu-id="bc987-143">**Returns**</span></span> | <span data-ttu-id="bc987-144">操作の結果を示す HTTP 状態コード。</span><span class="sxs-lookup"><span data-stu-id="bc987-144">An HTTP Status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="bc987-145">応答の本文には何も指定されていません。</span><span class="sxs-lookup"><span data-stu-id="bc987-145">Nothing is specified in the body of the response.</span></span> |

---
