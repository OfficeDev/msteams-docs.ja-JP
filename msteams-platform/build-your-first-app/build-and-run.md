---
title: 開始する - 最初のアプリをビルドして実行する
author: heath-hamilton
description: "\"Hello, World!\" を表示する Microsoft Teams アプリをすばやく作成します。 Microsoft Teams を使用したメッセージToolkit。"
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: bc5d18dd887cbdbf56b8d6d013f53c21d1540370
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795469"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="c0aec-104">最初の Microsoft Teams アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="c0aec-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="c0aec-105">"Hello, World!" を表示する個人用タブを作成すると、Microsoft Teams 開発に簡単に移動できます。</span><span class="sxs-lookup"><span data-stu-id="c0aec-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="c0aec-106">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="c0aec-106">1. Create your app project</span></span>

<span data-ttu-id="c0aec-107">最初のアプリ プロジェクトToolkitセットアップVisual Studioコードで Microsoft Teams プロジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. <span data-ttu-id="c0aec-109">ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="c0aec-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="c0aec-110">[機能 **の追加] 画面で、[Tab]** を選択し **、[次へ** ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="c0aec-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams プロジェクトを使用してアプリ プロジェクトをToolkit。":::
1. <span data-ttu-id="c0aec-112">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="c0aec-113">(これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。</span><span class="sxs-lookup"><span data-stu-id="c0aec-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="c0aec-114">[個人用]**タブオプションのみを** オンにし、画面の下部にある [完了] を選択してプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="c0aec-115">2. 重要なアプリ プロジェクト コンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="c0aec-115">2. Understand important app project components</span></span>

<span data-ttu-id="c0aec-116">ツールキットでプロジェクトを構成すると、Teams の基本的な個人用タブを構築するためのコンポーネントが提供されます。</span><span class="sxs-lookup"><span data-stu-id="c0aec-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="c0aec-117">プロジェクト ディレクトリとファイルは、プロジェクト コードのエクスプローラー領域Visual Studioされます。</span><span class="sxs-lookup"><span data-stu-id="c0aec-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="[コード] の [個人用] タブのアプリ プロジェクト ファイルVisual Studioスクリーンショット。":::

### <a name="app-scaffolding"></a><span data-ttu-id="c0aec-119">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="c0aec-119">App scaffolding</span></span>

<span data-ttu-id="c0aec-120">ツールキットは、セットアップ時に追加した機能に基づいて、ディレクトリにスキャフォールディング `src` を自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-120">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="c0aec-121">たとえば、セットアップ中にタブを作成する場合は、アプリの初期化とルーティングを処理するディレクトリ内のファイル `App.js` `src/components` が重要です。</span><span class="sxs-lookup"><span data-stu-id="c0aec-121">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="c0aec-122">Microsoft [Teams JavaScript クライアント SDK を呼び出](../tabs/how-to/using-teams-client-sdk.md) して、アプリと Teams の間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-122">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="c0aec-123">アプリ ID</span><span class="sxs-lookup"><span data-stu-id="c0aec-123">App ID</span></span>

<span data-ttu-id="c0aec-124">App Studio でアプリを構成するには、Teams アプリ ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="c0aec-124">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="c0aec-125">ID は、プロジェクト `teamsAppId` のファイルにあるオブジェクト内で確認 `package.json` できます。</span><span class="sxs-lookup"><span data-stu-id="c0aec-125">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="c0aec-126">3. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="c0aec-126">3. Build and run your app</span></span>

<span data-ttu-id="c0aec-127">時間の問題として、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-127">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="c0aec-128">(この情報はツールキットでも利用 `README` できます)。</span><span class="sxs-lookup"><span data-stu-id="c0aec-128">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="c0aec-129">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="c0aec-129">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="c0aec-130">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-130">Run `npm start`.</span></span>

<span data-ttu-id="c0aec-131">完了すると、コンパイルに **成功します。**</span><span class="sxs-lookup"><span data-stu-id="c0aec-131">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="c0aec-132">メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c0aec-132">message in the terminal.</span></span> <span data-ttu-id="c0aec-133">アプリが実行されています `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="c0aec-133">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="c0aec-134">4. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="c0aec-134">4. Sideload your app in Teams</span></span>

<span data-ttu-id="c0aec-135">アプリは Teams でテストする準備が整っています。</span><span class="sxs-lookup"><span data-stu-id="c0aec-135">Your app is ready to test in Teams.</span></span> <span data-ttu-id="c0aec-136">これを行うには、アプリのサイドローディングを許可するアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="c0aec-136">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="c0aec-137">(それが確実でない場合は、Teams 開発アカウントを取得する方法 [について説明します](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account))。</span><span class="sxs-lookup"><span data-stu-id="c0aec-137">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="c0aec-138">アプリをサイドロードする前に、ツールキットに含まれている [App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)の検証機能を使用して問題を確認します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-138">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="c0aec-139">アプリを正常にサイドロードするには、エラーを修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c0aec-139">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="c0aec-140">コードVisual Studio **F5** キーを押して、Teams Web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-140">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="c0aec-141">Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 ( `localhost` ) が信頼できる場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="c0aec-141">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="c0aec-142">F5 キーを押した後に開いた同じブラウザー ウィンドウ (Google Chrome 既定) で新しいタブ **を開きます**。</span><span class="sxs-lookup"><span data-stu-id="c0aec-142">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="c0aec-143">ページに `https://localhost:3000/tab` 移動し、ページに進みます。</span><span class="sxs-lookup"><span data-stu-id="c0aec-143">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="c0aec-144">Teams に戻る。</span><span class="sxs-lookup"><span data-stu-id="c0aec-144">Go back to Teams.</span></span> <span data-ttu-id="c0aec-145">ダイアログで、[追加] **を選択してアプリ** をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c0aec-145">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で実行されている &quot;Hello, World!&quot; 個人用タブ アプリの例を示すスクリーンショット。":::

<span data-ttu-id="c0aec-147">🎉おめでとうございます。</span><span class="sxs-lookup"><span data-stu-id="c0aec-147">🎉 Congratulations!</span></span> <span data-ttu-id="c0aec-148">アプリが Teams で実行されている。</span><span class="sxs-lookup"><span data-stu-id="c0aec-148">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="c0aec-149">次の手順</span><span class="sxs-lookup"><span data-stu-id="c0aec-149">Next step</span></span>

<span data-ttu-id="c0aec-150">作成した個人用タブを展開するか、別の種類の Teams アプリをビルドします。</span><span class="sxs-lookup"><span data-stu-id="c0aec-150">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0aec-151">個人用タブに追加する</span><span class="sxs-lookup"><span data-stu-id="c0aec-151">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="c0aec-152">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="c0aec-152">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="c0aec-153">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="c0aec-153">Build a bot</span></span>](../build-your-first-app/build-bot.md)
