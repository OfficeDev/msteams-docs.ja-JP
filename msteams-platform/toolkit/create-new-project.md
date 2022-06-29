---
title: Teams Toolkit を使用して新しい Teams アプリを作成する
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit を使用して新しい Teams アプリを作成し、ビュー サンプルを使用して新しい Teams アプリを作成する方法について説明します
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 1737c55598d5963a77317a0b37869275f96a902d
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503754"
---
# <a name="create-a-new-teams-app-using-teams-toolkit"></a>Teams Toolkit を使用して新しい Teams アプリを作成する 

Teams Toolkit を使用して新しい Teams アプリを作成するには、次のいずれかのオプションを選択できます。

* [[新しい Teams アプリを作成]](create-new-project.md#create-a-new-teams-app)
* [[サンプルを見る]](create-new-project.md#create-a-new-teams-app-using-view-samples)

## <a name="create-a-new-teams-app"></a>新しい Teams アプリを作成する

1. Visual Studio Code を開きます。
1. Visual Studio Code のサイド バーで Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG" border="true"::: アイコンを選択します。
1. **[新しい Teams アプリを作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar.png" alt-text="Teams ツールキットサイドバー":::

1. **新しい Teams アプリを作成する** または **サンプルから開始** を選択できます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/select-create-app.png" alt-text="アプリを作成する":::

1. **新しい Teams アプリを作成する** を選択した場合、シナリオベースの Teams アプリ、Basic Teams アプリ、拡張 Teams アプリの 3 つのカテゴリのテンプレートが Microsoft 365 に表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-capabilities.png" alt-text="Teams アプリのCapabilties":::

1. 少なくとも 1 つのオプションを選択すると、Teams アプリの作成を開始できます。

## <a name="create-a-new-teams-app-using-view-samples"></a>[サンプルを見る] を使用して、新しい Teams アプリを作成する

**[サンプルを見る]** を検索して既存のサンプルを選択すると、新しいアプリを作成することができます。 選択したサンプルには、Azure バックエンドを使用した To Do リストや、Microsoft Graph ツールキットとの統合など、一部の機能が既にある場合があります。

 1. Microsoft Visual Studio Code から **[Teams ツールキット]** を開きます。
 1. ツリービューで **[開発]** セクションを選択します。
 1. **[サンプルを見る]** を選択します。 

    :::image type="content" source="../assets/images/teams-toolkit-v2/view-samples.png" alt-text="[サンプルを見る]":::

    次の図に示すように、サンプル ギャラリーが表示されます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/sample-gallery.png" alt-text="サンプル ギャラリー":::

  サンプル ギャラリーは次のように調べることができます。

  1. 詳細情報を参照するサンプルを選択します。
  1. 各サンプルの情報ページで **作成** を選択してダウンロードします。 
  1. サンプルをダウンロードした後に自動的に開く手順に従って、アプリをローカルまたはリモートで実行して Teams Web クライアントでプレビューします。
  1. サンプルをダウンロードしない場合は、**View on GitHub** を選択して、GitHub サンプル リポジトリでサンプルを開き、ソース コードを参照できます。

## <a name="step-by-step-guides-using-teams-toolkit"></a>Teams ツールキットを使用したステップバイステップ ガイド

* [Blazor を使用して Teams アプリを構築する](../sbs-gs-blazorupdate.yml)
* [React](../sbs-gs-javascript.yml) を使用して JavaScript で Teams アプリを構築する
* [SPFx](../sbs-gs-spfx.yml) を使用して Teams アプリを構築する
* [C# または .NETを使用して Teams アプリをビルドする](../sbs-gs-csharp.yml)
* [Teams への通知の送信](../sbs-gs-notificationbot.yml)
* [ビルド コマンド ボット](../sbs-gs-commandbot.yml)

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリをクラウドに展開する](deploy.md)
* [Teams アプリの発行](../concepts/deploy-and-publish/appsource/publish.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)
