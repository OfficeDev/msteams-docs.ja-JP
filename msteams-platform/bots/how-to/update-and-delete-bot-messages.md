---
title: ボットから送信されたメッセージを更新および削除する
author: WashingtonKayaker
description: Microsoft Teams ボットから送信されたメッセージを更新および削除する方法
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 04a17914efd40173d761537773613b93563999aa
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596204"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>ボットから送信されたメッセージを更新および削除する

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="update-messages"></a>メッセージを更新する

ボットは、送信後にメッセージを動的に更新できます。 ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオで、動的メッセージ更新を使用できます。

新しいメッセージは、型の元のメッセージと一致する必要があります。 たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージには単純なテキスト メッセージを指定できます。

# <a name="c"></a>[C#](#tab/dotnet)

既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをクラス `Activity` の `UpdateActivityAsync` メソッドに渡 `TurnContext` します。 [「TurnContextClass」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをオブジェクトの `Activity` `updateActivity` メソッドに渡 `TurnContext` します。 updateActivity [を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをクラス `Activity` の `update_activity` メソッドに渡 `TurnContext` します。 [「TurnContextClass」を参照してください](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[REST API](#tab/rest)

>[!NOTE]
>任意の Web プログラミング テクノロジで Teams アプリを開発し、ボット コネクタ サービス [REST API を直接呼び出します](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。 これを行うには、API 要求で [認証](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) セキュリティ手順を実装する必要があります。

会話内の既存のアクティビティを更新するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。 このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|要求 |応答 |
|----|----|
|[Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)オブジェクト |[ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)オブジェクト  |

---

## <a name="update-cards"></a>カードの更新

ボタン選択時に既存のカードを更新するには、受信アクティビティ `ReplyToId` を使用できます。

# <a name="c"></a>[C#](#tab/dotnet)

ボタンクリックで既存のカードを更新するには、更新されたカードとアクティビティ ID を持つ新しいオブジェクトをクラスのメソッド `Activity` `ReplyToId` `UpdateActivityAsync` に渡 `TurnContext` します。 [「TurnContextClass」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。
```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)


ボタンクリックで既存のカードを更新するには、更新されたカードとアクティビティ ID を持つ新しいオブジェクトをオブジェクトのメソッド `Activity` `replyToId` `updateActivity` に渡 `TurnContext` します。 updateActivity [を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。
```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

ボタンクリックで既存のカードを更新するには、更新されたカードとアクティビティ ID を持つ新しいオブジェクトをクラスのメソッド `Activity` `reply_to_id` `update_activity` に渡 `TurnContext` します。 [「TurnContextClass」を参照してください](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)

```

# <a name="rest-api"></a>[REST API](#tab/rest)

会話内の既存のアクティビティを更新するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。 このシナリオを完了するには、元の通話後に返されたアクティビティ ID をキャッシュする必要があります。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|要求 |応答 |
|----|----|
| [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)オブジェクト。 | [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)オブジェクト。 |

---

## <a name="delete-messages"></a>メッセージを削除する

ボット フレームワークでは、すべてのメッセージに固有のアクティビティ識別子があります。
次に示すように、ボット フレームワークのメソッドを使用 `DeleteActivity` してメッセージを削除できます。

# <a name="c"></a>[C#](#tab/dotnet)

そのメッセージを削除するには、そのアクティビティの ID をクラス `DeleteActivityAsync` のメソッドに渡 `TurnContext` します。 [「TurnContext.DeleteActivityAsync メソッド」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

そのメッセージを削除するには、そのアクティビティの ID をオブジェクトの `deleteActivity` メソッドに渡 `TurnContext` します。 [「deleteActivity」を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)。

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

そのメッセージを削除するには、そのアクティビティの ID をオブジェクトの `delete_activity` メソッドに渡 `TurnContext` します。 [「activity-update-and-delete」を参照してください](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

会話内の既存のアクティビティを削除するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

|要求 |応答 |
|----|----|
| 該当なし | 操作の結果を示す HTTP 状態コード。 応答の本文には何も指定されていません。 |

---

## <a name="code-samples"></a>コード サンプル

公式の会話の基本は次のとおりです。

| サンプルの名前           | 説明                                                                      | .NET    | Node.js   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Teams での会話の基本  | メッセージの更新や削除など、Teams での会話の基本を示します。|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
