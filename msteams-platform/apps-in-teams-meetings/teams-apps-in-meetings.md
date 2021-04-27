---
title: Teams 会議のアプリ
author: laujan
description: 参加者とユーザーの役割に基づく Teams 会議のアプリの概要
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 29a24b70921e51d63d804e7a3edd901f607d3148
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018384"
---
# <a name="apps-in-teams-meetings"></a>Teams 会議のアプリ

会議では、包括的でアクティブなフォーラムで、共同作業、パートナーシップ、情報に基づいたコミュニケーション、共有フィードバックが可能になります。 会議アプリは、出席者の状態に応じて、会議前、会議中、会議後のアプリ エクスペリエンスなど、会議のライフサイクルの各段階でユーザー エクスペリエンスを提供できます。

Teams のエンド ユーザーは、次に示すタブ ギャラリーを使用して会議中にアプリにアクセスできます。

* かんばんボードの事前ステージ
* 会議内の操作可能なダイアログを起動する
* 会議後のポーリングを作成する

Teams の会議アプリの機能拡張は、次の概念に基づいて行います。

✔のライフサイクルには、会議の時間枠の前、中、後などのステージがあります。  
✔開催者、発表者、出席者などの会議の参加者の役割。  
✔、ゲスト、フェデレーション、匿名の Teams ユーザーなどの会議のユーザーの種類を指定します。

この記事では、会議のライフサイクルと、タブ、ボット、メッセージング拡張機能を会議に統合する方法について説明します。 また、参加者の役割を識別し、さまざまなユーザーの種類を使用してタスクを実行することもできます。

> [!NOTE]
> 会議アプリの機能拡張機能を使用するには、適切なアクセス許可が必要です。

### <a name="meeting-lifecycle"></a>会議のライフサイクル

会議のライフサイクルは、会議前、会議中、会議後のアプリ エクスペリエンスで構成されます。 会議のライフサイクルの各段階で、タブ、ボット、メッセージング拡張機能を統合できます。

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a>タブを会議のライフサイクルに統合する

タブを使用すると、チーム メンバーはチャネルまたはチャット内の特定の領域のサービスとコンテンツにアクセスできます。 これにより、チームはタブを直接処理し、タブ内で使用可能なツールとデータに関する会話を行います。 Teams 会議で、ユーザーはプラスを選択してタブを追加できます。 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>をクリックし、タブとしてインストールするアプリを選択します。

> [!IMPORTANT]
> タブを会議に統合している場合、アプリはタブの Teams シングル サインオン [(SSO) 認証フロー](../tabs/how-to/authentication/auth-aad-sso.md) に従う必要があります。

> [!NOTE]
> * モバイル クライアントは、会議の開催前と開催後のステージでのみタブをサポートします。 現在、会議中のダイアログとパネルである会議中のエクスペリエンスは、モバイルでは使用できません。
> * アプリは、プライベートスケジュールされた会議でのみサポートされます。

### <a name="pre-meeting-app-experience"></a>会議前アプリのエクスペリエンス

**会議前のエクスペリエンス:**

