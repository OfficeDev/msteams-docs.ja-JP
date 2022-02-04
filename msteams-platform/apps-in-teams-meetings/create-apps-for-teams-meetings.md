---
title: Teams 会議でのアプリの前提条件
author: surbhigupta
description: 会議のアプリで前提条件をTeamsする
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 4c42a66f7891691b8c53d61d1ce637d57048eae8
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2022
ms.locfileid: "62362740"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Teams 会議でのアプリの前提条件

会議のTeamsを使用すると、会議のライフサイクル全体にわたってアプリの機能を拡張できます。 会議のアプリを使用するTeams、次の前提条件を満たす必要があります。

* アプリを開発するTeamsします。 アプリの開発方法の詳細については、「Teams開発」[Teams参照してください](../overview.md)。

* アプリ マニフェストTeams更新して、アプリが会議で使用できる状態を示します。 詳細については、「アプリ マニフェスト [」を参照してください](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。

* groupchat スコープで構成可能なタブをサポートするアプリを使用します。 詳細については、「グループ チャットスコープ [」と「グループ](../resources/schema/manifest-schema.md#configurabletabs) [タブの作成」を参照してください](../build-your-first-app/build-channel-tab.md)。

* 会議前および会議Teamsの一般的なタブデザインガイドラインに従います。 会議中のエクスペリエンスについては、「会議内タブ」と「会議内ダイアログの設計ガイドライン」を参照してください。 詳細については、「タブデザイン[Teams](../tabs/design/tabs.md)、会議中のタブデザインガイドライン、[](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)および会議中のダイアログデザインガイドライン[」を参照してください](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 会議前 `groupchat` および会議後のチャットでアプリを有効にするスコープをサポートします。 会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、会議前のタスクを実行できます。 会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果や料金など、会議の結果を表示できます。
* 会議 API の URL パラメーターには、、 `meetingId`、および を `userId`指定する必要があります `tenantId`。 パラメーターは、クライアント SDK およびボット アクティビティTeams使用できます。 また、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼 [できる情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。

* 認証 `GetParticipant` トークンを生成するには、API にボット登録と ID が必要です。 詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。 これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。 [会議内] ダイアログ ボックスについては、「API の完了パラメーター `bot Id` 」を参照 `NotificationSignal` してください。

* API には `Meeting Details` ボット登録とボット ID が必要です。 ボット SDK を取得する必要があります `TurnContext`。 会議の詳細 API を使用するには、プライベート会議やチャネル会議など、会議の範囲に基づいて異なる RSC アクセス許可を取得する必要があります。

* リアルタイムの会議イベントの場合は、 `TurnContext` ボット SDK で使用できるオブジェクトに精通している必要があります。 オブジェクト `Activity` には、 `TurnContext` 実際の開始時刻と終了時刻を含むペイロードが含まれます。 リアルタイム会議イベントでは、会議プラットフォームから登録済みのボット ID がTeamsされます。 ボットは、マニフェストに追加することで、会議の開始イベントまたは終了イベントを自動的 `ChannelMeeting.ReadBasic.Group` に受信できます。

* パラメーター 、および`meetingId``userId`会議 `tenantId` API URL を持つ。 パラメーターは、クライアント SDK およびボット アクティビティTeams使用できます。 また、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼 [できる情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。

* 認証トークンを生成するボット登録と `GetParticipant` ID を API に登録します。 詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。

* 会議のイベント アクティビティに基づいてアプリを最新の状態に保つ。 これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。 [会議中] ダイアログ ボックスで、API の完了パラメーターを `bot Id` 確認 `NotificationSignal` します。

* API にボット登録とボット ID を設定 `MeetingDetails` します。 ボット SDK を取得する必要があります `TurnContext`。

* ボット SDK で使用できる `TurnContext` オブジェクトについてよく理解してください。 オブジェクト `Activity` には、 `TurnContext` 実際の開始時刻と終了時刻を含むペイロードが含まれます。 リアルタイム会議イベントでは、会議プラットフォームから登録済みのボット ID がTeamsされます。

前提条件を満たした後で、会議アプリ API `GetUserContext`リファレンス 、`GetParticipant``NotificationSignal``Meeting Details`を使用すると、属性を使用して情報にアクセスし、関連するコンテンツを表示できます。

> [!NOTE]
> Teamsサイド _パネルで SSO_ が機能する JavaScript SDK (バージョン: 1.10 以降) を使用します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [会議で使用するアプリを有効Teamsする](enable-and-configure-your-app-for-teams-meetings.md)

## <a name="see-also"></a>関連項目

* [会議中のダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teamsの認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [Teams 会議用アプリ](teams-apps-in-meetings.md)
* [Teamsまたはチャット メンバーをフェッチするボット API の変更を確認する](~/resources/team-chat-member-api-changes.md)
