---
title: Teams アプリに機能を追加する
author: MuyangAmigo
description: Teams Toolkitの機能の追加について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: a0ebea1fb05e3583c90c41596da98a25d89f9b4c
ms.sourcegitcommit: 74623035d7c18194e339f566c820e0653bc3d8b6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656762"
---
# <a name="add-capabilities-to-teams-apps"></a>Teams アプリに機能を追加する

Teams Toolkitに機能を追加すると、既存のTeams アプリに追加機能を追加できます。次の表に、Teams アプリの機能を示します。

|**機能**|**説明**|
|--------|-------------|
| タブ |  タブは、アプリ マニフェストで宣言されたドメインを参照する単純な HTML タグです。 個々のユーザーのチーム、グループ チャット、または個人用アプリ内のチャネルの一部としてタブを追加できます。|
| ボット |  ボットは、テキスト、対話型カード、タスク モジュールを使用して Web サービスと対話するのに役立ちます。|
| メッセージの拡張機能 | メッセージ拡張機能は、Microsoft Teams クライアントのボタンやフォームを使用して Web サービスと対話するのに役立ちます。|

## <a name="advantages"></a>メリット

次の一覧では、TeamsFx でさらに機能を追加する利点を提供します。

* 利便性を提供します
* Teams Toolkitを使用してソース コードを自動的に追加することで、アプリにさらに関数を追加します。

## <a name="limitations"></a>制限事項

TeamsFx でさらに機能を追加するための制限事項を次に示します。

* 最大 16 個のインスタンスにタブを追加できます
* 1 つのインスタンスごとにボットとメッセージ拡張機能を追加できます

## <a name="add-capabilities"></a>機能の追加

**次の方法で機能を追加できます。**

* Visual Studio Code でTeams Toolkitを使用して機能を追加するには
* コマンド パレットを使用して機能を追加するには

  > [!Note]
  > Teams アプリで機能を正常に追加した後は、環境ごとにプロビジョニングする必要があります。

* **Visual Studio Code でTeams Toolkitを使用して機能を追加するには:**

   1. **Visual Studio Code** を開きます。
   1. 左側 **の** パネルからTeams Toolkitを選択します。
   1. **[開発**] で [**機能の追加]** を選択します。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="更新された 1 つ" border="true":::

* **コマンド パレットを使用して機能を追加するには:**

   1. **コマンド パレットを** 開きます。
   1. **「Teams:機能の追加」と入力します**。
   1. **[Enter]** キーを押します。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/Teams-add-features.png" alt-text="チーム機能" border="true":::

   1. ポップアップから、プロジェクトに追加する機能を選択します。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="通知" border="true":::

## <a name="add-capabilities-using-teamsfx-cli"></a>TeamsFx CLI を使用して機能を追加する

* ディレクトリを **プロジェクト ディレクトリ** に変更する
* 次の表に、機能と必要なコマンドの一覧を示します。

  |機能とシナリオ| コマンド|
  |-----------------------|----------|
  |通知ボットを追加するには |`teamsfx add notification `|
  |コマンド ボットを追加するには |`teamsfx add command-and-response `|
  |sso 対応タブを追加するには |`teamsfx add sso-tab`|
  |タブを追加するには |`teamsfx add tab`|
  |ボットを追加するには |`teamsfx add bot`|
  |メッセージ拡張機能を追加するには |`teamsfx add message extension`|

## <a name="available-capabilities-to-add-for-different-teams-project"></a>さまざまなTeams プロジェクトに追加できる機能

アプリで作成したプロジェクトに基づいて、さまざまな機能を追加Teams選択できます。
次の表に、プロジェクトに追加できる機能の一覧を示します。

|既存の機能|サポートされているその他の機能|
|--------------------|--------------------|
|[SPFx] タブ |None|
|[SSO 対応] タブ |SSO 対応タブ, 通知ボット, コマンド ボット, ボット, メッセージ拡張機能|
|通知ボット |SSO 対応タブ、タブ|
|コマンド ボット |SSO 対応タブ、タブ|
|Tab |Tab, notification bot, command bot, bot, message extension|
|Bot |メッセージ拡張機能、SSO 対応タブ、タブ|
|メッセージ拡張機能: |ボット、SSO 対応タブ、タブ |

## <a name="add-bot-tab-and-message-extension"></a>ボット、タブ、メッセージ拡張機能を追加する

ボットとメッセージ拡張機能を追加した後、プロジェクトの変更は次のようになります。

* ボット テンプレート コードは、パス `yourProjectFolder/bot`を持つサブフォルダーに追加されます。 これには、プロジェクトへの **hello world** ボット アプリケーション テンプレートが含まれます。
* `launch.json`フォルダー`task.json`の下`.vscode`に更新され、Visual Studio Code に必要なスクリプトが含まれ、アプリケーションをローカルでデバッグするときに実行されます
* `manifest.template.json`フォルダー下`templates/appPackage`のファイルが更新されます。これには、Teams Platform 内のアプリケーションを表すマニフェスト ファイル内のボット関連情報が含まれます。 変更点は次のとおりです。
  * ボットの ID
  * ボットのスコープ
  * hello world ボット アプリケーションが応答できるコマンド
* 下の `templates/azure/teamsfx` ファイルが更新され `templates/azure/provision/xxx`、.bicep ファイルが再生成されます
* 下の `.fx/config` ファイルは再生成され、新しく追加された機能に対して適切な構成でプロジェクトが確実に設定されます

タブを追加すると、プロジェクトの変更は次のようになります。

* フロントエンド タブ テンプレート コードは、プロジェクトへの **hello world** タブ アプリケーション テンプレートを含むパス`yourProjectFolder/tab`を持つサブフォルダーに追加されます。
* `launch.json`フォルダー`task.json`の下`.vscode`に更新され、Visual Studio Code に必要なスクリプトが含まれ、アプリケーションをローカルでデバッグするときに実行されます
* `manifest.template.json`フォルダー下`templates/appPackage`のファイルが更新されます。これには、Teams プラットフォーム内のアプリケーションを表すマニフェスト ファイル内のタブ関連情報が含まれます。 変更は次のとおりです。
  * 構成可能なタブと静的タブ
  * タブのスコープ
* 下の `templates/azure/teamsfx` ファイルが更新され `templates/azure/provision/xxx`、.bicep ファイルが再生成されます
* 下 `.fx/config` のファイルが再生成されます。これにより、新しく追加された機能に対して適切な構成でプロジェクトが設定されます

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

* [ステップ バイ ステップ](../sbs-gs-commandbot.yml) ガイドに従って、Microsoft Teamsでコマンド ボットをビルドする

* [ステップ バイ ステップ](../sbs-gs-notificationbot.yml) ガイドに従って、Microsoft Teamsで通知ボットをビルドします。

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [新しいTeams プロジェクトを作成する](create-new-project.md)
