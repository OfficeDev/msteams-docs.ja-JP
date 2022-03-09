---
title: Teams Toolkit概要
author: zyxiaoyuer
description: 概要Teams Toolkit、インストール、Teams Toolkit機能のツアー Toolkitします。
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: fd3a72d3738fb835a5ef1e8092d1e59c06dad454
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398821"
---
# <a name="teams-toolkit-overview"></a>Teams Toolkit概要

> [!NOTE]
> 現時点では、この機能はパブリック開発者 **プレビューでのみ利用** できます。

Teams Toolkit Microsoft Visual Studio コードを使用すると、統合 ID、クラウド ストレージへのアクセス、Microsoft Graph からのデータ、Azure および Microsoft 365 の他のサービスをゼロ構成アプローチで使用して、Teams アプリを作成および展開できます。 アプリTeams開発では、Teams ToolkitのVisual Studioと同様に、[CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) ツールを使用Toolkit`teamsfx`。
Teams Toolkitを使用すると、アプリを作成、デバッグ、および展開TeamsからVisual Studio Code。 ツールキットを使用したアプリ開発には、次のような利点があります。

* 統合 ID
* クラウド ストレージへのアクセス
* Microsoft Graph
* ゼロ構成Microsoft 365 Azure サービスとセキュリティ サービス

Teams Toolkitは、アプリを 1 か所に構築するためにTeamsツールを提供します。

アプリTeams開発では、Teams ToolkitのVisual Studio Codeと同様に、[CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) ツールを使用Toolkit`teamsfx`。

## <a name="user-journey-of-teams-toolkit"></a>ユーザー体験のTeams Toolkit

Teams Toolkit作業を自動化し、リソースと Azure リソースのTeams統合します。 次の図は、ユーザー Teams Toolkitを示しています。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey.png" alt-text="Teams Toolkitユーザージャーニー" border="true":::

この旅行の主なマイルストーンは次のとおりです。

1. まず、新しいプロジェクトを作成するか、アプリでサンプル Teamsします。
1. 必要に応じて、機能を追加するか、マニフェスト ファイルを編集します。
1. アプリMicrosoft 365をビルドおよびデバッグするには、Teamsアカウントを使用します。
1. Azure アカウントを使用してアプリをプロビジョニングし、クラウドに展開します。
1. アプリをアプリに公開Teams。

## <a name="install-teams-toolkit-for-visual-studio-code"></a>インストールTeams ToolkitのVisual Studio Code

1. [ファイル **Visual Studio Code] を開きます。**
1. [拡張機能] ビューを選択します (**Ctrl + Shift +****X-X** /  または **View >拡張機能**):

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="インストール":::

1. 検索 **Teams Toolkit** 入力します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-2.png" alt-text="ツールキット":::

1. [インストール **] を選択します**。
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install.png" alt-text="ツールキットのインストール":::

