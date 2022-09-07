---
title: Teams アプリをローカルでデバッグする
author: surbhigupta
description: このモジュールでは、Teams Toolkit と Teams Toolkit の主な機能で Teams アプリをローカルでデバッグする方法について説明します
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 68999351232deb60015259840147d2a1ab55681a
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616567"
---
# <a name="debug-your-microsoft-teams-app-locally"></a>Microsoft Teams アプリをローカルでデバッグする

Microsoft Teams Toolkit は、Teams アプリをローカルでデバッグおよびプレビューするのに役立ちます。 デバッグ プロセス中、Teams Toolkit は自動的にアプリ サービスを開始し、デバッガーを起動し、Teams アプリをサイドロードします。 デバッグ後、Teams Web クライアントで Teams アプリをローカルでプレビューできます。 アプリをデバッグする前に、Teams Toolkit を設定する必要があります。

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

## <a name="see-also"></a>関連項目

* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリに機能を追加する](add-capability.md)
* [クラウドにデプロイする](deploy.md)
* [Teams Toolkit で複数の環境を管理する](TeamsFx-multi-env.md)
