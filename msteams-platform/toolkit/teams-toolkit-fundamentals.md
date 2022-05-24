---
title: Teams ツールキットの概要
author: zyxiaoyuer
description: Teams Toolkitの概要、Teams Toolkit のインストール、Toolkit 機能のツアー
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/17/2022
ms.openlocfilehash: 36436b5cc2cf7edec784ab653b12d8cf44172b8b
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2022
ms.locfileid: "65654612"
---
# <a name="teams-toolkit-overview"></a>Teams ツールキットの概要


Microsoft Visual Studio Code の Teams Toolkit は、統合 ID、クラウド ストレージへのアクセス、Microsoft Graph からのデータ、Azure のその他のサービス、およびゼロ構成アプローチによる Microsoft 365 を使用して、Teams アプリを作成してデプロイするのに役立ちます。 Teamsアプリ開発では、Visual Studio の Teams Toolkit と同様に、Toolkit `teamsfx` で構成される [CLI ツール](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)を使用できます。
Teams Toolkit では、Visual Studio Code から Teams アプリを作成、デバッグ、デプロイできます。 ツールキットを使用したアプリ開発には、次の利点があります。

* 統合 ID
* クラウド ストレージへのアクセス
* Microsoft Graph からユーザー データにアクセスする
* ゼロ構成アプローチを使用した Azure サービスとMicrosoft 365 サービス

Teams Toolkit は、Teams アプリのビルドに必要なすべてのツールを 1 か所にまとめています。

## <a name="user-journey-of-teams-toolkit"></a>Teams Toolkit のユーザー体験

Teams Toolkit は手動作業を自動化し、Teams と Azure リソースの優れた統合を提供します。 次の画像は、Teams Toolkit のユーザー体験を示しています。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey.png" alt-text="Teams Toolkit ユーザー体験" border="true":::

この体験の主なマイルストーンは次のとおりです。

1. まず、新しいプロジェクトを作成するか、サンプル Teams アプリを試します。
1. 必要に応じて、機能を追加するか、マニフェスト ファイルを編集します。
1. Microsoft 365 アカウントを使用して、Teams アプリをビルドしてデバッグします。
1. Azure アカウントを使用して、アプリをプロビジョニングしてクラウドにデプロイします。
1. アプリを Teams に公開する

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Visual Studio Code 用 Teams ツールキット

1. **Visual Studio Code** を開きます。
1. 拡張機能ビュー (**Ctrl + Shift + X** / **⌘⇧-X** または **ビュー > Extensions**) を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="インストール":::

1. 検索ボックス **に「Teams Toolkit**」と入力します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="ツールキット":::

1. [**インストール**] を選択します。
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit.png" alt-text="ツールキット 4.0.0 をインストールする":::

> [!TIP]
> Teams Toolkit は、[Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) でも見つけることができます。

## <a name="take-a-tour-of-teams-toolkit"></a>Teams Toolkit のツアーに参加する

Toolkit のインストール後、次の画像に示すように Teams Toolkit UI が表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/Teams-toolkit.png" alt-text="mini 関数":::

**はじめに** を選択してTeams Toolkitを調べるか、[**新しいTeams アプリの作成**] を選択して 1 つのTeams プロジェクトを作成します。 Visual Studio Code でTeams Toolkitによって作成されたTeams プロジェクトがある場合は、次の図に示すように、すべての機能を備えたTeams Toolkit UI が表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamstookit1.png" alt-text="スクリーン ショット ofteams ツールキット":::

このドキュメントで取り上げるトピックのツアーを見てみましょう。

## <a name="accounts"></a>アカウント

