---
title: Teams アプリをデバッグする
author: surbhigupta
description: このモジュールでは、Teams Toolkit で Teams アプリをデバッグする方法と Teams Toolkit の主な機能について説明します
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 8545d4bbd97a6a4c5065c279368505f18dd5a14a
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617142"
---
# <a name="debug-your-microsoft-teams-app"></a>Microsoft Teams アプリをデバッグする

Microsoft Teams Toolkit は、Teams アプリのデバッグとプレビューに役立ちます。 デバッグは、Teams でプログラムが正常に実行されるように、問題やバグを確認、検出、修正するプロセスです。

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

Teams Toolkit は、デバッグ プロセス中にバックグラウンド機能を実行します。これには、デバッグに必要な前提条件の検証が含まれます。検証プロセスの進行状況は、Teams Toolkit の出力チャネルで確認できます。 セットアップ プロセスでは、Teams アプリを登録して構成できます。

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

Teams Toolkit を使用すると、いくつかの前提条件をオフにして、デバッグ設定をカスタマイズしてタブまたはボットを作成できます。

<br>

<details>
<summary><b>ボット エンドポイントを使用する</b></summary>

1. Visual Studio Code の設定で、[ **Ngrok のインストールと開始 (ngrok)]** をオフにする必要があります。

1. エンドポイントに`.fx/configs/config.local.json`構成を設定`siteEndpoint`できます。

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

1. Visual Studio Code の設定で、[ **開発証明書が信頼されていることを確認する (devCert)]** をオフにする必要があります。

1. 証明書ファイル パス`.fx/configs/config.local.json`と`sslKeyFile`キー ファイル パスに設定`sslCertFile`および構成できます。

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

1. タブでは、スクリプトを更新`dev:teamsfx``tabs/package.json`する必要があります。

1. ボットまたはメッセージ拡張機能の場合は、スクリプトを更新`dev:teamsfx``bot/package.json`する必要があります。

1. Azure Functionsでは、TypeScript 更新スクリプトと TypeScript 更新`dev:teamsfx`スクリプトの`api/package.json`スクリプトを更新`watch:teamsfx`する必要があります。

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

1. コメント **`Attach to Bot`** と **`Attach to Backend`** デバッグ の複合ファイル ( `.vscode/launch.json`.

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

2. .vscode/tasks.json のすべてのタスクの開始からボットをコメント **`Start Backend`** および開始します。

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

## <a name="see-also"></a>関連項目

* [バックグランド プロセスのデバッグ](debug-background-process.md)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [クラウドにデプロイする](deploy.md)
* [Teams アプリ マニフェストのプレビューとカスタマイズ](TeamsFx-preview-and-customize-app-manifest.md)
