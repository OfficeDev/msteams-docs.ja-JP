---
title: Microsoft Teams でコラボレーション コントロールを使用してアプリを展開する
author: surbhigupta
description: このモジュールでは、Microsoft Teams でコラボレーション コントロールを使用してアプリを展開する方法と、他のユーザーがアプリを使用できるようにする方法について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 75a2aa9d09247ac152c31df02f2bb8d4fb507619
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027306"
---
# <a name="deploy-collaboration-controls-to-microsoft-teams"></a>コラボレーション コントロールを Microsoft Teams に展開する

コラボレーション コントロールは現在、Microsoft Teams 内で最適に機能します。 個人用アプリとタブ アプリの両方として Teams アプリ内に埋め込むことができる新しいアプリを作成できます。

> [!NOTE]
> 現在、コラボレーション コントロールは [、パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

## <a name="configure-the-app-for-teams"></a>Teams 用にアプリを構成する

[モデル駆動型アプリケーションの作成](~/samples/app-with-collaboration-controls.md#create-a-model-driven-application)で作成したアプリには、左側のウィンドウが 1 つだけあり、複雑なコマンドはありません。 そのため、Teams にアプリを追加する前に、左側のウィンドウを非表示にして、よりわかりやすいヘッダー ビューを作成できます。

> [!NOTE]
> 左側のウィンドウと高密度ヘッダーをユーザーに表示する場合は、次の手順を有効にしないでください。

これを行うには、Power Apps の **新しいアプリ** 設定を使用します。

1. 左側のウィンドウの **[ソリューション** ] に移動します。

1. ソリューションの一覧の一番下に移動し、 **既定のソリューション** を選択します。

1. 定義を検索 **して選択します**。

     :::image type="content" source="../assets/images/collaboration-control/settings-defnition.png" alt-text="定義の設定":::

1. 設定定義の一覧からナビゲーション バーを検索して **非表示にする** を選択します。 これにより、アプリケーションの左側のウィンドウが非表示になります。

     :::image type="content" source="../assets/images/collaboration-control/hide-the-nav-bar.png" alt-text="ナビゲーション バーを非表示にする":::

1. 編集ウィンドウのアプリケーションの右下に、「 **アプリ値の設定**」というタイトルのセクションがあります。 モダン アプリ デザイナーを使用してアプリを作成した場合、アプリが一覧に表示されます。 アプリの下にある **[新しいアプリの値** ] を選択します。

1. 値を **[いいえ]** から **[はい**] に変更します。

     :::image type="content" source="../assets/images/collaboration-control/value-to-yes.png" alt-text="値を yes に変更する":::

1. **[保存] を選択します。**

1. 設定定義の一覧から **アプリ高密度ページ ヘッダー** を検索して選択し、プロセスを繰り返します。

     :::image type="content" source="../assets/images/collaboration-control/density-page-header.png" alt-text="密度ページ ヘッダー":::

1. [ **ソリューションに戻る] を選択します**。

     :::image type="content" source="../assets/images/collaboration-control/default-solution.png" alt-text="既定のソリューション":::

1. [ **すべてのカスタマイズの発行]** を選択して、完了したすべての作業を公開します。

     :::image type="content" source="../assets/images/collaboration-control/publish-cusomization.png" alt-text="すべてのカスタマイズを発行する":::

## <a name="add-the-app-to-microsoft-teams-app-catalog"></a>Microsoft Teams アプリ カタログにアプリを追加する

設定が定義されたので、Microsoft Teams にアプリを追加できるようになりました。 まず、Power Apps Maker ポータルの **[アプリ**] ページに移動し、作成したアプリを見つけて省略記号を選択します **。...**

アプリを Teams に追加するには、[Teams **に追加]** を選択します。

:::image type="content" source="../assets/images/collaboration-control/add-to-teams.png" alt-text="Teams に追加する":::

**[Teams に追加]** を選択するとダイアログが開き、詳細を確認して **[アプリのダウンロード**] を選択すると、Microsoft Teams アプリ マニフェストがデバイスに保存されます。

:::image type="content" source="../assets/images/collaboration-control/colab-manager-inspection.png" alt-text="スクリーンショットは、コラボレーション マネージャーの検査を示す例です":::

アプリを Teams にアップロードするには、「 [Team でアプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)」を参照してください。

## <a name="enable-others-to-use-your-application"></a>他のユーザーがアプリケーションを使用できるようにする

ユーザーがコラボレーション コントロールを使用して構築されたデプロイされたCollaboration Manager アプリケーションを実行できるようにするには、次のものが必要です。

* コラボレーション チームを作成する
* チームにメンバーを追加する
* セキュリティ ロールを作成する
* チーム メンバーにセキュリティ ロールを割り当てる

### <a name="create-a-collaboration-team"></a>コラボレーション チームを作成する

1. [Power Platform 管理センター](https://admin.powerplatform.microsoft.com/environments)にサインインします。

     1. アプリがデプロイされている環境を選択します。
     1. [**ユーザーの** + **アクセス許可****の設定] を選択します** > 。
     1. [ **Teams] を選択します**。

1. ページの上部にある **[+ チームの作成** ] ボタンを選択します。

1. すべての必須フィールドを追加します。
     1. **チーム名:** 名前が部署内で一意であることを確認します。
     1. **説明：** チームの説明を入力します。
     1. **部署:** ドロップダウン リストから部署を選択します。
     1. **管理者：** 文字を入力して、管理者として割り当てる組織内のユーザーを検索します。
     1. **チームの種類:** チームの種類を選択します。 次の手順では、ドロップダウン リストから [所有者] を選択したことを前提としています。 他のチームの種類 (Microsoft 365 チームとMicrosoft Azure Active Directory チーム) では、Azure Active Directory からチーム メンバーが自動的に設定されます。

         :::image type="content" source="../assets/images/collaboration-control/new-team.png" alt-text="新しいチーム":::

     1. チーム名を書き留めます。 このチームをレコードの所有者として割り当てるには、後でこれが必要になります。

     1. **[次へ**] を選択します。

### <a name="add-members-to-the-team"></a>チームにメンバーを追加する

> [!NOTE]
> チームの種類が Azure Active Directory または Microsoft 365 の場合、チームにメンバーを追加する必要はありません。

1. チームを選択し、[ **チーム メンバーの管理**] を選択します。

1. 新しいチーム メンバーを追加するには、[ **+ チーム メンバーの追加]** を選択し、追加する組織のユーザーを選択します。

     :::image type="content" source="../assets/images/collaboration-control/add-team-members.png" alt-text="スクリーンショットでは、チーム メンバーを追加する方法について説明しています":::

1. チーム メンバーを削除するには、ユーザーを選択し、[削除] を選択 **します**。

### <a name="create-a-security-role"></a>セキュリティ ロールを作成する

1. アプリがデプロイされている環境で [ユーザーの **設定** >  + **] アクセス許可** を選択します。

1. [ **セキュリティ ロール**] を選択します。

     :::image type="content" source="../assets/images/collaboration-control/users-permission.png" alt-text="ユーザーのアクセス許可":::

1. ページの左上にある **[新しいロール** ] を選択すると、新しいページが開きます。

1. [ **詳細] タブ** で、セキュリティ ロールの名前を指定します。

1. **[カスタム エンティティ] タブに** 移動します。

     1. コラボレーション エンティティ、 **コラボレーション マップ**、 **コラボレーション メタデータ**、およびコラボレーション ルートごとに組織のアクセス許可 (完全な緑色の円) を付与 **します**。

         :::image type="content" source="../assets/images/collaboration-control/collab-map.png" alt-text="コラボレーション マップ":::

1. **[保存して****閉じる**] を選択します。

### <a name="assign-security-roles"></a>セキュリティ ロールの割り当て

1. アプリがデプロイされている環境で [ユーザーの **設定** >  + **] アクセス許可** を選択します。

1. **[Teams**] を選択し、コラボレーション チームの作成で作成 [したチームを選択します](#create-a-collaboration-team)。

1. ヘッダーから [ **セキュリティ ロールの管理** ] を選択します。

     :::image type="content" source="../assets/images/collaboration-control/edit-team.png" alt-text="チームを編集する":::

1. [セキュリティ ロールで作成されたロールを選択します](#create-a-security-role)。

1. **[保存]** を選択します。

ロールの特権の詳細については、 [環境内のユーザー セキュリティの構成に関するページを](/power-platform/admin/database-security)参照してください。
