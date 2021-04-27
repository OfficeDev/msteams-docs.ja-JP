---
title: ボットのアクティビティ ハンドラー
author: clearab
description: Teams のボット アクティビティ ハンドラーについて説明します。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: da770d930ca6d00503c0102f1e683a60161636fd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020191"
---
# <a name="bot-activity-handlers"></a>ボットのアクティビティ ハンドラー

このドキュメントでは、ボットの動作に[](https://aka.ms/how-bots-work)関する記事を基に、ボット フレームワークのコア[ドキュメントを参照してください](https://aka.ms/azure-bot-service-docs)。 Microsoft Teams 用に開発されたボットとコア ボット フレームワークの主な違いは、Teams で提供される機能です。

ボットの会話ロジックを整理するには、アクティビティ ハンドラーが使用されます。 アクティビティは、Teams アクティビティ ハンドラーとボット ロジックを使用して 2 つの方法で処理されます。 Teams アクティビティ ハンドラーは、Microsoft Teams 固有のイベントと対話のサポートを追加します。 ボット オブジェクトには、ターンの会話的な理由またはロジックが含まれています。ターン ハンドラーが公開されます。これは、ボット アダプターからの受信アクティビティを受け入れ可能なメソッドです。

## <a name="teams-activity-handlers"></a>Teams アクティビティ ハンドラー

Teams アクティビティ ハンドラーは、Microsoft Bot Framework のアクティビティ ハンドラーから派生します。 Teams 以外のアクティビティの処理を許可する前に、すべての Teams アクティビティをルーティングします。

Teams のボットがアクティビティを受信すると、アクティビティ ハンドラーにルーティングされます。 すべてのアクティビティは、ターン ハンドラーと呼ばれる 1 つの基本ハンドラーを介してルーティングされます。 ターン ハンドラーは、受信したアクティビティを管理するために必要なアクティビティ ハンドラーを呼び出します。 Teams ボットは、ボット フレームワークのクラスから派生したクラス `TeamsActivityHandler` から派生 `ActivityHandler` します。

# <a name="c"></a>[C#](#tab/csharp)

ボットは、ボット フレームワークを使用して作成されます。 ボットがメッセージ アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受け取ります。 ターン ハンドラーは、受信アクティビティをアクティビティ ハンドラーに `OnMessageActivityAsync` 送信します。 Teams では、この機能は変わりません。 ボットが会話更新アクティビティを受け取った場合、ターン ハンドラーはその受信アクティビティの通知を受け取り、受信アクティビティをに送信します `OnConversationUpdateActivityAsync` 。 Teams アクティビティ ハンドラーは、まず Teams 固有のイベントをチェックします。 イベントが見つからない場合は、それらをボット フレームワークのアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つの主要な Teams アクティビティ ハンドラーがあります `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` 。 `OnConversationUpdateActivityAsync` すべての会話更新アクティビティをルーティングし、 `OnInvokeActivityAsync` すべての Teams 呼び出しアクティビティをルーティングします。

Teams 固有のアクティビティ ハンドラーのロジックを実装するには、ボット ロジック セクションに示すように、ボット内のメソッドをオーバーライド [する必要](#bot-logic) があります。 これらのハンドラーの基本実装はありません。そのため、オーバーライドに必要なロジックを追加する必要があります。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

ボットは、ボット フレームワークを使用して作成されます。 ボットがメッセージ アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受け取ります。 ターン ハンドラーは、受信アクティビティをアクティビティ ハンドラーに `onMessage` 送信します。 Teams では、この機能は変わりません。 ボットが会話更新アクティビティを受け取った場合、ターン ハンドラーはその受信アクティビティの通知を受け取り、受信アクティビティをに送信します `dispatchConversationUpdateActivity` 。 Teams アクティビティ ハンドラーは、まず Teams 固有のイベントをチェックします。 イベントが見つからない場合は、それらをボット フレームワークのアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つの主要な Teams アクティビティ ハンドラーがあります `dispatchConversationUpdateActivity` `onInvokeActivity` 。 `dispatchConversationUpdateActivity` すべての会話更新アクティビティをルーティングし、 `onInvokeActivity` すべての Teams 呼び出しアクティビティをルーティングします。

Teams 固有のアクティビティ ハンドラーのロジックを実装するには、ボット ロジック セクションに示すように、ボット内のメソッドをオーバーライド [する必要](#bot-logic) があります。 これらのハンドラーのボット ロジックを定義し、最後に必ず `next()` 呼び出します。 呼び出 `next()` しによって、次のハンドラーが実行されます。

# <a name="python"></a>[Python](#tab/python)

ボットは、ボット フレームワークを使用して作成されます。 ボットがメッセージ アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受け取ります。 ターン ハンドラーは、受信アクティビティをアクティビティ ハンドラーに `on_message_activity` 送信します。 Teams では、この機能は変わりません。 ボットが会話更新アクティビティを受け取った場合、ターン ハンドラーはその受信アクティビティの通知を受け取り、受信アクティビティをに送信します `on_conversation_update_activity` 。 Teams アクティビティ ハンドラーは、まず Teams 固有のイベントをチェックします。 イベントが見つからない場合は、それらをボット フレームワークのアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つの主要な Teams アクティビティ ハンドラーがあります `on_conversation_update_activity` `on_invoke_activity` 。 `on_conversation_update_activity` すべての会話更新アクティビティをルーティングし、 `on_invoke_activity` すべての Teams 呼び出しアクティビティをルーティングします。

Teams 固有のアクティビティ ハンドラーのロジックを実装するには、ボット ロジック セクションに示すように、ボット内のメソッドをオーバーライド [する必要](#bot-logic) があります。 これらのハンドラーの基本実装はありません。そのため、オーバーライドに必要なロジックを追加する必要があります。

---

## <a name="bot-logic"></a>ボット ロジック

ボット ロジックは、1 つ以上のボット チャネルからの受信アクティビティを処理し、応答して送信アクティビティを生成します。 これは、Teams アクティビティ ハンドラー クラスから派生したボットに対して引き続き当てはめ、最初に Teams アクティビティをチェックします。 Teams アクティビティを確認した後、他のすべてのアクティビティをボット フレームワークのアクティビティ ハンドラーに渡します。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>Core Bot Framework ハンドラー

>[!NOTE]
> 追加および削除 **されたメンバー** の **アクティビティ** を除き、このセクションで説明するアクティビティ ハンドラーはすべて、Teams 以外のボットと同様に機能し続ける。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストでは異なります。

定義されているハンドラーの一覧には `ActivityHandler` 、次のものが含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `OnTurnAsync` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| 受信したメッセージ アクティビティ | `OnMessageActivityAsync` | このメソッドは、アクティビティを処理するためにオーバーライド `Message` できます。 |
| 会話の更新アクティビティの受信 | `OnConversationUpdateActivityAsync` | このメソッドは、ボット以外のメンバーがアクティビティで会話に参加または離された場合にハンドラーを呼び出 `ConversationUpdate` します。 |
| ボット以外のメンバーが会話に参加しました | `OnMembersAddedAsync` | このメソッドは、会話に参加するメンバーを処理するためにオーバーライドできます。 |
| ボット以外のメンバーが会話を離した | `OnMembersRemovedAsync` | このメソッドは、会話を離れるメンバーを処理するためにオーバーライドできます。 |
| 受信したイベント アクティビティ | `OnEventActivityAsync` | このメソッドは、アクティビティのイベントの種類に固有のハンドラーを呼び出 `Event` します。 |
| 受信したトークン応答イベント アクティビティ | `OnTokenResponseEventAsync` | このメソッドは、トークン応答イベントを処理するためにオーバーライドできます。 |
| トークン以外の応答イベント アクティビティの受信 | `OnEventAsync` | このメソッドは、他の種類のイベントを処理するためにオーバーライドできます。 |
| 受信したその他のアクティビティの種類 | `OnUnrecognizedActivityTypeAsync` | このメソッドは、それ以外の場合は未処理のアクティビティの種類を処理するためにオーバーライドできます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 固有のアクティビティ ハンドラー

コア Bot Framework ハンドラー セクションのハンドラーの一覧を拡張して `TeamsActivityHandler` 、次の項目を含める。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | このメソッドは、作成中の Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話更新イベント[で作成されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | このメソッドは、削除する Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話更新イベント[で削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | このメソッドは、名前を変更する Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話の更新イベント[でチャネルの名前が変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)[された」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` このメソッドは、名前を変更する Teams チームを処理するためにオーバーライドできます。 詳細については、「会話の更新イベント [でチームの名前を](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 変更 [する」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `OnTeamsMembersAddedAsync` | このメソッドは、 で `OnMembersAddedAsync` メソッドを呼び出します `ActivityHandler` 。 このメソッドは、チームに参加しているメンバーを処理するためにオーバーライドできます。 詳細については、「会話の更新 [イベントに追加されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | このメソッドは、 で `OnMembersRemovedAsync` メソッドを呼び出します `ActivityHandler` 。 このメソッドは、チームを離れるメンバーを処理するためにオーバーライドできます。 詳細については、「会話更新イベント [で削除されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの `OnInvokeActivityAsync` 一覧には、次のものが含まれます。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | このメソッドは、カード アクションの呼び出しアクティビティがコネクタから受信されると呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | このメソッドは、ユーザーがファイル同意カードを受け入れるときに呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | このメソッドは、ファイル同意カードのアクティビティがコネクタから受信されると呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | このメソッドは、ファイル同意カードがユーザーによって拒否された場合に呼び出されます。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | このメソッドは、O365 コネクタ カードのアクション アクティビティがコネクタから受信されると呼び出されます。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | このメソッドは、signIn verify state activity がコネクタから受信されると呼び出されます。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | このメソッドは、派生クラスでオーバーライドして、タスク モジュールのフェッチ時にロジックを提供できます。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | このメソッドは、タスク モジュールの送信時にロジックを提供するために派生クラスでオーバーライドできます。 |

このセクションに記載されている呼び出しアクティビティは、Teams の会話型ボット用です。 ボット フレームワーク SDK では、メッセージング拡張機能に固有の呼び出しアクティビティもサポートしています。 詳細については、「メッセージング拡張機能 [について」を参照してください](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>Core Bot Framework ハンドラー

>[!NOTE]
> 追加および削除 **されたメンバー** の **アクティビティ** を除き、このセクションで説明するアクティビティ ハンドラーはすべて、Teams 以外のボットと同様に機能し続ける。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストでは異なります。

定義されているハンドラーの一覧には `ActivityHandler` 、次のものが含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `onTurn` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| 受信したメッセージ アクティビティ | `onMessage` | このメソッドは、アクティビティの処理に役立 `Message` ちます。 |
| 会話の更新アクティビティの受信 | `onConversationUpdate` | このメソッドは、ボット以外のメンバーがアクティビティで会話に参加または離された場合にハンドラーを呼び出 `ConversationUpdate` します。 |
| ボット以外のメンバーが会話に参加しました | `onMembersAdded` | このメソッドは、会話に参加するメンバーを処理するのに役立ちます。 |
| ボット以外のメンバーが会話を離した | `onMembersRemoved` | このメソッドは、会話を離れるメンバーを処理するのに役立ちます。 |
| 受信したイベント アクティビティ | `onEvent` | このメソッドは、アクティビティのイベントの種類に固有のハンドラーを呼び出 `Event` します。 |
| 受信したトークン応答イベント アクティビティ | `onTokenResponseEvent` | このメソッドは、トークン応答イベントの処理に役立ちます。 |
| 受信したその他のアクティビティの種類 | `onUnrecognizedActivityType` | このメソッドは、それ以外の場合は未処理のアクティビティの種類を処理するのに役立ちます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 固有のアクティビティ ハンドラー

コア Bot Framework ハンドラー セクションのハンドラーの一覧を拡張して `TeamsActivityHandler` 、次の項目を含める。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | このメソッドは、作成中の Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話更新イベント[で作成されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | このメソッドは、削除する Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話更新イベント[で削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | このメソッドは、名前を変更する Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話の更新イベント[でチャネルの名前が変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)[された」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` このメソッドは、名前を変更する Teams チームを処理するためにオーバーライドできます。 詳細については、「会話の更新イベント [でチームの名前を](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 変更 [する」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | このメソッドは、 で `OnMembersAddedAsync` メソッドを呼び出します `ActivityHandler` 。 このメソッドは、チームに参加しているメンバーを処理するためにオーバーライドできます。 詳細については、「会話の更新 [イベントに追加されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | このメソッドは、 で `OnMembersRemovedAsync` メソッドを呼び出します `ActivityHandler` 。 このメソッドは、チームを離れるメンバーを処理するためにオーバーライドできます。 詳細については、「会話更新イベント [で削除されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの `onInvokeActivity` 一覧には、次のものが含まれます。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | このメソッドは、カード アクションの呼び出しアクティビティがコネクタから受信されると呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | このメソッドは、ユーザーがファイル同意カードを受け入れるときに呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | このメソッドは、ファイル同意カードのアクティビティがコネクタから受信されると呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | このメソッドは、ファイル同意カードがユーザーによって拒否された場合に呼び出されます。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | このメソッドは、O365 コネクタ カードのアクション アクティビティがコネクタから受信されると呼び出されます。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | このメソッドは、signIn verify state activity がコネクタから受信されると呼び出されます。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | このメソッドは、派生クラスでオーバーライドして、タスク モジュールのフェッチ時にロジックを提供できます。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | このメソッドは、タスク モジュールの送信時にロジックを提供するために派生クラスでオーバーライドできます。 |

このセクションに記載されている呼び出しアクティビティは、Teams の会話型ボット用です。 ボット フレームワーク SDK では、メッセージング拡張機能に固有の呼び出しアクティビティもサポートしています。 詳細については、「メッセージング拡張機能 [について」を参照してください](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>Core Bot Framework ハンドラー

>[!NOTE]
> 追加および削除 **されたメンバー** の **アクティビティ** を除き、このセクションで説明するアクティビティ ハンドラーはすべて、Teams 以外のボットと同様に機能し続ける。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストでは異なります。

定義されているハンドラーの一覧には `ActivityHandler` 、次のものが含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `on_turn` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| 受信したメッセージ アクティビティ | `on_message_activity` | このメソッドは、アクティビティを処理するためにオーバーライド `Message` できます。 |
| 会話の更新アクティビティの受信 | `on_conversation_update_activity` | ボット以外のメンバーが会話に参加または離れた場合、このメソッドはハンドラーを呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `on_members_added_activity` | このメソッドは、会話に参加するメンバーを処理するためにオーバーライドできます。 |
| ボット以外のメンバーが会話を離した | `on_members_removed_activity` | このメソッドは、会話を離れるメンバーを処理するためにオーバーライドできます。 |
| 受信したイベント アクティビティ | `on_event_activity` | このメソッドは、イベントの種類に固有のハンドラーを呼び出します。 |
| 受信したトークン応答イベント アクティビティ | `on_token_response_event` | このメソッドは、トークン応答イベントを処理するためにオーバーライドできます。 |
| トークン以外の応答イベント アクティビティの受信 | `on_event` | このメソッドは、他の種類のイベントを処理するためにオーバーライドできます。 |
| 受信したその他のアクティビティの種類 | `on_unrecognized_activity_type` | このメソッドは、処理されない任意の種類のアクティビティを処理するためにオーバーライドできます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 固有のアクティビティ ハンドラー

コアの Bot Framework ハンドラー セクションからハンドラーの一覧を拡張して `TeamsActivityHandler` 、次の項目を含める。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | このメソッドは、作成中の Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話更新イベント[で作成されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `on_teams_channel_deleted` | このメソッドは、削除する Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話更新イベント[で削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `on_teams_channel_renamed` | このメソッドは、名前を変更する Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話の更新イベント[でチャネルの名前が変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)[された」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` このメソッドは、名前を変更する Teams チームを処理するためにオーバーライドできます。 詳細については、「会話の更新イベント [でチームの名前を](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 変更 [する」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `on_teams_members_added` | このメソッドは、 で `OnMembersAddedAsync` メソッドを呼び出します `ActivityHandler` 。 このメソッドは、チームに参加しているメンバーを処理するためにオーバーライドできます。 詳細については、「会話の更新 [イベントに追加されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `on_teams_members_removed` | このメソッドは、 で `OnMembersRemovedAsync` メソッドを呼び出します `ActivityHandler` 。 このメソッドは、チームを離れるメンバーを処理するためにオーバーライドできます。 詳細については、「会話更新イベント [で削除されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの `on_invoke_activity` 一覧には、次のものが含まれます。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | このメソッドは、カード アクションの呼び出しアクティビティがコネクタから受信されると呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | このメソッドは、ユーザーがファイル同意カードを受け入れるときに呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent`            | このメソッドは、ファイル同意カードのアクティビティがコネクタから受信されると呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | このメソッドは、ファイル同意カードがユーザーによって拒否された場合に呼び出されます。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | このメソッドは、O365 コネクタ カードのアクション アクティビティがコネクタから受信されると呼び出されます。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | このメソッドは、signIn verify state activity がコネクタから受信されると呼び出されます。 |
| task/fetch                      | `on_teams_task_module_fetch`        | このメソッドは、派生クラスでオーバーライドして、タスク モジュールのフェッチ時にロジックを提供できます。 |
| task/submit                     | `on_teams_task_module_submit`       | このメソッドは、タスク モジュールの送信時にロジックを提供するために派生クラスでオーバーライドできます。 |

このセクションに記載されている呼び出しアクティビティは、Teams の会話型ボット用です。 ボット フレームワーク SDK では、メッセージング拡張機能に固有の呼び出しアクティビティもサポートしています。 詳細については、「メッセージング拡張機能 [について」を参照してください](https://aka.ms/azure-bot-what-are-messaging-extensions)。

---

* * *

ボット アクティビティ ハンドラーについて理解し、会話と受信または送信するメッセージに応じてボットの動作が異なる方法を確認します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会話の基本](~/bots/how-to/conversations/conversation-basics.md)
