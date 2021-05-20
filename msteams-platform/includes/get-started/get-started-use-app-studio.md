### <a name="use-app-studio-to-update-the-app-package"></a>アプリのスタジオを使用してアプリ パッケージを更新する

アプリスタジオは、TeamsストアからインストールできるTeamsアプリです。 これにより、アプリの作成と登録が簡素化されます。

アプリ パッケージを更新するには、次の手順を実行します。

1. Teamsでアプリスタジオをインストールするには、左側のバーの下部にある **[アプリ**]アイコンを選択し **、App Studioを** 検索します。

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. **[アプリケーションスタジオ]** タイルを選択し、[**インストール**] を選択します。 アプリスタジオがインストールされています。

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. Teams アプリのアプリ パッケージを作成するには、**アプリ スタジオ** の **[マニフェスト エディター** ] タブを選択します。

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    このサンプルには独自のマニフェストが付属しており、プロジェクトのビルド時にアプリ パッケージをビルドするように設計されています。 NET では、これはVisual Studioで行われ、Node.jsプロジェクト `gulp` のルート ディレクトリのコマンド ラインで入力します。

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

    生成されたアプリ パッケージの名前は **helloworldapp.zip** です。 使用しているツールで場所が明確でない場合は、このファイルを検索できます。

1. ここで、このアプリ パッケージを変更するには、[**マニフェスト エディター** で **既存のアプリをインポート** する] を選択します。

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. 新しくインポートしたアプリの **Hello World** タイルを選択します。

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

次の図は、App Studio でインポートされたアプリ パッケージを示しています。

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

マニフェスト エディターの左側には、手順の一覧があります。 右側には、各ステップに入力する必要があるプロパティのリストがあります。 サンプル アプリを使用すると、情報の多くが既に完了しています。 次の手順では、Hello World アプリのプロパティを更新できます。

#### <a name="app-details"></a>アプリの詳細

[詳細 **] の** [アプリの **詳細]** を選択します。 [ **生成** ] ボタンを選択して、新しいアプリ ID を作成します。

新しいアプリ ID は `2322041b-72bf-459d-b107-f4f335bc35bd` 、 と似ています。

右側のウィンドウで、 **開発者情報** や **ブランドの** 詳細を含むアプリの詳細を確認します。 配布用の新しいアプリを作成する場合は、これらの詳細が重要です。

#### <a name="tabs"></a>タブ

Teamsアプリにタブを追加するのは簡単です。 サンプル アプリでは、既にいくつかのタブがサポートされており、有効にすることができます。

##### <a name="team-tab"></a>[チーム] タブ

アプリには、チーム タブを 1 つだけ持つことができます。

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

