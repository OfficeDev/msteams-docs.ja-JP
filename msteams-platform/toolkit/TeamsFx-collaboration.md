---
title: グループを使用して TeamsFx Project共同作業Teams Toolkit
author: yanjiang
description: グループを使用して TeamsFx Project共同作業Teams Toolkit
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 5b08923d92e8b1ea7a6292754f62899669de4804
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435168"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>プロジェクトを使用Teams共同作業Teams Toolkit

複数の開発者が連携して同じ TeamsFx プロジェクトのデバッグ、プロビジョニング、展開を行うことができますが、Teams App と Azure AD App.Teams Toolkit の適切なアクセス許可を手動で設定して、開発者とプロジェクト所有者が TeamsFx プロジェクトに他の開発者や共同作業者を招待して、同じプロジェクトをデバッグ、プロビジョニング、および展開できるコラボレーション機能を手動で設定する必要があります。 TeamsFx プロジェクト。

## <a name="prerequisites"></a>前提条件

* アカウントの前提条件

    クラウド リソースをプロビジョニングするには、次のアカウントが必要です。 詳細については、「アプリをビルドするためのアカウント[の準備」をTeamsしてください](accounts.md)。

  * Microsoft 365 サブスクリプション
  * 有効なサブスクリプションを持つ Azure

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> アプリ プロジェクトがTeamsコードで開いているMicrosoft Visual Studioします。

## <a name="collaborate-with-other-developers"></a>他の開発者と共同作業する

次の一覧では、コラボレーション プロセスとその制限について説明します。

### <a name="as-project-owner"></a>プロジェクトの所有者として

> [!NOTE]
> 環境の共同作業者を追加する前に、プロジェクトの所有者が最初に [プロジェクトを準備する](provision.md) 必要があります。

* [**ユーザーの環境**] セクションでTeams Toolkit共同作業者 **を選択します**。 [アプリの追加] Microsoft 365 Teams **(Microsoft Azure Active Directory (Azure AD) アプリ)** の所有者とリスト Microsoft 365 Teams アプリ **(Azure AD アプリ) が表示されます。次の** 図に示すように、所有者。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="共同作業者":::

* [**アプリMicrosoft 365 TeamsをAzure AD]** 所有者を選択し、他Microsoft 365アカウントの電子メール アドレスを共同作業者として追加します。 追加するアカウントは、イメージに示すように、リモート デバッグ用のプロジェクト所有者と同じテナント上にある必要があります。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="envi を追加する":::

* 現在の環境で共同作業者を表示するには、[リスト Microsoft 365 Teams **App] (Azure AD App を使用して) [所有者]** を選択すると、次の図に示すように、共同作業者が出力チャネルに一覧表示されます。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="リスト":::

* プロジェクトをプッシュしてGitHub。

> [!NOTE]
> 新しく追加された共同作業者は通知を受け取らない。 Projectは、共同作業者に通知する必要があります。

### <a name="as-project-collaborator"></a>プロジェクトの共同作業者として

* プロジェクトのクローンを作成GitHub。
* アカウントにログインMicrosoft 365します。
* このプロジェクトで使用しているすべての Azure リソースに対する共同作成者のアクセス許可を持つ Azure アカウントにログインします。
* アプリをプレビュー Teams、プロジェクトをリモートに展開します。
* リモートを起動して、アプリのプレビュー Teamsします。

詳細については、「リモート環境[でアプリをビルドTeams実行する」を参照してください](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)。

> [!NOTE]
> 共同作業者は、プロジェクト所有者と同じテナントの下にあるプロジェクト所有者によって追加されたアカウントを使用してログインする必要があります。

### <a name="limitation"></a>制限

共同作業者を拡張機能から直接削除Teams Toolkitできません。 共同作業者を手動で削除するには、次の手順を実行します。

  1. [開発者ポータルTeamsに移動し、名前またはアプリ ID Teamsアプリを選択します。
  2. 左側の **パネルから [所有者** ] を選択します。
  3. 共同作業者を選択して削除します。
  4. [[アプリの](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)Azure Active Directory] に移動し、左側 **の** パネルから [アプリの登録] を選択し、アプリAzure ADします。
  5. [アプリ **の管理**] ページの左側のAzure ADから [所有者] を選択します。
  6. 共同作業者を選択して削除します。

> [!NOTE]
> * プロジェクトに追加された共同作業者は、通知を受け取る必要があります。 Project所有者は、オフラインで共同作業者に通知する必要があります。
> * Azure 関連のアクセス許可は、Azure サブスクリプション管理者がポータルで手動で設定Microsoft Azureがあります。 開発者が TeamsFx プロジェクトの準備と展開に協力できるよう、Azure アカウントにはサブスクリプションの共同作成者の役割が必要です。

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリをクラウドに展開する](deploy.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
