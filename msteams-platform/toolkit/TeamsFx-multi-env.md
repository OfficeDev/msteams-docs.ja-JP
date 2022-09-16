---
title: Teams Toolkit の TeamsFX 複数の環境
author: surbhigupta
description: このモジュールでは、TeamsFX マルチ環境 (新しい環境の作成、ターゲット環境の選択など) について説明します。
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 11/29/2021
ms.openlocfilehash: 964e7d8ad6e643d26178e04fb9ce706bb177f1d1
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780997"
---
# <a name="manage-multiple-environments"></a>複数の環境を管理する

 Microsoft Teams Toolkit では、複数の環境の作成と管理、成果物のプロビジョニング、および Microsoft Teams アプリのターゲット環境へのデプロイを簡単に行うことができます。

 複数の環境で次の操作を実行できます。

1. **運用環境の前にテスト** する: Teams アプリを運用環境に発行する前に、開発、テスト、ステージングなどの複数の環境を最新のアプリ開発ライフサイクルで設定できます。

2. **さまざまな環境でアプリの動作を管理** する: 運用環境でテレメトリを有効にするなど、複数の環境に対して異なるアプリ動作を設定できます。

   > [!NOTE]
   > 開発環境でテレメトリが無効になっていることを確認します。

   > [!TIP]
   > Teams アプリ プロジェクトが Visual Studio コードで開かれていることを確認します。

## <a name="create-new-environment"></a>新しい環境を作成する

プロジェクトを作成すると、既定で Teams Toolkit によって次が構成されます。

* ローカル コンピューター環境の構成を表す 1 つの `local` 環境。
* リモート環境またはクラウド環境の構成を表す 1 つの `dev` 環境。

> [!NOTE]
> 各プロジェクトに使用できる環境は 1 つだけです `local` が、リモート環境は複数あります。

**リモート環境を追加** する:

1. :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="アクティビティ バーのアクティビティ バーから"::: **Teams Toolkit** を選択します。
2. 次の図に示すように、[ **+Teams: 新しい環境の作成** ] セクションで [ **環境** ] セクションを選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="新しい環境を作成する":::

> [!Note]
> 複数の環境がある場合は、同じ環境を作成するために既存の環境を選択する必要があります。 このコマンドは、選択した既存の環境のファイルの `config.<newEnv>.json` 内容を `azure.parameters.<newEnv>.json` 、作成した新しい環境にコピーします。

## <a name="target-environment"></a>ターゲット環境

ターゲット環境を選択できます。複数のリモート環境がある場合は、Teams Toolkit からターゲット環境の選択を求めるメッセージが表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="env を追加する":::

## <a name="project-folder-structure"></a>プロジェクト フォルダー構造

プロジェクトを作成した後、Visual Studio Code の **エクスプローラー** の下にプロジェクト フォルダーとファイルを表示できます。 Teams Toolkit では、カスタム コードに加えて、いくつかのファイルを`configs`使用して、アプリの 、および`templates`アプリ`states`の保守を行います。 次の一覧では、ファイルを提供し、複数の環境との関係の概要を示します。

* `.fx/configs`: Teams アプリ用にユーザーがカスタマイズできるファイルを構成します。
  * `config.<envName>.json`: 環境ごとの構成ファイル。
  * `azure.parameters.<envName>.json`: 環境ごとの Azure Bicep プロビジョニングのパラメーター ファイル。
  * `projectSettings.json`: すべての環境に適用されるグローバル プロジェクト設定。
* `.fx/states`: Teams Toolkit によって生成された結果をプロビジョニングします。
  * `state.<envName>.json`: 環境ごとに出力ファイルをプロビジョニングします。
  * `<env>.userdata`: 環境ごとのプロビジョニング出力のユーザー データ。
* `templates`
  * `appPackage`: アプリ マニフェスト テンプレート ファイル。
  * `azure`: Bicep テンプレート ファイル。

## <a name="customize-resource-provision"></a>リソースのプロビジョニングをカスタマイズする

Teams Toolkit を使用すると、構成ファイルとテンプレート ファイルを変更して、各環境でリソースのプロビジョニングをカスタマイズできます。

次の表に、カスタマイズされたリソースプロビジョニングの一般的なシナリオを示します。

