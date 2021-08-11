---
title: ボットから送信されたメッセージを更新および削除する
author: WashingtonKayaker
description: ボットから送信されたメッセージを更新およびMicrosoft Teamsする方法
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 8f1738894aa5580f62b91fa44edf06d54fcc99f7786bae33ffc8cc7b95669fcc
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706093"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>ボットから送信されたメッセージを更新および削除する

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

ボットは、メッセージをデータの静的スナップショットとしてではなく、送信後に動的に更新できます。 ボット フレームワークのメソッドを使用してメッセージを削除 `DeleteActivity` することもできます。

## <a name="update-messages"></a>メッセージを更新する

ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更など、シナリオに対して動的なメッセージ更新を使用できます。

新しいメッセージが元の種類と一致する必要はありません。 たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージには単純なテキスト メッセージを指定できます。

# <a name="c"></a>[C#](#tab/dotnet)

既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをクラス `Activity` の `UpdateActivityAsync` メソッドに渡 `TurnContext` します。 詳細については [、「TurnContextClass」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

既存のメッセージを更新するには、既存のアクティビティ ID を持つ新しいオブジェクトをオブジェクトの `Activity` `updateActivity` メソッドに渡 `TurnContext` します。 詳細については [、「updateActivity 」を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。

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

> [!NOTE]

> Web プログラミング テクノロジTeamsアプリを開発し、ボット コネクタ サービス REST [API を直接呼び出します](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。 これを行うには、API 要求で [認証](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) セキュリティ手順を実装する必要があります。

会話内の既存のアクティビティを更新するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。 このシナリオを完了するには、元の通話後に返されたアクティビティ ID をキャッシュする必要があります。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|要求 |応答 |
|----|----|
| [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)オブジェクト。 | [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)オブジェクト。 |

---
* * *

メッセージが更新されたので、受信アクティビティのボタン選択の既存のカードを更新します。

## <a name="update-cards"></a>カードの更新

ボタン選択時に既存のカードを更新するには、受信アクティビティ `ReplyToId` を使用できます。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

ボタン選択の既存のカードを更新するには、更新されたカードとアクティビティ ID を持つ新しいオブジェクトをクラスのメソッド `Activity` `ReplyToId` `UpdateActivityAsync` に渡 `TurnContext` します。 [「TurnContextClass」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

ボタン選択の既存のカードを更新するには、新しいオブジェクトに更新されたカードとアクティビティ ID をオブジェクトのメソッド `Activity` `replyToId` `updateActivity` に渡 `TurnContext` します。 updateActivity [を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。

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

> [!NOTE]
> 任意の web プログラミング Teamsアプリを開発し、ボット コネクタ サービス[REST API を直接呼び出します](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。 これを行うには、API 要求 [で認証](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) セキュリティ手順を実装する必要があります。

会話内の既存のアクティビティを更新するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。 このシナリオを完了するには、元の通話後に返されたアクティビティ ID をキャッシュする必要があります。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|要求 |応答 |
|----|----|
| アクティビティ [オブジェクト](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) 。 | [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)オブジェクト。 |

* * *

カードを更新したので、ボット フレームワークを使用してメッセージを削除できます。

## <a name="delete-messages"></a>メッセージを削除する

ボット フレームワークでは、すべてのメッセージに固有のアクティビティ識別子があります。 メッセージは、ボット フレームワークのメソッドを使用して削除 `DeleteActivity` できます。

# <a name="c"></a>[C#](#tab/dotnet)

メッセージを削除するには、そのアクティビティの ID をクラスの `DeleteActivityAsync` メソッドに渡 `TurnContext` します。 詳細については [、「TurnContext.DeleteActivityAsync メソッド」を参照してください](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

メッセージを削除するには、そのアクティビティの ID をオブジェクトの `deleteActivity` メソッドに渡 `TurnContext` します。 詳細については [、「deleteActivity」を参照してください](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)。

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

そのメッセージを削除するには、そのアクティビティの ID をオブジェクトの `delete_activity` メソッドに渡 `TurnContext` します。 詳細については [、「activity-update-and-delete」を参照してください](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

会話内の既存のアクティビティを削除するには、要求エンドポイントに含 `conversationId` `activityId` める必要があります。

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **要求と応答** | **説明** |
|----|----|
| 該当なし | 操作の結果を示す HTTP 状態コード。 応答の本文には何も指定されていません。 |

---

## <a name="code-sample"></a>コード サンプル

次のコード サンプルは、会話の基本を示しています。

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Teams での会話の基本  | メッセージの更新と削除を含むTeamsの基本を示します。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [コンテキストTeams取得](~/bots/how-to/get-teams-context.md)
