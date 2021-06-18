### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="02135-101">App Studio を使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="02135-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="02135-102">App Studio は、TeamsストアからインストールできるアプリTeamsです。</span><span class="sxs-lookup"><span data-stu-id="02135-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="02135-103">アプリの作成と登録が簡略化されます。</span><span class="sxs-lookup"><span data-stu-id="02135-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="02135-104">アプリ パッケージを更新するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="02135-104">Complete the following steps to update the app package:</span></span>

1. <span data-ttu-id="02135-105">App Studio を Teamsにインストールするには、左側のバーの下部にある [アプリ] アイコンを選択し **、App Studio を検索します**。</span><span class="sxs-lookup"><span data-stu-id="02135-105">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**:</span></span>

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. <span data-ttu-id="02135-106">[App **Studio] タイルを選択し** 、[インストール] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="02135-106">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="02135-107">App Studio がインストールされています。</span><span class="sxs-lookup"><span data-stu-id="02135-107">The App Studio is installed:</span></span>

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. <span data-ttu-id="02135-108">アプリのアプリ パッケージを作成するにはTeams App Studio の [**マニフェスト エディター]** タブ **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="02135-108">To create the app package for your Teams app, select the **Manifest editor** tab in **App Studio**:</span></span>

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    <span data-ttu-id="02135-109">このサンプルには独自のマニフェストが付属し、プロジェクトのビルド時にアプリ パッケージをビルドするように設計されています。</span><span class="sxs-lookup"><span data-stu-id="02135-109">The sample comes with its own manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="02135-110">アプリ パッケージを .NET 上にビルドするには、次のVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="02135-110">You can build the app package on .NET with Visual Studio.</span></span> <span data-ttu-id="02135-111">このVisual Studio、manifest.jsファイルはマニフェストの下に **配置** されます `Microsoft.Teams.Samples.HelloWorld.Web` 。</span><span class="sxs-lookup"><span data-stu-id="02135-111">In Visual Studio, the manifest.json file is located in under **Manifest** in `Microsoft.Teams.Samples.HelloWorld.Web`.</span></span> <span data-ttu-id="02135-112">この手順は、次の図で説明します。</span><span class="sxs-lookup"><span data-stu-id="02135-112">This step is described by the following image:</span></span>  
    
    <img  width="450px" alt="Build the app package on .NET with Visual Studio" src="~/assets/images/get-started/app-package-on-.NET-with-Visual-Studio.png"/>
    
    <span data-ttu-id="02135-113">プロジェクトのルート ディレクトリのコマンド Node.js入力して、アプリ パッケージをビルド `gulp` できます。</span><span class="sxs-lookup"><span data-stu-id="02135-113">You can build the app package on Node.js by typing `gulp` at the command line in the root directory of the project.</span></span>

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

    <span data-ttu-id="02135-114">生成されたアプリ パッケージの名前は次 **helloworldapp.zip。**</span><span class="sxs-lookup"><span data-stu-id="02135-114">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="02135-115">使用しているツールで場所がクリアされていない場合は、このファイルを検索できます。</span><span class="sxs-lookup"><span data-stu-id="02135-115">You can search for this file if the location is not clear in the tool you are using.</span></span>

1. <span data-ttu-id="02135-116">次に、このアプリ パッケージを変更するには、[マニフェスト エディター] で **[既存の** アプリのインポート] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="02135-116">Now to modify this app package, select **Import an existing app** in the **Manifest editor**:</span></span>

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. <span data-ttu-id="02135-117">新しく **インポートしたアプリの** Hello World タイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="02135-117">Select the **Hello World** tile for your newly imported app:</span></span>

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="02135-118">次の図は、App Studio でインポートされたアプリ パッケージを示しています。</span><span class="sxs-lookup"><span data-stu-id="02135-118">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="02135-119">マニフェスト エディターの左側には、手順の一覧があります。</span><span class="sxs-lookup"><span data-stu-id="02135-119">On the left-hand side of the Manifest editor there is a list of steps.</span></span> <span data-ttu-id="02135-120">右側には、各手順で入力する必要があるプロパティの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="02135-120">On the right-hand side there is a list of properties that need to be filled in for each step.</span></span> <span data-ttu-id="02135-121">サンプル アプリの使用を開始すると、多くの情報が既に完了しています。</span><span class="sxs-lookup"><span data-stu-id="02135-121">As you started with a sample app, much of the information is already completed.</span></span> <span data-ttu-id="02135-122">次の手順では、Hello World アプリのプロパティを更新できます。</span><span class="sxs-lookup"><span data-stu-id="02135-122">The next steps enable you to update the properties of the Hello World app.</span></span>

