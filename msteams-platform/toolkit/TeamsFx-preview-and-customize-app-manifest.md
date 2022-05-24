---
title: Teams Toolkitでアプリ マニフェストをTeamsする
author: zyxiaoyuer
description: Teams アプリ マニフェスト
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: ebb6f7e66f09c3ebbc3834577f924f5a34bb8583
ms.sourcegitcommit: 264d3cc84d6eec4ab025cf86a7a6f4865f1aed07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2022
ms.locfileid: "65653882"
---
# <a name="edit-teams-app-manifest"></a>アプリ マニフェストTeams編集する

マニフェスト テンプレート ファイル `manifest.template.json` は、スキャフォールディング後にフォルダーの下で `templates/appPackage` 使用できます。 プレースホルダーを含むテンプレート ファイルと実際の値は、さまざまな環境のファイル`.fx/configs``.fx/states`を使用してTeams Toolkitによって解決されます。

**実際のコンテンツを使用してマニフェストをプレビューするには、Teams Toolkitフォルダーの下に`build/appPackage`プレビュー マニフェスト ファイルを生成します**。

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote Teams app
        ├───appPackage.local.zip - Zipped app package of local Teams app
        ├───manifest.{env}.json  - Previewed manifest of remote Teams app
        └───manifest.local.json  - Previewed manifest of local Teams app
