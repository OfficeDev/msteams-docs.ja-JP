---
title: CI または CD アプリケーション開発者向Teamsサポート
author: MuyangAmigo
description: CICD テンプレート
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ff5b77b7891d36e63f2fd3260ae114cbf536384d
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228045"
---
# <a name="ci-or-cd-support-for-teams-application-developers"></a>アプリケーション開発者向けの CI または CD Teamsサポート

TeamsFx は、アプリケーションの構築中に開発ワークフローをTeamsします。 このドキュメントには、GitHub、Azure Devops、Jenkins などの最も一般的な開発プラットフォームを使用して CI または CD パイプラインをセットアップする場合に使用するツールと事前に作成されたテンプレートが用意されています。


|ツールとテンプレート|説明|
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|TeamsFx CLI と統合GitHubすぐに使用できるアクション。|
|[github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) と [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHubアプリの CI テンプレートまたは CD テンプレートTeamsします。 |
|[jenkins-ci-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) と [jenkins-cd-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|アプリの Jenkins CI または CD テンプレートTeamsします。|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) と [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| オートメーション用のスクリプト テンプレートは、GitHub。 |

## <a name="ci-or-cd-workflow-templates-in-github"></a>ワークフロー内の CI または CD ワークフロー GitHub

**CI または CD ワークフローを含め、** アプリTeamsプロセスを自動化するには、次GitHub。

1. [フォルダーの作成] `.github/workflows`
1. テンプレート ファイル (一方または両方) をコピーします。
    * [github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) for CI ワークフロー。
    * [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml) for CD ワークフロー。
1. シナリオに合わせてこれらのワークフローをカスタマイズします。

### <a name="customize-ci-workflow"></a>CI ワークフローのカスタマイズ

次の変更を行って、プロジェクトのワークフローを調整できます。

1. CI フローのトリガー方法を変更します。 既定では、ブランチを対象とするプル要求が作成 `dev` されます。
1. npm ビルド スクリプトを使用するか、オートメーション コードでプロジェクトをビルドする方法をカスタマイズします。
1. 成功のためにゼロを返す npm テスト スクリプトを使用するか、テスト コマンドを変更します。

### <a name="customize-cd-workflow"></a>CD ワークフローのカスタマイズ

CD ワークフローをカスタマイズするには、次の手順を実行します。

1. 既定では、新しいコミットがブランチに対して行われたときに、CD ワークフローがトリガー `main` されます。
1. 環境GitHub[リポジトリ シークレット](https://docs.github.com/en/actions/reference/encrypted-secrets)を作成して、Azure またはログイン資格情報Microsoft 365保持します。 次の表に、GitHub で作成する必要があるすべてのシークレットを示し、詳細な使用方法については、「GitHub アクション」README.md を[参照してください](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md)。
1. 必要に応じてビルド スクリプトを変更します。
1. テストを実行しない場合は、テスト スクリプトを削除します。

> [!Note]
> 通常は 1 回しか実行されないので、プロビジョニング 手順は CD テンプレートには含まれません。 プロビジョニングは、TeamsFx CLI Teams Toolkit、または分離されたワークフローを使用して実行できます。 プロビジョニング後にコミットし (プロビジョニングの結果はフォルダー内に保存されます)、今後の使用のために名前を付けて GitHub リポジトリ シークレットにファイルの内容を `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` 保存してください[](https://docs.github.com/en/actions/reference/encrypted-secrets) `USERDATA_CONTENT` 。

### <a name="environment-variables"></a>環境変数

次の手順で環境変数を作成GitHub。

1. [プロジェクトの設定 **] ページ設定[** 環境]**セクションに** 移動し、[新しい環境]**を選択します**。
1. 環境の名前を入力します。 テンプレートに指定されている既定の環境名はです `test_environment` 。 [続行 **する環境の** 構成] を選択します。
1. 次のページで、[シークレットの **追加** ] を選択して、以下の表に示す各アイテムにシークレットを追加します。

|名前|説明|
|---|---|
|AZURE_ACCOUNT_NAME|リソースのプロビジョニングに使用される Azure のアカウント名。|
|AZURE_ACCOUNT_PASSWORD|Azure アカウントのパスワード。|
|AZURE_SUBSCRIPTION_ID|リソースがプロビジョニングされるサブスクリプションを特定します。|
|AZURE_TENANT_ID|サブスクリプションが存在するテナントを識別します。|
|Microsoft 365_ACCOUNT_NAME|アプリMicrosoft 365発行するためのユーザー アカウントTeamsです。|
|Microsoft 365_ACCOUNT_PASSWORD|アカウントのパスワードMicrosoft 365します。|
|Microsoft 365_TENANT_ID|アプリを作成/発行するTeamsを特定します。 マルチテナント アカウントを持ち、別のテナントを使用しない限り、この値はオプションです。 テナント ID を[検索する方法の詳細Microsoft 365参照してください](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)。|
> 注: ワークフローで使用される資格情報に対して多要素認証とセキュリティの既定値が無効になっている場合は、「Configure [Microsoft 365/Azure Credentials」](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret)を参照してください。

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>CI または CD PipelinesをAzure DevOps

自動化されたパイプラインは、Azure DevOpsで設定し、スクリプトを参照できます。 開始するには、以下の手順に従います。

* [CI スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>CI パイプラインのセットアップ

1. CI[スクリプトを](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)Azure DevOpsリポジトリに追加し、スクリプト ファイル内のコメントから考え出す場合に必要なカスタマイズを行います。
1. 手順に[従って、CI 用の Azure DevOpsパイプラインを作成します](/azure/devops/pipelines/create-first-pipeline)。
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

スクリプトまたはワークフロー定義に対して行える潜在的な変更:

1. CI フローのトリガー方法を変更します。 既定では、新しいコミットがブランチにプッシュ `dev` されます。
1. ノードと npm のインストール方法を変更します。
1. npm ビルド スクリプトを使用するか、オートメーション コードでのビルド方法をカスタマイズします。
1. 成功するには、0 を返す npm テスト スクリプトを使用するか、テスト コマンドを変更します。

### <a name="set-up-cd-pipeline"></a>CD パイプラインのセットアップ

1. CD[スクリプトを](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)Azure DevOps リポジトリに追加し、スクリプト ファイル内のコメントから確認する場合に必要なカスタマイズを行います。
1. このリンクを参照Azure DevOps、CD 用のパイプラインを作成[します](/azure/devops/pipelines/create-first-pipeline)。 パイプラインの定義は、CI パイプラインの次の定義例を参照できます。
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

- task: DownloadSecureFile@1
  name: userdata
  inputs:
    secureFile: 'staging.userdata'
- task: Bash@3
  inputs:
    targetType: 'inline'
    script: |
      mkdir -p .fx/states/
      cp $(userdata.secureFilePath) .fx/states/staging.userdata
  
- task: Bash@3
  env:
    AZURE_ACCOUNT_NAME: $(AZURE_ACCOUNT_NAME)
    AZURE_ACCOUNT_PASSWORD: $(AZURE_ACCOUNT_PASSWORD)
    AZURE_SUBSCRIPTION_ID: $(AZURE_SUBSCRIPTION_ID)
    AZURE_TENANT_ID: $(AZURE_TENANT_ID)
    Microsoft 365_ACCOUNT_NAME: $(Microsoft 365_ACCOUNT_NAME)
    Microsoft 365_ACCOUNT_PASSWORD: $(Microsoft 365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

スクリプトまたはワークフロー定義に対して行える潜在的な変更:

1. CD フローのトリガー方法。 既定では、メイン ブランチに対して新しいコミットが行われたときに **発生** します。
1. ノードと npm のインストール方法を変更します。
1. 環境名を変更します。既定では、**ステージングします。**
1. npm ビルド スクリプトを使用するか、オートメーション コードでのビルド方法をカスタマイズします。
1. 成功した場合は 0 を返す npm テスト スクリプトを使用し、テスト コマンドを変更してください。

> [!Note]
> 通常は 1 回しか実行されないので、プロビジョニング 手順は CD テンプレートには含まれません。 プロビジョニングは、TeamsFx CLI Teams Toolkit、または分離されたワークフローを使用して実行できます。 プロビジョニング後にコミットし (プロビジョニングの結果はフォルダー内に保存されます)、将来の使用のためにセキュリティで保護されたAzure DevOpsに `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` アップロードしてください。 [](/azure/devops/pipelines/library/secure-files)

### <a name="environment-variables-for-azure-devops"></a>変数の環境変数Azure DevOps

次の手順に従って、パイプライン変数をAzure DevOps。

1. [パイプラインの編集] ページで、右側 **の [変数]** を選択し、[新しい変数] **を選択します**。
1. 変数の名前と値のペアを入力します。
1. 必要に応じて、[この値を **秘密にする] のチェック ボックス** をオフにします。
1. **[OK] を** 選択して変数を作成します。

|名前|説明|
|---|---|
|AZURE_ACCOUNT_NAME|リソースのプロビジョニングに使用される Azure のアカウント名。|
|AZURE_ACCOUNT_PASSWORD|Azure アカウントのパスワード。|
|AZURE_SUBSCRIPTION_ID|リソースがプロビジョニングされるサブスクリプションを特定します。|
|AZURE_TENANT_ID|サブスクリプションが存在するテナントを識別します。|
|Microsoft 365_ACCOUNT_NAME|アプリMicrosoft 365発行するためのユーザー アカウントTeamsです。|
|Microsoft 365_ACCOUNT_PASSWORD|アカウントのパスワードMicrosoft 365します。|
|Microsoft 365_TENANT_ID|アプリを作成/発行するTeamsを特定します。 マルチテナント アカウントを持ち、別のテナントを使用しない限り、この値はオプションです。 テナント ID を[検索する方法の詳細Microsoft 365参照してください](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)。|

> !メモ ワークフローで使用される資格情報の多要素認証とセキュリティの既定値を無効にした場合は、「Configure [Microsoft 365/Azure Credentials」](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret)を参照してください。

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Jenkins の CI または CD パイプライン テンプレート

これらのテンプレートをリポジトリに追加するには、バージョンの [jenkins-ci-template が必要です。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) と  [jenkins-cd-template。Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile) をブランチ別にリポジトリに保存します。

また、Jenkins で CI または CD パイプラインを作成し、それに応じて特定の **Jenkinsfile を** 指す必要があります。

手順に従って、Jenkins をさまざまな SCM プラットフォームに接続する方法を確認します。

1. [Jenkins with GitHub](https://www.jenkins.io/solutions/github/)
2. [Jenkins with Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [GitLab を使用した Jenkins](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [Jenkins with Bitbucket](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>CI パイプラインのカスタマイズ

プロジェクトを調整するために行える変更の可能性は次のとおりです。

1. テンプレート ファイルの名前を **Jenkinsfile** に変更するのは一般的な方法であり、開発ブランチなど、ターゲット ブランチの下に **置** く方法です。
1. CI フローのトリガー方法を変更します。 新しい変更が開発ブランチにプッシュされる場合、既定では **pollSCM** のトリガーを **使用** します。
1. npm ビルド スクリプトを使用するか、オートメーション コードでのビルド方法をカスタマイズします。
1. 成功した場合は 0 を返す npm テスト スクリプトを使用し、テスト コマンドを変更してください。

### <a name="customize-cd-pipeline"></a>CD パイプラインのカスタマイズ

次の手順を変更して、CD パイプラインをカスタマイズします。

1. テンプレート ファイルの名前を **Jenkinsfile** に変更するのは一般的な方法であり、メイン ブランチなど、ターゲット ブランチの下に **置** く方法です。
1. CD フローのトリガー方法。 新しい変更がメイン ブランチにプッシュされると **、pollSCM** のトリガーが既定で **使用** されます。
1. Jenkins パイプライン[資格情報を作成して](https://www.jenkins.io/doc/book/using/using-credentials/)、Azure/Microsoft 365資格情報を保持します。 次の表に、Jenkins で作成する必要があるすべての資格情報を示します。
1. 必要に応じてビルド スクリプトを変更します。
1. テストを実行しない場合は、テスト スクリプトを削除します。

> [!Note]
 通常は 1 回しか実行されないので、プロビジョニング 手順は CD テンプレートには含まれません。 プロビジョニングは、TeamsFx CLI Teams Toolkit、または分離されたワークフローを使用して実行できます。 プロビジョニング後にコミットし (プロビジョニングの結果はフォルダー内に保存されます)、今後の使用のためにファイルの内容を `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` Jenkins 資格情報に保存してください。

### <a name="environment-variables-for-jenkins"></a>Jenkins の環境変数

[Using-credentials に従って](https://www.jenkins.io/doc/book/using/using-credentials/)Jenkins に資格情報を作成します。

|名前|説明|
|---|---|
|AZURE_ACCOUNT_NAME|リソースのプロビジョニングに使用される Azure のアカウント名。|
|AZURE_ACCOUNT_PASSWORD|Azure アカウントのパスワード。|
|AZURE_SUBSCRIPTION_ID|リソースがプロビジョニングされるサブスクリプションを特定します。|
|AZURE_TENANT_ID|サブスクリプションが存在するテナントを識別します。|
|Microsoft 365_ACCOUNT_NAME|アプリを作成して発行するための M3icrosoft 365 アカウントTeamsします。|
|Microsoft 365_ACCOUNT_PASSWORD|アカウントのパスワードMicrosoft 365します。|
|Microsoft 365_TENANT_ID|アプリを作成/発行するTeamsを特定します。 マルチテナント アカウントを持ち、別のテナントを使用しない限り、この値はオプションです。 テナント ID を[検索する方法の詳細Microsoft 365参照してください](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)。|
> 注: パイプラインで使用される資格情報に対して多要素認証とセキュリティの既定値が無効になっている場合は[、「Configure Microsoft 365/Azure Credentials」](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret)を参照してください。

## <a name="get-started-guide-for-other-platforms"></a>他のプラットフォームのガイドを開始する

リストされている定義済みの bash スクリプトの例に従って、他のプラットフォームで CI または CD パイプラインをビルドおよびカスタマイズできます。

* [CI スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD スクリプト](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) スクリプトは非常に簡単で、ほとんどの部分はクロスプラットフォーム CLI なので、PowerShell などの他の種類のスクリプトに簡単に変換できます。

スクリプトは、クロスプラットフォームの TeamsFx コマンド ライン ツール [TeamsFx-CLI に基づいて作成されます](https://www.npmjs.com/package/@microsoft/teamsfx-cli)。 このスクリプトをインストールし `npm install -g @microsoft/teamsfx-cli` 、ドキュメントに [従って](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) スクリプトをカスタマイズできます。

> [!Note]
> CI モード `@microsoft/teamsfx-cli` で実行を有効にするには、次の方法でオン `CI_ENABLED` にします `export CI_ENABLED=true` 。 CI モードでは `@microsoft/teamsfx-cli` 、CI または CD に対応しています。

環境変数に Azure と M365 の資格情報を安全に設定してください。 たとえば、ソース コード リポジトリGitHub使用している場合は[、Github Secrets](https://docs.github.com/en/actions/reference/encrypted-secrets)を使用して環境変数を安全に格納できます。

### <a name="see-also"></a>関連項目

* [[クイック スタート] GitHubアクション](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [最初のパイプラインをAzure DevOpsする](/azure/devops/pipelines/create-first-pipeline)
* [最初の Jenkins パイプラインを作成する](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
