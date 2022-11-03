---
title: Teams アプリの新規作成
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit を使用して新しい Teams アプリを作成する方法について説明します
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 234aa5ae8c118f323f8f0436f6b7226c490baa7c
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833052"
---
# <a name="create-a-new-teams-project"></a>新しい Teams プロジェクトを作成する

このセクションでは、Visual Studio Code と Visual Studio を使用して新しい Teams プロジェクトを作成する方法について説明します。

::: zone pivot="visual-studio-code"

## <a name="create-a-new-teams-project-for-visual-studio-code"></a>Visual Studio Code 用の新しい Teams プロジェクトを作成する

[Teams Toolkit で新しい Teams アプリを作成する] を選択して **、新しい Teams プロジェクトを** ビルドできます。 Teams Toolkit では、次の種類のアプリを作成できます。

| アプリの種類 | 定義 |
| --- | --- |
| Basic Teams アプリ | 基本的な Teams アプリは、必要に応じて作成およびカスタマイズできるタブ、ボット、またはメッセージ拡張機能アプリです。 |
| シナリオ ベースの Teams アプリ | シナリオ ベースの Teams アプリは、通知ボット、コマンド ボット、SSO 対応タブ、または SPFx タブ アプリであり、1 つの特定のシナリオに適しています。 たとえば、通知ボットは通知の送信にのみ適しており、チャットには使用されません。 |

## <a name="create-a-new-teams-app"></a>Teams アプリの新規作成

新しい Teams アプリを作成する手順は、SPFx と通知ボットを除くすべての種類のアプリに似ています。 次の手順は、新しいタブ アプリを構築するのに役立ちます。

**アプリを作成するには**

1. Visual Studio Code を開きます。

1. 左側のナビゲーション バーで [Teams ツールキット :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: ] アイコンを選択します。

1. **[新しい Teams アプリを作成]** を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. アプリの機能として **[Tab]** が選択されていることを確認します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-capabilities-tabapp.png" alt-text="アプリ機能の選択":::

1. プログラミング言語として **[JavaScript]** を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-language-tab.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. **[既定のフォルダー]** を選択して、プロジェクトのルート フォルダーを既定の場所に格納します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-default-location.png" alt-text="既定の場所を選択する":::

   次の手順では、既定の場所を変更する手順を示します。

      1. [ **参照] を選択します**。

          :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-browse.png" alt-text="ストレージの参照を選択する":::

      1. プロジェクト ワークスペースの場所を選択します。

      1. [ **フォルダーの選択] を選択します**。

          :::image type="content" source="../assets/images/teams-toolkit-v2/select-folder.png" alt-text="ストレージ用の select-folder":::

1. アプリケーション名として `helloworld` と入力します。 英数字のみを使用してください。 **Enter** キーを押します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/enter-name-tab1.png" alt-text="アプリ名を入力する場所を示すスクリーンショット。":::

1. 既定では、プロジェクトは 10 秒以内に新しいウィンドウで開きます。 現在のウィンドウで開く場合は、[現在のウィンドウ **で開く**] を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/new-window-notification.png" alt-text="新しいウィンドウ通知":::

   数秒で Teams タブ アプリが作成されます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/tap-app-created1.png" alt-text="作成されたアプリを示すスクリーンショット。":::

### <a name="directory-structure-for-different-app-types"></a>さまざまなアプリの種類のディレクトリ構造

Teams Toolkit には、アプリをビルドするためのすべてのコンポーネントが備わっています。 プロジェクトを作成したら、[ **エクスプローラー**] でプロジェクト のフォルダーとファイルを表示できます。

<br>
<details>
<summary><b>基本的な Teams アプリのディレクトリ構造</b></summary>

3 種類の基本的な Teams アプリがあり、ディレクトリ構造はすべての種類のアプリに似ています。 次の例は、基本的な Teams タブ アプリのディレクトリ構造を示しています。

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

4 種類のシナリオ ベースの Teams アプリがあり、ディレクトリ構造はすべての種類のアプリに似ています。 次の例は、シナリオベースの通知ボット Teams アプリディレクトリ構造を示しています。

新しいプロジェクト フォルダーには、次の内容が含まれています。