```

ローカル環境とリモート環境でマニフェスト ファイルをプレビューできます。

* [ローカル環境でマニフェスト ファイルをプレビューする](#preview-manifest-file-in-local-environment)
* [リモート環境でマニフェスト ファイルをプレビューする](#preview-manifest-file-in-remote-environment)
 
### <a name="preview-manifest-file-in-local-environment"></a>ローカル環境でマニフェスト ファイルをプレビューする

ローカル環境でマニフェスト ファイルをプレビューするには、 **F5** キーを押してローカル デバッグを実行します。 既定のローカル設定が生成され、アプリ パッケージとプレビュー マニフェストがフォルダーの下に `build/appPackage` ビルドされます。

次の手順に従って、ローカル マニフェスト ファイルをプレビューすることもできます。

1. ファイルの`manifest.template.json`コードレンズで **[プレビュー**] を選択し、**ローカル** を選択します。
2. ファイルのメニュー バー`manifest.template.json`で [**プレビュー マニフェスト ファイル**] を選択します。
3. Treeview **で Zip Teamsメタデータ パッケージ** を選択し、**ローカル** を選択します。

プレビュー ローカルは、イメージに示すように表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="プレビュー":::

### <a name="preview-manifest-file-in-remote-environment"></a>リモート環境でマニフェスト ファイルをプレビューする

**リモート環境でマニフェスト ファイルをプレビューするには**

* [**development** in Teams Toolkit extension] で [**クラウドでプロビジョニング**] を選択するか、 
* トリガー Teams: コマンド パレットから **クラウドにプロビジョニング** します。
 
リモート Teams アプリの構成を生成し、パッケージとプレビュー マニフェストをフォルダーの下に`build/appPackage`ビルドします。

次の手順で、リモート環境でマニフェスト ファイルをプレビューすることもできます。

1. ファイルの`manifest.template.json`コードレンズで **[プレビュー**] を選択します。
2. ファイルのメニュー バー`manifest.template.json`で [**プレビュー マニフェスト ファイル**] を選択します。
3. Treeview **で Zip Teamsメタデータ パッケージ** を選択します。
4. 環境を選択します。

> [!NOTE]
> 複数の環境がある場合は、イメージに示すようにプレビューする環境を選択する必要があります。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="env を追加する":::

## <a name="sync-local-changes-to-dev-portal"></a>ローカルの変更を Dev Portal に同期する

マニフェスト ファイルをプレビューしたら、次の方法でローカルの変更を Dev Portal に同期できます。

1. アプリ マニフェストTeamsデプロイする

   Teamsアプリ マニフェストは、次のいずれかの方法でデプロイできます。

   * ファイルに `manifest.template.json` 移動し、右クリックしてコンテキスト メニューから選択 `Deploy Teams app manifest` します

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="マニフェストをデプロイする":::

   * コマンド パレットからトリガーする`Teams: Deploy Teams app manifest`

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="コマンド パレットから配置する":::

2. Teams プラットフォームに更新する

   次のいずれかの方法で、Teams プラットフォームに更新できます。

   * の左上隅にある **プラットフォームTeams更新を** 選択します。`manifest.{env}.json`

   * **トリガー Teams: マニフェストをTeamsプラットフォーム** のメニュー バーに更新します。`manifest.{env}.json`

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="チームの更新":::

Teamsをトリガーすることもできます。コマンド パレットから **マニフェストをTeamsプラットフォームに更新** します。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="ツリー ビュー":::

> [!NOTE]
> エディターのコードレンズまたはメニュー バーからトリガーすると、現在のマニフェスト ファイルがTeams プラットフォームに更新されます。 コマンド パレットからトリガーするには、ターゲット環境を選択する必要があります。

 CLI コマンド:

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> Dev Portal に対する変更が更新されます。 Dev Portal の手動更新は上書きされます。

構成ファイルの変更またはテンプレートの変更によりマニフェスト ファイルが古い場合は、次のいずれかのアクションを選択します。

* **プレビューのみ**: ローカル マニフェスト ファイルは、現在の構成に従って上書きされます
* **プレビューと更新**: ローカル マニフェスト ファイルは現在の構成に従って上書きされ、プラットフォームTeams更新されます
* **キャンセル**: アクションは実行されません

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre" border="true":::


## <a name="customize-teams-app-manifest"></a>Teams アプリ マニフェストをカスタマイズする

Teams Toolkit は、ローカル環境とリモート環境の `manifest.template.json` フォルダーにある次のマニフェスト テンプレート ファイルで構成されています。

* `manifest.template.json`
* `templates/appPackage`


ローカル デバッグまたはプロビジョニング中に、Teams Toolkitから 、構成を`state.{env}.json`使用してマニフェスト`manifest.template.json`を読み込み、`config.{env}.json`[Dev Portal](https://dev.teams.microsoft.com/apps) でTeamsアプリを作成します。

## <a name="supported-placeholders-in-manifesttemplatejson"></a>manifest.template.json でサポートされているプレースホルダー

次の一覧では、サポートされているプレースホルダーを次に `manifest.template.json`示します。

* `{{state.xx}}` は定義済みのプレースホルダーであり、その値は Teams Toolkit によって解決されます。これは、`state.{env}.json` で定義されています。 内の値を変更しないようにしてください。 `state.{env}.json`
* `{{config.manifest.xx}}` はカスタマイズされたプレースホルダーであり、値は `config.{env}.json`

**カスタマイズされたパラメーターを追加するには**

1. 次のようにカスタマイズされたパラメーターを追加します。</br>
   a.  パターン`{{config.manifest.xx}}`を含むプレースホルダー`manifest.template.json`を追加します。</br>
   b. に構成値 `config.{env}.json`を追加します。

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. 構成ファイルに移動するには、いずれかの構成プレースホルダー [構成ファイル **に移動**] または [**状態ファイル**`manifest.template.json`の表示] を選択します。

### <a name="validate-manifest"></a>マニフェストを検証する

**Zip Teamsメタデータ パッケージ** などの操作中に、Teams Toolkitはそのスキーマに対してマニフェストを検証します。 次の一覧では、マニフェストを検証するさまざまな方法を示します。

* VSC では、コマンド パレットからトリガー `Teams: Validate manifest file` します。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="ファイルを検証する":::

* CLI で、次のコマンドを使用します。

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## Codelenses and hovers

In `manifest.template.json`, you can navigate to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Preview values":::

> [!NOTE] 
> Provision the environment or execute local debug to generate values for placeholders. 

You can navigate to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Select your environment":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Preview all values":::


## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md) 
