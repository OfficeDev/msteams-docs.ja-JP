---
title: Teams 会議でのアプリの前提条件
author: surbhigupta
description: 会議のアプリで前提条件をTeamsする
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 9f5e1ce756dbe465e90e18e6db178b0386ae6d2b
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887700"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Teams 会議でのアプリの前提条件

会議のTeamsを使用すると、会議のライフサイクル全体にわたってアプリの機能を拡張できます。 会議のアプリを使用するTeams、次の前提条件を満たす必要があります。

* アプリを開発するTeamsします。 アプリの開発方法の詳細については、「Teams開発[」をTeamsしてください](../overview.md)。

* アプリ マニフェストTeams更新して、アプリが会議で使用できる状態を示します。 詳細については、「アプリ マニフェスト [」を参照してください](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。

* groupchat スコープで構成可能なタブをサポートするアプリを使用します。 詳細については、「グループ チャットスコープ[」と「グループ](../resources/schema/manifest-schema.md#configurabletabs)[タブの作成」を参照してください](../build-your-first-app/build-channel-tab.md)。

* 会議前および会議Teamsの一般的なタブデザインガイドラインに従います。 会議中のエクスペリエンスについては、「会議内タブ」と「会議内ダイアログの設計ガイドライン」を参照してください。 詳細については、「[タブデザイン](../tabs/design/tabs.md)Teams、会議中のタブデザインガイドライン、[](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)および会議中のダイアログデザインガイドライン[」を参照してください](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 会議前 `groupchat` および会議後のチャットでアプリを有効にするスコープをサポートします。 会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、会議前のタスクを実行できます。 会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果や料金など、会議の結果を表示できます。
* 会議 API の URL パラメーターには、、 `meetingId` 、 `userId` および を指定する必要があります `tenantId` 。 パラメーターは、クライアント SDK およびボット アクティビティTeams使用できます。 また、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼 [できる情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。

* 認証 `GetParticipant` トークンを生成するには、API にボット登録と ID が必要です。 詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。 これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。 [会議内] ダイアログ ボックスについては、「API の完了 `bot Id` パラメーター」を参照 `NotificationSignal` してください。

* `Meeting Details`API にはボット登録とボット ID が必要です。 ボット SDK を取得する必要があります `TurnContext` 。

* リアルタイムの会議イベントの場合は、ボット SDK で使用できる `TurnContext` オブジェクトに精通している必要があります。 オブジェクト `Activity` には、 `TurnContext` 実際の開始時刻と終了時刻を含むペイロードが含まれます。 リアルタイム会議イベントでは、会議プラットフォームから登録済みのボット ID がTeamsされます。

* パラメーター 、 `meetingId` および `userId` 会議 API URL `tenantId` を持つ。 パラメーターは、クライアント SDK およびボット アクティビティTeams使用できます。 また、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼 [できる情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。

* 認証トークンを生成するボット登録と ID を `GetParticipant` API に登録します。 詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。

* 会議のイベント アクティビティに基づいてアプリを最新の状態に保つ。 これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。 [会議中] ダイアログ ボックスで、API の完了 `bot Id` パラメーターを確認 `NotificationSignal` します。

* API にボット登録とボット ID を設定 `MeetingDetails` します。 ボット SDK を取得する必要があります `TurnContext` 。

* ボット SDK で使用 `TurnContext` できるオブジェクトについてよく理解してください。 オブジェクト `Activity` には、 `TurnContext` 実際の開始時刻と終了時刻を含むペイロードが含まれます。 リアルタイム会議イベントでは、会議プラットフォームから登録済みのボット ID がTeamsされます。

前提条件を満たした後で、会議アプリ API リファレンス 、を使用すると、属性を使用して情報にアクセスし、関連するコンテンツ `GetUserContext` `GetParticipant` `NotificationSignal` `Meeting Details` を表示できます。

> [!NOTE]
> Teams会議 _のサイド_ パネルで SSO が機能する JavaScript SDK (バージョン : 1.10 以降)。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [会議アプリ API リファレンス](API-references.md)

## <a name="see-also"></a>関連項目

* [会議中のダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teamsの認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [会議のTeamsアプリ](teams-apps-in-meetings.md)
* [Teamsまたはチャット メンバーをフェッチするボット API の変更を確認する](~/resources/team-chat-member-api-changes.md)
