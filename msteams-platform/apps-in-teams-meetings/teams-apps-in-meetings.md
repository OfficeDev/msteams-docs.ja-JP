---
title: Teams 会議用アプリ
author: surbhigupta
description: この記事では、参加者とユーザーロールとアプリの拡張性に基づいて、Microsoft Teams 会議でのアプリのしくみについて説明します。
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: f253a4ca3d09e48f99df36fdcb77bdd740fab5ff
ms.sourcegitcommit: bb15ce26cd65bec90991b703069424ab4b4e1a61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2022
ms.locfileid: "68772273"
---
# <a name="apps-for-teams-meetings-and-calls"></a>Teams 会議と通話用アプリ

会議ではコラボレーション、パートナーシップ、事前に連携された十分な情報に基づくコミュニケーション、及びフィードバックの共有が可能です。 会議スペースは、会議ライフサイクルの各ステージのユーザー エクスペリエンスを提供できます。 次の図は、会議アプリの拡張機能のアイデアを示しています。

:::image type="content" source="../assets/images/apps-in-meetings/meetingappextensibility.png" alt-text="このスクリーンショットは、会議アプリの機能拡張のしくみを示しています。":::

Microsoft Teams でアプリを使用してカスタム会議エクスペリエンスを作成するには、次の製品の概念に精通している必要があります。

## <a name="supported-meeting-types-in-teams"></a>Teams でサポートされている会議の種類

Teams では、次の種類の会議で会議中にアプリへのアクセスがサポートされます。

