---
title: ボットのアクティビティ ハンドラー
author: surbhigupta
description: メッセージ、チャネル、チーム、メンバー、メンション、認証、Microsoft Bot Framework SDK を使用したカード アクションの Microsoft Teams イベントとアクティビティ ハンドラーについて説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 4780c4c2ca3965186411f7927f1fb5b555647004
ms.sourcegitcommit: b918181217995a47be34632e1051d0f4d4d481b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2022
ms.locfileid: "67321209"
---
# <a name="bot-activity-handlers"></a>ボットのアクティビティ ハンドラー

このドキュメントは、主要な [Bot Framework のドキュメント](https://aka.ms/azure-bot-service-docs)の「[ボットのしくみ](https://aka.ms/how-bots-work)」に基づいています。 Microsoft Teams 用に開発されたボットと主要な Bot Framework の主な違いは、Teams で提供される機能にあります。

ボットの会話ロジックを整理するために、アクティビティ ハンドラーが使用されます。 アクティビティは、Teams アクティビティ ハンドラーとボット ロジックを使用して 2 つの方法で処理されます。 Teams アクティビティ ハンドラーは、Teams 固有のイベントと対話のサポートを追加します。 ボット オブジェクトには、会話の推論またはターンのロジックが含まれ、ターン ハンドラーを公開します。これは、ボット アダプターからの受信アクティビティを承諾できるメソッドです。

## <a name="teams-activity-handlers"></a>Teams のアクティビティ ハンドラー

Teams のアクティビティ ハンドラーは、Microsoft Bot Framework のアクティビティ ハンドラーから派生したものです。 すべての Teams アクティビティをルーティングしてから、Teams 以外の特定のアクティビティを処理できるようにします。

Teams のボットがアクティビティを受信すると、アクティビティ ハンドラーにルーティングされます。 すべてのアクティビティは、ターン ハンドラーと呼ばれる 1 つのベース ハンドラーを経由してルーティングされます。 ターン ハンドラーは、受信したアクティビティを管理するために必要なアクティビティ ハンドラーを呼び出します。 Teams ボットは、Bot Framework の `ActivityHandler` クラスから派生した `TeamsActivityHandler` クラスから派生したものです。

> [!NOTE]
> ボットアクティビティの処理に 15 秒以上かかる場合、Teams はボット エンドポイントに再試行要求を送信します。 そのため、ボットに重複する要求が表示されます。

# <a name="c"></a>[C#](#tab/csharp)

ボットは Bot Framework を使用して作成されます。 ボットがメッセージ アクティビティを受信した場合、ターン ハンドラーは受信したアクティビティの通知を受け取ります。 その後、ターン ハンドラーは受信したアクティビティを `OnMessageActivityAsync` アクティビティ ハンドラーに送信します。 Teams では、この機能は変わりません。 ボットが会話更新アクティビティを受信した場合、ターン ハンドラーは受信したアクティビティの通知を受け取り、受信したアクティビティを `OnConversationUpdateActivityAsync` に送信します。 Teams アクティビティ ハンドラーは、最初に特定の Teams イベントがないかチェックします。 イベントが見つからなかった場合、それらを Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、主に `OnConversationUpdateActivityAsync` と `OnInvokeActivityAsync` の 2 つの Teams アクティビティ ハンドラーがあります。 `OnConversationUpdateActivityAsync` はすべての会話更新アクティビティをルーティングし、`OnInvokeActivityAsync` は Teams によって呼び出されたすべてのアクティビティをルーティングします。

特定の Teams のアクティビティ ハンドラーのロジックを実装するには、「[ボット ロジック](#bot-logic)」セクションに示すように、ボット内のメソッドをオーバーライドする必要があります。 これらのハンドラーの基本実装はありません。 そのため、オーバーライドに必要なロジックを追加します。

Teams のアクティビティ ハンドラーのコード スニペット:

`OnTeamsChannelCreatedAsync`

```csharp

protected override Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelDeletedAsync`

```csharp

protected override Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelRenamedAsync`

```csharp

protected override Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsTeamRenamedAsync`

```csharp

protected override Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsMembersAddedAsync`

```csharp

protected override Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsMembersRemovedAsync`

```csharp

protected override Task OnTeamsMembersRemovedAsync(IList<TeamsChannelAccount> teamsMembersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken);
  {
   // Code logic here
  }
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

ボットは Bot Framework を使用して作成されます。 ボットがメッセージ アクティビティを受信した場合、ターン ハンドラーは受信したアクティビティの通知を受け取ります。 その後、ターン ハンドラーは受信したアクティビティを `onMessage` アクティビティ ハンドラーに送信します。 Teams では、この機能は変わりません。 ボットが会話更新アクティビティを受信した場合、ターン ハンドラーは受信したアクティビティの通知を受け取り、受信したアクティビティを `dispatchConversationUpdateActivity` に送信します。 Teams アクティビティ ハンドラーは、最初に特定の Teams イベントがないかチェックします。 イベントが見つからなかった場合、それらを Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、主に `dispatchConversationUpdateActivity` と `onInvokeActivity` の 2 つの Teams アクティビティ ハンドラーがあります。 `dispatchConversationUpdateActivity` はすべての会話更新アクティビティをルーティングし、`onInvokeActivity` は Teams によって呼び出されたすべてのアクティビティをルーティングします。

特定の Teams のアクティビティ ハンドラーのロジックを実装するには、「[ボット ロジック](#bot-logic)」セクションに示すように、ボット内のメソッドをオーバーライドする必要があります。 これらのハンドラーのボット ロジックを定義し、最後に必ず `next()` を呼び出してください。 呼び出すと `next()`、次のハンドラーが確実に実行されます。

Teams のアクティビティ ハンドラーのコード スニペット:

`OnTeamsChannelCreatedAsync`

```javascript

onTeamsChannelCreated(async (channelInfo, teamInfo, context, next) => {
       // code for handling
        await next()
    });
```

`OnTeamsChannelDeletedAsync`

```javascript

onTeamsChannelDeleted(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsChannelRenamedAsync`

```javascript

onTeamsChannelRenamed(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsTeamRenamedAsync`

```javascript

onTeamsTeamRenamedAsync(async (teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsMembersAddedAsync`

```javascript

onTeamsMembersAdded(async (membersAdded, teamInfo, context, next) => {
       // code for handling
    await next();
    });
```

`OnTeamsMembersRemovedAsync`

```javascript

onTeamsMembersRemoved(async (membersRemoved, teamInfo, context, next) => {
       // code for handling
    await next();
    });
```

# <a name="python"></a>[Python](#tab/python)

ボットは Bot Framework を使用して作成されます。 ボットがメッセージ アクティビティを受信した場合、ターン ハンドラーは受信したアクティビティの通知を受け取ります。 その後、ターン ハンドラーは受信したアクティビティを `on_message_activity` アクティビティ ハンドラーに送信します。 Teams では、この機能は変わりません。 ボットが会話更新アクティビティを受信した場合、ターン ハンドラーは受信したアクティビティの通知を受け取り、受信したアクティビティを `on_conversation_update_activity` に送信します。 Teams アクティビティ ハンドラーは、最初に特定の Teams イベントがないかチェックします。 イベントが見つからなかった場合、それらを Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、主に `on_conversation_update_activity` と `on_invoke_activity` の 2 つの Teams アクティビティ ハンドラーがあります。 `on_conversation_update_activity` はすべての会話更新アクティビティをルーティングし、`on_invoke_activity` は Teams によって呼び出されたすべてのアクティビティをルーティングします。

特定の Teams のアクティビティ ハンドラーのロジックを実装するには、「[ボット ロジック](#bot-logic)」セクションに示すように、ボット内のメソッドをオーバーライドする必要があります。 これらのハンドラーの基本実装はありません。 そのため、オーバーライドに必要なロジックを追加します。

---

## <a name="bot-logic"></a>ボット ロジック

ボット ロジックは、1 つ以上のボット チャネルから受信したアクティビティを処理し、それに応じて送信アクティビティを生成します。 Teams アクティビティ ハンドラー クラスから派生したボットは、最初に Teams アクティビティをチェックします。 Teams アクティビティがないか確認したら、他のすべてのアクティビティが Bot Framework のアクティビティ ハンドラーに渡されます。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>主要な Bot Framework ハンドラー

>[!NOTE]
>
>* **追加** および **削除** されたメンバーのアクティビティを除き、このセクションで説明するすべてのアクティビティ ハンドラーは Teams 以外のボットと同様に動作し続けます。
>* `onInstallationUpdateActivityAsync()` メソッドは、ボットを Teams に追加するときに Teams ロケールを取得するために使用されます。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストで異なります。

定義されているハンドラー `ActivityHandler` の一覧には、次のものが含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 任意のアクティビティの種類を受信しました | `OnTurnAsync` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| メッセージ アクティビティを受信しました | `OnMessageActivityAsync` | このメソッドは、`Message` アクティビティを処理するためにオーバーライドできます。 |
| 会話更新アクティビティを受信しました | `OnConversationUpdateActivityAsync` | このメソッドは、`ConversationUpdate` アクティビティで、ボット以外のメンバーが会話に参加または退出した場合にハンドラーを呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `OnMembersAddedAsync` | このメソッドは、会話に参加するメンバーを処理するためにオーバーライドできます。 |
| ボット以外のメンバーが会話を退出しました | `OnMembersRemovedAsync` | このメソッドは、会話を退出するメンバーを処理するためにオーバーライドできます。 |
| イベント アクティビティを受信しました | `OnEventActivityAsync` | このメソッドは、`Event` アクティビティで、イベントの種類に固有のハンドラーを呼び出します。 |
| トークン応答イベント アクティビティを受信しました | `OnTokenResponseEventAsync` | このメソッドは、トークン応答イベントを処理するためにオーバーライドできます。 |
| トークン応答以外のイベント アクティビティを受信しました | `OnEventAsync` | このメソッドは、他の種類のイベントを処理するためにオーバーライドできます。 |
| その他のアクティビティの種類を受信しました | `OnUnrecognizedActivityTypeAsync` | このメソッドは、それ以外の場合は処理されないアクティビティの種類を処理するためにオーバーライドできます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams に固有のアクティビティ ハンドラー

`TeamsActivityHandler` は、「主要な Bot Framework ハンドラー」セクションのハンドラーの一覧を拡張して、次が含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | このメソッドは、作成される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)」の「[チャネルの作成](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | このメソッドは、削除される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)」の「[チャネルの削除](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | このメソッドは、名前が変更される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)」の「[チャネルの名前変更](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` このメソッドは、名前が変更される Teams チームを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)」の「[チームの名前変更](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|
| MembersAdded | `OnTeamsMembersAddedAsync` | このメソッドは `ActivityHandler` の `OnMembersAddedAsync` メソッドを呼び出します。 このメソッドは、チームに参加するメンバーを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)」の「[チーム メンバーの追加](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | このメソッドは `ActivityHandler` の `OnMembersRemovedAsync` メソッドを呼び出します。 このメソッドは、チームを離れるメンバーを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)」の「[チーム メンバーの削除](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|

#### <a name="teams-invoke-activities"></a>Teams の呼び出しアクティビティ

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの一覧には、 `OnInvokeActivityAsync` 次のものが含まれます。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | このメソッドは、カード アクションの呼び出しアクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | このメソッドは、ファイルの同意カードがユーザーによって承諾されたときに呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | このメソッドは、ファイルの同意カード アクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | このメソッドは、ファイルの同意カードがユーザーによって拒否されたときに呼び出されます。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | このメソッドは、Office 365 コネクタ カードアクション アクティビティがコネクタから受信されたときに呼び出されます。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | このメソッドは、signIn 検証状態がコネクタから受信されたときに呼び出されます。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | このメソッドは、タスク モジュールがフェッチされたときにロジックを提供するために、派生クラスでオーバーライドできます。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | このメソッドは、タスク モジュールが送信されたときにロジックを提供するために、派生クラスでオーバーライドできます。 |

このセクションに記載されている Invoke アクティビティは、Teams の会話ボット用です。 Bot Framework SDK は、メッセージ拡張機能に固有の呼び出しアクティビティもサポートしています。 詳細については、「[メッセージ拡張機能とは](https://aka.ms/azure-bot-what-are-messaging-extensions)」を参照してください。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>主要な Bot Framework ハンドラー

>[!NOTE]
> **追加** および **削除** されたメンバーのアクティビティを除き、このセクションで説明するすべてのアクティビティ ハンドラーは Teams 以外のボットと同様に動作し続けます。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストで異なります。

定義されているハンドラー `ActivityHandler` の一覧には、次のものが含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 任意のアクティビティの種類を受信しました | `onTurn` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| メッセージ アクティビティを受信しました | `onMessage` | このメソッドは、`Message` アクティビティを処理するのに役立ちます。 |
| 会話更新アクティビティを受信しました | `onConversationUpdate` | このメソッドは、`ConversationUpdate` アクティビティで、ボット以外のメンバーが会話に参加または退出した場合にハンドラーを呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `onMembersAdded` | このメソッドは、会話に参加するメンバーを処理するのに役立ちます。 |
| ボット以外のメンバーが会話を退出しました | `onMembersRemoved` | このメソッドは、会話を退出するメンバーを処理するのに役立ちます。 |
| イベント アクティビティを受信しました | `onEvent` | このメソッドは、`Event` アクティビティで、イベントの種類に固有のハンドラーを呼び出します。 |
| トークン応答イベント アクティビティを受信しました | `onTokenResponseEvent` | このメソッドは、トークン応答イベントを処理するのに役立ちます。 |
| その他のアクティビティの種類を受信しました | `onUnrecognizedActivityType` | このメソッドは、それ以外の場合は処理されないアクティビティの種類を処理するのに役立ちます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams に固有のアクティビティ ハンドラー

`TeamsActivityHandler` は、「主要な Bot Framework ハンドラー」セクションのハンドラーの一覧を拡張して、次が含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | このメソッドは、作成される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)」の「[チャネルの作成](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | このメソッドは、削除される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)」の「[チャネルの削除](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | このメソッドは、名前が変更される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)」の「[チャネルの名前変更](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` このメソッドは、名前が変更される Teams チームを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)」の「[チームの名前変更](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | このメソッドは `ActivityHandler` の `OnMembersAddedAsync` メソッドを呼び出します。 このメソッドは、チームに参加するメンバーを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)」の「[チーム メンバーの追加](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | このメソッドは `ActivityHandler` の `OnMembersRemovedAsync` メソッドを呼び出します。 このメソッドは、チームを離れるメンバーを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)」の「[チーム メンバーの削除](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。 |

#### <a name="teams-invoke-activities"></a>Teams の呼び出しアクティビティ

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの一覧には、 `onInvokeActivity` 次のものが含まれます。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | このメソッドは、カード アクションの呼び出しアクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | このメソッドは、ファイルの同意カードがユーザーによって承諾されたときに呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | このメソッドは、ファイルの同意カード アクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | このメソッドは、ファイルの同意カードがユーザーによって拒否されたときに呼び出されます。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | このメソッドは、Office 365 コネクタ カードアクション アクティビティがコネクタから受信されたときに呼び出されます。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | このメソッドは、signIn 検証状態がコネクタから受信されたときに呼び出されます。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | このメソッドは、タスク モジュールがフェッチされたときにロジックを提供するために、派生クラスでオーバーライドできます。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | このメソッドは、タスク モジュールが送信されたときにロジックを提供するために、派生クラスでオーバーライドできます。 |

このセクションに示す呼び出しアクティビティは、Teams の会話型ボット用です。 Bot Framework SDK は、メッセージ拡張機能に固有の呼び出しアクティビティもサポートしています。 詳細については、「[メッセージ拡張機能とは](https://aka.ms/azure-bot-what-are-messaging-extensions)」を参照してください。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>主要な Bot Framework ハンドラー

>[!NOTE]
> **追加** および **削除** されたメンバーのアクティビティを除き、このセクションで説明するすべてのアクティビティ ハンドラーは Teams 以外のボットと同様に動作し続けます。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストで異なります。

定義されているハンドラー `ActivityHandler` の一覧には、次のものが含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 任意のアクティビティの種類を受信しました | `on_turn` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| メッセージ アクティビティを受信しました | `on_message_activity` | このメソッドは、`Message` アクティビティを処理するためにオーバーライドできます。 |
| 会話更新アクティビティを受信しました | `on_conversation_update_activity` | このメソッドは、ボット以外のメンバーが会話に参加または退出するとハンドラーを呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `on_members_added_activity` | このメソッドは、会話に参加するメンバーを処理するためにオーバーライドできます。 |
| ボット以外のメンバーが会話を退出しました | `on_members_removed_activity` | このメソッドは、会話を退出するメンバーを処理するためにオーバーライドできます。 |
| イベント アクティビティを受信しました | `on_event_activity` | このメソッドは、イベントの種類に固有のハンドラーを呼び出します。 |
| トークン応答イベント アクティビティを受信しました | `on_token_response_event` | このメソッドは、トークン応答イベントを処理するためにオーバーライドできます。 |
| トークン応答以外のイベント アクティビティを受信しました | `on_event` | このメソッドは、他の種類のイベントを処理するためにオーバーライドできます。 |
| その他のアクティビティの種類を受信しました | `on_unrecognized_activity_type` | このメソッドは、処理されない任意の種類のアクティビティを処理するためにオーバーライドできます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams に固有のアクティビティ ハンドラー

`TeamsActivityHandler` は、「主要な Bot Framework ハンドラー」セクションのハンドラーの一覧を拡張して、次が含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | このメソッドは、作成される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)」の「[チャネルの作成](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。 |
| channelDeleted | `on_teams_channel_deleted` | このメソッドは、削除される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)」の「[チャネルの削除](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|
| channelRenamed | `on_teams_channel_renamed` | このメソッドは、名前が変更される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)」の「[チャネルの名前変更](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` このメソッドは、名前が変更される Teams チームを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)」の「[チームの名前変更](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|
| MembersAdded | `on_teams_members_added` | このメソッドは `ActivityHandler` の `OnMembersAddedAsync` メソッドを呼び出します。 このメソッドは、チームに参加するメンバーを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)」の「[チーム メンバーの追加](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|
| MembersRemoved | `on_teams_members_removed` | このメソッドは `ActivityHandler` の `OnMembersRemovedAsync` メソッドを呼び出します。 このメソッドは、チームを離れるメンバーを処理するためにオーバーライドできます。 詳細については、「[会話の更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)」の「[チーム メンバーの削除](https://aka.ms/azure-bot-subscribe-to-conversation-events)」を参照してください。|

#### <a name="teams-invoke-activities"></a>Teams の呼び出しアクティビティ

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの一覧には、 `on_invoke_activity` 次のものが含まれます。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | このメソッドは、カード アクションの呼び出しアクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | このメソッドは、ファイルの同意カードがユーザーによって承諾されたときに呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent`            | このメソッドは、ファイルの同意カード アクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | このメソッドは、ファイルの同意カードがユーザーによって拒否されたときに呼び出されます。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | このメソッドは、Office 365 コネクタ カードアクション アクティビティがコネクタから受信されたときに呼び出されます。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | このメソッドは、signIn 検証状態がコネクタから受信されたときに呼び出されます。 |
| task/fetch                      | `on_teams_task_module_fetch`        | このメソッドは、タスク モジュールがフェッチされたときにロジックを提供するために、派生クラスでオーバーライドできます。 |
| task/submit                     | `on_teams_task_module_submit`       | このメソッドは、タスク モジュールが送信されたときにロジックを提供するために、派生クラスでオーバーライドできます。 |

このセクションに示す呼び出しアクティビティは、Teams の会話型ボット用です。 Bot Framework SDK は、メッセージ拡張機能に固有の呼び出しアクティビティもサポートしています。 詳細については、「[メッセージ拡張機能とは](https://aka.ms/azure-bot-what-are-messaging-extensions)」を参照してください。

---

---

ボット アクティビティ ハンドラーについて理解したので、会話と、ボットが受信または送信するメッセージに応じて、ボットの動作が異なる方法を見てみましょう。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [会話の基本](~/bots/how-to/conversations/conversation-basics.md)
