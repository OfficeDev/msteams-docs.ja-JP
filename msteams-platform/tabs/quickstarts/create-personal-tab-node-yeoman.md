---
title: 'クイック スタート: Node.js と Microsoft Teams 用の Yeoman ジェネレーターを使用してカスタム 個人用タブを作成します。'
author: laujan
description: Microsoft Teams用の Yeoman ジェネレーターを使用して個人用タブを作成するためのクイック スタート ガイドです。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 88ad05aacaed69d695bc918e3e8a44ec18e560ae
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566609"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Node.jsとヨーマンジェネレータを使用してカスタムパーソナルタブを作成Microsoft Teams

>[!NOTE]
>このクイック スタートは、Microsoft OfficeDev GitHub リポジトリにある[最初のMicrosoft Teams アプリ](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)Wiki で説明されている手順に従います。

このクイック スタートでは[、yeoman ジェネレーターを使用](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)してカスタム パーソナル タブを作成するTeamsを示します。 アプリケーションはチームにアップロードします。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**構成可能または静的なタブを作成する**

矢印キーを使用して、静的タブを選択します。

>[!IMPORTANT]
>このクイック スタートで参照されているパス コンポーネント *の DefaultTabNameTab* は、ジェネレータで *[既定のタブ名]* に入力した値 *と、Tab* という語を使用して入力した値です。
>
>たとえば、デフォルトタブ名:*マイタブ*  =>  */マイタブタブ/*

## <a name="create-your-personal-tab"></a>個人用タブを作成する

このアプリケーションに個人用タブを追加するには、コンテンツ ページを作成し、既存のファイルを更新します。

- コード エディターで、新しい HTML ファイルを作成 **し、l をpersonal.htm** し、次のマークアップを追加します。

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

- **アプリケーションpersonal.htm** **Web** フォルダに保存します。

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- コード エディター **でmanifest.js** を開きます。

    ```bash
    ./src/manifest/manifest.json/
    ```

空の配列 ( ) に次の値を `staticTabs` `staticTabs":[]` 追加し、次の JSON オブジェクトを追加します。

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

**「コンテンツ URL」** パスコンポーネントを実際の **タブ** 名で更新してください。

- 更新された **manifest.jsを に** 保存します。

- コンテンツ ページは IFrame で提供される必要があります。 コード エディターで **Tab.ts** を開きます。

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- IFrame デコレータの一覧に次の項目を追加します。

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- 更新された **Tab.ts** ファイルを保存してください。 タブ コードが完成しました。

## <a name="build-and-run-your-application"></a>アプリケーションのビルドと実行

プロジェクト ディレクトリでコマンド プロンプトを開き、次のタスクを完了します。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

個人用タブを表示するには、 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![個人用タブのスクリーンショット](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへの安全なトンネルを確立する

Microsoft Teamsは完全にクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからタブ コンテンツを利用できるようにする必要があります。 Teamsローカル ホスティングを許可しないため、タブをパブリック URL に公開するか、インターネットに接続する URL にローカル ポートを公開するプロキシを使用する必要があります。

タブ拡張をテストするには、このアプリケーションに組み込まれている [ngrok](https://ngrok.com/docs)を使用します。 Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行されている Web サーバーの一般に公開されている HTTPS エンドポイントへのトンネルを作成します。 サーバーの Web エンドポイントは、ローカル コンピューター上の現在のセッション中に使用できます。 マシンがシャットダウンまたはスリープ状態になると、サービスは利用できなくなります。

コマンド プロンプトで localhost を終了し、次のように入力します。

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが Microsoft チームに **ngrok** 経由でアップロードされ、正常に保存された後、トンネル セッションが終了するまで、Teamsで表示できます。

## <a name="upload-your-application-to-teams"></a>アプリケーションをTeamsにアップロードする

- Microsoft Teams クライアントを開きます。 Web ベースの [バージョン](https://teams.microsoft.com) を使用する場合は、ブラウザーの [開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンド コードを検査できます。
- 左側の **[YourTeams]** パネルで、 `...` タブのテストに使用しているチームの横にあるメニューを選択し、[ **チームの管理**]を選択します。
- メインパネルでタブバーから **「アプリ**」を選択し、ページの右下隅にある **カスタムアプリアップロード** 選択します。
- プロジェクト ディレクトリを開き **、./package** フォルダを参照し、zip フォルダを選択して右クリックし、[ **開く**] を選択します。 タブがTeamsにアップロードされます。

## <a name="view-your-personal-tabs"></a>個人用タブを表示する

Teamsクライアントの左端にあるナビゲーションバーで、メニューを選択 `...` し、リストからアプリを選択します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ASP.NETCore を使用して個人用タブを作成する](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
