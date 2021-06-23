---
title: 'クイック スタート: カスタム 個人用タブを作成し、Node.js Yeoman Generator を使用Microsoft Teams'
author: surbhigupta
description: Yeoman Generator を使用して個人用タブを作成するクイック スタート Microsoft Teams。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 220d1018f174fc935a10311723a730ebc74ccc33
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069198"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>カスタム 個人用タブを作成するには、Node.js と Yeoman Generator を使用Microsoft Teams

>[!NOTE]
>このクイック スタートは、Microsoft OfficeDev Microsoft Teams リポジトリにあるビルド Your First [Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) App Wiki で説明されている手順にGitHubします。

このクイック スタートでは[、Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)ジェネレーターを使用してカスタム個人用タブを作成Teams説明します。 また、アプリケーションをチームにアップロードします。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**構成可能なタブまたは静的タブを作成する**

矢印キーを使用して静的タブを選択します。

>[!IMPORTANT]
>このクイック スタートで参照されるパス コンポーネント *yourDefaultTabNameTab* は、[既定のタブ名] のジェネレーターに入力した値に Tab という単語を加 *えた値です*。
>
>例: DefaultTabName: *MyTab*  =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>個人用タブを作成する

このアプリケーションに個人用タブを追加するには、コンテンツ ページを作成し、既存のファイルを更新します。

- コード エディターで、新しい HTML ファイルを作成し、lpersonal.htm **次** のマークアップを追加します。

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

- アプリケーション **personal.htmの Web** フォルダーに l を **保存** します。

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- コード **manifest.jsで[** オン] を開きます。

    ```bash
    ./src/manifest/manifest.json/
    ```

空の配列 ( ) に次を `staticTabs` 追加 `staticTabs":[]` し、次の JSON オブジェクトを追加します。

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

**"contentURL" パス コンポーネント** **yourDefaultTabNameTab** を実際のタブ名で更新してください。

- 更新されたファイルを **manifest.jsします**。

- コンテンツ ページは IFrame で提供する必要があります。 コード **エディターで Tab.ts** を開きます。

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- IFrame デコレータの一覧に次の項目を追加します。

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- 更新された **Tab.ts ファイルを保存してください** 。 タブ コードが完成しました。

## <a name="build-and-run-your-application"></a>アプリケーションのビルドと実行

プロジェクト ディレクトリでコマンド プロンプトを開き、次のタスクを完了します。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

個人用タブを表示するには、 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![個人用タブのスクリーンショット](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

Microsoft Teams完全にクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。 Teamsローカル ホスティングは許可されていないので、タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。

タブ拡張機能をテストするには、このアプリケーションに組み込まれる [ngrok](https://ngrok.com/docs)を使用します。 Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。 サーバーの Web エンドポイントは、ローカル コンピューター上の現在のセッション中に利用できます。 コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。

コマンド プロンプトで localhost を終了し、次のコマンドを入力します。

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが **ngrok** 経由で Microsoft チームにアップロードされ、正常に保存された後、トンネル セッションが終了するまで、Teamsで表示できます。

## <a name="upload-your-application-to-teams"></a>アップロードを使用してアプリケーションをTeams

- クライアントを開Microsoft Teamsします。 Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。
- 左側の **[YourTeams]** パネルで、タブのテストに使用するチームの横にあるメニューを選択し、[チームの管理 `...` ] **を選択します**。
- メイン パネルでタブ バーから **[** アプリ]を選択しアップロードの右下隅にあるカスタム アプリを選択します。
- プロジェクト ディレクトリを開き **、./package** フォルダーを参照し、zip フォルダーを選択して右クリックし、[開く] を選択 **します**。 タブがアプリにアップロードTeams。

## <a name="view-your-personal-tabs"></a>個人用タブを表示する

クライアントの左上にあるナビゲーション バーでTeamsメニューを選択し、一覧から `...` アプリを選択します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ASP.NETCore を使用して個人用タブを作成する](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
