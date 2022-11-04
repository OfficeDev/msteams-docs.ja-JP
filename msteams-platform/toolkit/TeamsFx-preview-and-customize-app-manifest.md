---
title: Teams Toolkit で Teams アプリ マニフェストをカスタマイズする
author: zyxiaoyuer
description: このモジュールでは、さまざまな環境で Teams アプリ マニフェストを編集、プレビュー、カスタマイズする方法について説明します。
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: e92e30cf30dd06dbbe3c513a79fe4b7ed7c4bc1a
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833101"
---
# <a name="customize-teams-app-manifest"></a>Teams アプリ マニフェストをカスタマイズする

Teams アプリ マニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。

::: zone pivot="visual-studio-code"

## <a name="customize-teams-app-manifest-for-visual-studio-code"></a>Visual Studio Code 用の Teams アプリ マニフェストをカスタマイズする

Teams アプリ マニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。 マニフェストの詳細については、「 [Teams のアプリ マニフェスト スキーマ](../resources/schema/manifest-schema.md)」を参照してください。 このセクションでは、次の手順について説明します。

* [ローカル環境でのマニフェスト ファイルのプレビュー](#preview-manifest-file-in-local-environment)
* [リモート環境でのマニフェスト ファイルのプレビュー](#preview-manifest-file-in-remote-environment)
* [ローカルの変更を開発者ポータルに同期する](#sync-local-changes-to-developer-portal)
* [Teams アプリ マニフェストをカスタマイズする](#customize-your-teams-app-manifest)
* [マニフェストを検証する](#validate-manifest)

マニフェスト テンプレート ファイル `manifest.template.json` は、スキャフォールディング後のフォルダーで `templates/appPackage` 使用できます。 プレースホルダーを含むテンプレート ファイルと実際の値は、Teams Toolkit によって、環境 `.fx/configs` や `.fx/states` 環境ごとにファイルを使用して解決されます。

実際のコンテンツでマニフェストをプレビューするには、Teams Toolkit によってフォルダーの下に `build/appPackage` プレビュー マニフェスト ファイルが生成されます。

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote Teams app
        ├───appPackage.local.zip - Zipped app package of local Teams app
        ├───manifest.{env}.json  - Previewed manifest of remote Teams app
        └───manifest.local.json  - Previewed manifest of local Teams app
```

マニフェスト ファイルは、ローカル環境とリモート環境でプレビューできます。

* [ローカル環境でのマニフェスト ファイルのプレビュー](#preview-manifest-file-in-local-environment)
* [リモート環境でのマニフェスト ファイルのプレビュー](#preview-manifest-file-in-remote-environment)

## <a name="preview-manifest-file-in-local-environment"></a>ローカル環境でのマニフェスト ファイルのプレビュー

ローカル環境でマニフェスト ファイルをプレビューするには、 **F5** キーを押してローカル デバッグを実行します。 既定のローカル設定が生成され、アプリ パッケージとプレビュー マニフェストがフォルダーの下に `build/appPackage` ビルドされます。

2 つの方法でローカル マニフェスト ファイルをプレビューすることもできます

* codelens でプレビュー オプションを使用する
* **Zip Teams メタデータ パッケージ** オプションを使用する

次の手順は、codelens で preview オプションを使用してローカル マニフェスト ファイルをプレビューするのに役立ちます。

1. ファイルの codelens `manifest.template.json` で [**プレビュー**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="スクリーンショットは、マニフェスト ファイルの codelens のプレビューを示す例です。":::

1. [ **ローカル]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="スクリーンショットは、環境内のローカルの選択を示す例です。":::

次の手順は、 **Zip Teams メタデータ パッケージ** オプションを使用してローカル マニフェスト ファイルをプレビューするのに役立ちます。

1. ファイルを選択 `manifest.template.json` します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="manifest.template.json の選択を示す例を示すスクリーンショット。":::

1. Visual Studio Code ツール バーの [Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: ] アイコンを選択します。

1. [デプロイ] **で [Zip Teams メタデータ パッケージ** ] を選択 **します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="スクリーンショットは、zip Teams メタデータ パッケージの選択を示す例です。":::

1. [ **ローカル]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="スクリーンショットは、環境内のローカルの選択を示す例です。":::

プレビュー ローカルは、イメージに示すように表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="スクリーンショットは、ローカルのプレビューを示す例です。":::

## <a name="preview-manifest-file-in-remote-environment"></a>リモート環境でのマニフェスト ファイルのプレビュー

Visual Studio Code を使用してマニフェスト ファイルをプレビューするには:

* [Teams Toolkit 拡張機能の **開発**] **で [クラウドでプロビジョニング]** を選択します
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="スクリーンショットは、クラウド リソースでのプロビジョニングの選択を示す例です。":::

コマンド パレットを使用してマニフェスト ファイルをプレビューするには:

* トリガー Teams: コマンド パレットから **クラウドでプロビジョニング** します。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="コマンド パレットを使用してクラウド リソースをプロビジョニングする例を示すスクリーンショット。":::

リモート Teams アプリの構成が生成され、フォルダーの下にパッケージマニフェストとプレビュー マニフェストが `build/appPackage` ビルドされます。

また、リモート環境で 2 つの方法でマニフェスト ファイルをプレビューすることもできます

* codelens でプレビュー オプションを使用する
* **Zip Teams メタデータ パッケージ** オプションを使用する

次の手順は、codelens でプレビュー オプションを使用してマニフェスト ファイルをプレビューするのに役立ちます。

1. ファイルの codelens `manifest.template.json` で [**プレビュー**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="スクリーンショットは、マニフェスト ファイルの codelens にプレビューを表示する例です。":::

1. 環境を選択します。

   > [!NOTE]
   > 複数の環境がある場合は、イメージに示すようにプレビューする環境を選択する必要があります。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="スクリーンショットは、環境の追加を示す例です。":::

次の手順は、リモート環境で **Zip Teams メタデータ パッケージ** オプションを使用してマニフェスト ファイルをプレビューするのに役立ちます。

1. ファイルを選択 `manifest.template.json` します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="manifest.template.json の選択を示す例を示すスクリーンショット。":::

1. Visual Studio Code ツール バーの [Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: ] アイコンを選択します。

1. [デプロイ] **で [Zip Teams メタデータ パッケージ** ] を選択 **します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="スクリーンショットは、zip Teams メタデータ パッケージの選択を示す例です。":::

1. 環境を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="スクリーンショットは、環境の追加を示す例です。":::

   > [!NOTE]
   > 複数の環境がある場合は、イメージに示すようにプレビューする環境を選択する必要があります。

## <a name="sync-local-changes-to-developer-portal"></a>ローカルの変更を開発者ポータルに同期する

マニフェスト ファイルをプレビューした後、次の方法でローカルの変更を開発者ポータルに同期できます。

> [!NOTE]
> 開発者ポータルの詳細については、「 [Teams 用開発者ポータル](../concepts/build-and-test/teams-developer-portal.md)」を参照してください。

1. Teams アプリ マニフェストをデプロイします。

   Teams アプリ マニフェストは、次のいずれかの方法で展開できます。

   * ファイルに `manifest.template.json` 移動し、右クリックしてコンテキスト メニューから選択 `Deploy Teams app manifest` します。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="スクリーンショットは、Teams アプリ マニフェストの展開の選択を示す例です。":::

   * コマンド パレットからトリガー `Teams: Deploy Teams app manifest` します。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="コマンド パレットから配置を示す例を示すスクリーンショット。":::

2. Teams プラットフォームに更新します。

   Teams プラットフォームには、次のいずれかの方法で更新できます。

   * の左上隅にある [ **Teams プラットフォームに更新** ] を選択します `manifest.{env}.json`。

   * **Teams をトリガーする: の** メニュー バー`manifest.{env}.json`にある Teams プラットフォームにマニフェストを更新します。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="スクリーンショットは、マニフェストのメニュー バーに Teams プラットフォームの更新プログラムを表示する例です。":::

コマンド パレットから **Teams: マニフェストを Teams プラットフォームに更新する** をトリガーすることもできます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="コマンド パレットから Teams: 更新マニフェストを Teams プラットフォームに更新するの選択を示す例を示すスクリーンショット。":::

> [!NOTE]
> エディターの codelens またはメニュー バーからトリガーすると、現在のマニフェスト ファイルが Teams プラットフォームに更新されます。 コマンド パレットからトリガーするには、ターゲット環境を選択する必要があります。

 CLI コマンド:

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> 変更が Dev Portal に更新されます。 開発ポータルの手動更新は上書きされます。

構成ファイルの変更またはテンプレートの変更によりマニフェスト ファイルが古くなっている場合は、次のいずれかのアクションを選択します。

* **プレビューのみ**: ローカル マニフェスト ファイルは、現在の構成に従って上書きされます。
* **プレビューと更新**: ローカル マニフェスト ファイルは現在の構成に従って上書きされ、Teams プラットフォームにも更新されます。
* **キャンセル**: アクションは実行されません。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="スクリーンショットは、プレビューのみを選択するためのナビゲーション、構成またはテンプレートの変更によりマニフェスト ファイルが古くなった場合のプレビューと更新、取り消しのオプションを示す例です。":::

## <a name="customize-your-teams-app-manifest"></a>Teams アプリ マニフェストをカスタマイズする

Teams Toolkit は、ローカル環境とリモート環境の `manifest.template.json` フォルダーにある次のマニフェスト テンプレート ファイルで構成されています。

* `manifest.template.json`
* `templates/appPackage`

ローカルデバッグまたはプロビジョニング中に、Teams Toolkit は、 から`manifest.template.json`マニフェストを読み込み、 から`state.{env}.json``config.{env}.json`構成を使用して[、Dev Portal](https://dev.teams.microsoft.com/apps) で Teams アプリを作成します。

### <a name="supported-placeholders-in-manifesttemplatejson"></a>manifest.template.json でサポートされているプレースホルダー

次の一覧では、 で `manifest.template.json`サポートされているプレースホルダーを示します。

* `{{state.xx}}` は定義済みのプレースホルダーであり、その値は Teams Toolkit によって解決されます。これは、`state.{env}.json` で定義されています。 の値を変更しないようにしてください `state.{env}.json`
* `{{config.manifest.xx}}` はカスタマイズされたプレースホルダーであり、値は から解決されます `config.{env}.json`

**カスタマイズされたパラメーターを追加するには**

1. 次のようにカスタマイズされたパラメーターを追加します。</br>
   a. パターン `{{config.manifest.xx}}`を使用して プレースホルダーを に`manifest.template.json`追加します。</br>
   b. に構成値を `config.{env}.json`追加します。

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. 構成ファイルに移動するには、構成プレースホルダーのいずれかを選択して構成 **ファイルに移動** するか、 `manifest.template.json`で **状態ファイルを表示** します。

### <a name="validate-manifest"></a>マニフェストを検証する

**Zip Teams メタデータ パッケージ** などの操作中に、Teams Toolkit はそのスキーマに対してマニフェストを検証します。 マニフェストを検証するさまざまな方法を次に示します。

* VSC で、コマンド パレットからトリガー `Teams: Validate manifest file` します。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="コマンド パレットから Teams 検証マニフェスト ファイルを表示する例を示すスクリーンショット。":::

* CLI で、次のコマンドを使用します。

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can go to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Screenshot is an example of showing preview values for local and dev environment.":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can go to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Screenshot is an example of showing the selection of an environment.":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Screenshot is an example of showing the preview values for all environments.":::

::: zone-end

::: zone pivot="visual-studio"

## Edit Teams app manifest using Visual Studio

Teams Toolkit in Visual Studio loads manifest from `manifest.template.json` with configurations from `state.{env}.json` and `config.{env}.json` while provisioning and preparing app dependencies. You can also create Microsoft Teams app in [Developer Portal](https://dev.teams.microsoft.com/apps) with the manifest.

After scaffolding, in the manifest template file under `templates/appPackage` folder,
`manifest.template.json` is shared between local and remote environment.

In the manifest template, select **Project** > **Teams Toolkit** > **Open Manifest File**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Screenshot is an example of showing the navigation to open manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png":::

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

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Screenshot is an example showing when you hover over placeholder, can view the values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png":::

* You can also hover over the key besides each placeholder in `manifest.template.json`, and you can see the same values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Screenshot is an example showing when you hover over key beside placeholder can view the same values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png":::

   > [!NOTE]
   > If the environment has not been provisioned, or the Teams app dependencies have not been prepared, it indicates that the values for placeholder have not been generated. Please follow the guidance inside hover to generate corresponding values.

### Preview manifest file

To preview the manifest file, you can sideload for local or deploy for Azure. You can preview the manifest file by performing the following step:

* Select **Project** > **Teams Toolkit** and trigger **Prepare Teams App Dependencies** or **Provision in the Cloud** that generates configuration for local or remote Teams app.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Screenshot is an example of showing preview manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png":::

There are two other ways to upload zip app package before you can preview manifest file:

1. From the list of menu select **Project** > **Teams Toolkit** > **Zip App Package**, and select **For Local** or **For Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Screenshot is an example of showing the navigation to zip app package for local and azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png":::

1. You can also upload zip app package from Solution Explorer, if you right-click on **MyTeamsApp1** and then select **Teams Toolkit** > **Zip App Package** > **For Local** or **For Azure**.

  > [!NOTE]
  > In this scenario the project name is **MyTeamsApp1**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="Screenshot is an example of showing the list of Teams toolkit menus from solution explorer." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png":::

Teams Toolkit generates the zip app package, and to preview manifest file content you can follow the step below:

* Right-click on **manifest.template.json** under **appPackage** folder, select **Preview Manifest File** > **For Local** or **For Azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Screenshot is an example of showing the preview manifest menu for local and azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png":::

This displays the preview of the manifest file in Visual Studio.

### Sync local changes to Developer Portal

After you've previewed the manifest file in Visual Studio, you can now sync the local changes to the Developer Portal. Select **Project** > **Teams Toolkit** > **Update Manifest in Teams Developer Portal**, or context menu from Solution Explorer. You can now preview the manifest file in Developer Portal as a result of syncing the local changes.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Screenshot is an example of showing the navigation to update manifest in Teams developer portal." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png":::

The changes are updated to Teams Developer Portal.

> [!NOTE]
>
> * Select **Overwrite and update** or **Cancel** from the **Warning** dialog box to make any manual updates that can be overwritten in the Developer Portal.
> * When you create a Teams command bot using Visual Studio, two app IDs are registered in Azure Active Directory. You can identify the app IDs in the Developer Portal as **Application client ID** under Basic information and existing **Bot ID** under **App features**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Screenshot is an example of showing the update warning." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png":::

::: zone-end

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)
* [Provision cloud resources using Visual Studio](provision-cloud-resources.md)
* [Deploy Teams app to the cloud using Visual Studio](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