| フォルダー名 | コンテンツ |
| --- | --- |
| `.fx` | プロジェクト レベルの設定、構成、環境の情報 |
| `.vscode` | ローカル デバッグ用の VS コード ファイル |
| `bot` | ボットのソース コード |
| `templates` | Teams アプリ マニフェストと対応する Azure リソースのテンプレート |

**ボット** フォルダー内の主要な通知の実装には、次のものが含まれています。

| ファイル名 | コンテンツ |
| --- | --- |
| `src/adaptiveCards/` | アダプティブ カードのテンプレート  |
| `src/internal/` | 生成された通知機能の初期化コード |
| `src/index.*s` | ボット メッセージを処理し、通知を送信するエントリ ポイント |
| `.gitignore` | ボット プロジェクトからローカル ファイルを除外するファイル |
| `package.json` | ボット プロジェクトの npm パッケージ ファイル |

> [!NOTE]
> コマンド ボット、SSO 対応タブ、または SPFx タブ アプリがある場合、関連するフォルダーがディレクトリ構造に追加されます。

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

機能の追加を使用して、既存の Teams アプリにさらに機能を追加できます。 たとえば、既存のタブ アプリにボット アプリを追加した場合、Teams Toolkit は、関連するファイルとコードを含むボット フォルダーを追加します。

次の図は、タブ アプリのディレクトリ構造を示しています。

   :::image type="content" source="../assets/images/teams-toolkit-v2/tabapp-directory.png" alt-text="タブ アプリディレクトリの構造":::

次の図は、ボット機能を備えたタブ アプリのディレクトリ構造を示しています。

   :::image type="content" source="../assets/images/teams-toolkit-v2/tab-app-with-bot-app.png" alt-text="ボット アプリディレクトリ構造を持つタブ アプリ":::

</details>

::: zone-end

::: zone pivot="visual-studio"

## <a name="create-new-teams-app-in-visual-studio"></a>Visual Studio で新しい Teams アプリを作成する

Teams ツールキットは、Teams アプリを作成するための Microsoft Teams アプリ テンプレートを Visual Studio に用意しています。  新しいプロジェクトを作成するときに必要な Teams アプリ テンプレートを検索して選択できます。 作成する Teams アプリ テンプレートを用意できます。

* タブ アプリ
* コマンド ボット
* 通知ボット
* メッセージ拡張機能アプリ

## <a name="prerequisites"></a>前提条件

| &nbsp; | インストール | 使用するには... |
| --- | --- | --- |
| &nbsp; | **必須** | &nbsp; |
| &nbsp; | Visual Studio バージョン 17.3 | Visual Studio のエンタープライズ エディションをインストールし、"ASP.NET" ワークロードと Microsoft Teams 開発ツールをインストールできます。 |
| &nbsp; | Teams ツールキット | アプリのプロジェクト スキャフォールディングを作成する Visual Studio 拡張機能。 最新バージョン​​を使用します。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams を使用して、チャット、会議、通話用のアプリを通じて共同作業を行うすべてのユーザーと 1 か所で共同作業を行うことができます。 |
 | &nbsp; | [Microsoft 365 テナントを準備する](../concepts/build-and-test/prepare-your-o365-tenant.md) | アプリをインストールするための適切なアクセス許可を持つ Teams アカウントにアクセスします。 |

## <a name="create-a-new-teams-app"></a>Teams アプリの新規作成

新しい Teams アプリを作成する手順は、通知ボットを除くすべての種類のアプリに似ています。 次の手順は、新しいタブ アプリを作成するのに役立ちます。

1. Visual Studio を開きます。
1. 次の 2 つのオプションのいずれかを使用して、新しいプロジェクトを作成します。

     :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project1_1.png" alt-text="開始からコードを使用して新しいプロジェクトを作成する":::

    * [**作業の開始**] で [**新しいプロジェクトの作成**] を選択すると、コード スキャフォールディングを使用してプロジェクト テンプレートを選択できます。
    * [ **コードなしで続行]** を選択して、コード スキャフォールディングなしでプロジェクトを作成し、Visual Studio で **[ファイル** > **] [新しい** > **プロジェクト** ] を選択します。

        :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project2_1.png" alt-text="[ファイル] メニューから新規プロジェクトを作成する":::

   [ **新しいプロジェクトの作成** ] ウィンドウが表示されます。  

