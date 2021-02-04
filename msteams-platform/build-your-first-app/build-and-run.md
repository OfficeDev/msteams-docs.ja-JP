---
title: 開始する - 最初のアプリをビルドして実行する
author: heath-hamilton
description: "\"Hello, World!\" を表示する Microsoft Teams アプリをすばやく作成します。 Microsoft Teams を使用したメッセージToolkit。"
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093951"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="e5b0e-104">最初の Microsoft Teams アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="e5b0e-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="e5b0e-105">"Hello, World!" を表示する個人用タブを作成して、Microsoft Teams の開発を開始します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-105">Start Microsoft Teams development by building a personal tab that displays "Hello, World!".</span></span>
<span data-ttu-id="e5b0e-106">次の手順を使用して、最初の Teams アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-106">Build and run your first Teams app using the following steps:</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="e5b0e-107">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="e5b0e-107">1. Create your app project</span></span>

<span data-ttu-id="e5b0e-108">最初のアプリ プロジェクトToolkitセットアップVisual Studioコードで Microsoft Teams プロジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span> <span data-ttu-id="e5b0e-109">次の手順を使用して、アプリ プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-109">Create your app project using the following steps:</span></span>

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. <span data-ttu-id="e5b0e-111">ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-111">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="e5b0e-112">[機能 **の追加] 画面で、[Tab]** を選択し **、[次へ** ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams プロジェクトを使用してアプリ プロジェクトをToolkit。":::
1. <span data-ttu-id="e5b0e-114">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-114">Enter a name for your Teams app.</span></span> <span data-ttu-id="e5b0e-115">(これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-115">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="e5b0e-116">[個人用]**タブオプションのみを** オンにし、画面の下部にある [完了] を選択してプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-116">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="e5b0e-117">2. 重要なアプリ プロジェクト コンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="e5b0e-117">2. Understand important app project components</span></span>

<span data-ttu-id="e5b0e-118">ツールキットでプロジェクトを構成すると、Teams の基本的な個人用タブを構築するためのコンポーネントが作成されます。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-118">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="e5b0e-119">プロジェクト ディレクトリとファイルは、プロジェクト コードのエクスプローラー領域Visual Studioされます。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-119">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="[コード] の [個人用] タブのアプリ プロジェクト ファイルVisual Studioスクリーンショット。":::

### <a name="app-scaffolding"></a><span data-ttu-id="e5b0e-121">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="e5b0e-121">App scaffolding</span></span>

<span data-ttu-id="e5b0e-122">ツールキットは、セットアップ時に追加した機能に基づいて、ディレクトリにスキャフォールディング `src` を自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-122">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="e5b0e-123">たとえば、セットアップ中にタブを作成する場合は、アプリの初期化とルーティングを処理するディレクトリ内のファイル `App.js` `src/components` が重要です。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-123">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="e5b0e-124">Microsoft [Teams JavaScript クライアント SDK を呼び出](../tabs/how-to/using-teams-client-sdk.md) して、アプリと Teams の間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-124">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="e5b0e-125">アプリ ID</span><span class="sxs-lookup"><span data-stu-id="e5b0e-125">App ID</span></span>

<span data-ttu-id="e5b0e-126">Teams アプリ ID を使用して App Studio でアプリを構成します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-126">Configure your app with App Studio using the Teams app ID.</span></span> <span data-ttu-id="e5b0e-127">プロジェクトのファイルにある `teamsAppId` オブジェクト内の ID を検索 `package.json` します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-127">Find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="e5b0e-128">3. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="e5b0e-128">3. Build and run your app</span></span>

<span data-ttu-id="e5b0e-129">時間を節約するために、ローカルでアプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-129">Build and run your app locally to save time.</span></span> <span data-ttu-id="e5b0e-130">この情報は、ツールキットでも利用できます `README` 。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-130">This information is also available in the toolkit `README`.</span></span> <span data-ttu-id="e5b0e-131">次の手順を使用して、アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-131">Build and run your app using the following steps:</span></span>

1. <span data-ttu-id="e5b0e-132">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="e5b0e-133">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-133">Run `npm start`.</span></span>

<span data-ttu-id="e5b0e-134">完了すると、コンパイルに **成功します。**</span><span class="sxs-lookup"><span data-stu-id="e5b0e-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="e5b0e-135">メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-135">message in the terminal.</span></span> <span data-ttu-id="e5b0e-136">アプリが実行されています `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="e5b0e-137">4. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="e5b0e-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="e5b0e-138">アプリは Teams でテストする準備が整っています。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="e5b0e-139">これを行うには、アプリのサイドローディングを許可する Microsoft 365 開発アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-139">To do this, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="e5b0e-140">アカウントを開く方法について詳しくは、Teams の開発アカウント [をご覧ください](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-140">For more information on account opening, see [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).</span></span> 

> [!TIP]
> <span data-ttu-id="e5b0e-141">アプリをサイドロードする前に、ツールキットに含まれている [App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)の検証機能を使用して問題を確認します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-141">Check for issues before sideloading your app, using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="e5b0e-142">エラーを修正して、アプリを正常にサイドローディングします。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-142">Fix the errors to successfully sideload the app.</span></span>

<span data-ttu-id="e5b0e-143">次の手順を使用して、Teams でアプリをサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-143">Sideload your app in Teams using the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="e5b0e-144">Teams でアプリをサイドローディングする前にサイドローディングを有効にするには、「アプリのサイドローディングを有効にする」の [手順に従います](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-144">To enable sideloading before you sideload your app in Teams, follow the steps in [Turn on app sideloading](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

1. <span data-ttu-id="e5b0e-145">**F5 キーを選択** して、Teams の Web クライアントを Visual Studioします。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-145">Select the **F5** key to launch a Teams web client in Visual Studio Code.</span></span>
1. <span data-ttu-id="e5b0e-146">Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 ( `localhost` ) が信頼できる場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-146">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="e5b0e-147">F5 キーを押した後に開いた同じブラウザー ウィンドウ (Google Chrome 既定) で新しいタブ **を開きます**。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-147">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="e5b0e-148">ページに `https://localhost:3000/tab` 移動し、ページに進みます。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-148">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="e5b0e-149">Teams に戻る。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-149">Go back to Teams.</span></span> <span data-ttu-id="e5b0e-150">ダイアログで、[追加] **を選択してアプリ** をインストールします。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-150">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で実行されている &quot;Hello, World!&quot; 個人用タブ アプリの例を示すスクリーンショット。":::

<span data-ttu-id="e5b0e-152">🎉おめでとうございます。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-152">🎉 Congratulations!</span></span> <span data-ttu-id="e5b0e-153">アプリが Teams で実行されている。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-153">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="e5b0e-154">次の手順</span><span class="sxs-lookup"><span data-stu-id="e5b0e-154">Next step</span></span>

<span data-ttu-id="e5b0e-155">作成した個人用タブを展開するか、別の種類の Teams アプリをビルドします。</span><span class="sxs-lookup"><span data-stu-id="e5b0e-155">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5b0e-156">個人用タブに追加する</span><span class="sxs-lookup"><span data-stu-id="e5b0e-156">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="e5b0e-157">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="e5b0e-157">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="e5b0e-158">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="e5b0e-158">Build a bot</span></span>](../build-your-first-app/build-bot.md)
