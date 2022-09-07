---
title: Teams アプリの新規作成
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit を使用して新しい Teams アプリを作成する方法について説明します
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: e64daa0c3288f97286177e814204404522a6d6b9
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616625"
---
# <a name="create-a-new-teams-project"></a>新しい Teams プロジェクトを作成する

Teams Toolkit で [新しい Teams アプリの作成] を選択すると **、新しい** Teams プロジェクトをビルドできます。 Teams Toolkit では、次の種類のアプリを作成できます。

| アプリの種類 | 定義 |
| --- | --- |
| Basic Teams アプリ | Basic Teams アプリは、ニーズに基づいて作成およびカスタマイズできるタブ、ボット、またはメッセージ拡張機能アプリです。 |
| シナリオ ベースの Teams アプリ | シナリオ ベースの Teams アプリは、通知ボット、コマンド ボット、SSO 対応タブ、または SPFx タブ アプリであり、1 つの特定のシナリオに適しています。 たとえば、通知ボットは通知の送信にのみ適しており、チャットには使用されません。 |

## <a name="create-a-new-teams-app"></a>Teams アプリの新規作成

新しい Teams アプリを作成する手順は、SPFx と通知ボットを除くすべての種類のアプリで似ています。 次の手順は、新しいタブ アプリを作成するのに役立ちます。

**アプリを作成するには**

