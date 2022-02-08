---
title: アプリに機能をTeamsする
author: MuyangAmigo
description: ドキュメントの機能の追加についてTeams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3e704b08caa9a3aafc388fe4aa2e8851292c944f
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435804"
---
# <a name="add-capabilities-to-your-teams-apps"></a>アプリに機能をTeamsする

アプリの機能の 1 つTeams新しいアプリをTeamsできます。 アプリの開発中に、Teams Toolkitを使用して、アプリにTeamsできます。 次の表に、アプリのTeams一覧を示します。

|**機能**|**説明**|
|--------|-------------|
| タブ |  タブは、アプリ マニフェストで宣言されたドメインを指す単純な HTML タグです。 個々のユーザーのチーム、グループ チャット、または個人用アプリ内のチャネルの一部としてタブを追加できます。|
| ボット |  ボットは、テキスト、対話型カード、タスク モジュールを介して Web サービスと対話するのに役立ちます。|
| メッセージング拡張機能 | メッセージング拡張機能は、Web サービスと対話するために、クライアント内のボタンとフォームMicrosoft Teamsします。|

## <a name="prerequisite"></a>前提条件

[バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> VS コードでTeamsアプリ プロジェクトが開いているか確認します。

## <a name="add-capabilities-using-teams-toolkit"></a>アプリケーションを使用して機能をTeams Toolkit

> [!IMPORTANT]
> アプリに機能を正常に追加した後、各環境に対してプロビジョニングをTeamsがあります。

1. [コード **Microsoft Visual Studio開きます**。
1. 左側 **のTeams Toolkit** を選択します。
1. [機能 **の追加] を選択します**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add capabilities.png" alt-text="capabilities":::

   コマンド パレットを開き、[機能の追加] Teams **入力することもできます**。 
      
    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/tree view capabilities.png" alt-text="代替機能":::

1. ポップアップから、プロジェクトに含める機能を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select capabilities.png" alt-text="select":::

1. [**OK**] を選択します。

選択した機能は、プロジェクトに完全に追加されます。 このTeams Toolkit新しく追加された機能のソース コードを生成します。

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>コマンド ウィンドウで TeamsFx CLI を使用して機能を追加する

1. ディレクトリをプロジェクト ディレクトリ **に変更します**。
1. 次のコマンドを実行して、プロジェクトにさまざまな機能を追加します。

   |機能とシナリオ| コマンド|
   |-----------------------|----------|
   |タブを追加するには|`teamsfx capability add tab`|
   |ボットを追加するには|`teamsfx capability add bot`|
   |メッセージング拡張機能を追加するには|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities-matrix"></a>サポートされる機能のマトリックス

アプリが既に持Teams機能とは別に、アプリにさまざまな機能を追加Teamsできます。 次の表に、さまざまなアプリ機能Teams示します。 

|既存の機能|その他のサポートされる機能を追加できます|
|--------------------|--------------------|
|タブとSPFx|なし|
|Azure のタブ|ボットとメッセージング拡張機能|
|Bot|タブ|
|メッセージング拡張機能|タブとボット|
|タブとボット|タブとメッセージ拡張機能|
|タブとメッセージング拡張機能|タブとボット|
|タブ、ボット、メッセージング拡張機能|タブ|
|タブ |ボットとメッセージ拡張機能|

## <a name="add-capabilities"></a>機能の追加

ボットとメッセージング拡張機能を追加した後、プロジェクトの変更点は次のとおりです。

- ボット テンプレート コードがパスを持つサブフォルダーに追加されます `yourProjectFolder/bot`。 これには、 **プロジェクトに hello world** ボット アプリケーション テンプレートが含まれます。
- `launch.json`フォルダー`task.json`とフォルダー`.vscode`の下が更新されます。このスクリプトには、Visual Studio Code必要なスクリプトが含まれています。アプリケーションをローカルでデバッグする場合に実行されます。 
- `manifest.remote.template.json`フォルダー`manifest.local.template.json`の下の`templates/appPackage`ファイルが更新されます。この情報には、アプリケーションを表すマニフェスト ファイル内のボット関連情報Teamsされます。 変更点は次のとおりです。
  - ボットの ID。
  - ボットのスコープ。
  - hello world ボット アプリケーションが応答できるコマンド。
- 下のファイル `templates/azure/teamsfx` が更新され、 `templates/azure/provision/xxx`.bicep ファイルが再生成されます。
- 下のファイル `.fx/config` が再生成され、プロジェクトが新しく追加された機能に対して適切な構成で設定されます。

タブを追加した後、プロジェクトの変更点は次のとおりです。

- フロントエンド タブ テンプレート コードは、 `yourProjectFolder/tab`プロジェクトに hello **world** タブ アプリケーション テンプレートを含むパスを持つサブフォルダーに追加されます。
- `launch.json`フォルダー`task.json`とフォルダー`.vscode`の下が更新されます。このスクリプトには、Visual Studio Code必要なスクリプトが含まれています。アプリケーションをローカルでデバッグする場合に実行されます。 
- `manifest.remote.template.json`フォルダー`manifest.local.template.json`の下の`templates/appPackage`ファイルが更新され、Teams プラットフォームのアプリケーションを表すマニフェスト ファイル内のタブ関連の情報が含まれます。変更は次のとおりです。
  - 構成可能なタブと静的タブ。
  - タブの範囲。
- 下のファイル `templates/azure/teamsfx` が更新され、 `templates/azure/provision/xxx`.bicep ファイルが再生成されます。
- 下のファイル `.fx/config` が再生成され、プロジェクトが新しく追加された機能に対して適切な構成で設定されます。

## <a name="limitations"></a>制限事項

さらに機能を追加する場合の TeamsFx の制限事項は次のとおりです。

* 最大 16 インスタンスのタブを追加できます。
* ボットとメッセージング拡張機能は、それぞれ 1 つのインスタンスに追加できます。

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [新しいプロジェクトTeamsする](create-new-project.md)
