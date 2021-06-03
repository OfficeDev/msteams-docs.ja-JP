---
title: アプリとアプリのMicrosoft Teams ToolkitをVisual Studio Code
description: アプリを使用して、アプリ内で直接素晴らしいカスタム Visual Studio Codeを構築Microsoft Teams Toolkit
keywords: teams visual studio コード ツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bc97a78df5618c87dfc66fae179145acd749ad1f
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721823"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="41e13-104">アプリとアプリのTeams ToolkitをVisual Studio Code</span><span class="sxs-lookup"><span data-stu-id="41e13-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="41e13-105">Visual Studio Code の Teams Toolkit は、開発者エクスペリエンスに対する "ゼロ構成" アプローチで、統合 ID、クラウド ストレージへのアクセス、Microsoft Graph からのデータ、および Azure および M365 の他のサービスを備えた Teams アプリを作成および展開するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="41e13-105">The Teams Toolkit for Visual Studio Code helps developers create and deploy Teams apps with integrated identity, access to cloud storage, data from Microsoft Graph, and other services in Azure and M365 with a “zero-configuration” approach to the developer experience.</span></span>  

<span data-ttu-id="41e13-106">また、このツールキットは、Visual Studio CLI (と呼ばれる) として使用することもできます `teamsfx` 。</span><span class="sxs-lookup"><span data-stu-id="41e13-106">You also can use the toolkit with Visual Studio or as a CLI (called `teamsfx`).</span></span>

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="41e13-107">インストール用のTeams ToolkitをインストールVisual Studio Code</span><span class="sxs-lookup"><span data-stu-id="41e13-107">Install the Teams Toolkit for Visual Studio Code</span></span>

