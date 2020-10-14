### <a name="use-app-studio-to-update-the-app-package"></a>アプリ Studio を使用してアプリパッケージを更新する

App Studio は teams アプリで、Teams ストアからインストールできます。 これにより、アプリの作成と登録が簡単になります。

Teams にアプリ Studio をインストールするには、左側のバーの下部にあるアプリストアアイコンをクリックして、アプリ Studio を検索します。

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

アプリ Studio のタイルを見つけたら、それをクリックして、ポップアップしたダイアログの [ *インストール* ] を選択します。

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

アプリ Studio がインストールされたら、[マニフェストエディター] タブをクリックして、Teams アプリのアプリパッケージの作成を開始します。

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

このサンプルには独自のマニフェストが用意されており、プロジェクトのビルド時にアプリパッケージを構築するように設計されています。 .NET では、これは Visual Studio とノード JS で行われます。これは、 `gulp` プロジェクトのルートディレクトリのコマンドラインで入力することによって行われます。

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

生成されたアプリパッケージの名前は *helloworldapp.zip*。 このファイルは、使用しているツールで場所が明確でない場合に検索できます。

このチュートリアルの次の部分では、マニフェストエディターの [既存のアプリタイルを *インポート* する] を選択して、このアプリパッケージを変更します。

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

アプリパッケージがインポートされると、アプリ Studio は次のようになります。

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

新しくインポートしたアプリ [ *Hello World*] のタイルをクリックします。

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

マニフェストエディターの左側に手順の一覧があり、それぞれの手順で入力する必要があるプロパティの一覧が右側に表示されています。 サンプルアプリの使用を開始したので、情報の多くは既に入力されています。次の手順では、更新が必要なパーツを変更する方法について説明します。

#### <a name="app-details"></a>アプリの詳細

[*詳細*] の下にある*アプリの詳細*エントリをクリックします。 [ *生成* ] ボタンをクリックして、新しいアプリ id を作成します。

新しいアプリ id は、次のようになり `2322041b-72bf-459d-b107-f4f335bc35bd` ます。

右側のウィンドウに表示されるアプリの詳細を確認して、 *開発者情報* や *ブランド*化などのエントリを理解してください。 これらのセクションは、配布用の新しいアプリを作成する場合に重要です。

#### <a name="capabilities-tabs"></a>機能: タブ

タブは Teams アプリに追加する最も簡単な要素の1つです。 サンプルアプリでは、複数のタブが既にサポートされており、それらを次のように有効にすることができます。

##### <a name="team-tab"></a>[チーム] タブ

アプリには、チームタブを1つだけ含めることができます。

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

この例では、[チーム] タブで構成ページが移動されます。 エントリの最後にある [. *..* ] 記号をクリックし、ドロップダウンから [ *編集* ] を選択します。 アプリをホストする `https://yourteamsapp.ngrok.io/configure` ときに上で使用した url で url を変更し `yourteamsapp.ngrok.io` ます。

##### <a name="personal-tabs"></a>[個人] タブ

アプリは、[チーム] タブを含む最大16個のタブを持つことができます。

個人用タブは、[チーム] タブとは異なる方法で表示されます。[個人用タブ] ボックスの一覧に [ *Hello Tab]* が表示されています。 その時点で、プレースホルダーの値があり `com.contoso.helloworld.hellotab` ます。 エントリの最後にある [. *..* ] 記号をクリックし、ドロップダウンから [ *編集* ] を選択します。 次のダイアログが表示されます。

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

アプリの URL で更新する必要があるフィールドは2つあります。

- コンテンツの URL をに変更 `https://yourteamsapp.ngrok.io/hello`
- Web サイトの URL をに変更する `https://yourteamsapp.ngrok.io/hello`

`yourteamsapp.ngrok.io`は、アプリをホストするときに上で使用した URL に置き換える必要があります。

#### <a name="bots"></a>ボット

Bot は、アプリに機能を追加する最も一般的な方法です。 Hello world サンプルには、このサンプルの一部として既に bot がありますが、Microsoft に登録されていません。

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

サンプルからインポートされた bot には、まだ関連付けられているアプリ ID がありません。 新しい bot を作成して、アプリ Studio が新しいアプリ ID を作成して Microsoft に登録できるようにする必要があります。 これは bot のアプリ ID であり、前の手順でアプリに対して作成したアプリ ID とは異なります。 アプリ内の各 bot は、独自のアプリ ID を必要とします。

