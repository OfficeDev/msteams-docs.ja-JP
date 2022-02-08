---
title: アプリ マニフェストTeamsのカスタマイズTeams Toolkit
author: zyxiaoyuer
description: Teams アプリ マニフェストをカスタマイズする
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ca06fe1c657d8cb2e437c1f6df2ff2cd880ed320
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435769"
---
# <a name="customize-app-manifest-in-teams-toolkit"></a>アプリ マニフェストをカスタマイズTeams Toolkit

Teams Toolkitは、フォルダーの下にある次のマニフェスト テンプレート ファイルで構成`templates/appPackage`されます。

- `manifest.local.template.json` - ローカル デバッグ チーム アプリ
- `manifest.remote.template.json` - すべての環境で共有

## <a name="prerequisite"></a>前提条件

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> アプリ プロジェクトTeams開いているか確認Visual Studio Code。

プロビジョニング中に、Teams Toolkit `manifest.remote.template.json``state.{env}.json` `config.{env}.json`からマニフェストを読み込み、構成と組み合わせて、Dev Portal で Teams アプリ[を作成します](https://dev.teams.microsoft.com/apps)。

ローカル デバッグ中に、Teams Toolkit`manifest.local.template.json``localSettings.json`からマニフェストを読み込み、構成と組み合わせて、開発ポータルで Teams アプリ[を作成します](https://dev.teams.microsoft.com/apps)。

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>manifest.remote.template.json でサポートされているプレースホルダー

- `{{state.xx}}`は定義済みのプレースホルダーで、その値はで定義されている Teams Toolkitによって解決されます`state.{env}.json`。 状態の値を変更しない。{env}.json。
- `{{config.manifest.xx}}` は、値がから解決されるカスタマイズされたプレースホルダーです `config.{env}.json`。
  - カスタマイズされたパラメーターは、次のように追加できます。
    - manifest.remote.template.json にパターン付きプレースホルダーを追加します。 `{{config.manifest.xx}}`
    - config に構成値を追加します。{env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    各構成プレースホルダーの他に`manifest.remote.template.json`、.`Go to config file` 構成ファイルを選択すると、構成ファイルに移動できます。

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>manifest.local.template.json でサポートされているプレースホルダー

`{{localSettings.xx}}`は定義済みのプレースホルダーで、その値はで定義されている Teams Toolkitによって解決されます`localSettings.json`。 localSettings.json の値を変更しない。

 > [!NOTE]
 > ローカル マニフェストをカスタマイズしない。

## <a name="see-also"></a>関連項目

[アプリTeamsマニフェストをプレビュー Teams Toolkit](TeamsFx-manifest-preview.md)
