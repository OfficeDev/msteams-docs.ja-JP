---
title: Teams アプリをデバッグする
author: surbhigupta
description: このモジュールでは、Teams Toolkit で Teams アプリをデバッグする方法と Teams Toolkit の主な機能について説明します
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 5f0e909c9b6fbccc1f1a9a886858177f4673f85f
ms.sourcegitcommit: 707dad21dc3cf79ac831afe05096c0341bcf2fee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68653694"
---
# <a name="debug-your-teams-app"></a>Teams アプリをデバッグする

Teams Toolkit は、Microsoft Teams アプリのデバッグとプレビューに役立ちます。 デバッグは、Teams でプログラムが正常に実行されるように、問題やバグを確認、検出、修正するプロセスです。

::: zone pivot="visual-studio-code"

## <a name="debug-your-teams-app-for-visual-studio-code"></a>Visual Studio Code 用の Teams アプリをデバッグする

Microsoft Visual Studio Code の Teams Toolkit は、デバッグ プロセスを自動化します。 エラーを検出して修正したり、Teams アプリをプレビューしたりできます。 デバッグ設定をカスタマイズして、タブまたはボットを作成することもできます。

## <a name="debug-your-microsoft-teams-app-for-visual-studio-code"></a>Visual Studio Code 用の Microsoft Teams アプリをデバッグする

Visual Studio Code の Teams Toolkit では、デバッグ プロセスが自動化されます。 エラーを検出して修正したり、Teams アプリをプレビューしたりできます。 デバッグ設定をカスタマイズして、タブまたはボットを作成することもできます。

デバッグ プロセス中:

* Teams Toolkit では、アプリ サービスが自動的に開始され、デバッガーが起動され、Teams アプリがサイドロードされます。
* Teams Toolkit は、デバッグのバックグラウンド プロセス中に前提条件を確認します。
* Teams アプリは、デバッグ後に Teams Web クライアントでローカルでプレビューできます。
* また、ボット エンドポイント、開発証明書、またはデバッグ部分コンポーネントを使用して構成済みアプリを読み込むデバッグ設定をカスタマイズすることもできます。
* Microsoft Visual Studio Code を使用すると、タブ、ボット、メッセージ拡張機能、およびAzure Functionsをデバッグできます。

## <a name="key-debug-features-of-teams-toolkit"></a>Teams Toolkit の主なデバッグ機能

Teams Toolkit では、次のデバッグ機能がサポートされています:

