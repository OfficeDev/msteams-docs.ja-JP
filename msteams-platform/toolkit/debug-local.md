---
title: Teams アプリをローカルでデバッグする
author: surbhigupta
description: このモジュールでは、Teams Toolkit と Teams Toolkit の主な機能で Teams アプリをローカルでデバッグする方法について説明します
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 5aeaba2248306d8f638ed2529dac964d96ffaea5
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780866"
---
# <a name="debug-your-microsoft-teams-app-locally"></a>Microsoft Teams アプリをローカルでデバッグする

Teams Toolkit は、Teams アプリをローカルでデバッグおよびプレビューするのに役立ちます。 デバッグ プロセス中、Teams Toolkit は自動的にアプリ サービスを開始し、デバッガーを起動し、Teams アプリをサイドロードします。 デバッグ後、Teams Web クライアントで Teams アプリをローカルでプレビューできます。

::: zone pivot="visual-studio-code"

## <a name="debug-your-microsoft-teams-app-locally-for-visual-studio-code"></a>Visual Studio Code 用に Microsoft Teams アプリをローカルでデバッグする

Visual Studio Code の Teams Toolkit では、Teams アプリのデバッグをローカルで自動化する機能が提供されます。 Visual Studio では、タブ、ボット、メッセージ拡張機能をデバッグできます。 アプリをデバッグする前に、Teams Toolkit を設定する必要があります。

## <a name="set-up-your-teams-toolkit-for-debugging"></a>デバッグ用に Teams Toolkit を設定する

次の手順は、デバッグ プロセスを開始する前に Teams Toolkit を設定するのに役立ちます。

# <a name="windows"></a>[Windows](#tab/Windows)

1. **[RUN AND** DEBUG] ドロップダウンからアクティビティ バーの [デバッグ **(Edge)]** または [**デバッグ (Chrome)]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="ブラウザー オプション":::

1. [**Run Start Debugging (F5)]\(デバッグの開始を実行** > \) を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="デバッグの開始":::

3. Microsoft 365 アカウントへ **[サインイン]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="サインイン":::

   > [!TIP]
   > Microsoft 365 開発者プログラムの詳細については **[詳細情報]** を選択してください。 既定の Web ブラウザーが開き、資格情報を使用して Microsoft 365 アカウントにサインインできます。

4. **[インストール]** を選択して localhost の開発証明書をインストールします。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="証明書":::

   > [!TIP]
   > 開発証明書について知るには **[詳細情報]** を選択できます。

5. [**セキュリティ警告**] ダイアログ ボックスに **[はい**] を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="証明機関":::

ツールキットは、選択内容に基づいて新しい Edge または Chrome ブラウザー インスタンスを起動し、Teams クライアントを読み込む Web ページを開きます。  

# <a name="macos"></a>[macOS](#tab/macOS)