Bot リストでインポートされた*bot*の横にある [*削除*] ボタンをクリックします。

これで、表示する bot がなくなりました。 [ *セットアップ*] をクリックします。 これにより、[ *bot の設定* ] ダイアログボックスが表示されます。

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

のような bot 名を追加 `Contoso bot` し、[ *scope*] の下にある3つのボタンすべてを選択します。

[ *ボットの作成* ] を選択してダイアログを終了します。 アプリ Studio は、ボットを Microsoft に登録するのに時間を費やして、bot リストに新しい bot を表示する必要があります。 これで、メモ帳でテキストファイルを開いて、新しい bot id をコピーして貼り付けるのはよい時間になります。 この id は後で必要になります。

[ *新しいパスワードの生成*] をクリックして、の BOT アプリ ID にメモしたものと同じテキストファイル内のパスワードをメモしておきます。 これは、パスワードが表示される唯一の時間なので、必ずこれを実行してください。

*Bot エンドポイントアドレス*をに更新し `https://yourteamsapp.ngrok.io/api/messages` ます。では、 `yourteamsapp.ngrok.io` アプリをホストするときに上で使用した URL で置き換える必要があります。

まだ実行していない場合は、テキストファイルを保存するのに適した時間になります。 この情報をホストされたアプリに追加します。このチュートリアルでは、後で bot とのセキュリティで保護された通信を許可します。

#### <a name="messaging-extensions"></a>メッセージングの拡張機能

メッセージング拡張機能を使用すると、ユーザーはサービスから情報を求め、カード形式でその情報をチャネル会話に直接送信できます。 メッセージング拡張機能は、[新規作成] ボックスの下部に表示されます。

App Studio の左側の列にある [*機能*] の [*メッセージング拡張*] をクリックして、メッセージング拡張機能の構成を開始します。

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

[ *メッセージング拡張*] の下の右側のウィンドウに、サンプルのメッセージング拡張機能が一覧表示されます。 [ *削除* ] をもう一度クリックしてこのエントリを削除し、次に [ *セットアップ] ボタン* をクリックして、bot をフォローしたときと同じ手順を実行します。 これにより、[ *メッセージングの内線番号* ] ダイアログボックスが表示されます。

[ *既存の bot を使用* ] タブを選択して、 *既存のボットのいずれかを選択*します。 ドロップダウンメニューで、上のセクションで作成した bot を選択します。 *Bot 名*を追加し、[*保存*] をクリックしてダイアログを閉じます。

[ *コマンド* ] セクションで、[ *追加*] をクリックします。 検索ベースのコマンドを追加しています。そのため、[ *ユーザーによるサービスのクエリを許可する* ] オプションを選択します。

[ *新しいコマンド* ] ダイアログボックスで、次の値を入力します。

[ *新規作成] コマンド*:

- *コマンド ID*  = Ge/domtext
- *Title*       = 楽しいテキストを取得する
- *Description* = ランダムなテキストとイメージを取得する

[ *パラメーター*]:

- *Name*        = cardtitle
- *タイトル*       = カードのタイトル
- *Description* = 使用するカードのタイトル

情報を入力したら、[ *保存* ] をクリックしてダイアログを閉じます。

#### <a name="register-your-app-in-teams"></a>Teams にアプリを登録する

アプリの詳細の入力が完了しましたが、2つの手順は残っています。 最初に、アプリを Teams にインストールするには、App Studio の [テストと配布] セクションを使用する必要があります。その後、ホストされたアプリケーションを bot のアプリ ID とパスワードで更新する必要があります。 このサンプルでは、ボットと messaging 拡張機能の両方で同じアプリ ID とパスワードを使用することが想定されています。

App Studio の左側の列にある [ *テスト] を* クリックし、[ *完了* ] の下にあるアイテムを配布します。

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

アプリを Teams にアップロードするために、[*テストおよび配布*] の下にある [*インストール*] ボタンをクリックします。

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

[*チームに追加*] セクションの [*検索*] ボックスをクリックして、サンプルアプリを追加するチームを選択します。 通常は、テストのために特別なチームをセットアップする必要があります。

ダイアログの下部にある [ *Install* ] ボタンをクリックします。

これで、このチュートリアルの App Studio の部分が完成します。 アプリが Teams で実行中であることが表示されるようになりましたが、ボットとメッセージング拡張機能は、ホストされているアプリケーションの環境を更新して、アプリ Id とパスワードが何かを知るまでは機能しません。

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