* [デバッグの開始](#start-debugging)
* [マルチターゲット デバッグ](#multi-target-debugging)
* [ブレークポイントの切り替え](#toggle-breakpoints)
* [ホット リロード](#hot-reload)
* [デバッグの停止](#stop-debugging)

Teams Toolkit は、デバッグ プロセス中にバックグラウンド機能を実行します。これには、デバッグに必要な前提条件の検証が含まれます。 検証プロセスの進行状況は、Teams Toolkit の出力チャネルで確認できます。 セットアップ プロセスでは、Teams アプリを登録して構成できます。

### <a name="start-debugging"></a>デバッグの開始

**F5** キーを 1 回の操作として押して、デバッグを開始できます。 Teams Toolkit は、前提条件の確認を開始し、Azure AD アプリ、Teams アプリ、ボットを登録し、サービスを開始し、ブラウザーを起動します。

### <a name="multi-target-debugging"></a>マルチターゲット デバッグ

Teams Toolkit では、マルチターゲット デバッグ機能を利用して、タブ、ボット、メッセージ拡張機能、および Azure Functions を同時にデバッグします。

### <a name="toggle-breakpoints"></a>ブレークポイントの切り替え

タブ、ボット、メッセージ拡張機能、および Azure Functions のソース コードのブレークポイントを切り替えることができます。 ブレークポイントは、Web ブラウザーで Teams アプリを操作するときに実行されます。 次の図は、ブレークポイントの切り替えを示しています。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="ブレークポイントの切り替え" lightbox="../assets/images/teams-toolkit-v2/debug/toggle-points.png":::

### <a name="hot-reload"></a>ホット リロード

Teams アプリをデバッグするときに、タブ、ボット、メッセージ拡張機能、およびAzure Functionsのソース コードを更新して保存できます。 アプリが再読み込みされ、デバッガーがプログラミング言語に再アタッチされます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="ソース コードのホット リロード" lightbox="../assets/images/teams-toolkit-v2/debug/hot-reload.png":::

### <a name="stop-debugging"></a>デバッグの停止

ローカル デバッグを完了したら、フローティング デバッグ ツール バーから **[停止] (Shift + F5)** または **[Alt] Disconnect (Shift + F5)** を選択して、すべてのデバッグ セッションを停止し、タスクを終了できます。 次の図は、デバッグの停止アクションを示しています。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="デバッグの停止":::

## <a name="prepare-for-debug"></a>デバッグの準備

次の手順は、デバッグの準備に役立ちます。

### <a name="sign-in-to-microsoft-365"></a>Microsoft 365 にサインインする

Microsoft 365 に既にサインアップしている場合は、Microsoft 365 にサインインします。 詳細については、[Microsoft 365 開発者プログラムに関するページを](tools-prerequisites.md#microsoft-365-developer-program)参照してください。

### <a name="toggle-breakpoints"></a>ブレークポイントの切り替え

詳細については、「ブレークポイントの切り替え」を参照してください。詳細については、「タブ、ボット、メッセージ拡張機能、およびAzure Functionsのソース コードでブレークポイントを[切り替](#toggle-breakpoints)えることができます。

## <a name="customize-debug-settings"></a>デバッグ設定をカスタマイズする

Teams Toolkit を使用すると、デバッグ設定をカスタマイズして、タブまたはボットを作成できます。 カスタマイズ可能なオプションの完全な一覧の詳細については、 [デバッグ設定に](https://aka.ms/teamsfx-debug-tasks)関するドキュメントを参照してください。

### <a name="customize-scenarios"></a>シナリオをカスタマイズする

<br>

<details>

<summary><b>前提条件チェックをスキップする</b></summary>

で`.fx/configs/tasks.json``"prerequisites"``"Validate & install prerequisites"` > `"args"` > 、スキップする前提条件チェックを更新します。

  :::image type="content" source="../assets/images/teams-toolkit-v2/debug/skip-prerequisite-checks.png" alt-text="前提条件チェックをスキップする":::

</details>

<details>
<summary><b>開発証明書を使用する</b></summary>

1. で`.fx/configs/tasks.json`、下のチェック ボックスをオフにします >  > `"prerequisites"``"devCert"``"Validate & install prerequisites"``"args"`。
1. 証明書ファイルパスとキー ファイル パスに "SSL_CRT_FILE" と "SSL_KEY_FILE" を `.env.teamsfx.local` 設定します。

</details>

<details>
<summary><b>npm install args をカスタマイズする</b></summary>

で`.fx/configs/tasks.json`、npmInstallArgs を .`"Install npm packages"`
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/customize-npm-install.png" alt-text="npm パッケージをインストールする":::

</details>

<details>
<summary><b>ポートを変更する</b></summary>

* Bot
  1. プロジェクト全体を検索`"3978"`し、表示形式`tasks.json`を検索します。および `index.js`. `ngrok.yml`
  1. ポートに置き換えます。
     :::image type="content" source="../assets/images/teams-toolkit-v2/debug/modify-ports-bot.png" alt-text="ボットのポートを置き換える":::
* Tab
  1. で `.fx/configs/tasks.json`、検索します `"53000"`。
  1. ポートに置き換えます。
     :::image type="content" source="../assets/images/teams-toolkit-v2/debug/modify-ports-tab.png" alt-text="タブのポートを置き換える":::

</details>

<details>
<summary><b>独自のアプリ パッケージを使用する</b></summary>

で`.fx/configs/tasks.json`、アプリ パッケージのパスに設定`"appPackagePath"``"Build & upload Teams manifest"`します。

  :::image type="content" source="../assets/images/teams-toolkit-v2/debug/app-package-path.png" alt-text="独自のアプリ パッケージ パスを使用する":::

</details>

<details>
<summary><b>独自のトンネルを使用する</b></summary>

1. で`.fx/configs/tasks.json``"Start Teams App Locally"`、更新`"Start Local tunnel"`できます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-local-tunnel.png" alt-text="独自のトンネルを使用する":::
1. 独自のトンネル サービスを起動し、.`"botMessagingEndpoint"` `.fx/configs/tasks.json` `"Set up bot"`

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/set-up-bot.png" alt-text="メッセージング エンドポイントを更新する":::

</details>

<details>

<summary><b>環境変数の追加</b></summary>

タブ、ボット、メッセージ拡張機能、および Azure Functions の `.env.teamsfx.local` ファイルに環境変数を追加できます。 Teams Toolkit は、ローカル デバッグ中にサービスを開始するために追加した環境変数を読み込みます。

 > [!NOTE]
 > 環境変数はホット リロードをサポートしていないため、新しい環境変数を追加した後で新しいローカル デバッグを開始してください。

</details>

<details>
<summary><b>部分的なコンポーネントのデバッグ</b></summary>

Teams Toolkit は、Visual Studio Code マルチターゲット デバッグを利用して、タブ、ボット、メッセージ拡張機能、および Azure Functions を同時にデバッグします。 部分コンポーネントをデバッグするには、`.vscode/launch.json` と `.vscode/tasks.json` を更新できます。 タブとAzure Functions プロジェクトを含むボットでのみタブをデバッグする場合は、次の手順を使用します。

1. でデバッグ の複合を更新 `"Attach to Bot"` および `"Attach to Backend"` デバッグから取得します `.vscode/launch.json`。

   ```json
   {
       "name": "Debug (Edge)",
        "configurations": [
           "Attach to Frontend (Edge)",
           // "Attach to Bot",
           // "Attach to Backend""
           ],
           "preLaunchTask": "Pre Debug Check & Start All",
           "presentation": {
               "group": "all",
               "order": 1
           },
           "stopAll": true

   }
   ```

2. .vscode/tasks.json のすべてのタスクを更新 `"Start Backend"` して `"Start Bot"` 開始します。

   ```json
   {
                                           
       "label": "Start All",
       "dependsOn": [
           "Start Frontend",
             // "Start Backend",
             // "Start Bot"

         ]
              
   }
   ```

</details>

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [アプリをローカルでデバッグする](debug-local.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-teams-app-using-visual-studio"></a>Visual Studio を使用して Teams アプリをデバッグする

Teams Toolkit は、アプリのスタートアップ サービスを自動化し、デバッグを開始し、Teams アプリをサイドロードします。 デバッグ後、Teams Web クライアントで Teams アプリをプレビューできます。 また、ボット エンドポイントを使用するようにデバッグ設定をカスタマイズしたり、構成済みアプリを読み込むように環境変数をカスタマイズしたりできます。 Visual Studio では、タブ、ボット、メッセージ拡張機能をデバッグできます。 デバッグ プロセス中、Teams Toolkit では次のデバッグ機能がサポートされます。

* Teams アプリの依存関係を準備する
* デバッグの開始
* ブレークポイントの切り替え
* ホット リロード
* デバッグの停止

## <a name="prerequisites"></a>前提条件

| &nbsp; | インストール | 使用するには... |
| --- | --- | --- |
| &nbsp; | **必須** | &nbsp; |
| &nbsp; | Visual Studio 2022 バージョン 17.3 | Visual Studio のエンタープライズ エディションをインストールし、"ASP.NET" ワークロードと Microsoft Teams 開発ツールをインストールできます。 |
| &nbsp; | Teams ツールキット | アプリのプロジェクト スキャフォールディングを作成する Visual Studio 拡張機能。 最新バージョン​​を使用します。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams を使用して、チャット、会議、通話用のアプリを通じて共同作業を行うすべてのユーザーと 1 か所で共同作業を行うことができます。 |
| &nbsp; | [Microsoft 365 テナントを準備する](../concepts/build-and-test/prepare-your-o365-tenant.md) | アプリをインストールするための適切なアクセス許可を持つ Teams アカウントにアクセスします。 |
| &nbsp; | [Microsoft 365 開発者アカウント](/../concepts/build-and-test/prepare-your-o365-tenant) | アプリをインストールするための適切なアクセス許可を持つ Teams アカウントにアクセスします。 |
| &nbsp; | Azure Tools と [Microsoft Azure CLI](/cli/azure/install-azure-cli) | 保存されたデータにアクセスしたり、Azure で Teams アプリ用のクラウドベースのバックエンドをデプロイしたりするための Azure ツール。 |
|&nbsp;  | **Optional** | &nbsp; |
|&nbsp; |[Ngrok](https://ngrok.com/) | Ngrok は、Azure Bot Framework からローカル コンピューターに外部メッセージを転送するために使用されます。|

## <a name="key-features-of-teams-toolkit"></a>Teams Toolkit の主な機能

Teams ツールキットの次の主な機能を確認できます。これらは、Teams アプリのローカル デバッグ プロセスを自動化します。

### <a name="prepare-teams-app-dependencies"></a>Teams アプリの依存関係を準備する

Teams ツールキットは、ローカル デバッグの依存関係を準備し、アカウント内のテナントに Teams アプリを登録します。 ボット アプリとメッセージ拡張機能アプリの場合、Teams ツールキットはボットを登録して構成します。

### <a name="start-debugging"></a>デバッグの開始

デバッグは 1 回の操作で実行できます。**F5** キーを押してデバッグを開始します。 Teams ツールキットは、コードをビルドし、サービスを開始し、ブラウザーでアプリを起動します。

### <a name="toggle-breakpoints"></a>ブレークポイントの切り替え

タブ、ボット、メッセージ拡張機能、および Azure 関数のソース コードのブレークポイントを切り替えることができます。 ブレークポイントは、Web ブラウザーで Teams アプリを操作すると実行されます。
次の図は、ブレークポイントの切り替えを示しています。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="ローカル デバッグのブレークポイントの切り替え" lightbox="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png":::

### <a name="hot-reload"></a>ホット リロード

デバッグ中にソース コードの更新と保存を同時に実行するには、**[ホット リロード]** を選択して Teams アプリに変更を適用します。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload.png" alt-text="[ホット リロード] アイコンを選択する":::

ドロップダウンから **[ファイルの保存時にホット リロード]** オプションを選択して、自動ホット リロードを有効にします。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload-filesave.png" alt-text="[ファイルの保存時にホット リロード] を選択する":::
  
   > [!Tip]
   > デバッグ中の Visual Studio のホット リロード機能の詳細については、<https://aka.ms/teamsfx-vs-hotreload> にアクセスしてください。

### <a name="stop-debugging"></a>デバッグの停止

ローカル デバッグが完了したら、**[デバッグの停止]** を選択します。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Stopdebug.png" alt-text="[デバッグの停止] アイコンを選択する":::

## <a name="customize-debug-settings"></a>デバッグ設定をカスタマイズする

Teams アプリのデバッグ設定で、ボット エンドポイントを使用するようにカスタマイズして、環境変数を追加できます。

### <a name="use-your-bot-endpoint"></a>ボット エンドポイントを使用する

**.fx/configs/config.local.json** で siteEndpoint 構成をエンドポイントに設定できます。

```
"bot": {
    "siteEndpoint": "https://baidu.com"
}
```

### <a name="add-environment-variables"></a>環境変数の追加

**launchSettings.json** ファイルに **environmentVariables** を追加できます。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-environment-variables.png" alt-text="環境変数の追加":::

### <a name="launch-teams-app-as-a-web-app"></a>Teams アプリを Web アプリとして起動する

Teams クライアントで実行する代わりに、Teams アプリを Web アプリとして起動できます。

1. プロジェクトのソリューション エクスプローラー パネルで **[プロパティ]** > **[launchSettings.json]** を選択します。
1. ファイルから **'launchUrl'** を削除します。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="launchurl を削除してチームを Web アプリとして起動する" lightbox="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png":::

1. **[ソリューション**] を右クリックし、[**プロパティ**] を選択します。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="[ソリューション] を右クリックし、[プロパティ] を選択する" lightbox="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png":::

1. ダイアログ ボックスで [**構成プロパティ** > の **構成**] を選択します。
1. **[デプロイ]** チェック ボックスをオフにします。
1. **[OK]** をクリックします。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="構成プロパティでのデプロイをオフにする" lightbox="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png":::

::: zone-end

## <a name="see-also"></a>関連項目

* [バックグランド プロセスのデバッグ](debug-background-process.md)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [クラウドにデプロイする](deploy.md)
* [Teams アプリ マニフェストのプレビューとカスタマイズ](TeamsFx-preview-and-customize-app-manifest.md)
