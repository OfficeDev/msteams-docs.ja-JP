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
# <a name="update-and-delete-messages-sent-from-your-bot"></a>Bot から送信されたメッセージの更新と削除

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a>メッセージを更新する

メッセージをデータの静的なスナップショットにするのではなく、bot がメッセージを送信した後にメッセージを動的に更新することができます。 動的メッセージ更新は、投票の更新、ボタンの押した後の使用可能なアクションの変更、またはその他の非同期状態の変更などのシナリオで使用できます。

新しいメッセージは、元の種類と一致する必要はありません。 たとえば、元のメッセージに添付ファイルが含まれていた場合、新しいメッセージは単純なテキストメッセージにすることができます。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

既存のメッセージを更新するには、 `Activity`既存のアクティビティ ID を持つ新しいオブジェクト`UpdateActivityAsync`を`TurnContext`クラスのメソッドに渡します。 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)を*参照してください*。

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

既存のメッセージを更新するには、 `Activity`既存のアクティビティ ID を持つ新しいオブジェクト`updateActivity`を`TurnContext`オブジェクトのメソッドに渡します。 *「* [Updateactivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--) 」を参照

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

既存のメッセージを更新するには、 `Activity`既存のアクティビティ ID を持つ新しいオブジェクト`update_activity`を`TurnContext`クラスのメソッドに渡します。 [TurnContextClass](link to Python API ref docs)を参照してください。

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[REST API](#tab/rest)

>[!NOTE]
>任意の web プログラミングテクノロジで Teams アプリを開発し、 [Bot コネクタサービス REST api](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0)を直接呼び出すことができます。 これを行うには、API 要求に[認証](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0)セキュリティ手順を実装する必要があります。

会話内の既存のアクティビティを更新するには`conversationId` 、 `activityId`とを要求エンドポイントに含めます。 このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| **要求本文** | [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object)オブジェクト |
| **返される値** | [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object)オブジェクト |

---

## <a name="deleting-messages"></a>メッセージの削除

Bot フレームワークでは、すべてのメッセージに固有のアクティビティ識別子があります。
次に示すように、Bot フレームワークの`DeleteActivity`メソッドを使用してメッセージを削除できます。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

そのメッセージを削除するには、そのアクティビティの ID `DeleteActivityAsync`を`TurnContext`クラスのメソッドに渡します。 *「TurnContext」を参照してください* [。](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

そのメッセージを削除するには、そのアクティビティの ID `deleteActivity`を`TurnContext`オブジェクトのメソッドに渡します。 *「* [Deleteactivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--) 」を参照

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

そのメッセージを削除するには、そのアクティビティの ID `delete_activity`を`TurnContext`オブジェクトのメソッドに渡します。 「 [Activity-update and delete」を](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)参照してください。

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

 会話内の既存のアクティビティを削除するには`conversationId` 、 `activityId`とを要求エンドポイントに含めます。

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| **要求本文** | 該当なし |
| **返される値** | 操作の結果を示す HTTP 状態コード。 応答の本文には何も指定されていません。 |

---