Teams アプリを開発するには、有効なサブスクリプションを持つ少なくとも 1 つのMicrosoft 365 アカウントが必要です。 Azure でバックエンド リソースをホストする場合は、Azure アカウントも必要です。 Teams Toolkitでは、Azure リソースのサインイン、プロビジョニング、デプロイを行うための統合エクスペリエンスがサポートされています。 開始する前に、[無料の Azure アカウントを作成](https://azure.microsoft.com/free/) できます。

## <a name="environment"></a>環境

Teams Toolkit は、複数の環境の作成と管理、Teams アプリのターゲット環境への成果物のプロビジョニングとデプロイに役立ちます。

### <a name="teamsfx-collaboration"></a>TeamsFx コラボレーション

これにより、開発者とプロジェクト所有者は、他のコラボレーターを TeamsFx プロジェクトに招待して、同じ TeamsFx プロジェクトをデバッグ、プロビジョニング、デプロイできます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamsfx.png" alt-text="Teamsfx プロジェクト":::

## <a name="development"></a>開発

Teams Toolkit は、Teams アプリ開発を簡単にする Teams アプリ プロジェクトを作成およびカスタマイズするのに役立ちます。

### <a name="create-a-new-teams-app"></a>新しい Teams アプリを作成する

新しいプロジェクトの作成またはサンプルからの開始を使用して、Teams Toolkitを使用して新しいTeams プロジェクトを作成することで、**Teamsアプリ** 開発 **を開始** するのに役立ちます。

### <a name="add-features"></a>機能の追加

**これは、Tab** や **Bot** などの追加のTeams機能を段階的に追加したり、必要に応じて、開発ニーズに合った **Azure SQL Database** や **Azure Key Vaultなどの Azure** リソースを現在のTeams アプリに追加したりするのに役立ちます。 Teams アプリの **シングル サインオン** または **CI/CD ワークフロー** を追加することもできます。 

### <a name="edit-manifest-file"></a>マニフェスト ファイルを編集する

これは、Teams アプリと Teams クライアントの統合を編集するのに役立ちます。

## <a name="deployment"></a>展開

開発中または開発後に、ユーザーがアクセスできるようになる前に、Teams アプリをプロビジョニング、デプロイ、および公開してください。

### <a name="provision-in-the-cloud"></a>クラウドでのプロビジョニング

Azure リソース マネージャーと統合され、アプリケーションでコード アプローチに必要な Azure リソースをプロビジョニングできます。

### <a name="deploy-to-the-cloud"></a>クラウドにデプロイする

 ソース コードを Azure にデプロイするのに役立ちます。

### <a name="publish-to-teams"></a>Teams ストアに公開する

アプリを作成した後は、個人、チーム、組織、すべてのユーザーなど、さまざまな範囲にアプリを配布できます。 Teams に発行すると、開発したアプリを発行できます。

#### <a name="teamsfx-cli"></a>TeamsFx CLI

これはテキスト ベースのコマンド ライン インターフェイスであり、Teams アプリケーション開発を高速化し、自動化のために CLI をスクリプトに統合できる CI/CD シナリオも可能にします。

#### <a name="teamsfx-sdk"></a>TeamsFx SDK

構成がゼロの単一行ステートメントに ID とクラウド リソースへのアクセスを実装するタスクを減らすのに役立ちます。

## <a name="help-and-feedback"></a>ヘルプとフィードバック

このセクションでは、必要なドキュメントとリソースを見つけることができます。 Teams Toolkitで **[GitHubに関する問題を報告する]** を選択すると、製品の専門家から **[クイック サポート]** を受けることができます。 新しい問題を作成する前に問題を参照するか、 [StackOverflow タグ `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) にアクセスしてフィードバックを送信します。

Teams Toolkit 機能を見てみましょう。

| Teams Toolkit 機能 | 含まれる内容... | 可能な操作 |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 アカウント | アプリをビルドするために有効な E5 サブスクリプションで Microsoft 365 アカウントを使用します。 |
| &nbsp; | Azure アカウント | Azure にアプリをデプロイするには、Azure アカウントを使用します。 |
| **環境** | &nbsp; | &nbsp; |
| &nbsp; | ローカル | ローカル コンピューター環境の構成を使用して、既定のローカル環境にアプリをデプロイします。 |
| &nbsp; | dev | リモートまたはクラウド環境の構成を使用して、既定の開発環境にアプリをデプロイします。 必要に応じて、より多くの環境を作成できます。 |
| **開発** | &nbsp; | &nbsp; |
| &nbsp; | 新しい Teams アプリを作成する | ツールキット ウィザードを使用して、アプリ開発用のプロジェクト スキャフォールディングを準備します。 |
| &nbsp; | [サンプルを見る] | Teams Toolkitの 12 個のサンプル アプリのいずれかを選択します。 ツールキットは GitHub からアプリ コードをダウンロードし、サンプル アプリをビルドできます。 |
| &nbsp; | 機能の追加 | - 開発プロセス中に、アプリに必要なその他のTeams機能Teams追加します。 </br> - アプリに適したオプションのクラウド リソースを追加します。 |
| &nbsp; | マニフェスト ファイルを編集する | Teams アプリと Teams クライアントの統合を編集します。 |
| **展開** | &nbsp; | &nbsp; |
| &nbsp; | クラウドでのプロビジョニング | アプリケーションに Azure リソースを割り当てます。 Teams Toolkit は Azure Resource Manager と統合されています。 |
| &nbsp; | Zip Teams メタデータ パッケージ | Teamsまたは開発者ポータルにアップロードできるアプリ パッケージを作成します。 アプリ マニフェストとアプリ アイコンが含まれています。  |
| &nbsp; | クラウドにデプロイする | ソース コードを Azure にデプロイします。 |
| &nbsp; | Teams ストアに公開する | 開発したアプリを公開し、個人、チーム、チャネル、組織などのスコープに配布します。 |
| &nbsp; | Teams の開発者ポータル | 開発者ポータルを使用して、アプリを構成、管理、デプロイします。 |
| **ヘルプとフィードバック** | &nbsp; | &nbsp; |
| &nbsp; | クイック スタート | Visual Studio Code 内のTeams Toolkitクイック スタートのヘルプを表示します。  |
| &nbsp; | チュートリアル | 選択すると、さまざまなチュートリアルにアクセスできます。 |
| &nbsp; | ドキュメント | Microsoft Teams 開発者向けドキュメントにアクセスする場合に選択します。 |
| &nbsp; | GitHub に関する問題を報告する | 選択すると、GitHub ページにアクセスし、問題が発生します。 |


> [!TIP]
> 新しい問題を作成する前に既存の問題を参照するか、 [StackOverflow タグ `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) にアクセスしてフィードバックを送信します。

## <a name="see-also"></a>関連項目

* [Teams Toolkit を使用して新しい Teams アプリを作成する](create-new-project.md)
* [Teams アプリを構築するためのアカウントを準備する](accounts.md)
* [Teams ツールキットを使用して Teams アプリを公開する](publish.md)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [クラウドにデプロイする](deploy.md)
