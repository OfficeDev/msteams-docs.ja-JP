---
title: Teams Toolkitでアプリ マニフェストTeamsプレビューする
author: zyxiaoyuer
description: Teams アプリ マニフェストをプレビューする
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 57dc719f872d502beded14c30a09d72c27ee74c3
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073284"
---
# <a name="preview-app-manifest-in-toolkit"></a>Toolkitでアプリ マニフェストをプレビューする

マニフェスト テンプレート ファイル `manifest.template.json` は、スキャフォールディング後にフォルダーの下で `templates/appPackage` 使用できます。 プレースホルダーを含むテンプレート ファイルと実際の値は、異なる環境のファイル`.fx/configs``.fx/states`のTeams Toolkitによって解決されます。

## <a name="prerequisite"></a>前提条件

* [最新バージョンのTeams Toolkitを](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)インストールする

> [!TIP]
> Visual Studio コードでアプリ プロジェクトTeams開かれていることを確認します。

## <a name="preview-manifest"></a>マニフェストのプレビュー

実際のコンテンツを使用してマニフェストをプレビューするために、Teams Toolkitはフォルダーの下にプレビュー マニフェスト ファイルを`build/appPackage`生成します。

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>ローカル マニフェスト ファイルをプレビューする

ローカル チーム アプリのマニフェスト ファイルをプレビューするには、 **F5** キーを押してローカル デバッグを実行します。 既定のローカル設定が生成され、アプリ パッケージとプレビュー マニフェストがフォルダーの下に `build/appPackage` ビルドされます。

次の手順に従って、ローカル マニフェストをプレビューすることもできます。

1. ファイルの`manifest.template.json`コーデレンズで **プレビュー** を選択し、**ローカル** を選択します
2. ファイルのメニュー バーで **プレビュー マニフェスト ファイル** を `manifest.template.json` 選択する
3. Treeview で **Zip Teamsメタデータ パッケージ** を選択し、**ローカル** を選択します

プレビュー ローカルは、イメージに示すように表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="プレビュー":::

### <a name="preview-manifest-in-remote-environment"></a>リモート環境でマニフェストをプレビューする

リモート チーム アプリのマニフェスト ファイルをプレビューするには、Teams Toolkit拡張機能 Treeview の **開発** パネルで **クラウドでプロビジョニング** を選択するか、コマンド パレットから **クラウドでプロビジョニングTeamsトリガーします**。 リモート チーム アプリの構成を生成し、パッケージとプレビュー マニフェストをフォルダーの下に `build/appPackage` ビルドします。

次の手順に従って、リモート環境でマニフェストをプレビューすることもできます。

1. ファイルの`manifest.template.json`コーデレンズで **[プレビュー]** を選択する
2. ファイルのメニュー バーで **プレビュー マニフェスト ファイル** を `manifest.template.json` 選択する
3. Treeview で **Zip Teamsメタデータ パッケージ** を選択する
4. 環境を選択する

複数の環境がある場合は、イメージに示すようにプレビューする環境を選択する必要があります。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="env を追加する":::

## <a name="sync-local-changes-to-developer-portal"></a>ローカルの変更を開発者ポータルに同期する

マニフェスト ファイルをプレビューしたら、次の手順に従ってローカルの変更を開発者ポータルに同期できます。

1. の左上隅にある **プラットフォームTeams更新を** 選択します。`manifest.{env}.json`
2. Teamsを選択 **します。マニフェストをTeamsプラットフォームに更新** します。`manifest.{env}.json`

 Teamsをトリガーすることもできます。コマンド パレットから **プラットフォームTeamsマニフェストを更新** します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="ツリー ビュー":::

> [!NOTE]
> エディターのコードレンズまたは **タイトル** からトリガーすると、現在のマニフェスト ファイルがTeams プラットフォームに更新されます。 コマンド パレットからトリガーするには、ターゲット環境を選択する必要があります

  

構成ファイルの変更またはテンプレートの変更によりマニフェスト ファイルが古い場合は、次のいずれかのアクションを選択します。

* **プレビューのみ**: ローカル マニフェスト ファイルは、現在の構成に従って上書きされます
* **プレビューと更新**: ローカル マニフェスト ファイルは現在の構成に従って上書きされ、プラットフォームTeams更新されます
* **キャンセル**: アクションは実行されません

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::



> [!NOTE]
> 変更は Dev Portal で更新されます。 開発ポータルの手動更新プログラムはすべて上書きされます。

## <a name="see-also"></a>関連項目

[Teams Toolkitでアプリ マニフェストTeamsカスタマイズする](TeamsFx-manifest-customization.md)
