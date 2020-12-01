---
title: Microsoft Teams Toolkit と Visual Studio コードを使用してアプリをビルドする
description: Microsoft Teams ツールキットを使用して、Visual Studio Code 内で魅力的なカスタムアプリを直接作成する
keywords: teams visual studio code toolkit
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 41b0eeaeef1c7094fc9c8cbdc05c2db899245fc6
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "49476931"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="908fd-104">Teams Toolkit と Visual Studio Code を使用してアプリをビルドする</span><span class="sxs-lookup"><span data-stu-id="908fd-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="908fd-105">Microsoft Teams ツールキットを使用すると、Visual Studio Code 環境内で直接カスタムの Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="908fd-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="908fd-106">ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="908fd-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="908fd-107">Teams ツールキットをインストールする</span><span class="sxs-lookup"><span data-stu-id="908fd-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="908fd-108">Microsoft Teams Toolkit for Visual studio code は、visual [Studio Marketplace](https://aka.ms/teams-toolkit) からダウンロードするか、Visual studio code 内の拡張機能として直接ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="908fd-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="908fd-109">インストール後に、Visual Studio Code アクティビティバーに Teams ツールキットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="908fd-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="908fd-110">表示されていない場合は、アクティビティバー内を右クリックし、[ **Microsoft Teams** ] を選択して、簡単にアクセスできるようにツールキットを固定します。</span><span class="sxs-lookup"><span data-stu-id="908fd-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="908fd-111">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="908fd-111">Using the toolkit</span></span>

- [<span data-ttu-id="908fd-112">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="908fd-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="908fd-113">既存のプロジェクトをインポートする</span><span class="sxs-lookup"><span data-stu-id="908fd-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="908fd-114">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="908fd-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="908fd-115">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="908fd-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="908fd-116">アプリをローカルで、または Teams で実行する</span><span class="sxs-lookup"><span data-stu-id="908fd-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="908fd-117">新しい Teams プロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="908fd-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="908fd-118">ローカル環境でプロジェクトのワークスペース/フォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="908fd-118">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="908fd-119">Visual Studio Code で、Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="908fd-119">In Visual Studio Code, select the Teams icon</span></span> ![Teams アイコン](../assets/icons/favicon-16x16.png) <span data-ttu-id="908fd-121">ウィンドウの左側にあるアクティビティバーから。</span><span class="sxs-lookup"><span data-stu-id="908fd-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="908fd-122">[コマンド] メニューから [ **Microsoft Teams Toolkit** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="908fd-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="908fd-123">[コマンド] メニューから [ **新しい Teams アプリの作成** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="908fd-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="908fd-124">メッセージが表示されたら、ワークスペースの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="908fd-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="908fd-125">これは、プロジェクトが存在するフォルダーの名前と、アプリの既定の名前の両方として使用されます。</span><span class="sxs-lookup"><span data-stu-id="908fd-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="908fd-126">**Enter** キーを押すと、[**機能の追加**] 画面が表示され、新しいアプリのプロパティを構成します。</span><span class="sxs-lookup"><span data-stu-id="908fd-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="908fd-127">[ **完了** ] ボタンを選択して、構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="908fd-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="908fd-128">既存の Teams アプリプロジェクトをインポートする</span><span class="sxs-lookup"><span data-stu-id="908fd-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="908fd-129">Visual Studio Code で、Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="908fd-129">In Visual Studio Code, select the Teams icon</span></span> ![Teams アイコン](../assets/icons/favicon-16x16.png) <span data-ttu-id="908fd-131">ウィンドウの左側にあるアクティビティバーから。</span><span class="sxs-lookup"><span data-stu-id="908fd-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="908fd-132">[コマンド] メニューから [ **アプリパッケージのインポート** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="908fd-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="908fd-133">既存の [Teams アプリパッケージ](../concepts/build-and-test/apps-package.md) の zip ファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="908fd-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="908fd-134">**[発行パッケージの選択**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="908fd-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="908fd-135">これで、ツールキットの [構成] タブにアプリの詳細が設定されます。</span><span class="sxs-lookup"><span data-stu-id="908fd-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="908fd-136">Visual studio code で、[**ファイル**] [  ->  **ワークスペースへのフォルダーの追加**] を選択して、ソースコードディレクトリを visual studio code Workspace に追加します。</span><span class="sxs-lookup"><span data-stu-id="908fd-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="908fd-137">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="908fd-137">Configure your app</span></span>

<span data-ttu-id="908fd-138">主に、Teams アプリは3つのコンポーネントをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="908fd-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="908fd-139">ユーザーがアプリを操作する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="908fd-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="908fd-140">Teams に表示されるコンテンツの要求に応答するサーバー。たとえば、HTML タブのコンテンツや bot のアダプティブカード。</span><span class="sxs-lookup"><span data-stu-id="908fd-140">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="908fd-141">3つのファイルで構成される Teams [アプリパッケージ](/concepts/build-and-test/apps-package.md) :</span><span class="sxs-lookup"><span data-stu-id="908fd-141">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="908fd-142">manifest.js</span><span class="sxs-lookup"><span data-stu-id="908fd-142">The manifest.json</span></span> 
  > - <span data-ttu-id="908fd-143">パブリックまたは組織のアプリカタログに表示するための、アプリの[カラーアイコン](../resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="908fd-143">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="908fd-144">Teams アクティビティバーに表示するための [アウトラインアイコン](../resources/schema/manifest-schema.md#icons) 。</span><span class="sxs-lookup"><span data-stu-id="908fd-144">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="908fd-145">アプリがインストールされると、Teams クライアントはマニフェストファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="908fd-145">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="908fd-146">アプリを構成するには、Visual Studio Code の [ **Microsoft Teams Toolkit** ] タブに移動します。</span><span class="sxs-lookup"><span data-stu-id="908fd-146">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="908fd-147">[ **アプリパッケージの編集** ] を選択して、[ **アプリの詳細** ] ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="908fd-147">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="908fd-148">[アプリの詳細] ページのフィールドを編集すると、最終的にアプリパッケージの一部として配布されるファイルの manifest.jsの内容が更新されます。</span><span class="sxs-lookup"><span data-stu-id="908fd-148">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="908fd-149">*「* [App Studio manifest Editor](https://aka.ms/teams-toolkit-manifest) 」を参照</span><span class="sxs-lookup"><span data-stu-id="908fd-149">*See* [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="908fd-150">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="908fd-150">Package your app</span></span>

<span data-ttu-id="908fd-151">アプリの **詳細** ページを変更するか、**マニフェスト**、またはアプリの **publish** フォルダー内の **env** ファイルを更新すると、 **Development.zip** ファイルが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="908fd-151">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="908fd-152">同じフォルダーに [2 つのアイコン](../concepts/build-and-test/apps-package.md#icons) を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="908fd-152">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="908fd-153">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="908fd-153">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="908fd-154">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="908fd-154">Install and run your app locally</span></span>

<span data-ttu-id="908fd-155">アプリをパッケージ化してテストする方法の詳細については、「プロジェクトホームページのコンテンツを *ビルドして実行* する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="908fd-155">Refer to the \**Build and Run* content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="908fd-156">一般に、アプリのサーバーをインストールし、実行して、トンネリングソリューションをセットアップして、Teams が localhost から実行されているコンテンツにアクセスできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="908fd-156">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="908fd-157">Localhost からの開発を有効にする</span><span class="sxs-lookup"><span data-stu-id="908fd-157">Enable development from localhost</span></span>

<span data-ttu-id="908fd-158">HTTPS を使用して localhost でタブベースのアプリをデバッグする場合は、提供元のアプリが信頼されていることをブラウザーに通知する必要があり <https://localhost> ます。</span><span class="sxs-lookup"><span data-stu-id="908fd-158">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="908fd-159"><https://localhost:3000/tab> に移動します。</span><span class="sxs-lookup"><span data-stu-id="908fd-159">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="908fd-160">サイトが信頼されていないことを示す警告が表示された場合は、そのまま続行するオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="908fd-160">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="908fd-161">これで、アプリは Teams クライアントからアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="908fd-161">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="908fd-162">Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="908fd-162">Run your app in Teams</span></span>

<span data-ttu-id="908fd-163">前提条件: [Teams 開発者プレビューモードを有効にする](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="908fd-163">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="908fd-164">Visual Studio の [コード] ウィンドウの左側にあるアクティビティバーに移動します。</span><span class="sxs-lookup"><span data-stu-id="908fd-164">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="908fd-165">[実行 **] アイコンを** 選択して、[ **実行] および [デバッグ** ] ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="908fd-165">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="908fd-166">キーボードショートカットを使用することもでき `Ctrl+Shift+D` ます。</span><span class="sxs-lookup"><span data-stu-id="908fd-166">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="908fd-167">次のステップ: 公開アプリの管理とサポート</span><span class="sxs-lookup"><span data-stu-id="908fd-167">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
