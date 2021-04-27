---
title: Microsoft Teams のコードとコードを使用ToolkitアプリVisual Studioする
description: Microsoft Teams アプリケーションを使用して、コード内でVisual Studioカスタム アプリを直接構築Toolkit
keywords: teams visual studio コード ツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 59f2943f37856c42346b2ffad4e01d88910679ae
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020262"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="d5c1f-104">Teams のコードとコードを使用ToolkitアプリVisual Studioする</span><span class="sxs-lookup"><span data-stu-id="d5c1f-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="d5c1f-105">Microsoft Teams ツールキットを使用すると、Visual Studio Code 環境内で直接カスタムの Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="d5c1f-106">ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="d5c1f-107">Teams サーバーのインストールToolkit</span><span class="sxs-lookup"><span data-stu-id="d5c1f-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="d5c1f-108">Microsoft Teams Toolkit Visual Studioコードは、Visual Studio [Marketplace](https://aka.ms/teams-toolkit) から、または Visual Studio コード内の拡張機能としてVisual Studioできます。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="d5c1f-109">インストール後、[コード] アクティビティ バーに Teams ToolkitがVisual Studio表示されます。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="d5c1f-110">設定されていない場合は、アクティビティ バー内を右クリックし **、[Microsoft Teams]** を選択してツールキットをピン留めして簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="d5c1f-111">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="d5c1f-111">Using the toolkit</span></span>

