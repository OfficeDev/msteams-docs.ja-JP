---
title: CI/CD テンプレート
author: MuyangAmigo
description: このモジュールでは、GitHub、Azure DevOps、Jenkins for Teams Application DevelopersCI/CD テンプレートで CI/CD パイプライン テンプレートを使用する方法について説明します
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 05f797afcf54cab2d23ee24aae2c4985f3d724f2
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806873"
---
# <a name="set-up-cicd-pipelines"></a>CI/CD パイプラインを設定する

TeamsFx は、Teams アプリケーションをビルドしながら開発ワークフローを自動化するのに役立ちます。 CI/CD パイプラインのセットアップ、ワークフロー テンプレートの作成、GitHub、Azure DevOps、Jenkins や他のプラットフォームを使用した CI/CD ワークフローのカスタマイズに使用できるツールとテンプレートを次に示します。 リソースをプロビジョニングしてデプロイするために、Teams 開発者ポータルを使用して Azure サービス プリンシパルを作成し、Teams アプリを発行できます。 Teams アプリを手動で発行するために、[Teams の開発者ポータル](https://dev.teams.microsoft.com/home)を使用できます。

|ツールとテンプレート | 説明 |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|TeamsFx CLI と統合する GitHub アクション。|
|[Visual Studio Codeの Teams ツールキット](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Teams アプリや、GitHub、Azure DevOps、および Jenkins の自動化ワークフローの開発に役立つ Visual Studio Code 拡張機能。 |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | Teams アプリや、GitHub、Azure DevOps、および Jenkins の自動化ワークフローの開発に役立つコマンドライン ツール。|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) と [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| GitHub、Azure DevOps、または Jenkins 以外の自動化用のスクリプト テンプレート。 |

## <a name="set-up-pipelines"></a>CI/CD パイプラインを設定する

パイプラインは、次のプラットフォームで設定できます。

1. [GitHub を使用してパイプラインを設定する](#set-up-pipelines-with-github)
1. [Azure DevOps を使用してパイプラインを設定する](#set-up-pipelines-with-azure-devops)
1. [Jenkins を使用してパイプラインを設定する](#set-up-pipelines-with-jenkins)
1. [他のプラットフォームのパイプラインを設定する](#set-up-pipelines-for-other-platforms)

## <a name="set-up-pipelines-with-github"></a>GitHub を使用してパイプラインを設定する

CI/CD で GitHub を使用してパイプラインを設定するには:

* ワークフロー テンプレートを作成します。

  * Visual Studio Code
  * TeamsFx CLI

* CI/CD ワークフローをカスタマイズします。

### <a name="create-workflow-templates"></a>ワークフロー テンプレートを作成する

GitHub を使用して、次のワークフロー テンプレートを作成できます。

**Visual Studio Codeの Teams ツールキット**

1. Teams Toolkit を使用して新しい Teams アプリを作成します。

1. 左側のウィンドウで **Teams Toolkit** アイコン :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: を選択します。

1. [**機能の追加]** を選択する

   :::image type="content" source="../assets/images/teams-toolkit-v2/add-feature.png" alt-text="機能の追加":::

1. **[CI/CD ワークフローの追加]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/toolkit-ci-cd-workflow.png" alt-text="CI/CD ワークフローを選択する":::

1. コマンド プロンプトから環境を選択します。
1. CI/CD プロバイダーとして **[GitHub]** を選択します。
1. [CI]、[CD]、[プロビジョニング]、[Teams に発行] のオプションから 1 つ以上のテンプレートを選択します。
1. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
1. `.github/workflows` にある README ファイルに従って、GitHub でワークフローを設定します。

**TeamsFx CLI**

1. Teams アプリ プロジェクト ディレクトリに「`cd`」と入力します。
2. `teamsfx add cicd` コマンドを入力して、対話型コマンド プロセスを開始します。
3. コマンド プロンプトから環境を選択します。
4. CI/CD プロバイダーとして **[GitHub]** を選択します。
5. [CI]、[CD]、[プロビジョニング]、[Teams に発行] のオプションから 1 つ以上のテンプレートを選択します。
7. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
8. `.github/workflows` にある README ファイルに従って、GitHub でワークフローを設定します。

> [!NOTE]
> 追加のワークフロー テンプレートを追加する必要がある場合、同じ手順に従って、Visual Studio Code または TeamsFx CLI でワークフロー テンプレートを作成できます。

### <a name="customize-cicd-workflow"></a>CI/CD ワークフローをカスタマイズする

テスト スクリプトを変更または削除して、CI/CD ワークフローをカスタマイズできます。

1. 既定では、`main` ブランチに対して新しいコミットが行われると、CD ワークフローがトリガーされます。
1. 必要に応じてビルド スクリプトを変更します。
1. 必要に応じてテスト スクリプトを削除します。

## <a name="set-up-pipelines-with-azure-devops"></a>Azure DevOps を使用してパイプラインを設定する

CI/CD で Azure DevOps を使用してパイプラインを設定するには:

* ワークフロー テンプレートを作成します。

  * Visual Studio Code
  * TeamsFx CLI

* CI/CD ワークフローをカスタマイズします。

### <a name="create-workflow-templates"></a>ワークフロー テンプレートを作成する

Azure DevOps を使用して、次のワークフロー テンプレートを作成できます。

**Visual Studio Codeの Teams ツールキット**

1. Teams Toolkit を使用して新しい Teams アプリを作成します。
2. 左側のウィンドウで **Teams Toolkit** アイコン :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: を選択します。
1. **[CI/CD ワークフローの追加]** を選択します。
1. コマンド プロンプトから環境を選択します。
1. CI/CD プロバイダーとして **[Azure DevOps]** を選択します。
1. [CI]、[CD]、[プロビジョニング]、および [Teams に発行] のオプションから 1 つ以上のテンプレートを選択します。
1. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
1. `.azure/pipelines` にある README ファイルに従って、Azure DevOps でワークフローを設定します。

**TeamsFx CLI**

1. Teams アプリ プロジェクト ディレクトリに「`cd`」と入力します。
2. `teamsfx add cicd` コマンドを入力して、対話型コマンド プロセスを開始します。
3. コマンド プロンプトから環境を選択します。
4. CI/CD プロバイダーとして **[Azure DevOps]** を選択します。
5. [CI]、[CD]、[プロビジョニング]、[Teams に発行] のオプションから 1 つ以上のテンプレートを選択します。
7. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
8. `.azure/pipelines` にある README ファイルに従って、Azure DevOps でワークフローを設定します。

> [!NOTE]
> 追加のワークフロー テンプレートを追加する必要がある場合、同じ手順に従って、Visual Studio Code または TeamsFx CLI でワークフロー テンプレートを作成できます。

### <a name="customize-ci-workflow"></a>CI ワークフローをカスタマイズする

スクリプトまたはワークフロー定義に対して次の変更を行うことができます。

1. npm ビルド スクリプトを使用するか、オートメーション コードでビルドする方法をカスタマイズします。
1. 成功するとゼロを返す npm テスト スクリプトを使用して、テスト コマンドを変更します。

### <a name="customize-cd-workflow"></a>CD ワークフローをカスタマイズする

スクリプトまたはワークフロー定義に対して次の変更を行うことができます。

1. npm ビルド スクリプトがあることを確認するか、オートメーション コードでビルドする方法をカスタマイズします。
1. 成功するとゼロを返す npm テスト スクリプトがあることを確認するか、テスト コマンドを変更します。

## <a name="set-up-pipelines-with-jenkins"></a>Jenkins を使用してパイプラインを設定する

CI/CD で Jenkins を使用してパイプラインを設定するには:

* ワークフロー テンプレートを作成します。

  * Visual Studio Code
  * TeamsFx CLI

* CI/CD ワークフローをカスタマイズします。

### <a name="create-workflow-templates"></a>ワークフロー テンプレートを作成する

Jenkins を使用して、次のワークフロー テンプレートを作成できます。

**Visual Studio Codeの Teams ツールキット**

1. Teams Toolkit を使用して新しい Teams アプリを作成します。
2. 左側のウィンドウで **Teams Toolkit** アイコン :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: を選択します。
3. **[CI/CD ワークフローの追加]** を選択します。
4. コマンド プロンプトから環境を選択します。
5. CI/CD プロバイダーとして **[Jenkins]** を選択します。
6. [CI]、[CD]、[プロビジョニング]、[Teams に発行] のオプションから 1 つ以上のテンプレートを選択します。
7. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
8. `.jenkins/pipelines` にある README ファイルに従って、Jenkins でワークフローを設定します。

**TeamsFx CLI**

1. Teams アプリ プロジェクト ディレクトリに「`cd`」と入力します。
2. `teamsfx add cicd` コマンドを入力して、対話型コマンド プロセスを開始します。
3. コマンド プロンプトから環境を選択します。
4. CI/CD プロバイダーとして **[Jenkins]** を選択します。
5. [CI]、[CD]、[プロビジョニング]、[Teams に発行] のオプションから 1 つ以上のテンプレートを選択します。
7. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
8. `.jenkins/pipelines` にある README ファイルに従って、Jenkins でワークフローを設定します。

> [!NOTE]
> 追加のワークフロー テンプレートを追加する必要がある場合、同じ手順に従って、Visual Studio Code または TeamsFx CLI でワークフロー テンプレートを作成できます。

### <a name="customize-ci-workflow"></a>CI ワークフローをカスタマイズする

プロジェクトに次の変更を加えることができます。

1. CI フローのトリガー方法を変更します。既定では、新しい変更が **dev** ブランチにプッシュされると **pollSCM** トリガーが使用されます。
1. npm ビルド スクリプトがあることを確認するか、オートメーション コードでビルドする方法をカスタマイズします。
1. 成功するとゼロを返す npm テスト スクリプトがあることを確認するか、テスト コマンドを変更します。

### <a name="customize-cd-workflow"></a>CD ワークフローをカスタマイズする

CD パイプラインをカスタマイズするには、次の手順を実行します。

1. CD フローを変更します。既定では、新しい変更が `main` ブランチにプッシュされると `pollSCM` トリガーが使用されます。
1. 必要に応じてビルド スクリプトを変更します。
1. テストがない場合は、テスト スクリプトを削除します。

## <a name="set-up-pipelines-for-other-platforms"></a>他のプラットフォームのパイプラインを設定する

定義済みの bash スクリプトの例に従って、他のプラットフォームで CI/CD パイプラインをビルドおよびカスタマイズできます。

* [CI スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

これらのスクリプトは、クロスプラットフォームの TeamsFx コマンド ライン ツール [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) に基づいています。 `npm install -g @microsoft/teamsfx-cli` でインストールして、[ドキュメント](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)に従ってスクリプトをカスタマイズできます。

> [!NOTE]
>
> * CI モードで `@microsoft/teamsfx-cli` の実行を有効にするには、`export CI_ENABLED=true` を使用して `CI_ENABLED` をオンにします。 CI モードでは、`@microsoft/teamsfx-cli` は CI/CD に適しています。
> * 非対話型モードで `@microsoft/teamsfx-cli` の実行を有効にするには、次のコマンドを使用してグローバル構成を設定します: `teamsfx config set -g interactive false`。 非対話型モードでは、`@microsoft/teamsfx-cli` によって入力を求めるメッセージは表示されません。

必ず環境変数に Azure と Microsoft 365 の資格情報を安全に設定してください。 たとえば、ソース コード リポジトリとして GitHub を使用している場合は、「[GitHub シークレット](https://docs.github.com/en/actions/reference/encrypted-secrets)」を参照してください。

## <a name="provision-and-deploy-resources"></a>リソースをプロビジョニングおよび展開する

CI/CD 内で Azure を対象とするリソースをプロビジョニングおよび展開するには、使用する Azure サービス プリンシパルを作成する必要があります。

Azure サービス プリンシパルを作成するには、次の手順に従います。

1. Microsoft Azure Active Directory (Azure AD) アプリケーションをシングル テナントに登録します。
2. Azure AD アプリケーションに、Azure サブスクリプションにアクセスするためのロールを割り当てます。`Contributor` ロールをお勧めします。
3. 新しい Azure AD アプリケーション シークレットを作成します。

> [!TIP]
> 今後使用できるように、テナント ID、アプリケーション ID (AZURE_SERVICE_PRINCIPAL_NAME)、シークレット (AZURE_SERVICE_PRINCIPAL_PASSWORD) を保存します。

詳細については、「[Azure サービス プリンシパルのガイドライン](/azure/active-directory/develop/howto-create-service-principal-portal)」を参照してください。 サービス プリンシパルを作成する 3 つの方法を次に示します。

* [Microsoft Azure ポータル](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Teams 開発者ポータルを使用して Teams アプリを発行する

Teams アプリのマニフェスト ファイルに関連する変更がある場合は、マニフェストを更新して、Teams アプリをもう一度発行できます。 Teams アプリを手動で発行するために、[Teams の開発者ポータル](https://dev.teams.microsoft.com/home)を使用できます。

アプリを発行するには、次の手順に従います。

1. 対応するアカウントを使用して [Teams の開発者ポータル](https://dev.teams.microsoft.com) にサインインします。
2. zip でアプリ パッケージをインポートし、 を選択します `App -> Import app -> Replace`。
3. アプリの一覧でターゲット アプリを選択します。
4. アプリを発行し、 を選択します `Publish -> Publish to your org`。

## <a name="see-also"></a>関連項目

* [GitHub アクションのクイック スタート](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [初めての Azure DevOps パイプラインを作成する](/azure/devops/pipelines/create-first-pipeline)
* [初めての Jenkins パイプラインを作成する](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Microsoft Teams の開発者ポータルを使用してアプリを管理する](../concepts/build-and-test/teams-developer-portal.md)
