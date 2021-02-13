### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="3a25d-101">App Studio を使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="3a25d-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="3a25d-102">App Studio は、Teams ストアからインストールできる Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="3a25d-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="3a25d-103">アプリの作成と登録が簡素化されます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="3a25d-104">Teams に App Studio をインストールするには、左側のバーの下部にある [アプリ] アイコンを選択し **、App Studio を検索します**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-104">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**.</span></span>

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

<span data-ttu-id="3a25d-105">App **Studio タイルを選択し** 、[インストール] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-105">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="3a25d-106">App Studio がインストールされている。</span><span class="sxs-lookup"><span data-stu-id="3a25d-106">The App Studio is installed.</span></span>

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

<span data-ttu-id="3a25d-107">[マニフェスト エディター **] タブを** 選択して、Teams アプリのアプリ パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-107">Select the **Manifest editor** tab to create the app package for your Teams app.</span></span>

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

<span data-ttu-id="3a25d-108">サンプルには独自の事前に作成されたマニフェストが付属し、プロジェクトのビルド時にアプリ パッケージをビルドするように設計されています。</span><span class="sxs-lookup"><span data-stu-id="3a25d-108">The sample comes with its own pre-made manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="3a25d-109">.NET では、これは Visual Studio で行われ、Node JS では、プロジェクトのルート ディレクトリにコマンド ラインで入力します `gulp` 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-109">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="3a25d-110">生成されたアプリ パッケージの名前は **helloworldapp.zip。**</span><span class="sxs-lookup"><span data-stu-id="3a25d-110">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="3a25d-111">使用しているツールで場所がはっきりしない場合は、このファイルを検索できます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-111">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="3a25d-112">このアプリ パッケージを変更するには、マニフェストエディターで [既存のアプリのインポート] タイル **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-112">Now to modify this app package, select the **Import an existing app** tile in the **Manifest editor**.</span></span>

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

<span data-ttu-id="3a25d-113">新しく **インポートしたアプリ** の Hello World タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="3a25d-113">Click the **Hello World** tile for your newly imported app.</span></span>

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="3a25d-114">次の図は、App Studio でインポートされたアプリ パッケージを示しています。</span><span class="sxs-lookup"><span data-stu-id="3a25d-114">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="3a25d-115">マニフェスト エディターの左側と右側には、各手順に入力する必要があるプロパティの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-115">There is a list of steps on the left-hand side of the Manifest editor and on the right-hand side, a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="3a25d-116">サンプル アプリを使い始めてから、情報の多くが既に入力されています。次の手順では、まだ更新する必要があるパーツを変更する手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-116">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="3a25d-117">アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="3a25d-117">App details</span></span>

<span data-ttu-id="3a25d-118">[詳細] の *[アプリの詳細]* エントリを *クリックします*。</span><span class="sxs-lookup"><span data-stu-id="3a25d-118">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="3a25d-119">[生成] *ボタンを* クリックして、新しいアプリ ID を作成します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-119">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="3a25d-120">新しいアプリ ID は次のように表示されます `2322041b-72bf-459d-b107-f4f335bc35bd` 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-120">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="3a25d-121">右側のウィンドウでアプリの残りの詳細を確認し、開発者情報やブランド化などのエントリの一部を *理解します*。 </span><span class="sxs-lookup"><span data-stu-id="3a25d-121">Look through the rest of the App details in the right-hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="3a25d-122">これらのセクションは、配布用の新しいアプリを作成する場合に重要です。</span><span class="sxs-lookup"><span data-stu-id="3a25d-122">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="3a25d-123">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="3a25d-123">Capabilities: Tabs</span></span>

<span data-ttu-id="3a25d-124">タブは、Teams アプリに追加する最も簡単な要素の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="3a25d-124">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="3a25d-125">サンプル アプリは既に複数のタブをサポートしています。次のようにして有効にできます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-125">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="3a25d-126">[チーム] タブ</span><span class="sxs-lookup"><span data-stu-id="3a25d-126">Team tab</span></span>

