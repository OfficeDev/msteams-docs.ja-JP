---
title: Teams Toolkit で Teams アプリ マニフェストをカスタマイズする
author: zyxiaoyuer
description: Teams アプリ マニフェストをカスタマイズする
ms.author: nliu
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 28a06da170ee52e4340aa3d401d39ad08f58e2ba
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65110261"
---
# <a name="customize-app-manifest-in-toolkit"></a>Toolkit でアプリ マニフェストをカスタマイズする

Teams Toolkit は、ローカル環境とリモート環境の `manifest.template.json` フォルダーにある次のマニフェスト テンプレート ファイルで構成されています。

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>前提条件

* [Teams Toolkit の最新バージョン](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)をインストールします。

> [!TIP]
> Teams アプリ プロジェクトが Visual Studio Code で開かれていることを確認します。

ローカル デバッグまたはプロビジョニング中に、Teams Toolkit は `manifest.template.json` からマニフェストを読み込みます。 `state.{env}.json`、`config.{env}.json` の構成を使用して、[Dev Portal](https://dev.teams.microsoft.com/apps) で Teams アプリを作成します。


## <a name="placeholders-supported-in-manifesttemplatejson"></a>manifest.template.json でサポートされているプレースホルダー

* `{{state.xx}}` は定義済みのプレースホルダーであり、その値は Teams Toolkit によって解決されます。これは、`state.{env}.json` で定義されています。 state.{env}.json の値を変更しないようにします。
* `{{config.manifest.xx}}` はカスタマイズされたプレースホルダーであり、値は `config.{env}.json` から解決されます

  1. 次のようにカスタマイズされたパラメーターを追加できます。
      1. manifest.template.json に次のパターンのプレースホルダーを追加します: `{{config.manifest.xx}}`
      2. config.{env}.json に構成値を追加します。

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

   2. 構成ファイルに移動するには、いずれかの構成プレースホルダーを選択 **構成ファイルに移動する** か、`manifest.template.json` で **状態ファイルを表示**

## <a name="see-also"></a>関連項目

[Teams Toolkit で Teams アプリ マニフェストをプレビューする](TeamsFx-manifest-preview.md)
