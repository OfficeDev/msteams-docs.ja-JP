---
title: Bot から送信されたメッセージの更新と削除
author: WashingtonKayaker
description: Microsoft Teams bot から送信されたメッセージを更新および削除する方法
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 012a6edb77f75c43cff01c58fb94e03fd4f61a85
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675009"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="b0c31-103">Bot から送信されたメッセージの更新と削除</span><span class="sxs-lookup"><span data-stu-id="b0c31-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="b0c31-104">メッセージを更新する</span><span class="sxs-lookup"><span data-stu-id="b0c31-104">Updating messages</span></span>

<span data-ttu-id="b0c31-105">メッセージをデータの静的なスナップショットにするのではなく、bot がメッセージを送信した後にメッセージを動的に更新することができます。</span><span class="sxs-lookup"><span data-stu-id="b0c31-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="b0c31-106">動的メッセージ更新は、投票の更新、ボタンの押した後の使用可能なアクションの変更、またはその他の非同期状態の変更などのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="b0c31-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="b0c31-107">新しいメッセージは、元の種類と一致する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b0c31-107">The new message need not match the original in type.</span></span> <span data-ttu-id="b0c31-108">たとえば、元のメッセージに添付ファイルが含まれていた場合、新しいメッセージは単純なテキストメッセージにすることができます。</span><span class="sxs-lookup"><span data-stu-id="b0c31-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="b0c31-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b0c31-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="b0c31-110">既存のメッセージを更新するには、 `Activity`既存のアクティビティ ID を持つ新しいオブジェクト`UpdateActivityAsync`を`TurnContext`クラスのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="b0c31-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="b0c31-111">[TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="b0c31-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="b0c31-112">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="b0c31-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="b0c31-113">既存のメッセージを更新するには、 `Activity`既存のアクティビティ ID を持つ新しいオブジェクト`updateActivity`を`TurnContext`オブジェクトのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="b0c31-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b0c31-114">*「* [Updateactivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--) 」を参照</span><span class="sxs-lookup"><span data-stu-id="b0c31-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="pythontabpython"></a>[<span data-ttu-id="b0c31-115">Python</span><span class="sxs-lookup"><span data-stu-id="b0c31-115">Python</span></span>](#tab/python)

<span data-ttu-id="b0c31-116">既存のメッセージを更新するには、 `Activity`既存のアクティビティ ID を持つ新しいオブジェクト`update_activity`を`TurnContext`クラスのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="b0c31-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="b0c31-117">[TurnContextClass](link to Python API ref docs)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b0c31-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

---

## <a name="deleting-messages"></a><span data-ttu-id="b0c31-118">メッセージの削除</span><span class="sxs-lookup"><span data-stu-id="b0c31-118">Deleting messages</span></span>

<span data-ttu-id="b0c31-119">Bot フレームワークでは、すべてのメッセージに固有のアクティビティ識別子があります。</span><span class="sxs-lookup"><span data-stu-id="b0c31-119">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="b0c31-120">次に示すように、Bot フレームワークの`DeleteActivity`メソッドを使用してメッセージを削除できます。</span><span class="sxs-lookup"><span data-stu-id="b0c31-120">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="b0c31-121">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b0c31-121">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="b0c31-122">そのメッセージを削除するには、そのアクティビティの ID `DeleteActivityAsync`を`TurnContext`クラスのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="b0c31-122">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="b0c31-123">*「TurnContext」を参照してください* [。](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="b0c31-123">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="b0c31-124">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="b0c31-124">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="b0c31-125">そのメッセージを削除するには、そのアクティビティの ID `deleteActivity`を`TurnContext`オブジェクトのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="b0c31-125">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b0c31-126">*「* [Deleteactivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--) 」を参照</span><span class="sxs-lookup"><span data-stu-id="b0c31-126">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="pythontabpython"></a>[<span data-ttu-id="b0c31-127">Python</span><span class="sxs-lookup"><span data-stu-id="b0c31-127">Python</span></span>](#tab/python)

<span data-ttu-id="b0c31-128">そのメッセージを削除するには、そのアクティビティの ID `delete_activity`を`TurnContext`オブジェクトのメソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="b0c31-128">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b0c31-129">[Delete_activity](link to Python API ref docs)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b0c31-129">See [delete_activity](link to Python API ref docs).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

---

