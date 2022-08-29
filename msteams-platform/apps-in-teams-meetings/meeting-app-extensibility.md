---
title: 統合された会議アプリ
author: surbhigupta
description: Teams 会議のライフサイクルと、デスクトップとモバイルでのユーザー会議エクスペリエンス、ユーザーの種類、会議ライフサイクルにおけるボットとメッセージ拡張機能の統合について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.date: 04/07/2022
ms.openlocfilehash: 3c9265f48191f4078d66b4166ce3a3c0650e762d
ms.sourcegitcommit: b060a3901a3ba770ea6fca96d0ab477c252af1a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2022
ms.locfileid: "67417508"
---
# <a name="unified-meetings-apps"></a>統合された会議アプリ

Teams 統合会議アプリは、次の概念に基づいています。

* 会議のライフサイクルには、会議前、会議中、会議後の異なる段階があります。  
* 会議では、開催者、発表者、出席者の 3 つの異なる参加者の役割があります。 詳細については、「[Teams 会議での役割](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。  
* 会議には、[テナント内、](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.)[ゲスト](/microsoftteams/guest-access)、フェデレーション、匿名ユーザーなど、さまざまな種類[の](/microsoftteams/manage-external-access)ユーザーがあります。

この記事では、会議のライフサイクルに関する情報と、タブ、ボット、メッセージ拡張機能を統合する方法について説明します。 さまざまな参加者ロールとユーザーの種類を識別します。

## <a name="meeting-lifecycle"></a>会議のライフサイクル

会議のライフサイクルは、会議前、会議中、会議後のアプリ エクスペリエンスで構成されます。 会議のライフサイクルの各段階で、タブ、ボット、メッセージ拡張機能を統合できます。

> [!NOTE]
>
> * インスタント会議、1 対 1、グループ通話用のアプリは、現在、 [パブリック開発者向けプレビュー](../resources/dev-preview/developer-preview-intro.md)でのみ利用できます。
>
> * ボット、カード、メッセージ拡張機能、メッセージ アクションなどの会議拡張機能は、Web クライアントでサポートされています。 ただし、現在、タブ、コンテンツ バブル、ステージへの共有などのホストされたエクスペリエンスは完全にはサポートされていません。

### <a name="integrate-tabs-into-the-meeting-lifecycle"></a>会議のライフサイクルにタブを統合する

タブを使用すると、チームのメンバーは会議内の特定のスペースでサービスとコンテンツにアクセスできます。 チームは、タブを直接操作し、タブの中で使用できるツールとデータに関する会話を行います。 Teams 会議では、次を選択してタブを追加できます。 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>をクリックし、インストールするアプリを選択します。

> [!IMPORTANT]
> 会議にタブ アプリを統合している場合は、 [タブの Teams シングル サインオン (SSO) 認証フロー](../tabs/how-to/authentication/tab-sso-overview.md)に従うことをお勧めします。

> [!NOTE]
> Teams 会議拡張機能タブ アプリのアプリの追加オプションは、Teams Web クライアントではサポートされていません。

#### <a name="pre-meeting-app-experience"></a>会議前のアプリ エクスペリエンス

会議前のアプリ エクスペリエンスでは、会議アプリを検索して追加できます。 会議の参加者にアンケートを取るための投票機能の開発など、会議前のタスクを行うこともできます。

既存の会議にタブを追加するには:

1. 予定表で、タブを追加する会議を選択します。
1. **[詳細]** タブを選択し、次を選択します: <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. タブ ギャラリーが表示されます。

    :::image type="content" source="~/assets/images/apps-in-meetings/Pre-Meeting-002.png" alt-text="会議前のアプリエクスペリエンス。":::

1. タブ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。 アプリはタブとしてインストールされます。

   > [!NOTE]
   >
   > * 会議 **チャット** タブを使用して、既存の会議にタブを追加することもできます。
   > * 投票またはアンケートが 10 件を超える場合、タブ レイアウトは整理された状態である必要があります。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/PreMeetingTab.png" alt-text="会議中のタブ。":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

モバイルで既存の会議にタブを追加した後、会議の詳細の **[その他** ] セクションで、会議前のエクスペリエンスで同じアプリを表示できます。

<img src="../assets/images/apps-in-meetings/mobilePostMeeting.png" alt="Mobile pre-meeting experience" width="200"/>  

---

#### <a name="in-meeting-app-experience"></a>会議中のアプリ エクスペリエンス

会議中のアプリ エクスペリエンスを使用すると、アプリと会議内ダイアログ ボックスを使用して、会議中に参加者とのやり取りを行うことができます。 会議アプリは、会議ウィンドウのツール バーに会議中タブとしてホストされます。会議中のダイアログ ボックスを使用して、会議の参加者に実用的なコンテンツを紹介できます。 詳細については、「 [Teams 会議用のアプリを有効にして構成する](enable-and-configure-your-app-for-teams-meetings.md)」を参照してください。

モバイルの場合、会議アプリは **、会議** で &#x25CF;&#x25CF;&#x25CF; アプリ>省略記号から利用できます。 [ **アプリ] を** 選択して、会議で使用可能なすべてのアプリを表示します。

デスクトップの場合、会議中にアプリを追加するには、[会議内] ウィンドウの **[アプリ**:::image type="icon" source="../assets/icons/add-icon.png" border="false":::の追加] オプションを使用します。

会議中にタブを使用するには:

1. Teams に移動します。
1. 予定表で、タブを使用する会議を選択します。
1. 会議に入った後、チャット ウィンドウのツール バーから、必要なアプリを選択します。
    アプリは、サイド パネルまたは会議内ダイアログ ボックスの Teams 会議に表示されます。
1. 会議中ダイアログ ボックスで、フィードバックとして応答を入力します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/desktop-in-meeting-dialog-view.png" alt-text="デスクトップの会議中ビュー。":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

会議に参加し、デスクトップまたは Web からアプリを追加すると、アプリはモバイル Teams 会議の [ **アプリ** ] セクションに表示されます。 [ **アプリ] を** 選択して、アプリの一覧を表示します。 ユーザーは、アプリの会議内サイド パネルとして任意のアプリを起動できます。

会議中ダイアログ ボックスが表示され、フィードバックとして応答を入力できます。

<img src="../assets/images/apps-in-meetings/mobile-in-meeting-dialog-view.png" alt="Mobile dialog box view" width="200"/>

> [!NOTE]
> アプリがモバイルで動作するようにアプリ マニフェストを変更する必要はありません。

---

> [!NOTE]
>
> * アプリは Teams クライアント SDK を利用して、`userMri`エクスペリエンスに`meetingId`適切にアクセスし`frameContext`、適切にレンダリングできます。
> * 会議中ダイアログ ボックスが正常に表示された場合は、結果が正常にダウンロードされたことを示す通知が送信されます。
> * アプリ マニフェストは、アプリを表示する場所を指定します。 これを行うには、マニフェストでコンテキスト フィールドを指定します。 また、指定された [設計ガイドライン](~\apps-in-teams-meetings\design\designing-apps-in-meetings.md)に従って、共有会議ステージエクスペリエンスの一部でもあります。
> * 会議ステージは、匿名ユーザーと Teams Web クライアントではサポートされていません。

次の図は、会議中のサイド パネルを示しています。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

![会議中のサイド パネル](../assets/images/in-meeting-dialog.png)

# <a name="mobile"></a>[モバイル](#tab/mobile)

<img src="../assets/images/apps-in-meetings/sidepanelmobile.png" alt="In-meeting side panel mobile" width="300"/>

---

次の表では、アプリが検証され、検証されていない場合のアプリの動作について説明します。

|アプリ機能 | アプリが検証される | アプリが検証されない |
|---|---|---|
| 会議の拡張性 | アプリは会議に表示されます。 | アプリは、モバイル クライアントの会議には表示されません。 |

詳細については、 [ストアの検証ガイドラインに関するページを](../concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)参照してください。

#### <a name="post-meeting-app-experience"></a>会議後のアプリエクスペリエンス

会議後のアプリ エクスペリエンスでは、アンケートの結果やフィードバックなど、会議の結果を表示できます。 選択 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/> タブを追加し、会議のメモを取得し、開催者と出席者がアクションを実行する必要がある結果を確認します。

次の図は、[ **Contoso** ] タブを表示し、会議出席者から受け取った投票とフィードバックの結果を示しています。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/post.png" alt-text="結果が表示された [Contoso] タブ。":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="~/assets/images/apps-in-meetings/mobilepremeeting.png" alt-text="会議アプリのエクスペリエンスを投稿します。":::

---

> [!NOTE]
> 10 を超える投票またはアンケートがある場合は、タブ レイアウトを整理する必要があります。

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>会議のライフサイクルにボットを統合する

グループ チャット スコープで有効になっているボットは、会議で機能し始めます。 ボットを実装するには、最初に [ボットをビルド](../build-your-first-app/build-bot.md)してから、 [Teams 会議用のアプリの作成](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references)を続行します。

### <a name="integrate-message-extensions-into-the-meeting-lifecycle"></a>メッセージ拡張機能を会議のライフサイクルに統合する

メッセージ拡張機能を実装するには、まず [メッセージ拡張機能を作成](../messaging-extensions/how-to/create-messaging-extension.md)してから、 [Teams 会議用のアプリの作成](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references)を続行します。

Teams 統合会議アプリを使用すると、会議の参加者ロールに基づいてアプリを設計できます。

## <a name="participant-roles-in-a-meeting"></a>会議の参加者ロール

:::image type="content" source="~/assets/images/apps-in-meetings/participant-roles.png" alt-text="会議の参加者ロール。":::

既定の参加者設定は、組織の IT 管理者によって決まります。 会議の参加者ロールを次に示します。

* **開催者**: 開催者は会議をスケジュールし、会議オプションを設定し、会議の役割を割り当て、会議を開始します。 Microsoft 365 アカウントと Teams ライセンスを持つユーザーは、開催者のみであり、出席者のアクセス許可を制御できます。 会議の開催者は、特定の会議の設定を変更できます。 開催者は、[ **会議オプション** ] Web ページでこれらの変更を行うことができます。

* **発表者**: 発表者は、除外された開催者と同じ機能を持ちます。 発表者は、開催者をセッションから削除したり、セッションの会議オプションを変更したりすることはできません。 既定では、会議に参加する参加者には発表者ロールがあります。

* **出席者**: 出席者は、会議に出席するように招待されたユーザーです。 出席者の機能には、次のような制限があります。
  * 他の会議メンバーと対話することはできますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。  
  * ユーザーは、Teams デスクトップ クライアントの会議ステージで、アプリをインストールしたり、アプリの資格なしでタブ アプリを表示したり操作したりできます。 Teams Web クライアントの会議ステージでアプリを表示または操作することはできません。
  * サイド パネルでアプリを表示したり操作したりすることはできません。アプリのエンタイトルメントはありません。
  * 発表者として機能する権限はありません。
  * 出席者が匿名ユーザーとして参加している場合、Teams Web クライアントとデスクトップ クライアントの両方の会議ステージでタブ アプリを表示または操作することはできません。

> [!NOTE]
> アプリを追加、削除、またはアンインストールできるのは、開催者または発表者のみです。

詳細については、「[Teams 会議での役割](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。

会議の参加者ロールに基づいてアプリを設計したら、会議の各ユーザーの種類を特定し、アクセスできる内容を選択できます。

## <a name="user-types-in-a-meeting"></a>会議のユーザーの種類

ユーザーの種類 (テナント内、ゲスト、フェデレーション、会議の外部ユーザーなど) は、会議の [参加者ロール](#participant-roles-in-a-meeting)の 1 つを実行できます。

> [!NOTE]
> ユーザーの種類は **、getParticipantRole** API には含まれません。

次の一覧では、アクセシビリティとパフォーマンスと共に、さまざまなユーザーの種類について詳しく説明します。

* **テナント内**: テナント内ユーザーは組織に属し、テナントのMicrosoft Azure Active Directory (Azure AD) に資格情報を持ちます。 フルタイム、オンサイト、またはリモートの従業員です。 テナント内ユーザーは、開催者、発表者、または出席者にすることができます。
* **ゲスト**: ゲストは、Teams または組織のテナント内の他のリソースにアクセスするように招待された別の組織の参加者です。 ゲストは組織の Azure AD に追加され、ネイティブ チーム メンバーと同じ Teams 機能を持ちます。 チーム チャット、会議、ファイルにアクセスできます。 ゲストは、開催者、発表者、または出席者にすることができます。 詳細については、「 [Teams でのゲスト アクセス](/microsoftteams/guest-access)」を参照してください。
* **フェデレーションユーザーまたは外部** ユーザー: フェデレーション ユーザーは、会議への参加を招待された別の組織の外部 Teams ユーザーです。 フェデレーション ユーザーは、フェデレーション パートナーと有効な資格情報を持ち、Teams によって承認されます。 チームや組織の他の共有リソースにアクセスすることはできません。 ゲスト アクセスは、外部ユーザーがチームやチャネルにアクセスするためのより優れたオプションです。 詳細については、「 [Teams で外部アクセスを管理](/microsoftteams/manage-external-access)する」を参照してください。

    > [!NOTE]
    > Teams ユーザーは、他の組織との会議やチャットをホストするときにアプリを追加できます。 ユーザーは、他の組織がホストする会議やチャットに参加するときに、外部ユーザーが共有するアプリを使用できます。 ホスティング ユーザーの組織のデータ ポリシーと、そのユーザーの組織によって共有されるサード パーティ製アプリのデータ共有プラクティスが有効になります。

    > [!IMPORTANT]
    > 現時点では、サイドローディング アプリは Government Community Cloud (GCC) で利用できますが、GCC-High および国防総省 (DOD) では使用できません。 GCC では、サード パーティ製アプリは既定で無効になっています。 GCC のサード パーティ製アプリを有効にするには、「[アプリのアクセス許可ポリシーを管理する](/microsoftteams/teams-app-permission-policies)」と「[アプリの管理](/microsoftteams/manage-apps)」を参照してください。

* **匿名**: 匿名ユーザーは Azure AD ID を持っていず、テナントとフェデレーションされていません。 匿名参加者は外部ユーザーに似ていますが、その ID は会議に表示されません。 匿名ユーザーは、会議ウィンドウと会議ステージ内のアプリにアクセスできません。 匿名ユーザーは開催者にすることはできませんが、発表者または出席者にすることができます。

    > [!NOTE]
    > 匿名ユーザーは、グローバルな既定のユーザー レベルのアプリアクセス許可ポリシーを継承します。 詳細については、「アプリの [管理」を](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)参照してください。

次の表に、ユーザーの種類と、スケジュールされた会議で各ユーザーがアクセスできる機能の一覧を示します。

| ユーザーの種類 | タブ | ボット | メッセージ拡張機能 | アダプティブ カード | タスク モジュール | 会議中ダイアログ | 会議ステージ |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| 匿名ユーザー | 使用不可 | 使用不可 | 使用不可 | 会議チャットでの対話は許可されます。 | アダプティブ カードからの会議チャットでの対話は許可されます。 | 使用不可 | 使用不可 |
| テナント Azure AD の一部であるゲスト | 対話は許可されます。 作成、更新、削除は許可されません。 | 使用不可 | 使用不可 | 会議チャットでの対話は許可されます。 | アダプティブ カードからの会議チャットでの対話は許可されます。 | Available | Teams デスクトップ クライアントでのみ、会議ステージでアプリを開始、表示、操作できます |
| フェデレーション ユーザーの詳細については、 [非標準ユーザーを](/microsoftteams/non-standard-users)参照してください。 | スケジュールされた会議では、対話が許可されます。 作成、更新、削除は許可されません。 | 対話は許可されます。 取得、更新、削除は許可されません。 | 使用不可 | 会議チャットでの対話は許可されます。 | アダプティブ カードからの会議チャットでの対話は許可されます。 | 使用不可 | Teams デスクトップ クライアントでのみ、会議ステージでアプリを開始、表示、操作できます。 |

> [!NOTE]
>
> 通話中のアプリのさまざまなユーザーの種類の動作は、次を除くスケジュールされた会議での動作と同じです。
>
> * フェデレーション ユーザーは、呼び出しでタブ アプリを操作できません。
> * フェデレーション ユーザーがテナント内ユーザーまたはゲスト ユーザーを含む既存の呼び出しに追加された場合、すべての参加者はアプリの追加、更新、または削除を行う機能を失います。 ただし、フェデレーション ユーザーを呼び出しに招待する前に追加されたアプリを操作できるのは、既存のテナント内ユーザーまたはゲスト ユーザーだけです。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [Teams 会議用にアプリを有効にして構成する](enable-and-configure-your-app-for-teams-meetings.md)

## <a name="see-also"></a>関連項目

* [Tab](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [ボット](../bots/what-are-bots.md)
* [メッセージ拡張機能](../messaging-extensions/what-are-messaging-extensions.md)
* [アプリをデザインする](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Microsoft Teams 会議出席レポート](/microsoftteams/teams-analytics-and-reports/meeting-attendance-report)