> [!TIP]
> マーケットプレースからTeams Toolkit[インストールVisual Studio Codeできます](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

## <a name="take-a-tour-of-teams-toolkit"></a>ガイドのツアーに参加Teams Toolkit

インストールToolkit、次の図に示すように、Teams Toolkit UI が表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teams toolkit.png" alt-text="ミニ関数":::

[クイック スタート] **を選択** してプロジェクトをTeams Toolkit、または [新しいアプリを作成する] Teams **を** 選択して、1 つのプロジェクトTeamsできます。 Visual Studio Code で Teams Toolkit v2.+ によって作成された Teams プロジェクトが開いている場合は、次の図に示すように、すべての機能を備えた Teams Toolkit UI が表示されます。クイック スタートを選択して、Teams Toolkit をクリックするか、[新 **しいアプリを作成Teams]を選択** して、1 つのプロジェクトTeamsします。 サイドバーで既存のプロジェクトを作成または開Toolkit、すべての機能の一覧Visual Studio Codeできます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/toolkit functions.png" alt-text="関数":::

このドキュメントで説明されているトピックについて説明します。

## <a name="accounts"></a>アカウント

アプリを開発Teams、有効なサブスクリプションを持Microsoft 365少なくとも 1 つのアカウントが必要です。 Azure でバックエンド リソースをホストする場合は、Azure アカウントも必要です。 Teams Toolkit Azure リソースのサインイン、プロビジョニング、展開を行う統合エクスペリエンスをサポートしています。 開始する [前に無料の Azure アカウント](https://azure.microsoft.com/free/) を作成できます。

## <a name="environment"></a>環境

Teams Toolkit、複数の環境を作成および管理し、アイテムを準備し、アプリのターゲット環境に展開Teamsします。

### <a name="teamsfx-collaboration"></a>TeamsFx コラボレーション

これにより、開発者とプロジェクト所有者は、TeamsFx プロジェクトに他の共同作業者を招待して、同じ TeamsFx プロジェクトをデバッグ、プロビジョニング、および展開できます。

## <a name="development"></a>開発

Teams Toolkitアプリ開発をより簡単にTeamsするアプリ プロジェクトをTeamsカスタマイズするのに役立ちます。

### <a name="create-a-new-teams-app"></a>新しいアプリをTeamsする

新しいプロジェクトの作成またはサンプルTeamsを使用して新しい Teams プロジェクトTeams Toolkitを作成することで、アプリ開発から始めるのに **役立ちます**。

### <a name="add-capabilities"></a>機能の追加

開発プロセス中にアプリに他Teams機能Teams追加するのに役立ちます。

### <a name="add-cloud-resources"></a>クラウド リソースの追加

必要に応じて、開発ニーズに合ったクラウド リソースを追加するのに役立ちます。

### <a name="edit-manifest-file"></a>マニフェスト ファイルの編集

これにより、アプリとクライアントとのTeamsを編集Teamsできます。

## <a name="deployment"></a>展開

開発中または開発後に、ユーザーがアクセスできる前に、Teamsアプリの準備、展開、発行を行います。

### <a name="provision-in-the-cloud"></a>クラウドでのプロビジョニング

Azure リソース マネージャーと統合され、アプリケーションでコードアプローチに必要な Azure リソースをプロビジョニングできます。

### <a name="deploy-to-the-cloud"></a>クラウドへの展開

 ソース コードを Azure に展開するのに役立ちます。

### <a name="publish-to-teams"></a>[発行] Teams

アプリを作成した後、アプリを個別、チーム、組織、またはだれでもなど、さまざまなスコープに配布できます。 開発したアプリTeams発行するのに役立つコンテンツを公開します。

### <a name="cicd-guide"></a>CI/CD ガイド

アプリケーションの構築中に開発ワークフローを自動化Teams役立ちます。 CI/CD ガイドには、CI または CD パイプラインのセットアップ中に開始するためのツールとテンプレートが含まれています。

#### <a name="teamsfx-cli"></a>TeamsFx CLI

これは、テキスト ベースのコマンド ライン インターフェイスであり、Teams開発を加速し、自動化のためのスクリプトに CLI を統合できる CI/CD シナリオも可能にします。

#### <a name="teamsfx-sdk"></a>TeamsFx SDK

ID の実装やクラウド リソースへのアクセスのタスクを、構成ゼロの単一行ステートメントに削減するのに役立ちます。

## <a name="help-and-feedback"></a>ヘルプとフィードバック

このセクションでは、必要なドキュメントとリソースを確認できます。 製品エキスパートから **クイック サポート** を受GitHub、Teams Toolkitで [問題の報告 **] を選択** できます。 新しい問題を作成する前に問題を参照するか、 [StackOverflow タグにアクセスしてフィードバック `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) を送信します。

この機能についてTeams Toolkitします。

| Teams Toolkit機能 | Includes.... | 可能な操作 |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 アカウント | アプリを構築Microsoft 365有効な E5 サブスクリプションを持つアカウントを使用します。 |
| &nbsp; | Azure アカウント | Azure にアプリを展開するには、Azure アカウントを使用します。 |
| **環境** | &nbsp; | &nbsp; |
| &nbsp; | 地元の | ローカル コンピューター環境の構成を使用して、既定のローカル環境にアプリを展開します。 |
| &nbsp; | dev | リモート環境またはクラウド環境構成を使用して、既定の開発環境にアプリを展開します。 必要に応じて、より多くの環境を作成できます。 |
| **開発** | &nbsp; | &nbsp; |
| &nbsp; | 新しいアプリをTeamsする | ツールキット ウィザードを使用して、アプリ開発用のプロジェクト スキャフォールディングを準備します。 |
| &nbsp; | サンプルの表示 | 12 のTeams Toolkitアプリを選択します。 ツールキットは、アプリ コードを GitHubダウンロードし、サンプル アプリをビルドできます。 |
| &nbsp; | 機能の追加 | 開発プロセス中にTeams機能をTeamsアプリに追加します。 |
| &nbsp; | クラウド リソースの追加 | アプリに適したオプションのクラウド リソースを追加します。 |
| &nbsp; | マニフェスト ファイルの編集 | アプリとクライアントTeams統合をTeamsします。 |
| **展開** | &nbsp; | &nbsp; |
| &nbsp; | クラウドでのプロビジョニング | アプリケーションに Azure リソースを割り当てる。 Teams Toolkit Azure リソース マネージャーと統合されています。 |
| &nbsp; | Zip Teams メタデータ パッケージ | アプリ または開発者ポータルにアップロードできるアプリ パッケージTeams作成します。 アプリ マニフェストとアプリ アイコンが含まれます。  |
| &nbsp; | クラウドへの展開 | ソース コードを Azure に展開します。 |
| &nbsp; | [発行] Teams | 開発したアプリを公開し、個人用、チーム、チャネル、組織などのスコープに配布します。 |
| &nbsp; | Teams の開発者ポータル | 開発者ポータルを使用して、アプリを構成およびTeamsします。 |
| &nbsp; | CI/CD ガイド | アプリケーションの構築中に開発ワークフロー Teams自動化します。 |
| **ヘルプとフィードバック** | &nbsp; | &nbsp; |
| &nbsp; | クイック スタート | クイック スタートTeams Toolkitヘルプを表示Visual Studio Code。  |
| &nbsp; | ドキュメント | 開発者向けドキュメントにアクセスMicrosoft Teams選択します。 |
| &nbsp; | レポートに関する問題GitHub | 選択すると、GitHubページにアクセスし、問題が発生します。 |
|

> [!TIP]
> 新しい問題を作成する前に既存の問題を参照するか、 [StackOverflow タグにアクセスしてフィードバック `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) を送信します。

## <a name="see-also"></a>関連項目

* [プロジェクトを使用して新しいプロジェクトをTeams Toolkit](create-new-project.md)
* [アカウントを準備してアプリTeamsする](accounts.md)
* [Teams ツールキットを使用して Teams アプリを公開する](publish.md)
* [クラウド Teams Toolkitプロビジョニングに使用する](provision.md)
* [クラウドへの展開](deploy.md)