1. **[RUN AND** DEBUG] ドロップダウンから [**Debug Edge**] または [**Debug Chrome**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="ブラウザー リスト":::

1. **[デバッグの開始 (F5)]** または **[実行]** を選択して、Teams アプリをデバッグ モードで実行します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="アプリのデバッグ":::

3. Microsoft 365 アカウントへ **[サインイン]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="M365 アカウントにサインイン":::

   > [!TIP]
   > Microsoft 365 開発者プログラムの詳細については **[詳細情報]** を選択してください。 既定の Web ブラウザーが開き、資格情報を使用して Microsoft 365 アカウントにサインインできます。

4. **[インストール]** を選択して localhost の開発証明書をインストールします。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="証明書":::

   > [!TIP]
   > 開発証明書について知るには **[詳細情報]** を選択できます。

5. **ユーザー名** と **パスワード** を入力し、[**更新設定]** を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="Mac サインイン":::

Teams Toolkit によってブラウザー インスタンスが起動され、Teams クライアントを読み込む Web ページが開きます。

---

## <a name="debug-your-app"></a>アプリのデバッグ

初期セットアップ プロセスの後、Teams Toolkit は次のプロセスを開始します。

* [アプリ サービスを開始](#starts-app-services)
* [デバッグ構成を起動します](#launches-debug-configurations)
* [Teams アプリをサイドロード](#sideloads-the-teams-app)

### <a name="starts-app-services"></a>アプリ サービスを開始します

で定義されているタスクを `.vscode/tasks.json`実行します。

|  コンポーネント |  タスク名  | フォルダー |
| --- | --- | --- |
|  Tab |  **フロントエンドの開始** |  tabs |
|  ボットまたはメッセージ拡張機能 |  **ボットの開始** |  ボット |
|  Azure Functions |  **バックエンドの開始** |  API |

次の図は、タブ、ボットまたはメッセージ拡張機能、およびAzure Functionsの実行中に、Visual Studio Code の **[OUTPUT**] タブと **[ターミナル**] タブにタスク名を表示します。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="アプリ サービスの開始":::

### <a name="launches-debug-configurations"></a>デバッグ構成を起動します

で `.vscode/launch.json`定義されているデバッグ構成を起動します。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="デバッガーの起動":::

次の表に、タブ、ボット、メッセージ拡張機能アプリ、およびAzure Functionsを含むプロジェクトのデバッグ構成名と種類を示します。

|  コンポーネント |  デバッグ構成名  | デバッグ構成の種類 |
| --- | --- | --- |
|  Tab |  **フロントエンド (Edge)** アタッチするか、または **フロントエンドにアタッチ (Chrome)** します  |  pwa-msedge または pwa-chrome  |
|  ボットまたはメッセージ拡張機能 |   **ボットにアタッチ** |  PWA ノード |
| Azure Functions |   **バックエンドにアタッチ** |  PWA ノード |

次の表に、ボット アプリを使用したプロジェクトのデバッグ構成名と種類の一覧を示します。Azure Functionsタブ アプリはありません。

|  コンポーネント |  デバッグ構成名  | デバッグ構成の種類  |
| --- | --- | --- |
|  ボットまたはメッセージ拡張機能  | **ボット (Edge) を起動する** か、**ボット (Chrome) を起動する**  |   pwa-msedge または pwa-chrome  |
|  ボットまたはメッセージ拡張機能  |   **ボットにアタッチ** |  PWA ノード  |
|  Azure Functions |  **バックエンドにアタッチ** |  PWA ノード |

### <a name="sideloads-the-teams-app"></a>Teams アプリをサイドロードする

[ **フロントエンドにアタッチ]** または **[起動ボット]** の構成では、Edge ブラウザーまたは Chrome ブラウザー インスタンスを起動して、Teams クライアントを Web ページに読み込みます。 Teams クライアントが読み込まれた後、Teams は、起動構成 Microsoft Teams で定義されたサイドローディング URL によって制御される Teams アプリをサイドロード [します](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint})。 Teams クライアントが Web ブラウザーに読み込まれたら、要件に従ってドロップダウンから [ **追加]** を選択するか、オプションを選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="ローカル デバッグを追加する" lightbox="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png":::

   アプリが Teams に追加されました。

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [バックグランド プロセスのデバッグ](debug-background-process.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-microsoft-teams-app-locally-using-visual-studio"></a>Visual Studio を使用して Microsoft Teams アプリをローカルでデバッグする

Teams ツールキットは、Microsoft Teams アプリをローカルでデバッグおよびプレビューするのに役立ちます。 Visual Studio では、タブ、ボット、メッセージ拡張機能をデバッグできます。 Teams ツールキットを使用して、Visual Studio でアプリをローカルにデバッグできます。これを行うには、次の操作を実行します。

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Ngrok を設定する (ボットとメッセージ拡張機能アプリの場合のみ)

コマンド プロンプトを使用して、次のコマンドを実行します。

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>Teams Toolkit を設定する

プロジェクトを作成した後、Teams ツールキットを使用して次の手順を実行して、アプリをデバッグします。

1. **プロジェクト** を右クリックします。
1. **Teams Toolkit** >  の [**Teams アプリの依存関係の準備] を選択します**。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="ローカル デバッグ用の Teams アプリの依存関係" lightbox="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png":::

   > [!NOTE]
   > このシナリオでは、プロジェクト名は MyTeamsApp1 です

   サインインする前に、Microsoft 365 アカウントにサイド ローディングのアクセス許可が必要です。  Teams アプリをテナントにアップロードできることを確認します。これを行わないと、Teams アプリが Teams クライアントで実行できない場合があります。

1. **Microsoft 365 アカウント** にサインインし、[**続行**] を選択します。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="Microsoft 365 アカウントにサインインする":::

   > [!Note]
   > サイドローディングのアクセス許可の詳細については、<https://aka.ms/teamsfx-sideloading-option> にアクセスしてください。

1. [ **デバッグ** > **開始デバッグ]** を選択するか、 **F5** を直接選択します。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="デバッグの開始":::

   Visual Studio がブラウザーの Microsoft Teams クライアント内で Teams アプリを起動します。

   > [!Note]
   > 詳細については、<https://aka.ms/teamsfx-vs-debug> にアクセスしてください。

1. Microsoft Teams が読み込まれたら、**[追加]** を選択して Teams にアプリをインストールします。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="[追加] を選択してアプリを読み込む":::

   > [!TIP]
   > デバッグ中に Visual Studio のホット リロード機能を使用することもできます。 詳細については、<https://aka.ms/teamsfx-vs-hotreload> にアクセスしてください。

   > [!NOTE]
   > 通知ボット アプリをデバッグするときは、通知をトリガーするために必ず HTTP 要求を '<http://localhost:5130/api/notification>' に投稿してください。 プロジェクトの作成時に HTTP トリガーを選択した場合、curl (Windows コマンド プロンプト)、Postman などの任意の API ツールを使用できます。

   > [!TIP]
   > Teams アプリ マニフェスト ファイル (/templates/appPackage/manifest.template.json) に変更を加える場合、Teams アプリの依存関係を準備するコマンドを必ず実行してください。 Teams アプリをローカルで再度実行する前に実行します。

::: zone-end

## <a name="see-also"></a>関連項目

* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリに機能を追加する](add-capability.md)
* [クラウドにデプロイする](deploy.md)
* [Teams Toolkit で複数の環境を管理する](TeamsFx-multi-env.md)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)
* [Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)
