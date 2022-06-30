---
title: Teams アプリに機能を追加する
author: MuyangAmigo
description: このモジュールでは、Teams Toolkit の機能、利点、制限事項、および機能を追加する方法について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 81cddad2297ec526f94a3ab362422028b14b4598
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66557989"
---
# <a name="add-capabilities-to-teams-apps"></a>Teams アプリに機能を追加する

Teams Toolkit で機能を追加すると、既存の Teams アプリに追加機能を追加できます。次の表に、Teams アプリの機能を示します。

|**機能**|**説明**|
|--------|-------------|
| タブ |  タブは、アプリ マニフェストで宣言されたドメインを参照する単純な HTML タグです。 個々のユーザーのチーム、グループ チャット、または個人用アプリ内のチャネルの一部としてタブを追加できます。|
| ボット |  ボットは、テキスト、対話型カード、タスク モジュールを使用して Web サービスと対話するのに役立ちます。|
| メッセージの拡張機能 | メッセージ拡張機能は、Microsoft Teams クライアントのボタンとフォームを使用して Web サービスを操作するのに役立ちます。|

## <a name="advantages"></a>メリット

次の一覧では、TeamsFx でさらに機能を追加する利点を提供します。

* 利便性を提供します。
* Teams Toolkit を使用してソース コードを自動的に追加することで、アプリにさらに関数を追加します。

## <a name="limitations"></a>制限事項

TeamsFx でさらに機能を追加するための制限事項を次に示します。

* 最大 16 個のインスタンスにタブを追加できます。
* 1 つのインスタンスごとにボットとメッセージ拡張機能を追加できます。

## <a name="add-capabilities"></a>機能の追加

**次の方法で機能を追加できます。**

* Visual Studio Code で Teams Toolkit を使用して機能を追加する。
* コマンド パレットを使用して機能を追加する場合。

  > [!Note]
  > Teams アプリで機能を正常に追加した後は、環境ごとにプロビジョニングする必要があります。

* **Visual Studio Code で Teams Toolkit を使用して機能を追加するには、**

   1. **Visual Studio Code** を開きます。
   1. 左側のパネルから **Teams Toolkit を** 選択します。
   1. **[開発**] で [**機能の追加]** を選択します。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="更新された 1 つ":::

* **コマンド パレットを使用して機能を追加するには:**

   1. **コマンド パレットを** 開きます。
   1. **Teams:機能の追加を入力します**。
   1. **[Enter]** キーを押します。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/Teams-add-features.png" alt-text="チーム機能":::

   1. ポップアップから、プロジェクトに追加する機能を選択します。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="通知":::

## <a name="add-capabilities-using-teamsfx-cli"></a>TeamsFx CLI を使用して機能を追加する

* **プロジェクト ディレクトリ** をプロジェクト フォルダーに変更します。
* 次の表に、機能と必要なコマンドの一覧を示します。

  |機能とシナリオ| コマンド|
  |-----------------------|----------|
  |通知ボットを追加するには |`teamsfx add notification`|
  |コマンド ボットを追加するには |`teamsfx add command-and-response`|
  |sso 対応タブを追加するには |`teamsfx add sso-tab`|
  |タブを追加するには |`teamsfx add tab`|
  |ボットを追加するには |`teamsfx add bot`|
  |メッセージ拡張機能を追加するには |`teamsfx add message extension`|

## <a name="available-capabilities-to-add-for-different-teams-project"></a>さまざまな Teams プロジェクトに追加できる機能

Teams アプリで作成したプロジェクトに基づいて、さまざまな機能を追加することもできます。
次の表に、プロジェクトに追加できる機能の一覧を示します。

|既存の機能|サポートされているその他の機能|
|--------------------|--------------------|
|[SPFx] タブ |なし|
|[SSO 対応] タブ |SSO 対応タブ, 通知ボット, コマンド ボット, ボット, メッセージ拡張機能|
|通知ボット |SSO 対応タブ、タブ|
|コマンド ボット |SSO 対応タブ、タブ|
|Tab |Tab, notification bot, command bot, bot, message extension|
|Bot |メッセージ拡張機能、SSO 対応タブ、タブ|
|メッセージ拡張機能: |ボット、SSO 対応タブ、タブ |

## <a name="add-bot-tab-and-message-extension"></a>ボット、タブ、メッセージ拡張機能を追加する

ボットとメッセージ拡張機能を追加した後、プロジェクトの変更は次のようになります。

* ボット テンプレート コードは、パス `yourProjectFolder/bot`を持つサブフォルダーに追加されます。 これには、プロジェクトに **hello world** ボット アプリケーション テンプレートが含まれます。
* `launch.json` フォルダー `task.json` の下 `.vscode` には、Visual Studio Code に必要なスクリプトが含まれるフォルダーが更新され、アプリケーションをローカルでデバッグするときに実行されます。
* `manifest.template.json` フォルダー下の `templates/appPackage` ファイルが更新されます。これには、Teams プラットフォーム内のアプリケーションを表すマニフェスト ファイル内のボット関連情報が含まれます。 変更点は次のとおりです。
  * ボットの ID
  * ボットのスコープ
  * hello world ボット アプリケーションが応答できるコマンド
* 下の `templates/azure/teamsfx` ファイルが更新され `templates/azure/provision/xxx`、.bicep ファイルが再生成されます。
* 下の `.fx/config` ファイルは再生成され、新しく追加された機能に対して適切な構成でプロジェクトが設定されます。

タブを追加すると、プロジェクトの変更は次のようになります。

* フロントエンド タブ テンプレート コードは、プロジェクトへの **hello world** タブ アプリケーション テンプレートを含むパス`yourProjectFolder/tab`を持つサブフォルダーに追加されます。
* `launch.json` フォルダー `task.json` の下 `.vscode` には、Visual Studio Code に必要なスクリプトが含まれるフォルダーが更新され、アプリケーションをローカルでデバッグするときに実行されます。
* `manifest.template.json` フォルダー下の `templates/appPackage` ファイルが更新されます。これには、Teams プラットフォームのアプリケーションを表すマニフェスト ファイル内のタブ関連情報が含まれます。 変更は次のとおりです。
  * 構成可能なタブと静的タブ
  * タブのスコープ
* 下の `templates/azure/teamsfx` ファイルが更新され `templates/azure/provision/xxx`、.bicep ファイルが再生成されます。
* 下 `.fx/config` のファイルは再生成され、新しく追加された機能に対して適切な構成でプロジェクトが設定されます。

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

* Microsoft Teams でコマンド ボットをビルドするには、 [ステップ バイ ステップ](../sbs-gs-commandbot.yml) ガイドに従ってください

* Microsoft Teams で通知ボットを構築するには、 [ステップ バイ ステップ](../sbs-gs-notificationbot.yml) ガイドに従ってください。

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [新しい Teams プロジェクトを作成する](create-new-project.md)
