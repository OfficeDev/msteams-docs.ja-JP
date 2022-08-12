---
title: Visual Studio を使用して Teams アプリをクラウドに展開する
author: surbhigupta
description: このモジュールでは、アプリをクラウド、Azure、または SharePoint に展開し、Visual Studio の Teams ツールキットを使用して Teams アプリを展開する方法について説明します。
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: be4eeb10e16b0dda4d789e4607ac8ffbc302b0e1
ms.sourcegitcommit: f192d7685ee3ddf4a55dc9787d56744403c3f8f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2022
ms.locfileid: "67302445"
---
# <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>Visual Studio を使用して Teams アプリをクラウドに展開する

Teams ツールキットを使用すると、Azure サブスクリプションでプロビジョニングされたクラウド リソースにアプリケーションのフロントエンド コードとバックエンド コードを展開またはアップロードできます。 展開後、使用を開始する前に、Teams クライアントまたは Web ブラウザーでアプリをプレビューできます。 Visual Studio では、次のアプリを展開できます。

* フロントエンド アプリケーションなどのタブ アプリは、静的な Web ホスティング用に構成された Azure ストレージに展開されます。
* Azure 関数トリガーを使用した通知ボット アプリを Azure 関数に展開できます。
* ボット アプリまたはメッセージ拡張機能を Azure アプリ サービスに展開できます。

## <a name="prerequisite"></a>前提条件

アプリをビルドして展開するために必要なツールの一覧を次に示します。

| &nbsp; | インストール | 使用するには... |
| --- | --- | --- |
| &nbsp; | **必須** | &nbsp; |
| &nbsp; | Visual Studio 2022 バージョン 17.3 | Visual Studio のエンタープライズ エディションをインストールし、"ASP.NET" ワークロードと Microsoft Teams 開発ツールをインストールできます。 |
| &nbsp; | Teams ツールキット | アプリのプロジェクト スキャフォールディングを作成する Visual Studio 拡張機能。 最新バージョン​​を使用します。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams を使用して、チャット、会議、通話用のアプリを通じて共同作業を行うすべてのユーザーと 1 か所で共同作業を行うことができます。 |
| &nbsp; | Azure Tools と [Microsoft Azure CLI](/cli/azure/install-azure-cli) | 保存されたデータにアクセスしたり、Azure で Teams アプリ用のクラウドベースのバックエンドをデプロイしたりするための Azure ツール。 |

  > [!NOTE]
  > プロジェクト コードをクラウドに展開する前に、[TTK Visual Studio のクラウド リソースをプロビジョニングします](provision VS.md)。

## <a name="deploy-teams-app-using-teams-toolkit"></a>Teams ツールキットを使用して Teams アプリを展開する

1. Visual Studio を起動します。
1. **[新しいプロジェクトを作成する]** を選択するか、一覧から既存のプロジェクトを開きます。
1. **MyTeamsApp1** のプロジェクトを右クリックします。
1. **[Teams ツールキット]** を選択します。
1. **[クラウドに展開する...]** を選択します。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="[クラウドに展開する]":::

   > [!NOTE]
   > このシナリオでは、プロジェクト名は MyTeamsApp1 です。

1. 確認ダイアログで **[展開]** を選択します。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="[クラウドに展開する] の確認ダイアログ":::

1. 展開プロセスがトリガーされて完了すると、正常に展開されたことの確認を含むポップアップが表示されます。 出力ウィンドウで状態を確認することもできます。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="[クラウドに展開する] のポップアップ":::

プロジェクトが Azure に正常に展開されると、Teams ツールキットでアプリをプレビューするさまざまな方法があります。

1. **[プロジェクト]** > **[Teams ツールキット]** > **[Zip アプリ パッケージ]** を選択して、Teams アプリ パッケージを生成します。
1. **[ローカル用]** または **[Azure 用]** のオプションを選択し、Teams クライアントにアップロードします。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package.png" alt-text="Teams アプリ パッケージを作成する":::

  **Teams クライアントでアプリをプレビューするには**

3. **[プロジェクト]** を選択します。
4. **[Teams ツールキット]** を選択します。
5. **[Teams でプレビュー]** を選択します。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams1.png" alt-text="Teams クライアントで Teams アプリをプレビューする":::

アプリをプレビューするもう 1 つの方法:

1. ソリューション エクスプローラー パネルで、**MyTeamsApp1** のプロジェクトを右クリックします。
1. **[Teams ツールキット]** を選択します。
1. **[Teams でプレビュー]** を選択して、Web ブラウザーで Teams アプリを起動します。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="Web ブラウザーで Teams アプリをプレビューする":::

   > [!NOTE]
   > 同じメニュー オプションが [プロジェクト] メニューでも使用できます。

## <a name="see-also"></a>関連項目

* [Visual Studio で新しい Teams アプリを作成する](create-new-teams-app-for-Visual-Studio.md)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Visual Studio を使用して Teams アプリをローカルでデバッグする](debug-teams-app-visual-studio.md)