1. Visual Studio Code を開きます。
1. Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: アイコンを選択します。
1. **[新しい Teams アプリを作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-teams-app.png" alt-text="Teams ツールキットサイドバー":::

1. **[新しい Teams アプリを作成]** を選択して、Teams Toolkit を使用してアプリを作成します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/select-create-app.png" alt-text="アプリを作成する":::

1. このチュートリアルでは、アプリをビルドする機能として **[Tab]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/select-tabapp1.png" alt-text="アプリ機能の選択":::

   > [!NOTE]
   > 要件に基づいて、任意の種類の機能を選択できます。

1. プログラミング言語として **[JavaScript]** を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/select-language-tab.png" alt-text="プログラミング言語を選択する方法を示すスクリーンショット":::

1. プロジェクト ワークスペースの場所を選択し、 **フォルダーを選択します**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/select-folder1.png" alt-text="select-folder":::

1. このチュートリアルでは、アプリケーション名として入力 `helloworld` します。 **Enter** キーを押します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/enter-name-tab.png" alt-text="アプリ名を入力する場所を示すスクリーンショット":::

   > [!NOTE]
   > 他の機能には独自のアプリケーション名を入力し、英数字のみを使用することを確認できます。

   数秒で Teams タブ アプリが作成されます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/tap-app-created1.png" alt-text="作成されたアプリを示すスクリーンショット":::

### <a name="directory-structure-for-different-app-types"></a>さまざまな種類のアプリのディレクトリ構造

Teams Toolkit には、アプリをビルドするためのすべてのコンポーネントが備わっています。 プロジェクトを作成した後、 **エクスプローラー** の下にプロジェクト のフォルダーとファイルを表示できます。

<br>
<details>
<summary><b>基本的な Teams アプリのディレクトリ構造</b></summary>

Teams の基本的なアプリとディレクトリ構造には、すべての種類のアプリに似た 3 種類があります。 次の例は、Teams タブ アプリの基本的なディレクトリ構造を示しています。

| フォルダー名 | コンテンツ |
| --- | --- |
| `.fx/configs` | ユーザーが Teams アプリ用にカスタマイズできる構成ファイル。 |
| - `.fx/configs/config.<envName>.json` | 環境すべての構成ファイル。 |
| - `.fx/configs/azure.parameters.<envName>.json` | すべての環境に対する Azure BICEP プロビジョニングのパラメーター ファイル。 |
| - `.fx/configs/projectSettings.json` | すべての環境に適用されるグローバル プロジェクト設定。 |
| `tabs` | プライバシーに関する通知、使用条件、構成タブなど、実行時に必要なタブ機能のためのコード。 |
| - `tabs/src/index.jsx` | メインのアプリ コンポーネントが `ReactDOM.render()` によってレンダリングされる、フロントエンド アプリのエントリ ポイント |
| - `tabs/src/components/App.jsx` | アプリで URL ルーティングを処理するためのコード。 [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) を呼び出して、アプリと Teams の間の通信を確立します。 |
| - `tabs/src/components/Tab.jsx` | アプリの UI を実装するコード。 |
| - `tabs/src/components/TabConfig.jsx` | アプリを構成する UI を実装するコード。 |
| `templates/appPackage` | アプリ マニフェスト テンプレート ファイルとアプリ アイコン: color.png および outline.png。 |
| - `templates/appPackage/manifest.template.json` | ローカルまたはリモートの環境でアプリを実行するためのアプリ マニフェスト。  |
| `templates/azure` | BICEP テンプレート ファイル |

> [!NOTE]
> ボットまたはメッセージ拡張機能アプリがある場合は、関連するフォルダーがディレクトリ構造に追加されます。

さまざまな種類の基本的な Teams アプリのディレクトリ構造の詳細については、次の表を参照してください。

| アプリの種類 | リンク |
| --- | --- |
| タブ アプリの場合 | [JavaScript を使用して初めてのタブ アプリを構築する](../sbs-gs-javascript.yml) |
| ボット アプリの場合 | [JavaScript を使用して初めてのボット アプリを構築する](../sbs-gs-bot.yml) |
| メッセージ拡張機能アプリの場合 | [JavaScript を使用して最初のメッセージ拡張アプリを作成する](../sbs-gs-msgext.yml) |

</details>
<br>
<details>
<summary><b>シナリオ ベースの Teams アプリのディレクトリ構造</b></summary>

4 種類のシナリオ ベースの Teams アプリとディレクトリ構造は、すべての種類のアプリで似ています。 次の例は、シナリオベースの通知ボット Teams アプリディレクトリ構造を示しています。

新しいプロジェクト フォルダーには、次のコンテンツが含まれています。

| フォルダー名 | コンテンツ |
| --- | --- |
| `.fx` | プロジェクト レベルの設定、構成、および環境の情報 |
| `.vscode` | ローカル デバッグ用の VS コード ファイル |
| `bot` | ボットのソース コード |
| `templates` | Teams アプリ マニフェストと対応する Azure リソースのテンプレート |

**ボット** フォルダー内のコア通知の実装とその内容は次のとおりです。

| ファイル名 | コンテンツ |
| --- | --- |
| `src/adaptiveCards/` | アダプティブ カードのテンプレート  |
| `src/internal/` | 通知機能用に生成された初期化コード |
| `src/index.*s` | ボット メッセージを処理し、通知を送信するエントリポイント |
| `.gitignore` | ボット プロジェクトからローカル ファイルを除外するファイル |
| `package.json` | ボット プロジェクトの npm パッケージ ファイル |

> [!NOTE]
> コマンド ボット、SSO 対応タブ、または SPFx タブ アプリがある場合は、関連するフォルダーがディレクトリ構造に追加されます。

さまざまな種類のシナリオ ベースの Teams アプリのディレクトリ構造の詳細については、次の表を参照してください。

| アプリの種類 | リンク |
| --- | --- |
| 通知ボット アプリの場合 | [Teams への通知の送信](../sbs-gs-notificationbot.yml) |
| コマンド ボット アプリの場合 | [ビルド コマンド ボット](../sbs-gs-commandbot.yml) |
| SPFx タブ アプリの場合 | [SPFx](../sbs-gs-spfx.yml) を使用して Teams アプリを構築する |

</details>
<br>
<details>
<summary><b>複数機能アプリのディレクトリ構造</b></summary>

追加機能を使用して、既存の Teams アプリにさらに機能を追加できます。 たとえば、既存のタブ アプリにボット アプリを追加すると、Teams Toolkit は関連するファイルとコードを含むボット フォルダーを追加します。

次の図は、タブ アプリのディレクトリ構造を示しています。

   :::image type="content" source="../assets/images/teams-toolkit-v2/tabapp-directory.png" alt-text="Tab アプリのディレクトリ構造":::

次の図は、ボット機能を備えたタブ アプリのディレクトリ構造を示しています。

   :::image type="content" source="../assets/images/teams-toolkit-v2/tab-app-with-bot-app.png" alt-text="ボット アプリディレクトリ構造を持つタブ アプリ":::

</details>

## <a name="see-also"></a>関連項目

* [Blazor を使用して Teams アプリを構築する](../sbs-gs-blazorupdate.yml)
* [C# または .NETを使用して Teams アプリをビルドする](../sbs-gs-csharp.yml)
* [すべての種類の環境の前提条件と Teams アプリの作成](tools-prerequisites.md)
* [Microsoft Teams Toolkit を使用してアプリをビルドする準備をする](build-environments.md)
