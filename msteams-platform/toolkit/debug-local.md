---
title: Teams アプリをデバッグする
description: Teams Toolkit で Teams アプリをローカルでデバッグする
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: a41cbac6a0cee3f42a6de2d436c227c858347d4e
ms.sourcegitcommit: ff31cbe4840191f004d8fc61dd4fd93d35fcaecb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2022
ms.locfileid: "65938962"
---
# <a name="debug-your-teams-app-locally"></a>Teams アプリをローカルでデバッグする

Teams Toolkit は、Teams アプリをローカルでデバッグおよびプレビューするのに役立ちます。 デバッグとは、問題やバグをチェック、検出、修正して、プログラムが正常に実行されるようにするプロセスです。 Visual Studio Code では、タブ、ボット、メッセージ拡張機能、および Azure Functions をデバッグできます。 Teams Toolkit では、次のデバッグ機能がサポートされています:

* [デバッグの開始](#start-debugging)
* [マルチターゲット デバッグ](#multi-target-debugging)
* [ブレークポイントの切り替え](#toggle-breakpoints)
* [ホット リロード](#hot-reload)
* [デバッグの停止](#stop-debugging)  

デバッグ プロセス中に、Teams Toolkit は自動的にアプリ サービスを開始し、デバッガーを起動し、Teams アプリをサイドロードします。 Teams アプリは、デバッグ後にローカルの Teams Web クライアントでプレビューできます。 また、ボット エンドポイント、開発証明書、またはデバッグ部分コンポーネントを使用して構成済みアプリを読み込むデバッグ設定をカスタマイズすることもできます。

## <a name="prerequisite"></a>前提条件

[Teams Toolkit の最新バージョン](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)をインストールします。

## <a name="key-features-of-teams-toolkit"></a>Teams Toolkit の主な機能

次の一覧は、Teams Toolkit の主な機能を示しています。

### <a name="start-debugging"></a>デバッグの開始

1 回の操作を実行できます。**F5** キーを押してデバッグを開始します。 Teams Toolkit は、前提条件の確認を開始し、Azure AD アプリ、Teams アプリ、ボットを登録し、サービスを開始し、ブラウザーを起動します。

### <a name="multi-target-debugging"></a>マルチターゲット デバッグ

Teams Toolkit では、マルチターゲット デバッグ機能を利用して、タブ、ボット、メッセージ拡張機能、および Azure Functions を同時にデバッグします。

### <a name="toggle-breakpoints"></a>ブレークポイントの切り替え

タブ、ボット、メッセージ拡張機能、および Azure Functions のソース コードのブレークポイントを切り替えることができます。 ブレークポイントは、Web ブラウザーで Teams アプリを操作するときに実行されます。 次の図は、ブレークポイントの切り替えを示しています。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="ブレークポイントの切り替え":::

### <a name="hot-reload"></a>ホット リロード

Teams アプリをデバッグするときに、タブ、ボット、メッセージ拡張機能、および Azure Functions のソース コードを同時に更新して保存できます。 アプリが再読み込みされ、デバッガーがプログラミング言語に再アタッチされます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="ソース コードのホット リロード":::

### <a name="stop-debugging"></a>デバッグの停止

ローカル デバッグを完了すると、フローティング デバッグ ツール バーから **[停止]** または **[切断]** を選択して、すべてのデバッグ セッションを停止し、タスクを終了できます。次の図は、デバッグ操作の停止を示しています:

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="デバッグの停止":::

## <a name="debug-your-teams-app-locally"></a>Teams アプリをローカルでデバッグする

次の手順は、Teams アプリをローカルでデバッグするのに役立ちます。

### <a name="set-up-your-teams-toolkit"></a>Teams Toolkit を設定する

Teams Toolkit を使用して新しいアプリを作成した後、次の手順を実行してアプリをデバッグします:

# <a name="windows"></a>[Windows](#tab/Windows)

1. アクティビティ バーで **[Edge のデバッグ]** または **[Chrome デバッグ]** を **[実行とデバグ]** から選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="ブラウザー オプション" border="false":::

1. **[デバッグの開始 (F5)]** または **[実行]** を選択して、Teams アプリをデバッグ モードで実行します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="デバッグの開始" border="false":::

3. Microsoft 365 アカウントへ **[サインイン]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="サインイン" border="true":::

   > [!TIP]
   > Microsoft 365 開発者プログラムの詳細については **[詳細情報]** を選択してください。 既定の Web ブラウザーが開き、資格情報を使用して Microsoft 365 アカウントにサインインできます。

4. **[インストール]** を選択して localhost の開発証明書をインストールします。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="証明書" border="true":::

   > [!TIP]
   > 開発証明書について知るには **[詳細情報]** を選択できます。

5. 以下のダイアログが表示されたら、**[はい]** を選択します:

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="証明機関" border="true":::

ツールキットは、選択内容に基づいて新しい Edge または Chrome ブラウザー インスタンスを起動し、Teams クライアントを読み込む Web ページを開きます。  

# <a name="macos"></a>[macOS](#tab/macOS)

1. アクティビティ バーで **[Edge のデバッグ]** または **[Chrome デバッグ]** を **[実行とデバグ]** から選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="ブラウザー リスト" border="false":::

1. **[デバッグの開始 (F5)]** または **[実行]** を選択して、Teams アプリをデバッグ モードで実行します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="アプリのデバッグ" border="false":::

3. Microsoft 365 アカウントへ **[サインイン]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="M365 アカウントにサインイン" border="true":::

   > [!TIP]
   > Microsoft 365 開発者プログラムの詳細については **[詳細情報]** を選択してください。 既定の Web ブラウザーが開き、資格情報を使用して Microsoft 365 アカウントにサインインできます。

4. **[インストール]** を選択して localhost の開発証明書をインストールします。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="証明書" border="true":::

   > [!TIP]
   > 開発証明書について知るには **[詳細情報]** を選択できます。

5. **ユーザ名** と **パスワード** を入力し、次のダイアログ ボックスで **[設定の更新]** を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="Mac サインイン" border="true":::

ツールキットは、選択内容に応じて新しい Edge または Chrome ブラウザー インスタンスを起動し、Teams クライアントを読み込む Web ページを開きます。

---

### <a name="debug-your-app"></a>アプリのデバッグ

初期セットアップ プロセスの後、Teams Toolkit は次のプロセスを開始します:

<br>

<details>
<summary><b>アプリ サービスを開始</b></summary>

次のように、`.vscode/tasks.json` で定義されているタスクを実行します。

|  コンポーネント |  タスク名  | フォルダー |
| --- | --- | --- |
|  Tab |  **フロントエンドの開始** |  tabs |
|  ボットまたはメッセージ拡張機能 |  **ボットの開始** |  ボット |
|  Azure Functions |  **バックエンドの開始** |  API |

次の図は、タブ、ボット、メッセージ拡張機能、およびAzure Functionsの実行中に、Visual Studio Code の **[出力]** **[ターミナル]** タブにタスク名を表示します。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="アプリ サービスの開始":::

</details>
<details>
<summary><b>デバッガーを起動</b></summary>

`.vscode/launch.json` で定義されているデバッグ構成を次のように起動します。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="デバッガーの起動":::

次の表に、タブ アプリとボット アプリを含むプロジェクトのデバッグ構成名と種類を示します:

|  コンポーネント |  デバッグ構成名  | デバッグ構成の種類 |
| --- | --- | --- |
|  Tab |  **フロントエンド (Edge)** アタッチするか、または **フロントエンドにアタッチ (Chrome)** します  |  pwa-msedge または pwa-chrome  |
|  ボットまたはメッセージ拡張機能 |   **ボットにアタッチ** |  PWA ノード |
| Azure Functions |   **バックエンドにアタッチ** |  PWA ノード |

次の表に、ボット アプリとタブ アプリを使用しないプロジェクトのデバッグ構成名と種類を示します。

|  コンポーネント |  デバッグ構成名  | デバッグ構成の種類  |
| --- | --- | --- |
|  ボットまたはメッセージ拡張機能  | **ボット (Edge) を起動する** か、**ボット (Chrome) を起動する**  |   pwa-msedge または pwa-chrome  |
|  ボットまたはメッセージ拡張機能  |   **ボットにアタッチ** |  PWA ノード  |
|  Azure Functions |  **バックエンドにアタッチ** |  PWA ノード |

</details>
<details>
<summary><b>Teams アプリをサイドロード</b></summary>

構成 **フロントエンドにアタッチ**、または **立ち上げボット** を起動すると、新しい Edge または Chrome ブラウザー インスタンスが起動され、Teams クライアントを読み込む Web ページが開きます。 Teams クライアントが読み込まれた後、Teams は、[Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}) 起動構成で定義されているサイドローディング URL によって制御される Teams アプリをサイドロードします。  Teams クライアントが Web ブラウザーに読み込まれたら、**[追加]** を選択するか、要件に従ってドロップダウン リストから 1 つ選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="ローカル デバッグ" border="true":::

   アプリが Teams に追加されました。

</details>

## <a name="customize-debug-settings"></a>デバッグ設定をカスタマイズする

Teams Toolkit を使用すると、いくつかの前提条件をオフにして、デバッグ設定をカスタマイズしてタブまたはボットを作成できます。

<br>

<details>
<summary><b>ボット エンドポイントを使用する</b></summary>

1. [Visual Studio Codeの設定] で **[Ngrok がインストールされ、起動されていることを確認する (ngrok) ]** をオフにします。

1. `.fx/configs/config.local.json` で `siteEndpoint` の構成をエンドポイントに設定します。

```json
{
    "bot": {
        "siteEndpoint": "https://your-bot-tunneling-url"
    }
}

```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/bot-endpoint.png" alt-text="ボット エンドポイントのカスタマイズ":::

</details>

<details>
<summary><b>開発証明書を使用する</b></summary>

1. Visual Studio Code 設定で [**開発証明書が信頼されていることを確認する (devCert)**] をオフにします。

1. `.fx/configs/config.local.json` の `sslCertFile` と `sslKeyFile` の構成を、証明書ファイル パスとキー ファイル パスに設定します。

```json
{
    "frontend": {
        "sslCertFile": "",
        "sslKeyFile": ""
    }
}
```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate-customize.png" alt-text="証明書のカスタマイズ":::

</details>

<details>
<summary><b>開始スクリプトを使用して App Services を開始する</b></summary>

1. タブの場合は、`tabs/package.json` の `dev:teamsfx` スクリプトを更新します。

1. ボットまたはメッセージ拡張機能の場合は、`bot/package.json` で `dev:teamsfx` スクリプトを更新します。

1. Azure Functions の場合は、`api/package.json` の `dev:teamsfx` スクリプトと TypeScript 更新 `watch:teamsfx` スクリプトを更新します。

   > [!NOTE]
   > 現時点では、タブ、ボット、メッセージ拡張機能アプリ、Azure Functions ポートはカスタマイズをサポートしていません。

</details>

<details>
<summary><b>環境変数の追加</b></summary>

タブ、ボット、メッセージ拡張機能、および Azure Functions の `.env.teamsfx.local` ファイルに環境変数を追加できます。 Teams Toolkit は、ローカル デバッグ中にサービスを開始するために追加した環境変数を読み込みます。

 > [!NOTE]
 > 環境変数がホット リロードをサポートしていないため、新しい環境変数を追加した後は、新しいローカル デバッグを開始するようにします。

</details>

<details>
<summary><b>部分的なコンポーネントのデバッグ</b></summary>

Teams Toolkit は、Visual Studio Code マルチターゲット デバッグを利用して、タブ、ボット、メッセージ拡張機能、および Azure Functions を同時にデバッグします。 部分コンポーネントをデバッグするには、`.vscode/launch.json` と `.vscode/tasks.json` を更新できます。 タブとAzure Functions プロジェクトを含むボットでのみタブをデバッグする場合は、次の手順を使用します。

1. コメント **[Bot にアタッチ]** し、`.vscode/launch.json` のデバッグ複合から **[バックエンドにアタッチ]**。

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

2. コメント **[バックエンドを起動]** と .vscode/tasks.json の [すべてのタスクを起動] から [ボットを起動]。

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

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [バックグランド プロセスをデバッグします](debug-background-process.md)。

## <a name="see-also"></a>関連項目

* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリに機能を追加する](add-capability.md)
* [クラウドにデプロイする](deploy.md)
* [Teams Toolkit で複数の環境を管理する](TeamsFx-multi-env.md)
