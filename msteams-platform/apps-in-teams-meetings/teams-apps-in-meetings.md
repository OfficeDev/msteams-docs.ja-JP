---
title: Teams 会議のアプリ
author: laujan
description: 参加者とユーザーの役割に基づく Teams 会議のアプリの概要
ms.topic: overview
ms.author: lajanuar
keywords: Teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: 217737cbbf73104d4d78cf817e6df0244229c53c
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797758"
---
# <a name="apps-in-teams-meetings"></a>Teams 会議のアプリ

会議は、Teams の生産性の鍵です。 共同作業、パートナーシップ、情報に基づいたコミュニケーション、包括的でアクティブなフォーラムでのフィードバックの共有を可能にします。 開発者は、構成可能なタブ、ボット、[](../bots/what-are-bots.md)およびメッセージ拡張[](../messaging-extensions/what-are-messaging-extensions.md)アプリケーションを作成して、Teams の会議エクスペリエンスを強化および強化できます。 [](../tabs/what-are-tabs.md#how-do-tabs-work) 会議ユーザーは、タブ ギャラリーを介してアプリにアクセスして、カンバボードの事前設定、会議内の操作可能なダイアログの起動、会議後の投票の作成などの関連シナリオを有効にできます。 会議アプリは、出席者の状態に基づいて、会議のライフサイクルの各段階でユーザー エクスペリエンスを提供できます。

Teams の会議アプリの拡張性は、次の 3 つの概念を中心に行います。

✔ **のライフサイクル (会議** の時間枠の前、中、および後) を管理します。  
✔ **参加者の役割** — 会議の開催者、発表者、または出席者。  
✔ **ユーザーの種類** — テナント内、ゲスト、フェデレーション、または匿名の Teams ユーザー。

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a>会議ライフサイクルのシナリオ

## <a name="tabs"></a>タブ

> [!IMPORTANT]
> すべてのタブ アプリケーションと同様に、アプリはタブの Teams [SSO](../tabs/how-to/authentication/auth-aad-sso.md) 認証フローに従う必要があります。

> [!NOTE]
> モバイル クライアントは、会議前サーフェスと会議後サーフェスでのみタブをサポートします。 モバイルでの会議中のエクスペリエンス (会議中のダイアログとパネル) は間もなく利用可能になります。

### <a name="pre-meeting-app-experience"></a>会議前アプリのエクスペリエンス

**会議前のエクスペリエンス:**

![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

**[会議前] タブ:**

![会議前タブ ビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔アクセス許可を持つユーザーは、次の 2 つの方法でタブ ギャラリーを介して会議にアプリを追加できます。

&emsp;&emsp;&#9679; Teams のスケジュール **フォームの** [詳細] タブを使用します。

&emsp;&emsp;&#9679;既存の会議の **[会議チャット** ] タブを使用します。</br> </br>

✔タブ アプリは、プラスアイコン (➕)ボタンを使用して会議の [詳細] ページと [チャット] ページでアクセスできます。| 

✔投票またはアンケートが 10 件を超える場合、タブ レイアウトは整理された状態である必要があります。

### <a name="in-meeting-app-experience"></a>会議中アプリのエクスペリエンス

✔アプリは、チャット ウィンドウの上部バーにホストされ、会議内タブから会議内タブエクスペリエンスとしてホストされます。ユーザーがタブ ギャラリーを使用して会議にタブを追加すると、会議のエクスペリエンス中のアプリが表示されます。

✔アクセス許可を持つユーザーは、会議中にアプリを追加できます。

✔会議のコンテキストで読み込まれると、アプリは Teams クライアント SDK を利用して、エクスペリエンスにアクセスし、適切にレンダリング `meetingId` `userMri` `frameContext` することができます。

✔または投票の結果をエクスポートする場合は、ユーザーに "結果が正常にダウンロードされました" と通知する必要があります。

✔ Teams 会議にアプリを表示するには、次の 2 つの領域を使用します。

&emsp;&emsp;&#9679; **パネル**。 </br>

> [!NOTE]
> アプリ マニフェスト _で、_ タブがサイド パネル [](create-apps-for-teams-meetings.md#during-a-meeting)用に最適化されている場合、それが表示されます。 また、指定された設計ガイドラインに従って、共有トレイ エクスペリエンスの一部にできます。

&emsp;&emsp;&#9679; **ダイアログを表示します**。 会議内ダイアログを使用して、会議参加者の操作可能なコンテンツを表示します。 *「Teams* [会議用アプリの作成」を参照してください](create-apps-for-teams-meetings.md)。

**会議中のエクスペリエンス:**

![会議内エクスペリエンス](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会議内ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog.png)

**ユーザーの会議中の操作可能なダイアログ:**

![ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>会議後のアプリエクスペリエンス

**会議後のエクスペリエンス:**

![会議後ビュー](../assets/images/apps-in-meetings/PostMeeting.png)

✔会議後のアプリのシナリオは、現在の会議後のエクスペリエンスと似ていますが、サーフェス内にタブが存在するという利点があります。 

✔アクセス許可を持つユーザーは、Teams のスケジュール フォームの [詳細] タブと既存の会議の [会議チャット] タブを使用して、タブ ギャラリーから会議にアプリを追加できます。

✔投票またはアンケートが 10 件を超える場合、タブ レイアウトは整理された状態である必要があります。

### <a name="bots"></a>ボット

ボットの実装については、Teams 会議のドキュメント [のボットを参照](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) してください。

### <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージング拡張機能の実装については、Teams 会議のドキュメントの [メッセージング拡張機能を参照](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) してください。

## <a name="participant-roles-and-user-types-in-a-meeting"></a>会議の参加者の役割とユーザーの種類

![会議の参加者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>参加者の役割

参加者固有の承認を使用してアプリを設計できます。 たとえば、開催者や発表者だけが会議で投票を作成できるとします。 既定の参加者設定は組織の IT 管理者によって決まりますが、会議の開催者は特定の会議の設定を変更できます。 開催者は、会議オプション Web ページでこれらの変更を行えます。

1. **開催者**。 開催者が会議をスケジュールし、会議オプションを設定し、会議の役割を割り当て、会議を開始します。 M365 アカウント (Teams ライセンスを所有) を持つユーザーだけが開催者になされ、出席者のアクセス許可を制御できます。
1. **発表者**。 発表者の機能は開催者とほぼ同じです。ただし、発表者は、セッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。 既定では、会議に参加する参加者は発表者の役割を持っています。
1. **Attendee**. 出席者とは、会議に招待されているが、発表者として機能する権限が与えされていないユーザーです。 出席者は他の会議メンバーと対話できますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。

 [ **「Teams 会議での役割」を参照**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

[会議オプション]  **ページには、次** のようにアクセスできます。

&#11200; Teams で、[予定表のロゴ] に移動し、会議を選択して、[会議オプション] ![ ](../assets/images/apps-in-meetings/calendar-logo.png) **を選択します**。

&#11200;会議出席依頼で、[会議オプション] **を選択します**。

&#11200;会議中に、会議コントロールの **[参加者** に参加者 ![ を表示する] ](../assets/images/apps-in-meetings/show-participants.png) アイコンを選択します。 次に、参加者の一覧の上で、[アクセス許可の管理 **] を選択します**。

### <a name="user-types"></a>ユーザーの種類

> [!NOTE]
> ユーザーの種類は会議に参加し、上記の参加者の役割のいずれかを想定できます。 ユーザーの種類は **、getParticipantRole** API の一部として公開されません。

1. **テナント内。** これらのユーザーは組織に属し、テナントの Azure Active Directory の資格情報を持っています。 通常、フルタイム、オンサイト、またはリモートの従業員です。
1. **ゲスト 。** ゲストとは、Teams または組織のテナント内の他のリソースにアクセスするために招待された別の組織の参加者です。 ゲストは組織の Active Directory に追加され、チーム チャット、会議、ファイルにフル アクセスできるネイティブ チーム メンバーと同じ Teams 機能をほぼすべて提供できます。  [Microsoft Teams でのゲスト アクセスを確認する](/microsoftteams/guest-access)
1. **フェデレーション/外部**。 フェデレーション ユーザーとは、会議への参加を招待された別の組織の外部 Teams ユーザーです。 これらのユーザーはフェデレーション パートナーとの有効な資格情報を持つので、Teams によって認証済みとして扱われるが、チームや組織の他の共有リソースにアクセスできない。 外部ユーザーにチームとチャネルへのアクセスを許可する場合は、ゲスト アクセスの方が優れたオプションである可能性があります。 _「Microsoft_ [Teams での外部アクセスの管理」を参照](/microsoftteams/manage-external-access)
1. **匿名**。 匿名ユーザーは Active Directory ID を持ち、テナントとフェデレーションされません。 匿名参加者は外部ユーザーに似たユーザーですが、その ID は会議に投影されません。 匿名ユーザーは、会議ウィンドウでアプリにアクセスできます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [アプリをデザインする](create-apps-for-teams-meetings.md)
> [!div class="nextstepaction"]
> [アプリを作成する](create-apps-for-teams-meetings.md)