1. <span data-ttu-id="41e13-108">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="41e13-108">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="41e13-109">[拡張機能] ビューを選択します **(Ctrl + Shift +**  /   **>** X</span><span class="sxs-lookup"><span data-stu-id="41e13-109">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="41e13-110">検索ボックスに「Teams Toolkit」_と入力します_。</span><span class="sxs-lookup"><span data-stu-id="41e13-110">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="41e13-111">[インストール] ウィンドウの横にある緑色のインストール ボタンTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="41e13-111">Select on the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="41e13-112">また、マーケットプレースでTeams ToolkitをVisual Studio Code[できます](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。</span><span class="sxs-lookup"><span data-stu-id="41e13-112">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="41e13-113">次のツールは、必要に応じてVisual Studio Code拡張機能によってインストールされます。</span><span class="sxs-lookup"><span data-stu-id="41e13-113">The following tools will be installed by the Visual Studio Code extension when they are needed.</span></span>  <span data-ttu-id="41e13-114">既にインストールされている場合は、インストールされているバージョンが代わりに使用されます。</span><span class="sxs-lookup"><span data-stu-id="41e13-114">If already installed, the installed version will be used instead.</span></span>  <span data-ttu-id="41e13-115">Linux (WSL を含む) を使用する場合は、次のツールをインストールしてから使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="41e13-115">If using Linux (including WSL), you must install these tools before use:</span></span>

- [<span data-ttu-id="41e13-116">Azure Functions コア ツール</span><span class="sxs-lookup"><span data-stu-id="41e13-116">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="41e13-117">Azure Functions Core Tools は、Azure でサービスを実行するときに必要な認証ヘルパーを含む、ローカル デバッグ実行時にバックエンド コンポーネントをローカルで実行するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="41e13-117">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span>  <span data-ttu-id="41e13-118">プロジェクト ディレクトリ内にインストールされます (npm を使用 `devDependencies` )。</span><span class="sxs-lookup"><span data-stu-id="41e13-118">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="41e13-119">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="41e13-119">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="41e13-120">.NET SDK は、ローカル デバッグと Azure Functions アプリの展開用にカスタマイズされたバインドをインストールするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="41e13-120">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span>  <span data-ttu-id="41e13-121">.NET 3.1 (以降) SDK をグローバルにインストールしていない場合は、ポータブル バージョンがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="41e13-121">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version will be installed.</span></span>

- [<span data-ttu-id="41e13-122">ngrok</span><span class="sxs-lookup"><span data-stu-id="41e13-122">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="41e13-123">一部Teamsアプリ機能 (会話型ボット、メッセージング拡張機能、受信 Webhook) では、受信接続が必要です。</span><span class="sxs-lookup"><span data-stu-id="41e13-123">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span>  <span data-ttu-id="41e13-124">開発システムをトンネル経由でTeamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="41e13-124">You need to expose your development system to Teams through a tunnel.</span></span>  <span data-ttu-id="41e13-125">タブのみを含むアプリでは、トンネルは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="41e13-125">A tunnel is not required for apps that only include tabs.</span></span>  <span data-ttu-id="41e13-126">このパッケージは、(npm を使用して) プロジェクト ディレクトリ内にインストールされます `devDependencies` 。</span><span class="sxs-lookup"><span data-stu-id="41e13-126">This package is installed within the project directory (using npm `devDependencies`).</span></span>

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="41e13-127">次のTeams Toolkitを使用Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="41e13-127">Use the Teams Toolkit for Visual Studio Code</span></span>

- [<span data-ttu-id="41e13-128">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="41e13-128">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="41e13-129">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="41e13-129">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="41e13-130">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="41e13-130">Run your app locally</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="41e13-131">アプリを公開する</span><span class="sxs-lookup"><span data-stu-id="41e13-131">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="41e13-132">新しいプロジェクトをTeamsする</span><span class="sxs-lookup"><span data-stu-id="41e13-132">Set up a new Teams project</span></span>

<span data-ttu-id="41e13-133">このTeams Toolkitは、Azure Reactまたは M365 環境でホストされる SPFx Web パーツでホストされるアプリをSharePointできます。</span><span class="sxs-lookup"><span data-stu-id="41e13-133">The Teams Toolkit can create React apps that will be hosted in Azure or SPFx web parts that will be hosted on your M365 SharePoint environment.</span></span>  <span data-ttu-id="41e13-134">Azure でホストReact新しいアプリを作成するには、次の方法を実行します。</span><span class="sxs-lookup"><span data-stu-id="41e13-134">To create a new React app to be hosted on Azure:</span></span>

1. <span data-ttu-id="41e13-135">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="41e13-135">Open Visual Studio code.</span></span>
1. <span data-ttu-id="41e13-136">サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。</span><span class="sxs-lookup"><span data-stu-id="41e13-136">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="41e13-138">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="41e13-138">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="41e13-140">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="41e13-140">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="41e13-142">**[機能の選択]** 手順では、**[タブ]** 機能がすでに選択されています。</span><span class="sxs-lookup"><span data-stu-id="41e13-142">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="41e13-143">必要に応じて、[**ボットとメッセージング拡張機能\*\*\*\*] を選択することもできます**。</span><span class="sxs-lookup"><span data-stu-id="41e13-143">You can also optionally select **Bot** and **Messaging Extension**.</span></span>  <span data-ttu-id="41e13-144">**[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="41e13-144">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="41e13-146">**[フロントエンド ホストの種類]** 手順で、**[Azure]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="41e13-146">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="新規アプリのホスティングを選択する方法を示すスクリーンショット":::。

1. <span data-ttu-id="41e13-148">(省略可能)[クラウド **リソース] ステップ** で、アプリケーションで使用するクラウド リソースを選択します。</span><span class="sxs-lookup"><span data-stu-id="41e13-148">(Optional) On the **Cloud resources** step, select cloud resources that your application will use.</span></span>  <span data-ttu-id="41e13-149">CRUD (作成、読み取り、更新、削除) を選択して、テーブルまたは API SQLアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="41e13-149">You can select CRUD (create, read, update, delete) access to a SQL table or an API:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="新しいアプリにクラウド リソースを追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="41e13-151">[プログラミング **言語] ステップで\*\*\*\*、JavaScript** または **TypeScript を選択できます**。</span><span class="sxs-lookup"><span data-stu-id="41e13-151">On the **Programming Language** step, you can choose **JavaScript** or **TypeScript**:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. <span data-ttu-id="41e13-153">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="41e13-153">Select a workspace folder.</span></span>  <span data-ttu-id="41e13-154">ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="41e13-154">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="41e13-155">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="41e13-155">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="41e13-156">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="41e13-156">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="41e13-157">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="41e13-157">Press **Enter** to continue.</span></span>

<span data-ttu-id="41e13-158">数秒後に Teams アプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="41e13-158">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="41e13-159">スキャフォールディング されたアプリには、シングル サインオンを処理するコードが含Azure Active Directory、Microsoft サービスへのアクセスGraph。</span><span class="sxs-lookup"><span data-stu-id="41e13-159">The scaffolded app contains code to handle single sign-on with Azure Active Directory and access to the Microsoft Graph.</span></span>  <span data-ttu-id="41e13-160">Azure リソースを選択した場合、それらのリソースのコードも使用できます。</span><span class="sxs-lookup"><span data-stu-id="41e13-160">If you selected Azure resources, then the code for those resources will also be available.</span></span>

<span data-ttu-id="41e13-161">作成および発行プロセスの詳細についてはSPFxチュートリアルを参照[SPFxしてください](../get-started/first-app-spfx.md)。</span><span class="sxs-lookup"><span data-stu-id="41e13-161">For a walk-through of the SPFx creation and publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="41e13-162">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="41e13-162">Configure your app</span></span>

<span data-ttu-id="41e13-163">このアプリの中核となるのは、Teams 3 つのコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="41e13-163">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="41e13-164">ユーザー Microsoft Teamsアプリを操作するクライアント (Web、デスクトップ、モバイル) を指定します。</span><span class="sxs-lookup"><span data-stu-id="41e13-164">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="41e13-165">サーバーに表示されるコンテンツの要求に応答するTeams。</span><span class="sxs-lookup"><span data-stu-id="41e13-165">A server that responds to requests for content that will be displayed in Teams.</span></span> <span data-ttu-id="41e13-166">たとえば、HTML タブ コンテンツやボットアダプティブ カードなどです。</span><span class="sxs-lookup"><span data-stu-id="41e13-166">For example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="41e13-167">アプリ Teamsは、次の 3 つのファイルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="41e13-167">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="41e13-168">このmanifest.jsオンです。</span><span class="sxs-lookup"><span data-stu-id="41e13-168">The manifest.json.</span></span>
      > - <span data-ttu-id="41e13-169">パブリック [または組織](../resources/schema/manifest-schema.md#icons) のアプリ カタログに表示するアプリの色アイコン。</span><span class="sxs-lookup"><span data-stu-id="41e13-169">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="41e13-170">アクティビティ[バーに](../resources/schema/manifest-schema.md#icons)表示するアウトライン Teamsアイコン。</span><span class="sxs-lookup"><span data-stu-id="41e13-170">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="41e13-171">マニフェストとアイコンは、プロジェクトにアップロードされる前にプロジェクトのフォルダー `.fx` にTeams。</span><span class="sxs-lookup"><span data-stu-id="41e13-171">The manifest and icons are stored in the `.fx` folder of your project prior to being uploaded to Teams.</span></span> <span data-ttu-id="41e13-172">アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="41e13-172">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="41e13-173">アプリを構成するには、アプリの **[Teams Toolkit]** タブにVisual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="41e13-173">To configure your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="41e13-174">[**マニフェスト エディター] セクション** の **[マニフェスト エディター Project** します。</span><span class="sxs-lookup"><span data-stu-id="41e13-174">Select **Manifest Editor** in the **Project** section.</span></span>

<span data-ttu-id="41e13-175">[アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。</span><span class="sxs-lookup"><span data-stu-id="41e13-175">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="41e13-176">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="41e13-176">Install and run your app locally</span></span>

<span data-ttu-id="41e13-177">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="41e13-177">To build and run your app locally:</span></span>

1. <span data-ttu-id="41e13-178">Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="41e13-178">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="41e13-179">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="41e13-179">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="41e13-180">ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="41e13-180">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="41e13-181">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="41e13-181">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="41e13-182">必要に応じて、ローカル証明書のインストールを求めるメッセージがツールキットに表示されます。</span><span class="sxs-lookup"><span data-stu-id="41e13-182">The toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="41e13-183">この証明書により、Teams は `https://localhost` からアプリケーションを読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="41e13-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="41e13-184">以下のダイアログが表示されたら、「はい」を選択します。</span><span class="sxs-lookup"><span data-stu-id="41e13-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. <span data-ttu-id="41e13-186">アプリケーションを実行するために Web ブラウザーが起動します。</span><span class="sxs-lookup"><span data-stu-id="41e13-186">Your web browser is started to run the application.</span></span> <span data-ttu-id="41e13-187">Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="41e13-187">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="41e13-188">また、他の場合は、アプリケーションに切り替Teams表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="41e13-188">You may also be prompted to switch to the Teams application at other times.</span></span> <span data-ttu-id="41e13-189">このような場合は、Web アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="41e13-189">Select the web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. <span data-ttu-id="41e13-191">サインインするように求めるメッセージが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="41e13-191">You may be prompted to sign in.</span></span>  <span data-ttu-id="41e13-192">その場合は、M365 アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="41e13-192">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="41e13-193">Teams へのアプリのインストールを促すメッセージが表示された場合は、**[追加]** を押してください。</span><span class="sxs-lookup"><span data-stu-id="41e13-193">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="41e13-194">バックエンドとフロントエンドの両方が、アプリケーション デバッガー Visual Studio Codeされます。</span><span class="sxs-lookup"><span data-stu-id="41e13-194">Both the backend and frontend are hooked into the Visual Studio Code debugger.</span></span>  <span data-ttu-id="41e13-195">これにより、コード内の任意の場所にブレークポイントを設定し、状態を検査できます。</span><span class="sxs-lookup"><span data-stu-id="41e13-195">This allows you to set breakpoints anywhere in your code and inspect state.</span></span>  <span data-ttu-id="41e13-196">また、ブラウザー内でフロントエンド デバッグ ツール (開発者向けツールReactなど) を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="41e13-196">You can also use any frontend debugging tools (such as the React Developer Tools) within the browser.</span></span>  <span data-ttu-id="41e13-197">デバッグの詳細については、Visual Studio Codeを[参照してください](https://code.visualstudio.com/Docs/editor/debugging)。</span><span class="sxs-lookup"><span data-stu-id="41e13-197">For more information about debugging in Visual Studio Code, review [the documentation](https://code.visualstudio.com/Docs/editor/debugging).</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="41e13-198">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="41e13-198">Publish your app to Teams</span></span>

<span data-ttu-id="41e13-199">他のユーザーがアプリを使用する前に、アプリを開発者ポータルに発行して、他のユーザー Teams。</span><span class="sxs-lookup"><span data-stu-id="41e13-199">Before it can be used by other people, you must publish your app to the Developer Portal for Teams.</span></span>

1. <span data-ttu-id="41e13-200">アプリを発行するには、アプリの **[Teams Toolkit]** タブにVisual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="41e13-200">To publish your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="41e13-201">[**発行] をTeams** セクションで **Project** します。</span><span class="sxs-lookup"><span data-stu-id="41e13-201">Select **Publish to Teams** in the **Project** section.</span></span>

<span data-ttu-id="41e13-202">Azure ホスティングを使用する場合は、クラウドにプロビジョニングして展開している必要があります。</span><span class="sxs-lookup"><span data-stu-id="41e13-202">If using Azure hosting, you must have provisioned and deployed to the cloud.</span></span> <span data-ttu-id="41e13-203">文書の公開プロセスの詳細については、「SPFxチュートリアル」[をSPFxしてください](../get-started/first-app-spfx.md)。</span><span class="sxs-lookup"><span data-stu-id="41e13-203">For a walk-through of the SPFx publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="41e13-204">次の手順</span><span class="sxs-lookup"><span data-stu-id="41e13-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="41e13-205">発行済みアプリの保守とサポート</span><span class="sxs-lookup"><span data-stu-id="41e13-205">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
