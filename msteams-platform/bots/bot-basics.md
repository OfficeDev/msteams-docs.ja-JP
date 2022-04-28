---
title: ボットのアクティビティ ハンドラー
author: surbhigupta
description: Teamsのボット アクティビティ ハンドラーについて理解します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: アクティビティ ハンドラー フレームワーク のボット カード同意チャネル イベント
ms.openlocfilehash: 34dd5e8042b71f4e7cc78df7e7c543c86a53f58e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104036"
---
# <a name="bot-activity-handlers"></a>ボットのアクティビティ ハンドラー

このドキュメントは、Bot Framework のコア ドキュメントでの [ボットのしくみ](https://aka.ms/how-bots-work) に関する記事に基 [づいています](https://aka.ms/azure-bot-service-docs)。 Microsoft Teams用に開発されたボットとコア Bot Framework の主な違いは、Teamsで提供される機能にあります。

ボットの会話ロジックを整理するために、アクティビティ ハンドラーが使用されます。 アクティビティは、Teams アクティビティ ハンドラーとボット ロジックを使用して 2 つの方法で処理されます。 Teams アクティビティ ハンドラーは、Microsoft Teams固有のイベントと対話のサポートを追加します。 ボット オブジェクトには、ターンの会話の推論またはロジックが含まれ、ターン ハンドラーが公開されます。これは、ボット アダプターからの受信アクティビティを受け入れることができるメソッドです。

## <a name="teams-activity-handlers"></a>Teams アクティビティ ハンドラー

Teamsアクティビティ ハンドラーは、Microsoft Bot Frameworkのアクティビティ ハンドラーから派生します。 すべてのTeams アクティビティをルーティングしてから、Teams以外の特定のアクティビティを処理できるようにします。

Teamsのボットがアクティビティを受信すると、アクティビティ ハンドラーにルーティングされます。 すべてのアクティビティは、ターン ハンドラーと呼ばれる 1 つのベース ハンドラーを介してルーティングされます。 ターン ハンドラーは、受信したアクティビティを管理するために必要なアクティビティ ハンドラーを呼び出します。 Teams ボットは、Bot Framework `ActivityHandler` のクラスから`TeamsActivityHandler`派生したクラスから派生します。

# <a name="c"></a>[C#](#tab/csharp)

ボットは Bot Framework を使用して作成されます。 ボットがメッセージ アクティビティを受信した場合、ターン ハンドラーはその受信アクティビティの通知を受け取ります。 その後、ターン ハンドラーは受信アクティビティをアクティビティ ハンドラーに `OnMessageActivityAsync` 送信します。 Teamsでは、この機能は変わりません。 ボットが会話更新アクティビティを受信した場合、ターン ハンドラーはその受信アクティビティの通知を受け取り、受信アクティビティ `OnConversationUpdateActivityAsync`を . Teams アクティビティ ハンドラーは、最初に特定のイベントTeamsチェックします。 イベントが見つからない場合は、それらを Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つのプライマリ Teams アクティビティ ハンドラーと `OnInvokeActivityAsync`. `OnConversationUpdateActivityAsync` `OnConversationUpdateActivityAsync`は、すべての会話更新アクティビティをルーティングし、すべてのアクティビティを呼び`OnInvokeActivityAsync`出Teamsルーティングします。

特定のアクティビティ ハンドラー Teamsロジックを実装するには、ボット[ロジック](#bot-logic)セクションに示すように、ボット内のメソッドをオーバーライドする必要があります。 これらのハンドラーの基本実装がないため、オーバーライドに必要なロジックを追加する必要があります。

Teams アクティビティ ハンドラーのコード スニペット:

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

ボットは Bot Framework を使用して作成されます。 ボットがメッセージ アクティビティを受信した場合、ターン ハンドラーはその受信アクティビティの通知を受け取ります。 その後、ターン ハンドラーは受信アクティビティをアクティビティ ハンドラーに `onMessage` 送信します。 Teamsでは、この機能は変わりません。 ボットが会話更新アクティビティを受信した場合、ターン ハンドラーはその受信アクティビティの通知を受け取り、受信アクティビティ `dispatchConversationUpdateActivity`を . Teams アクティビティ ハンドラーは、最初に特定のイベントTeamsチェックします。 イベントが見つからない場合は、それらを Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つのプライマリ Teams アクティビティ ハンドラーと `onInvokeActivity`. `dispatchConversationUpdateActivity` `dispatchConversationUpdateActivity`は、すべての会話更新アクティビティをルーティングし、すべてのアクティビティを呼び`onInvokeActivity`出Teamsルーティングします。

特定のアクティビティ ハンドラー Teamsロジックを実装するには、ボット[ロジック](#bot-logic)セクションに示すように、ボット内のメソッドをオーバーライドする必要があります。 これらのハンドラーのボット ロジックを定義し、最後に必ず呼び出 `next()` してください。 呼び出すことで `next()` 、次のハンドラーが確実に実行されるようにします。

Teams アクティビティ ハンドラーのコード スニペット:

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

ボットは Bot Framework を使用して作成されます。 ボットがメッセージ アクティビティを受信した場合、ターン ハンドラーはその受信アクティビティの通知を受け取ります。 その後、ターン ハンドラーは受信アクティビティをアクティビティ ハンドラーに `on_message_activity` 送信します。 Teamsでは、この機能は変わりません。 ボットが会話更新アクティビティを受信した場合、ターン ハンドラーはその受信アクティビティの通知を受け取り、受信アクティビティ `on_conversation_update_activity`を . Teams アクティビティ ハンドラーは、最初に特定のイベントTeamsチェックします。 イベントが見つからない場合は、それらを Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つのプライマリ Teams アクティビティ ハンドラーと `on_invoke_activity`. `on_conversation_update_activity` `on_conversation_update_activity`は、すべての会話更新アクティビティをルーティングし、すべてのアクティビティを呼び`on_invoke_activity`出Teamsルーティングします。

特定のアクティビティ ハンドラー Teamsロジックを実装するには、ボット[ロジック](#bot-logic)セクションに示すように、ボット内のメソッドをオーバーライドする必要があります。 これらのハンドラーの基本実装がないため、オーバーライドに必要なロジックを追加する必要があります。

---

## <a name="bot-logic"></a>ボット ロジック

ボット ロジックは、1 つ以上のボット チャネルからの受信アクティビティを処理し、応答で送信アクティビティを生成します。 これは、最初にTeamsアクティビティをチェックするTeams アクティビティ ハンドラー クラスから派生したボットにも当てはまります。 Teamsアクティビティを確認すると、他のすべてのアクティビティが Bot Framework のアクティビティ ハンドラーに渡されます。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Core Bot Framework ハンドラー

>[!NOTE]
>
>* **追加** および **削除** されたメンバーのアクティビティを除き、このセクションで説明するすべてのアクティビティ ハンドラーは、Teams以外のボットと同様に動作し続けます。
>* `onInstallationUpdateActivityAsync()`メソッドは、ボットをTeamsに追加するときにロケールTeams取得するために使用されます。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストで異なります。

定義されているハンドラーの一覧を次に示します。`ActivityHandler`

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `OnTurnAsync` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| 受信したメッセージ アクティビティ | `OnMessageActivityAsync` | このメソッドは、アクティビティを処理 `Message` するためにオーバーライドできます。 |
| 受信した会話更新アクティビティ | `OnConversationUpdateActivityAsync` | このメソッドは、ボット以外のメンバーがアクティビティに参加または会話を離れた場合にハンドラーを `ConversationUpdate` 呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `OnMembersAddedAsync` | このメソッドは、会話に参加するメンバーを処理するためにオーバーライドできます。 |
| ボット以外のメンバーが会話を離れた | `OnMembersRemovedAsync` | このメソッドは、会話を離れるメンバーを処理するためにオーバーライドできます。 |
| 受信したイベント アクティビティ | `OnEventActivityAsync` | このメソッドは、イベントの種類に固有のハンドラーをアクティビティで `Event` 呼び出します。 |
| 受信したトークン応答イベント アクティビティ | `OnTokenResponseEventAsync` | このメソッドは、トークン応答イベントを処理するためにオーバーライドできます。 |
| 受信した非トークン応答イベント アクティビティ | `OnEventAsync` | このメソッドは、他の種類のイベントを処理するためにオーバーライドできます。 |
| 受信したその他のアクティビティの種類 | `OnUnrecognizedActivityTypeAsync` | このメソッドは、それ以外の場合はハンドルされないアクティビティの種類を処理するためにオーバーライドできます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams特定のアクティビティ ハンドラー

コア `TeamsActivityHandler` Bot Framework ハンドラー セクションのハンドラーの一覧を拡張して、次を含めます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | このメソッドは、作成中のTeams チャネルを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[作成されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)に関する記事を参照してください。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | このメソッドは、削除されるTeams チャネルを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)に関する記事を参照してください。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | このメソッドは、名前を変更するTeams チャネルを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[名前が変更されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)に関する記事を参照してください。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`このメソッドをオーバーライドして、名前を変更するTeams チームを処理できます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[名前が変更されたチーム](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)を参照してください。|
| MembersAdded | `OnTeamsMembersAddedAsync` | このメソッドは 、`OnMembersAddedAsync``ActivityHandler`. このメソッドは、チームに参加するメンバーを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)に[追加されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)に関する記事を参照してください。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | このメソッドは 、`OnMembersRemovedAsync``ActivityHandler`. このメソッドは、チームから離れるメンバーを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[削除されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)に関する記事を参照してください。|

#### <a name="teams-invoke-activities"></a>アクティビティを呼び出すTeams

Teams アクティビティ ハンドラーから呼び出されるTeamsアクティビティ ハンドラーの`OnInvokeActivityAsync`一覧を次に示します。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | このメソッドは、カード アクションの呼び出しアクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | このメソッドは、ユーザーがファイルの同意カードを受け入れたときに呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | このメソッドは、ファイルの同意カード アクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | このメソッドは、ファイルの同意カードがユーザーによって拒否されたときに呼び出されます。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | このメソッドは、Office 365 コネクタ カードアクション アクティビティがコネクタから受信されたときに呼び出されます。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | このメソッドは、signIn によって状態アクティビティがコネクタから受信されたことを確認するときに呼び出されます。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | このメソッドは、派生クラスでオーバーライドして、タスク モジュールがフェッチされたときにロジックを提供できます。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | このメソッドは、派生クラスでオーバーライドして、タスク モジュールの送信時にロジックを提供できます。 |

このセクションに示す呼び出しアクティビティは、Teamsの会話型ボット用です。 Bot Framework SDK では、メッセージ拡張機能に固有の呼び出しアクティビティもサポートされています。 詳細については、 [メッセージ拡張機能の概要](https://aka.ms/azure-bot-what-are-messaging-extensions)を参照してください。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Core Bot Framework ハンドラー

>[!NOTE]
> **追加** および **削除** されたメンバーのアクティビティを除き、このセクションで説明するすべてのアクティビティ ハンドラーは、Teams以外のボットと同様に動作し続けます。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストで異なります。

定義されているハンドラーの一覧を次に示します。`ActivityHandler`

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `onTurn` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| 受信したメッセージ アクティビティ | `onMessage` | このメソッドは、アクティビティを処理 `Message` するのに役立ちます。 |
| 受信した会話更新アクティビティ | `onConversationUpdate` | このメソッドは、ボット以外のメンバーがアクティビティに参加または会話を離れた場合にハンドラーを `ConversationUpdate` 呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `onMembersAdded` | このメソッドは、会話に参加するメンバーを処理するのに役立ちます。 |
| ボット以外のメンバーが会話を離れた | `onMembersRemoved` | このメソッドは、会話を離れるメンバーを処理するのに役立ちます。 |
| 受信したイベント アクティビティ | `onEvent` | このメソッドは、イベントの種類に固有のハンドラーをアクティビティで `Event` 呼び出します。 |
| 受信したトークン応答イベント アクティビティ | `onTokenResponseEvent` | このメソッドは、トークン応答イベントを処理するのに役立ちます。 |
| 受信したその他のアクティビティの種類 | `onUnrecognizedActivityType` | このメソッドは、それ以外の場合はハンドルされないアクティビティの種類を処理するのに役立ちます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams特定のアクティビティ ハンドラー

コア `TeamsActivityHandler` Bot Framework ハンドラー セクションのハンドラーの一覧を拡張して、次を含めます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | このメソッドは、作成中のTeams チャネルを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[作成されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)に関する記事を参照してください。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | このメソッドは、削除されるTeams チャネルを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)に関する記事を参照してください。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | このメソッドは、名前を変更するTeams チャネルを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[名前が変更されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)に関する記事を参照してください。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`このメソッドをオーバーライドして、名前を変更するTeams チームを処理できます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[名前が変更されたチーム](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)を参照してください。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | このメソッドは 、`OnMembersAddedAsync``ActivityHandler`. このメソッドは、チームに参加するメンバーを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)に[追加されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)に関する記事を参照してください。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | このメソッドは 、`OnMembersRemovedAsync``ActivityHandler`. このメソッドは、チームから離れるメンバーを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[削除されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)に関する記事を参照してください。 |

#### <a name="teams-invoke-activities"></a>アクティビティを呼び出すTeams

Teams アクティビティ ハンドラーから呼び出されるTeamsアクティビティ ハンドラーの`onInvokeActivity`一覧を次に示します。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | このメソッドは、カード アクションの呼び出しアクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | このメソッドは、ユーザーがファイルの同意カードを受け入れたときに呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | このメソッドは、ファイルの同意カード アクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | このメソッドは、ファイルの同意カードがユーザーによって拒否されたときに呼び出されます。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | このメソッドは、Office 365 コネクタ カードアクション アクティビティがコネクタから受信されたときに呼び出されます。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | このメソッドは、signIn によって状態アクティビティがコネクタから受信されたことを確認するときに呼び出されます。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | このメソッドは、派生クラスでオーバーライドして、タスク モジュールがフェッチされたときにロジックを提供できます。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | このメソッドは、派生クラスでオーバーライドして、タスク モジュールの送信時にロジックを提供できます。 |

このセクションに示す呼び出しアクティビティは、Teamsの会話型ボット用です。 Bot Framework SDK では、メッセージ拡張機能に固有の呼び出しアクティビティもサポートされています。 詳細については、 [メッセージ拡張機能の概要](https://aka.ms/azure-bot-what-are-messaging-extensions)を参照してください。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Core Bot Framework ハンドラー

>[!NOTE]
> **追加** および **削除** されたメンバーのアクティビティを除き、このセクションで説明するすべてのアクティビティ ハンドラーは、Teams以外のボットと同様に動作し続けます。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストで異なります。

定義されているハンドラーの一覧を次に示します。`ActivityHandler`

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `on_turn` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| 受信したメッセージ アクティビティ | `on_message_activity` | このメソッドは、アクティビティを処理 `Message` するためにオーバーライドできます。 |
| 受信した会話更新アクティビティ | `on_conversation_update_activity` | このメソッドは、ボット以外のメンバーが会話に参加または離れる場合にハンドラーを呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `on_members_added_activity` | このメソッドは、会話に参加するメンバーを処理するためにオーバーライドできます。 |
| ボット以外のメンバーが会話を離れた | `on_members_removed_activity` | このメソッドは、会話を離れるメンバーを処理するためにオーバーライドできます。 |
| 受信したイベント アクティビティ | `on_event_activity` | このメソッドは、イベントの種類に固有のハンドラーを呼び出します。 |
| 受信したトークン応答イベント アクティビティ | `on_token_response_event` | このメソッドは、トークン応答イベントを処理するためにオーバーライドできます。 |
| 受信した非トークン応答イベント アクティビティ | `on_event` | このメソッドは、他の種類のイベントを処理するためにオーバーライドできます。 |
| 受信したその他のアクティビティの種類 | `on_unrecognized_activity_type` | このメソッドは、処理されない任意の種類のアクティビティを処理するためにオーバーライドできます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams特定のアクティビティ ハンドラー

コア `TeamsActivityHandler` Bot Framework ハンドラー セクションからハンドラーの一覧が拡張され、次のものが含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | このメソッドは、作成中のTeams チャネルを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[作成されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)に関する記事を参照してください。 |
| channelDeleted | `on_teams_channel_deleted` | このメソッドは、削除されるTeams チャネルを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)に関する記事を参照してください。|
| channelRenamed | `on_teams_channel_renamed` | このメソッドは、名前を変更するTeams チャネルを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[名前が変更されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)に関する記事を参照してください。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;`このメソッドをオーバーライドして、名前を変更するTeams チームを処理できます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[名前が変更されたチーム](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)を参照してください。|
| MembersAdded | `on_teams_members_added` | このメソッドは 、`OnMembersAddedAsync``ActivityHandler`. このメソッドは、チームに参加するメンバーを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)に[追加されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)に関する記事を参照してください。|
| MembersRemoved | `on_teams_members_removed` | このメソッドは 、`OnMembersRemovedAsync``ActivityHandler`. このメソッドは、チームから離れるメンバーを処理するためにオーバーライドできます。 詳細については、[会話更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[削除されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)に関する記事を参照してください。|

#### <a name="teams-invoke-activities"></a>アクティビティを呼び出すTeams

Teams アクティビティ ハンドラーから呼び出されるTeamsアクティビティ ハンドラーの`on_invoke_activity`一覧を次に示します。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | このメソッドは、カード アクションの呼び出しアクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | このメソッドは、ユーザーがファイルの同意カードを受け入れたときに呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent`            | このメソッドは、ファイルの同意カード アクティビティがコネクタから受信されたときに呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | このメソッドは、ファイルの同意カードがユーザーによって拒否されたときに呼び出されます。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | このメソッドは、Office 365 コネクタ カードアクション アクティビティがコネクタから受信されたときに呼び出されます。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | このメソッドは、signIn によって状態アクティビティがコネクタから受信されたことを確認するときに呼び出されます。 |
| task/fetch                      | `on_teams_task_module_fetch`        | このメソッドは、派生クラスでオーバーライドして、タスク モジュールがフェッチされたときにロジックを提供できます。 |
| task/submit                     | `on_teams_task_module_submit`       | このメソッドは、派生クラスでオーバーライドして、タスク モジュールの送信時にロジックを提供できます。 |

このセクションに示す呼び出しアクティビティは、Teamsの会話型ボット用です。 Bot Framework SDK では、メッセージ拡張機能に固有の呼び出しアクティビティもサポートされています。 詳細については、 [メッセージ拡張機能の概要](https://aka.ms/azure-bot-what-are-messaging-extensions)を参照してください。

---

---

ボット アクティビティ ハンドラーについて理解したので、会話と、ボットが受信または送信するメッセージに応じて、ボットの動作が異なる方法を見てみましょう。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会話の基本](~/bots/how-to/conversations/conversation-basics.md)
