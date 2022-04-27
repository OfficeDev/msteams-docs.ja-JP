---
title: Teams アプリケーション開発者向けの GitHub、Azure DevOps、および Jenkins で CI/CD パイプライン テンプレートを使用する方法について説明します
author: MuyangAmigo
description: CI/CD テンプレート
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 66560b1f228c32b0faf6569ff0ae536a81dc33c0
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073294"
---
# <a name="set-up-cicd-pipelines"></a>CI/CD パイプラインを設定する

TeamsFx は、アプリケーションの構築中に開発ワークフロー Teams自動化するのに役立ちます。 CI/CD パイプラインのセットアップ、ワークフロー テンプレートの作成、GitHub、Azure DevOps、Jenkins などのプラットフォームを使用した CI/CD ワークフローのカスタマイズに使用できるツールとテンプレートを次に示します。 リソースをプロビジョニングしてデプロイするには、Teams Developer Portal を使用して Azure サービス プリンシパルを作成し、Teams アプリを発行します。 アプリTeams手動で発行するには、[開発者ポータルを利用してTeams](https://dev.teams.microsoft.com/home)できます。


|ツールとテンプレート | 説明 |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|TeamsFx CLI と統合するGitHubアクション。|
|[Visual Studio CodeのTeams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Teams アプリの開発に役立つVisual Studio Code拡張機能と、GitHub、Azure DevOps、および Jenkins の自動化ワークフロー。 |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | GitHub、Azure DevOps、および Jenkins の自動化ワークフローだけでなく、Teams アプリの開発に役立つコマンド ライン ツール。|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) と [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| GitHub、Azure DevOps、または Jenkins 以外のオートメーション用のスクリプト テンプレート。 |


## <a name="set-up-pipelines"></a>パイプラインを設定する

パイプラインは、次のプラットフォームで設定できます。

1. [GitHubを使用してパイプラインを設定する](#set-up-pipelines-with-github)
1. [Azure DevOpsを使用してパイプラインを設定する](#set-up-pipelines-with-azure-devops)
1. [Jenkins を使用してパイプラインを設定する](#set-up-pipelines-with-jenkins)
1. [他のプラットフォームのパイプラインを設定する](#set-up-pipelines-for-other-platforms)


### <a name="set-up-pipelines-with-github"></a>GitHubを使用してパイプラインを設定する

CI/CD のGitHubを使用してパイプラインを設定するには:

1. ワークフロー テンプレートを作成します。

   * Visual Studio Code
   * TeamsFx CLI

1. CI/CD ワークフローをカスタマイズする。


## <a name="create-workflow-templates-with-github"></a>GitHubを使用してワークフロー テンプレートを作成する

**Visual Studio CodeのTeams Toolkitを使用してワークフロー テンプレートを作成する**

1. Teams Toolkitを使用して、新しいTeams アプリ プロジェクトを作成します。
1. **Visual Studio Code** アクティビティ バーでTeams Toolkitアイコンを選択します。
1. [ **CI/CD ワークフローの追加]** を選択します。
1. コマンド プロンプトから環境を選択します。
1. CI/CD プロバイダーとして **GitHub** を選択します。
1. これらのオプションから少なくとも 1 つのテンプレート (CI、CD、プロビジョニング、またはTeamsに発行) を選択します。
1. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
1. README `.github/workflows` ファイルに従って、GitHubでワークフローを設定します。

**TeamsFx CLI を使用してワークフロー テンプレートを作成する**

1. Teams アプリ プロジェクト ディレクトリに入力`cd`します。
2. コマンドを入力 `teamsfx add cicd` して、対話型コマンド プロセスを開始します。
3. コマンド プロンプトから環境を選択します。
4. CI/CD プロバイダーとして **GitHub** を選択します。
5. これらのオプションから少なくとも 1 つのテンプレート (CI、CD、プロビジョニング、またはTeamsに発行) を選択します。
7. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
8. README `.github/workflows` ファイルに従って、GitHubでワークフローを設定します。

> [!NOTE]
> ワークフロー テンプレートを追加する必要がある場合は、同じ手順に従って、Visual Studio Codeまたは TeamsFx CLI でワークフロー テンプレートを作成できます。

### <a name="customize-cicd-workflow"></a>CI/CD ワークフローをカスタマイズする

テスト スクリプトを変更または削除して、CI/CD ワークフローをカスタマイズできます。

1. 既定では、ブランチに対して新しいコミットが行われる `main` と、CD ワークフローがトリガーされます。
1. 必要に応じてビルド スクリプトを変更します。
1. 必要に応じてテスト スクリプトを削除します。

### <a name="set-up-pipelines-with-azure-devops"></a>Azure DevOpsを使用してパイプラインを設定する

CI/CD のAzure DevOpsを使用してパイプラインを設定するには:

1. ワークフロー テンプレートを作成します。

   * Visual Studio Code
   * TeamsFx CLI

1. CI/CD ワークフローをカスタマイズする。


## <a name="create-workflow-templates-with-azure-devops"></a>Azure DevOpsを使用してワークフロー テンプレートを作成する

**Visual Studio CodeのTeams Toolkitを使用してワークフロー テンプレートを作成する**

1. Teams Toolkitを使用して、新しいTeams アプリ プロジェクトを作成します。
2. **Visual Studio Code** アクティビティ バーでTeams Toolkitアイコンを選択します。
3. [ **CI/CD ワークフローの追加]** を選択します。
4. コマンド プロンプトから環境を選択します。
5. CI/CD プロバイダーとして **Azure DevOps** を選択します。
6. 次のオプションから少なくとも 1 つのテンプレート (CI、CD、プロビジョニング、およびTeamsに発行) を選択します。
7. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
8. README ファイル`.azure/pipelines`に従って、Azure DevOpsでワークフローを設定します。

**TeamsFx CLI を使用してワークフロー テンプレートを作成する**

1. Teams アプリ プロジェクト ディレクトリに入力`cd`します。
2. コマンドを入力 `teamsfx add cicd` して、対話型コマンド プロセスを開始します。
3. コマンド プロンプトから環境を選択します。
4. CI/CD プロバイダーとして **Azure DevOps** を選択します。
5. これらのオプションから少なくとも 1 つのテンプレート (CI、CD、プロビジョニング、またはTeamsに発行) を選択します。
7. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
8. README ファイル`.azure/pipelines`に従って、Azure DevOpsでワークフローを設定します。

> [!NOTE]
> ワークフロー テンプレートを追加する必要がある場合は、同じ手順に従って、Visual Studio Codeまたは TeamsFx CLI でワークフロー テンプレートを作成できます。

### <a name="customize-ci-workflow"></a>CI ワークフローをカスタマイズする

スクリプトまたはワークフロー定義に対して行うことができる変更を次に示します。

1. npm ビルド スクリプトを使用するか、オートメーション コードでビルドする方法をカスタマイズします。
1. 成功のためにゼロを返す npm テスト スクリプトを使用し、テスト コマンドを変更します。

### <a name="customize-cd-workflow"></a>CD ワークフローをカスタマイズする

スクリプトまたはワークフロー定義に対して行うことができる変更を次に示します。

1. npm ビルド スクリプトがあることを確認するか、オートメーション コードでビルドする方法をカスタマイズします。
1. 成功した場合は 0 を返すか、テスト コマンドを変更する npm テスト スクリプトがあることを確認します。

### <a name="set-up-pipelines-with-jenkins"></a>Jenkins を使用してパイプラインを設定する

CI/CD 用に Jenkins を使用してパイプラインを設定するには:

1. ワークフロー テンプレートを作成します。

   * Visual Studio Code
   * TeamsFx CLI

1. CI/CD ワークフローをカスタマイズする。

## <a name="create-workflow-templates-with-jenkins"></a>Jenkins を使用してワークフロー テンプレートを作成する

**Visual Studio CodeのTeams Toolkitを使用してワークフロー テンプレートを作成する**

1. Teams Toolkitを使用して、新しいTeams アプリ プロジェクトを作成します。
2. **Visual Studio Code** サイドバーでTeams Toolkitアイコンを選択します。
3. [ **CI/CD ワークフローの追加]** を選択します。
4. コマンド プロンプトから環境を選択します。
5. CI/CD プロバイダーとして **Jenkins** を選択します。
6. これらのオプションから少なくとも 1 つのテンプレート (CI、CD、プロビジョニング、またはTeamsに発行) を選択します。
7. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
8. 下の README ファイル `.jenkins/pipelines` に従って、Jenkins でワークフローを設定します。

**TeamsFx CLI を使用してワークフロー テンプレートを作成する**

1. Teams アプリ プロジェクト ディレクトリに入力`cd`します。
2. コマンドを入力 `teamsfx add cicd` して、対話型コマンド プロセスを開始します。
3. コマンド プロンプトから環境を選択します。
4. CI/CD プロバイダーとして **Jenkins** を選択します。
5. これらのオプションから少なくとも 1 つのテンプレート (CI、CD、プロビジョニング、またはTeamsに発行) を選択します。
7. テンプレートを開き、シナリオに合ったワークフローをカスタマイズします。
8. 下の README ファイル `.jenkins/pipelines` に従って、Jenkins でワークフローを設定します。

> [!NOTE]
> ワークフロー テンプレートを追加する必要がある場合は、同じ手順に従って、Visual Studio Codeまたは TeamsFx CLI でワークフロー テンプレートを作成できます。

### <a name="customize-ci-workflow"></a>CI ワークフローをカスタマイズする

プロジェクトに対して行うことができる変更の一部を次に示します。

1. CI フローのトリガー方法を変更します。 既定値は、新しい変更が **開発** ブランチにプッシュされたときに **pollSCM** のトリガーを使用することです。
1. npm ビルド スクリプトがあることを確認するか、オートメーション コードでビルドする方法をカスタマイズします。
1. 成功した場合は 0 を返すか、テスト コマンドを変更する npm テスト スクリプトがあることを確認します。


### <a name="customize-cd-workflow"></a>CD ワークフローをカスタマイズする

CD パイプラインをカスタマイズするには、次の手順を実行します。

1. CD フローを変更します。 既定では、新しい変更がブランチにプッシュされたときの `pollSCM` トリガーを `main` 使用します。
1. 必要に応じてビルド スクリプトを変更します。
1. テストがない場合は、テスト スクリプトを削除します。


### <a name="set-up-pipelines-for-other-platforms"></a>他のプラットフォームのパイプラインを設定する

定義済みの bash スクリプトの例に従って、他のプラットフォームで CI/CD パイプラインをビルドおよびカスタマイズできます。

* [CI スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

スクリプトは、クロスプラットフォームの TeamsFx コマンド ライン ツール [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) に基づいています。 このスクリプトを `npm install -g @microsoft/teamsfx-cli` インストールし、 [ドキュメント](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) に従ってスクリプトをカスタマイズできます。

> [!NOTE]
>
> * CI モードで実行を有効 `@microsoft/teamsfx-cli` にするには、次の操作を行 `CI_ENABLED` います `export CI_ENABLED=true`。 CI モードでは、 `@microsoft/teamsfx-cli` CI/CD に適しています。
> * 非対話型モードで実行を有効 `@microsoft/teamsfx-cli` にするには、次のコマンドを使用してグローバル構成を設定します `teamsfx config set -g interactive false`。 非対話型モードでは、 `@microsoft/teamsfx-cli` 入力を求めるメッセージは表示されません。

環境変数に Azure とMicrosoft 365資格情報を安全に設定してください。 たとえば、ソース コード リポジトリとしてGitHubを使用している場合は、[Github Secrets](https://docs.github.com/en/actions/reference/encrypted-secrets) に関するページを参照してください。


## <a name="provision-and-deploy-resources"></a>リソースのプロビジョニングとデプロイ

CI/CD 内で Azure をターゲットとするリソースをプロビジョニングしてデプロイするには、使用する Azure サービス プリンシパルを作成する必要があります。

Azure サービス プリンシパルを作成するには、次の手順に従います。

1. Microsoft Azure Active Directory (Azure AD) アプリケーションをシングル テナントに登録します。
2. azure サブスクリプションにアクセスするために、Azure AD アプリケーションにロールを割り当てます。 ロールをお `Contributor` 勧めします。
3. 新しいAzure ADアプリケーション シークレットを作成します。

> [!TIP]
> 今後使用できるように、テナント ID、アプリケーション ID (AZURE_SERVICE_PRINCIPAL_NAME)、シークレット (AZURE_SERVICE_PRINCIPAL_PASSWORD) を保存します。

詳細については、 [Azure サービス プリンシパルのガイドラインに関するページを](/azure/active-directory/develop/howto-create-service-principal-portal)参照してください。 サービス プリンシパルを作成する 3 つの方法を次に示します。

* [Microsoft Azure ポータル](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [MICROSOFT AZURE CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Teams開発者ポータルを使用してアプリTeams発行する

Teams アプリのマニフェスト ファイルに関連する変更がある場合は、マニフェストを更新して、Teams アプリをもう一度発行できます。

アプリTeams手動で発行するには、[開発者ポータルを利用してTeams](https://dev.teams.microsoft.com/home)できます。

アプリを発行するには、次の手順に従います。

1. 対応するアカウントを使用して[Teams開発者ポータル](https://dev.teams.microsoft.com)にサインインします。
2. を選択して、zip 形式でアプリ パッケージをインポートします `App -> Import app -> Replace`。
3. アプリの一覧でターゲット アプリを選択します。
4. を選択してアプリを発行します `Publish -> Publish to your org`。

### <a name="see-also"></a>関連項目

* [GitHub Actionsのクイック スタート](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [最初のAzure DevOps パイプラインを作成する](/azure/devops/pipelines/create-first-pipeline)
* [初めての Jenkins パイプラインを作成する](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Microsoft Teams の開発者ポータルを使用してアプリを管理する](/concepts/build-and-test/teams-developer-portal)