#### <a name="app-details"></a><span data-ttu-id="02135-123">アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="02135-123">App details</span></span>

<span data-ttu-id="02135-124">[詳細 **] で [アプリの** 詳細] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="02135-124">Select **App details** under **Details**.</span></span> <span data-ttu-id="02135-125">[生成] **ボタンを** 選択して、新しいアプリ ID を作成します。</span><span class="sxs-lookup"><span data-stu-id="02135-125">Select the **Generate** button to create a new App ID.</span></span>

<span data-ttu-id="02135-126">新しいアプリ ID はに似ています `2322041b-72bf-459d-b107-f4f335bc35bd` 。</span><span class="sxs-lookup"><span data-stu-id="02135-126">Your new App ID is similar to `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="02135-127">開発者情報やブランドの詳細など、右側のウィンドウでアプリの **詳細を確認** します。</span><span class="sxs-lookup"><span data-stu-id="02135-127">Go through the app details in the right-hand pane including **Developer information** and **Branding** details.</span></span> <span data-ttu-id="02135-128">これらの詳細は、配布用の新しいアプリを作成する場合に重要です。</span><span class="sxs-lookup"><span data-stu-id="02135-128">These details are important if you are writing a new app for distribution.</span></span>

#### <a name="tabs"></a><span data-ttu-id="02135-129">タブ</span><span class="sxs-lookup"><span data-stu-id="02135-129">Tabs</span></span>

<span data-ttu-id="02135-130">アプリにタブを追加Teamsです。</span><span class="sxs-lookup"><span data-stu-id="02135-130">It is simple to add tabs to a Teams app.</span></span> <span data-ttu-id="02135-131">サンプル アプリは既に複数のタブをサポートし、有効にできます。</span><span class="sxs-lookup"><span data-stu-id="02135-131">The sample app already supports several tabs, and you can enable them.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="02135-132">[チーム] タブ</span><span class="sxs-lookup"><span data-stu-id="02135-132">Team tab</span></span>

<span data-ttu-id="02135-133">アプリで使用できるチーム タブは次の 1 つのみです。</span><span class="sxs-lookup"><span data-stu-id="02135-133">Your app can only have one Team tab:</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="02135-134">このサンプルでは、[チーム] タブに構成ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="02135-134">In this sample, the Team tab is where your configuration page is displayed.</span></span> <span data-ttu-id="02135-135">タブ構成 **URL の ...** 記号 **を選択** し、ドロップダウン メニューから **[編集** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="02135-135">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="02135-136">URL を、アプリのホスティング時に使用した URL に置き換える必要がある `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` [場所に変更します](#host-the-sample-app)。</span><span class="sxs-lookup"><span data-stu-id="02135-136">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` must be replaced with the URL that you used when [hosting your app](#host-the-sample-app).</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="02135-137">[個人] タブ</span><span class="sxs-lookup"><span data-stu-id="02135-137">Personal tabs</span></span>

<span data-ttu-id="02135-138">アプリには、[チーム] タブを含む最大 16 のタブを含め、16 つまで使用できます。</span><span class="sxs-lookup"><span data-stu-id="02135-138">Your app can have up to 16 tabs, including the Team tab.</span></span>

<span data-ttu-id="02135-139">個人用タブは、[チーム] タブとは異なります **。Hello Tab** は、プレースホルダー値を持つ個人用タブリストに既に一覧表示されています `com.contoso.helloworld.hellotab` 。</span><span class="sxs-lookup"><span data-stu-id="02135-139">Personal tabs are different from the Team tab. **Hello Tab** is already listed in the personal tabs list with a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="02135-140">タブ構成 **URL の ...** 記号 **を選択** し、ドロップダウン メニューから **[編集** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="02135-140">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="02135-141">次のダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="02135-141">The following dialog box appears:</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="02135-142">アプリの URL で次のボックスを更新します。</span><span class="sxs-lookup"><span data-stu-id="02135-142">Update the following boxes with your app URL:</span></span>

- <span data-ttu-id="02135-143">[コンテンツ **の URL] ボックスを** に変更する `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="02135-143">Change the **Content URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="02135-144">[Web サイト **の URL] ボックスをに** 変更する `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="02135-144">Change the **Website URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="02135-145">アプリ `yourteamsapp.ngrok.io` をホストするときに使用した URL に置き換える。</span><span class="sxs-lookup"><span data-stu-id="02135-145">Replace `yourteamsapp.ngrok.io` by the URL that you used when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="02135-146">ボット</span><span class="sxs-lookup"><span data-stu-id="02135-146">Bots</span></span>

<span data-ttu-id="02135-147">ボット機能をアプリに簡単に追加できます。</span><span class="sxs-lookup"><span data-stu-id="02135-147">It is easy to add the bots functionality to your app.</span></span> <span data-ttu-id="02135-148">**Hello World サンプル** アプリには、サンプルの一部としてボットが既に存在しますが、Microsoft に登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02135-148">The **Hello World** sample app already has a bot as part of the sample, but you must register it with Microsoft:</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="02135-149">サンプルからインポートされたボットには、関連付けられたアプリ ID が含まれません。</span><span class="sxs-lookup"><span data-stu-id="02135-149">The bot that was imported from the sample does not have an associated App ID.</span></span> <span data-ttu-id="02135-150">App Studio で新しいアプリ ID を作成して Microsoft に登録するには、新しいボットを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02135-150">You must create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span>

> [!NOTE]
> <span data-ttu-id="02135-151">ボットの App Studio によって作成されたアプリ ID は、アプリ用に作成されたアプリ ID とは異なります。</span><span class="sxs-lookup"><span data-stu-id="02135-151">The App ID created by App Studio for the bot is different from the App ID created for the app.</span></span> <span data-ttu-id="02135-152">アプリ内の各ボットには、独自のアプリ ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="02135-152">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="02135-153">ボットをセットアップするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="02135-153">Complete the following steps to setup your bot:</span></span>

1. <span data-ttu-id="02135-154">ボットリスト **の** インポートされたボットの横にある [削除] を選択します。</span><span class="sxs-lookup"><span data-stu-id="02135-154">Select **Delete** next to the imported bot in the bot list.</span></span> <span data-ttu-id="02135-155">これで、表示するボットは残りはありません。</span><span class="sxs-lookup"><span data-stu-id="02135-155">Now there are no bots left to show.</span></span> 
1. <span data-ttu-id="02135-156">[ **セットアップ] を** 選択して 、[ **ボットのセットアップ] ダイアログ ボックスを** 表示します。</span><span class="sxs-lookup"><span data-stu-id="02135-156">Select **Setup** to display the **Set up a bot** dialog box.</span></span>

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. <span data-ttu-id="02135-157">Contoso ボットのボット名 **を追加し** 、[スコープ] で 3 つのチェック ボックスをオン **にします**。</span><span class="sxs-lookup"><span data-stu-id="02135-157">Add a bot name **Contoso bot** and select all three check boxes under **Scope**.</span></span>
1. <span data-ttu-id="02135-158">[保存 **] を** 選択してダイアログ ボックスを終了します。</span><span class="sxs-lookup"><span data-stu-id="02135-158">Choose **Save** to exit the dialog box.</span></span> <span data-ttu-id="02135-159">App Studio は、ボットを Microsoft に登録し、ボットリストに新しいボットを表示します。</span><span class="sxs-lookup"><span data-stu-id="02135-159">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> 
1. <span data-ttu-id="02135-160">次に、メモ帳でテキスト ファイルを開き、新しいボット ID をコピーして貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="02135-160">Now open a text file in notepad and copy and paste your new bot ID into it.</span></span>
1. <span data-ttu-id="02135-161">[ **新しいパスワードの生成]** をクリックし、ボット アプリ ID をメモしたのと同じテキスト ファイルにパスワードをメモします。</span><span class="sxs-lookup"><span data-stu-id="02135-161">Click **Generate New Password**, and note the password in the same text file you noted your bot App ID.</span></span>
1. <span data-ttu-id="02135-162">ボット エンドポイント **のアドレスを更新し** 、アプリのホスト時に使用した `https://yourteamsapp.ngrok.io/api/messages` URL `yourteamsapp.ngrok.io` に置き換える。</span><span class="sxs-lookup"><span data-stu-id="02135-162">Update the **Bot endpoint address** to `https://yourteamsapp.ngrok.io/api/messages`, and replace `yourteamsapp.ngrok.io` with the URL that you used when hosting your app.</span></span>
1. <span data-ttu-id="02135-163">次に、ボットとの安全な通信を可能にするために、ファイルからホストされたアプリに情報を追加する必要があるテキスト ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="02135-163">Now save your text file as you must add the information from the file to your hosted app to allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="02135-164">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="02135-164">Messaging extensions</span></span>

<span data-ttu-id="02135-165">メッセージング拡張機能を使用すると、ユーザーはサービスから情報を求め、その情報を投稿できます。</span><span class="sxs-lookup"><span data-stu-id="02135-165">Messaging extensions let users ask for information from your service and post that information.</span></span> <span data-ttu-id="02135-166">情報は、カードの形式でチャネル会話に投稿されます。</span><span class="sxs-lookup"><span data-stu-id="02135-166">The information is posted in the form of cards into the channel conversation.</span></span> <span data-ttu-id="02135-167">メッセージング拡張機能は、作成ボックスの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="02135-167">Messaging extensions appear at the bottom of the compose box.</span></span>

<span data-ttu-id="02135-168">メッセージング拡張機能をセットアップするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="02135-168">Complete the following steps to setup your messaging extension:</span></span>

1. <span data-ttu-id="02135-169">App Studio **の左側の** ウィンドウで [ **機能]** の下にある [メッセージング拡張機能] を選択して、メッセージング拡張機能を構成します。</span><span class="sxs-lookup"><span data-stu-id="02135-169">Select **Messaging extensions** under **Capabilities** in the left-hand pane of App Studio to configure the messaging extension:</span></span>

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    <span data-ttu-id="02135-170">サンプル メッセージング拡張機能は、[メッセージング拡張機能] ウィンドウ **に一覧表示** されます。</span><span class="sxs-lookup"><span data-stu-id="02135-170">The sample messaging extension is listed in the **Messaging Extensions** pane.</span></span>

1. <span data-ttu-id="02135-171">[ **削除] を** 選択してメッセージング拡張機能を削除し、[ **セットアップ**] を選択し、ボットに使用する手順と同じ手順 [を実行します](#bots)。</span><span class="sxs-lookup"><span data-stu-id="02135-171">Select **Delete** to remove the messaging extension, select **Set up**, and follow the same steps used for [bots](#bots).</span></span> <span data-ttu-id="02135-172">[ **メッセージング拡張機能] ダイアログ** ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="02135-172">The **Messaging Extension** dialog box is displayed.</span></span>
1. <span data-ttu-id="02135-173">[既存の **ボットを使用する] タブを** 選択し、 **既存のボットの 1 つから選択します**。</span><span class="sxs-lookup"><span data-stu-id="02135-173">Select the **Use existing bot** tab and **Select from one of my existing bots**.</span></span>
1. <span data-ttu-id="02135-174">ドロップダウン メニューから作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="02135-174">Select the bot you created from the drop-down menu.</span></span> <span data-ttu-id="02135-175">ボット名 **を追加し、[** 保存] **を選択して** ダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="02135-175">Add a **Bot name** and select **Save** to close the dialog box.</span></span>
1. <span data-ttu-id="02135-176">[コマンド] **セクションで** 、[追加] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="02135-176">Under the **Command** section, select **Add**.</span></span> <span data-ttu-id="02135-177">検索ベースのコマンドを追加するには、[ユーザーがサービスに情報をクエリしてメッセージに挿入する] **オプションを選択** します。</span><span class="sxs-lookup"><span data-stu-id="02135-177">To add a search-based command, select the **Allow users to query your service for information and insert that into a message** option.</span></span>
1. <span data-ttu-id="02135-178">[新しい **コマンド] ダイアログ** ボックスで、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="02135-178">In the **New command** dialog box, enter the following values:</span></span>

    <span data-ttu-id="02135-179">[新 **しいコマンド] で次のコマンドを実行します**。</span><span class="sxs-lookup"><span data-stu-id="02135-179">Under **New command**:</span></span>

    - <span data-ttu-id="02135-180">**コマンド ID**: ランダム テキストを入力する</span><span class="sxs-lookup"><span data-stu-id="02135-180">**Command ID**: Enter random text</span></span>
    - <span data-ttu-id="02135-181">**Title**: ランダムなタイトルを入力する</span><span class="sxs-lookup"><span data-stu-id="02135-181">**Title**: Enter random title</span></span>
    - <span data-ttu-id="02135-182">**説明**: ランダムな説明を入力する</span><span class="sxs-lookup"><span data-stu-id="02135-182">**Description**: Enter random description</span></span>

    <span data-ttu-id="02135-183">[パラメーター **] の下**:</span><span class="sxs-lookup"><span data-stu-id="02135-183">Under **Parameter**:</span></span>

    - <span data-ttu-id="02135-184">**名前**: パラメーター名を入力します。</span><span class="sxs-lookup"><span data-stu-id="02135-184">**Name**: Enter the parameter name</span></span>
    - <span data-ttu-id="02135-185">**タイトル**: カードタイトルを入力する</span><span class="sxs-lookup"><span data-stu-id="02135-185">**Title**: Enter the card title</span></span>
    - <span data-ttu-id="02135-186">**説明**: カードの説明を入力する</span><span class="sxs-lookup"><span data-stu-id="02135-186">**Description**: Enter card description</span></span>

1. <span data-ttu-id="02135-187">情報を入力した後、[保存] **を選択して** ダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="02135-187">After you enter the information, select **Save** to close the dialog box.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="02135-188">アプリをアプリに登録Teams</span><span class="sxs-lookup"><span data-stu-id="02135-188">Register your app in Teams</span></span>

<span data-ttu-id="02135-189">アプリの詳細を入力したら、次の手順を実行してアプリをアプリに登録Teams。</span><span class="sxs-lookup"><span data-stu-id="02135-189">After entering the details of your app, complete the following steps to register your app in Teams:</span></span>

1. <span data-ttu-id="02135-190">App **Studio のテストと配布** を使用して、アプリをアプリにインストールTeams。</span><span class="sxs-lookup"><span data-stu-id="02135-190">Use **Test and distribute** of App Studio to install your app in Teams.</span></span> 
1. <span data-ttu-id="02135-191">ボットのアプリ ID とパスワードを使用してホストされたアプリケーションを更新します。</span><span class="sxs-lookup"><span data-stu-id="02135-191">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="02135-192">サンプル アプリでは、ボットとメッセージング拡張機能の両方に同じアプリ ID とパスワードを使用します。</span><span class="sxs-lookup"><span data-stu-id="02135-192">For the sample app, use the same App ID and password for both bot and messaging extension.</span></span> 
1. <span data-ttu-id="02135-193">App Studio **の左側のウィンドウ\*\*\*\*で 、[完了]** で [テストと配布] を選択します。</span><span class="sxs-lookup"><span data-stu-id="02135-193">Select **Test and distribute**  under **Finish** in the left-hand pane of App Studio:</span></span>

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. <span data-ttu-id="02135-194">アプリをアプリにアップロードするには、[テストTeams配布] の [**インストール**]**ボタンを選択します**。</span><span class="sxs-lookup"><span data-stu-id="02135-194">To upload your app to Teams, select the **Install** button under **Test and Distribute**:</span></span>

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. <span data-ttu-id="02135-195">[チームに **追加** ] セクションで **[検索] ボックスを選択** し、サンプル アプリを追加するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="02135-195">Select the **Search** box in the **Add to a team** section and select a team to add the sample app.</span></span> <span data-ttu-id="02135-196">テスト用に特別なチームを設定できます。</span><span class="sxs-lookup"><span data-stu-id="02135-196">You can set up a special team for testing.</span></span>
1. <span data-ttu-id="02135-197">ダイアログ ボックス **の下部** にある [インストール] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="02135-197">Select the **Install** button at the bottom of the dialog box.</span></span>

<span data-ttu-id="02135-198">アプリがアプリで使用Teams。</span><span class="sxs-lookup"><span data-stu-id="02135-198">Your app is now available in Teams.</span></span> <span data-ttu-id="02135-199">ただし、ボットとメッセージング拡張機能は、ホストされているアプリケーション環境をアプリの ID とパスワードで更新するまで機能しません。</span><span class="sxs-lookup"><span data-stu-id="02135-199">However, the bot and the messaging extension will not work until you update the hosted applications environment with the App IDs and passwords.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
