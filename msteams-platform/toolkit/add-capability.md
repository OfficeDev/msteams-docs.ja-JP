---
title: Teams アプリに機能を追加する
author: surbhigupta
description: このモジュールでは、Teams Toolkit の機能を追加する方法について説明します
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: abcda0dd19388d1cdce2f2b440ecbae833b5f9c3
ms.sourcegitcommit: 6926cf5eee55d5047c11ca13afc7f6f23e270396
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2022
ms.locfileid: "68740605"
---
# <a name="add-capabilities-to-teams-apps"></a>Teams アプリに機能を追加する

Teams Toolkit を使用して機能を追加すると、既存の Microsoft Teams アプリに追加の機能を含めることができます。 より多くの機能を追加する利点は、Teams Toolkit を使用してソース コードを自動的に追加することで、アプリにさらに関数を追加できることです。 Teams アプリで作成したプロジェクトに基づいて、さまざまな機能を選択することもできます。 次の表に、Teams アプリの機能を示します。

|機能|説明|その他のサポートされている機能|
|--------|-------------|-----------------|
|**Basic Teams アプリ**|              |
| Tab |  タブは、アプリ マニフェストで宣言されたドメインを参照する単純な HTML タグです。 個々のユーザーのチーム、グループ チャット、または個人用アプリ内のチャネルの一部としてタブを追加できます。|タブ、通知ボット、コマンド ボット、ボット、メッセージ拡張機能|
|[SPFx] タブ| SPFx タブ アプリは Microsoft 365 でホストされており、クライアント側の SPFx ソリューションの開発とホストをサポートしています|None|
|[SSO 対応] タブ|シングル サインオン機能を持つユーザーを許可する SSO 対応タブ アプリを構築できます|SSO 対応タブ、通知ボット、コマンド ボット、ボット、メッセージ拡張機能|
| Bot |  ボットは、テキスト、対話型カード、タスク モジュールを介して Web サービスと対話するのに役立ちます。|メッセージ拡張機能、SSO 対応タブ、タブ|
| メッセージ拡張機能: | メッセージ拡張機能は、Microsoft Teams クライアントのボタンとフォームを使用して Web サービスと対話するのに役立ちます。|ボット、SSO 対応タブ、タブ|
|**シナリオ ベースの Teams アプリ**|             |
| 通知ボット | 通知ボットは、Teams チャネルまたはグループ チャットまたは個人用チャットでメッセージを事前に送信します。 通知ボットは、カードやテキストなどの HTTP 要求でトリガーできます。 |[SSO 対応] タブの [タブ]|
| コマンド ボット | コマンド ボットを使用すると、コマンド ボットを使用して反復的なタスクを自動化できます。 これは、アダプティブ カードを使用してチャットで送信される簡単なコマンドに応答します。 |[SSO 対応] タブの [タブ]|
| ワークフロー ボット| ワークフロー ボットを使用すると、ユーザーはワークフロー ボット アプリのアダプティブ カード アクション ハンドラー機能によって有効になっているアダプティブ カードと対話できます。|[SSO 対応] タブの [タブ]|

> [!NOTE]
> タブは最大 16 個のインスタンスに追加できます。 ボットとメッセージ拡張機能については、インスタンスごとに一度に 1 つずつ追加できます。

## <a name="add-capabilities"></a>機能の追加

次の方法で機能を追加できます。