<span data-ttu-id="3a25d-127">アプリで使用できるチーム タブは 1 つのみです。</span><span class="sxs-lookup"><span data-stu-id="3a25d-127">Your app can only have one Team tab.</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="3a25d-128">このサンプルでは、[チーム] タブが構成ページの場所です。</span><span class="sxs-lookup"><span data-stu-id="3a25d-128">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="3a25d-129">エントリの末尾 *にある ...* 記号をクリックし、ドロップダウンから *[* 編集] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-129">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="3a25d-130">URL を、アプリをホストするときに上記で使用した URL に置き換える `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` 必要がある場所に変更します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-130">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="3a25d-131">[個人] タブ</span><span class="sxs-lookup"><span data-stu-id="3a25d-131">Personal tabs</span></span>

<span data-ttu-id="3a25d-132">アプリには、チーム タブを含め、最大 16 のタブを含めできます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-132">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="3a25d-133">[個人用] タブは、チーム タブとは異なる方法で表示されます。[Hello *Tab] が個人用タブ* の一覧に既に表示されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a25d-133">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="3a25d-134">現時点では、プレースホルダー値が設定されます `com.contoso.helloworld.hellotab` 。</span><span class="sxs-lookup"><span data-stu-id="3a25d-134">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="3a25d-135">エントリの末尾 *にある ...* 記号をクリックし、ドロップダウンから *[* 編集] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-135">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="3a25d-136">次のダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-136">The following dialog will appear.</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="3a25d-137">アプリの URL で更新する必要があるフィールドが 2 つある。</span><span class="sxs-lookup"><span data-stu-id="3a25d-137">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="3a25d-138">コンテンツ URL を次に変更する `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="3a25d-138">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="3a25d-139">Web サイトの URL を次に変更する `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="3a25d-139">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="3a25d-140">アプリ `yourteamsapp.ngrok.io` をホストするときに上記で使用した URL に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a25d-140">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="3a25d-141">ボット</span><span class="sxs-lookup"><span data-stu-id="3a25d-141">Bots</span></span>

<span data-ttu-id="3a25d-142">ボットは、アプリに機能を追加する最も一般的な方法です。</span><span class="sxs-lookup"><span data-stu-id="3a25d-142">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="3a25d-143">Hello World サンプルには、サンプルの一部としてボットが既に存在しますが、まだ Microsoft に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="3a25d-143">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="3a25d-144">サンプルからインポートされたボットには、アプリ ID がまだ関連付けされていません。</span><span class="sxs-lookup"><span data-stu-id="3a25d-144">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="3a25d-145">App Studio で新しいアプリ ID を作成して Microsoft に登録するには、新しいボットを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a25d-145">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="3a25d-146">これはボットのアプリ ID で、アプリ用に作成されたアプリ ID とは異なります。</span><span class="sxs-lookup"><span data-stu-id="3a25d-146">Note that this is the App ID for the bot, which is different from the App ID created for the app.</span></span> <span data-ttu-id="3a25d-147">アプリ内の各ボットには、独自のアプリ ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="3a25d-147">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="3a25d-148">ボットの *一覧* で、インポートされたボット *の横にある* [削除] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="3a25d-148">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="3a25d-149">表示するボットが残っていない。</span><span class="sxs-lookup"><span data-stu-id="3a25d-149">Now there are no bots left to show.</span></span> <span data-ttu-id="3a25d-150">[セットアップ *] をクリックします*。</span><span class="sxs-lookup"><span data-stu-id="3a25d-150">Click *Setup*.</span></span> <span data-ttu-id="3a25d-151">これにより、[ボットの *セットアップ] ダイアログが表示* されます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-151">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

<span data-ttu-id="3a25d-152">次のようなボット名を追加し、[スコープ] の下の `Contoso bot` 3 つすべてのボタンを **選択します**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-152">Add a bot name such as `Contoso bot`, and select all three buttons under **Scope**.</span></span>

