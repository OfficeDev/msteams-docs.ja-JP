---
title: 会議でのアプリTeams前提条件
author: surbhigupta
description: 会議のアプリで前提条件をTeamsする
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: dcfde3136d711d4049060dd59c37e818bdf1a700
ms.sourcegitcommit: 95e0c767ca0f2a51c4a7ca87700ce50b7b154b7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2021
ms.locfileid: "58528783"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>会議でのアプリTeams前提条件

会議のTeamsを使用すると、会議のライフサイクル全体にわたってアプリの機能を拡張できます。 会議のアプリを使用するTeams、次の前提条件を満たす必要があります。

* アプリを開発するTeamsします。 アプリの開発方法の詳細については、「Teams開発[」をTeamsしてください](../overview.md)。

* アプリ マニフェストTeams更新して、アプリが会議で使用できる状態を示します。 詳細については、「アプリ マニフェスト [」を参照してください](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。

* groupchat スコープで構成可能なタブをサポートするアプリを使用します。 詳細については、「グループ チャットスコープ[」と「グループ](../resources/schema/manifest-schema.md#configurabletabs)[タブの作成」を参照してください](../build-your-first-app/build-channel-tab.md)。

* 会議前と会議Teamsの一般的なタブデザインガイドラインに従います。 会議中のエクスペリエンスについては、「会議内タブ」と「会議内ダイアログの設計ガイドライン」を参照してください。 詳細については、「[タブデザイン](../tabs/design/tabs.md)Teams、会議中のタブデザインガイドライン、[](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)および会議中のダイアログデザインガイドライン[」を参照してください](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 会議前 `groupchat` および会議後のチャットでアプリを有効にするスコープをサポートします。 会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、会議前のタスクを実行できます。 会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果やフィードバックなど、会議の結果を表示できます。

* パラメーター 、 `meetingId` および `userId` 会議 API URL `tenantId` を持つ。 パラメーターは、クライアント SDK およびボット アクティビティTeams使用できます。 また、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼 [できる情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。

* 認証トークンを生成するボット登録と ID を `GetParticipant` API に登録します。 詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。

* 会議のイベント アクティビティに基づいてアプリを最新の状態に保つ。 これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。 [会議中] ダイアログ ボックスで、API の完了 `bot Id` パラメーターを確認 `NotificationSignal` します。

* API にボット登録とボット ID を設定 `MeetingDetails` します。 ボット SDK を取得する必要があります `TurnContext` 。

* ボット SDK で使用 `TurnContext` できるオブジェクトについてよく理解してください。 オブジェクト `Activity` には、 `TurnContext` 実際の開始時刻と終了時刻を含むペイロードが含まれます。 リアルタイム会議イベントでは、会議プラットフォームから登録済みのボット ID がTeamsされます。

## <a name="see-also"></a>関連項目

* [会議中のダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teamsの認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [会議のTeamsアプリ](teams-apps-in-meetings.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会議アプリ API の参照](API-references.md)
