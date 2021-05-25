---
title: アプリとアプリのMicrosoft Teams ToolkitをVisual Studio Code
description: アプリを使用して、アプリ内で直接素晴らしいカスタム Visual Studio Codeを構築Microsoft Teams Toolkit
keywords: teams visual studio コード ツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: d51ccf3ed62e22fb417eec72d1f409b1b77b9da6
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629838"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="b3fe5-104">アプリとアプリのTeams ToolkitをVisual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b3fe5-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="b3fe5-105">Microsoft Teams ツールキットを使用すると、Visual Studio Code 環境内で直接カスタムの Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="b3fe5-106">ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="b3fe5-107">アプリケーションのインストールTeams Toolkit</span><span class="sxs-lookup"><span data-stu-id="b3fe5-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="b3fe5-108">このMicrosoft Teams ToolkitはVisual Studio Code[マーケット](https://aka.ms/teams-toolkit)プレースから、またはVisual Studio内の拡張機能として直接ダウンロードVisual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="b3fe5-109">インストール後、アクティビティ バーにTeams ToolkitがVisual Studio Code表示されます。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="b3fe5-110">表示されない場合は、アクティビティ バー内を右クリックし、[Microsoft Teams]を選択してツールキットをピン留めして簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="b3fe5-111">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="b3fe5-111">Using the toolkit</span></span>

- [<span data-ttu-id="b3fe5-112">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="b3fe5-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="b3fe5-113">既存のプロジェクトをインポートする</span><span class="sxs-lookup"><span data-stu-id="b3fe5-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="b3fe5-114">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="b3fe5-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="b3fe5-115">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="b3fe5-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="b3fe5-116">アプリをローカルまたはローカルで実行Teams</span><span class="sxs-lookup"><span data-stu-id="b3fe5-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="b3fe5-117">新しいプロジェクトをTeamsする</span><span class="sxs-lookup"><span data-stu-id="b3fe5-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="b3fe5-118">ローカル環境でプロジェクトのワークスペースまたはフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-118">Create a workspace or folder for your project in your local environment.</span></span>
1. <span data-ttu-id="b3fe5-119">[Visual Studio Code] アイコンをTeamsします。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-119">In Visual Studio Code, select the Teams icon</span></span> ![Teams アイコン](../assets/icons/favicon-16x16.png) <span data-ttu-id="b3fe5-121">ウィンドウの左側のアクティビティ バーから。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="b3fe5-122">[**コマンド メニューからMicrosoft Teams Toolkit** を開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="b3fe5-123">コマンド **メニューから [新Teamsアプリ** を作成する] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="b3fe5-124">プロンプトが表示されたら、ワークスペースの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="b3fe5-125">これは、プロジェクトが存在するフォルダーの名前と、アプリの既定の名前の両方として使用されます。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="b3fe5-126">Enter **キーを** 押すと、[機能の追加 **] 画面が** 表示され、新しいアプリのプロパティが構成されます。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="b3fe5-127">[完了] **ボタンを** 選択して構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="b3fe5-128">既存のアプリ プロジェクトTeamsインポートする</span><span class="sxs-lookup"><span data-stu-id="b3fe5-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="b3fe5-129">[Visual Studio Code] アイコンをTeamsします。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-129">In Visual Studio Code, select the Teams icon</span></span> ![Teams アイコン](../assets/icons/favicon-16x16.png) <span data-ttu-id="b3fe5-131">ウィンドウの左側のアクティビティ バーから。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="b3fe5-132">コマンド メニュー **から [アプリ パッケージの** インポート] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="b3fe5-133">アプリ パッケージの zip ファイルTeams[既存のファイルを](/microsoftteams/platform/concepts/build-and-test/apps-package?view=msteams-client-js-latest&preserve-view=true)選択します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-133">Choose your existing Teams [app package](/microsoftteams/platform/concepts/build-and-test/apps-package?view=msteams-client-js-latest&preserve-view=true) zip file.</span></span>
1. <span data-ttu-id="b3fe5-134">[発行パッケージ **の選択] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="b3fe5-135">これで、ツールキットの構成タブにアプリの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="b3fe5-136">[Visual Studio Code] で[ワークスペースにフォルダーを追加] を選択して、ソース コード ディレクトリをワークスペースに  ->  Visual Studio Codeします。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="b3fe5-137">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="b3fe5-137">Configure your app</span></span>

<span data-ttu-id="b3fe5-138">このアプリの中核となるのは、Teams 3 つのコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="b3fe5-139">ユーザー Microsoft Teamsアプリを操作するクライアント (Web、デスクトップ、モバイル) を指定します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="b3fe5-140">サーバーに表示されるコンテンツの要求に応答するTeams。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-140">A server that responds to requests for content that will be displayed in Teams.</span></span> <span data-ttu-id="b3fe5-141">たとえば、HTML タブ コンテンツやボットアダプティブ カードなどです。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-141">For example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="b3fe5-142">アプリ Teamsは、次の 3 つのファイルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-142">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="b3fe5-143">このmanifest.jsオンです。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-143">The manifest.json.</span></span> 
      > - <span data-ttu-id="b3fe5-144">パブリック [または組織](../resources/schema/manifest-schema.md#icons) のアプリ カタログに表示するアプリの色アイコン。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="b3fe5-145">アクティビティ[バーに](../resources/schema/manifest-schema.md#icons)表示するアウトライン Teamsアイコン。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="b3fe5-146">アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="b3fe5-147">アプリを構成するには、アプリの **[Microsoft Teams Toolkit]** タブにVisual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-147">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="b3fe5-148">[アプリ **パッケージの編集] を** 選択して、[ **アプリの詳細] ページを表示** します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-148">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="b3fe5-149">[アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-149">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="b3fe5-150">詳細については、「App Studio マニフェスト [エディター」を参照してください。](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="b3fe5-150">For more information, See [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="b3fe5-151">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="b3fe5-151">Package your app</span></span>

<span data-ttu-id="b3fe5-152">アプリの .publish **フォルダー** でアプリの詳細ページ、マニフェスト、または **.env** ファイルを **変更** すると、アプリのファイルが自動的にDevelopment.zipされます。 </span><span class="sxs-lookup"><span data-stu-id="b3fe5-152">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="b3fe5-153">同じフォルダーに 2 [つのアイコン](../concepts/build-and-test/apps-package.md#app-icons) を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-153">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="b3fe5-154">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="b3fe5-154">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="b3fe5-155">アプリの実行</span><span class="sxs-lookup"><span data-stu-id="b3fe5-155">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="b3fe5-156">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="b3fe5-156">Install and run your app locally</span></span>

<span data-ttu-id="b3fe5-157">アプリをパッケージ **化してテストする** 方法の詳細な手順については、プロジェクトのホームページのビルドと実行のコンテンツを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-157">Refer to the **Build and Run** content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="b3fe5-158">一般に、アプリのサーバーをインストールし、実行してからトンネリング ソリューションをセットアップし、Teams localhost から実行されているコンテンツにアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-158">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="b3fe5-159">localhost からの開発を有効にする</span><span class="sxs-lookup"><span data-stu-id="b3fe5-159">Enable development from localhost</span></span>

<span data-ttu-id="b3fe5-160">HTTPS を使用して localhost でタブ ベースのアプリをデバッグする場合は、ブラウザーに対して、サービスを提供するアプリを信頼するように伝える必要があります `<https://localhost>` 。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-160">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from `<https://localhost>`.</span></span> <span data-ttu-id="b3fe5-161">`<https://localhost:3000/tab>` に移動します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-161">Navigate to `<https://localhost:3000/tab>`.</span></span> <span data-ttu-id="b3fe5-162">サイトが信頼されていないという警告が表示される場合は、続行するオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-162">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="b3fe5-163">これで、アプリはクライアントからアクセスTeams必要があります。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-163">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="b3fe5-164">アプリをアプリで実行Teams</span><span class="sxs-lookup"><span data-stu-id="b3fe5-164">Run your app in Teams</span></span>

<span data-ttu-id="b3fe5-165">前提条件:[開発者Teamsモードを有効にする](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="b3fe5-165">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="b3fe5-166">ウィンドウの左側にあるアクティビティ バーにVisual Studio Codeします。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-166">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="b3fe5-167">[実行] **アイコンを** 選択して、[実行] ビュー **と [デバッグ] ビューを表示** します。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-167">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="b3fe5-168">キーボード ショートカットを使用することもできます `Ctrl+Shift+D` 。</span><span class="sxs-lookup"><span data-stu-id="b3fe5-168">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

## <a name="next-step"></a><span data-ttu-id="b3fe5-169">次の手順</span><span class="sxs-lookup"><span data-stu-id="b3fe5-169">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b3fe5-170">発行済みアプリの保守とサポート</span><span class="sxs-lookup"><span data-stu-id="b3fe5-170">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