| シナリオ | 場所| 説明 |
| --- | --- | --- |
| Azure リソースをカスタマイズする |下の Bicep ファイル `templates/azure` `.fx/azure.parameters.<envName>.json` | [ARM パラメーターとテンプレートをカスタマイズする](provision.md#customize-arm-template-files) |
| Teams アプリ用に既存の Azure AD アプリを再利用する | `auth` のセクション`.fx/config.<envName>.json`|  [Teams アプリに既存の Azure AD アプリを使用する](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| ボット用に既存の Azure AD アプリを再利用する |`bot` のセクション`.fx/config.<envName>.json`| [ボットに既存の Azure AD アプリを使用する](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| SQL のプロビジョニング中にユーザーの追加をスキップする |`skipAddingSqlUser` 内のプロパティ`.fx/config.<envName>.json`| [SQL データベースのユーザーの追加をスキップする](provision.md#skip-adding-user-for-sql-database) |
| アプリ マニフェストをカスタマイズする |`templates/manifest.template.json` セクションの下 `manifest` のファイル `.fx/config.<envName>.json`| [Toolkit でアプリ マニフェストをプレビューする](TeamsFx-preview-and-customize-app-manifest.md)|

## <a name="scenarios"></a>シナリオ

さまざまな環境でリソースプロビジョニングをカスタマイズするには、次のシナリオを参照してください。
<br>

<br><details>
<summary><b>シナリオ 1: さまざまな環境に合わせて Teams アプリ名をカスタマイズする </b></summary>

Teams アプリ名`myapp(dev)`は、既定の環境と`myapp(staging)`ステージング`staging`環境`dev`に設定できます。

カスタマイズの手順:

1. 構成ファイル `.fx/configs/config.dev.json`を開きます。
2. **short** **`myapp(dev)`** のプロパティを **`manifest`****`appName`** >  >  .

  更新対象 `.fx/configs/config.dev.json` は次のとおりです。

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

3. 新しい環境を作成し、存在しない場合は名前を付 `staging` けることができます。
4. 構成ファイル `.fx/configs/config.staging.json`を開きます。
5. 同じプロパティを更新します `myapp(staging)`。
6. これで、プロビジョニング コマンドと`staging`環境を`dev`実行して、リモート環境でアプリ名を更新できます。 Teams Toolkit でプロビジョニング コマンドを実行するには、「 [プロビジョニング](provision.md#provision-using-teams-toolkit-in-visual-studio-code)」を参照してください。

</details>

<details>
<summary><b>シナリオ 2: さまざまな環境に合わせて Teams アプリの説明をカスタマイズする</b></summary>

さまざまな環境に対して異なる Teams アプリの説明を設定できます。

* 既定の環境 `dev`の場合、説明は `my app description for dev`.
* ステージング環境 `staging`の場合、説明は `my app description for staging`.

カスタマイズの手順:

1. 構成ファイル `.fx/configs/config.dev.json`を開きます。
2. 値を持つ新しいプロパティを **`manifest`** > **`short`** > **`description`** 追加します。**`my app description for dev`**

  更新対象 `.fx/configs/config.dev.json` は次のとおりです。

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

3. 新しい環境を作成し、存在しない場合は名前を付 `staging` けます。
4. 構成ファイル `.fx/configs/config.staging.json`を開きます。
5. 同じプロパティ `my app description for staging`を .
6. Teams アプリ マニフェスト テンプレート `templates/appPackage/manifest.template.json`を開きます。
7. mustache 構文を使用してファイルを構成するで定義されている **変数** を使用するようにプロパティ **`short`****`description`** > を更新します。**`{{config.manifest.description.short}}`**
  
  更新対象 `manifest.template.json` は次のとおりです。

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

8. これで、プロビジョニング コマンドと`staging`環境を`dev`実行して、リモート環境でアプリ名を更新できるようになりました。

</details>

<details>
<summary><b>シナリオ 3: すべての環境の Teams アプリの説明をカスタマイズする</b></summary>

Teams アプリの説明は、すべての環境に対して `my app description` 設定できます。

Teams アプリ マニフェスト テンプレートはすべての環境で共有されるため、ターゲットの説明の値を更新できます。

1. Teams アプリ マニフェスト テンプレート `templates/appPackage/manifest.template.json`を開きます。
2. ハードコーディングされた文字列を使用してプロパティ **`description`** > **`short`** を更新します。**`my app description`**
  
  更新対象 `manifest.template.json` は次のとおりです。

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

3. **すべての** 環境に対してプロビジョニング コマンドを実行して、リモート環境でアプリ名を更新できるようになりました。

</details>

<details>
<br><summary><b>シナリオ 4: さまざまな環境に合わせて Azure リソースをカスタマイズする</b></summary>

環境ごとに Azure リソースをカスタマイズできます。たとえば、fx/configs/azure.parameters に対応する環境を編集できます。Azure 関数名を指定する {env}.json ファイル。

Bicep テンプレートとパラメーター ファイルの詳細については、 [クラウド リソースのプロビジョニング](provision.md)に関するページを参照してください。
</details>
</br>

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [クラウド リソースをさらに追加する](add-resource.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)
* [さまざまな環境でアプリの動作をテストする](test-app-behavior.md)
