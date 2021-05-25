---
title: カスタム チャネルとグループ タブを作成し、Node.jsの Yeoman Generator を使用Microsoft Teams
author: laujan
description: Yeoman Generator を使用してチャネルとグループ タブを作成するクイック スタート Microsoft Teams。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 70b1dbe5a5abafa44ddbdf9045c55a33cf8fcb20
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630246"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>カスタム チャネルとグループ タブを作成するには、Node.js と Yeoman Generator を使用Microsoft Teams

>[!NOTE]
>このクイック スタートは、Microsoft OfficeDev Microsoft Teams リポジトリにあるビルド Your First [Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) App Wiki で説明されている手順にGitHubします。

このクイック スタートでは[、Yeoman](https://github.com/OfficeDev/generator-teams/)ジェネレーターを使用してカスタム チャネルとグループ タブを作成Teams説明します。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**構成可能なタブまたは静的タブを作成しますか?**

矢印キーを使用して、構成可能なタブを選択します。

**Tab に使用するスコープは何ですか?**

チームチャットまたはグループ チャットを選択できます

**このタブをオンラインで使用SharePointしますか?(Y/n)** 

**[n] を選択します**。

>[!IMPORTANT]
>このクイック スタートで参照されるパス コンポーネント **yourDefaultTabNameTab** は、[既定のタブ名] のジェネレーターに入力した値に Tab という単語を加 **えた値です**。
>
>例: DefaultTabName: **MyTab**  =>  **/MyTabTab/**

プロジェクト ディレクトリで、次の場所に移動します。

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

そこで、タブ ロジックを見つける必要があります。 メソッドを `render()` 見つけて、コンテナー コードの上部に `<div>` 次のタグとコンテンツを `<PanelBody>` 追加します。

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

更新されたファイルを保存してください。

## <a name="build-and-run-your-application"></a>アプリケーションのビルドと実行

プロジェクト ディレクトリでコマンド プロンプトを開き、次のタスクを完了します。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

タブ構成ページを表示するには、 に移動します `https://localhost:3007/<yourDefaultAppNameTab>/config.html` 。 以下のように表示されます。

![構成ページのスクリーンショット](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

Microsoft Teams完全にクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。 Teamsローカル ホスティングは許可されていないので、タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。

タブ拡張機能をテストするには、このアプリケーションに組み込まれる [ngrok](https://ngrok.com/docs)を使用します。 Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。 サーバーの Web エンドポイントは、ローカル コンピューター上の現在のセッション中に利用できます。 コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。

コマンド プロンプトで localhost を終了し、次のコマンドを入力します。

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが Microsoft チームにアップロードされ、正常に保存された後は、タブ ギャラリーでタブを表示し、タブ バーに追加し、ngrok トンネル セッションが終了するまで操作できます。 ngrok セッションを再起動する場合は、新しい URL でアプリを更新する必要があります。

## <a name="upload-your-application-to-teams"></a>アップロードを使用してアプリケーションをTeams

- クライアントを開Microsoft Teamsします。 Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。
- 左側の *[YourTeams]* パネルで、タブのテストに使用するチームの横にあるメニューを選択し、[チームの管理 `...` ] **を選択します**。
- メイン パネルでタブ バーから **[** アプリ]を選択しアップロードの右下隅にあるカスタム アプリを選択します。
- プロジェクト ディレクトリを開き **、./package** フォルダーを参照し、アプリ パッケージの zip フォルダーを選択し、[開く] を選択 **します**。 タブがアプリにアップロードTeams。
- チームに戻り、タブを表示するチャネルを選択し、タブ バーから [➕] を選択し、ギャラリーからタブを選択します。
- タブを追加するには、指示に従います。チャネル/グループ タブのカスタム構成ダイアログがあります。
- [ **保存]** を選択すると、タブがチャネルのタブ バーに追加されます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ASP.NETCore を使用してカスタム チャネルとグループ タブを作成する](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)
