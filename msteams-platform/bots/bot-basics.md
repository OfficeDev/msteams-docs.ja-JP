---
title: Bot の基本
author: clearab
description: Teams でのボットの基本事項について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e1b0c79b73ae89c8ab76ba0a1ff045603ab0b932
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674790"
---
# <a name="bot-basics"></a>Bot の基本

この記事では、「core [Bot Framework」ドキュメント](https://aka.ms/azure-bot-service-docs)での[ボットの機能](https://aka.ms/how-bots-work)について説明します。 この記事やその他の記事については、「*概念*」の「役に立つ場合があります。

Microsoft Teams 向けに開発された bot の主な違いは、アクティビティの処理方法です。 Microsoft Teams アクティビティハンドラーは、ボットフレームワークのアクティビティハンドラーから派生して、teams 以外のすべてのアクティビティを処理できるようにする前に、すべての Teams アクティビティをルーティングします。

## <a name="teams-activity-handlers"></a>Teams アクティビティハンドラー

Microsoft Teams の bot がアクティビティを受信すると、そのアクティビティは*アクティビティハンドラー*に渡されます。 この記事では、 *turn ハンドラー*と呼ばれる基本的なハンドラーが1つあります。これには、すべてのアクティビティがルーティングされます。 *Turn ハンドラー*は、どの種類のアクティビティを受信したかを処理するために必要なアクティビティハンドラーを呼び出します。 Microsoft Teams 向けに設計された bot は、ボットフレームワークの`TeamsActivityHandler` `ActivityHandler`クラスから派生したクラスから派生したものであるという点が異なります。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

Microsoft Bot フレームワークを使用して作成された bot と同様に、bot がメッセージアクティビティを受信すると、turn ハンドラーはその受信アクティビティ`OnMessageActivityAsync`を認識し、アクティビティハンドラーに送信します。 Teams では、この機能は変わりません。 Bot が会話更新アクティビティを受信した場合、turn ハンドラーはその受信アクティビティを認識して`OnConversationUpdateActivityAsync` *teams*アクティビティハンドラーに送信します。これにより、チーム固有のイベントがあるかどうかが最初にチェックされ、見つからない場合は bot フレームワークのアクティビティハンドラーに渡されます。

Teams activity handler クラスには、2つの主な Teams アクティビティハンドラー `OnConversationUpdateActivityAsync`があります。これは、すべて`OnInvokeActivityAsync`の会話更新アクティビティをルーティングし、すべてのチーム呼び出しアクティビティをルーティングします。

Teams 固有のアクティビティハンドラーのロジックを実装するには、以下の「 [bot ロジック](#bot-logic)」セクションで示されているように、bot でこれらのメソッドをオーバーライドします。 これらの各ハンドラーには基本実装はありません。そのため、オーバーライドに必要なロジックを追加するだけです。

# <a name="javascripttabjavascript"></a>[JavaScript](#tab/javascript)

Microsoft Bot フレームワークを使用して作成された bot と同様に、bot がメッセージアクティビティを受信すると、turn ハンドラーはその受信アクティビティ`onMessage`を認識し、アクティビティハンドラーに送信します。 Teams では、この機能は変わりません。 Bot が会話更新アクティビティを受信した場合、turn ハンドラーはその受信アクティビティを認識して`dispatchConversationUpdateActivity` *teams*アクティビティハンドラーに送信します。これにより、チーム固有のイベントがあるかどうかが最初にチェックされ、見つからない場合は bot フレームワークアクティビティハンドラーに渡されます。

Teams activity handler クラスには、2つの主な Teams アクティビティハンドラー `dispatchConversationUpdateActivity`があります。これは、すべて`onInvokeActivity`の会話更新アクティビティをルーティングし、すべてのチーム呼び出しアクティビティをルーティングします。

Teams 固有のアクティビティハンドラーのロジックを実装するには、以下の「 [bot ロジック](#bot-logic)」セクションに示されているように、bot でこれらのメソッドをオーバーライドします。 これらの各ハンドラーに対して、bot ロジックを定義してから、**必ず最後にを呼び出し`next()` **ます。 呼び出し`next()`により、次のハンドラーが実行されることを確認します。

---

## <a name="bot-logic"></a>Bot ロジック

Bot ロジックは、1つ以上の bot チャネルからの受信アクティビティを処理し、応答で送信アクティビティを生成します。  Teams アクティビティハンドラクラスから派生したボットの場合もあります。これは、最初に Teams アクティビティをチェックし、その他のすべてのアクティビティを bot フレームワークアクティビティハンドラーに渡します。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>コアボットフレームワークハンドラー

以下で説明するすべてのアクティビティハンドラーは、Teams 以外の bot を使用した場合と同じように機能します。ただし、メンバーを*追加*したり、メンバーを*削除*したりすることは例外で、これらはチームのコンテキストでは異なり、メッセージスレッドではなくチームに新しいメンバーが追加されます。

で`ActivityHandler`定義されているハンドラの概要を以下に示します。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したすべてのアクティビティの種類 | `OnTurnAsync` | 受信したアクティビティの種類に基づいて、他のいずれかのハンドラーを呼び出します。 |
| 受信したメッセージアクティビティ | `OnMessageActivityAsync` | アクティビティを`Message`処理するためにオーバーライドします。 |
| 受信した会話の更新アクティビティ | `OnConversationUpdateActivityAsync` | `ConversationUpdate`アクティビティで、会話に参加または残された bot 以外のメンバーがいる場合は、ハンドラーを呼び出します。 |
| Bot 以外のメンバーが会話に参加した | `OnMembersAddedAsync` | 会話に参加しているメンバーを処理するには、このをオーバーライドします。 |
| Bot 以外のメンバーが会話に出た | `OnMembersRemovedAsync` | 会話を残しているメンバーを処理するには、このをオーバーライドします。 |
| 受信したイベントアクティビティ | `OnEventActivityAsync` | `Event`アクティビティで、はイベントの種類に固有のハンドラーを呼び出します。 |
| 受信したトークン応答イベントアクティビティ | `OnTokenResponseEventAsync` | トークン応答イベントを処理するためにオーバーライドします。 |
| トークンに応答しないイベントの処理 | `OnEventAsync` | これをオーバーライドして、他の種類のイベントを処理します。 |
| 受信したその他のアクティビティの種類 | `OnUnrecognizedActivityTypeAsync` | それ以外の処理の種類を処理するには、このオプションを無効にします。 |

#### <a name="teams-specific-handlers"></a>Teams 固有のハンドラー

で`TeamsActivityHandler`は、上のハンドラーの一覧を拡張して、次のものを含めることができます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 作成する Teams チャネルを処理するには、この機能を無効にします。 詳細については、「[スレッド更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[作成されるチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)」を参照してください。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 削除する Teams チャネルを処理するには、この機能を無効にします。 詳細については、「[スレッドの更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[削除されるチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)」を参照してください。|
| channelRenamed 名前変更 | `OnTeamsChannelRenamedAsync` | 名前を変更する Teams チャネルを処理するには、この機能を無効にします。 詳細については、「[スレッドの更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)での[チャネル名の変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)」を参照してください。|
| teamRenamed 名前変更 | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`名前を変更する Teams チームを処理するには、この操作を上書きします。 詳細については、「[スレッドの更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)での[チーム名の変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)」を参照してください。|
| メンバーが追加されました | `OnTeamsMembersAddedAsync` | で`ActivityHandler`メソッド`OnMembersAddedAsync`を呼び出します。 チームに参加するメンバーを処理するには、これをオーバーライドします。 詳細については、「[スレッドの更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)に[チームメンバーが追加されました](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Added)」を参照してください。|
| メンバーの削除 | `OnTeamsMembersRemovedAsync` | で`ActivityHandler`メソッド`OnMembersRemovedAsync`を呼び出します。 チームを離れるメンバーを処理するためにオーバーライドします。 詳細については、「[スレッド更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)での[チームメンバーの削除](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Removed)」を参照してください。|

#### <a name="teams-invoke--activities"></a>Teams がアクティビティを呼び出す

`OnInvokeActivityAsync` _Teams_アクティビティハンドラーから呼び出されたすべての teams アクティビティハンドラーのリストを次に示します。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction. Invoke               | `OnTeamsCardActionInvokeAsync`       | Teams カードアクションの呼び出し。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Teams ファイルの同意を承諾します。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Teams ファイルの同意。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Teams ファイルの同意。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Teams O365 コネクタカードアクション。 |
| サインイン/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Teams サインイン状態を確認します。 |
| タスク/フェッチ                      | `OnTeamsTaskModuleFetchAsync`        | Teams タスクモジュールのフェッチ。 |
| タスク/提出                     | `OnTeamsTaskModuleSubmitAsync`       | Teams タスクモジュール提出。 |

上記の呼び出しアクティビティは Teams の会話のボットに対応しています。 Bot フレームワーク SDK は、メッセージング拡張機能に固有の呼び出しもサポートしています。 詳細について[は、「メッセージング拡張機能に](https://aka.ms/azure-bot-what-are-messaging-extensions)ついて」を参照してください。

# <a name="javascripttabjavascript"></a>[JavaScript](#tab/javascript)

以下で説明するすべてのアクティビティハンドラーは、Teams 以外の bot を使用した場合と同じように動作します。ただし、メンバーを*追加*したり、メンバーを*削除*したりすることは例外です。これらは、メッセージスレッドではなくチームに新しいメンバーが追加されるチームのコンテキストでは異なります。

#### <a name="core-bot-framework-handlers"></a>コアボットフレームワークハンドラー

で`ActivityHandler`定義されているハンドラの概要を以下に示します。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| 受信したすべてのアクティビティの種類 | `onTurn` | 受信したアクティビティの種類に基づいて、他のいずれかのハンドラーを呼び出します。 |
| 受信したメッセージアクティビティ | `onMessage` | `Message`アクティビティを処理するための関数を提供します。 |
| 受信した会話の更新アクティビティ | `onConversationUpdate` | `ConversationUpdate`アクティビティで、会話に参加または残された bot 以外のメンバーがいる場合は、ハンドラーを呼び出します。 |
| Bot 以外のメンバーが会話に参加した | `onMembersAdded` | 会話に参加するメンバーを処理するための関数を提供します。 |
| Bot 以外のメンバーが会話に出た | `onMembersRemoved` | 会話を残しているメンバーを処理するための関数を提供します。 |
| 受信したイベントアクティビティ | `onEvent` | `Event`アクティビティで、はイベントの種類に固有のハンドラーを呼び出します。 |
| 受信したトークン応答イベントアクティビティ | `onTokenResponseEvent` | トークン応答イベントを処理するための関数を提供します。 |
| 受信したその他のアクティビティの種類 | `onUnrecognizedActivityType` | それ以外の処理の種類を処理するための関数を提供します。 |
| アクティビティハンドラーが完了しました | `onDialog` | アクティビティハンドラーの残りの処理が完了した後で、ターンの最後に実行する必要がある処理を処理するための関数を提供します。 |

#### <a name="teams-specific-handlers"></a>Teams 固有のハンドラー

で`TeamsActivityHandler`は、上のハンドラーの一覧を拡張して、次のものを含めることができます。

| イベント | ハンドラー | 説明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 作成する Teams チャネルを処理するには、この機能を無効にします。 詳細については、「[スレッド更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[作成されるチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)」を参照してください。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 削除する Teams チャネルを処理するには、この機能を無効にします。 詳細については、「[スレッドの更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)で[削除されるチャネル](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)」を参照してください。|
| channelRenamed 名前変更 | `OnTeamsChannelRenamedAsync` | 名前を変更する Teams チャネルを処理するには、この機能を無効にします。 詳細については、「[スレッドの更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)での[チャネル名の変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)」を参照してください。 |
| teamRenamed 名前変更 | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`名前を変更する Teams チームを処理するには、この操作を上書きします。 詳細については、「[スレッドの更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)での[チーム名の変更](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)」を参照してください。 |
| メンバーが追加されました | `OnTeamsMembersAddedAsync` | で`ActivityHandler`メソッド`OnMembersAddedAsync`を呼び出します。 チームに参加するメンバーを処理するには、これをオーバーライドします。 詳細については、「[スレッドの更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)に[チームメンバーが追加されました](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Added)」を参照してください。 |
| メンバーの削除 | `OnTeamsMembersRemovedAsync` | で`ActivityHandler`メソッド`OnMembersRemovedAsync`を呼び出します。 チームを離れるメンバーを処理するためにオーバーライドします。 詳細については、「[スレッド更新イベント](https://aka.ms/azure-bot-subscribe-to-conversation-events)での[チームメンバーの削除](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Removed)」を参照してください。 |

#### <a name="teams-invoke-activities"></a>Teams がアクティビティを呼び出す

`onInvokeActivity` _Teams_アクティビティハンドラーから呼び出されたすべての teams アクティビティハンドラーのリストを次に示します。

| 呼び出しの種類                    | ハンドラー                              | 説明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction. Invoke               | `handleTeamsCardActionInvoke`       | Teams カードアクションの呼び出し。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Teams ファイルの同意を承諾します。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Teams ファイルの同意。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Teams ファイルの同意。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Teams O365 コネクタカードアクション。 |
| サインイン/verifyState              | `handleTeamsSigninVerifyState`      | Teams サインイン状態を確認します。 |
| タスク/フェッチ                      | `handleTeamsTaskModuleFetch`        | Teams タスクモジュールのフェッチ。 |
| タスク/提出                     | `handleTeamsTaskModuleSubmit`       | Teams タスクモジュール提出。 |

上記の呼び出しアクティビティは Teams の会話のボットに対応しています。 Bot フレームワーク SDK は、メッセージング拡張機能に固有の呼び出しもサポートしています。 詳細について[は、「メッセージング拡張機能に](https://aka.ms/azure-bot-what-are-messaging-extensions)ついて」を参照してください。

---