<span data-ttu-id="3a25d-153">[ *ボットの作成] を* 選択してダイアログを終了します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-153">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="3a25d-154">App Studio はボットを Microsoft に登録し、ボットの一覧に新しいボットを表示します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-154">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> <span data-ttu-id="3a25d-155">メモ帳でテキスト ファイルを開き、新しいボット ID をコピーして貼り付けるのが良い方法です。</span><span class="sxs-lookup"><span data-stu-id="3a25d-155">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="3a25d-156">この ID は後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="3a25d-156">You will need this id later.</span></span>

<span data-ttu-id="3a25d-157">[ *新しいパスワードの* 生成] をクリックし、ボット アプリ ID をメモしたテキスト ファイルにパスワードをメモします。</span><span class="sxs-lookup"><span data-stu-id="3a25d-157">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="3a25d-158">パスワードが表示されるのは今回だけなので、この時点で確認してください。</span><span class="sxs-lookup"><span data-stu-id="3a25d-158">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="3a25d-159">Bot エンドポイント *のアドレスを更新* します。ここで、アプリをホストするときに上記で使用した URL に置き `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` 換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a25d-159">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="3a25d-160">まだ保存していない場合は、テキスト ファイルを保存する良い時間です。</span><span class="sxs-lookup"><span data-stu-id="3a25d-160">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="3a25d-161">この情報は、このチュートリアルの後半でホストされるアプリに追加します。これにより、ボットとの安全な通信が可能になります。</span><span class="sxs-lookup"><span data-stu-id="3a25d-161">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="3a25d-162">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="3a25d-162">Messaging extensions</span></span>

<span data-ttu-id="3a25d-163">メッセージング拡張機能を使用すると、ユーザーはサービスから情報を求め、その情報をカードの形式でチャネルの会話に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-163">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="3a25d-164">メッセージング拡張機能は、作成ボックスの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-164">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="3a25d-165">App Studio **の左側の** 列にある **[機能** ] の下にある [メッセージング拡張機能] を選択して、メッセージング拡張機能を構成します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-165">Select **Messaging extensions** under **Capabilities** in the left-hand column of App Studio to configure the messaging extension.</span></span>

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

<span data-ttu-id="3a25d-166">サンプルのメッセージング拡張機能は、右側のウィンドウの [メッセージング拡張機能] の下 **に一覧表示されます**。</span><span class="sxs-lookup"><span data-stu-id="3a25d-166">The sample messaging extension is listed in the right-hand pane under **Messaging Extensions**.</span></span> <span data-ttu-id="3a25d-167">もう **一度 [** 削除] を選択してこのエントリを削除し、ボットの場合と同じ手順に従って [セットアップ] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="3a25d-167">Select **Delete** again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="3a25d-168">これにより、[メッセージング拡張機能 *] ダイアログが表示* されます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-168">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="3a25d-169">[既存 *のボットを使用する* ] タブを選択し、既存のボット *の 1 つから選択します*。</span><span class="sxs-lookup"><span data-stu-id="3a25d-169">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="3a25d-170">ドロップダウン メニューで、上記のセクションで作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-170">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="3a25d-171">ボット名 *を追加し、[* 保存] *をクリックして* ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-171">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="3a25d-172">[コマンド] *セクションで* 、[追加] を *クリックします*。</span><span class="sxs-lookup"><span data-stu-id="3a25d-172">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="3a25d-173">検索ベースのコマンドを追加します。そのため、[サービスのクエリをユーザーに許可する *] オプションを選択* します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-173">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="3a25d-174">[新しい **コマンド] ダイアログ** ボックスで、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-174">In the **New command** dialog, enter the following values.</span></span>

<span data-ttu-id="3a25d-175">[新 *しいコマンド] で、次のコマンドを実行します*。</span><span class="sxs-lookup"><span data-stu-id="3a25d-175">Under *New command*:</span></span>