![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

**[会議前] タブ:**

![会議前のタブ ビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔アクセス許可ユーザーとは、会議のライフサイクルの異なる段階で会議にアプリを追加できるユーザーです。 これらのユーザーは、次の 2 つの方法でタブ ギャラリーを介して会議にアプリを追加できます。

   * [Teams の **スケジュール設定]** フォームの [詳細] タブを使用します。

   * 既存の会議 **で [** 会議チャット] タブを使用する。

✔タブ アプリは、プラスボタンを使用して会議の詳細ページとチャット ページ➕できます。

✔が 10 件を超える場合は、タブ レイアウトが整理された状態である必要があります。

### <a name="in-meeting-app-experience"></a>会議中のアプリ エクスペリエンス

✔アプリは、チャット ウィンドウの上部バーでホストされ、会議内タブを使用して会議内タブエクスペリエンスとしてホストされます。ユーザーがタブ ギャラリーを通じて会議にタブを追加すると、会議のエクスペリエンス中の **アプリが** 表示されます。

✔アクセス許可を持つユーザーは、会議中にアプリを追加できます。

✔会議のコンテキストで読み込まれると、アプリは Teams クライアント SDK を利用して 、 にアクセスし、エクスペリエンスを適切に `meetingId` `userMri` `frameContext` レンダリングできます。

✔アンケートまたはポーリングの結果をエクスポートすると、結果が正常にダウンロードされたことをユーザーに通知します。

✔サイド パネルまたは会議内ダイアログ ボックスの Teams 会議にアプリが表示されます。 会議の参加者に対してアクション可能なコンテンツを紹介するには、会議内ダイアログ ボックスを使用します。 詳細については [、「Create apps for Teams meetings」を参照してください](create-apps-for-teams-meetings.md)。

   > [!NOTE]
   > アプリ マニフェストは、タブがサイド[](create-apps-for-teams-meetings.md#during-a-meeting)パネル用に最適化され、表示される場所を指定します。 また、指定された設計ガイドラインに従って、共有トレイエクスペリエンスの一部になれ得る。

次の画像は、アプリを会議中のダイアログ ボックスとして、別のサイド パネルとして表示します。

![会議中のエクスペリエンス](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会議内ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a>ユーザーの会議中の操作可能なダイアログ

![ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>会議後のアプリ エクスペリエンス

![会議ビューの投稿](../assets/images/apps-in-meetings/PostMeeting.png)

✔会議後アプリのシナリオは、現在の会議後のエクスペリエンスと似ています。表面内にタブが存在する利点が追加されています。

✔権限を持つユーザーは、[Teams のスケジュール] フォームの [詳細] タブと既存の会議の[会議チャット] タブを使用して、タブ ギャラリーから会議にアプリを追加できます。

✔が 10 件を超える場合は、タブ レイアウトを整理する必要があります。

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>ボットを会議のライフサイクルに統合する

ボットの実装については、ボットの [ビルドから始め](../build-your-first-app/build-bot.md) 、Teams 会議用 [のアプリの作成を続行します](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>メッセージング拡張機能を会議のライフサイクルに統合する

メッセージング拡張機能の実装では、まずメッセージング [拡張機能を](../messaging-extensions/how-to/create-messaging-extension.md) ビルドしてから、Teams 会議用のアプリの作成 [を続行します](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。

## <a name="participant-roles-and-user-types-in-a-meeting"></a>会議の参加者の役割とユーザーの種類

![会議の参加者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>参加者の役割

既定の参加者設定は、組織の IT 管理者によって決まります。 会議の参加者の役割を次に示します。

* **開催** 者 : 開催者は会議をスケジュールし、会議のオプションを設定し、会議の役割を割り当て、会議を開始します。 Teams ライセンスを持つ M365 アカウントを持つユーザーだけが開催者として使用し、出席者のアクセス許可を制御できます。 会議の開催者は、特定の会議の設定を変更できます。 開催者は、[会議のオプション] Web ページ **でこれらの変更を** 行えます。
* **発表者**: 発表者は開催者と同じ機能を持っています。 ただし、発表者はセッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。 既定では、会議に参加する参加者には発表者の役割があります。
* **出席者**: 出席者とは、会議に出席するために招待されたが、発表者として機能する権限を持つユーザーです。 出席者は他の会議メンバーとやり取りできますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。

アプリを追加、削除、またはアンインストールできるのは、開催者または発表者のみです。 開催者または発表者だけが会議でポーリングを作成できます。

詳細については [、「Teams 会議の役割」を参照してください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

[会議のオプション]  **ページには、次** のようにアクセスできます。

* Teams で、[予定表] の **ロゴに** ![ 移動し ](../assets/images/apps-in-meetings/calendar-logo.png) 、会議を選択し、[会議のオプション] **を選択します**。

* 会議出席依頼で、[会議のオプション] **を選択します**。

* 会議中に、[会議コントロールに **参加者** ![ を表示する ](../assets/images/apps-in-meetings/show-participants.png) ] アイコンを選択します。 次に、参加者の一覧の上で、[アクセス許可の **管理] を選択します**。

### <a name="user-types"></a>ユーザーの種類

> [!NOTE]
> 特定のユーザーの種類が割り当てられているユーザーは、会議に参加し、参加者の役割で説明されている参加者の役割の 1 つを [引き受け取ります](#participant-roles)。 ユーザーの種類は **getParticipantRole** API には含まれません。

次のユーザーの種類は、各ユーザーが実行できる操作と、ユーザーがアクセスできる操作を識別します。

* **テナント内 :** テナント内ユーザーは組織に属し、テナントの Azure Active Directory (AAD) に資格情報を持ちます。 通常、フルタイム、オンサイト、またはリモートの従業員です。 テナント内のユーザーには、開催者、発表者、または出席者を指定できます。
* **ゲスト**: ゲストは、Teams または組織のテナント内の他のリソースにアクセスするために招待された別の組織の参加者です。 ゲストは組織の AAD に追加され、チーム チャット、会議、ファイルにアクセスできるネイティブ チーム メンバーと同じ Teams 機能を持ちます。 ゲスト ユーザーには、開催者、発表者、または出席者を指定できます。 詳細については [、「Teams でのゲスト アクセス」を参照してください](/microsoftteams/guest-access)。
* **フェデレーションまたは外部**: フェデレーション ユーザーとは、会議への参加を招待された別の組織の外部 Teams ユーザーです。 これらのユーザーは、フェデレーション パートナーと有効な資格情報を持ち、Teams によって承認されています。 組織からチームや他の共有リソースにアクセスできない。 ゲスト アクセスは、外部ユーザーがチームとチャネルにアクセスできる優れたオプションです。 詳細については、「Teams での外部 [アクセスの管理」を参照してください](/microsoftteams/manage-external-access)。
* **匿名**: 匿名ユーザーは AAD ID を持ち、テナントとフェデレーションされません。 匿名参加者は外部ユーザーに似ていましたが、その ID は会議に投影されません。 匿名ユーザーは開催者にすることはできませんが、発表者または出席者にできます。

> [!NOTE]
> 匿名ユーザーは、グローバル既定のユーザー レベルのアプリアクセス許可ポリシーを継承します。 詳細については、「アプリの管理 [」を参照してください](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)。

次の表に、ユーザーの種類と、各ユーザーがアクセスできる機能を示します。

| ユーザーの種類 | タブ | ボット | メッセージング拡張機能 | アダプティブ カード | タスク モジュール | 会議中ダイアログ |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| 匿名ユーザー | 使用不可 | 使用不可 | 使用不可 | 会議チャットでの操作は許可されます。 | アダプティブ カードからの会議チャットでの操作は許可されます。 | 利用不可 |
| テナント AAD の一部であるゲスト | 対話は許可されます。 作成、更新、削除は許可されません。 | 使用不可 | 使用不可 | 会議チャットでの操作は許可されます。 | アダプティブ カードからの会議チャットでの操作は許可されます。 | Available |
| フェデレーション | 使用不可 | 使用不可 | 使用不可 | 使用不可 | 使用不可 | 使用不可 |

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [Tab](../tabs/what-are-tabs.md#how-do-tabs-work)

> [!div class="nextstepaction"]
> [Bot](../bots/what-are-bots.md)

> [!div class="nextstepaction"]
> [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)

> [!div class="nextstepaction"]
> [アプリをデザインする](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [アプリを作成する](create-apps-for-teams-meetings.md)
