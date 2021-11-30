---
title: グループを使用して TeamsFx Project共同作業Teams Toolkit
author: yanjiang
description: グループを使用して TeamsFx Project共同作業Teams Toolkit
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: bb58e7f54fe3ad75b2a52148540119ae5dbbc9e6
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228000"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>プロジェクトを使用Teams共同作業Teams Toolkit

複数の開発者が一緒に作業して、同じ TeamsFx プロジェクトのデバッグ、プロビジョニング、展開を行うことができますが、Teams App と AAD App の適切なアクセス許可を手動で設定する必要があります。これは簡単ではありません。

Teams Toolkitコラボレーション機能がサポートされ、開発者 (プロジェクト所有者) が他の開発者 (共同作業者) を TeamsFx プロジェクトに招待して、同じ TeamsFx プロジェクトをデバッグ、プロビジョニング、展開できます。

## <a name="prerequisites"></a>前提条件

* アカウントの前提条件

    Azure およびクラウド サーバーでクラウド リソースをMicrosoft 365するには、適切なアクセス許可を持つ次のアカウントが必要です。 詳細については[、「Prepare accounts to build Teamsアプリ」](accounts.md)を参照してください。

    * Microsoft 365
    * 有効なサブスクリプションを持つ Azure

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> VS コードで開Teamsアプリ プロジェクトを既に持っている必要があります。

## <a name="collaborate-with-other-developers"></a>他の開発者と共同作業する

### <a name="as-a-project-owner"></a>プロジェクトの所有者として

> [!NOTE]
> 環境の共同作業者を追加する前に、プロジェクトの所有者が最初に [プロジェクトを準備する](provision.md) 必要があります。

* Teams Toolkitの [環境] セクションで、環境名をマウスで移動して共同作業者のボタンを見つけ、1 つは **[M365 Teams** アプリの追加 (AAD App 付き) 所有者] ボタンで、もう 1 つは [リスト **M365 Teams アプリ (AAD アプリ付き) 所有者]** ボタンです。次の図に示すように、

  ![コラボレーション ボタン](./images/collaboration-buttons.png)

* **[M365** Teams アプリを追加する (AAD アプリを使用して) [所有者] ボタンを選択し、別の M365 アカウントの電子メール アドレスを共同作業者として追加します。 追加するアカウントは、イメージに示すように、リモート デバッグ用のプロジェクト所有者と同じテナント上にある必要があります。

  ![共同作業者のメールを入力する](./images/collaboration-add-owner-email.png)

* 現在の環境で共同作業者を表示するには、[**リスト M365 Teams App (AAD App 付き) 所有者]** ボタンを選択すると、次の図に示すように、共同作業者が出力チャネルに一覧表示されます。

  ![コラボレーション リストの所有者](./images/collaboration-list-owners.png)

* プロジェクトをプッシュしてGitHub。

> [!NOTE]
> 新しく追加された共同作業者は、通知を受け取る必要があります。 Projectは、共同作業者に通知する必要があります。

### <a name="as-a-project-collaborator"></a>プロジェクトの共同作業者として

* プロジェクトのクローンを作成GitHub
* ログイン M365 アカウント

> [!NOTE]
> 共同作業者は、プロジェクト所有者と同じテナントの下にあるプロジェクト所有者によって追加されたアカウントを使用 **してログインする必要があります**。

* このプロジェクトで使用しているすべての Azure リソースに対する共同作成者のアクセス許可を持つ Azure アカウントにログインします。
* プロジェクト コードに取り組み、プロジェクトをリモートに展開し、アプリをプレビューする時間Teamsします。
* リモートを起動して、アプリのプレビュー Teamsします。 詳細については、「リモート環境[でアプリをビルドしてTeams実行する」を参照してください](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)。

### <a name="limitations"></a>制限事項

> [!NOTE]
> Azure 関連のアクセス許可は、Azure portal の Azure サブスクリプション管理者が手動で設定する必要があります。 開発者が TeamsFx プロジェクトの準備と展開に協力できるよう、Azure アカウントには少なくともサブスクリプションの共同作成者の役割が必要です。

1. **削除できません**: 共同作業者を拡張機能から直接Teams Toolkitできません。 以下の手順に従って、共同作業者を手動で削除します。

      1. [開発者[ポータルTeams] に](https://  dev.teams.microsoft.com/apps)移動し、名前Teamsアプリ ID でアプリを検索します。
      2. [アプリのTeams] ページで、左側の **パネルから [所有者**] を選択します。
      3. 共同作業者を検索して削除します。
      4. [アプリの登録 [Azure Active Directory]](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)**に移動** し、左側のパネルから [アプリの登録] を選択し、アプリAADします。
      5. [アプリのAAD] ページで、左側の **パネルから [所有者**] を選択します。
      6. 共同作業者を検索して削除します。
    

1. コラボレーション機能は Azure でホストされるプロジェクトのみをサポートSPFxホストされているプロジェクトは今後サポートされる予定です。

1. プロジェクトに追加された共同作業者は、通知を受け取る必要があります。 Project所有者は、オフラインで共同作業者に通知する必要があります。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [クラウド リソースのプロビジョニング](provision.md)

> [!div class="nextstepaction"]
> [クラウドTeamsアプリを展開する](deploy.md)

> [!div class="nextstepaction"]
> [複数の環境を管理する](TeamsFx-multi-env.md)
