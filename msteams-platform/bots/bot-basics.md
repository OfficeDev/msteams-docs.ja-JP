---
title: ボットの基本
author: clearab
description: Teams のボットの基本について理解します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 3c4e707fa4677c2441f348e8d09ecf4428ef1296
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014503"
---
# <a name="bot-basics"></a>ボットの基本

このドキュメントでは、Bot Framework のコア ドキュメントでボットがどのように機能する[](https://aka.ms/how-bots-work)のかという記事に基を組み込む Microsoft Teams のボットの概要[について説明します](https://aka.ms/azure-bot-service-docs)。 Microsoft Teams 用に開発されたボットと主要な Bot Framework の主な違いは、Teams で提供される機能です。

## <a name="teams-activity-handlers"></a>Teams アクティビティ ハンドラー

Teams アクティビティ ハンドラーは、Microsoft Bot Framework のアクティビティ ハンドラーから派生します。 Teams 以外の特定のアクティビティの処理を許可する前に、すべての Teams アクティビティをルーティングします。

Teams のボットがアクティビティを受信すると、アクティビティ ハンドラーに *指示されます*。 すべてのアクティビティは、ターン ハンドラーと呼ばれる 1 つの基本ハンドラーを介 *してルーティングされます*。 ターン *ハンドラーは、受信* したアクティビティを管理するために必要なアクティビティ ハンドラーを呼び出します。 Teams ボットは、Bot Framework のクラスから派生したクラス `TeamsActivityHandler` から派生 `ActivityHandler` します。

# <a name="c"></a>[C#](#tab/csharp)

ボットは Bot Framework を使用して作成されます。 ボットがメッセージ アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受け取ります。 次に、ターン ハンドラーは受信アクティビティをアクティビティ ハンドラーに `OnMessageActivityAsync` 送信します。 Teams では、この機能は変わりません。 ボットが会話の更新アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受け取り、着信アクティビティを送信します `OnConversationUpdateActivityAsync` 。 Teams アクティビティ ハンドラーは、最初に Teams 固有のイベントをチェックします。 イベントが見つからない場合は、それらを Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つの主要な Teams アクティビティ ハンドラーと `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` . `OnConversationUpdateActivityAsync` すべての会話更新アクティビティをルーティングし、 `OnInvokeActivityAsync` すべての Teams 呼び出しアクティビティをルーティングします。

Teams 固有のアクティビティ ハンドラーのロジックを実装するには、ボットのロジック セクションに示すように、ボットのメソッドを [オーバーライドする必要](#bot-logic) があります。 これらのハンドラーの基本実装は何も行うので、オーバーライドで必要なロジックを追加する必要があります。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

ボットは Bot Framework を使用して作成されます。 ボットがメッセージ アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受け取ります。 次に、ターン ハンドラーは受信アクティビティをアクティビティ ハンドラーに `onMessage` 送信します。 Teams では、この機能は変わりません。 ボットが会話の更新アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受け取り、着信アクティビティを送信します `dispatchConversationUpdateActivity` 。 Teams アクティビティ ハンドラーは、最初に Teams 固有のイベントをチェックします。 イベントが見つからない場合は、それらを Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つの主要な Teams アクティビティ ハンドラーと `dispatchConversationUpdateActivity` `onInvokeActivity` . `dispatchConversationUpdateActivity` すべての会話更新アクティビティをルーティングし、 `onInvokeActivity` すべての Teams 呼び出しアクティビティをルーティングします。

Teams 固有のアクティビティ ハンドラーのロジックを実装するには、ボットのロジック セクションに示すように、ボットのメソッドを [オーバーライドする必要](#bot-logic) があります。 これらのハンドラーのボット ロジックを定義し、 **最後に `next()` 必ず呼び出してください**。 呼び `next()` 出すことによって、次のハンドラーが実行されます。

# <a name="python"></a>[Python](#tab/python)

ボットは Bot Framework を使用して作成されます。 ボットがメッセージ アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受け取ります。 次に、ターン ハンドラーは受信アクティビティをアクティビティ ハンドラーに `on_message_activity` 送信します。 Teams では、この機能は変わりません。 ボットが会話の更新アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受け取り、着信アクティビティを送信します `on_conversation_update_activity` 。 Teams アクティビティ ハンドラーは、最初に Teams 固有のイベントをチェックします。 イベントが見つからない場合は、それらを Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つの主要な Teams アクティビティ ハンドラーと `on_conversation_update_activity` `on_invoke_activity` . `on_conversation_update_activity` すべての会話更新アクティビティをルーティングし、 `on_invoke_activity` すべての Teams 呼び出しアクティビティをルーティングします。

Teams 固有のアクティビティ ハンドラーのロジックを実装するには、ボットのロジック セクションに示すように、ボットのメソッドを [オーバーライドする必要](#bot-logic) があります。 これらのハンドラーの基本実装は何も行うので、オーバーライドで必要なロジックを追加する必要があります。

---

## <a name="bot-logic"></a>ボット ロジック

ボット ロジックは、1 つ以上のボット チャネルからの受信アクティビティを処理し、応答で送信アクティビティを生成します。 これは、最初に Teams アクティビティをチェックする Teams アクティビティ ハンドラー クラスから派生したボットにも当てはまる場合です。 Teams アクティビティを確認すると、その他のすべてのアクティビティが Bot Framework のアクティビティ ハンドラーに渡されます。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>コア Bot Framework ハンドラー

>[!NOTE]
> 追加および *削除された* メンバーのアクティビティを除き、このセクションで説明するアクティビティ ハンドラーはすべて、Teams 以外のボットの場合と同様に引き続き動作します。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストでは異なります。

定義されているハンドラーの一覧は `ActivityHandler` 次のとおりです。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `OnTurnAsync` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーの 1 つを呼び出します。 |
| 受信したメッセージ アクティビティ | `OnMessageActivityAsync` | このメソッドは、アクティビティを処理するためにオーバーライド `Message` できます。 |
| 受信した会話の更新アクティビティ | `OnConversationUpdateActivityAsync` | このメソッドは、ボット以外のメンバーがアクティビティで会話に参加または会話から出た場合にハンドラーを呼び出 `ConversationUpdate` します。 |
| ボット以外のメンバーが会話に参加しました | `OnMembersAddedAsync` | このメソッドは、会話に参加するメンバーを処理するためにオーバーライドできます。 |
| ボット以外のメンバーが会話を離した | `OnMembersRemovedAsync` | このメソッドは、会話を離れるメンバーを処理するためにオーバーライドできます。 |
| 受信したイベント アクティビティ | `OnEventActivityAsync` | このメソッドは、アクティビティのイベントの種類に固有のハンドラーを呼び出 `Event` します。 |
| 受信したトークン応答イベント アクティビティ | `OnTokenResponseEventAsync` | このメソッドは、トークン応答イベントを処理するためにオーバーライドできます。 |
| 受信した非トークン応答イベント アクティビティ | `OnEventAsync` | このメソッドは、他の種類のイベントを処理するためにオーバーライドできます。 |
| 受信したその他のアクティビティの種類 | `OnUnrecognizedActivityTypeAsync` | このメソッドはオーバーライドして、それ以外の場合は未処理のアクティビティの種類を処理できます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 固有のアクティビティ ハンドラー

コア Bot Framework ハンドラー セクションのハンドラーの一覧を `TeamsActivityHandler` 拡張し、次の項目を含める。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | このメソッドは、作成中の Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話の更新[イベントで作成された](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[チャネル」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | このメソッドは、削除される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話の更新[イベントで削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | このメソッドは、名前を変更する Teams チャネルを処理するためにオーバーライドできます。 詳細については、会話の更新[イベントでチャネルの名前が変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)[されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` このメソッドは、名前を変更する Teams チームを処理するためにオーバーライドできます。 詳細については、会話の更新 [イベントでチームの名前が](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 変更 [されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `OnTeamsMembersAddedAsync` | このメソッドは、次のメソッド `OnMembersAddedAsync` を呼び出します `ActivityHandler` 。 このメソッドは、チームに参加するメンバーを処理するためにオーバーライドできます。 詳細については、「会話の更新 [イベントで追加された](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) チーム メンバー [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | このメソッドは、次のメソッド `OnMembersRemovedAsync` を呼び出します `ActivityHandler` 。 このメソッドは、チームから離れるメンバーを処理するためにオーバーライドできます。 詳細については、「会話の更新 [イベントで削除されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの `OnInvokeActivityAsync` 一覧は、次のとおりです。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | このメソッドは、カード アクション呼び出しアクティビティがコネクタから受信されると呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | このメソッドは、ユーザーがファイル同意カードを受け入れるときに呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | このメソッドは、コネクタからファイル同意カードアクティビティを受信すると呼び出されます。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | このメソッドは、ユーザーがファイル同意カードを拒否すると呼び出されます。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | このメソッドは、O365 コネクタ カードアクション アクティビティがコネクタから受信されると呼び出されます。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | このメソッドは、サインイン検証状態アクティビティがコネクタから受信されると呼び出されます。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | このメソッドは、タスク モジュールのフェッチ時にロジックを提供するために派生クラスでオーバーライドできます。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | このメソッドは、タスク モジュールの送信時にロジックを提供するために派生クラスでオーバーライドできます。 |

このセクションに記載されている起動アクティビティは、Teams の会話ボット用です。 Bot Framework SDK は、メッセージング拡張機能に固有の呼び出しアクティビティもサポートします。 詳細については、「メッセージング拡張機能 [について」を参照してください](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>コア Bot Framework ハンドラー

>[!NOTE]
> 追加および *削除された* メンバーのアクティビティを除き、このセクションで説明するアクティビティ ハンドラーはすべて、Teams 以外のボットの場合と同様に引き続き動作します。

アクティビティ ハンドラーは、新しいメンバーがメッセージ スレッドではなくチームに追加されるチームのコンテキストでは異なります。

定義されているハンドラーの一覧は `ActivityHandler` 次のとおりです。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `onTurn` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーの 1 つを呼び出します。 |
| 受信したメッセージ アクティビティ | `onMessage` | このメソッドは、アクティビティの処理に役立 `Message` ちます。 |
| 受信した会話の更新アクティビティ | `onConversationUpdate` | このメソッドは、ボット以外のメンバーがアクティビティで会話に参加または会話から出た場合にハンドラーを呼び出 `ConversationUpdate` します。 |
| ボット以外のメンバーが会話に参加しました | `onMembersAdded` | このメソッドは、会話に参加するメンバーを処理するのに役立ちます。 |
| ボット以外のメンバーが会話を離した | `onMembersRemoved` | このメソッドは、会話を離れるメンバーを処理するのに役立ちます。 |
| 受信したイベント アクティビティ | `onEvent` | このメソッドは、アクティビティのイベントの種類に固有のハンドラーを呼び出 `Event` します。 |
| 受信したトークン応答イベント アクティビティ | `onTokenResponseEvent` | このメソッドは、トークン応答イベントの処理に役立ちます。 |
| 受信したその他のアクティビティの種類 | `onUnrecognizedActivityType` | このメソッドは、それ以外の場合は処理されないアクティビティの種類を処理するのに役立ちます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 固有のアクティビティ ハンドラー

コア Bot Framework ハンドラー セクションのハンドラーの一覧を `TeamsActivityHandler` 拡張し、次の項目を含める。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | このメソッドは、作成中の Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話の更新[イベントで作成された](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[チャネル」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | このメソッドは、削除される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話の更新[イベントで削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | このメソッドは、名前を変更する Teams チャネルを処理するためにオーバーライドできます。 詳細については、会話の更新[イベントでチャネルの名前が変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)[されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` このメソッドは、名前を変更する Teams チームを処理するためにオーバーライドできます。 詳細については、会話の更新 [イベントでチームの名前が](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 変更 [されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | このメソッドは、次のメソッド `OnMembersAddedAsync` を呼び出します `ActivityHandler` 。 このメソッドは、チームに参加するメンバーを処理するためにオーバーライドできます。 詳細については、「会話の更新 [イベントで追加された](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) チーム メンバー [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | このメソッドは、次のメソッド `OnMembersRemovedAsync` を呼び出します `ActivityHandler` 。 このメソッドは、チームから離れるメンバーを処理するためにオーバーライドできます。 詳細については、「会話の更新 [イベントで削除されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの `onInvokeActivity` 一覧は、次のとおりです。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | このメソッドは、カード アクション呼び出しアクティビティがコネクタから受信されると呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | このメソッドは、ユーザーがファイル同意カードを受け入れるときに呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | このメソッドは、コネクタからファイル同意カードアクティビティを受信すると呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | このメソッドは、ユーザーがファイル同意カードを拒否すると呼び出されます。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | このメソッドは、O365 コネクタ カードアクション アクティビティがコネクタから受信されると呼び出されます。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | このメソッドは、サインイン検証状態アクティビティがコネクタから受信されると呼び出されます。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | このメソッドは、タスク モジュールのフェッチ時にロジックを提供するために派生クラスでオーバーライドできます。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | このメソッドは、タスク モジュールの送信時にロジックを提供するために派生クラスでオーバーライドできます。 |

このセクションに記載されている起動アクティビティは、Teams の会話ボット用です。 Bot Framework SDK は、メッセージング拡張機能に固有の呼び出しアクティビティもサポートします。 詳細については、「メッセージング拡張機能 [について」を参照してください](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>コア Bot Framework ハンドラー

>[!NOTE]
> 追加および *削除された* メンバーのアクティビティを除き、このセクションで説明するアクティビティ ハンドラーはすべて、Teams 以外のボットの場合と同様に引き続き動作します。

アクティビティ ハンドラーは、新しいメンバーがメッセージ スレッドではなくチームに追加されるチームのコンテキストでは異なります。

定義されているハンドラーの一覧は `ActivityHandler` 次のとおりです。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `on_turn` | このメソッドは、受信したアクティビティの種類に基づいて、他のハンドラーの 1 つを呼び出します。 |
| 受信したメッセージ アクティビティ | `on_message_activity` | このメソッドは、アクティビティを処理するためにオーバーライド `Message` できます。 |
| 受信した会話の更新アクティビティ | `on_conversation_update_activity` | ボット以外のメンバーが会話に参加または会話を離れた場合、このメソッドはハンドラーを呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `on_members_added_activity` | このメソッドは、会話に参加するメンバーを処理するためにオーバーライドできます。 |
| ボット以外のメンバーが会話を離した | `on_members_removed_activity` | このメソッドは、会話を離れるメンバーを処理するためにオーバーライドできます。 |
| 受信したイベント アクティビティ | `on_event_activity` | このメソッドは、イベントの種類に固有のハンドラーを呼び出します。 |
| 受信したトークン応答イベント アクティビティ | `on_token_response_event` | このメソッドは、トークン応答イベントを処理するためにオーバーライドできます。 |
| 受信した非トークン応答イベント アクティビティ | `on_event` | このメソッドは、他の種類のイベントを処理するためにオーバーライドできます。 |
| 受信したその他のアクティビティの種類 | `on_unrecognized_activity_type` | このメソッドは、処理されない任意の種類のアクティビティを処理するためにオーバーライドできます。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 固有のアクティビティ ハンドラー

コア Bot Framework ハンドラー セクションのハンドラーの一覧を `TeamsActivityHandler` 拡張し、次の項目を含める。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | このメソッドは、作成中の Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話の更新[イベントで作成された](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[チャネル」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `on_teams_channel_deleted` | このメソッドは、削除される Teams チャネルを処理するためにオーバーライドできます。 詳細については、「会話の更新[イベントで削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `on_teams_channel_renamed` | このメソッドは、名前を変更する Teams チャネルを処理するためにオーバーライドできます。 詳細については、会話の更新[イベントでチャネルの名前が変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)[されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` このメソッドは、名前を変更する Teams チームを処理するためにオーバーライドできます。 詳細については、会話の更新 [イベントでチームの名前が](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 変更 [されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `on_teams_members_added` | このメソッドは、次のメソッド `OnMembersAddedAsync` を呼び出します `ActivityHandler` 。 このメソッドは、チームに参加するメンバーを処理するためにオーバーライドできます。 詳細については、「会話の更新 [イベントで追加された](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) チーム メンバー [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `on_teams_members_removed` | このメソッドは、次のメソッド `OnMembersRemovedAsync` を呼び出します `ActivityHandler` 。 このメソッドは、チームから離れるメンバーを処理するためにオーバーライドできます。 詳細については、「会話の更新 [イベントで削除されたチーム メンバー](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの `on_invoke_activity` 一覧は、次のとおりです。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | このメソッドは、カード アクション呼び出しアクティビティがコネクタから受信されると呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | このメソッドは、ユーザーがファイル同意カードを受け入れるときに呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent`            | このメソッドは、コネクタからファイル同意カードアクティビティを受信すると呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | このメソッドは、ユーザーがファイル同意カードを拒否すると呼び出されます。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | このメソッドは、O365 コネクタ カードアクション アクティビティがコネクタから受信されると呼び出されます。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | このメソッドは、サインイン検証状態アクティビティがコネクタから受信されると呼び出されます。 |
| task/fetch                      | `on_teams_task_module_fetch`        | このメソッドは、タスク モジュールのフェッチ時にロジックを提供するために派生クラスでオーバーライドできます。 |
| task/submit                     | `on_teams_task_module_submit`       | このメソッドは、タスク モジュールの送信時にロジックを提供するために派生クラスでオーバーライドできます。 |

このセクションに記載されている起動アクティビティは、Teams の会話ボット用です。 Bot Framework SDK は、メッセージング拡張機能に固有の呼び出しアクティビティもサポートします。 詳細については、「メッセージング拡張機能 [について」を参照してください](https://aka.ms/azure-bot-what-are-messaging-extensions)。

---
