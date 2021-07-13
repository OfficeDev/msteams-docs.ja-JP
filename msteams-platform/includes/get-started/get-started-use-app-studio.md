### <a name="use-app-studio-to-update-the-app-package"></a>App Studio を使用してアプリ パッケージを更新する

> [!TIP]
> **開発者ポータルを試してみてください**: App Studio はまもなく削除されます。 新しい開発者ポータルを使用して、Teamsアプリを構成、配布、[および管理します](https://dev.teams.microsoft.com/)。

App Studio は、TeamsストアからインストールできるアプリTeamsです。 アプリの作成と登録が簡略化されます。

アプリ パッケージを更新するには、次の手順を実行します。

1. App Studio を Teamsにインストールするには、左側のバーの下部にある [アプリ] アイコンを選択し **、App Studio を検索します**。

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. [App **Studio] タイルを選択し** 、[インストール] を **選択します**。 App Studio がインストールされています。

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. アプリのアプリ パッケージを作成するにはTeams App Studio の [**マニフェスト エディター]** タブ **を選択します**。

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>


    このサンプルには独自のマニフェストが付属し、プロジェクトのビルド時にアプリ パッケージをビルドするように設計されています。 .NET では、[マニフェスト] manifest.jsにある [マニフェスト] の [Visual Studioに配置できます ```Microsoft.Teams.Samples.HelloWorld.Web``` 。 このNode.js、プロジェクトのルート ディレクトリのコマンド ラインで `gulp` 入力します。

     このVisual Studio、manifest.jsファイルはマニフェストの下に **配置** されます `Microsoft.Teams.Samples.HelloWorld.Web` 。 この手順は、次の図で説明します。  
    
    <img  width="450px" alt="Build the app package on .NET with Visual Studio" src="~/assets/images/get-started/app-package-on-.NET-with-Visual-Studio.png"/>
    
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
    > アプリをサイドロードできない場合は、カスタム アプリのアップロードを有効 [にしたかどうかを確認します](#prepare-your-development-environment)。

1. [チームに **追加** ] セクションで **[検索] ボックスを選択** し、サンプル アプリを追加するチームを選択します。 テスト用に特別なチームを設定できます。
1. ダイアログ ボックス **の下部** にある [インストール] ボタンを選択します。

    アプリがアプリで使用Teams。 ただし、ボットとメッセージング拡張機能は、ホストされているアプリケーション環境をアプリの ID とパスワードで更新するまで機能しません。

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
