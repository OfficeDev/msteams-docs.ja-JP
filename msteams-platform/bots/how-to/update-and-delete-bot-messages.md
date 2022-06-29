---
title: ボットから送信されたメッセージを更新および削除する
author: WashingtonKayaker
description: さまざまな環境で、およびコード サンプルを使用して REST API を使用して、Microsoft Teams ボットから送信されたメッセージを更新および削除する方法について説明します。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: bd52a3cfa27153c4349d50f4263dc29346fdfb45
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503803"
---
# <a name="update-and-delete-messages-sent-from-bot"></a>ボットから送信されたメッセージを更新および削除する 

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

ボットは、メッセージをデータの静的スナップショットとして保持する代わりに、メッセージを送信した後に動的に更新できます。 メッセージは、Bot Framework の `DeleteActivity` メソッドを使用して削除することもできます。

## <a name="update-messages"></a>メッセージを更新する

ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオでは、動的メッセージ更新を使用できます。

新しいメッセージが元の種類と一致する必要はありません。 たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージは単純なテキスト メッセージにすることができます。

# <a name="c"></a>[C#](#tab/dotnet)

既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しい `Activity` オブジェクトを `TurnContext` クラスの `UpdateActivityAsync` メソッドに渡します。 詳細については、[TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true) を参照してください。

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しい `Activity` オブジェクトを `TurnContext` オブジェクトの `updateActivity` メソッドに渡します。 詳細については、[updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)を参照してください。

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しい `Activity` オブジェクトを `TurnContext` クラスの `update_activity` メソッドに渡します。 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true) を参照してください。

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]
> 任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。 これを行うには、API 要求で [[認証]](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) セキュリティ手順を実装する必要があります。

会話内の既存のアクティビティを更新するには、リクエスト エンドポイントに `conversationId` と `activityId` を含めます。 このシナリオを完了するには、元の POST 呼び出しによって返されたアクティビティ ID をキャッシュする必要があります。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|要求 |応答 |
|----|----|
| [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) オブジェクト。 | [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) オブジェクト。 |

---
---

メッセージを更新したので、受信アクティビティのボタン選択時に既存のカードを更新します。

## <a name="update-cards"></a>カードを更新する

ボタン選択時に既存のカードを更新するには、着信アクティビティの `ReplyToId`を使用できます。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

ボタン選択で既存のカードを更新するには、更新されたカードとアクティビティ ID として `ReplyToId` を含む新しい `Activity` オブジェクトを `TurnContext` クラスの `UpdateActivityAsync` メソッドに渡します。 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true) を参照してください。

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

ボタン選択で既存のカードを更新するには、更新されたカードとアクティビティ ID として `replyToId` を含む新しい `Activity` オブジェクトを `TurnContext` オブジェクトの `updateActivity` メソッドに渡します。 [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true) に関する記事を参照してください。

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

ボタン クリックで既存のカードを更新するには、更新されたカードとアクティビティ ID として `reply_to_id` を含む新しい `Activity` オブジェクトを `TurnContext` クラスの `update_activity` メソッドに渡します。 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true) を参照してください。

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]
> 任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。 これを行うには、API 要求で [[認証]](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) セキュリティ手順を実装する必要があります。

会話内の既存のアクティビティを更新するには、リクエスト エンドポイントに `conversationId` と `activityId` を含めます。 このシナリオを完了するには、元の POST 呼び出しによって返されたアクティビティ ID をキャッシュする必要があります。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|要求 |応答 |
|----|----|
| [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) オブジェクト。 | [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) オブジェクト。 |

---

カードを更新したので、Bot Framework を使用してメッセージを削除できます。

## <a name="delete-messages"></a>メッセージを削除する

Bot Framework では、すべてのメッセージに一意のアクティビティ識別子があります。 メッセージは、Bot Framework の `DeleteActivity` メソッドを使用して削除できます。

# <a name="c"></a>[C#](#tab/dotnet)

メッセージを削除するには、そのアクティビティの ID を `TurnContext` クラスの `DeleteActivityAsync` メソッドに渡します。 詳細については、「[TurnContext.DeleteActivityAsync メソッド](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)」を参照してください。

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

メッセージを削除するには、そのアクティビティの ID を `TurnContext` オブジェクトの `deleteActivity` メソッドに渡します。 詳細については、[deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)を参照してください。

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

そのメッセージを削除するには、そのアクティビティの ID を `TurnContext` オブジェクトの `delete_activity` メソッドに渡します。 詳細については、[activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py) を参照してください。

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

会話内の既存のアクティビティを削除するには、リクエスト エンドポイントに `conversationId` と `activityId` を含めます。

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **要求および応答** | **[説明]** |
|----|----|
| 該当なし | 操作の結果を示す HTTP 状態コード。 応答の本文には何も指定されません。 |

---

## <a name="code-sample"></a>コード サンプル

次のコード サンプルは、会話の基本を示しています。

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Teams での会話の基本  | メッセージの更新や削除など、Teams での会話の基本を示します。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Teams のコンテキストを取得する](~/bots/how-to/get-teams-context.md)
