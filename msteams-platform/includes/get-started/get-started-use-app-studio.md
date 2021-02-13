### <a name="use-app-studio-to-update-the-app-package"></a>App Studio を使用してアプリ パッケージを更新する

App Studio は、Teams ストアからインストールできる Teams アプリです。 アプリの作成と登録が簡素化されます。

Teams に App Studio をインストールするには、左側のバーの下部にある [アプリ] アイコンを選択し **、App Studio を検索します**。

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

App **Studio タイルを選択し** 、[インストール] を **選択します**。 App Studio がインストールされている。

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

[マニフェスト エディター **] タブを** 選択して、Teams アプリのアプリ パッケージを作成します。

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

サンプルには独自の事前に作成されたマニフェストが付属し、プロジェクトのビルド時にアプリ パッケージをビルドするように設計されています。 .NET では、これは Visual Studio で行われ、Node JS では、プロジェクトのルート ディレクトリにコマンド ラインで入力します `gulp` 。

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

生成されたアプリ パッケージの名前は **helloworldapp.zip。** 使用しているツールで場所がはっきりしない場合は、このファイルを検索できます。

このアプリ パッケージを変更するには、マニフェストエディターで [既存のアプリのインポート] タイル **を選択します**。

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

新しく **インポートしたアプリ** の Hello World タイルをクリックします。

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

次の図は、App Studio でインポートされたアプリ パッケージを示しています。

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

マニフェスト エディターの左側と右側には、各手順に入力する必要があるプロパティの一覧が表示されます。 サンプル アプリを使い始めてから、情報の多くが既に入力されています。次の手順では、まだ更新する必要があるパーツを変更する手順について説明します。

#### <a name="app-details"></a>アプリの詳細

[詳細] の *[アプリの詳細]* エントリを *クリックします*。 [生成] *ボタンを* クリックして、新しいアプリ ID を作成します。

新しいアプリ ID は次のように表示されます `2322041b-72bf-459d-b107-f4f335bc35bd` 。

右側のウィンドウでアプリの残りの詳細を確認し、開発者情報やブランド化などのエントリの一部を *理解します*。  これらのセクションは、配布用の新しいアプリを作成する場合に重要です。

#### <a name="capabilities-tabs"></a>機能: タブ

タブは、Teams アプリに追加する最も簡単な要素の 1 つです。 サンプル アプリは既に複数のタブをサポートしています。次のようにして有効にできます。

##### <a name="team-tab"></a>[チーム] タブ

アプリで使用できるチーム タブは 1 つのみです。

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

このサンプルでは、[チーム] タブが構成ページの場所です。 エントリの末尾 *にある ...* 記号をクリックし、ドロップダウンから *[* 編集] を選択します。 URL を、アプリをホストするときに上記で使用した URL に置き換える `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` 必要がある場所に変更します。

##### <a name="personal-tabs"></a>[個人] タブ

アプリには、チーム タブを含め、最大 16 のタブを含めできます。

[個人用] タブは、チーム タブとは異なる方法で表示されます。[Hello *Tab] が個人用タブ* の一覧に既に表示されている必要があります。 現時点では、プレースホルダー値が設定されます `com.contoso.helloworld.hellotab` 。 エントリの末尾 *にある ...* 記号をクリックし、ドロップダウンから *[* 編集] を選択します。 次のダイアログが表示されます。

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

アプリの URL で更新する必要があるフィールドが 2 つある。

- コンテンツ URL を次に変更する `https://yourteamsapp.ngrok.io/hello`
- Web サイトの URL を次に変更する `https://yourteamsapp.ngrok.io/hello`

アプリ `yourteamsapp.ngrok.io` をホストするときに上記で使用した URL に置き換える必要があります。

#### <a name="bots"></a>ボット

ボットは、アプリに機能を追加する最も一般的な方法です。 Hello World サンプルには、サンプルの一部としてボットが既に存在しますが、まだ Microsoft に登録されていません。

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

サンプルからインポートされたボットには、アプリ ID がまだ関連付けされていません。 App Studio で新しいアプリ ID を作成して Microsoft に登録するには、新しいボットを作成する必要があります。 これはボットのアプリ ID で、アプリ用に作成されたアプリ ID とは異なります。 アプリ内の各ボットには、独自のアプリ ID が必要です。