* [Microsoft Visual Studio Code での Teams Toolkit の使用](#using-teams-toolkit-in-microsoft-visual-studio-code)
* [コマンド パレットの使用](#using-the-command-palette)
* [TeamsFx CLI の使用](#using-teamsfx-cli)

### <a name="using-teams-toolkit-in-microsoft-visual-studio-code"></a>Microsoft Visual Studio Code での Teams Toolkit の使用

   1. **Visual Studio Code** を開きます。
   1. アクティビティ バーから **[Teams Toolkit** ] を選択します。
   1. [**開発**] で [**機能の追加] を** 選択します。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="Teams Toolkit から機能を追加する":::

      > [!NOTE]
      > Teams アプリで機能が正常に追加されたら、環境ごとにプロビジョニングする必要があります。

### <a name="using-the-command-palette"></a>コマンド パレットの使用

   1. [ **コマンド パレットの表示** > **]を選択します** 。または **Ctrl + Shift + P キーを押** します。

      :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add-capabilities-command-palette.png" alt-text="コマンド 宮殿から機能を追加する":::

   1. **「Teams: 機能の追加」と入力します**。
   1. Enter キーを押します。

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/teams-add-features.png" alt-text="コマンド パレットを使用して機能を追加するには。":::

   1. ポップアップから、プロジェクトに追加する必要がある機能を選択します。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="通知":::

### <a name="using-teamsfx-cli"></a>TeamsFx CLI の使用

* **プロジェクト ディレクトリ** をプロジェクト フォルダーに変更します。
* 次の表に、機能と必要なコマンドを示します。

  |機能とシナリオ| command|
  |-----------------------|----------|
  |通知ボットを追加するには |`teamsfx add notification`|
  |コマンド ボットを追加するには |`teamsfx add command-and-response`|
  |SSO 対応タブを追加するには |`teamsfx add sso-tab`|
  |タブを追加するには |`teamsfx add tab`|
  |ボットを追加するには |`teamsfx add bot`|
  |メッセージ拡張機能を追加するには |`teamsfx add message extension`|

## <a name="changes-after-adding-capabilities"></a>機能を追加した後の変更

次の表は、機能を追加するときにアプリのファイルで確認できる変更を示しています。

|機能の追加|説明| 変更内容|
|------------|------------------------|---------|
|ボット、メッセージ拡張機能、タブ|**hello world**&nbsp;ボットまたはタブ アプリケーション テンプレートをプロジェクトに含めます。|フロントエンド ボットまたはタブ テンプレート コードは、それぞれパス `yourProjectFolder/bot` または `yourProjectFolder/tab` サブフォルダーに追加されます。|
| ボット、メッセージ拡張機能、タブ |Visual Studio Code に必要なスクリプトが含まれており、アプリケーションをローカルでデバッグするときに実行されます。 |フォルダーの下`.vscode`にあるファイル`launch.json`が`task.json`更新されます。|
| ボットとメッセージ拡張機能|Teams Platform のアプリケーションを表すボットまたはタブ関連の情報をマニフェスト ファイルに含めます。|フォルダーの下の`templates/appPackage`ファイル`manifest.template.json`が更新されます。これには、Teams プラットフォームのアプリケーションを表すマニフェスト ファイルにタブ関連情報が含まれます。 変更は、ボットの ID、ボットのスコープ、hello world ボットまたはタブ アプリケーションが応答できるコマンドに表示されます。|
|Tab|Teams Platform のアプリケーションを表すボットまたはタブ関連の情報をマニフェスト ファイルに含めます。|フォルダーの下の`templates/appPackage`ファイル`manifest.template.json`が更新されます。これには、Teams プラットフォームのアプリケーションを表すマニフェスト ファイルにタブ関連情報が含まれます。 変更は、構成可能なタブと静的タブ、およびタブのスコープに表示されます。|
|ボット、メッセージ拡張機能、タブ|teamsfx にボットまたはタブ関連&nbsp;の情報を含め、Azure 関数を統合するためのファイルをプロビジョニングします。|の下の `templates/azure/teamsfx` ファイルが更新され `templates/azure/provision/xxx`、.bicep ファイルが再生成されます。|
|ボット、メッセージ拡張機能、タブ|新しく追加された機能の適切な構成でプロジェクトが設定されていることを確認します。|の下の `.fx/config` ファイルが再生成されます|

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

* 詳細 [な](../sbs-gs-commandbot.yml) ガイドに従って、Microsoft Teams でコマンド ボットをビルドします。

* Microsoft Teams [で](../sbs-gs-notificationbot.yml) 通知ボットを構築するには、ステップバイステップ ガイドに従います。

* 詳細 [な](../sbs-gs-workflow-bot.yml) ガイドに従って、Microsoft Teams でワークフロー ボットを構築します。

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [新しい Teams プロジェクトを作成する](create-new-project.md)