* [**スケジュールされた会議**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop): Teams 予定表を使用してスケジュールされた会議。
* [**スケジュールされたチャネル会議**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop): Teams パブリック チャネルを介してスケジュールされた会議。
* [**1 対 1 の呼び出し**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798): 1 対 1 のチャットで開始された呼び出し。
* グループ通話: グループ チャットで開始された呼 [**び出し**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798)。
* [**インスタント会議**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5): Teams 予定表の [ **今すぐ会議** ] ボタンを使用して開始された会議。
* [**ウェビナー: [**](https://support.microsoft.com/office/get-started-with-teams-webinars-42f3f874-22dc-4289-b53f-bbc1a69013e3)**新しい会議**] ドロップダウンの [ウェビナー] ボタンを使用して開始された **ウェビナー**。

[Teams 会議、有効期限とポリシー、](/MicrosoftTeams/meeting-expiration)[会議、ウェビナー、ライブ イベント](/microsoftteams/quick-start-meetings-live-events)の詳細について説明します。
> [!NOTE]
>
> * スケジュールされたパブリック チャネル会議のアプリは、現在、 [パブリック開発者プレビュー](../resources/dev-preview/developer-preview-intro.md)でのみ使用できます。
> * アプリは、次ではサポートされていません。
>   * [公衆交換電話網 (PSTN) Teams 通話](/microsoftteams/cloud-voice-landing-page#public-switched-telephone-network-connectivity-options)
>   * [エンドツーエンドの暗号化された Teams 呼び出し](https://support.microsoft.com/office/use-end-to-end-encryption-for-teams-calls-1274b4d2-b5c5-4b24-a376-606fa6728a90)
>   * [インスタント チャネル会議](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5)
>   * [共有チャネル](https://support.microsoft.com/office/what-is-a-shared-channel-in-teams-e70a8c22-fee4-4d6e-986f-9e0781d7d11d)での会議

## <a name="meeting-lifecycle"></a>会議のライフサイクル

会議ライフサイクルには、Teams 会議でのユーザーの種類とユーザーの役割に応じて、会議前、会議中、会議後のアプリ エクスペリエンスが含まれます。

## <a name="user-types-in-teams"></a>Teams のユーザーの種類

Teams では、Teams 会議のテナント内、ゲスト、フェデレーションユーザー、外部ユーザーなどのユーザーの種類がサポートされています。 各ユーザーの種類には、 [Teams 会議のユーザー ロール](#user-roles-in-teams-meeting)のいずれかを指定できます。

> [!NOTE]
>
> 現在、3 人目が 1 対 1 の呼び出しに追加されると、新しいセッションが開始されることを意味するグループ呼び出しに昇格されます。 1 対 1 の呼び出しに追加されたアプリは、グループ呼び出しでは使用できません。 ただし、再度追加することもできます。

次の一覧では、さまざまなユーザーの種類とそのアクセシビリティについて詳しく説明します。

* **テナント内**: テナント内ユーザーは組織に属し、テナントの Azure Active Directory (AAD) に資格情報を持っています。 彼らはフルタイム、オンサイト、またはリモートの従業員です。 テナント内ユーザーには、開催者、発表者、または出席者を指定できます。
* **ゲスト: ゲスト** は、組織のテナント内の Teams またはその他のリソースにアクセスするために招待された別の組織の参加者です。 ゲストは組織の Azure AD に追加され、ネイティブ チーム メンバーと同じ Teams 機能を持ちます。 チーム チャット、会議、ファイルにアクセスできます。 ゲストには、開催者、発表者、または出席者を指定できます。 詳細については、「 [Teams でのゲスト アクセス](/microsoftteams/guest-access)」を参照してください。
* **フェデレーションまたは外部**: フェデレーションユーザーまたは外部ユーザーは、会議に参加するために招待された別の組織の Teams ユーザーです。 フェデレーション ユーザーは、フェデレーション パートナーとの有効な資格情報を持ち、Teams によって承認されます。 Teams や組織の他の共有リソースにアクセスすることはできません。 ゲスト アクセスは、外部ユーザーが Teams とチャネルにアクセスできる優れたオプションです。 詳細については、「 [Teams での外部アクセスの管理](/microsoftteams/manage-external-access)」を参照してください。

    > [!NOTE]
    > Teams ユーザーは、会議や他の組織とのチャットをホストするときにアプリを追加できます。 外部ユーザーが会議にアプリを共有すると、すべてのユーザーがアプリにアクセスできます。 ホスト組織のデータ ポリシーと、そのユーザーの組織が共有するサード パーティ製アプリのデータ共有プラクティスが有効になります。

* **匿名**: 匿名ユーザーには Azure AD ID がなく、テナントとフェデレーションされていません。 匿名の参加者は外部ユーザーに似ていますが、その ID は会議に表示されません。 匿名ユーザーは会議ウィンドウでアプリにアクセスできません。 匿名ユーザーは、会議チャットでボットのロゴを表示できません。 匿名ユーザーは発表者または出席者にすることができますが、開催者にすることはできません。

    > [!NOTE]
    > 匿名ユーザーは、グローバル既定のユーザー レベルのアプリアクセス許可ポリシーを継承します。 詳細については、「アプリの [管理](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)」を参照してください。

## <a name="user-roles-in-teams-meeting"></a>Teams 会議のユーザー ロール

Teams 会議のユーザー ロールを次に示します。

* **開催者**: 開催者は会議をスケジュールし、会議オプションを設定し、会議の役割を割り当て、出席者のアクセス許可を制御し、会議を開始します。 Microsoft 365 アカウントと Teams ライセンスを持つユーザーのみが開催者にできます。 会議の開催者は、[ [**会議オプション** ] ページ](https://support.microsoft.com/en-us/office/change-participant-settings-for-a-teams-meeting-53261366-dbd5-45f9-aae9-a70e6354f88e)から特定の会議の設定を変更できます。

* **発表者**: 会議の発表者は、開催者と同様の機能を持ちます。ただし、開催者をセッションから削除し、セッションの会議オプションを変更する場合を除きます。

* **出席者**: 出席者は、会議に出席するように招待されたユーザーです。 会議中の出席者の機能は限られています。

> [!NOTE]
> アプリを追加、削除、またはアンインストールできるのは、開催者または発表者のみです。

詳細については、「[Teams 会議での役割](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。

> [!TIP]
>
> * [既定の参加者設定](/microsoftteams/meeting-policies-participants-and-guests)は、組織の IT 管理者によって決定されます。既定の設定に従って、会議に参加する参加者には発表者の役割があります。
> * 発表者ロールは、1 対 1 の呼び出しでは使用できません。
> * チャットからグループ通話を開始するユーザーは、開催者と見なされます。

> [!IMPORTANT]
>
> * 現在、サード パーティ製アプリは Government Community Cloud (GCC) で使用できますが、GCC-Highおよび国防総省 (DOD) テナントでは使用できません。
> * GCC では、サード パーティ製アプリは既定で無効になっています。 GCC のサード パーティ製アプリを有効にするには、「[アプリのアクセス許可ポリシーを管理する](/microsoftteams/teams-app-permission-policies)」と「[アプリの管理](/microsoftteams/manage-apps)」を参照してください。

## <a name="see-also"></a>関連項目

* [Microsoft Teams 会議拡張機能の設計](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [会議用のビルド タブ](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Teams 会議ステージ用のアプリを構築する](build-apps-for-teams-meeting-stage.md)
* [会議チャット用の拡張可能な会話を構築する](build-extensible-conversation-for-meeting-chat.md)
* [匿名ユーザー向けのアプリを構築する](build-apps-for-anonymous-user.md)
* [会議アプリ API](meeting-apps-apis.md)
* [Live Share SDK による強化されたコラボレーション](teams-live-share-overview.md)
* [カスタム Together モード シーン](~/apps-in-teams-meetings/teams-together-mode.md)
