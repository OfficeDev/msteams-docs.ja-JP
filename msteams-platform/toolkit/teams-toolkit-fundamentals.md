---
title: Teams ツールキットの概要
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit、Teams Toolkit のインストール、Teams Toolkit のユーザー体験について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: fe9bbbb7a6d3668f43c31322ad8099bf994051b1
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558332"
---
# <a name="teams-toolkit-overview"></a>Teams ツールキットの概要

Microsoft Visual Studio Code の Teams Toolkit は、統合 ID、クラウド ストレージへのアクセス、Microsoft Graph からのデータ、Azure のその他のサービス、およびゼロ構成アプローチによる Microsoft 365 を使用して、Teams アプリを作成してデプロイするのに役立ちます。 Teamsアプリ開発では、Visual Studio の Teams Toolkit と同様に、Toolkit `teamsfx` で構成される [CLI ツール](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)を使用できます。
Teams Toolkit では、Visual Studio Code から Teams アプリを作成、デバッグ、デプロイできます。 ツールキットを使用したアプリ開発には、次の利点があります。

* 統合 ID
* クラウド ストレージへのアクセス
* Microsoft Graph からユーザー データにアクセスする
* ゼロ構成アプローチの Azure および Microsoft 365 サービス。

Teams Toolkit は、Teams アプリのビルドに必要なすべてのツールを 1 か所にまとめています。

## <a name="user-journey-of-teams-toolkit"></a>Teams Toolkit のユーザー体験

Teams Toolkit は手動作業を自動化し、Teams と Azure リソースの優れた統合を提供します。 次の画像は、Teams Toolkit のユーザー体験を示しています。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey1.png" alt-text="Teams Toolkit のユーザー体験" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

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

1. 検索ボックスに **「Teams Toolkit** 」と入力します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="ツールキット":::

1. [**インストール**] を選択します。
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit.png" alt-text="ツールキット 4.0.0 をインストールする":::

> [!TIP]
> Teams Toolkit は、[Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) でも見つけることができます。

## <a name="take-a-tour-of-teams-toolkit"></a>Teams Toolkit のツアーに参加する

Toolkit のインストール後、次の画像に示すように Teams Toolkit UI が表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/Teams-toolkit.png" alt-text="mini 関数":::

[ **作業の開始]** を選択して Teams Toolkit を調べるか、[ **新しい Teams アプリの作成** ] を選択して 1 つの Teams プロジェクトを作成します。 Teams Toolkit によって作成された Teams プロジェクトが Visual Studio Code で開かれている場合は、次の図に示すように、すべての機能を備えた Teams Toolkit UI が表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamstookit1.png" alt-text="スクリーン ショット ofteams ツールキット":::

このドキュメントで取り上げるトピックのツアーを見てみましょう。

## <a name="accounts"></a>アカウント

Teams アプリを開発するには、有効なサブスクリプションを持つ少なくとも 1 つのMicrosoft 365 アカウントが必要です。 Azure でバックエンド リソースをホストする場合は、Azure アカウントも必要です。 Teams Toolkit では、Azure リソースのサインイン、プロビジョニング、デプロイを行うための統合エクスペリエンスがサポートされています。 開始する前に、[無料の Azure アカウントを作成](https://azure.microsoft.com/free/) できます。

## <a name="environment"></a>環境

Teams Toolkit は、複数の環境の作成と管理、Teams アプリのターゲット環境への成果物のプロビジョニングとデプロイに役立ちます。

### <a name="teamsfx-collaboration"></a>TeamsFx コラボレーション

これにより、開発者とプロジェクト所有者は、他のコラボレーターを TeamsFx プロジェクトに招待して、同じ TeamsFx プロジェクトをデバッグ、プロビジョニング、デプロイできます。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamsfx.png" alt-text="Teamsfx プロジェクト":::

## <a name="development"></a>開発

Teams Toolkit は、Teams アプリ開発を簡単にする Teams アプリ プロジェクトを作成およびカスタマイズするのに役立ちます。

### <a name="create-a-new-teams-app"></a>新しい Teams アプリを作成する

新しいプロジェクトの作成または **サンプルからの開始** を使用して Teams Toolkit を使用して新しい Teams **プロジェクトを作成** することで、Teams アプリ開発を開始できます。

### <a name="add-features"></a>機能の追加

**これにより、Tab** や **Bot** などの Teams 機能を段階的に追加したり、必要に応じて、開発ニーズに合った **Azure SQL Database** や **Azure Key Vaultなどの Azure** リソースを現在の Teams アプリに追加したりできます。 Teams アプリの **シングル サインオン** または **CI/CD ワークフロー** を追加することもできます。

### <a name="edit-manifest-file"></a>マニフェスト ファイルを編集する

これは、Teams アプリと Teams クライアントの統合を編集するのに役立ちます。

## <a name="deployment"></a>展開

開発中または開発後に、ユーザーがアクセスできるようになる前に、Teams アプリをプロビジョニング、デプロイ、および公開してください。

### <a name="provision-in-the-cloud"></a>クラウドでのプロビジョニング

Azure Resource Managerと統合され、アプリケーションでコード アプローチに必要な Azure リソースをプロビジョニングできます。

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
<!--  
Let's explore Teams Toolkit features.

| Teams Toolkit Features | Includes | What you can do |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 account | Use your Microsoft 365 account with a valid E5 subscription for building your app. |
| &nbsp; | Azure account | Use your Azure account for deploying app on Azure. |
| **Environment** | &nbsp; | &nbsp; |
| &nbsp; | local | Deploy your app in the default local environment with local machine environment configurations. |
| &nbsp; | dev | Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need. |
| **Development** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Use the toolkit wizard to prepare project scaffolding for app development. |
| &nbsp; | View samples | Select any of Teams Toolkit's 12 sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app. |
| &nbsp; | Add Features | - Add other required Teams capabilities to Teams app during development process. </br> - Add optional cloud resources suitable for your app. |
| &nbsp; | Edit manifest file | Edit the Teams app integration with Teams client. |
| **Deployment** | &nbsp; | &nbsp; |
| &nbsp; | Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager. |
| &nbsp; | Zip Teams metadata package | Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons.  |
| &nbsp; | Deploy to the cloud | Deploy the source code to Azure. |
| &nbsp; | Publish to Teams | Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization. |
| &nbsp; | Developer Portal for Teams | Use Developer Portal to configure and manage your Teams app. |
| **Help and Feedback** | &nbsp; | &nbsp; |
| &nbsp; | Quick start | View the Teams Toolkit Quick start help within Visual Studio Code.  |
| &nbsp; | Tutorial | Select to access different tutorials. |
| &nbsp; | Documentation | Select to access the Microsoft Teams Developer Documentation. |
| &nbsp; | Report issues on GitHub | Select to access GitHub page and raise any issues. |

-->
> [!TIP]
> 新しい問題を作成する前に既存の問題を参照するか、 [StackOverflow タグ `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) にアクセスしてフィードバックを送信します。

## <a name="see-also"></a>関連項目

* [Teams Toolkit を使用して新しい Teams アプリを作成する](create-new-project.md)
* [Teams アプリを構築するためのアカウントを準備する](accounts.md)
* [Teams ツールキットを使用して Teams アプリを公開する](publish.md)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [クラウドにデプロイする](deploy.md)
