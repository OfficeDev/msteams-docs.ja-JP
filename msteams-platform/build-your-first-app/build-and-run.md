---
title: 作業の開始-最初のアプリをビルドして実行する
author: heath-hamilton
description: "\"Hello, World!\" を表示する Microsoft Teams アプリをすばやく作成する Microsoft Teams ツールキットを使用したメッセージ。"
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 2d357ef71bfc4c498b54d94f9d0717cf886df17d
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552480"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="5fa8d-104">最初の Microsoft Teams アプリを構築して実行する</span><span class="sxs-lookup"><span data-stu-id="5fa8d-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="5fa8d-105">"Hello, World!" と表示される個人タブを作成することによって、Microsoft Teams 開発に直接ジャンプできます。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="5fa8d-106">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-106">1. Create your app project</span></span>

<span data-ttu-id="5fa8d-107">最初のアプリプロジェクトをセットアップするには、Visual Studio Code の Microsoft Teams ツールキットを使用します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
1. <span data-ttu-id="5fa8d-109">メッセージが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="5fa8d-110">[ **機能の追加** ] 画面で、[ **タブ]** 、[ **次へ**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams Toolkit を使用してアプリプロジェクトを構成する方法を示すスクリーンショット。":::
1. <span data-ttu-id="5fa8d-112">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="5fa8d-113">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="5fa8d-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="5fa8d-114">[ **個人用] タブ** のオプションのみをチェックし、画面の下部にある [ **完了** ] を選択してプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

> [!NOTE]

> <span data-ttu-id="5fa8d-115">ツールキットで新しいプロジェクトを作成した後にアプリパッケージをインストールするには、F5 キーまたは run キーを押します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-115">To install your app package after creating a new project in the toolkit, press F5/run.</span></span> <span data-ttu-id="5fa8d-116">Chrome が起動し、パッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-116">It will launch Chrome and install your package.</span></span> <span data-ttu-id="5fa8d-117">このパッケージは、アプリ Studio に格納され、を使用してインストールされ `appId` ます。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-117">The package is stored in App Studio and installed using the `appId`.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="5fa8d-118">2. 重要なアプリプロジェクトコンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="5fa8d-118">2. Understand important app project components</span></span>

<span data-ttu-id="5fa8d-119">ツールキットによってプロジェクトが構成されると、Teams 用の基本的な個人用タブを作成するためのコンポーネントが用意されます。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-119">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="5fa8d-120">プロジェクトのディレクトリとファイルは、Visual Studio Code のエクスプローラー領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-120">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Visual Studio Code の [個人用] タブのアプリプロジェクトファイルを示すスクリーンショット。":::

### <a name="app-scaffolding"></a><span data-ttu-id="5fa8d-122">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="5fa8d-122">App scaffolding</span></span>

<span data-ttu-id="5fa8d-123">このツールキットは、 `src` セットアップ時に追加された機能に基づいてディレクトリ内に自動的にスキャフォールディングを作成します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-123">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="5fa8d-124">たとえば、セットアップ時にタブを作成した場合、 `App.js` ディレクトリ内のファイル `src/components` は、アプリの初期化とルーティングを処理するので重要です。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-124">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="5fa8d-125">[Microsoft TEAMS SDK](../tabs/how-to/using-teams-client-sdk.md)を呼び出して、アプリと teams 間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-125">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="5fa8d-126">アプリ ID</span><span class="sxs-lookup"><span data-stu-id="5fa8d-126">App ID</span></span>

<span data-ttu-id="5fa8d-127">Teams アプリ ID は、アプリをアプリ Studio で構成するために必要です。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-127">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="5fa8d-128">ID は、 `teamsAppId` プロジェクトのファイル内にあるオブジェクトで見つけることができ `package.json` ます。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-128">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="5fa8d-129">3. アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-129">3. Build and run your app</span></span>

<span data-ttu-id="5fa8d-130">時間の経過とともに、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-130">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="5fa8d-131">(この情報は、ツールキットでも利用でき `README` ます。)</span><span class="sxs-lookup"><span data-stu-id="5fa8d-131">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="5fa8d-132">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="5fa8d-133">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-133">Run `npm start`.</span></span>

<span data-ttu-id="5fa8d-134">完了すると、**コンパイルに成功** しました。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="5fa8d-135">ターミナルのメッセージ。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-135">message in the terminal.</span></span> <span data-ttu-id="5fa8d-136">アプリが実行されている `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="5fa8d-137">4. アプリを Teams でサイドロード</span><span class="sxs-lookup"><span data-stu-id="5fa8d-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="5fa8d-138">アプリは Teams でテストする準備ができています。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="5fa8d-139">これを行うには、アプリのサイドロードを許可するアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-139">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="5fa8d-140">(あるかどうかがわからない場合は、 [Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)の取得についてを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-140">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="5fa8d-141">アプリのサイドロード前に、ツールキットに含まれている [アプリ Studio の検証機能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)を使用して、問題点を確認します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-141">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="5fa8d-142">アプリケーションを正常にサイドロードするには、エラーを修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-142">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="5fa8d-143">Visual Studio Code で、 **F5** キーを押して Teams web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-143">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="5fa8d-144">Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 () を信頼するように指定し `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-144">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="5fa8d-145">**F5** キーを押した後に開いた同じブラウザーウィンドウ (既定では Google Chrome) で新しいタブを開きます。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-145">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="5fa8d-146">に移動 `https://localhost:3000/tab` して、ページに進みます。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-146">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="5fa8d-147">Teams に戻ります。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-147">Go back to Teams.</span></span> <span data-ttu-id="5fa8d-148">ダイアログボックスで、[ **追加** ] を選択してアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-148">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で実行されている ' Hello, World! ' personal tab アプリの例を示すスクリーンショット。":::

<span data-ttu-id="5fa8d-150">おめでとうございます🎉</span><span class="sxs-lookup"><span data-stu-id="5fa8d-150">🎉 Congratulations!</span></span> <span data-ttu-id="5fa8d-151">アプリは Teams で実行されています。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-151">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="5fa8d-152">次のステップ</span><span class="sxs-lookup"><span data-stu-id="5fa8d-152">Next step</span></span>

<span data-ttu-id="5fa8d-153">作成したばかりの [個人] タブを展開するか、別の種類の Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="5fa8d-153">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="5fa8d-154">[[個人用] タブに追加する](../build-your-first-app/build-personal-tab.md)</span><span class="sxs-lookup"><span data-stu-id="5fa8d-154">[Add to your personal tab](../build-your-first-app/build-personal-tab.md)</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5fa8d-155">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="5fa8d-155">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="5fa8d-156">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="5fa8d-156">Build a bot</span></span>](../build-your-first-app/build-bot.md)
