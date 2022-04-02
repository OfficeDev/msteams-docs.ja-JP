---
title: アプリケーション開発者向けの CI または CD パイプライン テンプレートGitHub Azure Devops、Jenkins で使用するTeams説明します。
author: MuyangAmigo
description: CICD テンプレート
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 5fa12248969f589282ecf8fd80c4d908ff42e8d8
ms.sourcegitcommit: 2236204ff710f4eca606ceffb233572981f6edbe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2022
ms.locfileid: "64614538"
---
# <a name="cicd-guide"></a>CI/CD ガイド

TeamsFx は、アプリケーションの構築中に開発ワークフローをTeamsします。 このドキュメントには、CI または CD パイプラインのセットアップを開始するためのツールとテンプレートが記載されています。GitHub Azure Devops、Jenkins を使用します。

|ツールとテンプレート|説明|
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|GitHub TeamsFx CLI と統合するアクション。|
|[github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) と [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHubアプリの CI または CD テンプレートTeamsします。 |
|[jenkins-ci-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) と [jenkins-cd-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|アプリの Jenkins CI または CD テンプレートTeamsします。|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) と [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| スクリプト テンプレートを使用して、GitHub。 |

## <a name="ci-or-cd-workflow-templates-in-github"></a>CI または CD ワークフロー テンプレート (GitHub

**CI または CD ワークフローを含め**、アプリTeamsプロセスを自動化するには、次GitHub。

1. [フォルダーの作成] `.github/workflows`
1. 次のいずれかのテンプレート ファイルをコピーします。
    * [github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) for CI ワークフロー。
    * [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml) for CD ワークフロー。
1. シナリオに合ったワークフローをカスタマイズします。

### <a name="customize-ci-workflow"></a>CI ワークフローのカスタマイズ

プロジェクトのワークフローを調整するには、次の手順を実行します。

1. CI フローを変更します。
1. npm ビルド スクリプトを使用するか、オートメーション コードでプロジェクトをビルドする方法をカスタマイズします。
1. 成功するためにゼロを返す npm テスト スクリプトを使用し、テスト コマンドを変更します。

### <a name="customize-cd-workflow"></a>CD ワークフローのカスタマイズ

以下の手順を実行して、CD ワークフローをカスタマイズします。

1. 既定では、新しいコミットがブランチに対して行われたときに、CD ワークフローがトリガー `main` されます。
1. 環境GitHub[リポジトリ シークレットを作成](https://docs.github.com/en/actions/reference/encrypted-secrets)して、Azure サービス プリンシパルを保持し、Microsoft 365ログイン資格情報を保持します。 詳細については、「GitHub Actions」[を参照してください](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md)。
1. 必要に応じてビルド スクリプトを変更します。
1. 必要に応じてテスト スクリプトを削除します。

> [!NOTE]
> 通常は 1 回しか実行されないので、プロビジョニング 手順は CD テンプレートには含まれません。 プロビジョニングは、Teams Toolkit TeamsFx CLI 内で実行するか、別のワークフローを使用して実行できます。 プロビジョニング後にコミットしてください。 プロビジョニングの結果はフォルダーに保存 `.fx` されます。

### <a name="github-secrets"></a>Github シークレット

次の表に、環境を作成するために必要なすべてのシークレットを次の表GitHub。

1. [**設定**] を選択します。
1. [環境] **セクションに移動** します。
1. [新 **しい環境] を選択します**。
1. 環境の名前を入力します。 テンプレートに指定されている既定の環境名はです `test_environment`。
1. [環境 **の構成] を選択します**。
1. [シークレット **の追加] を選択します**。

次の表に、環境の作成に必要なすべてのシークレットを示します。

|名前|説明|
|---|---|
|`AZURE_SERVICE_PRINCIPAL_NAME`|リソースのプロビジョニングに使用される Azure のサービス プリンシパル名。|
|`AZURE_SERVICE_PRINCIPAL_PASSWORD`|Azure サービス プリンシパルのパスワード。|
|`AZURE_SUBSCRIPTION_ID`|リソースがプロビジョニングされるサブスクリプションを特定します。|
|`AZURE_TENANT_ID`|サブスクリプションが存在するテナントを識別します。|
|`M365_ACCOUNT_NAME`|アプリMicrosoft 365発行するアカウントをTeamsします。|
|`M365_ACCOUNT_PASSWORD`|アカウントのパスワードMicrosoft 365します。|
|`M365_TENANT_ID`|アプリを作成/発行するTeamsを特定します。 マルチテナント アカウントを持ち、別のテナントを使用しない限り、この値はオプションです。 詳細については、「テナント [ID を検索するMicrosoft 365参照してください](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)。|

> [!NOTE]
> 現在、Azure のサービス プリンシパルは CI/CD ワークフローで使用されています。 詳細については、「 [Create Azure Service principles」を参照してください](#create-azure-service-principals)。

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>CI または CD パイプラインをセットアップするには、Azure DevOps

自動化されたパイプラインは、Azure DevOpsで設定し、スクリプトを参照できます。

開始するには、次の手順を実行します。

* [CI スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>CI パイプラインのセットアップ

1. CI [スクリプトを](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) Azure DevOpsリポジトリに追加し、スクリプト ファイル内のコメントから考え出す場合に必要なカスタマイズを行います。
1. 手順に[従って、CI 用パイプラインAzure DevOps作成します](/azure/devops/pipelines/create-first-pipeline)。
一般的な CI パイプライン スクリプトのシナリオを次に示します。

```yml
trigger:
- dev 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true
  
- task: Bash@3
  inputs:
    filePath: './others-script-ci-template.sh'
```

スクリプトまたはワークフロー定義に対して行える変更を次に示します。

1. CI フローを変更します。 既定では、新しいコミットがブランチにプッシュされます `dev` 。
1. ノードと npm のインストール方法を変更します。
1. npm ビルド スクリプトを使用するか、オートメーション コードでのビルド方法をカスタマイズします。
1. 成功するためにゼロを返す npm テスト スクリプトを使用し、テスト コマンドを変更します。

### <a name="set-up-cd-pipeline"></a>CD パイプラインのセットアップ

1. CD [スクリプトを](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) Azure DevOpsリポジトリに追加し、スクリプト ファイル内のコメントから確認できる必要なカスタマイズを行います。
1. CD 用のAzure DevOpsパイプラインを作成します。 詳細については、「Create [first pipeline」を参照してください](/azure/devops/pipelines/create-first-pipeline)。 パイプラインの定義は、CI パイプラインの次の定義例を参照できます。
1. [変数の定義] [で必要な](/azure/devops/pipelines/process/variables)変数を追加し、必要に応じてシークレットとして作成します。

```yml
trigger:
- main 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true
  
- task: Bash@3
  env:
    SP_NAME: $(AZURE_SERVICE_PRINCIPAL_NAME)
    SP_PASSWORD: $(AZURE_SERVICE_PRINCIPAL_PASSWORD)
    TENANT_ID: $(AZURE_TENANT_ID)
    AZURE_SUBSCRIPTION_ID: $(AZURE_SUBSCRIPTION_ID)
    M365_ACCOUNT_NAME: $(M365_ACCOUNT_NAME)
    M365_ACCOUNT_PASSWORD: $(M365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

スクリプトまたはワークフロー定義に対して行える変更を次に示します。

1. CD フローのトリガー方法。 既定では、メイン ブランチに対して新しいコミットが行われたときに **発生** します。
1. ノードと npm のインストール方法を変更します。
1. 既定では、ステージング環境名を変更 **します**。
1. npm ビルド スクリプトを使用するか、オートメーション コードでのビルド方法をカスタマイズします。
1. 成功した場合は 0 を返す npm テスト スクリプトを使用し、テスト コマンドを変更してください。

### <a name="pipeline-variables-for-azure-devops"></a>パイプライン変数のAzure DevOps

次の手順を実行して、パイプライン変数を作成Azure DevOps。

1. [パイプラインの編集] ページで、[変数] **を選択し、[** 新しい変数] **を選択します**。
1. 変数の [名前] または [値のペア] を入力します。
1. 必要に応じて、[この値を **秘密にする] のチェック ボックス** をオフにします。
1. [ **OK] を** 選択して変数を作成します。

|名前|説明|
|---|---|
|`AZURE_SERVICE_PRINCIPAL_NAME`|リソースのプロビジョニングに使用される Azure のサービス プリンシパル名。|
|`AZURE_SERVICE_PRINCIPAL_PASSWORD`|Azure サービス プリンシパルのパスワード。|
|`AZURE_SUBSCRIPTION_ID`|リソースがプロビジョニングされるサブスクリプションを識別します。|
|`AZURE_TENANT_ID`|サブスクリプションが存在するテナントを識別します。|
|`M365_ACCOUNT_NAME`|アプリMicrosoft 365発行するためのアカウントをTeamsします。|
|`M365_ACCOUNT_PASSWORD`|アカウントのパスワードMicrosoft 365します。|
|`M365_TENANT_ID`|アプリが作成または発行されるテナントTeams識別します。 マルチテナント アカウントを持ち、別のテナントを使用しない限り、この値はオプションです。 テナント ID を[検索する方法の詳細Microsoft 365参照してください](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)。|

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Jenkins の CI または CD パイプライン テンプレート

これらのテンプレートをリポジトリに追加するには、 [jenkins-ci-template のバージョンが必要です。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) と  [jenkins-cd-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile) をブランチ別にリポジトリに保存します。

また、Jenkins で CI または CD パイプラインを作成し、それに応じて特定のパイプラインを指す必要 `Jenkinsfile` があります。

手順に従って、Jenkins をさまざまな SCM プラットフォームに接続する方法を確認します。

1. [Jenkins with GitHub](https://www.jenkins.io/solutions/github/)
2. [Jenkins with Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [GitLab を使用した Jenkins](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [Jenkins with Bitbucket](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>CI パイプラインのカスタマイズ

プロジェクトを調整するために行える変更の一部を次に示します。

1. テンプレート ファイルの名前を **Jenkinsfile** に変更し、ターゲット ブランチ (開発ブランチなど) の下に **配置** します。
1. CI フローのトリガー方法を変更します。 新しい変更が開発ブランチにプッシュされる場合、 **既定では pollSCM** のトリガーを **使用** します。
1. npm ビルド スクリプトを使用するか、オートメーション コードでのビルド方法をカスタマイズします。
1. 成功した場合は 0 を返す npm テスト スクリプトを使用し、テスト コマンドを変更してください。

### <a name="customize-cd-pipeline"></a>CD パイプラインのカスタマイズ

次の手順を実行して、CD パイプラインをカスタマイズします。

1. テンプレート ファイルの名前を 、 `Jenkinsfile`に変更し、ブランチなど、ターゲット ブランチに配置 `main` します。
1. CD フローを変更します。 既定では、新しい変更が `pollSCM` ブランチにプッシュされるトリガーを使用 `main` します。
1. Jenkins パイプライン[資格情報を作成](https://www.jenkins.io/doc/book/using/using-credentials/)して、Azure サービス プリンシパルを保持し、Microsoft 365ログイン資格情報を保持します。
1. 必要に応じてビルド スクリプトを変更します。
1. テストを実行しない場合は、テスト スクリプトを削除します。

### <a name="credentials-for-jenkins"></a>Jenkins の資格情報

[Using-credentials に従って](https://www.jenkins.io/doc/book/using/using-credentials/) Jenkins に資格情報を作成します。

|名前|説明|
|---|---|
|`AZURE_SERVICE_PRINCIPAL_NAME`|リソースのプロビジョニングに使用される Azure のサービス プリンシパル名。|
|`AZURE_SERVICE_PRINCIPAL_PASSWORD`|Azure サービス プリンシパルのパスワード。|
|`AZURE_SUBSCRIPTION_ID`|リソースがプロビジョニングされるサブスクリプションを特定します。|
|`AZURE_TENANT_ID`|サブスクリプションが存在するテナントを識別します。|
|`M365_ACCOUNT_NAME`|アプリMicrosoft 365発行するためのアカウントをTeamsします。|
|`M365_ACCOUNT_PASSWORD`|アカウントのパスワードMicrosoft 365します。|
|`M365_TENANT_ID`|アプリが作成または発行されるテナントTeams識別します。 マルチテナント アカウントを持ち、別のテナントを使用する場合を指定しない限り、この値は省略可能です。 テナント ID を[検索する方法の詳細Microsoft 365参照してください](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)。|

## <a name="get-started-guide-for-other-platforms"></a>概要プラットフォームの詳細ガイド

リストされている定義済みの bash スクリプトの例に従って、他のプラットフォームで CI または CD パイプラインをビルドおよびカスタマイズできます。

* [CI スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

スクリプトは、クロスプラットフォームの TeamsFx コマンド ライン ツール [TeamsFx-CLI に基づいて作成されます](https://www.npmjs.com/package/@microsoft/teamsfx-cli)。 このスクリプトをインストールし `npm install -g @microsoft/teamsfx-cli` 、ドキュメントに [従って](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) スクリプトをカスタマイズできます。

> [!NOTE]
>
> * CI モードで `@microsoft/teamsfx-cli` 実行を有効にするには、次の方法でオン `CI_ENABLED` にします `export CI_ENABLED=true`。 CI モードでは、 `@microsoft/teamsfx-cli` CI または CD に対応しています。
> * 非対話型モード`@microsoft/teamsfx-cli`での実行を有効にするには、コマンドを使用してグローバル構成を設定します。 `teamsfx config set -g interactive false` 非対話型モードでは、入力 `@microsoft/teamsfx-cli` を求めるメッセージは表示されません。

必ず、環境変数に Azure Microsoft 365資格情報を安全に設定してください。 たとえば、ソース コード リポジトリとしてGitHub使用している場合などです。 詳細については、「 [Github Secrets」を参照してください](https://docs.github.com/en/actions/reference/encrypted-secrets)。

## <a name="create-azure-service-principals"></a>Azure サービス プリンシパルの作成

CI/CD 内で Azure を対象とするリソースをプロビジョニングおよび展開するには、使用する Azure サービス プリンシパルを作成する必要があります。

Azure サービス プリンシパルを作成するには、次の手順を実行します。

1. 単一テナントMicrosoft Azure Active Directory (Azure AD) アプリケーションを登録します。
2. Azure サブスクリプションにアクセスするには、Azure ADアプリケーション`Contributor`にロールを割り当て、ロールをお勧めします。
3. 新しいアプリケーション シークレットAzure AD作成します。

> [!TIP]
> 将来使用するために、テナント ID、アプリケーション id(AZURE_SERVICE_PRINCIPAL_NAME)、および secret(AZURE_SERVICE_PRINCIPAL_PASSWORD) を保存します。

詳細については、「 [Azure サービス プリンシパルのガイドライン」を参照してください](/azure/active-directory/develop/howto-create-service-principal-portal)。 サービス プリンシパルを作成する 3 つの方法を次に示します。

* [Microsoft Azure ポータル](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>開発者ポータルTeamsを使用Teamsアプリを発行する

アプリのマニフェスト ファイルに関連Teams変更がある場合は、マニフェストを更新するために、Teamsアプリを再度発行できます。

アプリを手動Teams発行するには、開発者ポータルを使用してアプリ[をTeams](https://dev.teams.microsoft.com/home)。

アプリを発行するには、次の手順を実行します。

1. 対応するアカウントを[使用Teams](https://dev.teams.microsoft.com)開発者ポータルにサインインします。
2. を選択して、アプリ パッケージを zip にインポートします `App -> Import app -> Replace`。
3. アプリ一覧でターゲット アプリを選択します。
4. 選択してアプリを発行する `Publish -> Publish to your org`

### <a name="see-also"></a>関連項目

* [クイック スタートのGitHub Actions](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [最初のパイプラインをAzure DevOpsする](/azure/devops/pipelines/create-first-pipeline)
* [最初の Jenkins パイプラインを作成する](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Microsoft Teams の開発者ポータルを使用してアプリを管理する](/concepts/build-and-test/teams-developer-portal)
