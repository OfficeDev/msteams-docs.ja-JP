---
title: Teams 会議のアプリ
author: laujan
description: 参加者とユーザーの役割に基づく Teams 会議のアプリの概要
ms.topic: overview
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: 13fc44e9831cf58f0ab847eab06cc5b99ed8cc70
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796226"
---
# <a name="apps-in-teams-meetings-developer-preview"></a>Teams 会議のアプリ (開発者プレビュー)

>[!IMPORTANT]
> Microsoft Teams の開発者プレビューに含まれる機能は、すぐにアクセス、テスト、フィードバック目的のみに提供されています。 公開リリースで利用できるようになる前に変更が行われ、運用アプリケーションでは使用できません。

会議は、Teams の生産性にとって重要です。 このツールを使用すると、包括的でアクティブなフォーラムで、コラボレーション、パートナーシップ、情報を伝えるコミュニケーション、および共有フィードバックを行うことができます。 開発者は、 [構成可能なタブ](../tabs/what-are-tabs.md#how-do-tabs-work)、 [ボット](../bots/what-are-bots.md)、および [メッセージ拡張](../messaging-extensions/what-are-messaging-extensions.md) アプリケーションを作成して、Teams の会議環境を強化し、充実させることができます。 会議ユーザーは、タブギャラリーを使用してアプリにアクセスし、かんばんボードの事前ステージング、会議中のアクション可能なダイアログの開始、会議後の投票の作成など、関連するシナリオを有効にすることができます。 会議アプリは、出席者の状態に基づいて、会議のライフサイクルの各段階でユーザー環境を提供できます。

Teams のアプリの拡張機能センターは3つの概念に基づいています。

会議の **ライフサイクル** の✔ (会議の時間枠の前、前後、および後)。  
✔ **参加者の役割** —会議の開催者、発表者、または出席者。  
✔ **ユーザーの種類** -テナント、ゲスト、フェデレーション、または匿名 Teams ユーザー。

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a>会議のライフサイクルのシナリオ

## <a name="tabs"></a>タブ

> [!IMPORTANT]
> すべてのタブアプリケーションと同様に、アプリは、タブの Teams [SSO 認証フロー](../tabs/how-to/authentication/auth-aad-sso.md) に従う必要があります。

> [!NOTE]
> モバイルクライアントは、会議のプレおよびポストの表面でのみタブをサポートします。 モバイルでの会議中のエクスペリエンス (会議中のダイアログとパネル) は近日中に利用できるようになります。

### <a name="pre-meeting-app-experience"></a>ミーティング前アプリの作業

**ミーティング前の環境:**

![ミーティング前の環境](../assets/images/apps-in-meetings/PreMeeting.png)

**[会議前] タブ:**

![会議前のタブビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔権限ユーザーは、次の2つの方法で、タブギャラリーを使用して会議にアプリを追加できます。

&emsp;&emsp; Teams スケジュールフォームの [ **詳細** ] タブを使用して&#9679; します。

&emsp;&emsp; 既存の会議の [ミーティングの **チャット** ] タブを使用して&#9679; します。</br> </br>

✔タブアプリは、プラスアイコン (➕) ボタンを使用して、会議の **詳細** と **チャット** ページからアクセスできます。 |

### <a name="in-meeting-app-experience"></a>会議中のアプリ環境

✔ Meeting アプリは、[会議中] タブを使用して、チャットウィンドウの上部上のバーと、会議のタブ操作としてホストされます。ユーザーがタブギャラリーを使用して会議にタブを追加すると、 **会議** のエクスペリエンス中のアプリが表示されます。

✔権限ユーザーは、会議中にアプリを追加できます。

✔会議のコンテキストでロードされた場合、アプリは Teams クライアント SDK を活用して、にアクセス `meetingId` し、を `userMri` 適切に表示することができ `frameContext` ます。

アプリの✔は、次の2つの領域で Teams 会議に表示できます。

&emsp;&emsp;&#9679; **サイドパネル** 。 </br>

> [!NOTE]
> アプリの _マニフェスト_ で、タブが [サイドパネル用に最適化](create-apps-for-teams-meetings.md#in-meeting)されていることが指定されている場合は、それが表示されます。 また、この機能は、指定された設計ガイドラインに従って、共有トレイの環境の一部にすることもできます。

&emsp;&emsp;&#9679; **会議中] ダイアログ** 。 会議中のダイアログを使用して、会議の参加者に対して操作可能なコンテンツを示します。 「 [Teams 会議用アプリの作成」を](create-apps-for-teams-meetings.md)*参照してください* 。

**ミーティング中の環境:**

![会議中の作業](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会議中のダイアログ表示](../assets/images/apps-in-meetings/in-meeting-dialog.png)

**ユーザーに対する会議中のアクション可能なダイアログ:**

![ダイアログビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>ミーティング後のアプリの作業

**ミーティング後の環境:**

![投稿会議の表示](../assets/images/apps-in-meetings/PostMeeting.png)

ミーティング後のアプリのシナリオは、現在の会議の後の状態と似ています。これには、タブが表面内に存在するという利点があります。 権限ユーザーは、[チームのスケジュール] フォームの [ **詳細** ] タブと既存の会議の [会議 **チャット** ] タブを使用して、タブギャラリーからアプリケーションを会議に追加できます。

### <a name="bots"></a>ボット

Bot 実装の場合は、 [Teams の会議のドキュメントでボット](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) を参照してください。

### <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージング拡張機能の実装については、「 [Teams 会議のドキュメント」の「メッセージング拡張機能](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) 」を参照してください。

## <a name="participant-roles-and-user-types-in-a-meeting"></a>会議での参加者の役割とユーザーの種類

![会議の参加者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>参加者の役割

参加者固有の承認を使用してアプリを設計できます。 たとえば、開催者または発表者のみが会議で投票を作成できるとします。 既定の参加者設定は組織の IT 管理者によって決定されますが、会議の開催者は特定の会議の設定を変更することをお勧めします。 開催者は、会議オプション web ページでこれらの変更を行うことができます。

1. **開催者** 。 開催者が会議をスケジュールし、会議オプションを設定し、会議の役割を割り当て、会議を開始します。 M365 アカウント (Teams ライセンスを所有) を持つユーザーのみが、開催者と参加者のアクセス許可を管理できます。
1. **プレゼンター** 。 プレゼンターには開催者とほぼ同じ機能があります。ただし、発表者はセッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。 既定では、会議に参加する参加者には発表者の役割が割り当てられます。
1. **出席者** 。 出席者は、会議への参加を招待されているが、発表者としての権限を持っていないユーザーです。 出席者が他の会議メンバーと対話することはできますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。

_See_ [ **Teams 会議でのロールの** 表示](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

[  **会議オプション** ] ページには、次のようにアクセスできます。

&#11200; Teams で、 **予定** 表の予定表のロゴに移動し、 ![ 会議を選択し ](../assets/images/apps-in-meetings/calendar-logo.png) てから、[ **会議のオプション** ] をクリックします。

会議出席依頼の &#11200; で、[ **会議オプション** ] を選択します。

会議中に &#11200; は、[ **参加者** に参加者を表示する ![ ] アイコンをミーティングのコントロールに選択し ](../assets/images/apps-in-meetings/show-participants.png) ます。 次に、参加者のリストの上にある [ **権限の管理** ] を選択します。

### <a name="user-types"></a>ユーザーの種類

> [!NOTE]
> ユーザーの種類は会議に参加でき、前述の参加者の役割の1つを引き受けます。 ユーザーの種類は、 **getParticipantRole** API の一部として公開されません。

1. **テナント内** 。 これらのユーザーは組織に属しており、テナントの Azure Active Directory に資格情報を持っています。 通常は、フルタイム、オンサイト、またはリモートの従業員です。
1. **ゲスト** 。 ゲストは、組織のテナント内の Teams またはその他のリソースへのアクセスを招待された別の組織からの参加者です。 ゲストは組織の Active Directory に追加され、チームのチャット、会議、およびファイルへのフルアクセスを備えたネイティブのチームメンバーと同じ Teams の機能をほぼすべて提供できます。 [Microsoft Teams でのゲストアクセスを](/microsoftteams/guest-access)_参照してください_ 。
1. **フェデレーション/外部** 。 フェデレーションユーザーは、会議への参加を招待された別の組織の外部 Teams ユーザーです。 これらのユーザーは、フェデレーションパートナーとの間に有効な資格情報を持っているため、これらのユーザーは Teams によって認証されたものとして扱われますが、組織からチームや他の共有リソースにアクセスすることはできません。 外部ユーザーが teams やチャネルにアクセスできるようにする場合は、ゲストアクセスの方が適していることがあります。 「 [Microsoft Teams で外部アクセスを管理](/microsoftteams/manage-external-access)する _」を参照してください_ 。
1. **匿名** 。 匿名ユーザーは、Active Directory id を持たず、テナントと共にフェデレーションされません。 匿名の参加者は外部ユーザーのようになりますが、その id は会議に投影されません。 匿名ユーザーは、会議ウィンドウでアプリにアクセスできません。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [Teams 会議用のアプリを作成する](create-apps-for-teams-meetings.md)
