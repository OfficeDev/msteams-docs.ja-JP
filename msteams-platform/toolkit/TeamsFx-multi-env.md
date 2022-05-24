---
title: Teams Toolkitの TeamsFX 複数の環境
author: MuyangAmigo
description: TeamsFX マルチ環境について
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 684951451519ca5e1aaa82344de802259df22a63
ms.sourcegitcommit: 264d3cc84d6eec4ab025cf86a7a6f4865f1aed07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2022
ms.locfileid: "65653281"
---
# <a name="manage-multiple-environments"></a>複数の環境を管理する

 Teams Toolkitは、複数の環境を作成および管理し、Teams アプリのターゲット環境に成果物をプロビジョニングしてデプロイするための簡単な方法を提供します。

 複数の環境で次の操作を実行できます。

1. **運用環境の前にテスト** する: 最新のアプリ開発ライフサイクルでTeamsアプリを運用環境に発行する前に、開発、テスト、ステージングなどの複数の環境を設定できます。

2. **異なる環境でアプリの動作を管理** する: 運用環境でテレメトリを有効にするなど、複数の環境に対して異なる動作を設定できますが、開発環境では無効にできます

## <a name="prerequisite"></a>前提条件

* [Teams Toolkit の最新バージョン](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)をインストールします。

> [!TIP]
> Microsoft Visual Studio コードでアプリ プロジェクトTeams開かれていることを確認します。

## <a name="create-a-new-environment"></a>新しい環境を作成します。

新しいプロジェクトを作成した後、既定でTeams Toolkit次が作成されます。

* ローカル コンピューター環境の構成を表す 1 つの `local` 環境
* リモート環境またはクラウド環境の構成を表す 1 つの `dev` 環境

> [!NOTE]
> 各プロジェクトに使用できる環境は 1 つだけです `local` が、リモート環境は複数あります。

**別のリモート環境を追加するには**:

