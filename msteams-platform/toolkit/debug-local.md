---
title: Teams アプリをローカルでデバッグする
author: surbhigupta
description: このモジュールでは、Teams Toolkit と Teams Toolkit の主な機能で Teams アプリをローカルでデバッグする方法について説明します
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 65eb9599bb60b35448aaf1b6239fc155b7d397d5
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791574"
---
# <a name="debug-your-teams-app-locally"></a>Teams アプリをローカルでデバッグする

Teams ツールキットは、Microsoft Teams アプリをローカルでデバッグおよびプレビューするのに役立ちます。 デバッグ プロセス中に、Teams Toolkit によってアプリ サービスが自動的に開始され、デバッガーが起動され、Teams アプリがサイドロードされます。 デバッグ後、Teams Web クライアントで Teams アプリをローカルでプレビューできます。

::: zone pivot="visual-studio-code"

## <a name="debug-your-microsoft-teams-app-locally-for-visual-studio-code"></a>Visual Studio Code 用に Microsoft Teams アプリをローカルでデバッグする

Visual Studio Code の Teams Toolkit では、Teams アプリのデバッグをローカルで自動化する機能が提供されます。 Visual Studio では、タブ、ボット、メッセージ拡張機能をデバッグできます。 アプリをデバッグする前に、Teams Toolkit を設定する必要があります。