- <span data-ttu-id="3a25d-176">*コマンド ID*  = getRandomText</span><span class="sxs-lookup"><span data-stu-id="3a25d-176">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="3a25d-177">*Title*       = 楽しいテキストをランダムに取得する</span><span class="sxs-lookup"><span data-stu-id="3a25d-177">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="3a25d-178">*Description* = ランダムなテキストと画像を取得します</span><span class="sxs-lookup"><span data-stu-id="3a25d-178">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="3a25d-179">Under *Parameter*:</span><span class="sxs-lookup"><span data-stu-id="3a25d-179">Under *Parameter*:</span></span>

- <span data-ttu-id="3a25d-180">*Name*        = cardTitle</span><span class="sxs-lookup"><span data-stu-id="3a25d-180">*Name*        = cardTitle</span></span>
- <span data-ttu-id="3a25d-181">*Title*       = カード タイトル</span><span class="sxs-lookup"><span data-stu-id="3a25d-181">*Title*       = Card title</span></span>
- <span data-ttu-id="3a25d-182">*説明* = 使用するカード タイトル</span><span class="sxs-lookup"><span data-stu-id="3a25d-182">*Description* = Card title to use</span></span>

<span data-ttu-id="3a25d-183">情報を入力したら、[保存] をクリック *して* ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-183">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="3a25d-184">Teams でアプリを登録する</span><span class="sxs-lookup"><span data-stu-id="3a25d-184">Register your app in Teams</span></span>

<span data-ttu-id="3a25d-185">これで、アプリの詳細の入力が完了しましたが、次の 2 つの手順が残っています。</span><span class="sxs-lookup"><span data-stu-id="3a25d-185">You have now completed entering the details of your app, but the following two steps remain:</span></span>
1. <span data-ttu-id="3a25d-186">App Studio の [テストと配布] セクションを使用して、Teams にアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="3a25d-186">Use the Test and Distribute section of App Studio to install your app in Teams.</span></span>
1. <span data-ttu-id="3a25d-187">ホストされたアプリケーションを、ボットのアプリ ID とパスワードで更新します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-187">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="3a25d-188">このサンプルでは、ボットとメッセージング拡張機能の両方に同じアプリ ID とパスワードを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a25d-188">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="3a25d-189">App Studio **の左側の列にある** **[完了** ] の下にある [テストと配布] 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-189">Select the **Test and distribute** item under **Finish** in the left-hand column of App Studio.</span></span>

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

<span data-ttu-id="3a25d-190">Teams にアプリをアップロードするには、[テストと配布] の下の [*インストール\*\*] ボタンをクリックします*。</span><span class="sxs-lookup"><span data-stu-id="3a25d-190">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

<span data-ttu-id="3a25d-191">[チーム **に追加** ] セクションの [検索] ボックス **を選択し** 、サンプル アプリを追加するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-191">Select the **Search** box in the **Add to a team** section and select a team to add the sample app to.</span></span> <span data-ttu-id="3a25d-192">通常、テスト用に特別なチームをセットアップできます。</span><span class="sxs-lookup"><span data-stu-id="3a25d-192">Usually, you can set up a special team for testing.</span></span>

<span data-ttu-id="3a25d-193">ダイアログの **下部** にある [インストール] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-193">Select the **Install** button at the bottom of the dialog.</span></span>

<span data-ttu-id="3a25d-194">これで、このチュートリアルの App Studio 部分が終了します。</span><span class="sxs-lookup"><span data-stu-id="3a25d-194">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="3a25d-195">Teams で実行されているアプリが表示されます。ただし、ホストされたアプリケーション環境を更新してアプリの ID とパスワードを確認するまで、ボットとメッセージング拡張機能は機能しません。</span><span class="sxs-lookup"><span data-stu-id="3a25d-195">You should now see your app running in Teams, however, the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
