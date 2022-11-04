---
title: Teams Toolkit を調べる
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit の探索について学習します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 0fa31c52b206738cfb174519fc6d3c445b604a8e
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833129"
---
# <a name="explore-teams-toolkit"></a>Teams Toolkit を調べる

このドキュメントでは、Visual Studio Code と Visual Studio の両方について、Teams Toolkit のさまざまな UI 要素と説明と基本的な使用方法について説明します。

::: zone pivot="visual-studio-code"

## <a name="teams-toolkit-for-visual-studio-code-basic-ui-elements"></a>Teams Toolkit for Visual Studio Code の基本的な UI 要素

Teams Toolkit のインストール後、次の図に示すように Teams Toolkit UI が表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/overview1.png" alt-text="Teams Toolkit の概要":::

| シリアル番号 | UI 要素 | 定義 |
| --- | --- |
| 1 | **はじめに** | Teams Toolkit を調べる。 |
| &nbsp; | **チュートリアル** | さまざまなチュートリアルにアクセスします。 |
| &nbsp; | **ドキュメント** | Microsoft Teams 開発者向けドキュメントにアクセスします。 |
| 2 | **新しい Teams アプリを作成する** | 要件に基づいて新しい Teams アプリを作成します。 |
| 3 | **サンプルの表示** | 既存のサンプルに基づいてさまざまな種類のアプリをビルドします。 |
| 4 | **フォルダーを開く** | 既存の Teams アプリを開きます。 |
| 5 | **新しいファイル** | 新しいファイルを作成します。 |
| &nbsp; | **ファイルを開く** | 既存のファイルを開きます。 |
| &nbsp; | **フォルダーを開く** | 既存のフォルダーを開きます。 |
| 6 | **最近** | 最近使用したファイルを表示します。 |

### <a name="exploring-the-teams-toolkit-task-pane"></a>Teams Toolkit 作業ウィンドウの探索

Teams Toolkit の作業ウィンドウから、その他の UI 要素を調べることができます。 作業ウィンドウは、Teams Toolkit を使用してアプリを作成した後にのみ表示されます。 次のビデオは、新しい Teams アプリを作成するプロセスについて理解するのに役立ちます。このプロセスの後、Teams Toolkit で作業ウィンドウを表示できます。

   ![Teams アプリを作成する](~/assets/videos/javascript-tab-app1.gif)

新しい Teams アプリを作成すると、左側のパネルにアプリのディレクトリ構造が表示され、右側のパネルに readme ファイルが表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/first-page.png" alt-text="Teams Toolkit の最初のページ":::

Teams Toolkit UI のツアーを見てみましょう。

 Visual Studio Code ツール バーでは、次のアイコンが Teams Toolkit に関連します。

| アイコン | 説明 |
| --- | --- |
| **エクスプローラー** :::image type="icon" source="../assets/images/teams-toolkit-v2/file-explorer-icon.PNG":::  | アプリのディレクトリ構造を表示するには。 |
| **実行とデバッグ** :::image type="icon" source="../assets/images/teams-toolkit-v2/run-debug-icon.PNG":::  | ローカルまたはリモートのデバッグ プロセスを開始する。 |
| **Teams ツールキット** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: | Teams Toolkit で作業ウィンドウを表示するには。 |

