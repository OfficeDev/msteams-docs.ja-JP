---
title: Teams アプリに機能を追加する
author: MuyangAmigo
description: Teams Toolkitの機能の追加について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 746b089bf8be4b091a34969118e640d8571c2237
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103272"
---
# <a name="add-capabilities-to-your-teams-apps"></a>Teams アプリに機能を追加する

アプリの開発中に、Teamsアプリ機能を備えた新しいTeams アプリを作成できます。 次の表に、Teams アプリの機能を示します。

|**機能**|**説明**|
|--------|-------------|
| タブ |  タブは、アプリ マニフェストで宣言されたドメインを指す単純な HTML タグです。 個々のユーザーのチーム、グループ チャット、または個人用アプリ内のチャネルの一部としてタブを追加できます|
| ボット |  ボットは、テキスト、対話型カード、タスク モジュールを使用して Web サービスと対話するのに役立ちます|
| メッセージ拡張機能 | メッセージ拡張機能は、Microsoft Teams クライアントのボタンやフォームを使用して Web サービスと対話するのに役立ちます|

## <a name="prerequisite"></a>前提条件

* [Teams Toolkit の最新バージョン](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)をインストールします。

> [!TIP]
> TEAMSアプリ プロジェクトが VS コードで開かれていることを確認します。

## <a name="limitations"></a>制限事項

TeamsFx に対する制限事項と、さらに機能を追加する場合の制限事項は次のとおりです。

* 最大 16 個のインスタンスにタブを追加できます
* 1 つのインスタンスごとにボットとメッセージ拡張機能を追加できます

## <a name="add-capabilities"></a>機能を追加する

> [!Note]
> Teams アプリに機能を正常に追加した後は、環境ごとにプロビジョニングを実行する必要があります。
* Visual Studio CodeでTeams Toolkitを使用して機能を追加できます
    1. **Microsoft Visual Studio コードを** 開く
    1. 左側 **の** パネルからTeams Toolkitを選択する
    1. [**機能の追加]** を選択する

        :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add capabilities.png" alt-text="capabilities":::

*   コマンド パレットを開き、「Teams: 機能の追加:」と入力することもできます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/tree view capabilities.png" alt-text="代替機能":::


    1. ポップアップから、プロジェクトに含める機能を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select capabilities.png" alt-text="select":::

    2. [**OK**] を選択します。

選択した機能がプロジェクトに正常に追加されます。 Teams Toolkitは、新しく追加された機能のソース コードを生成します

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>コマンド ウィンドウで TeamsFx CLI を使用して機能を追加する

1. ディレクトリを **プロジェクト ディレクトリ** に変更する
1. 次のコマンドを実行して、プロジェクトにさまざまな機能を追加します。

   |機能とシナリオ| コマンド|
   |-----------------------|----------|
   |タブを追加するには|`teamsfx capability add tab`|
   |ボットを追加するには|`teamsfx capability add bot`|
   |メッセージ拡張機能を追加するには|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities"></a>サポートされている機能

Teams アプリに既に用意されている機能とは別に、Teams アプリにさまざまな機能を追加することもできます。 次の表に、さまざまなTeamsアプリ機能を示します。

|既存の機能|サポートされているその他の機能|
|--------------------|--------------------|
|SPFxタブ|None|
|Azure のタブ|ボットとメッセージの拡張機能|
|Bot|タブ|
|メッセージ拡張機能|タブとボット|
|タブとボット|タブとメッセージ拡張機能|
|タブとメッセージ拡張機能|タブとボット|
|タブ、ボット、メッセージ拡張機能|タブ|
|タブ |ボットとメッセージの拡張機能|

## <a name="add-bot-tab-and-message-extension"></a>ボット、タブ、メッセージ拡張機能を追加する

ボットとメッセージ拡張機能を追加した後、プロジェクトの変更は次のようになります。

* ボット テンプレート コードは、パス `yourProjectFolder/bot`を持つサブフォルダーに追加されます。 これには、プロジェクトへの **hello world** ボット アプリケーション テンプレートが含まれます。
* `launch.json`フォルダー`task.json`の下`.vscode`に更新され、Visual Studio Codeに必要なスクリプトが含まれ、アプリケーションをローカルでデバッグするときに実行されます
* `manifest.template.json`フォルダー下`templates/appPackage`のファイルが更新されます。これには、Teams Platform 内のアプリケーションを表すマニフェスト ファイル内のボット関連情報が含まれます。 変更点は次のとおりです。
  * ボットの ID
  * ボットのスコープ
  * hello world ボット アプリケーションが応答できるコマンド
* 下の `templates/azure/teamsfx` ファイルが更新され `templates/azure/provision/xxx`、.bicep ファイルが再生成されます
* 下の `.fx/config` ファイルは再生成され、新しく追加された機能に対して適切な構成でプロジェクトが確実に設定されます

タブを追加すると、プロジェクトの変更は次のようになります。

* フロントエンド タブ テンプレート コードは、プロジェクトへの **hello world** タブ アプリケーション テンプレートを含むパス`yourProjectFolder/tab`を持つサブフォルダーに追加されます。
* `launch.json`フォルダー`task.json`の下`.vscode`に更新され、Visual Studio Codeに必要なスクリプトが含まれ、アプリケーションをローカルでデバッグするときに実行されます
* `manifest.template.json`フォルダー下`templates/appPackage`のファイルが更新されます。これには、Teams プラットフォーム内のアプリケーションを表すマニフェスト ファイル内のタブ関連情報が含まれます。 変更は次のとおりです。
  * 構成可能なタブと静的タブ
  * タブのスコープ
* 下の `templates/azure/teamsfx` ファイルが更新され `templates/azure/provision/xxx`、.bicep ファイルが再生成されます
* 下 `.fx/config` のファイルが再生成されます。これにより、新しく追加された機能に対して適切な構成でプロジェクトが設定されます


## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [新しいTeams プロジェクトを作成する](create-new-project.md)
