---
title: アプリTeamsマニフェストをプレビュー Teams Toolkit
author: zyxiaoyuer
description: Teams アプリ マニフェストをプレビューする
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3555725fdea8ff858c842ed26ed652bb13e82b7f
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768586"
---
# <a name="preview-teams-app-manifest-in-teams-toolkit"></a>アプリ Teamsマニフェストをプレビュー Teams Toolkit

スキャフォールディング後、フォルダーで使用できるマニフェスト テンプレート ファイルを次に示 `templates/appPackage` します。

- `manifest.local.template.json` - ローカル デバッグ チーム アプリ。
- `manifest.remote.template.json` - すべてのリモート環境間で共有されます。

プレースホルダーから成るテンプレート ファイル、およびファイルの実際のTeams Toolkitは、以下のファイルおよび `.fx/configs` `.fx/states` .

## <a name="prerequisite"></a>前提条件

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> VS コードでTeamsアプリ プロジェクトが開いているか確認します。

## <a name="preview-manifest"></a>プレビュー マニフェスト

実際のコンテンツでマニフェストをプレビューするには、Teams Toolkit下にプレビュー マニフェスト ファイルを生成 `build/appPackage` します。

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>ローカル マニフェスト ファイルのプレビュー

ローカル チーム アプリのマニフェスト ファイルをプレビューするには **、F5** キーを押してローカル デバッグを実行する必要があります。 既定のローカル設定が生成され、ビルド **/appPackage** フォルダーの下にアプリ パッケージとプレビュー マニフェストビルドが生成されます。

次の手順に従ってローカル マニフェストをプレビューできます。

1. **manifest.local.template.json** ファイルの codelens で [プレビュー] を選択します。 
2. manifest.local.template.json ファイルのメニュー バーで [**マニフェスト ファイルのプレビュー] を選択** します。 
3. Treeview **で [zip Teamsメタデータ パッケージ] を選択** し、[ローカル] を **選択します**。
プレビュー ローカルは、イメージに示すように表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-1.png" alt-text="プレビュー":::

### <a name="preview-manifest-in-remote-environment"></a>リモート環境でマニフェストをプレビューする

リモート チーム アプリのマニフェスト ファイルをプレビューするには、Teams Toolkit拡張子 Treeview の開発パネルでクラウドで [プロビジョニング] を選択するか、Teams:**コマンド** パレットからクラウドでプロビジョニングをトリガーします。 リモート チーム アプリの構成を生成し、ビルド **/appPackage** フォルダーの下にパッケージマニフェストとプレビュー マニフェストをビルドします。

次の手順に従って、リモート環境でマニフェストをプレビューできます。

1. **manifest.remote.template.json ファイルの codelens で [プレビュー] を選択** します。 
2. **manifest.remote.template.json** ファイルのメニュー バーで [マニフェスト ファイルのプレビュー] を選択します。 
3. ツリー **ビューで [zip Teamsメタデータ パッケージ]** を選択します。
4. 環境を選択します。

複数の環境がある場合は、イメージに示すようにプレビューする環境を選択する必要があります。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="env の追加":::

## <a name="sync-local-changes-to-dev-portal"></a>ローカルの変更を開発ポータルに同期する

マニフェスト ファイルをプレビューした後、次の手順に従ってローカルの変更を Dev ポータルに同期できます。

1.  [**更新] をTeamsの左上** 隅にある [プラットフォームの更新] を選択します。`manifest.{env}.json`
2. **[Teams: マニフェストを更新して、Teamsの** メニュー バーでプラットフォームに更新します。`manifest.{env}.json`

 コマンド パレットからマニフェスト **TeamsプラットフォームにTeamsトリガー** することもできます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="ツリー ビュー":::

> [!NOTE]
> エディター の codelens または title からのトリガー **は**、現在のマニフェスト ファイルを新しいプラットフォームTeamsします。 コマンド パレットからトリガーするには、ターゲット環境を選択する必要があります。

構成ファイルの変更またはテンプレートの変更によりマニフェスト ファイルが古くなった場合は、次の操作を確認してください。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::

- **プレビューのみ**: ローカル マニフェスト ファイルは、現在の構成に従って上書きされます
- **プレビューと更新**: ローカル マニフェスト ファイルは、現在の構成に従って上書きされ、新しいTeamsされます
- **キャンセル**: 何もしない

> [!NOTE]
> 変更は開発ポータルに更新されます。 開発ポータルでいくつかの手動更新プログラムがある場合は、上書きされます。

## <a name="see-also"></a>関連項目

[アプリ マニフェストTeamsのカスタマイズTeams Toolkit](TeamsFx-manifest-customization.md)
