---
title: はじめに - 最初のアプリを構築して実行する
author: heath-hamilton
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 Microsoft Teams のツールキットを使用したメッセージ。"
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093951"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="3fa42-104">最初の Microsoft Teams アプリを構築して実行する</span><span class="sxs-lookup"><span data-stu-id="3fa42-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="3fa42-105">"こんにちは!!" を表示する個人タブを構築することから Microsoft Teams の開発を開始します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-105">Start Microsoft Teams development by building a personal tab that displays "Hello, World!".</span></span>
<span data-ttu-id="3fa42-106">以下の手順で、最初の Teams アプリを構築して実行します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-106">Build and run your first Teams app using the following steps:</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="3fa42-107">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="3fa42-107">1. Create your app project</span></span>

<span data-ttu-id="3fa42-108">Visual Studio Code で Microsoft Teams ツールキットを使用して、最初のアプリ プロジェクトを設定します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span> <span data-ttu-id="3fa42-109">以下の手順でアプリ プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-109">Create your app project using the following steps:</span></span>

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. <span data-ttu-id="3fa42-111">メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="3fa42-111">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="3fa42-112">[**機能の追加**] 画面で、[**タブ**] を選択し、[**次へ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams ツールキットを使用して、アプリ プロジェクトを構成する方法を示すスクリーンショット。":::
1. <span data-ttu-id="3fa42-114">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-114">Enter a name for your Teams app.</span></span> <span data-ttu-id="3fa42-115">(これは、アプリの既定の名前であり、ローカル コンピューター上のアプリのプロジェクト ディレクトリの名前でもあります)。</span><span class="sxs-lookup"><span data-stu-id="3fa42-115">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="3fa42-116">[**個人用タブ**] オプションのみをチェックし、画面下の [**終了**] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-116">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="3fa42-117">2. アプリ プロジェクトの重要なコンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="3fa42-117">2. Understand important app project components</span></span>

<span data-ttu-id="3fa42-118">ツールキットでプロジェクトを構成すると、Teams 向けの基本的な個人用タブを構築するためのコンポーネントがあります。</span><span class="sxs-lookup"><span data-stu-id="3fa42-118">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="3fa42-119">プロジェクトのディレクトリとファイルには、Visual Studio Code の [エクスプローラー] 領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="3fa42-119">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Visual Studio Code で個人用タブ向けのアプリのプロジェクト ファイルを表示したスクリーンショット。":::

### <a name="app-scaffolding"></a><span data-ttu-id="3fa42-121">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="3fa42-121">App scaffolding</span></span>

<span data-ttu-id="3fa42-122">ツールキットは、セットアップ時に追加した機能に基づいて、`src` ディレクトリにスキャフォールディングを自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-122">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="3fa42-123">たとえば、セットアップ中にタブを作成した場合、`src/components` ディレクトリ内の `App.js` ファイルは、アプリの初期化とルーティングを処理するため重要です。</span><span class="sxs-lookup"><span data-stu-id="3fa42-123">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="3fa42-124">[Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) を呼び出して、アプリと Teams の間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-124">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="3fa42-125">アプリ ID</span><span class="sxs-lookup"><span data-stu-id="3fa42-125">App ID</span></span>

<span data-ttu-id="3fa42-126">Teams アプリ ID を使用して、App Studio でアプリを構成します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-126">Configure your app with App Studio using the Teams app ID.</span></span> <span data-ttu-id="3fa42-127">プロジェクトの `package.json` ファイルにある `teamsAppId` オブジェクトで ID を検索します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-127">Find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="3fa42-128">3. アプリの構築と実行</span><span class="sxs-lookup"><span data-stu-id="3fa42-128">3. Build and run your app</span></span>

<span data-ttu-id="3fa42-129">アプリをローカルに構築して実行することで、時間を節約できます。</span><span class="sxs-lookup"><span data-stu-id="3fa42-129">Build and run your app locally to save time.</span></span> <span data-ttu-id="3fa42-130">この情報は、ツールキット `README` でも参照できます。</span><span class="sxs-lookup"><span data-stu-id="3fa42-130">This information is also available in the toolkit `README`.</span></span> <span data-ttu-id="3fa42-131">以下の手順を使用して、最初のアプリを構築して実行します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-131">Build and run your app using the following steps:</span></span>

1. <span data-ttu-id="3fa42-132">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="3fa42-133">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-133">Run `npm start`.</span></span>

<span data-ttu-id="3fa42-134">完了すると、[**正常にコンパイルされました**] と表示されます。</span><span class="sxs-lookup"><span data-stu-id="3fa42-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="3fa42-135">ターミナルのメッセージ。</span><span class="sxs-lookup"><span data-stu-id="3fa42-135">message in the terminal.</span></span> <span data-ttu-id="3fa42-136">お使いのアプリは `https://localhost:3000` で動作しています。</span><span class="sxs-lookup"><span data-stu-id="3fa42-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="3fa42-137">4. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="3fa42-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="3fa42-138">お使いのアプリは Teams でテストする準備ができています。</span><span class="sxs-lookup"><span data-stu-id="3fa42-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="3fa42-139">そのためには、アプリのサイドロードを許可する Microsoft 365 開発アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="3fa42-139">To do this, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="3fa42-140">アカウント開設の詳細については、「[Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3fa42-140">For more information on account opening, see [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).</span></span> 

> [!TIP]
> <span data-ttu-id="3fa42-141">ツールキットに含まれる [App Studio の検証機能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool) を使用して、アプリをサイドロードする前に問題がないか確認します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-141">Check for issues before sideloading your app, using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="3fa42-142">エラーを修正して、アプリを正常にサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="3fa42-142">Fix the errors to successfully sideload the app.</span></span>

<span data-ttu-id="3fa42-143">以下の手順を使用して、Teams でアプリをサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="3fa42-143">Sideload your app in Teams using the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="3fa42-144">Teams でアプリをサイドロードする前にサイドロードを有効にするには、[[アプリのサイドロードをオンにする](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)] の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="3fa42-144">To enable sideloading before you sideload your app in Teams, follow the steps in [Turn on app sideloading](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

1. <span data-ttu-id="3fa42-145">**F5** キーを選択すると、Visual Studio Code で Teams Web クライアントが起動します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-145">Select the **F5** key to launch a Teams web client in Visual Studio Code.</span></span>
1. <span data-ttu-id="3fa42-146">アプリ コンテンツを Teams で表示するには、信頼できるアプリを実行する場所 (`localhost`) を指定します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-146">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="3fa42-147">**F5** を押した後に開いたのと同じブラウザー ウィンドウ (既定では Google Chrome) で新しいタブを開きます。</span><span class="sxs-lookup"><span data-stu-id="3fa42-147">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="3fa42-148">`https://localhost:3000/tab` に進み、ページを進めます。</span><span class="sxs-lookup"><span data-stu-id="3fa42-148">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="3fa42-149">Teams に戻ります。</span><span class="sxs-lookup"><span data-stu-id="3fa42-149">Go back to Teams.</span></span> <span data-ttu-id="3fa42-150">ダイアログで [**自分に追加**] を選択して、アプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="3fa42-150">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で動作する個人用タブ アプリの ' こんにちは! ' の例を表示するスクリーンショット。":::

<span data-ttu-id="3fa42-152">🎉 おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="3fa42-152">🎉 Congratulations!</span></span> <span data-ttu-id="3fa42-153">お使いのアプリは Teams で動作しています。</span><span class="sxs-lookup"><span data-stu-id="3fa42-153">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="3fa42-154">次の手順</span><span class="sxs-lookup"><span data-stu-id="3fa42-154">Next step</span></span>

<span data-ttu-id="3fa42-155">先ほど作成した個人用タブの拡張や別のタイプの Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="3fa42-155">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fa42-156">個人用タブに追加</span><span class="sxs-lookup"><span data-stu-id="3fa42-156">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="3fa42-157">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="3fa42-157">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="3fa42-158">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="3fa42-158">Build a bot</span></span>](../build-your-first-app/build-bot.md)
