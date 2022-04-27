---
title: Teams Toolkitでアプリ マニフェストTeamsカスタマイズする
author: zyxiaoyuer
description: Teams アプリ マニフェストをカスタマイズする
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: de85674891a53c1e87b43ae1d472daf35716c348
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073541"
---
# <a name="customize-app-manifest-in-toolkit"></a>Toolkitでアプリ マニフェストをカスタマイズする

Teams Toolkitは、ローカル環境とリモート環境のフォルダー下にある次のマニフェスト テンプレート ファイルで`manifest.template.json`構成されます。

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>前提条件

* [Teams Toolkit の最新バージョン](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)をインストールします。

> [!TIP]
> Visual Studio Codeでアプリ プロジェクトTeams開かれていることを確認します。

ローカル デバッグまたはプロビジョニング中に、Teams Toolkitから構成`state.{env}.json`を使用してマニフェスト`manifest.template.json`を読み込み、`config.{env}.json`[開発ポータル](https://dev.teams.microsoft.com/apps)でチーム アプリを作成します。


## <a name="placeholders-supported-in-manifesttemplatejson"></a>manifest.template.json でサポートされているプレースホルダー

* `{{state.xx}}`は定義済みのプレースホルダーであり、値は Teams Toolkit `state.{env}.json`によって解決されます。. 状態の値を変更しないようにしてください。{env}.json
* `{{config.manifest.xx}}` はカスタマイズされたプレースホルダーであり、その値は `config.{env}.json`

  1. カスタマイズされたパラメーターは、次のように追加できます。
      1. manifest.template.json に次のパターンを含むプレースホルダーを追加します。 `{{config.manifest.xx}}`
      2. config に構成値を追加します。{env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

   2. 構成ファイルに移動するには、いずれかの構成プレースホルダー [構成 **ファイルに移動** ] または [ **状態ファイルの表示** ] を選択します。 `manifest.template.json`

## <a name="see-also"></a>関連項目

[Teams Toolkitでアプリ マニフェストTeamsプレビューする](TeamsFx-manifest-preview.md)