- [<span data-ttu-id="d5c1f-112">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="d5c1f-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="d5c1f-113">既存のプロジェクトをインポートする</span><span class="sxs-lookup"><span data-stu-id="d5c1f-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="d5c1f-114">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="d5c1f-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="d5c1f-115">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="d5c1f-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="d5c1f-116">アプリをローカルまたは Teams で実行する</span><span class="sxs-lookup"><span data-stu-id="d5c1f-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="d5c1f-117">新しい Teams プロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="d5c1f-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="d5c1f-118">ローカル環境でプロジェクトのワークスペース/フォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-118">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="d5c1f-119">[Visual Studioコード] で、[Teams] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-119">In Visual Studio Code, select the Teams icon</span></span> ![Teams アイコン](../assets/icons/favicon-16x16.png) <span data-ttu-id="d5c1f-121">ウィンドウの左側のアクティビティ バーから。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="d5c1f-122">コマンド **メニューから [Microsoft Teams Toolkit** 開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="d5c1f-123">コマンド メニュー **から [新しい Teams アプリの** 作成] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="d5c1f-124">プロンプトが表示されたら、ワークスペースの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="d5c1f-125">これは、プロジェクトが存在するフォルダーの名前と、アプリの既定の名前の両方として使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="d5c1f-126">Enter **キーを** 押すと、[機能の追加 **] 画面が** 表示され、新しいアプリのプロパティが構成されます。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="d5c1f-127">[完了] **ボタンを** 選択して構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="d5c1f-128">既存の Teams アプリ プロジェクトをインポートする</span><span class="sxs-lookup"><span data-stu-id="d5c1f-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="d5c1f-129">[Visual Studioコード] で、[Teams] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-129">In Visual Studio Code, select the Teams icon</span></span> ![Teams アイコン](../assets/icons/favicon-16x16.png) <span data-ttu-id="d5c1f-131">ウィンドウの左側のアクティビティ バーから。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="d5c1f-132">コマンド メニュー **から [アプリ パッケージの** インポート] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="d5c1f-133">既存の Teams アプリ パッケージ [の zip ファイルを](../concepts/build-and-test/apps-package.md) 選択します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="d5c1f-134">[発行パッケージ **の選択] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="d5c1f-135">これで、ツールキットの構成タブにアプリの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="d5c1f-136">[Visual Studio コード] で、[ワークスペースにフォルダーを追加する] を選択して、ソース コード ディレクトリを [コード]  ->  ワークスペースVisual Studio追加します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="d5c1f-137">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="d5c1f-137">Configure your app</span></span>

<span data-ttu-id="d5c1f-138">Teams アプリの中核となるのは、次の 3 つのコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="d5c1f-139">ユーザーがアプリを操作する Microsoft Teams クライアント (Web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="d5c1f-140">Teams に表示されるコンテンツの要求 (HTML タブ コンテンツやボットアダプティブ カードなど) に応答するサーバー。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-140">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="d5c1f-141">3 [つのファイルで構成](/concepts/build-and-test/apps-package.md) される Teams アプリ パッケージ。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-141">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="d5c1f-142">[manifest.js]</span><span class="sxs-lookup"><span data-stu-id="d5c1f-142">The manifest.json</span></span> 
  > - <span data-ttu-id="d5c1f-143">パブリック [または組織の](../resources/schema/manifest-schema.md#icons) アプリ カタログに表示するアプリの色アイコン</span><span class="sxs-lookup"><span data-stu-id="d5c1f-143">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="d5c1f-144">Teams [アクティビティ バー](../resources/schema/manifest-schema.md#icons) に表示するアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-144">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="d5c1f-145">アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-145">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="d5c1f-146">アプリを構成するには、[コード] の **[Microsoft Teams Toolkit]** タブVisual Studioします。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-146">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="d5c1f-147">[アプリ **パッケージの編集] を** 選択して、[ **アプリの詳細] ページを表示** します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-147">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="d5c1f-148">[アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-148">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="d5c1f-149">*「App* [Studio マニフェスト エディター」を参照してください。](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="d5c1f-149">*See* [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="d5c1f-150">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="d5c1f-150">Package your app</span></span>

<span data-ttu-id="d5c1f-151">アプリの .publish **フォルダー** でアプリの詳細ページ、マニフェスト、または **.env** ファイルを **変更** すると、アプリのファイルが自動的にDevelopment.zipされます。 </span><span class="sxs-lookup"><span data-stu-id="d5c1f-151">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="d5c1f-152">同じフォルダーに 2 [つのアイコン](../concepts/build-and-test/apps-package.md#app-icons) を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-152">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="d5c1f-153">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="d5c1f-153">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="d5c1f-154">アプリの実行</span><span class="sxs-lookup"><span data-stu-id="d5c1f-154">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="d5c1f-155">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="d5c1f-155">Install and run your app locally</span></span>

<span data-ttu-id="d5c1f-156">アプリをパッケージ化 *してテストする* 方法の詳細な手順については、プロジェクトのホームページの \*Build and Run コンテンツを参照してください。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-156">Refer to the \**Build and Run* content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="d5c1f-157">一般に、アプリのサーバーをインストールし、それを実行してから、Teams が localhost から実行されているコンテンツにアクセスできるよう、トンネリング ソリューションをセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-157">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="d5c1f-158">localhost からの開発を有効にする</span><span class="sxs-lookup"><span data-stu-id="d5c1f-158">Enable development from localhost</span></span>

<span data-ttu-id="d5c1f-159">HTTPS を使用して localhost でタブ ベースのアプリをデバッグする場合は、ブラウザーに対して、サービスを提供するアプリを信頼するように伝える必要があります <https://localhost> 。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-159">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="d5c1f-160"><https://localhost:3000/tab> に移動します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-160">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="d5c1f-161">サイトが信頼されていないという警告が表示される場合は、続行するオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-161">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="d5c1f-162">これで、Teams クライアントからアプリにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-162">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="d5c1f-163">Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="d5c1f-163">Run your app in Teams</span></span>

<span data-ttu-id="d5c1f-164">前提条件: [Teams 開発者プレビュー モードを有効にする](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="d5c1f-164">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="d5c1f-165">[コード] ウィンドウの左側にあるアクティビティ バー Visual Studio移動します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-165">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="d5c1f-166">[実行] **アイコンを** 選択して、[実行] ビュー **と [デバッグ] ビューを表示** します。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-166">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="d5c1f-167">キーボード ショートカットを使用することもできます `Ctrl+Shift+D` 。</span><span class="sxs-lookup"><span data-stu-id="d5c1f-167">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5c1f-168">次の手順: 発行済みアプリの保守とサポート</span><span class="sxs-lookup"><span data-stu-id="d5c1f-168">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