作業ウィンドウから、次のセクションを確認できます。

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/accounts1.png" alt-text="accounts セクション":::
   :::column-end:::
   :::column span="":::

        Teams アプリを開発するには、次のアカウントが必要です。
        
        * **M365 にサインインする**: アプリをビルドするために、有効な E5 サブスクリプションで Microsoft 365 アカウントを使用します。

        * **Azure にサインインする: Azure** にアプリをデプロイするために Azure アカウントを使用します。 開始する前に、[無料の Azure アカウントを作成](https://azure.microsoft.com/free/) できます。
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/environment1.png" alt-text="環境セクション":::
   :::column-end:::
   :::column span="":::

        Teams アプリをデプロイするには、次の環境が必要です。
        
       * **local**: ローカル コンピューター環境の構成を使用して、既定のローカル環境にアプリをデプロイします。

        * **dev**: リモート環境またはクラウド環境構成を使用して、既定の開発環境にアプリをデプロイします。 必要に応じて、より多くの環境を作成できます。
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/development.png" alt-text="開発セクション":::
   :::column-end:::
   :::column span="":::

        Teams アプリを作成してカスタマイズするには、次の機能が必要です。
        
       * **新しい Teams アプリを作成** する: ツールキット ウィザードを使用して、アプリ開発用のプロジェクト スキャフォールディングを準備します。

        * **サンプルの表示**: Teams Toolkit のサンプル アプリのいずれかを選択します。 ツールキットは GitHub からアプリ コードをダウンロードし、サンプル アプリをビルドできます。
        
        * **機能の追加**: 開発プロセス中に他の必要な Teams 機能を Teams アプリに追加し、アプリに適したオプションのクラウド リソースを追加します。
       
        * **マニフェスト ファイルの編集**: Teams アプリと Teams クライアントの統合を編集します。
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deployment1.png" alt-text="[デプロイ] セクション":::
   :::column-end:::
   :::column span="":::

        Teams アプリをプロビジョニング、デプロイ、発行するには、次の機能が必要です。
        
        * **クラウドでのプロビジョニング**: アプリケーションに Azure リソースを割り当てます。 Teams Toolkit は Azure Resource Manager と統合されています。

        * **Zip Teams メタデータ パッケージ: Teams** または開発者ポータルにアップロードできるアプリ パッケージを作成します。 アプリ マニフェストとアプリ アイコンが含まれています。
        
        * **クラウドへのデプロイ**: ソース コードを Azure にデプロイします。
       
        * **Teams に発行する**: 開発したアプリを発行し、個人用、チーム、チャネル、組織などのスコープに配布します。
        
        * **Teams 用開発者ポータル**: 開発者ポータルを使用して、Teams アプリを構成および管理します。 
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/help-and-feedback1.png" alt-text="[ヘルプとフィードバック] セクション":::
   :::column-end:::
   :::column span="":::

        Teams Toolkit の詳細にアクセスするには。 次のドキュメントとリソースが必要です。
        
        * **はじめに**: Visual Studio Code 内で Teams Toolkit の概要ヘルプを表示します。

        * **チュートリアル**: 選択すると、さまざまなチュートリアルにアクセスできます。
        
        * **ドキュメント**: Microsoft Teams 開発者向けドキュメントにアクセスする場合に選択します。
       
        * **GitHub で問題を報告する: GitHub** ページにアクセスして問題を発生させる場合に選択します。
   :::column-end:::
:::row-end:::

::: zone-end

::: zone pivot="visual-studio"

## <a name="explore-teams-toolkit-for-visual-studio"></a>Teams Toolkit for Visual Studio を調べる

Teams Toolkit をインストールした後、次の 2 つの方法で Teams Toolkit オプションを表示できます。

# <a name="project"></a>[プロジェクト](#tab/prj)

Teams Toolkit には **、[プロジェクト**] でアクセスできます。

1. **[Project** > **Teams Toolkit] を** 選択します。
1. さまざまな Teams ツールキット オプションにアクセスできるようになりました。

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu_1.png" alt-text="Teams ツールキットの操作メニュー":::

# <a name="solution-explorer"></a>[ソリューション エクスプローラー](#tab/solutionexplorer)

   Teams Toolkit には **、ソリューション エクスプローラー** でアクセスできます。

1. [**表示** > **ソリューション エクスプローラー**] を選択して、パネルソリューション エクスプローラー表示します。
1. **プロジェクト** を右クリックします。
1. [ **Teams Toolkit** ] を選択して、さまざまな Teams Toolkit オプションにアクセスします。

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu1_1.png" alt-text="プロジェクトからの Teams ツールキットの操作":::

   > [!NOTE]
   > このシナリオでは、プロジェクト名は **MyTeamsApp1** です。

---

Teams プロジェクトを作成したら、Teams Toolkit for Visual Studio で次の機能を実行できます。

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-menu-options.png"alt-text="[プロジェクト] メニューからの Teams ツールキット操作":::

|関数  |説明  |
|---------|---------|
|Teams アプリの依存関係を準備する     |ローカル デバッグを実行する前に、この手順を実行します。これにより、ローカル デバッグの依存関係を設定し、Teams プラットフォームに Teams アプリを登録するのに役立ちます。 Microsoft 365 アカウントが必要です。 詳細については、「[Visual Studio を使用して Teams アプリをローカルでデバッグする](debug-local.md)」を参照してください。         |
|マニフェスト ファイルを開く     |Teams マニフェスト ファイルを開くには、パラメーターにカーソルを合わせて値をプレビューします。 詳細については、「[Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)」を参照してください。         |
|Teams 開発者ポータルでマニフェストを更新する     |マニフェスト ファイルを更新した後でなければ、プロジェクト全体を再度展開することなくマニフェスト ファイルを Azure に再展開することはできません。 このコマンドを使用して、変更をリモートに更新します。 詳細については、「[Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)」を参照してください。       |
|クラウドへのプロビジョニング     |このオプションは、Teams アプリをホストする Azure リソースを作成するのに役立ちます。 詳細については、「[Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)」を参照してください。        |
|クラウドに展開する     |このオプションを使用すると、"クラウドへのプロビジョニング" を行ったときに作成された Azure リソースにコードをコピーできます。 詳細については、「[Visual Studio を使用して Teams アプリをクラウドに展開する](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)」を参照してください。        |
|Teams でプレビュー     |このオプションを選択すると、Teams Web クライアントが起動し、ブラウザーで Teams アプリをプレビューできます。         |
|Zip アプリ パッケージ     |このオプションでは、プロジェクトの下の `Build` フォルダーに Teams アプリ パッケージを生成します。 パッケージを Teams クライアントにアップロードし、Teams アプリを実行できます。         |

::: zone-end

## <a name="see-also"></a>関連項目

* [Teams Toolkit のインストール](install-Teams-Toolkit.md)
* [Teams Toolkit を使用して新しい Teams アプリを作成する](create-new-project.md)
* [Microsoft Teams Toolkit を使用してアプリを構築する準備をする](build-environments.md)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [Visual Studio で新しい Teams アプリを作成する](create-new-project.md#create-new-teams-app-in-visual-studio)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)

<!--  
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ui-elements.png" alt-text="UI Elements":::

|Section|Features|Details
|---------|---------|--------|
| **1. ACCOUNTS** | &nbsp; | &nbsp; |
| &nbsp; |Microsoft 365 account|  Use your Microsoft 365 account with a valid E5 subscription for building your app.|
| &nbsp; | Azure Account |  Use your Azure account for deploying app on Azure. You can [create a free Azure account](https://azure.microsoft.com/free/) before you start.|
|**2.ENVIRONMENT** |  &nbsp; | &nbsp;|
| &nbsp; |Local |Deploy your app in the default local environment with local machine environment configurations.|
| &nbsp; | Dev |Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need.|
| **3.DEVELOPMENT** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Teams Toolkit helps you to create and customize your Teams app project that makes the Teams app development work simpler. Create a new Teams app helps you to start with Teams app development by creating new Teams project using Teams Toolkit either by using **Create new project**|
| &nbsp; | View Samples | Select any of Teams Toolkit's sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app.|
| &nbsp; | Add Features | It helps you to add additional Teams capabilities such as **Tab** or **Bot** or **Message extension** or **Command bot** or **Notification bot**, or **SSO enabled tab** optionally add Azure resources such as **Azure SQL Database** or **Azure Key Vault**, or **Azure function** or **Azure API Management** which fits your development needs to your current Teams app. You can also add **API connection** or **Single Sign-on** or **CI/CD workflows** for your Teams app.
| &nbsp; | Edit Manifest file | It helps you customize manifest file based on the app requirements |
| **4.DEPLOYMENT** | &nbsp; | &nbsp; |
| &nbsp;| Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager.|
| &nbsp; | Zip Teams metadata package| Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons. |
| &nbsp; | Deploy to the cloud| Deploy the source code to Azure.|
| &nbsp; | Publish to Teams| Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization.|
| &nbsp; | Developer Portal for Teams| It is the primary tool for configuring, distributing, and managing your Microsoft Teams apps. You can collaborate with colleagues on your app, set up runtime environments, and much more. |
| **5.HELP AND FEEDBACK** | &nbsp; | &nbsp; |
| &nbsp; | Get Started |  View the Teams Toolkit Get started help within Visual Studio Code.|
| &nbsp; | Tutorials| Select to access different tutorials.|
| &nbsp; | Documentation| Select to access the Microsoft Teams Developer Documentation.|
| &nbsp; | Report issues on GitHub| It helps to get **Quick support** from product expert. Browse the existing issues before you create a new one, or visit [StackOverflow tag `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) to submit feedback.|
| **6.Explorer** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | It helps to view the directory structure of your app.|
| **7.Run and Debug** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | To start the local or remote debug process.|
-->
