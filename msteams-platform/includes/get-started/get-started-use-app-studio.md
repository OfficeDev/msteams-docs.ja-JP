### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="61197-101">アプリ Studio を使用してアプリパッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="61197-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="61197-102">App Studio は teams アプリで、Teams ストアからインストールできます。</span><span class="sxs-lookup"><span data-stu-id="61197-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="61197-103">これにより、アプリの作成と登録が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="61197-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="61197-104">Teams にアプリ Studio をインストールするには、左側のバーの下部にあるアプリストアアイコンをクリックして、アプリ Studio を検索します。</span><span class="sxs-lookup"><span data-stu-id="61197-104">To install App Studio in Teams, click on the app store icon at the bottom of the left hand bar, and search for App Studio.</span></span>

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

<span data-ttu-id="61197-105">アプリ Studio のタイルを見つけたら、それをクリックして、ポップアップしたダイアログの [ *インストール* ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="61197-105">Once you find the tile for App Studio, click on it and choose *install* in the dialog that pops up.</span></span>

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

<span data-ttu-id="61197-106">アプリ Studio がインストールされたら、[マニフェストエディター] タブをクリックして、Teams アプリのアプリパッケージの作成を開始します。</span><span class="sxs-lookup"><span data-stu-id="61197-106">Once App Studio is installed click on the Manifest editor tab to begin creating the app package for your Teams app.</span></span>

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

<span data-ttu-id="61197-107">このサンプルには独自のマニフェストが用意されており、プロジェクトのビルド時にアプリパッケージを構築するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="61197-107">The sample comes with its own pre-made manifest, and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="61197-108">.NET では、これは Visual Studio とノード JS で行われます。これは、 `gulp` プロジェクトのルートディレクトリのコマンドラインで入力することによって行われます。</span><span class="sxs-lookup"><span data-stu-id="61197-108">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="61197-109">生成されたアプリパッケージの名前は *helloworldapp.zip*。</span><span class="sxs-lookup"><span data-stu-id="61197-109">The name of the generated app package is *helloworldapp.zip*.</span></span> <span data-ttu-id="61197-110">このファイルは、使用しているツールで場所が明確でない場合に検索できます。</span><span class="sxs-lookup"><span data-stu-id="61197-110">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="61197-111">このチュートリアルの次の部分では、マニフェストエディターの [既存のアプリタイルを *インポート* する] を選択して、このアプリパッケージを変更します。</span><span class="sxs-lookup"><span data-stu-id="61197-111">In the next part of this walkthrough you are going to modify this app package by selecting the *Import an existing app* tile in the Manifest Editor.</span></span>

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

<span data-ttu-id="61197-112">アプリパッケージがインポートされると、アプリ Studio は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="61197-112">Once the app package has been imported App Studio should look like this:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="61197-113">新しくインポートしたアプリ [ *Hello World*] のタイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="61197-113">Click on the tile for your newly imported app, *Hello World*.</span></span>

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="61197-114">マニフェストエディターの左側に手順の一覧があり、それぞれの手順で入力する必要があるプロパティの一覧が右側に表示されています。</span><span class="sxs-lookup"><span data-stu-id="61197-114">There is a list of steps in the left-hand side of the Manifest editor, and on the right a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="61197-115">サンプルアプリの使用を開始したので、情報の多くは既に入力されています。次の手順では、更新が必要なパーツを変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="61197-115">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="61197-116">アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="61197-116">App details</span></span>

<span data-ttu-id="61197-117">[*詳細*] の下にある*アプリの詳細*エントリをクリックします。</span><span class="sxs-lookup"><span data-stu-id="61197-117">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="61197-118">[ *生成* ] ボタンをクリックして、新しいアプリ id を作成します。</span><span class="sxs-lookup"><span data-stu-id="61197-118">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="61197-119">新しいアプリ id は、次のようになり `2322041b-72bf-459d-b107-f4f335bc35bd` ます。</span><span class="sxs-lookup"><span data-stu-id="61197-119">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="61197-120">右側のウィンドウに表示されるアプリの詳細を確認して、 *開発者情報* や *ブランド*化などのエントリを理解してください。</span><span class="sxs-lookup"><span data-stu-id="61197-120">Look through the rest of the App details in the right hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="61197-121">これらのセクションは、配布用の新しいアプリを作成する場合に重要です。</span><span class="sxs-lookup"><span data-stu-id="61197-121">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="61197-122">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="61197-122">Capabilities: Tabs</span></span>

<span data-ttu-id="61197-123">タブは Teams アプリに追加する最も簡単な要素の1つです。</span><span class="sxs-lookup"><span data-stu-id="61197-123">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="61197-124">サンプルアプリでは、複数のタブが既にサポートされており、それらを次のように有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="61197-124">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="61197-125">[チーム] タブ</span><span class="sxs-lookup"><span data-stu-id="61197-125">Team tab</span></span>

<span data-ttu-id="61197-126">アプリには、チームタブを1つだけ含めることができます。</span><span class="sxs-lookup"><span data-stu-id="61197-126">Your app can only have one Team tab.</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="61197-127">この例では、[チーム] タブで構成ページが移動されます。</span><span class="sxs-lookup"><span data-stu-id="61197-127">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="61197-128">エントリの最後にある [. *..* ] 記号をクリックし、ドロップダウンから [ *編集* ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="61197-128">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="61197-129">アプリをホストする `https://yourteamsapp.ngrok.io/configure` ときに上で使用した url で url を変更し `yourteamsapp.ngrok.io` ます。</span><span class="sxs-lookup"><span data-stu-id="61197-129">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="61197-130">[個人] タブ</span><span class="sxs-lookup"><span data-stu-id="61197-130">Personal tabs</span></span>

<span data-ttu-id="61197-131">アプリは、[チーム] タブを含む最大16個のタブを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="61197-131">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="61197-132">個人用タブは、[チーム] タブとは異なる方法で表示されます。[個人用タブ] ボックスの一覧に [ *Hello Tab]* が表示されています。</span><span class="sxs-lookup"><span data-stu-id="61197-132">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="61197-133">その時点で、プレースホルダーの値があり `com.contoso.helloworld.hellotab` ます。</span><span class="sxs-lookup"><span data-stu-id="61197-133">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="61197-134">エントリの最後にある [. *..* ] 記号をクリックし、ドロップダウンから [ *編集* ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="61197-134">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="61197-135">次のダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="61197-135">The following dialog will appear.</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="61197-136">アプリの URL で更新する必要があるフィールドは2つあります。</span><span class="sxs-lookup"><span data-stu-id="61197-136">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="61197-137">コンテンツの URL をに変更 `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="61197-137">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="61197-138">Web サイトの URL をに変更する `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="61197-138">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="61197-139">`yourteamsapp.ngrok.io`は、アプリをホストするときに上で使用した URL に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="61197-139">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="61197-140">ボット</span><span class="sxs-lookup"><span data-stu-id="61197-140">Bots</span></span>

<span data-ttu-id="61197-141">Bot は、アプリに機能を追加する最も一般的な方法です。</span><span class="sxs-lookup"><span data-stu-id="61197-141">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="61197-142">Hello world サンプルには、このサンプルの一部として既に bot がありますが、Microsoft に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="61197-142">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="61197-143">サンプルからインポートされた bot には、まだ関連付けられているアプリ ID がありません。</span><span class="sxs-lookup"><span data-stu-id="61197-143">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="61197-144">新しい bot を作成して、アプリ Studio が新しいアプリ ID を作成して Microsoft に登録できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61197-144">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="61197-145">これは bot のアプリ ID であり、前の手順でアプリに対して作成したアプリ ID とは異なります。</span><span class="sxs-lookup"><span data-stu-id="61197-145">Note that this is the App ID for the bot, which is different from the App ID that we created for the app in a earlier step.</span></span> <span data-ttu-id="61197-146">アプリ内の各 bot は、独自のアプリ ID を必要とします。</span><span class="sxs-lookup"><span data-stu-id="61197-146">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="61197-147">Bot リストでインポートされた*bot*の横にある [*削除*] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="61197-147">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="61197-148">これで、表示する bot がなくなりました。</span><span class="sxs-lookup"><span data-stu-id="61197-148">Now there are no bots left to show.</span></span> <span data-ttu-id="61197-149">[ *セットアップ*] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="61197-149">Click *Setup*.</span></span> <span data-ttu-id="61197-150">これにより、[ *bot の設定* ] ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="61197-150">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

<span data-ttu-id="61197-151">のような bot 名を追加 `Contoso bot` し、[ *scope*] の下にある3つのボタンすべてを選択します。</span><span class="sxs-lookup"><span data-stu-id="61197-151">Add a bot name such as `Contoso bot`, and select all three buttons under *scope*.</span></span>

<span data-ttu-id="61197-152">[ *ボットの作成* ] を選択してダイアログを終了します。</span><span class="sxs-lookup"><span data-stu-id="61197-152">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="61197-153">アプリ Studio は、ボットを Microsoft に登録するのに時間を費やして、bot リストに新しい bot を表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61197-153">App Studio will spend a moment registering your bot with Microsoft, and then should display your new bot in the bot list.</span></span> <span data-ttu-id="61197-154">これで、メモ帳でテキストファイルを開いて、新しい bot id をコピーして貼り付けるのはよい時間になります。</span><span class="sxs-lookup"><span data-stu-id="61197-154">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="61197-155">この id は後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="61197-155">You will need this id later.</span></span>

<span data-ttu-id="61197-156">[ *新しいパスワードの生成*] をクリックして、の BOT アプリ ID にメモしたものと同じテキストファイル内のパスワードをメモしておきます。</span><span class="sxs-lookup"><span data-stu-id="61197-156">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="61197-157">これは、パスワードが表示される唯一の時間なので、必ずこれを実行してください。</span><span class="sxs-lookup"><span data-stu-id="61197-157">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="61197-158">*Bot エンドポイントアドレス*をに更新し `https://yourteamsapp.ngrok.io/api/messages` ます。では、 `yourteamsapp.ngrok.io` アプリをホストするときに上で使用した URL で置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="61197-158">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="61197-159">まだ実行していない場合は、テキストファイルを保存するのに適した時間になります。</span><span class="sxs-lookup"><span data-stu-id="61197-159">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="61197-160">この情報をホストされたアプリに追加します。このチュートリアルでは、後で bot とのセキュリティで保護された通信を許可します。</span><span class="sxs-lookup"><span data-stu-id="61197-160">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="61197-161">メッセージングの拡張機能</span><span class="sxs-lookup"><span data-stu-id="61197-161">Messaging extensions</span></span>

<span data-ttu-id="61197-162">メッセージング拡張機能を使用すると、ユーザーはサービスから情報を求め、カード形式でその情報をチャネル会話に直接送信できます。</span><span class="sxs-lookup"><span data-stu-id="61197-162">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="61197-163">メッセージング拡張機能は、[新規作成] ボックスの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="61197-163">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="61197-164">App Studio の左側の列にある [*機能*] の [*メッセージング拡張*] をクリックして、メッセージング拡張機能の構成を開始します。</span><span class="sxs-lookup"><span data-stu-id="61197-164">Click on *Messaging extensions* under *Capabilities* in the left hand column of App Studio to begin configuring the messaging extension.</span></span>

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

<span data-ttu-id="61197-165">[ *メッセージング拡張*] の下の右側のウィンドウに、サンプルのメッセージング拡張機能が一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="61197-165">The sample messaging extension is listed in the right hand pane under *Messaging Extensions*.</span></span> <span data-ttu-id="61197-166">[ *削除* ] をもう一度クリックしてこのエントリを削除し、次に [ *セットアップ] ボタン* をクリックして、bot をフォローしたときと同じ手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="61197-166">Click *Delete* again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="61197-167">これにより、[ *メッセージングの内線番号* ] ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="61197-167">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="61197-168">[ *既存の bot を使用* ] タブを選択して、 *既存のボットのいずれかを選択*します。</span><span class="sxs-lookup"><span data-stu-id="61197-168">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="61197-169">ドロップダウンメニューで、上のセクションで作成した bot を選択します。</span><span class="sxs-lookup"><span data-stu-id="61197-169">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="61197-170">*Bot 名*を追加し、[*保存*] をクリックしてダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="61197-170">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="61197-171">[ *コマンド* ] セクションで、[ *追加*] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="61197-171">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="61197-172">検索ベースのコマンドを追加しています。そのため、[ *ユーザーによるサービスのクエリを許可する* ] オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="61197-172">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="61197-173">[ *新しいコマンド* ] ダイアログボックスで、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="61197-173">In the *New command* dialog enter the following values.</span></span>

<span data-ttu-id="61197-174">[ *新規作成] コマンド*:</span><span class="sxs-lookup"><span data-stu-id="61197-174">Under *New command*:</span></span>

- <span data-ttu-id="61197-175">*コマンド ID*  = Ge/domtext</span><span class="sxs-lookup"><span data-stu-id="61197-175">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="61197-176">*Title*       = 楽しいテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="61197-176">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="61197-177">*Description* = ランダムなテキストとイメージを取得する</span><span class="sxs-lookup"><span data-stu-id="61197-177">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="61197-178">[ *パラメーター*]:</span><span class="sxs-lookup"><span data-stu-id="61197-178">Under *Parameter*:</span></span>

- <span data-ttu-id="61197-179">*Name*        = cardtitle</span><span class="sxs-lookup"><span data-stu-id="61197-179">*Name*        = cardTitle</span></span>
- <span data-ttu-id="61197-180">*タイトル*       = カードのタイトル</span><span class="sxs-lookup"><span data-stu-id="61197-180">*Title*       = Card title</span></span>
- <span data-ttu-id="61197-181">*Description* = 使用するカードのタイトル</span><span class="sxs-lookup"><span data-stu-id="61197-181">*Description* = Card title to use</span></span>

<span data-ttu-id="61197-182">情報を入力したら、[ *保存* ] をクリックしてダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="61197-182">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="61197-183">Teams にアプリを登録する</span><span class="sxs-lookup"><span data-stu-id="61197-183">Register your app in Teams</span></span>

<span data-ttu-id="61197-184">アプリの詳細の入力が完了しましたが、2つの手順は残っています。</span><span class="sxs-lookup"><span data-stu-id="61197-184">You have now completed entering the details of your app, but two steps remain.</span></span> <span data-ttu-id="61197-185">最初に、アプリを Teams にインストールするには、App Studio の [テストと配布] セクションを使用する必要があります。その後、ホストされたアプリケーションを bot のアプリ ID とパスワードで更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61197-185">First you must use the Test and Distribute section of App Studio to install your app in Teams, and second you must update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="61197-186">このサンプルでは、ボットと messaging 拡張機能の両方で同じアプリ ID とパスワードを使用することが想定されています。</span><span class="sxs-lookup"><span data-stu-id="61197-186">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="61197-187">App Studio の左側の列にある [ *テスト] を* クリックし、[ *完了* ] の下にあるアイテムを配布します。</span><span class="sxs-lookup"><span data-stu-id="61197-187">Click on the *Test and distribute* item under *Finish* in the left hand column of App Studio.</span></span>

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

<span data-ttu-id="61197-188">アプリを Teams にアップロードするために、[*テストおよび配布*] の下にある [*インストール*] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="61197-188">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

<span data-ttu-id="61197-189">[*チームに追加*] セクションの [*検索*] ボックスをクリックして、サンプルアプリを追加するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="61197-189">Click on the *Search* box in the *Add to a team* section and select a team to add the sample app to.</span></span> <span data-ttu-id="61197-190">通常は、テストのために特別なチームをセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61197-190">Usually you will want to set up a special team for testing.</span></span>

<span data-ttu-id="61197-191">ダイアログの下部にある [ *Install* ] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="61197-191">Click the *Install* button at the bottom of the dialog.</span></span>

<span data-ttu-id="61197-192">これで、このチュートリアルの App Studio の部分が完成します。</span><span class="sxs-lookup"><span data-stu-id="61197-192">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="61197-193">アプリが Teams で実行中であることが表示されるようになりましたが、ボットとメッセージング拡張機能は、ホストされているアプリケーションの環境を更新して、アプリ Id とパスワードが何かを知るまでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="61197-193">You should now see your app running in Teams, however the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
