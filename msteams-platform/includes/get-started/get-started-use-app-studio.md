### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="91dec-101">アプリ Studio を使用してアプリパッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="91dec-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="91dec-102">App Studio は teams アプリで、Teams ストアからインストールできます。</span><span class="sxs-lookup"><span data-stu-id="91dec-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="91dec-103">これにより、アプリの作成と登録が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="91dec-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="91dec-104">Teams にアプリ Studio をインストールするには、左側のバーの下部にあるアプリストアアイコンをクリックして、アプリ Studio を検索します。</span><span class="sxs-lookup"><span data-stu-id="91dec-104">To install App Studio in Teams, click on the app store icon at the bottom of the left hand bar, and search for App Studio.</span></span>

<img  width="450px" title="ストア内のアプリ Studio の検索" src="~/assets/images/get-started/app-studio-store.png"/>

<span data-ttu-id="91dec-106">アプリ Studio のタイルを見つけたら、それをクリックして、ポップアップしたダイアログの [*インストール*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="91dec-106">Once you find the tile for App Studio, click on it and choose *install* in the dialog that pops up.</span></span>

<img  width="450px" title="アプリ Studio をインストールする" src="~/assets/images/get-started/app-studio-install.png"/>

<span data-ttu-id="91dec-108">アプリ Studio がインストールされたら、[マニフェストエディター] タブをクリックして、Teams アプリのアプリパッケージの作成を開始します。</span><span class="sxs-lookup"><span data-stu-id="91dec-108">Once App Studio is installed click on the Manifest editor tab to begin creating the app package for your Teams app.</span></span>

<img  width="450px" title="App Studio" src="~/assets/images/get-started/app-studio.png"/>

<span data-ttu-id="91dec-110">このサンプルには独自のマニフェストが用意されており、プロジェクトのビルド時にアプリパッケージを構築するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="91dec-110">The sample comes with its own pre-made manifest, and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="91dec-111">.NET では、これは Visual Studio とノード JS で行われます。これは`gulp` 、プロジェクトのルートディレクトリのコマンドラインで入力することによって行われます。</span><span class="sxs-lookup"><span data-stu-id="91dec-111">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="91dec-112">生成されたアプリパッケージの名前は*helloworldapp*です。</span><span class="sxs-lookup"><span data-stu-id="91dec-112">The name of the generated app package is *helloworldapp.zip*.</span></span> <span data-ttu-id="91dec-113">このファイルは、使用しているツールで場所が明確でない場合に検索できます。</span><span class="sxs-lookup"><span data-stu-id="91dec-113">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="91dec-114">このチュートリアルの次の部分では、マニフェストエディターの [既存のアプリタイルを*インポート*する] を選択して、このアプリパッケージを変更します。</span><span class="sxs-lookup"><span data-stu-id="91dec-114">In the next part of this walkthrough you are going to modify this app package by selecting the *Import an existing app* tile in the Manifest Editor.</span></span>

<img  width="450px" title="アプリのインポート" src="~/assets/images/get-started/app-studio-import.png"/>

<span data-ttu-id="91dec-116">アプリパッケージがインポートされると、アプリ Studio は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="91dec-116">Once the app package has been imported App Studio should look like this:</span></span>

<img  width="450px" title="アプリのインポート" src="~/assets/images/get-started/app-studio-imported-app.png"/>

<span data-ttu-id="91dec-118">新しくインポートしたアプリ [ *Hello World*] のタイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="91dec-118">Click on the tile for your newly imported app, *Hello World*.</span></span>

<img  width="450px" title="アプリのインポート" src="~/assets/images/get-started/app-studio-manifest-editor.png"/>

<span data-ttu-id="91dec-120">マニフェストエディターの左側に手順の一覧があり、それぞれの手順で入力する必要があるプロパティの一覧が右側に表示されています。</span><span class="sxs-lookup"><span data-stu-id="91dec-120">There is a list of steps in the left-hand side of the Manifest editor, and on the right a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="91dec-121">サンプルアプリの使用を開始したので、情報の多くは既に入力されています。次の手順では、更新が必要なパーツを変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="91dec-121">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="91dec-122">アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="91dec-122">App details</span></span>

<span data-ttu-id="91dec-123">[*詳細*] の下にある*アプリの詳細*エントリをクリックします。</span><span class="sxs-lookup"><span data-stu-id="91dec-123">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="91dec-124">[*生成*] ボタンをクリックして、新しいアプリ id を作成します。</span><span class="sxs-lookup"><span data-stu-id="91dec-124">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="91dec-125">新しいアプリ id は、次`2322041b-72bf-459d-b107-f4f335bc35bd`のようになります。</span><span class="sxs-lookup"><span data-stu-id="91dec-125">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="91dec-126">右側のウィンドウに表示されるアプリの詳細を確認して、*開発者情報*や*ブランド*化などのエントリを理解してください。</span><span class="sxs-lookup"><span data-stu-id="91dec-126">Look through the rest of the App details in the right hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="91dec-127">これらのセクションは、配布用の新しいアプリを作成する場合に重要です。</span><span class="sxs-lookup"><span data-stu-id="91dec-127">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="91dec-128">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="91dec-128">Capabilities: Tabs</span></span>

<span data-ttu-id="91dec-129">タブは Teams アプリに追加する最も簡単な要素の1つです。</span><span class="sxs-lookup"><span data-stu-id="91dec-129">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="91dec-130">サンプルアプリでは、複数のタブが既にサポートされており、それらを次のように有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="91dec-130">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="91dec-131">[チーム] タブ</span><span class="sxs-lookup"><span data-stu-id="91dec-131">Team tab</span></span>

<span data-ttu-id="91dec-132">アプリには、チームタブを1つだけ含めることができます。</span><span class="sxs-lookup"><span data-stu-id="91dec-132">Your app can only have one Team tab.</span></span>

<img  width="450px" title="Teams タブの追加" src="~/assets/images/get-started/app-studio-manifest-editor-tabs.png"/>

<span data-ttu-id="91dec-134">この例では、[チーム] タブで構成ページが移動されます。</span><span class="sxs-lookup"><span data-stu-id="91dec-134">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="91dec-135">エントリの最後にある [. *..* ] 記号をクリックし、ドロップダウンから [*編集*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="91dec-135">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="91dec-136">アプリを`https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io`ホストするときに上で使用した url で url を変更します。</span><span class="sxs-lookup"><span data-stu-id="91dec-136">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="91dec-137">個人用タブ</span><span class="sxs-lookup"><span data-stu-id="91dec-137">Personal tabs</span></span>

<span data-ttu-id="91dec-138">アプリは、[チーム] タブを含む最大16個のタブを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="91dec-138">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="91dec-139">個人用タブは、[チーム] タブとは異なる方法で表示されます。[個人用タブ] ボックスの一覧に [ *Hello Tab]* が表示されています。</span><span class="sxs-lookup"><span data-stu-id="91dec-139">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="91dec-140">その時点で、プレースホルダーの値`com.contoso.helloworld.hellotab`があります。</span><span class="sxs-lookup"><span data-stu-id="91dec-140">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="91dec-141">エントリの最後にある [. *..* ] 記号をクリックし、ドロップダウンから [*編集*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="91dec-141">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="91dec-142">次のダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="91dec-142">The following dialog will appear.</span></span>

<img  width="450px" title="個人用タブダイアログの追加" src="~/assets/images/get-started/app-studio-manifest-editor-p-tabs-dialog.png"/>

<span data-ttu-id="91dec-144">アプリの URL で更新する必要があるフィールドは2つあります。</span><span class="sxs-lookup"><span data-stu-id="91dec-144">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="91dec-145">コンテンツの URL をに変更`https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="91dec-145">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="91dec-146">Web サイトの URL をに変更する`https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="91dec-146">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="91dec-147">`yourteamsapp.ngrok.io`は、アプリをホストするときに上で使用した URL に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="91dec-147">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="91dec-148">ボット</span><span class="sxs-lookup"><span data-stu-id="91dec-148">Bots</span></span>

<span data-ttu-id="91dec-149">Bot は、アプリに機能を追加する最も一般的な方法です。</span><span class="sxs-lookup"><span data-stu-id="91dec-149">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="91dec-150">Hello world サンプルには、このサンプルの一部として既に bot がありますが、Microsoft に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="91dec-150">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" title="Bot を追加する" src="~/assets/images/get-started/app-studio-manifest-editor-bots.png"/>

<span data-ttu-id="91dec-152">サンプルからインポートされた bot には、まだ関連付けられているアプリ ID がありません。</span><span class="sxs-lookup"><span data-stu-id="91dec-152">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="91dec-153">新しい bot を作成して、アプリ Studio が新しいアプリ ID を作成して Microsoft に登録できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="91dec-153">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="91dec-154">これは bot のアプリ ID であり、前の手順でアプリに対して作成したアプリ ID とは異なります。</span><span class="sxs-lookup"><span data-stu-id="91dec-154">Note that this is the App ID for the bot, which is different from the App ID that we created for the app in a earlier step.</span></span> <span data-ttu-id="91dec-155">アプリ内の各 bot は、独自のアプリ ID を必要とします。</span><span class="sxs-lookup"><span data-stu-id="91dec-155">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="91dec-156">Bot リストでインポートされた*bot*の横にある [*削除*] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="91dec-156">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="91dec-157">これで、表示する bot がなくなりました。</span><span class="sxs-lookup"><span data-stu-id="91dec-157">Now there are no bots left to show.</span></span> <span data-ttu-id="91dec-158">[*セットアップ*] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="91dec-158">Click *Setup*.</span></span> <span data-ttu-id="91dec-159">これにより、[ *bot の設定*] ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="91dec-159">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" title="Bot ダイアログの追加" src="~/assets/images/get-started/app-studio-manifest-editor-bots-setup-dialog.png"/>

<span data-ttu-id="91dec-161">`Contoso bot`のような bot 名を追加し、[*範囲*] の下にあるボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="91dec-161">Add a bot name such as `Contoso bot`, and click both the buttons under *scope*.</span></span>

<span data-ttu-id="91dec-162">[*ボットの作成*] を選択してダイアログを終了します。</span><span class="sxs-lookup"><span data-stu-id="91dec-162">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="91dec-163">アプリ Studio は、ボットを Microsoft に登録するのに時間を費やして、bot リストに新しい bot を表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91dec-163">App Studio will spend a moment registering your bot with Microsoft, and then should display your new bot in the bot list.</span></span> <span data-ttu-id="91dec-164">これで、メモ帳でテキストファイルを開いて、新しい bot id をコピーして貼り付けるのはよい時間になります。</span><span class="sxs-lookup"><span data-stu-id="91dec-164">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="91dec-165">この id は後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="91dec-165">You will need this id later.</span></span>

<span data-ttu-id="91dec-166">[*新しいパスワードの生成*] をクリックして、の BOT アプリ ID にメモしたものと同じテキストファイル内のパスワードをメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="91dec-166">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="91dec-167">これは、パスワードが表示される唯一の時間なので、必ずこれを実行してください。</span><span class="sxs-lookup"><span data-stu-id="91dec-167">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="91dec-168">*Bot エンドポイントアドレス*をに`https://yourteamsapp.ngrok.io/api/messages`更新し`yourteamsapp.ngrok.io`ます。では、アプリをホストするときに上で使用した URL で置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="91dec-168">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="91dec-169">まだ実行していない場合は、テキストファイルを保存するのに適した時間になります。</span><span class="sxs-lookup"><span data-stu-id="91dec-169">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="91dec-170">この情報をホストされたアプリに追加します。このチュートリアルでは、後で bot とのセキュリティで保護された通信を許可します。</span><span class="sxs-lookup"><span data-stu-id="91dec-170">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="91dec-171">メッセージングの拡張機能</span><span class="sxs-lookup"><span data-stu-id="91dec-171">Messaging extensions</span></span>

<span data-ttu-id="91dec-172">メッセージング拡張機能を使用すると、ユーザーはサービスから情報を求め、カード形式でその情報をチャネル会話に直接送信できます。</span><span class="sxs-lookup"><span data-stu-id="91dec-172">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="91dec-173">メッセージング拡張機能は、[新規作成] ボックスの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="91dec-173">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="91dec-174">App Studio の左側の列にある [*機能*] の [*メッセージング拡張*] をクリックして、メッセージング拡張機能の構成を開始します。</span><span class="sxs-lookup"><span data-stu-id="91dec-174">Click on *Messaging extensions* under *Capabilities* in the left hand column of App Studio to begin configuring the messaging extension.</span></span>

<img  width="450px" title="メッセージング拡張機能を追加する" src="~/assets/images/get-started/app-studio-manifest-editor-mess-ext.png"/>

<span data-ttu-id="91dec-176">[*メッセージング拡張*] の下の右側のウィンドウに、サンプルのメッセージング拡張機能が一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="91dec-176">The sample messaging extension is listed in the right hand pane under *Messaging Extensions*.</span></span> <span data-ttu-id="91dec-177">[*削除*] をもう一度クリックしてこのエントリを削除し、次に [*セットアップ] ボタン*をクリックして、bot をフォローしたときと同じ手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="91dec-177">Click *Delete* again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="91dec-178">これにより、[*メッセージングの内線番号*] ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="91dec-178">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="91dec-179">[*既存の bot を使用*] タブを選択して、*既存のボットのいずれかを選択*します。</span><span class="sxs-lookup"><span data-stu-id="91dec-179">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="91dec-180">ドロップダウンメニューで、上のセクションで作成した bot を選択します。</span><span class="sxs-lookup"><span data-stu-id="91dec-180">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="91dec-181">*Bot 名*を追加し、[*保存*] をクリックしてダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="91dec-181">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="91dec-182">[*コマンド*] セクションで、[*追加*] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="91dec-182">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="91dec-183">検索ベースのコマンドを追加しています。そのため、[*ユーザーによるサービスのクエリを許可する*] オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="91dec-183">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="91dec-184">[*新しいコマンド*] ダイアログボックスで、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="91dec-184">In the *New command* dialog enter the following values.</span></span>

<span data-ttu-id="91dec-185">[*新規作成] コマンド*:</span><span class="sxs-lookup"><span data-stu-id="91dec-185">Under *New command*:</span></span>

- <span data-ttu-id="91dec-186">*コマンド ID* = Ge/domtext</span><span class="sxs-lookup"><span data-stu-id="91dec-186">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="91dec-187">*Title* = 楽しいテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="91dec-187">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="91dec-188">*Description* = ランダムなテキストとイメージを取得する</span><span class="sxs-lookup"><span data-stu-id="91dec-188">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="91dec-189">[*パラメーター*]:</span><span class="sxs-lookup"><span data-stu-id="91dec-189">Under *Parameter*:</span></span>

- <span data-ttu-id="91dec-190">*Name* = cardtitle</span><span class="sxs-lookup"><span data-stu-id="91dec-190">*Name*        = cardTitle</span></span>
- <span data-ttu-id="91dec-191">*タイトル*= カードのタイトル</span><span class="sxs-lookup"><span data-stu-id="91dec-191">*Title*       = Card title</span></span>
- <span data-ttu-id="91dec-192">*Description* = 使用するカードのタイトル</span><span class="sxs-lookup"><span data-stu-id="91dec-192">*Description* = Card title to use</span></span>

<span data-ttu-id="91dec-193">情報を入力したら、[*保存*] をクリックしてダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="91dec-193">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="91dec-194">Teams にアプリを登録する</span><span class="sxs-lookup"><span data-stu-id="91dec-194">Register your app in Teams</span></span>

<span data-ttu-id="91dec-195">アプリの詳細の入力が完了しましたが、2つの手順は残っています。</span><span class="sxs-lookup"><span data-stu-id="91dec-195">You have now completed entering the details of your app, but two steps remain.</span></span> <span data-ttu-id="91dec-196">最初に、アプリを Teams にインストールするには、App Studio の [テストと配布] セクションを使用する必要があります。その後、ホストされたアプリケーションを bot のアプリ ID とパスワードで更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91dec-196">First you must use the Test and Distribute section of App Studio to install your app in Teams, and second you must update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="91dec-197">このサンプルでは、ボットと messaging 拡張機能の両方で同じアプリ ID とパスワードを使用することが想定されています。</span><span class="sxs-lookup"><span data-stu-id="91dec-197">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="91dec-198">App Studio の左側の列にある [*テスト] を*クリックし、[*完了*] の下にあるアイテムを配布します。</span><span class="sxs-lookup"><span data-stu-id="91dec-198">Click on the *Test and distribute* item under *Finish* in the left hand column of App Studio.</span></span>

<img  width="450px" title="アプリのテスト" src="~/assets/images/get-started/app-studio-manifest-editor-test.png"/>

<span data-ttu-id="91dec-200">アプリを Teams にアップロードするために、[*テストおよび配布*] の下にある [*インストール*] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="91dec-200">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" title="メッセージング拡張ダイアログの追加" src="~/assets/images/get-started/app-studio-manifest-editor-test-dialog.png"/>

<span data-ttu-id="91dec-202">[*チームに追加*] セクションの [*検索*] ボックスをクリックして、サンプルアプリを追加するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="91dec-202">Click on the *Search* box in the *Add to a team* section and select a team to add the sample app to.</span></span> <span data-ttu-id="91dec-203">通常は、テストのために特別なチームをセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="91dec-203">Usually you will want to set up a special team for testing.</span></span>

<span data-ttu-id="91dec-204">ダイアログの下部にある [ *Install* ] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="91dec-204">Click the *Install* button at the bottom of the dialog.</span></span>

<span data-ttu-id="91dec-205">これで、このチュートリアルの App Studio の部分が完成します。</span><span class="sxs-lookup"><span data-stu-id="91dec-205">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="91dec-206">アプリが Teams で実行中であることが表示されるようになりましたが、ボットとメッセージング拡張機能は、ホストされているアプリケーションの環境を更新して、アプリ Id とパスワードが何かを知るまでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="91dec-206">You should now see your app running in Teams, however the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" title="完成したアプリ" src="~/assets/images/get-started/app-studio-finished-app.png"/>