このサンプルでは、[チーム] タブが構成ページの表示場所です。 **タブ構成 URL** の **..** 記号を選択し、ドロップダウン メニューから **[編集]** を選択します。 URL を `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` [、アプリのホスティング](#host-the-sample-app)時に使用した URL に置き換える必要がある場所に変更します。

##### <a name="personal-tabs"></a>[個人] タブ

アプリには、[チーム] タブを含めて最大 16 個のタブを設定できます。

[個人] タブは [チーム] タブとは異 **なります。** `com.contoso.helloworld.hellotab` **タブ構成 URL** の **..** 記号を選択し、ドロップダウン メニューから **[編集]** を選択します。 次のダイアログ ボックスが表示されます。

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

アプリの URL で次のボックスを更新します。

- **[コンテンツ URL]** ボックスを`https://yourteamsapp.ngrok.io/hello`
- **[Web サイトの URL]** ボックスを`https://yourteamsapp.ngrok.io/hello`

`yourteamsapp.ngrok.io`アプリをホストするときに使用した URL で置き換えます。

#### <a name="bots"></a>ボット

ボット機能をアプリに簡単に追加できます。 **Hello World** サンプル アプリには、サンプルの一部としてボットが既に含まれていますが、マイクロソフトに登録する必要があります。

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

サンプルからインポートされたボットには、関連付けられたアプリ ID がありません。 アプリ スタジオが新しいアプリ ID を作成してマイクロソフトに登録できるように、新しいボットを作成する必要があります。

> [!NOTE]
> アプリスタジオによってボット用に作成されたアプリ ID は、アプリ用に作成されたアプリ ID とは異なります。 アプリの各ボットには、独自のアプリ ID が必要です。

ボットを設定するには、次の手順を実行します。

1. ボットリストでインポートしたボットの横にある **[削除** ] を選択します。 今、表示するボットは残っていません。 
1. [ **設定]** を選択して [ **ボットの設定** ] ダイアログ ボックスを表示します。

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. ボット名 **Contoso ボット** を追加し、[ **スコープ**] の下の 3 つのチェック ボックスをすべてオンにします。
1. [ **保存] を** 選択してダイアログ ボックスを閉じます。 アプリスタジオは、ボットをマイクロソフトに登録し、ボットリストに新しいボットを表示します。 
1. 次に、メモ帳でテキスト ファイルを開き、新しいボット ID をコピーして貼り付けます。
1. [ **新しいパスワードの生成**] をクリックし、ボットアプリ ID にメモしたのと同じテキスト ファイルにパスワードを書き留めます。
1. Bot **エンドポイントアドレス** を `https://yourteamsapp.ngrok.io/api/messages` に更新し、 `yourteamsapp.ngrok.io` アプリをホストするときに使用した URL に置き換えます。
1. ここで、ボットとの安全な通信を可能にするために、ファイルの情報をホストされたアプリに追加する必要がある場合は、テキスト ファイルを保存します。

#### <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージング拡張機能を使用すると、ユーザーはサービスから情報を要求し、その情報を投稿できます。 情報はカードの形でチャンネル会話に投稿されます。 メッセージ拡張機能は、作成ボックスの下部に表示されます。

メッセージング拡張機能をセットアップするには、次の手順を実行します。

1. App Studio の左側のペインにある **[機能**] で [**メッセージング** 拡張機能] を選択して、メッセージング拡張機能を構成します。

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    サンプルのメッセージング拡張機能は、[ **メッセージング拡張機能** ] ウィンドウに一覧表示されます。

1. [ **削除]** を選択してメッセージング拡張機能を削除し、[ **セットアップ**] を選択して [、ボット](#bots)で使用する手順と同じ手順に従います。 [ **メッセージング拡張機能** ] ダイアログ ボックスが表示されます。
1. [ **既存のボットを使用** ] タブと [ **既存のボットの 1 つから選択]** を選択します。
1. ドロップダウンメニューから作成したボットを選択します。 **ボット名** を追加し、[**保存]** を選択してダイアログ ボックスを閉じます。
1. [ **コマンド** ] セクションで、[ **追加**] を選択します。 検索ベースのコマンドを追加するには、[ **ユーザーがサービスに情報を照会し、それをメッセージに挿入できるようにする]** オプションを選択します。
1. [ **新規コマンド** ]ダイアログ ボックスで、次の値を入力します。

    新規 **コマンド** の下:

    - **コマンド ID**: ランダムテキストを入力します
    - **タイトル**: ランダムなタイトルを入力します
    - **説明**: ランダムな説明を入力します

    パラメータの下 **で**:

    - **名前**: パラメータ名を入力します。
    - **タイトル**: カードタイトルを入力します。
    - **説明**: カードの説明を入力します

1. 情報を入力したら、[ **保存]** を選択してダイアログ ボックスを閉じます。

#### <a name="register-your-app-in-teams"></a>アプリをTeamsに登録する

アプリの詳細を入力したら、次の手順を実行して、Teamsにアプリを登録します。

1. アプリスタジオの **テストと配布** を使用して、Teamsでアプリをインストールします。 
1. ボットのアプリ ID とパスワードでホストアプリケーションを更新します。 サンプル アプリでは、ボットとメッセージングの両方の拡張機能に同じアプリ ID とパスワードを使用します。 
1. [ **テスト] を選択し、App**  Studio の左側のウィンドウで **[完了** ] の下で配布します。

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. アプリをTeamsにアップロードするには、[**テストと配布**] の [**インストール**] ボタンを選択します。

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. [**チームに追加**] セクションの **[検索**] ボックスを選択し、サンプル アプリを追加するチームを選択します。 テスト用の特別なチームを設定できます。
1. ダイアログボックスの下部にある **[インストール** ]ボタンを選択します。

アプリがTeamsで利用可能になりました。 ただし、アプリ ID とパスワードでホストされたアプリケーション環境を更新するまで、ボットとメッセージング拡張機能は機能しません。

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
