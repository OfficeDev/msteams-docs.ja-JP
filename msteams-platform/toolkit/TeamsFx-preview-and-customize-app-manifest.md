---
title: Teams Toolkit で Teams アプリ マニフェストをカスタマイズする
author: zyxiaoyuer
description: このモジュールでは、さまざまな環境で Teams アプリ マニフェストを編集、プレビュー、カスタマイズする方法について説明します。
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 02bbcc86c769f8ebff87803b6a12bf882e214bf6
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780710"
---
# <a name="customize-teams-app-manifest"></a>Teams アプリ マニフェストをカスタマイズする

Teams アプリ マニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。

::: zone pivot="visual-studio-code"

## <a name="customize-teams-app-manifest-for-visual-studio-code"></a>Visual Studio Code の Teams アプリ マニフェストをカスタマイズする

Teams アプリ マニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。 マニフェストの詳細については、「 [Teams のアプリ マニフェスト スキーマ」を参照してください](../resources/schema/manifest-schema.md)。 このセクションでは、次の手順について説明します。

* [ローカル環境でマニフェスト ファイルをプレビューする](#preview-manifest-file-in-local-environment)
* [リモート環境でマニフェスト ファイルをプレビューする](#preview-manifest-file-in-remote-environment)
* [ローカルの変更を開発者ポータルに同期する](#sync-local-changes-to-developer-portal)
* [Teams アプリ マニフェストをカスタマイズする](#customize-your-teams-app-manifest)
* [マニフェストを検証する](#validate-manifest)

マニフェスト テンプレート ファイル `manifest.template.json` は、スキャフォールディング後にフォルダーの下で `templates/appPackage` 使用できます。 プレースホルダーを含むテンプレート ファイルと実際の値は、さまざまな環境のファイル`.fx/configs``.fx/states`を使用して Teams Toolkit によって解決されます。

実際のコンテンツを使用してマニフェストをプレビューするために、Teams Toolkit はフォルダーの下にプレビュー マニフェスト ファイルを `build/appPackage` 生成します。

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

## <a name="preview-manifest-file-in-local-environment"></a>ローカル環境でマニフェスト ファイルをプレビューする

ローカル環境でマニフェスト ファイルをプレビューするには、 **F5** キーを押してローカル デバッグを実行します。 既定のローカル設定が生成され、アプリ パッケージとプレビュー マニフェストがフォルダーの下に `build/appPackage` ビルドされます。

2 つの方法でローカル マニフェスト ファイルをプレビューすることもできます

* codelens でプレビュー オプションを使用する
* **Zip Teams メタデータ パッケージ オプションを** 使用する

次の手順は、codelens でプレビュー オプションを使用してローカル マニフェスト ファイルをプレビューするのに役立ちます。

1. ファイルの`manifest.template.json`コードレンズで **[プレビュー**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="プレビュー":::

1. ローカルを選択 **します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="環境の選択1":::

次の手順は、 **Zip Teams メタデータ パッケージ** オプションを使用してローカル マニフェスト ファイルをプレビューするのに役立ちます。

1. ファイルを選択 `manifest.template.json` します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="[マニフェスト] を選択します":::

1. Visual Studio Code ツール バーで Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: アイコンを選択します。

1. [展開] **で [Zip Teams メタデータ パッケージ****] を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Teams メタデータ パッケージを選択する":::

1. ローカルを選択 **します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="環境を選択する":::

プレビュー ローカルは、イメージに示すように表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="プレビュー":::

## <a name="preview-manifest-file-in-remote-environment"></a>リモート環境でマニフェスト ファイルをプレビューする

Visual Studio Code を使用してマニフェスト ファイルをプレビューするには:

* Teams Toolkit 拡張機能の **[開発**] で [**クラウドでのプロビジョニング**] を選択します
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="クラウド リソースをプロビジョニングする":::

コマンド パレットを使用してマニフェスト ファイルをプレビューするには:

* トリガー Teams: コマンド パレットから **クラウドにプロビジョニング** します。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="コマンド パレットを使用してクラウド リソースをプロビジョニングする":::

リモート Teams アプリの構成を生成し、パッケージとプレビュー マニフェストをフォルダーの下に `build/appPackage` ビルドします。

リモート環境で 2 つの方法でマニフェスト ファイルをプレビューすることもできます

* codelens でプレビュー オプションを使用する
* **Zip Teams メタデータ パッケージ オプションを** 使用する

次の手順は、codelens でプレビュー オプションを使用してマニフェスト ファイルをプレビューするのに役立ちます。

1. ファイルの`manifest.template.json`コードレンズで **[プレビュー**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="プレビュー":::

1. 環境を選択します。

   > [!NOTE]
   > 複数の環境がある場合は、イメージに示すようにプレビューする環境を選択する必要があります。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="env を追加する":::

次の手順は、リモート環境で **Zip Teams メタデータ パッケージ** オプションを使用してマニフェスト ファイルをプレビューするのに役立ちます。

1. ファイルを選択 `manifest.template.json` します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="[マニフェスト] を選択します":::

1. Visual Studio Code ツール バーで Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: アイコンを選択します。

1. [展開] **で [Zip Teams メタデータ パッケージ****] を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Teams メタデータ パッケージを選択する":::

1. 環境を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="env を追加する":::

   > [!NOTE]
   > 複数の環境がある場合は、イメージに示すようにプレビューする環境を選択する必要があります。

## <a name="sync-local-changes-to-developer-portal"></a>ローカルの変更を開発者ポータルに同期する

マニフェスト ファイルをプレビューしたら、次の方法でローカルの変更を開発者ポータルに同期できます。

> [!NOTE]
> 開発者ポータルの詳細については、「 [Teams 用開発者ポータル](../concepts/build-and-test/teams-developer-portal.md)」を参照してください。

1. Teams アプリ マニフェストを展開します。

   Teams アプリ マニフェストは、次のいずれかの方法で展開できます。

   * ファイルに `manifest.template.json` 移動し、右クリックしてコンテキスト メニューから選択 `Deploy Teams app manifest` します。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="マニフェストをデプロイする":::

   * コマンド パレットからトリガー `Teams: Deploy Teams app manifest` します。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="コマンド パレットから配置する":::

2. Teams プラットフォームに更新します。

   Teams プラットフォームは、次のいずれかの方法で更新できます。

   * の左上隅にある `manifest.{env}.json`**[Teams プラットフォームに更新]** を選択します。

   * **トリガー Teams: の** メニュー バー`manifest.{env}.json`にある Teams プラットフォームにマニフェストを更新します。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="チームの更新":::

Teams: コマンド パレットから **Teams プラットフォームにマニフェストを更新** することもできます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="ツリー ビュー":::

> [!NOTE]
> エディター のコードレンズまたはメニュー バーからトリガーすると、現在のマニフェスト ファイルが Teams プラットフォームに更新されます。 コマンド パレットからトリガーするには、ターゲット環境を選択する必要があります。

 CLI コマンド:

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> Dev Portal に対する変更が更新されます。 Dev Portal の手動更新は上書きされます。

構成ファイルの変更またはテンプレートの変更によりマニフェスト ファイルが古い場合は、次のいずれかのアクションを選択します。

* **プレビューのみ**: ローカル マニフェスト ファイルは、現在の構成に従って上書きされます。
* **プレビューと更新**: ローカル マニフェスト ファイルは、現在の構成に従って上書きされ、Teams プラットフォームにも更新されます。
* **キャンセル**: アクションは実行されません。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::

## <a name="customize-your-teams-app-manifest"></a>Teams アプリ マニフェストをカスタマイズする

Teams Toolkit は、ローカル環境とリモート環境の `manifest.template.json` フォルダーにある次のマニフェスト テンプレート ファイルで構成されています。

* `manifest.template.json`
* `templates/appPackage`

ローカルデバッグまたはプロビジョニング中に、Teams Toolkit は、Dev Portal の `manifest.template.json`構成を使用してマニフェストを `state.{env}.json`読み込み、 `config.{env}.json`Teams アプリを [作成します](https://dev.teams.microsoft.com/apps)。

### <a name="supported-placeholders-in-manifesttemplatejson"></a>manifest.template.json でサポートされているプレースホルダー

次の一覧では、サポートされているプレースホルダーを次に `manifest.template.json`示します。

* `{{state.xx}}` は定義済みのプレースホルダーであり、その値は Teams Toolkit によって解決されます。これは、`state.{env}.json` で定義されています。 内の値を変更しないようにしてください。 `state.{env}.json`
* `{{config.manifest.xx}}` はカスタマイズされたプレースホルダーであり、値は `config.{env}.json`

**カスタマイズされたパラメーターを追加するには**

1. 次のようにカスタマイズされたパラメーターを追加します。</br>
   a. パターン`{{config.manifest.xx}}`を含むプレースホルダー`manifest.template.json`を追加します。</br>
   b. に構成値 `config.{env}.json`を追加します。

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. 構成ファイルに移動するには、構成プレースホルダーのいずれかを選択して構成 **ファイルに移動** するか、**状態ファイル**`manifest.template.json`を表示します。

### <a name="validate-manifest"></a>マニフェストを検証する

**Zip Teams メタデータ パッケージ** などの操作中に、Teams Toolkit はマニフェストをスキーマと照合して検証します。 次の一覧では、マニフェストを検証するさまざまな方法を示します。

* VSC では、コマンド パレットからトリガー `Teams: Validate manifest file` します。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="ファイルを検証する":::

* CLI で、次のコマンドを使用します。

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can navigate to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Preview values":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can navigate to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Select your environment":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Preview all values":::

::: zone-end

::: zone pivot="visual-studio"

## Edit Teams app manifest using Visual Studio

Teams Toolkit in Visual Studio loads manifest from `manifest.template.json` with configurations from `state.{env}.json` and `config.{env}.json` while provisioning and preparing app dependencies. You can also create Microsoft Teams app in [Developer Portal](https://dev.teams.microsoft.com/apps) with the manifest.

After scaffolding, in the manifest template file under `templates/appPackage` folder,
`manifest.template.json` is shared between local and remote environment.

In the manifest template, select **Project** > **Teams Toolkit** > **Open Manifest File**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Open manifest file" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png":::

### Customize app manifest in Teams Toolkit

There are two types of placeholders in `manifest.template.json`:

* `{{state.xx}}` is pre-defined placeholder, whose value is resolved by Teams Toolkit, defined in `state.{env}.json`. It's recommended to not modify the values in `state.{env}.json`.
* `{{config.manifest.xx}}` is customized placeholder, whose value is resolved from `config.{env}.json`.

You can add a customized parameter by:

* Adding a placeholder in `manifest.template.json` with pattern: `{{config.manifest.xx}}`.
* Adding a config value in `config.{env}.json`.

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### Preview app manifest in Teams Toolkit

You can preview values in app manifest in two ways:

* When you hover over the placeholder in `manifest.template.json`, then you can see the values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Hover over placeholder" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png":::

* You can also hover over the key besides each placeholder in `manifest.template.json`, and you can see the same values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Hover over key beside placeholder" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png":::

   > [!NOTE]
   > If the environment has not been provisioned, or the Teams app dependencies have not been prepared, it indicates that the values for placeholder have not been generated. Please follow the guidance inside hover to generate corresponding values.

### Preview manifest file

To preview the manifest file, you can sideload for local or deploy for Azure. You can preview the manifest file by performing the following step:

* Select **Project** > **Teams Toolkit** and trigger **Prepare Teams App Dependencies** or **Provision in the Cloud** that generates configuration for local or remote Teams app.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Preview manifest file" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png":::

There are two other ways to upload zip app package before you can preview manifest file:

1. From the list of menu select **Project** > **Teams Toolkit** > **Zip App Package**, and select **For Local** or **For Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Zip app package" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png":::

1. You can also upload zip app package from Solution Explorer, if you right-click on **MyTeamsApp1** and then select **Teams Toolkit** > **Zip App Package** > **For Local** or **For Azure**.

  > [!NOTE]
  > In this scenario the project name is **MyTeamsApp1**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="List of Teams Toolkit menus from solution explorer" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png":::

Teams Toolkit generates the zip app package, and to preview manifest file content you can follow the step below:

* Right-click on **manifest.template.json** under **appPackage** folder, select **Preview Manifest File** > **For Local** or **For Azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Preview context menu" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png":::

This displays the preview of the manifest file in Visual Studio.

### Sync local changes to Developer Portal

After you've previewed the manifest file in Visual Studio, you can now sync the local changes to the Developer Portal. Select **Project** > **Teams Toolkit** > **Update Manifest in Teams Developer Portal**, or context menu from Solution Explorer. You can now preview the manifest file in Developer Portal as a result of syncing the local changes.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Update manifest in teams developer portal" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png":::

> [!NOTE]
> The changes are updated to Teams Developer Portal. If you have some manual updates in Developer Portal, that can be overwritten. In the **Warning** dialog box you can select **Overwrite and update** or **Cancel**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Update warning" lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png":::

::: zone-end

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)

* [Provision cloud resources using Visual Studio](provision-cloud-resources.md)

* [Deploy Teams app to the cloud using Visual Studio](deploy-teams-app.md)
