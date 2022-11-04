---
title: クラウドにデプロイする
author: MuyangAmigo
description: このモジュールでは、クラウド、Azure、または SharePoint にアプリをデプロイし、Teams Toolkit を使用して Teams アプリをデプロイする方法について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 17d4d1d80f9ffd634e2fdae815b8504bb6c0ca99
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833136"
---
# <a name="deploy-teams-app-to-the-cloud"></a>Teams アプリをクラウドに展開する

Teams Toolkit を使用すると、アプリケーションのフロントエンドとバックエンドのコードを Azure のプロビジョニング済みクラウド リソースにデプロイまたはアップロードできます。

::: zone pivot="visual-studio-code"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio-code"></a>Visual Studio Code を使用して Teams アプリをクラウドにデプロイする

次をクラウドにデプロイできます。

* フロントエンド アプリケーションなどのタブは Azure Storage にデプロイされ、静的 Web ホスティングまたは SharePoint サイト用に構成されます。
* バックエンド API は、Azure Functionsにデプロイされます。
* ボットまたはメッセージ拡張機能は、Azure App Serviceにデプロイされます。

  > [!NOTE]
  > Azure クラウドにアプリ コードをデプロイする前に、 [クラウド リソースのプロビジョニング](provision.md)を正常に完了する必要があります。

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Teams Toolkit を使用して Teams アプリを展開する

「はじめに」ガイドは、Teams Toolkit を使用してデプロイするのに役立ちます。 次を使用して、Teams アプリをデプロイできます。

* [アプリを Azure にデプロイする](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [アプリを SharePoint にデプロイする](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Teams アプリのワークロードの詳細

| Teams アプリのワークロード | ソース コード | 成果物をビルドする| ターゲット リソース |
|-------------|----------|---------------|---------------|
|Reactを含むタブ </br> フロントエンド ワークロード| `yourProjectFolder/tabs`| `tabs/build` |Azure Storage |
|SharePoint を使用したタブ </br> フロントエンド ワークロード | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint アプリ カタログ |
|Azure Functionsの API </br> バックエンド ワークロード | `yourProjectFolder/api`| 対象外 |Azure Functions |
|ボットとメッセージ拡張機能 </br> バックエンド ワークロード | `yourProjectFolder/bot` | 対象外 | Azure App Services |

> [!NOTE]
> プロジェクトに Azure API 管理リソースを含め、デプロイをトリガーすると、Azure Functionsの API を Azure API 管理サービスに発行できます。

::: zone-end

::: zone pivot="visual-studio"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>Visual Studio を使用して Teams アプリをクラウドに展開する

Visual Studio では、次のアプリを展開できます。

* フロントエンド アプリケーションなどのタブ アプリは、静的 Web ホスティング用に構成された Azure Storage にデプロイされます。
* Azure Functions トリガーを含む通知ボット アプリは、Azure Functionsにデプロイできます。
* ボット アプリまたはメッセージ拡張機能は、Azure アプリ Services にデプロイできます。

展開後、使用を開始する前に、Teams クライアントまたは Web ブラウザーでアプリをプレビューできます。

## <a name="deploy-teams-app-using-teams-toolkit"></a>Teams ツールキットを使用して Teams アプリを展開する

1. Visual Studio を開きます。
1. **[新しいプロジェクトを作成する]** を選択するか、一覧から既存のプロジェクトを開きます。
1. **プロジェクト MyTeamsApp1** > **Teams Toolkit** > **クラウドへのデプロイを** 右クリックします。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="[クラウドに展開する]":::

   > [!NOTE]
   > このシナリオでは、プロジェクト名は MyTeamsApp1 です。

1. 確認ダイアログで **[展開]** を選択します。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="[クラウドに展開する] の確認ダイアログ":::

   デプロイ プロセスが完了すると、正常にデプロイされたことを確認するポップアップが表示されます。 出力ウィンドウで状態を確認することもできます。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="[クラウドに展開する] のポップアップ":::

### <a name="preview-your-app"></a>アプリをプレビューする

アプリをプレビューするには、まず Zip アプリ パッケージを作成し、Teams クライアントにサイドロードする必要があります。

1. **[Project** > **Teams Toolkit** > **Zip App Package**] を選択します。
1. [ **ローカル]** オプションまたは [ **Azure 用** ] オプションを選択して Teams アプリ パッケージを生成します。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package1.png" alt-text="Teams アプリ パッケージを作成する":::

**Teams クライアントでアプリをプレビューするには**

1. [ **Teams での Project** > **Teams ツールキット** > **プレビュー] を選択します**。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams2.png" alt-text="Teams クライアントで Teams アプリをプレビューする":::

   これで、アプリが Teams にサイドロードされます。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="Teams クライアントで Teams アプリをサイドロードする":::

アプリをプレビューするもう 1 つの方法:

1. **[ソリューション エクスプローラー**] でプロジェクト **MyTeamsApp1** を右クリックします。
1. **[Teams ツールキット** > **プレビュー]** を選択して、Web ブラウザーで Teams アプリを起動します。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="Web ブラウザーで Teams アプリをプレビューする":::

   > [!NOTE]
   > 同じメニュー オプションが [プロジェクト] メニューでも使用できます。

   これで、アプリが Teams にサイドロードされます。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="Teams クライアントで Teams アプリをサイドロードする":::

::: zone-end

## <a name="see-also"></a>関連項目

* [Azure クラウド サービスを作成してデプロイする](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [複数機能の Teams アプリを作成する](add-capability.md)
* [Microsoft Teams アプリにクラウド リソースを追加する](add-resource.md)
* [Visual Studio で新しい Teams アプリを作成する](create-new-project.md#create-new-teams-app-in-visual-studio)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Visual Studio を使用して Teams アプリをローカルでデバッグする](debug-local.md#debug-your-teams-app-locally-using-visual-studio)