1. 検索ボックスに「teams」と入力し、一覧から [ **Microsoft Teams アプリ** ] を選択し、[ **次へ**] を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/visual-studio.png" alt-text="Microsoft Teams アプリを検索して選択する":::

   [ **新しいプロジェクトの構成]** ウィンドウが表示されます。

     :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-project-name_1.png" alt-text="アプリケーションに名前を付ける":::

    1. プロジェクトに適した名前を入力します。

         > [!NOTE]
         > 入力するプロジェクト名は、 **ソリューション名** にも自動的に入力されます。 必要に応じて、プロジェクト名に影響を与えなくてもソリューション名を変更できます。

    1. プロジェクト ワークスペースを作成するフォルダー パスを選択します。
    1. 必要に応じて、別のソリューション名を入力します。
    1. 必要に応じて、プロジェクトとソリューションを同じフォルダーに保存するオプションをオンにします。 このチュートリアルでは、このオプションは必要ありません。
    1. **[作成]** を選択します。

   [ **新しい Teams アプリケーションの作成]** ウィンドウが表示されます。

1. このチュートリアルでは、 **新** しい Teams アプリケーションを作成するために Tab が選択され、[ **作成**] を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-type_3.png" alt-text="Teams アプリの種類を選択する":::

   > [!NOTE]
   > プロジェクトに必要な種類の Teams アプリを選択できます。

   [**Teams ツールキットへようこそ**] ウィンドウの **[はじめに**] が表示されます。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-getting-started-page.png" alt-text="はじめに teams ツールキットを選択する":::

### <a name="directory-structure"></a>ディレクトリ構造

Teams Toolkit には、アプリをビルドするためのすべてのコンポーネントが備わっています。 プロジェクトを作成したら、[エクスプローラー] でプロジェクト のフォルダーとファイルを表示できます。

* **基本的な Teams アプリのディレクトリ構造**

  :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project-solution-explorer_1.png" alt-text="Teams ツールキットソリューション エクスプローラータブを選択する":::

* **シナリオ ベースの Teams アプリのディレクトリ構造**

  :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project-solution-explorer.png" alt-text="ソリューション エクスプローラー Teams ツールキットを選択する":::

## <a name="teams-app-templates-in-teams-toolkit-for-visual-studio"></a>Visual Studio 用 Teams ツールキットの Teams アプリ テンプレート

Teams ツールキットで、Teams アプリ テンプレートが既にさまざまな種類の Teams アプリ用に設定されていることがわかります。 次の表に、使用可能なすべてのテンプレートを示します。

|Teams アプリのテンプレート  |説明  |
|---------|---------|
|通知ボット     |通知ボット アプリは Teams クライアントに通知を送信できます。通知をトリガーする方法は複数あります。 たとえば、HTTP 要求または時間単位で通知をトリガーします。 また、ビジネス シナリオに基づいて通知のトリガーを選択することもできます。         |
|コマンド ボット     |ユーザーは、コマンドを入力してボットと対話するためにコマンド ボット アプリを使用できます。         |
|Tab     |タブ アプリは Teams 内に Web ページを表示し、Teams アカウントを使用してシングル サインオンを有効にします。         |
|メッセージ拡張機能     |Message Extension アプリには、アダプティブ カードの作成、Nugget パッケージの検索、"dev.botframework.com" ドメインのリンクの展開などの簡単な機能が実装されています。         |

> [!NOTE]
> プロジェクトが作成されると、Teams Toolkit によって [ **作業の開始** ] ウィンドウが自動的に開きます。 [ **作業の開始** ] ウィンドウの手順を確認し、Teams Toolkit のさまざまな機能を確認できるようになりました。

::: zone-end

## <a name="see-also"></a>関連項目

* [Blazor を使用して Teams アプリを構築する](../sbs-gs-blazorupdate.yml)
* [C# または .NETを使用して Teams アプリをビルドする](../sbs-gs-csharp.yml)
* [すべての種類の環境の前提条件と Teams アプリの作成](tools-prerequisites.md)
* [Microsoft Teams Toolkit を使用してアプリを構築する準備をする](build-environments.md)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
