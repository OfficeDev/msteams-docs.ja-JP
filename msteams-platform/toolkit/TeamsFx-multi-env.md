---
title: TeamsFX の複数のTeams Toolkit
author: MuyangAmigo
description: TeamsFX マルチ環境について
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 1c0bb7eb75ee982e7c08d3039e59f03fc7f18146
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768465"
---
# <a name="manage-multiple-environments-in-teams-toolkit"></a>複数の環境を管理Teams Toolkit

 Teams Toolkitは、複数の環境を作成および管理し、アイテムを準備し、アプリのターゲット環境に展開するための簡単なTeamsです。

 複数の環境を使用すると、次の操作を実行できます。

1. **運用前のテスト**: 開発、テスト、ステージングなどの複数の環境をセットアップしてから、Teams App を最新のアプリ開発ライフサイクルで運用環境に公開する一般的な方法です。

2. **さまざまな環境でアプリの** 動作を管理する : 複数の環境に対して異なる動作を設定できます 。たとえば、実稼働環境でテレメトリを有効にし、開発環境では無効にできます。

## <a name="prerequisite"></a>前提条件

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> VS コードでTeamsアプリ プロジェクトが開いているか確認します。

## <a name="create-a-new-environment"></a>新しい環境を作成する

新しいプロジェクトを作成した後、既定Teams Toolkit作成されます。

- ローカル `local` コンピューター環境構成を表す 1 つの環境。
- リモート `dev` 環境またはクラウド環境構成を表す 1 つの環境。

> [!NOTE]
> 各プロジェクトには、1 つの環境しか `local` 使用できませんが、複数のリモート環境を使用できます。

別のリモート環境を追加するには、サイドバー Teamsアイコンを選択し、次の図に示すように、[環境] セクションで [新しい環境の作成] を選択します。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="作成":::

> [!NOTE]
> 複数の既存の環境がある場合は、既存の環境を選択して同じ環境を作成する必要があります。 このコマンドは、選択した既存の環境のファイルの内容とファイルの内容を、作成中の `config.<newEnv>.json` `azure.parameters.<newEnv>.json` 新しい環境にコピーします。

## <a name="select-target-environment"></a>ターゲット環境の選択 

すべての環境関連操作のターゲット環境を選択できます。 次の図に示すように、複数のリモート環境がある場合、ツールキットはターゲット環境のプロンプトを表示して要求します。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="env を追加する":::

## <a name="project-folder-structure"></a>Projectフォルダー構造 

プロジェクトを作成した後、プロジェクト フォルダーとファイルをプロジェクト のエクスプローラー領域に表示Visual Studio Code。 カスタム コードの他に、アプリの構成、状態Teams Toolkitテンプレートを維持するために、一部のファイルが使用されます。 次の一覧は、ファイルを提供し、複数の環境との関係の概要を示します。

- `.fx/configs`: ユーザーがアプリ用にカスタマイズできるファイルをTeamsします。
  - `config.<envName>.json`: 環境ごとの構成ファイル。
  - `azure.parameters.<envName>.json`: Azure bicep プロビジョニング用の環境ごとのパラメーター ファイル。
  - `projectSettings.json`: すべての環境に適用されるグローバル プロジェクト設定。
  - `localSettings.json`: ローカル デバッグ構成ファイル。
- `.fx/states`: ユーザーが生成するプロビジョニング結果Toolkit。
  - `state.<envName>.json`: 環境ごとのプロビジョニング出力ファイル。
  - `<env>.userdata`: プロビジョニング出力の環境ごとの機密ユーザー データ。
- `templates`
  - `appPackage`: アプリ マニフェスト テンプレート ファイル。
  - `azure`: Bicep テンプレート ファイル。

## <a name="customize-the-provision"></a>プロビジョニングをカスタマイズする 

Teams Toolkit構成ファイルとテンプレート ファイルを変更して、各環境でリソースの準備をカスタマイズできます。

次の表に、カスタマイズされたプロビジョニングでサポートされる一般的なシナリオとカスタマイズする場所を示します。

