---
title: ボットの基本
author: clearab
description: Teams のボットの基本について理解します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 43dd351b30fdba3435d39aca43aae0f2de00ed24
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731959"
---
# <a name="bot-basics"></a>ボットの基本

これは、Bot Framework のコア ドキュメント[](https://aka.ms/how-bots-work)でのボットの動作に関する記事を基にした[概要です](https://aka.ms/azure-bot-service-docs)。 その記事と、その他の記事については、「概念」 *セクションを参照* してください。

Microsoft Teams 用に開発されたボットの主な違いは、アクティビティの処理方法です。 Microsoft Teams アクティビティ ハンドラーは、Bot Framework のアクティビティ ハンドラーから派生し、Teams 以外のアクティビティの処理を許可する前に、すべての Teams アクティビティをルーティングします。

## <a name="teams-activity-handlers"></a>Teams アクティビティ ハンドラー

Microsoft Teams 向けのボットは、受信したアクティビティを *アクティビティ ハンドラー* に渡します。 内部には *ターン ハンドラー* と呼ばれる 1 つの基本ハンドラーがあり、すべてのアクティビティがルーティングされます。 ターン *ハンドラーは、* 受信したアクティビティの種類を処理するために必要なアクティビティ ハンドラーを呼び出します。 Microsoft Teams 用に設計されたボットが異なるのは、Bot Framework のクラスから派生したクラスから `TeamsActivityHandler` 派生 `ActivityHandler` する点です。

# <a name="c"></a>[C#](#tab/csharp)

Microsoft Bot Framework を使用して作成されたボットと同様に、ボットがメッセージ アクティビティを受信すると、ターン ハンドラーは受信アクティビティを確認し、それをアクティビティ ハンドラーに `OnMessageActivityAsync` 送信します。 Teams では、この機能は変わりません。 ボットが会話の更新アクティビティを受け取った場合、ターン ハンドラーは受信アクティビティを確認し、それを次のアクティビティに送信します `OnConversationUpdateActivityAsync` 。 *Teams* のアクティビティ ハンドラー。最初に Teams 固有のイベントをチェックし、見つからない場合は Bot Framework のアクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つの主要な Teams アクティビティ ハンドラーがあります。このハンドラーは、すべての会話更新アクティビティをルーティングし、すべての Teams 呼び出しアクティビティを `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` ルーティングします。

Teams 固有のアクティビティ ハンドラーのロジックを実装するには、以下のボット ロジック セクションに示すように、ボットでこれらのメソッド [を](#bot-logic) オーバーライドします。 これらの各ハンドラーに基本実装はないので、オーバーライドで必要なロジックを追加します。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Microsoft Bot Framework を使用して作成されたボットと同様に、ボットがメッセージ アクティビティを受信すると、ターン ハンドラーは受信アクティビティを確認し、それをアクティビティ ハンドラーに `onMessage` 送信します。 Teams では、この機能は変わりません。 ボットが会話の更新アクティビティを受け取った場合、ターン ハンドラーは受信アクティビティを確認し、それを次のアクティビティに送信します `dispatchConversationUpdateActivity` 。 *Teams* のアクティビティ ハンドラー。最初に Teams 固有のイベントをチェックし、見つからない場合はボット フレームワーク アクティビティ ハンドラーに渡します。

Teams アクティビティ ハンドラー クラスには、2 つの主要な Teams アクティビティ ハンドラーがあります。このハンドラーは、すべての会話更新アクティビティをルーティングし、すべての Teams 呼び出しアクティビティを `dispatchConversationUpdateActivity` `onInvokeActivity` ルーティングします。

Teams 固有のアクティビティ ハンドラーのロジックを実装するには、ボットのロジック セクションに示されているボットでこれらのメソッド [をオーバーライド](#bot-logic) します。 これらの各ハンドラーについて、ボットロジックを定義し、 **最後に `next()` 必ず呼び出してください**。 呼び `next()` 出すことによって、次のハンドラーが実行されます。

# <a name="python"></a>[Python](#tab/python)

ボットは Microsoft Bot Framework を使用して作成され、ボットがメッセージ アクティビティを受信すると、ターン ハンドラーはその受信アクティビティの通知を受信します。 その後、ターン ハンドラーは受信アクティビティをアクティビティ ハンドラーに `on_message_activity` 送信します。 Teams では、この機能は変わりません。 ボットが会話更新アクティビティを受け取った場合、ターン ハンドラーはその受信アクティビティの通知を受け取り、着信アクティビティを次に送信します `on_conversation_update_activity` 。 Teams アクティビティ ハンドラーは、最初に Teams 固有のイベントをチェックします。 イベントが見つからない場合は、Bot Framework のアクティビティ ハンドラーに渡されます。

Teams アクティビティ ハンドラー クラスには、2 つの主要な Teams アクティビティ ハンドラーと `on_conversation_update_activity` `on_invoke_activity` . `on_conversation_update_activity` すべての会話更新アクティビティをルーティングし、 `on_invoke_activity` すべての Teams 呼び出しアクティビティをルーティングします。

Teams 固有のアクティビティ ハンドラーのロジックを実装するには、ボットのロジック セクションに示すように、ボットでこれらのメソッドを [オーバーライドする必要](#bot-logic) があります。 これらのハンドラーの基本実装はありません。そのため、オーバーライドで必要なロジックを追加する必要があります。

---

## <a name="bot-logic"></a>ボット ロジック

ボット ロジックは、1 つ以上のボット チャネルからの受信アクティビティを処理し、応答で送信アクティビティを生成します。  これは、Teams アクティビティ ハンドラー クラスから派生したボットの場合にも当てはまるので、最初に Teams アクティビティをチェックし、次に他のすべてのアクティビティをボット フレームワークアクティビティ ハンドラーに渡します。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>コア Bot Framework ハンドラー

以下に説明するアクティビティ ハンドラーはすべて、Teams ボット以外のボットの場合と同様に引き続き動作します。ただし、追加されたメンバーとメンバーがアクティビティを削除する場合を除き、これらはチームのコンテキストでは異なります。チームでは、メッセージ スレッドではなく、新しいメンバーがチームに追加されます。

定義されているハンドラーの `ActivityHandler` 概要を以下に示します。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `OnTurnAsync` | 受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| 受信したメッセージ アクティビティ | `OnMessageActivityAsync` | これをオーバーライドしてアクティビティを処理 `Message` します。 |
| 受信した会話の更新アクティビティ | `OnConversationUpdateActivityAsync` | アクティビティで、ボット以外のメンバーが会話に参加または会話を離えた場合に `ConversationUpdate` ハンドラーを呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `OnMembersAddedAsync` | これをオーバーライドして、会話に参加するメンバーを処理します。 |
| ボット以外のメンバーが会話を離した | `OnMembersRemovedAsync` | メンバーが会話を離れる処理を行う場合は、これをオーバーライドします。 |
| 受信したイベント アクティビティ | `OnEventActivityAsync` | アクティビティでは `Event` 、イベントの種類に固有のハンドラーを呼び出します。 |
| 受信したトークン応答イベント アクティビティ | `OnTokenResponseEventAsync` | トークン応答イベントを処理するには、これをオーバーライドします。 |
| 受信した非トークン応答イベント アクティビティ | `OnEventAsync` | これをオーバーライドして、他の種類のイベントを処理します。 |
| 受信したその他のアクティビティの種類 | `OnUnrecognizedActivityTypeAsync` | それ以外の場合は処理されないアクティビティの種類を処理するには、これをオーバーライドします。 |

#### <a name="teams-specific-handlers"></a>Teams 固有のハンドラー

上記 `TeamsActivityHandler` のハンドラーの一覧を拡張して、以下を含める。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | これをオーバーライドして、作成中の Teams チャネルを処理します。 詳細については、会話の[更新イベントで作成された](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[チャネルを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | これを上書きして、削除される Teams チャネルを処理します。 詳細については、会話の[更新イベントで削除された](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[チャネルを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | これをオーバーライドして、名前を変更する Teams チャネルを処理します。 詳細については、会話の更新[イベントでチャネルの名前が](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)[変更されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` これをオーバーライドして、名前を変更する Teams チームを処理します。 詳細については、会話の更新[イベントでチームの名前が](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)[変更されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `OnTeamsMembersAddedAsync` | でメソッドを `OnMembersAddedAsync` 呼び出します `ActivityHandler` 。 これをオーバーライドして、チームに参加するメンバーを処理します。 詳細については、会話の[更新イベントで追加された](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[チーム メンバーを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | でメソッドを `OnMembersRemovedAsync` 呼び出します `ActivityHandler` 。 これをオーバーライドして、チームから離れるメンバーを処理します。 詳細については、会話の更新[イベントで削除された](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)[チーム メンバーを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの一覧を `OnInvokeActivityAsync` 次に示します。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Teams カード アクションの呼び出し。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Teams ファイルの同意に同意します。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Teams ファイルの同意。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Teams ファイルの同意。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Teams O365 コネクタ カード アクション。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Teams サインインの確認状態。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Teams タスク モジュールのフェッチ。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | Teams タスク モジュール提出。 |

上記の起動アクティビティは、Teams の会話ボット用です。 Bot Framework SDK は、メッセージング拡張機能に固有の呼び出しもサポートします。 詳細については、「 [メッセージング拡張機能について」を参照してください。](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="javascript"></a>[JavaScript](#tab/javascript)

以下で説明するアクティビティ ハンドラーはすべて、Teams ボット以外のボットと同様に引き続き動作します。ただし、追加されたメンバーと削除されたアクティビティを処理する場合を除き、これらはチームのコンテキストでは異なります。チームでは、メッセージ スレッドではなく、新しいメンバーがチームに追加されます。

#### <a name="core-bot-framework-handlers"></a>コア Bot Framework ハンドラー

定義されているハンドラーの `ActivityHandler` 概要を以下に示します。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `onTurn` | 受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| 受信したメッセージ アクティビティ | `onMessage` | アクティビティを処理する関数を提供 `Message` します。 |
| 受信した会話の更新アクティビティ | `onConversationUpdate` | アクティビティで、ボット以外のメンバーが会話に参加または会話を離えた場合に `ConversationUpdate` ハンドラーを呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `onMembersAdded` | 会話に参加するメンバーを処理する関数を提供します。 |
| ボット以外のメンバーが会話を離した | `onMembersRemoved` | 会話を離れるメンバーを処理する関数を提供します。 |
| 受信したイベント アクティビティ | `onEvent` | アクティビティでは `Event` 、イベントの種類に固有のハンドラーを呼び出します。 |
| 受信したトークン応答イベント アクティビティ | `onTokenResponseEvent` | トークン応答イベントを処理する関数を提供します。 |
| 受信したその他のアクティビティの種類 | `onUnrecognizedActivityType` | それ以外の場合は未処理のアクティビティの種類を処理する関数を提供します。 |
| アクティビティ ハンドラーが完了しました | `onDialog` | 残りのアクティビティ ハンドラーが完了した後、ターンの最後に実行する必要がある処理を処理する関数を提供します。 |

#### <a name="teams-specific-handlers"></a>Teams 固有のハンドラー

コア Bot Framework ハンドラー セクションのハンドラーの一覧を `TeamsActivityHandler` 拡張し、次の項目を含める。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | これをオーバーライドして、作成中の Teams チャネルを処理します。 詳細については、会話の[更新イベントで作成された](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[チャネルを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | これを上書きして、削除される Teams チャネルを処理します。 詳細については、会話の[更新イベントで削除された](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[チャネルを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | これをオーバーライドして、名前を変更する Teams チャネルを処理します。 詳細については、会話の更新[イベントでチャネルの名前が](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)[変更されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` これを上書きして、名前を変更する Teams チームを処理します。 詳細については、会話の更新[イベントでチームの名前が](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)[変更されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | でメソッドを `OnMembersAddedAsync` 呼び出します `ActivityHandler` 。 これをオーバーライドして、チームに参加するメンバーを処理します。 詳細については、会話の[更新イベントで追加された](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[チーム メンバーを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | でメソッドを `OnMembersRemovedAsync` 呼び出します `ActivityHandler` 。 これをオーバーライドして、チームから離れるメンバーを処理します。 詳細については、会話の更新[イベントで削除された](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)[チーム メンバーを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの一覧を `onInvokeActivity` 次に示します。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Teams カード アクションが呼び出されます。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Teams ファイルの同意に同意します。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Teams ファイルの同意。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Teams ファイルの同意。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Teams O365 コネクタ カードアクション。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Teams サインインの確認状態。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Teams タスク モジュールのフェッチ。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | Teams タスク モジュール送信。 |

Teams の呼び出しアクティビティ セクションにリストされている起動アクティビティは、Teams の会話ボット用です。 Bot Framework SDK は、メッセージング拡張機能に固有の呼び出しアクティビティもサポートします。 詳細については、「メッセージング拡張機能について [」を参照してください](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>コア Bot Framework ハンドラー

>[!NOTE]
> 追加および削除されたメンバーのアクティビティを除き、このセクションで説明するアクティビティ ハンドラーはすべて、Teams 以外のボットと同様に引き続き動作します。

アクティビティ ハンドラーは、メッセージ スレッドの代わりに新しいメンバーがチームに追加されるチームのコンテキストでは異なります。

定義されているハンドラーの一覧は `ActivityHandler` 次のとおりです。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したアクティビティの種類 | `on_turn` | 受信したアクティビティの種類に基づいて、他のハンドラーのいずれかを呼び出します。 |
| 受信したメッセージ アクティビティ | `on_message_activity` | アクティビティを処理するためにこれをオーバーライド `Message` します。 |
| 受信した会話の更新アクティビティ | `on_conversation_update_activity` | ボット以外のメンバーが会話に参加または会話を離れた場合にハンドラーを呼び出します。 |
| ボット以外のメンバーが会話に参加しました | `on_members_added_activity` | これをオーバーライドして、会話に参加するメンバーを処理します。 |
| ボット以外のメンバーが会話を離した | `on_members_removed_activity` | 会話から退出するメンバーを処理するためにこれをオーバーライドします。 |
| 受信したイベント アクティビティ | `on_event_activity` | イベントの種類に固有のハンドラーを呼び出します。 |
| 受信したトークン応答イベント アクティビティ | `on_token_response_event` | トークン応答イベントを処理するためにこれをオーバーライドします。 |
| 受信した非トークン応答イベント アクティビティ | `on_event` | 他の種類のイベントを処理するためにこれをオーバーライドします。 |
| 受信したその他のアクティビティの種類 | `on_unrecognized_activity_type` | これをオーバーライドして、処理されない種類のアクティビティを処理します。 |

#### <a name="teams-specific-handlers"></a>Teams 固有のハンドラー

コア Bot Framework ハンドラー セクションのハンドラーの一覧 `TeamsActivityHandler` を拡張して、次のものが含まれます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | 作成中の Teams チャネルを処理するためにこれをオーバーライドします。 詳細については、「会話の更新[イベントで作成された](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[チャネル」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `on_teams_channel_deleted` | 削除する Teams チャネルを処理するためにこれをオーバーライドします。 詳細については、「会話の更新[イベントで削除されたチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `on_teams_channel_renamed` | これをオーバーライドして、名前を変更する Teams チャネルを処理します。 詳細については、会話の更新[イベントでチャネルの名前が変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)[されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` これを上書きして、名前を変更する Teams チームを処理します。 詳細については、会話の更新[イベントでチームの名前が変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)[されたを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `on_teams_members_added` | でメソッドを `OnMembersAddedAsync` 呼び出します `ActivityHandler` 。 これをオーバーライドして、チームに参加するメンバーを処理します。 詳細については、「会話の更新 [イベントで追加された](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added) チーム メンバー [」を参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `on_teams_members_removed` | でメソッドを `OnMembersRemovedAsync` 呼び出します `ActivityHandler` 。 チームから退出するメンバーを処理するためにこれをオーバーライドします。 詳細については、会話の更新[イベントで削除されたチーム](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)[メンバーを参照してください](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

Teams アクティビティ ハンドラーから呼び出される Teams アクティビティ ハンドラーの `on_invoke_activity` 一覧は、次のとおりです。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Teams カード アクションが呼び出されます。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Teams ファイルの同意に同意します。 |
| fileConsent/invoke              | `on_teams_file_consent`            | Teams ファイルの同意。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Teams ファイルの同意が拒否されます。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Teams O365 コネクタ カードアクション。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | Teams サインインの確認状態。 |
| task/fetch                      | `on_teams_task_module_fetch`        | Teams タスク モジュールのフェッチ。 |
| task/submit                     | `on_teams_task_module_submit`       | Teams タスク モジュール送信。 |

Teams の呼び出しアクティビティ セクションにリストされている起動アクティビティは、Teams の会話ボット用です。 Bot Framework SDK は、メッセージング拡張機能に固有の呼び出しアクティビティもサポートします。 詳細については、「メッセージング拡張機能について [」を参照してください](https://aka.ms/azure-bot-what-are-messaging-extensions)。

---