ボットの *一覧* で、インポートされたボット *の横にある* [削除] ボタンをクリックします。

表示するボットが残っていない。 [セットアップ *] をクリックします*。 これにより、[ボットの *セットアップ] ダイアログが表示* されます。

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

次のようなボット名を追加し、[スコープ] の下の `Contoso bot` 3 つすべてのボタンを **選択します**。

[ *ボットの作成] を* 選択してダイアログを終了します。 App Studio はボットを Microsoft に登録し、ボットの一覧に新しいボットを表示します。 メモ帳でテキスト ファイルを開き、新しいボット ID をコピーして貼り付けるのが良い方法です。 この ID は後で必要になります。

[ *新しいパスワードの* 生成] をクリックし、ボット アプリ ID をメモしたテキスト ファイルにパスワードをメモします。 パスワードが表示されるのは今回だけなので、この時点で確認してください。

Bot エンドポイント *のアドレスを更新* します。ここで、アプリをホストするときに上記で使用した URL に置き `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` 換える必要があります。

まだ保存していない場合は、テキスト ファイルを保存する良い時間です。 この情報は、このチュートリアルの後半でホストされるアプリに追加します。これにより、ボットとの安全な通信が可能になります。

#### <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージング拡張機能を使用すると、ユーザーはサービスから情報を求め、その情報をカードの形式でチャネルの会話に投稿できます。 メッセージング拡張機能は、作成ボックスの下部に表示されます。

App Studio **の左側の** 列にある **[機能** ] の下にある [メッセージング拡張機能] を選択して、メッセージング拡張機能を構成します。

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

サンプルのメッセージング拡張機能は、右側のウィンドウの [メッセージング拡張機能] の下 **に一覧表示されます**。 もう **一度 [** 削除] を選択してこのエントリを削除し、ボットの場合と同じ手順に従って [セットアップ] ボタンをクリックします。 これにより、[メッセージング拡張機能 *] ダイアログが表示* されます。

[既存 *のボットを使用する* ] タブを選択し、既存のボット *の 1 つから選択します*。 ドロップダウン メニューで、上記のセクションで作成したボットを選択します。 ボット名 *を追加し、[* 保存] *をクリックして* ダイアログを閉じます。

[コマンド] *セクションで* 、[追加] を *クリックします*。 検索ベースのコマンドを追加します。そのため、[サービスのクエリをユーザーに許可する *] オプションを選択* します。

[新しい **コマンド] ダイアログ** ボックスで、次の値を入力します。

[新 *しいコマンド] で、次のコマンドを実行します*。

- *コマンド ID*  = getRandomText
- *Title*       = 楽しいテキストをランダムに取得する
- *Description* = ランダムなテキストと画像を取得します

Under *Parameter*:

- *Name*        = cardTitle
- *Title*       = カード タイトル
- *説明* = 使用するカード タイトル

情報を入力したら、[保存] をクリック *して* ダイアログを閉じます。

#### <a name="register-your-app-in-teams"></a>Teams でアプリを登録する

これで、アプリの詳細の入力が完了しましたが、次の 2 つの手順が残っています。
1. App Studio の [テストと配布] セクションを使用して、Teams にアプリをインストールします。
1. ホストされたアプリケーションを、ボットのアプリ ID とパスワードで更新します。 このサンプルでは、ボットとメッセージング拡張機能の両方に同じアプリ ID とパスワードを使用する必要があります。

App Studio **の左側の列にある** **[完了** ] の下にある [テストと配布] 項目を選択します。

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

Teams にアプリをアップロードするには、[テストと配布] の下の [*インストール**] ボタンをクリックします*。

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

[チーム **に追加** ] セクションの [検索] ボックス **を選択し** 、サンプル アプリを追加するチームを選択します。 通常、テスト用に特別なチームをセットアップできます。

ダイアログの **下部** にある [インストール] ボタンを選択します。

これで、このチュートリアルの App Studio 部分が終了します。 Teams で実行されているアプリが表示されます。ただし、ホストされたアプリケーション環境を更新してアプリの ID とパスワードを確認するまで、ボットとメッセージング拡張機能は機能しません。

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
