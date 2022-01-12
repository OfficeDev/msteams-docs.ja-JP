---
title: アプリ マニフェストTeamsのカスタマイズTeams Toolkit
author: zyxiaoyuer
description: Teams アプリ マニフェストをカスタマイズする
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d9f2ea49ece8728101a738129e45dd8155887ebc
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768078"
---
# <a name="customize-app-manifest-in-teams-toolkit"></a>アプリ マニフェストをカスタマイズTeams Toolkit

Teams Toolkitは、フォルダーの下にある次のマニフェスト テンプレート ファイルで構成 `templates/appPackage` されます。

- `manifest.local.template.json` - ローカル デバッグ チーム アプリ
- `manifest.remote.template.json` - すべての環境で共有

## <a name="prerequisite"></a>前提条件

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> アプリ プロジェクトがTeams開いているVS Code。

プロビジョニング中に、Teams Toolkitからマニフェストを読み込み、構成と組み合わせて、開発ポータルで `manifest.remote.template.json` `state.{env}.json` Teams `config.{env}.json` アプリ[を作成します](https://dev.teams.microsoft.com/apps)。

ローカル デバッグ中に、Teams Toolkitからマニフェストを読み込み、構成と組み合わせて、開発ポータルで `manifest.local.template.json` `localSettings.json` Teams アプリ[を作成します](https://dev.teams.microsoft.com/apps)。

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>manifest.remote.template.json でサポートされているプレースホルダー

- `{{state.xx}}`は、定義済みのプレースホルダーで定義され、その値は Teams Toolkitによって解決されます `state.{env}.json` 。 状態の値を変更しない。{env}.json。
- `{{config.manifest.xx}}` は、値がから解決されるカスタマイズされたプレースホルダーです `config.{env}.json` 。
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

    各構成プレースホルダーの他に `manifest.remote.template.json` 、. `Go to config file` 構成ファイルを選択すると、構成ファイルに移動できます。

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>manifest.local.template.json でサポートされているプレースホルダー

`{{localSettings.xx}}`は、定義済みのプレースホルダーで定義され、その値は Teams Toolkitによって解決されます `localSettings.json` 。 localSettings.json の値を変更しない。

 > [!NOTE]
 > ローカル マニフェストをカスタマイズしない。

## <a name="see-also"></a>関連項目

[アプリTeamsマニフェストをプレビュー Teams Toolkit](TeamsFx-manifest-preview.md)
