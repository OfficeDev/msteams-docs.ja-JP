---
title: App Studio でアプリを使用してNode.jsを展開する
description: App Studio でアプリを使用Microsoft TeamsアプリをNode.jsする方法について学習する
keywords: アプリ スタジオnode.js開始する
ms.custom: scenarios:getting-started; languages:ASP,Node.js
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: ea6e85f2552504cdb98959ef8ab585f9afa90e6f
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2021
ms.locfileid: "60721259"
---
# <a name="update-nodejs-app-package-in-app-studio"></a>App Studio Node.jsアプリ パッケージを更新する

> [!TIP]
> **開発者ポータルを試してみてください**: App Studio が進化しました。 新しい開発者ポータルを使用して、Teamsアプリを構成、配布、[および管理します](https://dev.teams.microsoft.com/)。

App Studio は、TeamsストアからインストールできるアプリTeamsです。 アプリの作成と登録が簡略化されます。

アプリ パッケージを更新するには、次の手順を実行します。

1. App Studio を Teamsにインストールするには、左側のバーの下部にある [アプリ] アイコンを選択し **、App Studio を検索します**。

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. [App **Studio] タイルを選択し** 、[インストール] を **選択します**。 App Studio がインストールされています。

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. アプリのアプリ パッケージを作成するにはTeams App Studio の [**マニフェスト エディター]** タブ **を選択します**。

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    このサンプルには独自のマニフェストが付属し、プロジェクトのビルド時にアプリ パッケージをビルドするように設計されています。 このNode.js、プロジェクトのルート ディレクトリのコマンド ラインで `gulp` 入力します。

    プロジェクトのルート ディレクトリのコマンド Node.js入力して、アプリ パッケージをビルド `gulp` できます。

    ```bash
    $ gulp
    [13:39:27] Using gulpfile ~\documents\github\msteams-samples-hello-world-nodejs\gulpfile.js
    [13:39:27] Starting 'clean'...
    [13:39:27] Starting 'generate-manifest'...
    [13:39:27] Finished 'generate-manifest' after 11 ms
    [13:39:27] Finished 'clean' after 21 ms
    [13:39:27] Starting 'default'...
    Build completed. Output in manifest folder
    [13:39:27] Finished 'default' after 62 μs
    ```

    生成されたアプリ パッケージの名前は次 **helloworldapp.zip。** 使用しているツールで場所がクリアされていない場合は、このファイルを検索できます。

1. 次に、このアプリ パッケージを変更するには、[マニフェスト エディター] で **[既存の** アプリのインポート] **を選択します**。

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. 新しく **インポートしたアプリの** Hello World タイルを選択します。

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

    次の図は、App Studio でインポートされたアプリ パッケージを示しています。

    <img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

    マニフェスト エディターの左側には、手順の一覧があります。 右側には、各手順で入力する必要があるプロパティの一覧があります。 サンプル アプリの使用を開始すると、多くの情報が既に完了しています。 次の手順では、Hello World アプリのプロパティを更新できます。

#### <a name="app-details"></a>アプリの詳細

[詳細 **] で [アプリの** 詳細] **を選択します**。 [生成] **ボタンを** 選択して、新しいアプリ ID を作成します。

新しいアプリ ID はに似ています `2322041b-72bf-459d-b107-f4f335bc35bd` 。

開発者情報やブランドの詳細など、右側のウィンドウでアプリの **詳細を確認** します。 これらの詳細は、配布用の新しいアプリを作成する場合に重要です。

#### <a name="tabs"></a>タブ

アプリにタブを追加Teamsです。 サンプル アプリは既に複数のタブをサポートし、有効にできます。

##### <a name="team-tab"></a>[チーム] タブ

アプリで使用できるチーム タブは次の 1 つのみです。

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

このサンプルでは、[チーム] タブに構成ページが表示されます。 タブ構成 **URL の ...** 記号 **を選択** し、ドロップダウン メニューから **[編集** ] を選択します。 URL を、アプリのホスト時に使用した URL に置き換える `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` 必要がある場所に変更します。

##### <a name="personal-tabs"></a>[個人] タブ

アプリには、[チーム] タブを含む最大 16 のタブを含め、16 つまで使用できます。

個人用タブは、[チーム] タブとは異なります **。Hello Tab** は、プレースホルダー値を持つ個人用タブリストに既に一覧表示されています `com.contoso.helloworld.hellotab` 。 タブ構成 **URL の ...** 記号 **を選択** し、ドロップダウン メニューから **[編集** ] を選択します。 次のダイアログ ボックスが表示されます。

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

アプリの URL で次のボックスを更新します。

- [コンテンツ **の URL] ボックスを** に変更する `https://yourteamsapp.ngrok.io/hello`
- [Web サイト **の URL] ボックスをに** 変更する `https://yourteamsapp.ngrok.io/hello`

アプリ `yourteamsapp.ngrok.io` をホストするときに使用した URL に置き換える。

#### <a name="bots"></a>ボット

ボット機能をアプリに簡単に追加できます。 **Hello World サンプル** アプリには、サンプルの一部としてボットが既に存在しますが、Microsoft に登録する必要があります。

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

サンプルからインポートされたボットには、関連付けられたアプリ ID が含まれません。 App Studio で新しいアプリ ID を作成して Microsoft に登録するには、新しいボットを作成する必要があります。

> [!NOTE]
> ボットの App Studio によって作成されたアプリ ID は、アプリ用に作成されたアプリ ID とは異なります。 アプリ内の各ボットには、独自のアプリ ID が必要です。

ボットをセットアップするには、次の手順を実行します。

1. ボットリスト **の** インポートされたボットの横にある [削除] を選択します。 これで、表示するボットは残りはありません。 
1. [ **セットアップ] を** 選択して 、[ **ボットのセットアップ] ダイアログ ボックスを** 表示します。

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. Contoso ボットのボット名 **を追加し** 、[スコープ] で 3 つのチェック ボックスをオン **にします**。
1. [保存 **] を** 選択してダイアログ ボックスを終了します。 App Studio は、ボットを Microsoft に登録し、ボットリストに新しいボットを表示します。 
1. 次に、メモ帳でテキスト ファイルを開き、新しいボット ID をコピーして貼り付けます。
1. [ **新しいパスワードの生成]** をクリックし、ボット アプリ ID をメモしたのと同じテキスト ファイルにパスワードをメモします。
1. ボット エンドポイント **のアドレスを更新し** 、アプリのホスト時に使用した `https://yourteamsapp.ngrok.io/api/messages` URL `yourteamsapp.ngrok.io` に置き換える。
1. 次に、ボットとの安全な通信を可能にするために、ファイルからホストされたアプリに情報を追加する必要があるテキスト ファイルを保存します。

#### <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージング拡張機能を使用すると、ユーザーはサービスから情報を求め、その情報を投稿できます。 情報は、カードの形式でチャネル会話に投稿されます。 メッセージング拡張機能は、作成ボックスの下部に表示されます。

メッセージング拡張機能をセットアップするには、次の手順を実行します。

1. App Studio **の左側の** ウィンドウで [ **機能]** の下にある [メッセージング拡張機能] を選択して、メッセージング拡張機能を構成します。

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    サンプル メッセージング拡張機能は、[メッセージング拡張機能] ウィンドウ **に一覧表示** されます。

1. [ **削除] を** 選択してメッセージング拡張機能を削除し、[ **セットアップ**] を選択し、ボットに使用する手順と同じ手順 [を実行します](#bots)。 [ **メッセージング拡張機能] ダイアログ** ボックスが表示されます。
1. [既存の **ボットを使用する] タブを** 選択し、 **既存のボットの 1 つから選択します**。
1. ドロップダウン メニューから作成したボットを選択します。 ボット名 **を追加し、[** 保存] **を選択して** ダイアログ ボックスを閉じます。
1. [コマンド] **セクションで** 、[追加] を **選択します**。 検索ベースのコマンドを追加するには、[ユーザーがサービスに情報をクエリしてメッセージに挿入する] **オプションを選択** します。
1. [新しい **コマンド] ダイアログ** ボックスで、次の値を入力します。

    [新 **しいコマンド] で次のコマンドを実行します**。

    - **コマンド ID**: ランダム テキストを入力する
    - **Title**: ランダムなタイトルを入力する
    - **説明**: ランダムな説明を入力する

    [パラメーター **] の下**:

    - **名前**: パラメーター名を入力します。
    - **タイトル**: カードタイトルを入力する
    - **説明**: カードの説明を入力する

1. 情報を入力した後、[保存] **を選択して** ダイアログ ボックスを閉じます。

#### <a name="register-your-app-in-teams"></a>アプリをアプリに登録Teams

アプリの詳細を入力したら、次の手順を実行してアプリをアプリに登録Teams。

1. App **Studio のテストと配布** を使用して、アプリをアプリにインストールTeams。 
1. ボットのアプリ ID とパスワードを使用してホストされたアプリケーションを更新します。 サンプル アプリでは、ボットとメッセージング拡張機能の両方に同じアプリ ID とパスワードを使用します。 
1. App Studio **の左側のウィンドウ****で 、[完了]** で [テストと配布] を選択します。

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. アプリをアプリにアップロードするには、[テストTeams配布] の [**インストール**]**ボタンを選択します**。

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

    > [!NOTE]
    > アプリをサイドロードできない場合は、カスタム アプリのアップロードを有効 [にしたかどうかを確認します](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option)。

1. [チームに **追加** ] セクションで **[検索] ボックスを選択** し、サンプル アプリを追加するチームを選択します。 テスト用に特別なチームを設定できます。
1. ダイアログ ボックス **の下部** にある [インストール] ボタンを選択します。

    アプリがアプリで使用Teams。 ただし、ボットとメッセージング拡張機能は、ホストされているアプリケーション環境をアプリの ID とパスワードで更新するまで機能しません。

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>

## <a name="update-the-credentials-for-your-hosted-app"></a>ホストされたアプリの資格情報を更新する

サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

環境変数は環境の一部です。 アプリのコードだけがアクセスできます。 第三者に公開されることはありません。

ngrok を使用してアプリを実行している場合は、ローカル環境変数を設定する必要があります。 次のコマンドをVisual Studio Code起動構成[を追加できます](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)。

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

ここで、

- ボットの認証資格情報は次のとおりです。
  - MICROSOFT_APP_ID is ID
  - MICROSOFT_APP_PASSWORDパスワード
- NODE_DEBUGデバッグ コンソールでボットで何が起こっているかをVisual Studio Codeする
- NODE_CONFIG_DIRリポジトリのルートにあるディレクトリをポイントします (既定では、アプリをローカルで実行すると、フォルダー内のルート ディレクトリが検索 `src` されます)。

> [!Note]
> チュートリアルの前のバージョンから npm を停止していない場合は、起動構成変数を正しく取得Visual Studio Code実行 `npm stop` する必要があります。

<a name="ConfigureTheAppTab"></a>

## <a name="test-the-app-capabilities-in-teams"></a>アプリの機能をテストTeams

アプリをアプリにインストールした後Teamsコンテンツを表示するために構成する必要があります。

### <a name="test-your-tab-in-teams"></a>タブをテストTeams

1. 新しいタブを追加するには、Teamsのチャネルに移動し **、[+]** ボタンを選択します。
1. 次に、[タブ `Hello World` の追加 **] リストから選択** できます。
1. 構成ダイアログで、チャネルに表示するタブを選択します。 次に、[保存] **を選択します**。 

選択したタブが `Hello World` 読み込まれたタブを確認できます。

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>ボットをテストTeams

これで、ボットと対話できます。Teams。 アプリを登録したチーム内のチャネルを選択し、「」と入力し `@your-bot-name` 、その後にメッセージを入力します。 この種類のメッセージはメンションと呼 **\@ ばれる。** ボットに送信するメッセージは、返信として返されます。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

**メッセージング拡張機能をテストするには**
1. 会話ビューの入力ボックスの下にある 3 つのドットを選択します。 「Hello **World」アプリを含むメニュー** が表示されます。
1. メニューを選択します。 ランダムなテキストのセットが表示されます。 ランダムなテキストの 1 つを選択し、会話に挿入できます。

    <img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. ランダムなテキストのいずれかを選択します。 書式設定されたカードは、下部に独自のメッセージが含まれて送信できる状態で表示されます。

    <img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />


| &nbsp; | &nbsp; |
|:--- | ---:|
|[Back](get-started-overview.md) | &nbsp; |
|