> [!NOTE]
>
> 古い Teams Toolkit プロジェクトをアップグレードして新しいタスクを使用できます。詳細については、「[デバッグ設定のドキュメント](https://aka.ms/teamsfx-debug-upgrade-new-tasks)」を参照してください

## <a name="set-up-your-teams-toolkit-for-debugging"></a>デバッグ用に Teams ツールキットを設定する

次の手順は、デバッグ プロセスを開始する前に Teams Toolkit を設定するのに役立ちます。

# <a name="windows"></a>[Windows](#tab/Windows)

1. [**RUN AND DEBUG ▷** ] ドロップダウンから、アクティビティ バーで [デバッグ **(Edge)]** または [**デバッグ (Chrome)]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="ブラウザー オプション":::

1. [**デバッグ****の開始の** 実行  >  ] (F5) を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="デバッグの開始":::

3. Microsoft 365 アカウントへ **[サインイン]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="サインイン":::

   > [!TIP]
   > Microsoft 365 開発者プログラムの詳細については **[詳細情報]** を選択してください。 既定の Web ブラウザーが開き、資格情報を使用して Microsoft 365 アカウントにサインインできます。

4. **[インストール]** を選択して localhost の開発証明書をインストールします。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="証明書":::

   > [!TIP]
   > 開発証明書について知るには **[詳細情報]** を選択できます。

5. [**セキュリティ警告**] ダイアログ ボックスに [**はい] を** 選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="証明機関":::

ツールキットは、選択内容に基づいて新しい Edge または Chrome ブラウザー インスタンスを起動し、Teams クライアントを読み込む Web ページを開きます。  

# <a name="macos"></a>[macOS](#tab/macOS)

1. [**RUN AND DEBUG ▷** ] ドロップダウンから [**デバッグ エッジ**] または [**デバッグ Chrome**] を選択します。

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

5. **[ユーザー名]** と **[パスワード**] を入力し、[**設定の更新**] を選択します。

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

次の図は、タブ、ボットまたはメッセージ拡張機能、およびAzure Functionsの実行中に、Visual Studio Code の **OUTPUT** タブと **TERMINAL** タブにタスク名を表示しています。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal1.png" alt-text="アプリ サービスの開始" lightbox="../assets/images/teams-toolkit-v2/debug/Terminal1.png":::

### <a name="launches-debug-configurations"></a>デバッグ構成を起動します

で `.vscode/launch.json`定義されているデバッグ構成を起動します。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="デバッガーの起動":::

次の表に、タブ、ボットまたはメッセージ拡張機能アプリ、およびAzure Functionsを含むプロジェクトのデバッグ構成の名前と種類を示します。

|  コンポーネント |  デバッグ構成名  | デバッグ構成の種類 |
| --- | --- | --- |
|  Tab |  **フロントエンド (Edge)** アタッチするか、または **フロントエンドにアタッチ (Chrome)** します  |  pwa-msedge または pwa-chrome  |
|  ボットまたはメッセージ拡張機能 |   **ボットにアタッチ** |  PWA ノード |
| Azure Functions |   **バックエンドにアタッチ** |  PWA ノード |

次の表に、ボット アプリ、Azure Functions、タブ アプリを使用しないプロジェクトのデバッグ構成の名前と種類を示します。

|  コンポーネント |  デバッグ構成名  | デバッグ構成の種類  |
| --- | --- | --- |
|  ボットまたはメッセージ拡張機能  | **ボット (Edge) を起動する** か、**ボット (Chrome) を起動する**  |   pwa-msedge または pwa-chrome  |
|  ボットまたはメッセージ拡張機能  |   **ボットにアタッチ** |  PWA ノード  |
|  Azure Functions |  **バックエンドにアタッチ** |  PWA ノード |

### <a name="sideloads-the-teams-app"></a>Teams アプリをサイドロードする

[ **フロントエンドにアタッチ]** または **[ボットの起動]** 構成では、Web ページで Teams クライアントを読み込むための Edge または Chrome ブラウザー インスタンスが起動します。 Teams クライアントが読み込まれた後、Teams は、起動構成 [Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}) で定義されているサイドローディング URL によって制御される Teams アプリをサイドロードします。 Teams クライアントが Web ブラウザーに読み込まれたら、[ **追加]** を選択するか、要件に従ってドロップダウンからオプションを選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="ローカル デバッグを追加する" lightbox="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png":::

   アプリが Teams に追加されました。

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [バックグランド プロセスのデバッグ](debug-background-process.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-teams-app-locally-using-visual-studio"></a>Visual Studio を使用して Teams アプリをローカルでデバッグする

Teams ツールキットは、Microsoft Teams アプリをローカルでデバッグおよびプレビューするのに役立ちます。 Visual Studio では、タブ、ボット、メッセージ拡張機能をデバッグできます。 Teams ツールキットを使用して、Visual Studio でアプリをローカルにデバッグできます。これを行うには、次の操作を実行します。

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Ngrok を設定する (ボットとメッセージ拡張機能アプリの場合のみ)

コマンド プロンプトを使用して、次のコマンドを実行します。

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>Teams Toolkit を設定する

プロジェクトを作成した後、Teams ツールキットを使用して次の手順を実行して、アプリをデバッグします。

1. **プロジェクト** を右クリックします。
1. [ **Teams Toolkit** > **] [Teams アプリの依存関係の準備] の順に選択します**。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="ローカル デバッグ用の Teams アプリの依存関係" lightbox="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png":::

   > [!NOTE]
   > このシナリオでは、プロジェクト名は MyTeamsApp1 です

   サインインする前に、Microsoft 365 アカウントにサイド ローディングのアクセス許可が必要です。  Teams アプリをテナントにアップロードできることを確認します。これを行わないと、Teams アプリが Teams クライアントで実行できない場合があります。

1. **Microsoft 365 アカウント** にサインインし、[続行] を選択 **します**

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="Microsoft 365 アカウントにサインインする":::

   > [!Note]
   > サイドローディングのアクセス許可の詳細については、<https://aka.ms/teamsfx-sideloading-option> にアクセスしてください。

1. [ **デバッグ** > **] [デバッグの開始] の順に** 選択するか、 **F5** を直接選択します。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="デバッグの開始":::

   Visual Studio がブラウザーの Microsoft Teams クライアント内で Teams アプリを起動します。

   > [!Note]
   > 詳細については、<https://aka.ms/teamsfx-vs-debug> にアクセスしてください。

1. Microsoft Teams が読み込まれたら、**[追加]** を選択して Teams にアプリをインストールします。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="[追加] を選択してアプリを読み込む":::

   > [!TIP]
   > デバッグ中に Visual Studio のホット リロード機能を使用することもできます。 詳細については、<https://aka.ms/teamsfx-vs-hotreload> にアクセスしてください。

   > [!NOTE]
   > 通知ボット アプリをデバッグするときに、通知を `http://localhost:5130/api/notification` トリガーする HTTP 要求を に投稿してください。 プロジェクトの作成時に HTTP トリガーを選択した場合、curl (Windows コマンド プロンプト)、Postman などの任意の API ツールを使用できます。

   > [!TIP]
   > Teams アプリ マニフェスト ファイル (/templates/appPackage/manifest.template.json) に変更を加える場合、Teams アプリの依存関係を準備するコマンドを必ず実行してください。 Teams アプリをローカルで再度実行する前に実行します。

::: zone-end

## <a name="see-also"></a>関連項目

* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリに機能を追加する](add-capability.md)
* [クラウドにデプロイする](deploy.md)
* [Teams Toolkit で複数の環境を管理する](TeamsFx-multi-env.md)
