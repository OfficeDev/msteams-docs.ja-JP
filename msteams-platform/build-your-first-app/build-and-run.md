---
title: 作業の開始-最初のアプリをビルドして実行する
author: heath-hamilton
description: "\"Hello, World!\" を表示する Microsoft Teams アプリをすばやく作成する Microsoft Teams ツールキットを使用したメッセージ。"
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 62c4bd950183ceb64fb30b528661cf84e9210d89
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931779"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="f21e4-104">最初の Microsoft Teams アプリを構築して実行する</span><span class="sxs-lookup"><span data-stu-id="f21e4-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="f21e4-105">"Hello, World!" と表示される個人タブを作成することによって、Microsoft Teams 開発に直接ジャンプできます。</span><span class="sxs-lookup"><span data-stu-id="f21e4-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="f21e4-106">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-106">1. Create your app project</span></span>

<span data-ttu-id="f21e4-107">最初のアプリプロジェクトをセットアップするには、Visual Studio Code の Microsoft Teams ツールキットを使用します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成** ] を選択します。
1. <span data-ttu-id="f21e4-109">メッセージが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="f21e4-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="f21e4-110">[ **機能の追加** ] 画面で、[ **タブ]** 、[ **次へ** ] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams Toolkit を使用してアプリプロジェクトを構成する方法を示すスクリーンショット。":::
1. <span data-ttu-id="f21e4-112">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="f21e4-113">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="f21e4-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="f21e4-114">[ **個人用] タブ** のオプションのみをチェックし、画面の下部にある [ **完了** ] を選択してプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="f21e4-115">2. 重要なアプリプロジェクトコンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="f21e4-115">2. Understand important app project components</span></span>

<span data-ttu-id="f21e4-116">ツールキットによってプロジェクトが構成されると、Teams 用の基本的な個人用タブを作成するためのコンポーネントが用意されます。</span><span class="sxs-lookup"><span data-stu-id="f21e4-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="f21e4-117">プロジェクトのディレクトリとファイルは、Visual Studio Code のエクスプローラー領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f21e4-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Visual Studio Code の [個人用] タブのアプリプロジェクトファイルを示すスクリーンショット。":::

### <a name="app-scaffolding"></a><span data-ttu-id="f21e4-119">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="f21e4-119">App scaffolding</span></span>

<span data-ttu-id="f21e4-120">このツールキットは、 `src` セットアップ時に追加された機能に基づいてディレクトリ内に自動的にスキャフォールディングを作成します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-120">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="f21e4-121">たとえば、セットアップ時にタブを作成した場合、 `App.js` ディレクトリ内のファイル `src/components` は、アプリの初期化とルーティングを処理するので重要です。</span><span class="sxs-lookup"><span data-stu-id="f21e4-121">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="f21e4-122">[Microsoft TEAMS SDK](../tabs/how-to/using-teams-client-sdk.md)を呼び出して、アプリと teams 間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-122">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="f21e4-123">アプリ ID</span><span class="sxs-lookup"><span data-stu-id="f21e4-123">App ID</span></span>

<span data-ttu-id="f21e4-124">Teams アプリ ID は、アプリをアプリ Studio で構成するために必要です。</span><span class="sxs-lookup"><span data-stu-id="f21e4-124">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="f21e4-125">ID は、 `teamsAppId` プロジェクトのファイル内にあるオブジェクトで見つけることができ `package.json` ます。</span><span class="sxs-lookup"><span data-stu-id="f21e4-125">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="f21e4-126">3. アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-126">3. Build and run your app</span></span>

<span data-ttu-id="f21e4-127">時間の経過とともに、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-127">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="f21e4-128">(この情報は、ツールキットでも利用でき `README` ます。)</span><span class="sxs-lookup"><span data-stu-id="f21e4-128">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="f21e4-129">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-129">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="f21e4-130">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-130">Run `npm start`.</span></span>

<span data-ttu-id="f21e4-131">完了すると、 **コンパイルに成功** しました。</span><span class="sxs-lookup"><span data-stu-id="f21e4-131">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="f21e4-132">ターミナルのメッセージ。</span><span class="sxs-lookup"><span data-stu-id="f21e4-132">message in the terminal.</span></span> <span data-ttu-id="f21e4-133">アプリが実行されている `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="f21e4-133">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="f21e4-134">4. アプリを Teams でサイドロード</span><span class="sxs-lookup"><span data-stu-id="f21e4-134">4. Sideload your app in Teams</span></span>

<span data-ttu-id="f21e4-135">アプリは Teams でテストする準備ができています。</span><span class="sxs-lookup"><span data-stu-id="f21e4-135">Your app is ready to test in Teams.</span></span> <span data-ttu-id="f21e4-136">これを行うには、アプリのサイドロードを許可するアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="f21e4-136">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="f21e4-137">(あるかどうかがわからない場合は、 [Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)の取得についてを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="f21e4-137">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="f21e4-138">アプリのサイドロード前に、ツールキットに含まれている [アプリ Studio の検証機能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)を使用して、問題点を確認します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-138">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="f21e4-139">アプリケーションを正常にサイドロードするには、エラーを修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f21e4-139">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="f21e4-140">Visual Studio Code で、 **F5** キーを押して Teams web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-140">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="f21e4-141">Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 () を信頼するように指定し `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="f21e4-141">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="f21e4-142">**F5** キーを押した後に開いた同じブラウザーウィンドウ (既定では Google Chrome) で新しいタブを開きます。</span><span class="sxs-lookup"><span data-stu-id="f21e4-142">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="f21e4-143">に移動 `https://localhost:3000/tab` して、ページに進みます。</span><span class="sxs-lookup"><span data-stu-id="f21e4-143">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="f21e4-144">Teams に戻ります。</span><span class="sxs-lookup"><span data-stu-id="f21e4-144">Go back to Teams.</span></span> <span data-ttu-id="f21e4-145">ダイアログボックスで、[ **追加** ] を選択してアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f21e4-145">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で実行されている ' Hello, World! ' personal tab アプリの例を示すスクリーンショット。":::

<span data-ttu-id="f21e4-147">おめでとうございます🎉</span><span class="sxs-lookup"><span data-stu-id="f21e4-147">🎉 Congratulations!</span></span> <span data-ttu-id="f21e4-148">アプリは Teams で実行されています。</span><span class="sxs-lookup"><span data-stu-id="f21e4-148">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="f21e4-149">次の手順</span><span class="sxs-lookup"><span data-stu-id="f21e4-149">Next step</span></span>

<span data-ttu-id="f21e4-150">作成したばかりの [個人] タブを展開するか、別の種類の Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="f21e4-150">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="f21e4-151">[[個人用] タブに追加する](../build-your-first-app/build-personal-tab.md)</span><span class="sxs-lookup"><span data-stu-id="f21e4-151">[Add to your personal tab](../build-your-first-app/build-personal-tab.md)</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f21e4-152">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="f21e4-152">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="f21e4-153">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="f21e4-153">Build a bot</span></span>](../build-your-first-app/build-bot.md)
