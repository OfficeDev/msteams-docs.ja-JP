---
title: Teams Toolkit概要
author: zyxiaoyuer
description: 概要Teams Toolkit、インストール、Teams Toolkit機能のツアー Toolkitします。
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 0a048e12167847c1cc34560531cba13da9d74f8f
ms.sourcegitcommit: 58a24422bb04a529b6629a56803ed2efabc17cb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2022
ms.locfileid: "62323167"
---
# <a name="teams-toolkit-overview"></a>Teams Toolkit概要

> [!NOTE]
> 現時点では、この機能はパブリック開発者 **プレビューでのみ利用** できます。

Teams Toolkitを使用すると、アプリを作成、デバッグ、および展開TeamsからVisual Studio Code。 ツールキットを使用したアプリ開発には、次のような利点があります。

- 統合 ID
- クラウド ストレージへのアクセス
- Microsoft Graph
- ゼロ構成Microsoft 365 Azure サービスとセキュリティ サービス

Teams Toolkitアプリを 1 か所に構築するためにTeamsツールが提供されます。

アプリTeams開発では、Teams ToolkitのVisual Studio Codeと同様に、[CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) ツールを使用Toolkit`teamsfx`。

## <a name="user-journey-of-teams-toolkit"></a>ユーザーのTeams Toolkit

Teams Toolkit作業を自動化し、リソースと Azure リソースのTeams統合します。 次の図は、ユーザー Teams Toolkitを示しています。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey.png" alt-text="Teams Toolkitユーザージャーニー" border="true":::

この旅行の主なマイルストーンは次のとおりです。

1. まず、新しいプロジェクトを作成するか、アプリでサンプル Teamsします。
1. 必要に応じて、機能を追加するか、マニフェスト ファイルを編集します。
1. アプリMicrosoft 365をビルドしてデバッグするには、Teamsアカウントを使用します。
1. Azure アカウントを使用してアプリをプロビジョニングし、クラウドに展開します。
1. アプリをアプリに公開Teams。

## <a name="install-teams-toolkit-for-visual-studio-code"></a>インストールTeams ToolkitインストールVisual Studio Code

1. [ファイル **Visual Studio Code] を開きます。**
1. [拡張機能] ビューを選択します (**Ctrl + Shift + X** / **¥--X** または **[拡張機能>します**)。

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

[クイック スタート] **を選択** してプロジェクトをTeams Toolkit、または [新しいアプリを作成する] Teams **を** 選択して、1 つのプロジェクトTeamsできます。 サイドバーで既存のプロジェクトを作成または開Toolkit、すべての機能の一覧Visual Studio Codeできます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/toolkit functions.png" alt-text="関数":::

この機能をTeams Toolkitします。

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
| &nbsp; | サンプルの表示 | 12 のTeams Toolkitアプリを選択します。 ツールキットは、アプリ コードを GitHubからダウンロードし、サンプル アプリをビルドできます。 |
| &nbsp; | 機能の追加 | 開発プロセス中にTeams機能をTeamsアプリに追加します。 |
| &nbsp; | クラウド リソースの追加 | アプリに適したオプションのクラウド リソースを追加します。 |
| &nbsp; | マニフェスト ファイルの編集 | アプリとクライアントTeams統合を編集Teamsします。 |
| **展開** | &nbsp; | &nbsp; |
| &nbsp; | クラウドでのプロビジョニング | アプリケーションに Azure リソースを割り当てる。 Teams Toolkit Azure リソース マネージャーと統合されています。 |
| &nbsp; | Zip Teams メタデータ パッケージ | アプリ または開発者ポータルにアップロードできるアプリ パッケージTeams作成します。 アプリ マニフェストとアプリ アイコンが含まれます。  |
| &nbsp; | クラウドへの展開 | ソース コードを Azure に展開します。 |
| &nbsp; | [ファイルに発行Teams | 開発したアプリを公開し、個人用、チーム、チャネル、組織などのスコープに配布します。 |
| &nbsp; | Teams の開発者ポータル | 開発者ポータルを使用して、アプリを構成およびTeamsします。 |
| &nbsp; | CI/CD ガイド | アプリケーションの構築中に開発ワークフロー Teams自動化します。 |
| **ヘルプとフィードバック** | &nbsp; | &nbsp; |
| &nbsp; | クイック スタート | [クイック スタート] Teams Toolkitヘルプを表示するには、Visual Studio Code。  |
| &nbsp; | ドキュメント | 開発者向けドキュメントにアクセスMicrosoft Teams選択します。 |
| &nbsp; | レポートに関する問題GitHub | 選択すると、GitHubページにアクセスし、問題が発生します。 |
|

> [!TIP]
> 新しい問題を作成する前に既存の問題を参照するか、 [StackOverflow タグにアクセスしてフィードバック `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) を送信します。

## <a name="see-also"></a>関連項目

* [プロジェクトを使用して新しいプロジェクトをTeams Toolkit](create-new-project.md)
* [アプリをビルドするためのアカウントTeamsする](accounts.md)
* [Teams ツールキットを使用して Teams アプリを公開する](publish.md)
* [クラウド Teams Toolkitプロビジョニングに使用する](provision.md)
* [クラウドへの展開](deploy.md)
