### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="312b1-101">アプリのスタジオを使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="312b1-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="312b1-102">アプリスタジオは、TeamsストアからインストールできるTeamsアプリです。</span><span class="sxs-lookup"><span data-stu-id="312b1-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="312b1-103">これにより、アプリの作成と登録が簡素化されます。</span><span class="sxs-lookup"><span data-stu-id="312b1-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="312b1-104">アプリ パッケージを更新するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="312b1-104">Complete the following steps to update the app package:</span></span>

1. <span data-ttu-id="312b1-105">Teamsでアプリスタジオをインストールするには、左側のバーの下部にある **[アプリ**]アイコンを選択し **、App Studioを** 検索します。</span><span class="sxs-lookup"><span data-stu-id="312b1-105">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**:</span></span>

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. <span data-ttu-id="312b1-106">**[アプリケーションスタジオ]** タイルを選択し、[**インストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-106">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="312b1-107">アプリスタジオがインストールされています。</span><span class="sxs-lookup"><span data-stu-id="312b1-107">The App Studio is installed:</span></span>

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. <span data-ttu-id="312b1-108">Teams アプリのアプリ パッケージを作成するには、**アプリ スタジオ** の **[マニフェスト エディター** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-108">To create the app package for your Teams app, select the **Manifest editor** tab in **App Studio**:</span></span>

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    <span data-ttu-id="312b1-109">このサンプルには独自のマニフェストが付属しており、プロジェクトのビルド時にアプリ パッケージをビルドするように設計されています。</span><span class="sxs-lookup"><span data-stu-id="312b1-109">The sample comes with its own manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="312b1-110">NET では、これはVisual Studioで行われ、Node.jsプロジェクト `gulp` のルート ディレクトリのコマンド ラインで入力します。</span><span class="sxs-lookup"><span data-stu-id="312b1-110">On .NET this is done in Visual Studio and on Node.js this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

    <span data-ttu-id="312b1-111">生成されたアプリ パッケージの名前は **helloworldapp.zip** です。</span><span class="sxs-lookup"><span data-stu-id="312b1-111">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="312b1-112">使用しているツールで場所が明確でない場合は、このファイルを検索できます。</span><span class="sxs-lookup"><span data-stu-id="312b1-112">You can search for this file if the location is not clear in the tool you are using.</span></span>

1. <span data-ttu-id="312b1-113">ここで、このアプリ パッケージを変更するには、[**マニフェスト エディター** で **既存のアプリをインポート** する] を選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-113">Now to modify this app package, select **Import an existing app** in the **Manifest editor**:</span></span>

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. <span data-ttu-id="312b1-114">新しくインポートしたアプリの **Hello World** タイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-114">Select the **Hello World** tile for your newly imported app:</span></span>

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="312b1-115">次の図は、App Studio でインポートされたアプリ パッケージを示しています。</span><span class="sxs-lookup"><span data-stu-id="312b1-115">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="312b1-116">マニフェスト エディターの左側には、手順の一覧があります。</span><span class="sxs-lookup"><span data-stu-id="312b1-116">On the left-hand side of the Manifest editor there is a list of steps.</span></span> <span data-ttu-id="312b1-117">右側には、各ステップに入力する必要があるプロパティのリストがあります。</span><span class="sxs-lookup"><span data-stu-id="312b1-117">On the right-hand side there is a list of properties that need to be filled in for each step.</span></span> <span data-ttu-id="312b1-118">サンプル アプリを使用すると、情報の多くが既に完了しています。</span><span class="sxs-lookup"><span data-stu-id="312b1-118">As you started with a sample app, much of the information is already completed.</span></span> <span data-ttu-id="312b1-119">次の手順では、Hello World アプリのプロパティを更新できます。</span><span class="sxs-lookup"><span data-stu-id="312b1-119">The next steps enable you to update the properties of the Hello World app.</span></span>

#### <a name="app-details"></a><span data-ttu-id="312b1-120">アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="312b1-120">App details</span></span>

<span data-ttu-id="312b1-121">[詳細 **] の** [アプリの **詳細]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-121">Select **App details** under **Details**.</span></span> <span data-ttu-id="312b1-122">[ **生成** ] ボタンを選択して、新しいアプリ ID を作成します。</span><span class="sxs-lookup"><span data-stu-id="312b1-122">Select the **Generate** button to create a new App ID.</span></span>

<span data-ttu-id="312b1-123">新しいアプリ ID は `2322041b-72bf-459d-b107-f4f335bc35bd` 、 と似ています。</span><span class="sxs-lookup"><span data-stu-id="312b1-123">Your new App ID is similar to `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="312b1-124">右側のウィンドウで、 **開発者情報** や **ブランドの** 詳細を含むアプリの詳細を確認します。</span><span class="sxs-lookup"><span data-stu-id="312b1-124">Go through the app details in the right-hand pane including **Developer information** and **Branding** details.</span></span> <span data-ttu-id="312b1-125">配布用の新しいアプリを作成する場合は、これらの詳細が重要です。</span><span class="sxs-lookup"><span data-stu-id="312b1-125">These details are important if you are writing a new app for distribution.</span></span>

#### <a name="tabs"></a><span data-ttu-id="312b1-126">タブ</span><span class="sxs-lookup"><span data-stu-id="312b1-126">Tabs</span></span>

<span data-ttu-id="312b1-127">Teamsアプリにタブを追加するのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="312b1-127">It is simple to add tabs to a Teams app.</span></span> <span data-ttu-id="312b1-128">サンプル アプリでは、既にいくつかのタブがサポートされており、有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="312b1-128">The sample app already supports several tabs, and you can enable them.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="312b1-129">[チーム] タブ</span><span class="sxs-lookup"><span data-stu-id="312b1-129">Team tab</span></span>

<span data-ttu-id="312b1-130">アプリには、チーム タブを 1 つだけ持つことができます。</span><span class="sxs-lookup"><span data-stu-id="312b1-130">Your app can only have one Team tab:</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="312b1-131">このサンプルでは、[チーム] タブが構成ページの表示場所です。</span><span class="sxs-lookup"><span data-stu-id="312b1-131">In this sample, the Team tab is where your configuration page is displayed.</span></span> <span data-ttu-id="312b1-132">**タブ構成 URL** の **..** 記号を選択し、ドロップダウン メニューから **[編集]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-132">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="312b1-133">URL を `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` [、アプリのホスティング](#host-the-sample-app)時に使用した URL に置き換える必要がある場所に変更します。</span><span class="sxs-lookup"><span data-stu-id="312b1-133">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` must be replaced with the URL that you used when [hosting your app](#host-the-sample-app).</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="312b1-134">[個人] タブ</span><span class="sxs-lookup"><span data-stu-id="312b1-134">Personal tabs</span></span>

<span data-ttu-id="312b1-135">アプリには、[チーム] タブを含めて最大 16 個のタブを設定できます。</span><span class="sxs-lookup"><span data-stu-id="312b1-135">Your app can have up to 16 tabs, including the Team tab.</span></span>

<span data-ttu-id="312b1-136">[個人] タブは [チーム] タブとは異 **なります。** `com.contoso.helloworld.hellotab`</span><span class="sxs-lookup"><span data-stu-id="312b1-136">Personal tabs are different from the Team tab. **Hello Tab** is already listed in the personal tabs list with a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="312b1-137">**タブ構成 URL** の **..** 記号を選択し、ドロップダウン メニューから **[編集]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-137">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="312b1-138">次のダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="312b1-138">The following dialog box appears:</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="312b1-139">アプリの URL で次のボックスを更新します。</span><span class="sxs-lookup"><span data-stu-id="312b1-139">Update the following boxes with your app URL:</span></span>

- <span data-ttu-id="312b1-140">**[コンテンツ URL]** ボックスを`https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="312b1-140">Change the **Content URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="312b1-141">**[Web サイトの URL]** ボックスを`https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="312b1-141">Change the **Website URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="312b1-142">`yourteamsapp.ngrok.io`アプリをホストするときに使用した URL で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="312b1-142">Replace `yourteamsapp.ngrok.io` by the URL that you used when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="312b1-143">ボット</span><span class="sxs-lookup"><span data-stu-id="312b1-143">Bots</span></span>

<span data-ttu-id="312b1-144">ボット機能をアプリに簡単に追加できます。</span><span class="sxs-lookup"><span data-stu-id="312b1-144">It is easy to add the bots functionality to your app.</span></span> <span data-ttu-id="312b1-145">**Hello World** サンプル アプリには、サンプルの一部としてボットが既に含まれていますが、マイクロソフトに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="312b1-145">The **Hello World** sample app already has a bot as part of the sample, but you must register it with Microsoft:</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="312b1-146">サンプルからインポートされたボットには、関連付けられたアプリ ID がありません。</span><span class="sxs-lookup"><span data-stu-id="312b1-146">The bot that was imported from the sample does not have an associated App ID.</span></span> <span data-ttu-id="312b1-147">アプリ スタジオが新しいアプリ ID を作成してマイクロソフトに登録できるように、新しいボットを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="312b1-147">You must create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span>

> [!NOTE]
> <span data-ttu-id="312b1-148">アプリスタジオによってボット用に作成されたアプリ ID は、アプリ用に作成されたアプリ ID とは異なります。</span><span class="sxs-lookup"><span data-stu-id="312b1-148">The App ID created by App Studio for the bot is different from the App ID created for the app.</span></span> <span data-ttu-id="312b1-149">アプリの各ボットには、独自のアプリ ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="312b1-149">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="312b1-150">ボットを設定するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="312b1-150">Complete the following steps to setup your bot:</span></span>

1. <span data-ttu-id="312b1-151">ボットリストでインポートしたボットの横にある **[削除** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-151">Select **Delete** next to the imported bot in the bot list.</span></span> <span data-ttu-id="312b1-152">今、表示するボットは残っていません。</span><span class="sxs-lookup"><span data-stu-id="312b1-152">Now there are no bots left to show.</span></span> 
1. <span data-ttu-id="312b1-153">[ **設定]** を選択して [ **ボットの設定** ] ダイアログ ボックスを表示します。</span><span class="sxs-lookup"><span data-stu-id="312b1-153">Select **Setup** to display the **Set up a bot** dialog box.</span></span>

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. <span data-ttu-id="312b1-154">ボット名 **Contoso ボット** を追加し、[ **スコープ**] の下の 3 つのチェック ボックスをすべてオンにします。</span><span class="sxs-lookup"><span data-stu-id="312b1-154">Add a bot name **Contoso bot** and select all three check boxes under **Scope**.</span></span>
1. <span data-ttu-id="312b1-155">[ **保存] を** 選択してダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="312b1-155">Choose **Save** to exit the dialog box.</span></span> <span data-ttu-id="312b1-156">アプリスタジオは、ボットをマイクロソフトに登録し、ボットリストに新しいボットを表示します。</span><span class="sxs-lookup"><span data-stu-id="312b1-156">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> 
1. <span data-ttu-id="312b1-157">次に、メモ帳でテキスト ファイルを開き、新しいボット ID をコピーして貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="312b1-157">Now open a text file in notepad and copy and paste your new bot ID into it.</span></span>
1. <span data-ttu-id="312b1-158">[ **新しいパスワードの生成**] をクリックし、ボットアプリ ID にメモしたのと同じテキスト ファイルにパスワードを書き留めます。</span><span class="sxs-lookup"><span data-stu-id="312b1-158">Click **Generate New Password**, and note the password in the same text file you noted your bot App ID.</span></span>
1. <span data-ttu-id="312b1-159">Bot **エンドポイントアドレス** を `https://yourteamsapp.ngrok.io/api/messages` に更新し、 `yourteamsapp.ngrok.io` アプリをホストするときに使用した URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="312b1-159">Update the **Bot endpoint address** to `https://yourteamsapp.ngrok.io/api/messages`, and replace `yourteamsapp.ngrok.io` with the URL that you used when hosting your app.</span></span>
1. <span data-ttu-id="312b1-160">ここで、ボットとの安全な通信を可能にするために、ファイルの情報をホストされたアプリに追加する必要がある場合は、テキスト ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="312b1-160">Now save your text file as you must add the information from the file to your hosted app to allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="312b1-161">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="312b1-161">Messaging extensions</span></span>

<span data-ttu-id="312b1-162">メッセージング拡張機能を使用すると、ユーザーはサービスから情報を要求し、その情報を投稿できます。</span><span class="sxs-lookup"><span data-stu-id="312b1-162">Messaging extensions let users ask for information from your service and post that information.</span></span> <span data-ttu-id="312b1-163">情報はカードの形でチャンネル会話に投稿されます。</span><span class="sxs-lookup"><span data-stu-id="312b1-163">The information is posted in the form of cards into the channel conversation.</span></span> <span data-ttu-id="312b1-164">メッセージ拡張機能は、作成ボックスの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="312b1-164">Messaging extensions appear at the bottom of the compose box.</span></span>

<span data-ttu-id="312b1-165">メッセージング拡張機能をセットアップするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="312b1-165">Complete the following steps to setup your messaging extension:</span></span>

1. <span data-ttu-id="312b1-166">App Studio の左側のペインにある **[機能**] で [**メッセージング** 拡張機能] を選択して、メッセージング拡張機能を構成します。</span><span class="sxs-lookup"><span data-stu-id="312b1-166">Select **Messaging extensions** under **Capabilities** in the left-hand pane of App Studio to configure the messaging extension:</span></span>

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    <span data-ttu-id="312b1-167">サンプルのメッセージング拡張機能は、[ **メッセージング拡張機能** ] ウィンドウに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="312b1-167">The sample messaging extension is listed in the **Messaging Extensions** pane.</span></span>

1. <span data-ttu-id="312b1-168">[ **削除]** を選択してメッセージング拡張機能を削除し、[ **セットアップ**] を選択して [、ボット](#bots)で使用する手順と同じ手順に従います。</span><span class="sxs-lookup"><span data-stu-id="312b1-168">Select **Delete** to remove the messaging extension, select **Set up**, and follow the same steps used for [bots](#bots).</span></span> <span data-ttu-id="312b1-169">[ **メッセージング拡張機能** ] ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="312b1-169">The **Messaging Extension** dialog box is displayed.</span></span>
1. <span data-ttu-id="312b1-170">[ **既存のボットを使用** ] タブと [ **既存のボットの 1 つから選択]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-170">Select the **Use existing bot** tab and **Select from one of my existing bots**.</span></span>
1. <span data-ttu-id="312b1-171">ドロップダウンメニューから作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-171">Select the bot you created from the drop-down menu.</span></span> <span data-ttu-id="312b1-172">**ボット名** を追加し、[**保存]** を選択してダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="312b1-172">Add a **Bot name** and select **Save** to close the dialog box.</span></span>
1. <span data-ttu-id="312b1-173">[ **コマンド** ] セクションで、[ **追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-173">Under the **Command** section, select **Add**.</span></span> <span data-ttu-id="312b1-174">検索ベースのコマンドを追加するには、[ **ユーザーがサービスに情報を照会し、それをメッセージに挿入できるようにする]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-174">To add a search-based command, select the **Allow users to query your service for information and insert that into a message** option.</span></span>
1. <span data-ttu-id="312b1-175">[ **新規コマンド** ]ダイアログ ボックスで、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="312b1-175">In the **New command** dialog box, enter the following values:</span></span>

    <span data-ttu-id="312b1-176">新規 **コマンド** の下:</span><span class="sxs-lookup"><span data-stu-id="312b1-176">Under **New command**:</span></span>

    - <span data-ttu-id="312b1-177">**コマンド ID**: ランダムテキストを入力します</span><span class="sxs-lookup"><span data-stu-id="312b1-177">**Command ID**: Enter random text</span></span>
    - <span data-ttu-id="312b1-178">**タイトル**: ランダムなタイトルを入力します</span><span class="sxs-lookup"><span data-stu-id="312b1-178">**Title**: Enter random title</span></span>
    - <span data-ttu-id="312b1-179">**説明**: ランダムな説明を入力します</span><span class="sxs-lookup"><span data-stu-id="312b1-179">**Description**: Enter random description</span></span>

    <span data-ttu-id="312b1-180">パラメータの下 **で**:</span><span class="sxs-lookup"><span data-stu-id="312b1-180">Under **Parameter**:</span></span>

    - <span data-ttu-id="312b1-181">**名前**: パラメータ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="312b1-181">**Name**: Enter the parameter name</span></span>
    - <span data-ttu-id="312b1-182">**タイトル**: カードタイトルを入力します。</span><span class="sxs-lookup"><span data-stu-id="312b1-182">**Title**: Enter the card title</span></span>
    - <span data-ttu-id="312b1-183">**説明**: カードの説明を入力します</span><span class="sxs-lookup"><span data-stu-id="312b1-183">**Description**: Enter card description</span></span>

1. <span data-ttu-id="312b1-184">情報を入力したら、[ **保存]** を選択してダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="312b1-184">After you enter the information, select **Save** to close the dialog box.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="312b1-185">アプリをTeamsに登録する</span><span class="sxs-lookup"><span data-stu-id="312b1-185">Register your app in Teams</span></span>

<span data-ttu-id="312b1-186">アプリの詳細を入力したら、次の手順を実行して、Teamsにアプリを登録します。</span><span class="sxs-lookup"><span data-stu-id="312b1-186">After entering the details of your app, complete the following steps to register your app in Teams:</span></span>

1. <span data-ttu-id="312b1-187">アプリスタジオの **テストと配布** を使用して、Teamsでアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="312b1-187">Use **Test and distribute** of App Studio to install your app in Teams.</span></span> 
1. <span data-ttu-id="312b1-188">ボットのアプリ ID とパスワードでホストアプリケーションを更新します。</span><span class="sxs-lookup"><span data-stu-id="312b1-188">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="312b1-189">サンプル アプリでは、ボットとメッセージングの両方の拡張機能に同じアプリ ID とパスワードを使用します。</span><span class="sxs-lookup"><span data-stu-id="312b1-189">For the sample app, use the same App ID and password for both bot and messaging extension.</span></span> 
1. <span data-ttu-id="312b1-190">[ **テスト] を選択し、App**  Studio の左側のウィンドウで **[完了** ] の下で配布します。</span><span class="sxs-lookup"><span data-stu-id="312b1-190">Select **Test and distribute**  under **Finish** in the left-hand pane of App Studio:</span></span>

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. <span data-ttu-id="312b1-191">アプリをTeamsにアップロードするには、[**テストと配布**] の [**インストール**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-191">To upload your app to Teams, select the **Install** button under **Test and Distribute**:</span></span>

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. <span data-ttu-id="312b1-192">[**チームに追加**] セクションの **[検索**] ボックスを選択し、サンプル アプリを追加するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-192">Select the **Search** box in the **Add to a team** section and select a team to add the sample app.</span></span> <span data-ttu-id="312b1-193">テスト用の特別なチームを設定できます。</span><span class="sxs-lookup"><span data-stu-id="312b1-193">You can set up a special team for testing.</span></span>
1. <span data-ttu-id="312b1-194">ダイアログボックスの下部にある **[インストール** ]ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="312b1-194">Select the **Install** button at the bottom of the dialog box.</span></span>

<span data-ttu-id="312b1-195">アプリがTeamsで利用可能になりました。</span><span class="sxs-lookup"><span data-stu-id="312b1-195">Your app is now available in Teams.</span></span> <span data-ttu-id="312b1-196">ただし、アプリ ID とパスワードでホストされたアプリケーション環境を更新するまで、ボットとメッセージング拡張機能は機能しません。</span><span class="sxs-lookup"><span data-stu-id="312b1-196">However, the bot and the messaging extension will not work until you update the hosted applications environment with the App IDs and passwords.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
