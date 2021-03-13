---
title: Teams 会議のアプリ
author: laujan
description: 参加者とユーザーの役割に基づく Teams 会議のアプリの概要
ms.topic: overview
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 51fe2e0ebdaa56197bbebd1e5dbcf90698fb1f92
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753554"
---
# <a name="apps-in-teams-meetings"></a>Teams 会議のアプリ

会議は Teams の生産性の重要なポイントです。 包括的でアクティブなフォーラムで、コラボレーション、パートナーシップ、情報に基づいたコミュニケーション、共有フィードバックを有効にします。 開発者は、Teams 会議のエクスペリエンスを強化[](../bots/what-are-bots.md)し、強化[](../messaging-extensions/what-are-messaging-extensions.md)するために、構成可能なタブ、ボット、およびメッセージ拡張アプリケーションを作成できます。 [](../tabs/what-are-tabs.md#how-do-tabs-work) 会議ユーザーは、タブ ギャラリーを介してアプリにアクセスして、かんばんボードの事前ステージング、会議中の操作可能なダイアログの起動、会議後のポーリングの作成など、関連するシナリオを有効にできます。 会議アプリは、出席者の状態に基づいて、会議ライフサイクルの各ステージのユーザー エクスペリエンスを提供できます。

Teams の会議アプリの機能拡張は、次の 3 つの概念を中心に行います。

**✔、会議の時間の** 前、中、および後の会議のライフサイクルを設定します。  
✔ **参加者の役割** - 会議の開催者、発表者、または出席者。  
✔ **ユーザーの種類** ( テナント内、ゲスト、フェデレーション、または匿名の Teams ユーザー)。

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a>会議のライフサイクル シナリオ

## <a name="tabs"></a>タブ

> [!IMPORTANT]
> すべてのタブ アプリケーションと同様に、アプリはタブの Teams [SSO 認証フローに従う](../tabs/how-to/authentication/auth-aad-sso.md) 必要があります。

> [!NOTE]
> * モバイル クライアントは、会議前および会議後のサーフェスでのみタブをサポートします。 会議中のダイアログやモバイル上のパネルなどの会議中のエクスペリエンスは、近日利用可能になります。
> * アプリは、プライベートスケジュールされた会議でのみサポートされます。

### <a name="pre-meeting-app-experience"></a>会議前アプリのエクスペリエンス

**会議前のエクスペリエンス:**

![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

**[会議前] タブ:**

![会議前のタブ ビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔アクセス許可ユーザーは、次の 2 つの方法でタブ ギャラリーを介して会議にアプリを追加できます。

&emsp;&emsp;&#9679; Teams スケジュール **フォームの [** 詳細] タブを使用します。

&emsp;&emsp;&#9679;既存の会議の **[会議チャット** ] タブを使用します。</br> </br>

✔ タブ アプリは、プラス アイコン(➕) ボタンを使用して会議の詳細ページとチャット ページでアクセスできます。| 

✔が 10 件を超える場合は、タブ レイアウトが整理された状態である必要があります。

### <a name="in-meeting-app-experience"></a>会議中のアプリ エクスペリエンス

✔会議アプリは、チャット ウィンドウの上部バーでホストされ、会議内タブエクスペリエンスとして会議内タブエクスペリエンスとしてホストされます。ユーザーがタブ ギャラリーを通じて会議にタブを追加すると、会議のエクスペリエンス中のアプリが表示されます。

✔アクセス許可を持つユーザーは、会議中にアプリを追加できます。

✔会議のコンテキストに読み込まれると、アプリは Teams クライアント SDK を利用して 、アクセスし、エクスペリエンスを適切に `meetingId` `userMri` `frameContext` レンダリングできます。

✔アンケートまたはアンケートの結果をエクスポートすると、ユーザーに「結果が正常にダウンロードされました」と通知する必要があります。

✔ 2 つの領域で Teams 会議にアプリを表示するには、次の 2 つの領域を使用します。

&emsp;&emsp;&#9679; **サイド パネル**。 </br>

> [!NOTE]
> アプリ マニフェスト _でタブ_ がサイド パネル用 [](create-apps-for-teams-meetings.md#during-a-meeting)に最適化されている場合、それが表示される場所です。 また、指定された設計ガイドラインに従って、共有トレイエクスペリエンスの一部になれ得る。

&emsp;&emsp;&#9679; **会議中ダイアログ を開きます**。 会議の参加者に対してアクション可能なコンテンツを表示するには、会議内ダイアログを使用します。 *「Create* [Apps for Teams 会議」を参照してください](create-apps-for-teams-meetings.md)。

**会議中のエクスペリエンス:**

![会議中のエクスペリエンス](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会議内ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog.png)

**ユーザーの会議中の操作可能なダイアログ:**

![ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>会議後のアプリ エクスペリエンス

**会議後のエクスペリエンス:**

![会議ビューの投稿](../assets/images/apps-in-meetings/PostMeeting.png)

✔会議後アプリのシナリオは、現在の会議後のエクスペリエンスと似ています。表面内にタブが存在する利点が追加されています。 

✔権限を持つユーザーは、[Teams のスケジュール] フォームの [詳細] タブと既存の会議の [会議チャット] タブを使用して、タブ ギャラリーから会議にアプリを追加できます。

✔が 10 件を超える場合は、タブ レイアウトが整理された状態である必要があります。

### <a name="bots"></a>ボット

ボットの実装については、ボットの [ビルドから始め](../build-your-first-app/build-bot.md) 、Teams 会議用 [のアプリの作成を続行します](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。

### <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージング拡張機能の実装では、まずメッセージング [拡張機能を](../messaging-extensions/how-to/create-messaging-extension.md) ビルドしてから、Teams 会議用のアプリの作成 [を続行します](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。

## <a name="participant-roles-and-user-types-in-a-meeting"></a>会議の参加者の役割とユーザーの種類

![会議の参加者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>参加者の役割

参加者固有の承認を使用してアプリを設計できます。 たとえば、開催者や発表者だけが会議で投票を作成できる可能性があります。 既定の参加者設定は組織の IT 管理者によって決まりますが、会議の開催者は特定の会議の設定を変更できます。 開催者は、[会議のオプション] Web ページでこれらの変更を行えます。

1. **オーガナイザー**. 開催者は会議をスケジュールし、会議のオプションを設定し、会議の役割を割り当て、会議を開始します。 M365 アカウントを持つユーザー (Teams ライセンスを所有している) のみを開催者にし、出席者のアクセス許可を制御できます。
1. **発表者**. 発表者は、開催者とほぼ同じ機能を持っています。ただし、発表者はセッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。 既定では、会議に参加する参加者には発表者の役割があります。
1. **出席者**。 出席者とは、会議に出席するために招待されたが、発表者として機能する権限を持つユーザーです。 出席者は他の会議メンバーとやり取りできますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。

_「Teams_ [**会議での役割」を参照してください。**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

[会議のオプション]  **ページには、次** のようにアクセスできます。

&#11200; Teams で、[ **予定表の予定表** のロゴ] に移動し、 ![ 会議を ](../assets/images/apps-in-meetings/calendar-logo.png) 選択し、[会議のオプション] **を選択します**。

&#11200;会議出席依頼で、[会議のオプション] **を選択します**。

&#11200;会議中に、[会議コントロールに参加者 ![ を表示する] ](../assets/images/apps-in-meetings/show-participants.png) アイコンを選択します。 次に、参加者の一覧の上で、[アクセス許可の **管理] を選択します**。

### <a name="user-types"></a>ユーザーの種類

> [!NOTE]
> ユーザーの種類は、会議に参加し、上記のいずれかの参加者の役割を引き受け取ります。 User 型は **getParticipantRole** API の一部として公開されません。

1. **テナント内**。 これらのユーザーは組織に属し、テナントの Azure Active Directory の資格情報を持ちます。 通常、フルタイム、オンサイト、またはリモートの従業員です。
1. **ゲスト**。 ゲストは、組織のテナント内の Teams または他のリソースにアクセスするために招待された別の組織の参加者です。 ゲストは組織の Active Directory に追加され、チーム チャット、会議、ファイルにフル アクセスできるネイティブ チーム メンバーと同じ Teams 機能をほぼすべて提供できます。 _「Microsoft_ [Teams のゲスト アクセス」を参照してください。](/microsoftteams/guest-access)
1. **フェデレーション/外部**. フェデレーション ユーザーは、会議への参加を招待された別の組織の外部 Teams ユーザーです。 これらのユーザーはフェデレーション パートナーと有効な資格情報を持つので、Teams によって認証されますが、組織からチームや他の共有リソースにアクセスできないと処理されます。 外部ユーザーにチームとチャネルへのアクセスを許可する場合は、ゲスト アクセスの方が良いオプションになる可能性があります。 _「Microsoft_ [Teams での外部アクセスの管理」を参照してください。](/microsoftteams/manage-external-access)
1. **匿名**. 匿名ユーザーは Active Directory ID を持ち、テナントとフェデレーションされません。 匿名参加者は外部ユーザーに似ていましたが、その ID は会議に投影されません。 匿名ユーザーは、会議ウィンドウでアプリにアクセスできます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [アプリをデザインする](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
> [!div class="nextstepaction"]
> [アプリを作成する](create-apps-for-teams-meetings.md)
