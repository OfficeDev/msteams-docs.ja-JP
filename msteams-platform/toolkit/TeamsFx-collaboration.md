---
title: Teams Toolkitを使用して TeamsFx Projectで共同作業する
author: yanjiang
description: Teams Toolkitを使用して TeamsFx Projectで共同作業する
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 099820252fd83a2d916e8d61f3b83b63291695e9
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66124019"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>Teams Toolkit を使用して Teams プロジェクトで共同作業する

複数の開発者が連携して同じ TeamsFx プロジェクトのデバッグ、プロビジョニング、デプロイを行うことができますが、Teams アプリとMicrosoft Azure Active Directory (Azure AD) アプリの適切なアクセス許可を手動で設定する必要があります。 Teams Toolkitでは、開発者とプロジェクト所有者が TeamsFx プロジェクトに他の開発者またはコラボレーターを招待して、同じ TeamsFx プロジェクトをデバッグ、プロビジョニング、デプロイできるようにするコラボレーション機能がサポートされています。

## <a name="prerequisites"></a>必須条件

* Microsoft 365 サブスクリプション
* 有効なサブスクリプションを持つ Azure
  
  さまざまなアカウントの詳細については、[アプリをビルドするためのアカウントの準備Teams](accounts.md)参照してください。

* [Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) バージョン v3.0.0 以降をインストールする

> [!TIP]
> Visual Studio Code でTeams アプリ プロジェクトが開かれていることを確認します。

## <a name="collaborate-with-other-developers"></a>他の開発者と共同作業する

コラボレーション プロセスとその制限事項を理解するには、次の一覧を参照してください。

* プロジェクト所有者として

  > [!NOTE]
  > 環境のコラボレーターを追加する前に、プロジェクト所有者が最初にプロジェクトを [プロビジョニング](provision.md) する必要があります。

  1. Teams Toolkit **の [ENVIRONMENT**] セクションで、**コラボレーターを選択します**。 次の図に示すように、オプション [**Add Microsoft 365 Teams App (Azure AD App を使用) の所有者** と **リスト Microsoft 365 Teams アプリ (Azure AD アプリを含む) 所有者** を表示します。

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="協力":::

  2. **[Add Microsoft 365 Teams App (Azure AD App を使用) 所有者]** を選択し、コラボレーターとして他のMicrosoft 365 アカウントの電子メール アドレスを追加します。 追加するアカウントは、イメージに示すように、リモート デバッグのプロジェクト所有者と同じテナント上にある必要があります。

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="envi を追加する":::

  3. 現在の環境でコラボレーターを表示するには、[**アプリの一覧Microsoft 365 Teams (Azure AD アプリを含む) 所有者]** を選択すると、次の図に示すようにコラボレーターが出力チャネルに一覧表示されます。

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="リスト":::

  4. プロジェクトをGitHubにプッシュする

     > [!NOTE]
     > 新しく追加されたコラボレーターは、通知を受け取りません。 Project所有者はコラボレーターに通知する必要があります。

* プロジェクトコラボレーターとして

  1. GitHub からプロジェクトを複製します。
  2. Microsoft 365 アカウントにログオンします。
  3. Azure アカウントにログオンすると、プロジェクトで使用されるすべての Azure リソースに対する共同作成者アクセス許可が付与されます。
  4. Teams アプリをプレビューするには、プロジェクトをリモートにデプロイします。
  5. リモートを起動して、Teams アプリのプレビューを表示します。

     > [!NOTE]
     > コラボレーターは、プロジェクト所有者がプロジェクト所有者と同じテナントの下に追加するアカウントを使用してログインする必要があります。 詳細については、[リモート環境でのTeams アプリのビルドと実行に関するページを参照してください](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)。

### <a name="limitations"></a>制限事項

Teams Toolkit拡張機能からコラボレーターを削除する場合は、直接削除できないため、手動で削除する必要があります。 コラボレーターを手動で削除するには、次の手順を実行します。

* 開発者ポータルの使用

  * [開発者ポータルTeams](https://dev.teams.microsoft.com/home)移動し、名前またはアプリ ID でTeamsアプリを選択します。
  * 左側のパネルから **[所有者]** を選択します。
  * コラボレーターを選択して削除します。

* Azure Active Directoryの使用

  * [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)に移動し、左側のパネルから **[アプリの登録**] を選択し、Azure AD アプリを見つけます。
  * Azure AD アプリ管理ページの左側のパネルから **[所有者** ] を選択します。
  * コラボレーターを選択して削除します。

   > [!NOTE]
   >
   > * プロジェクトに追加されたコラボレーターは、通知を受け取りません。 Project所有者はコラボレーターにオフラインで通知する必要があります。
   > * Azure 関連のアクセス許可は、Azure portalの Azure サブスクリプション管理者が手動で設定する必要があります。 開発者が連携して TeamsFx プロジェクトをプロビジョニングおよびデプロイできるように、Azure アカウントにはサブスクリプションの共同作成者ロールが必要です。

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリをクラウドに展開する](deploy.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