1. サイドバーで **Teams** アイコンを選択します
2. **[+Teams:** 次の図に示すように、[環境] セクションの下に新しい環境を作成するを選択します。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="作成":::

複数の環境がある場合は、同じ環境を作成するために既存の環境を選択する必要があります。 このコマンドは、選択した既存の環境のファイルの `config.<newEnv>.json` 内容を `azure.parameters.<newEnv>.json` 、作成した新しい環境にコピーします。

## <a name="select-target-environment"></a>ターゲット環境を選択する

環境関連のすべての操作に対してターゲット環境を選択できます。 次の図に示すように、複数のリモート環境がある場合、Toolkitはターゲット環境を求め、要求します。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="env を追加する":::

## <a name="project-folder-structure"></a>Project フォルダー構造

プロジェクトを作成した後、Visual Studio Code のエクスプローラー領域にプロジェクト フォルダーとファイルを表示できます。 カスタム コードに加えて、一部のファイルは、アプリの構成、状態、テンプレートを維持するためにTeams Toolkitによって使用されます。 次の一覧では、ファイルを提供し、複数の環境との関係の概要を示します。

* `.fx/configs`: ユーザーがTeams アプリ用にカスタマイズできるファイルを構成する
  * `config.<envName>.json`: 環境ごとの構成ファイル 
  * `azure.parameters.<envName>.json`: Azure bicep プロビジョニング用の環境ごとのパラメーター ファイル
  * `projectSettings.json`: すべての環境に適用されるグローバル プロジェクト設定
* `.fx/states`: Toolkitによって生成されるプロビジョニング結果
  * `state.<envName>.json`: 環境ごとのプロビジョニング出力ファイル
  * `<env>.userdata`: プロビジョニング出力の環境ごとの機密ユーザー データ
* `templates`
  * `appPackage`: アプリ マニフェスト テンプレート ファイル
  * `azure`: Bicep テンプレート ファイル

## <a name="customize-resource-provision"></a>リソースのプロビジョニングをカスタマイズする

Teams Toolkitでは、構成ファイルとテンプレート ファイルを変更して、各環境のリソースプロビジョニングをカスタマイズできます。

次の表に、カスタマイズされたリソースプロビジョニングの一般的なシナリオを示します。

| シナリオ | 場所| 説明 |
| --- | --- | --- |
| Azure リソースをカスタマイズする | <ul> <li>下の Bicep ファイル `templates/azure`</li> <li>`.fx/azure.parameters.<envName>.json`</li></ul> | [ARM パラメーターとテンプレートをカスタマイズする](provision.md#customize-arm-parameters-and-templates) |
| Teams アプリ用に既存の Azure AD アプリを再利用する | <ul> <li>`auth` のセクション`.fx/config.<envName>.json`</li> </ul> |  [Teams アプリに既存の Azure AD アプリを使用する](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| ボット用に既存の Azure AD アプリを再利用する | <ul> <li>`bot` のセクション`.fx/config.<envName>.json`</li> </ul> | [ボットに既存の Azure AD アプリを使用する](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| SQLのプロビジョニング中にユーザーの追加をスキップする | <ul> <li>`skipAddingSqlUser` 内のプロパティ`.fx/config.<envName>.json`</li> </ul> | [SQL データベースのユーザーの追加をスキップする](provision.md#skip-adding-user-for-sql-database) |
| アプリ マニフェストをカスタマイズする | <ul> <li>`templates/manifest.template.json`</li> <li>`manifest` のセクション `.fx/config.<envName>.json`</li>  </ul> | [Toolkitでアプリ マニフェストをプレビューする](TeamsFx-preview-and-customize-app-manifest.md)|

## <a name="scenarios"></a>シナリオ

異なる環境でリソースプロビジョニングをカスタマイズするには、4 つのシナリオがあります。
<br>

<br><details>
<summary><b>シナリオ 1: さまざまな環境Teamsアプリ名をカスタマイズする</b></summary>

Teamsアプリ名は`myapp(dev)`、既定の環境と`myapp(staging)`ステージング`staging`環境`dev`に設定できます。

カスタマイズするには、次の手順を実行します。

1. 構成ファイルを開く `.fx/configs/config.dev.json`
2. *appName >マニフェストのプロパティを短い>* に更新します。`myapp(dev)`

  更新プログラム `.fx/configs/config.dev.json` は次のとおりです。

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          "appName": {
              "short": "myapp(dev)"
              ...
          }
      }
      ...
  }
  ```

3. 新しい環境を作成し、存在しない場合は名前を付 `staging` けます
4. 構成ファイルを開く `.fx/configs/config.staging.json`
5. 同じプロパティを更新する `myapp(staging)`
6. プロビジョニング コマンドと`staging`環境を`dev`実行して、リモート環境でアプリ名を更新します。 Teams Toolkitを使用してプロビジョニング コマンドを実行するには、「プロビジョニング」を参照してください[。](provision.md#provision-using-teams-toolkit)
</details>
<br>


<details>
<summary><b>シナリオ 2: さまざまな環境Teamsアプリの説明をカスタマイズする</b></summary>

このシナリオでは、さまざまな環境に対して異なるTeamsアプリの説明を設定する方法について説明します。

* 既定の環境 `dev`の場合、説明は次のように指定します。 `my app description for dev`
* ステージング環境 `staging`の場合、説明は次の内容になります。 `my app description for staging`

カスタマイズするには、次の手順を実行します。

1. 構成ファイルを開く `.fx/configs/config.dev.json`
2. マニフェスト>説明の新しいプロパティ *を追加>値を指定して短く* する `my app description for dev`

  更新プログラム `.fx/configs/config.dev.json` は次のとおりです。

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          ...
          "description": {
              "short": "`my app description for dev"
              ...
          }
      }
      ...
  }
  ```

3. 新しい環境を作成し、存在しない場合は名前を付 `staging` けます
4. 構成ファイルを開く `.fx/configs/config.staging.json`
5. 同じプロパティを追加する `my app description for staging`
6. アプリ マニフェスト テンプレートTeams開く`templates/appPackage/manifest.template.json`
7. mustache 構文を使用してファイルを構成するで定義されている **変数** を使用するようにプロパティ`description > short`を更新する`{{config.manifest.description.short}}`
  
  更新プログラム `manifest.template.json` は次のとおりです。

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "{{config.manifest.description.short}}", 
      ...
    },
    ...
  }
  ```

8. 環境に対して `dev` プロビジョニング コマンドを `staging` 実行して、リモート環境でアプリ名を更新します。 Teams Toolkitを使用してプロビジョニング コマンドを実行するには、「プロビジョニング」を参照してください[。](provision.md#provision-using-teams-toolkit)

</details>
<br>

<details>
<summary><b>シナリオ 3: すべての環境Teamsアプリの説明をカスタマイズする</b></summary>

このシナリオでは、Teams アプリの説明をすべての環境に対して設定する`my app description`方法について説明します。

Teams アプリ マニフェスト テンプレートはすべての環境で共有されるため、ターゲットの説明の値を更新できます。

1. アプリ マニフェスト テンプレートTeams開く`templates/appPackage/manifest.template.json`
2. **ハードコーディングされた文字列** を使用してプロパティ`description > short`を更新する `my app description`
  
  更新プログラム `manifest.template.json` は次のとおりです。

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "my app description",
      ...
    },
    ...
  }
 ```
3. **すべての** 環境に対してプロビジョニング コマンドを実行して、リモート環境でアプリ名を更新します。 Teams Toolkitを使用してプロビジョニング コマンドを実行するには、「プロビジョニング」を参照してください[。](provision.md#provision-using-teams-toolkit)
<br></details>
<br>
<details>
<br><summary><b>シナリオ 4: さまざまな環境用に Azure リソースをカスタマイズする</b></summary>
fx/configs/azure.parameters に対応する環境を編集することで、Azure 関数名を指定するなど、環境ごとに Azure リソースをカスタマイズできます。{env}.json. ファイル。

Bicep テンプレートとパラメーター ファイルの詳細については、「 [クラウド リソース](provision.md)
</details> を br <プロビジョニングする」を参照してください。



## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [クラウド リソースをさらに追加する](add-resource.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)