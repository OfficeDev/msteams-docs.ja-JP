---
title: アプリ マニフェストTeamsのカスタマイズTeams Toolkit
author: zyxiaoyuer
description: アプリ マニフェストTeamsカスタマイズする
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 34b454f63eb900fce2f38748838ce46558835ac5
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228107"
---
# <a name="customize-teams-app-manifest-in-teams-toolkit"></a>アプリ マニフェストTeamsのカスタマイズTeams Toolkit

Teams Toolkitは、フォルダーの下にある 2 つのマニフェスト テンプレート ファイルで構成 `templates/appPackage` されます。

- `manifest.local.template.json` - ローカル デバッグ チーム アプリ
- `manifest.remote.template.json` - すべての環境で共有

## <a name="prerequisite"></a>前提条件

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> VS コードで開Teamsアプリ プロジェクトを既に持っている必要があります。

プロビジョニング中に、Teams Toolkitから、およびから構成と組み合わせてマニフェスト `manifest.remote.template.json` を読み込 `state.{env}.json` む `config.{env}.json` 。 次に、このマニフェストを使用して [開発ポータルに Teams](https://dev.teams.microsoft.com/apps) アプリを作成します。

ローカル デバッグ中に、Teams Toolkitからマニフェストを読み込み、構成 `manifest.local.template.json` と組み合わせて `localSettings.json` 使用します。 次に、このマニフェストを使用して [開発ポータルに Teams](https://dev.teams.microsoft.com/apps) アプリを作成します。

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>manifest.remote.template.json でサポートされているプレースホルダー

- `{{state.xx}}`は、定義済みのプレースホルダーで定義され、その値は Teams Toolkitによって解決されます `state.{env}.json` 。 状態の値を変更する必要があります。{env}.json。
- `{{config.manifest.xx}}` は、値がから解決されるカスタマイズされたプレースホルダーです `config.{env}.json` 。
  - カスタマイズしたパラメーターを追加するには、次の手順を実行します。
    - manifest.remote.template.json にパターン付きプレースホルダーを追加します。 `{{config.manifest.xx}}`
    - config に構成値を追加します。{env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    各構成プレースホルダーの他 `manifest.remote.template.json` に、ボタン `Go to config file` があります。 イメージに示すように構成ファイルを選択すると、構成ファイルに移動できます。

    ![構成ファイルに移動する](./images/gotoconfigfile.png)

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>manifest.local.template.json でサポートされているプレースホルダー

`{{localSettings.xx}}`は、定義済みのプレースホルダーで定義され、その値は Teams Toolkitによって解決されます `localSettings.json` 。 localSettings.json の値を変更する必要があります。

 > [!NOTE]
 > ローカル マニフェストのカスタマイズは推奨されません。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [アプリTeamsマニフェストをプレビュー Teams Toolkit](TeamsFx-manifest-preview.md)