| シナリオ | Location| Description |
| --- | --- | --- |
| Azure リソースのカスタマイズ | <ul> <li>下のバイセップ ファイル `templates/azure` 。</li> <li>`.fx/azure.parameters.<envName>.json`.</li></ul> | [パラメーター ARMテンプレートをカスタマイズします](provision.md#customize-arm-parameters-and-templates)。 |
| 既存のアプリをAADアプリにTeamsする | <ul> <li>`auth`セクション `.fx/config.<envName>.json`</li> </ul> |  [既存のアプリをAADアプリにTeamsします](provision.md#use-an-existing-aad-app-for-your-teams-app)。 |
| ボットに既存のAADアプリを再利用する | <ul> <li>`bot`セクション `.fx/config.<envName>.json`</li> </ul> | [ボットに既存のAADアプリを使用します](provision.md#use-an-existing-aad-app-for-your-bot)。 |
| プロビジョニング中にユーザーの追加をスキップSQL | <ul> <li>`skipAddingSqlUser`のプロパティ `.fx/config.<envName>.json`</li> </ul> | [データベースのユーザーの追加SQLスキップします](provision.md#skip-adding-user-for-sql-database)。 |
| アプリ マニフェストのカスタマイズ | <ul> <li>`templates/manifest.remote.template.json`.</li> <li>`manifest`セクション `.fx/config.<envName>.json`</li>  </ul> | [[Teamsアプリ マニフェストをカスタマイズTeams Toolkit。](TeamsFx-manifest-customization.md) |

## <a name="scenarios"></a>シナリオ

### <a name="scenario-1-customize-teams-app-name-for-different-environment"></a>シナリオ 1: さまざまな環境Teamsアプリ名をカスタマイズする

既定の環境Teamsステージング環境 `myapp(dev)` のアプリ名を `dev` `myapp(staging)` 設定できます `staging` 。

カスタマイズのために次の手順を実行します。

- 1. 構成ファイルを開きます `.fx/configs/config.dev.json` 。
- 2. 短い *appName の>を>する*`myapp(dev)`

  更新プログラムは `.fx/configs/config.dev.json` 次のとおりです。

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

- 3. 新しい環境を作成し、存在しない `staging` 場合は名前を付けします。
- 4. 構成ファイルを開きます `.fx/configs/config.staging.json` 。
- 5. 同じプロパティを更新します `myapp(staging)` 。
- 6. リモート環境でアプリ名を更新するには、プロビジョニング コマンドを on と environment `dev` `staging` で実行します。 このコマンドを使用してプロビジョニング コマンドをTeams Toolkit、provision を[参照してください](provision.md#provision-using-teams-toolkit)。

### <a name="scenario-2-customize-teams-app-description-for-different-environment"></a>シナリオ 2: さまざまな環境Teamsアプリの説明をカスタマイズする

このシナリオでは、さまざまな環境に対して異なるアプリTeamsを設定する方法について説明します。

- 既定の環境の `dev` 場合、説明は次になります `my app description for dev` 。
- ステージング環境の `staging` 場合、説明は次になります `my app description for staging` 。

カスタマイズのために次の手順を実行します。

- 1. 構成ファイルを開きます `.fx/configs/config.dev.json` 。
- 2. マニフェストと説明の新 *しいプロパティ>値>短く* 追加します `my app description for dev` 。

  更新プログラムは `.fx/configs/config.dev.json` 次のとおりです。

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

- 3. 新しい環境を作成し、存在しない `staging` 場合は名前を付けします。
- 4. 構成ファイルを開きます `.fx/configs/config.staging.json` 。
- 5. に同じプロパティを追加します `my app description for staging` 。
- 6. リモートTeamsアプリ マニフェスト テンプレートを開きます `templates/appPackage/manifest.remote.template.json` 。
- 7. 口ひげ `description > short` 構文を使用してファイル **を構成するで** 定義されている変数を使用するプロパティを更新します `{{config.manifest.description.short}}` 。
  
  更新プログラムは `manifest.remote.template.json` 次のとおりです。

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
- 8. プロビジョニング コマンドと環境 `dev` を `staging` 実行して、リモート環境でアプリ名を更新します。 このコマンドを使用してプロビジョニング コマンドをTeams Toolkit、provision を[参照してください](provision.md#provision-using-teams-toolkit)。

### <a name="scenario-3-customize-teams-app-description-for-all-environments"></a>シナリオ 3: すべてのTeamsアプリの説明をカスタマイズする

このシナリオでは、アプリの説明をすべての環境にTeamsする `my app description` 方法について説明します。

アプリ マニフェスト Teamsテンプレートがすべての環境で共有されている場合、ターゲットの説明の値を更新できます。

- 1. リモートTeamsアプリ マニフェスト テンプレートを開きます `templates/appPackage/manifest.remote.template.json` 。
- 2. ハードコードされた `description > short` 文字列 **でプロパティを更新します** `my app description` 。
  
  更新プログラムは `manifest.remote.template.json` 次のとおりです。

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

- 3. Run provision command against **all** environment to update the app name in remote environments. To run provision command with Teams Toolkit, see [provision](provision.md#provision-using-teams-toolkit).

### Scenario 4: customize Azure resources for different environment

You can customize Azure resources for each environment, for example specify Azure Function name, by editing the environment corresponding to `.fx/configs/azure.parameters.{env}.json` file.

For more information on Bicep template and parameter files, see [provision cloud resources](provision.md)

## See also

* [Provision cloud resources](provision.md)
* [Add more cloud resources](add-resource.md)
* [Collaborate with other developers on Teams project](TeamsFx-collaboration.md)
