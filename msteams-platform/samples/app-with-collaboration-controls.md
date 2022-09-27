---
title: コラボレーション コントロールを使用したアプリケーション
author: surbhigupta
description: このモジュールでは、Teams のコラボレーション コントロールを使用してモデル駆動型アプリを構築する方法と、コラボレーション コントロールをアプリに追加する方法について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: e712c55dd4543edda9115751be09d81d1795f02b
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027341"
---
# <a name="create-a-new-model-driven-app-with-collaboration-controls-for-teams"></a>Teams のコラボレーション コントロールを使用して新しいモデル駆動型アプリを作成する

コラボレーション コントロールは、 [モデル駆動型アプリケーション](/power-apps/maker/model-driven-apps/model-driven-app-overview)向けに設計されています。 次のセクションでは、モデル駆動型アプリを作成する方法について説明します。

> [!NOTE]
> 現在、コラボレーション コントロールは [、パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

## <a name="create-a-model-driven-application"></a>モデル駆動型アプリケーションを作成する

1. 開きます [https://make.powerapps.com。](https://make.powerapps.com/) または [https://make.preview.powerapps.com.](https://make.preview.powerapps.com/)

1. 左側のウィンドウで **[ソリューション** ] を選択します。

1. [ **新しいソリューション]** を選択して、今後のすべてのカスタマイズにホームを提供できるようにします。

   :::image type="content" source="../assets/images/collaboration-control/new-solution.png" alt-text="スクリーンショットは、新しいソリューションを示す例です。":::

1. 新しいソリューションの名前と発行元を指定します。このソリューションはカスタム Collaboration Managerを保持します。

   :::image type="content" source="../assets/images/collaboration-control/collaboration-manager.png" alt-text="スクリーンショットは、コラボレーション マネージャーを示す例です。":::

1. [**作成**] を選択します

1. ソリューションが作成されると、ソリューションの一覧に表示されます。 ソリューションを選択して開きます。

1. アプリを作成する前に、データのホームを作成します。 [ **新しい** > **テーブル** ] を選択して作業を開始します。

     :::image type="content" source="../assets/images/collaboration-control/create-table.png" alt-text="スクリーンショットでは、新しいテーブルを作成する方法について説明しています。":::

1. テーブルに名前を付けます。 [ **詳細設定] オプション** で、[ **新しいアクティビティの作成**] を選択します。

   :::image type="content" source="../assets/images/collaboration-control/new-activity.png" alt-text="スクリーンショットでは、新しいアクティビティを作成する方法について説明しています。":::

1. **[保存]** を選択します。

1. テーブルの作成が完了したら、追加の列、リレーションシップなどを追加してカスタマイズできます (省略可能)。

1. 次に、[新しいアプリ モデル駆動型アプリ] を選択して **、新しい** >  > **モデル駆動型アプリを** 作成できます。

   :::image type="content" source="../assets/images/collaboration-control/model-driven-app.png" alt-text="スクリーンショットは、新しいモデル駆動型アプリを示す例です。":::

1. 新しい **モダン アプリ デザイナー (プレビュー)** を選択して、新しいアプリを開きます。

   :::image type="content" source="../assets/images/collaboration-control/model-driven-app-blank.png" alt-text="スクリーンショットは、新しいモデル駆動型アプリが空白であることを示す例です。":::

1. [作成] を選択 **します。**

1. アプリに名前を付けて、[**作成**] を選択します。

   :::image type="content" source="../assets/images/collaboration-control/collaboration-manager-for-inspection.png" alt-text="スクリーンショットは、検査用のコラボレーション マネージャーを示す例です。":::

1. [ **ページの追加] を選択します。**

1. **テーブル ベースのビューとフォームを選択します。**

   :::image type="content" source="../assets/images/collaboration-control/table-based.png" alt-text="スクリーンショットは、テーブル ベースのビューとフォームを示す例です。":::

1. **[次へ**] を選択します。

1. 前に作成したテーブルを検索して選択します。

   :::image type="content" source="../assets/images/collaboration-control/table-view-form-pages.png" alt-text="スクリーンショットは、テーブル ビューのフォーム ページを示す例です。":::

1. [ **追加] を選択します。**

1. [ **発行]** を選択して、アプリを保存して発行します。

1. **[再生] を** 選択して、新しいアプリをテストします。

これで、モデル駆動型アプリが正常に構築されました。

## <a name="add-collaboration-controls-to-your-application"></a>アプリケーションにコラボレーション コントロールを追加する

作成したアプリに、タスク、会議、ファイル、ノートエクスペリエンスなどのコラボレーションコントロール機能を追加する手順を次に示します。

1. [タスク]、[会議]、[メモ] タブを含めるには、[メイン情報] フォームを編集する必要があります。 開始するには、エクスプローラーに戻り、ソリューションを選択します。

1. [Teams 用の新しいモデル駆動型アプリの作成で作成したテーブルを選択します。](#create-a-new-model-driven-app-with-collaboration-controls-for-teams)

1. テーブルの [フォーム] タブに移動します。

     :::image type="content" source="../assets/images/collaboration-control/forms-tab.png" alt-text="スクリーンショットは、テーブルの [フォーム] タブを示す例です。":::

1. フォーム の種類 **Main** の [情報] フォームを選択して、フォーム デザイナーで開きます。

1. フォーム デザイナーに入ったら、[**コンポーネント**] セクションから **1 列のタブ** を押してドラッグします。

     :::image type="content" source="../assets/images/collaboration-control/components.png" alt-text="スクリーンショットは、Power アプリのコンポーネントを示す例です。":::

1. タブを選択したら、プロパティ ウィンドウでタブの名前を "タスク" に変更します。

1. タブ名を選択してセクション全体を選択し、[プロパティ] ウィンドウで **[最初のコンポーネントを完全なタブに展開]** を選択します。 これは、コラボレーション コントロールが完全なタブ ビューで最適に表示されるために必要です。

    :::image type="content" source="../assets/images/collaboration-control/tasks-pane.png" alt-text=" スクリーンショットでは、最初のコンポーネントを完全なタブに選択する方法について説明しています。":::

     :::image type="content" source="../assets/images/collaboration-control/expand-first-component.png" alt-text=" スクリーンショットでは、最初のコンポーネントを完全なタブに展開する方法について説明しています。":::

1. コントロール ドロワーの [コラボレーション (プレビュー)] カテゴリを展開し、タスク (プレビュー) コントロールを [タスク] フォームのセクションにドラッグします。

     :::image type="content" source="../assets/images/collaboration-control/collab-preview.png" alt-text="タスク フォームのセクションにコントロールをプレビューする":::

3. テーブルを [アクティビティ] に設定&、[完了] を選択します。

     :::image type="content" source="../assets/images/collaboration-control/select-table-activities.png" alt-text="アクティビティのテーブルを選択する":::

5. プロパティで [ラベルの非表示] を選択します。

     :::image type="content" source="../assets/images/collaboration-control/hide-label-properties.png" alt-text="ラベルを非表示にするを選択する":::

1. タスク コントロールが表示されます。

     :::image type="content" source="../assets/images/collaboration-control/new-collab-control.png" alt-text="タスク コントロールの表示":::

1. タスクの手順を繰り返して、承認、ファイル、会議、メモのコントロールをアプリに追加します。
1. すべてのコントロールが追加されると、フォーム デザイナーで下に表示されるコントロールが表示されます。 フォーム デザイナーでコントロールがレンダリングされない場合 (空白のフォームなど) は、Power Apps でアプリを実行し、"構成" ページまたは "空の状態" が存在すると、コントロールが正常に追加されたことを意味します。

     :::image type="content" source="../assets/images/collaboration-control/new-collab-approval.png" alt-text="コントロール フォーム デザイナー":::

1. Power Apps で Power アプリを選択して実行できるようになりました。

     :::image type="content" source="../assets/images/collaboration-control/collaboration-manager-for-inspections-power-apps.png" alt-text="検査用のコラボレーション マネージャー":::

1. **[+ 新規**] を選択して新しいレコードを作成し、レコードを開きます。

     :::image type="content" source="../assets/images/collaboration-control/power-apps-open-the-record.png" alt-text="スクリーンショットは、レコードを開く Power Apps を示す例です。":::

1. 次の図のように表示される各タブのビューを表示できるようになりました。

     :::image type="content" source="../assets/images/collaboration-control/tabs.png" alt-text="スクリーンショットは、タスクを示す例です。":::

     > [!TIP]
     > コントロールは、レコードがアプリケーションに保存された後にのみ表示されます。 コントロール タブがレコードに表示されない場合は、ブラウザーを更新するか、Power Apps からアプリを再発行してみてください。

これで、アプリケーションにコラボレーション コントロールが正常に追加されました。 これで、Power Apps でアプリケーションを実行し、コントロールを起動できるようになりました。 設定はまだ構成されていないため、タスクや会議などのエンティティを追加するまで作成できません。

## <a name="define-settings-for-your-collaboration"></a>コラボレーションの設定を定義する

[新しいモデル駆動型アプリ](#create-a-new-model-driven-app-with-collaboration-controls-for-teams)で作成されたテーブルなど、ビジネス エンティティのコラボレーション コントロールの設定を定義できます。

適用できる設定は次のとおりです。

|Settings|使用元|
|---|---|
|グループ ID|タスク、内部会議、承認。|
|Bookings ビジネス ID|Bookings を使用した外部会議 |
|サイト ID|SharePoint ファイル |
|ドライブ ID|SharePoint ファイル|

> [!NOTE]
> 設定はアプリを起動する際に役立つため、推奨される手順に従っていることを確認してください。 コントロールの起動と保存に問題がある場合は、値を再確認します。

新しいチームを作成するか、Microsoft Teams で既存のチームを使用してアプリケーションをホストし、設定変数を作成することで、グループ ID を取得できます。

新しいチームを作成するには、 [最初からチームを作成する方法に関するページを](https://support.microsoft.com/en-us/office/create-a-team-from-scratch-174adf5f-846b-4780-b765-de1a0a737e2b)参照してください。

承認、タスク、および内部会議のために Teams チームのグループ ID を取得するには、次の手順に従います。

1. チームの一覧でチームを見つけます。

1. 省略記号を選択します **。[****Get link to team]\(チームへのリンクを取得する\**) を選択します。

     :::image type="content" source="../assets/images/collaboration-control/get-link.png" alt-text="スクリーンショットでは、チームにリンクを取得する方法について説明しています。":::

1. リンクをコピーし、URL から値 `groupId` を記録します。 この値は後の段階で使用し、ソリューションの設定を定義します。

     `https://teams.microsoft.com/l/team/19%3akk_TuKhjXu92yJvg4TZ10S6rouLSCgvHIb5NOOTfRjg1%40thread.tacv2/conversations?groupId=4310f270-1aa5-4089-99f3-47eb3b4d69ad&tenantId=b699419b-e0df-47e3-9909-24076fdcf68b`

ファイルの SharePoint サイト ID とドライブ ID を取得するには、次の手順に従います。

1. ファイル コントロールを使用するには、既存の SharePoint サイトに対して構成するか、新しい SharePoint サイトを作成する必要があります。 新しいサイトを作成するには、「サイト [の作成」を](/sharepoint/create-site-collection)参照してください。

1. 次に、SharePoint サイトの詳細を使用して呼び出すことができるサイト ID とドライブ ID の設定値を取得します。

     1. **サイト ID**: [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) を使用してサインインし、Directory.ReadWrite.All と User.ReadWrite.All にアクセス許可を付与する

         :::image type="content" source="../assets/images/collaboration-control/graph-permissions.png" alt-text="スクリーンショットは、グラフ エクスプローラーを示す例です。":::

     1. ホスト名をホスト名に置き換え、サイト パスへの相対パスを指定し、.`https://graph.microsoft.com/v1.0/sites/{hostname}:/{relative-path-to-site}` 次に例を示します。
         1. サイト URL が = の場合 `https://myhostname.sharepoint.com/sites/MySiteName`
         1. ホスト名 = `myhostname.sharepoint.com`
         1. サイトへの相対パス = `sites/MySiteName`

              :::image type="content" source="../assets/images/collaboration-control/graph-call.png" alt-text="スクリーンショットは、Graph 呼び出しを示す例です。":::

            Graph 呼び出しは次のようになります。 `https://graph.microsoft.com/v1.0/sites/myhostname.sharepoint.com:/sites/MySiteName`.

     1. 受信した応答は、サイトを表す Json オブジェクトです。たとえば、サイト ID は次のようになります `abcdef.sharepoint.com,0abe7394-6fce-4dcc-9884-7eaceb48cd41,8cb86762-16cd-495e-87cb-893cfdf94054`。

     1. サイト ID 値パラメーターを保存します。

     1. **ドライブ ID**: [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) を使用してサインインし、前に保存したサイト ID の値を使用してグラフを呼び出 `https://graph.microsoft.com/v1.0/sites/{site-id}/drives` します。

     1. Json 応答は、配列型またはドライブ オブジェクトのリストのパラメーター値を使用して返されます。 ドキュメント ライブラリの名前と一致する名前パラメーターを持つ Json オブジェクトの Json を調べます。 ドライブ ID パラメーターの値を保存します。

顧客などの組織外のユーザーとの会議を作成し、アプリ内で仮想アクセス機能を使用するには、Bookings ビジネスを提供する必要があります。 詳細については、「[Microsoft Bookings](/microsoft-365/bookings/bookings-overview?view=o365-worldwide&preserve-view=true)」を参照してください。

## <a name="add-settings-to-your-collaboration-manager-app"></a>Collaboration Manager アプリに設定を追加する

設定を適用し、Power Apps でアプリの共同作業機能を調べるには、前に作成したアプリケーションを開きます。 既存のレコードを選択したり、新しいレコードを作成したりできるビュー ページが表示されます。 最初にレコードを開くか作成します。

アプリケーション用に前に保存した設定 ID を追加する必要があります。

|Settings|使用元|
|---|---|
|グループ ID|タスク、内部会議、承認。|
|Bookings ビジネス ID|Bookings を使用した外部会議 |
|サイト ID|SharePoint ファイル |
|ドライブ ID|SharePoint ファイル|

### <a name="add-settings-for-tasks-meetings-and-files"></a>タスク、会議、ファイルの設定を追加する

1. コントロールを起動すると、ウィンドウが次のように表示されます。

     :::image type="content" source="../assets/images/collaboration-control/launch-window.png" alt-text="スクリーンショットは、コントロール ウィンドウを示す例です。":::

1. [ **構成] を** 選択し、[全般] タブに移動してグループ ID を追加します。

     :::image type="content" source="../assets/images/collaboration-control/groupid-general.png" alt-text="スクリーンショットでは、[全般] タブでグループ ID を追加する方法について説明します。":::

1. [ファイル] タブを開き、サイト ID とドライブ ID を追加します。

     :::image type="content" source="../assets/images/collaboration-control/files-tab.png" alt-text="スクリーンショットでは、[ファイル] タブにサイト ID とドライブ ID を追加する方法について説明します。":::

Notes コントロールには設定値は必要ありません。 これで、アプリケーションでタスクや会議などのエンティティを作成できるようになりました。 コントロールの起動と保存で問題が発生している場合は、設定値を再確認します。

## <a name="explore-your-new-collaboration-manager-app"></a>新しいCollaboration Manager アプリを調べる

以下のセクションでは、タスク、ノート、会議、ファイル、承認の各コントロールを使用する方法について説明します。

### <a name="create-tasks"></a>タスクの作成

[タスク] タブで共同作業を確認するには、[タスク] タブを選択すると、ユーザーが完了するために必要なすべての関連タスクを追加できる空のページが開きます。

1. チームの新しいタスクを作成するには、[ **タスクの追加]** を選択します。 タスクに関する詳細を指定し、チームの関連するユーザーに割り当て、[保存] を選択できるダイアログが開きます。

     :::image type="content" source="../assets/images/collaboration-control/add-task.png" alt-text="スクリーンショットでは、タスクを追加する方法について説明しています。":::

1. 保存されたタスクがタスクの一覧に表示されます。

1. すべてのタスクはMicrosoft Plannerによってサポートされます。 ユーザーは、Microsoft Teams 内のタスク アプリを使用して、割り当てられているすべてのタスクを表示できます。 作業を開始するには、省略記号 **...** を選択します。 Teams の左側のウィンドウに表示されます。 Planner と To Do でタスクを検索して選択します。

     :::image type="content" source="../assets/images/collaboration-control/tasks-planner.png" alt-text="スクリーンショットは、Planner と To Do によるタスクの例です。":::

1. Planner と To Do アプリでタスクを開いた後、ユーザーはアプリの **[自分に割り当てる** ] セクション内で、アプリで作成されたすべてのタスクを表示できます。 ユーザーは、タスクの詳細を表示したり、添付ファイルを追加したり、完了としてマークしたりできます。

### <a name="create-notes"></a>メモを作成する

メモを作成するには、アプリから [ **メモ** ] タブを選択します。これにより、ユーザーが関連情報を入力できる空の画面にリダイレクトされます。 新しいメモを追加するには、[ **新しいメモ**] を選択します。
ノートに関連する詳細を追加したら、[ **保存]** を選択します。

### <a name="create-meetings"></a>会議を作成する

レコード **の [会議** ] タブを選択して、内部会議と外部会議の両方をスケジュールします。

内部会議をスケジュールするには、[ **新しい** 会議] ボタンの横にあるドロップダウンを選択し、[ **内部会議**] を選択します。

:::image type="content" source="../assets/images/collaboration-control/new-meeting-tab.png" alt-text="スクリーンショットでは、内部会議をスケジュールする方法について説明しています。":::

> [!NOTE]
>
> アプリに対して有効な設定で Microsoft Booking を構成している場合は、カスタマー ブッキングが有効になります。

**[新しい会議**] ダイアログで、ユーザーは会議に関する関連情報を入力し、[**保存]** を選択できます。 会議が会議の一覧に表示されます。

:::image type="content" source="../assets/images/collaboration-control/new-meeting.png" alt-text="スクリーンショットでは、新しい会議をスケジュールする方法について説明しています。":::

顧客と外部会議をスケジュールするには、[ **新しい会議** ] ボタンの横にあるドロップダウンを選択し、 **Customer Booking** を選択します。 **[新しい会議**] ドロップダウンで **[顧客の予約**] オプションを使用できない場合は、アプリが [設定] でMicrosoft Bookingsするように構成されていて、ユーザーが Bookings 管理者ロールを持っているかどうかを確認します。 詳細については、「 [Bookings にスタッフを追加する」を](/microsoft-365/bookings/add-staff?view=o365-worldwide&preserve-view=true)参照してください。 Bookings ビジネス内にサービスを追加することで、予約の種類を追加できます。

:::image type="content" source="../assets/images/collaboration-control/customer-booking.png" alt-text="スクリーンショットでは、顧客の予約をスケジュールする方法について説明しています。":::

ユーザーは、社内会議と顧客の予約の両方を自分の会議リストに表示できます。 会議の開始後、ユーザーは [ **参加** ] ボタンを選択して参加できます。このボタンを選択すると、Microsoft Teams で直接会議が開きます。

会議は Outlook によってサポートされるため、ユーザーは Bookings に移動するか、Outlook カレンダーに移動して、1 つの予定表に一覧表示されたすべての会議を表示できます。 内部会議は共有予定表に一覧表示されます。

共有予定表を Outlook に追加する手順を次に示します (省略可能)。

1. リボンの [ホーム] タブの [予定表の管理] セクションで、[予定表を開く] > [共有予定表を開く] を選択します。

1. [共有予定表を開く] ダイアログで、ユーザーの名前を入力します。 探しているユーザーを選択し、[OK] を選択します。

左側のウィンドウの [共有予定表] に、ユーザーの名前を含む追加の予定表が表示されます。

:::image type="content" source="../assets/images/collaboration-control/customer-booking.png" alt-text="スクリーンショットでは、顧客の予約をスケジュールする方法について説明しています。":::

### <a name="add-files"></a>ファイルの追加

アプリケーションの [**ファイル**] タブを開き、[**アップロード**] を選択して、OneDrive for Businessまたはコンピューターからファイルをアップロードします。 ファイルが正常にアップロードされると、メイン リスト ビューが自動的に更新され、リスト内のファイルが表示されます。

:::image type="content" source="../assets/images/collaboration-control/meeting-calendar.png" alt-text="スクリーンショットでは、共有予定表を開く方法について説明しています。":::

### <a name="approvals"></a>承認

承認により、ユーザーはレコードで作業するときに他のユーザーにサインアウトを要求できます。 たとえば、承認を要求してタスクを完了したり、レコードを閉じたりします。

1. アプリケーションの **[承認** ] タブに移動します。

1. 承認要求がない場合、ユーザーには次の画面が表示されます。

      :::image type="content" source="../assets/images/collaboration-control/no-approvals.png" alt-text="スクリーンショットは、承認要求を示さない例です。":::

1. **[新しい承認要求**] を選択して、承認要求フォームを開きます。

      :::image type="content" source="../assets/images/collaboration-control/approval-request-form.png" alt-text="スクリーンショットは、新しい承認要求フォームを示す例です。":::

1. [承認要求] フォームで、必要なフィールドに入力し、[ **送信**] を選択して要求を作成し、一覧に追加します。

      :::image type="content" source="../assets/images/collaboration-control/approvals-list.png" alt-text="スクリーンショットは、承認の一覧を示す例です。":::

1. 承認を選択して詳細を表示します。

承認の詳細については、「 [承認の作成」を](https://support.microsoft.com/en-us/office/create-an-approval-6548a338-f837-4e3c-ad02-8214fc165c84)参照してください。
