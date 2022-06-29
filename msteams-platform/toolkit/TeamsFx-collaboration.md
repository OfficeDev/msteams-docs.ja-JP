---
title: Teams Toolkit を使用して TeamsFx プロジェクトで共同作業する
author: yanjiang
description: この記事では、Teams Toolkit を使用して TeamsFx Project で共同作業を行い、他の開発者と共同作業する方法について説明します。
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: e9ae53530cc38ebbb02664e080f5420a0b6f4cc6
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485476"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>Teams Toolkit を使用して Teams プロジェクトで共同作業する

複数の開発者が連携して同じ TeamsFx プロジェクトのデバッグ、プロビジョニング、デプロイを行うことができますが、Teams アプリとMicrosoft Azure Active Directory (Azure AD) アプリの適切なアクセス許可を手動で設定する必要があります。 Teams Toolkit では、開発者とプロジェクト所有者が TeamsFx プロジェクトに他の開発者またはコラボレーターを招待して、同じ TeamsFx プロジェクトをデバッグ、プロビジョニング、および展開できるようにするコラボレーション機能がサポートされています。

## <a name="prerequisites"></a>前提条件

* Microsoft 365 サブスクリプション。
* 有効なサブスクリプションを持つ Azure。
  
  さまざまなアカウントの詳細については、「 [アカウントを準備して Teams アプリを構築する」を](accounts.md)参照してください。

* [Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) バージョン v3.0.0 以降をインストールする

> [!TIP]
> Visual Studio Code で Teams アプリ プロジェクトが開かれていることを確認します。

## <a name="collaborate-with-other-developers"></a>他の開発者と共同作業する

コラボレーション プロセスとその制限事項を理解するには、次の一覧を参照してください。

* プロジェクト所有者として

  > [!NOTE]
  > 環境のコラボレーターを追加する前に、プロジェクト所有者が最初にプロジェクトを [プロビジョニング](provision.md) する必要があります。

  1. Teams Toolkit の **[環境** ] セクションで、 **コラボレーターを選択します**。 次の図に示すように、 **Microsoft 365 Teams アプリの追加 (Azure AD アプリを使用) 所有者** と **Microsoft 365 Teams アプリの一覧表示 (Azure AD アプリを使用) の所有者** のオプションが表示されます。

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="協力":::

  2. [ **Microsoft 365 Teams App (Azure AD アプリを使用) 所有者を追加する]** を選択し、他の Microsoft 365 アカウントのメール アドレスをコラボレーターとして追加します。 追加するアカウントは、イメージに示すように、リモート デバッグのプロジェクト所有者と同じテナント上にある必要があります。

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="envi を追加する":::

  3. 現在の環境でコラボレーターを表示するには、 **Microsoft 365 Teams アプリの一覧表示 (Azure AD アプリを使用) 所有者** を選択し、次の図に示すようにコラボレーターが出力チャネルに一覧表示されます。

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="リスト":::

  4. プロジェクトを GitHub にプッシュする

     > [!NOTE]
     > 新しく追加されたコラボレーターは、通知を受け取りません。 プロジェクトの所有者はコラボレーターに通知する必要があります。

* プロジェクトコラボレーターとして

  1. GitHub からプロジェクトを複製します。
  2. Microsoft 365 アカウントにログオンします。
  3. Azure アカウントにログオンすると、プロジェクトで使用されるすべての Azure リソースに対する共同作成者アクセス許可が付与されます。
  4. Teams アプリをプレビューするには、プロジェクトをリモートにデプロイします。
  5. リモートを起動して Teams アプリのプレビューを作成します。

     > [!NOTE]
     > コラボレーターは、プロジェクト所有者がプロジェクト所有者と同じテナントの下に追加するアカウントを使用してログインする必要があります。 詳細については、「 [リモート環境で Teams アプリをビルドして実行](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)する」を参照してください。

### <a name="limitations"></a>制限事項

Teams Toolkit 拡張機能からコラボレーターを削除する場合は、直接削除できないため、手動で削除する必要があります。 コラボレーターを手動で削除するには、次の手順を実行します。

* 開発者ポータルの使用

  * [Teams 開発者ポータル](https://dev.teams.microsoft.com/home)に移動し、名前またはアプリ ID で Teams アプリを選択します。
  * 左側のパネルから **[所有者]** を選択します。
  * コラボレーターを選択して削除します。

* Azure Active Directory の使用

  * [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) に移動し、左側のパネルから **[アプリの登録**] を選択し、Azure AD アプリを見つけます。
  * Azure AD アプリ管理ページの左側のパネルから **[所有者** ] を選択します。
  * コラボレーターを選択して削除します。

   > [!NOTE]
   >
   > * プロジェクトに追加されたコラボレーターは、通知を受け取りません。 プロジェクト所有者はコラボレーターにオフラインで通知する必要があります。
   > * Azure 関連のアクセス許可は、Azure portalの Azure サブスクリプション管理者が手動で設定する必要があります。 開発者が連携して TeamsFx プロジェクトをプロビジョニングおよびデプロイできるように、Azure アカウントにはサブスクリプションの共同作成者ロールが必要です。

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリをクラウドに展開する](deploy.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
