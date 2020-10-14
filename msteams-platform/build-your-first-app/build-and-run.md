---
title: 作業の開始-最初のアプリをビルドして実行する
author: heath-hamilton
description: "\"Hello, World!\" を表示する Microsoft Teams アプリをすばやく作成する Microsoft Teams ツールキットを使用したメッセージ。"
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: quickstart
ms.openlocfilehash: 20c9eee14649cda23e1d682940f489e78cba24b9
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452646"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="ba262-104">最初の Microsoft Teams アプリを構築して実行する</span><span class="sxs-lookup"><span data-stu-id="ba262-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="ba262-105">"Hello, World!" と表示される個人タブを作成することによって、Microsoft Teams 開発に直接ジャンプできます。</span><span class="sxs-lookup"><span data-stu-id="ba262-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="ba262-106">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="ba262-106">1. Create your app project</span></span>

<span data-ttu-id="ba262-107">最初のアプリプロジェクトをセットアップするには、Visual Studio Code の Microsoft Teams ツールキットを使用します。</span><span class="sxs-lookup"><span data-stu-id="ba262-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Visual Studio Code Teams ツールキットを使用して新しいアプリを作成する方法を示すスクリーンショット。":::
1. <span data-ttu-id="ba262-110">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ba262-110">Enter a name for your Teams app.</span></span> <span data-ttu-id="ba262-111">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="ba262-111">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="ba262-112">[ **機能の追加** ] 画面で、[ **タブ]** 、[ **次へ**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="ba262-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams ツールキットを使用して新しいアプリを作成する方法を示すスクリーンショット。":::
1. <span data-ttu-id="ba262-114">[ **個人用] タブ** のオプションを確認し、画面の下部にある [ **完了** ] を選択してプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="ba262-114">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="ba262-115">2. 重要なアプリプロジェクトコンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="ba262-115">2. Understand important app project components</span></span>

<span data-ttu-id="ba262-116">ツールキットによってプロジェクトが構成されると、Teams 用の基本的な個人用タブを作成するためのコンポーネントが用意されます。</span><span class="sxs-lookup"><span data-stu-id="ba262-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="ba262-117">プロジェクトのディレクトリとファイルは、Visual Studio Code のエクスプローラー領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ba262-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Visual Studio Code Teams ツールキットを使用して新しいアプリを作成する方法を示すスクリーンショット。":::

<span data-ttu-id="ba262-119">Teams アプリ開発者が扱う主要なファイルのいくつかについて理解しておきましょう。</span><span class="sxs-lookup"><span data-stu-id="ba262-119">Let's take a moment to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="ba262-120">アプリマニフェスト ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="ba262-120">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="ba262-121">アプリケーションマニフェストは、ディレクトリに配置されており、 `.publish` アプリプロジェクトの開始点となります。</span><span class="sxs-lookup"><span data-stu-id="ba262-121">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="ba262-122">マニフェストは、アプリの基本属性を定義し、必要なリソースをポイントします。</span><span class="sxs-lookup"><span data-stu-id="ba262-122">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="ba262-123">アプリをインストールすると、チームはマニフェストを解析して、アプリをクライアントにレンダリングする方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="ba262-123">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="ba262-124">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="ba262-124">App scaffolding</span></span>

<span data-ttu-id="ba262-125">このツールキットは、 `src` セットアップ時に追加された機能に基づいてディレクトリ内に自動的にスキャフォールディングを作成します。</span><span class="sxs-lookup"><span data-stu-id="ba262-125">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="ba262-126">たとえば、セットアップ時にタブを作成した場合、 `App.js` ディレクトリ内のファイル `src/components` は、アプリの初期化とルーティングを処理するので重要です。</span><span class="sxs-lookup"><span data-stu-id="ba262-126">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="ba262-127">[Microsoft TEAMS SDK](../tabs/how-to/using-teams-client-sdk.md)を呼び出して、アプリと teams 間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="ba262-127">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="ba262-128">アプリパッケージ ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="ba262-128">App package (`Development.zip`)</span></span>

<span data-ttu-id="ba262-129">このディレクトリには、アプリパッケージを作成して、アプリ `.publish` を Teams に [サイドロード](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ba262-129">Located in the `.publish` directory, you need the app package to [sideload your app](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="ba262-130">このパッケージは、 [組織のアプリカタログ](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) または [appsource](../concepts/deploy-and-publish/appsource/publish.md)に発行するときにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="ba262-130">The package is also used when [publishing to your organization's app catalog](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="ba262-131">アプリパッケージファイルの詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ba262-131">Here are some details about the app package files:</span></span>

|<span data-ttu-id="ba262-132">名前</span><span class="sxs-lookup"><span data-stu-id="ba262-132">Name</span></span>|<span data-ttu-id="ba262-133">型</span><span class="sxs-lookup"><span data-stu-id="ba262-133">Type</span></span>|<span data-ttu-id="ba262-134">Size</span><span class="sxs-lookup"><span data-stu-id="ba262-134">Size</span></span>|<span data-ttu-id="ba262-135">マニフェストの場所</span><span class="sxs-lookup"><span data-stu-id="ba262-135">Manifest location</span></span>|<span data-ttu-id="ba262-136">ツールキットのファイル名</span><span class="sxs-lookup"><span data-stu-id="ba262-136">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="ba262-137">**アプリマニフェスト**</span><span class="sxs-lookup"><span data-stu-id="ba262-137">**App manifest**</span></span>|`.json`| <span data-ttu-id="ba262-138">—</span><span class="sxs-lookup"><span data-stu-id="ba262-138">—</span></span> | <span data-ttu-id="ba262-139">—</span><span class="sxs-lookup"><span data-stu-id="ba262-139">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="ba262-140">**色のロゴ**</span><span class="sxs-lookup"><span data-stu-id="ba262-140">**Color logo**</span></span>|`.png`|<span data-ttu-id="ba262-141">192 &times; 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="ba262-141">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="ba262-142">**アウトラインロゴ**</span><span class="sxs-lookup"><span data-stu-id="ba262-142">**Outline logo**</span></span>|`.png`|<span data-ttu-id="ba262-143">32 &times; 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="ba262-143">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="3-run-your-app"></a><span data-ttu-id="ba262-144">3. アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="ba262-144">3. Run your app</span></span>

<span data-ttu-id="ba262-145">時間の経過とともに、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="ba262-145">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="ba262-146">(この情報は、ツールキットでも利用でき `README` ます。)</span><span class="sxs-lookup"><span data-stu-id="ba262-146">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="ba262-147">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="ba262-147">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="ba262-148">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="ba262-148">Run `npm start`.</span></span> <span data-ttu-id="ba262-149">完了すると、**コンパイルに成功**しました。</span><span class="sxs-lookup"><span data-stu-id="ba262-149">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="ba262-150">ターミナルのメッセージ。</span><span class="sxs-lookup"><span data-stu-id="ba262-150">message in the terminal.</span></span>
1. <span data-ttu-id="ba262-151">ブラウザーを開き、に移動して、 `https://localhost:3000` **Microsoft Teams タブ**という名前の空の web ページを表示します。(ページ上にコンテンツが表示されないことを心配しないでください)。</span><span class="sxs-lookup"><span data-stu-id="ba262-151">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="Visual Studio Code Teams ツールキットを使用して新しいアプリを作成する方法を示すスクリーンショット。":::

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="ba262-153">4. アプリへのセキュリティで保護されたトンネルをセットアップする</span><span class="sxs-lookup"><span data-stu-id="ba262-153">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="ba262-154">アプリは、ローカル web サーバー上で実行されています。</span><span class="sxs-lookup"><span data-stu-id="ba262-154">Your app is up and running on your local web server.</span></span> <span data-ttu-id="ba262-155">Teams でアプリを実行するには、HTTPS を介してアクセスできるようにする必要があり `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="ba262-155">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="ba262-156">[Ngrok](https://ngrok.com/download)をまだインストールしていない場合はインストールします。</span><span class="sxs-lookup"><span data-stu-id="ba262-156">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="ba262-157">このツールを実行すると、ローカル web サーバーを指す、グローバルに使用できる2つの Url が作成さ `http://localhost:3000` れます ()。</span><span class="sxs-lookup"><span data-stu-id="ba262-157">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="ba262-158">で始まる転送 URL が必要 `HTTPS` です。</span><span class="sxs-lookup"><span data-stu-id="ba262-158">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="ba262-159">新しいターミナルを開き、を実行 `ngrok http 3000` します。</span><span class="sxs-lookup"><span data-stu-id="ba262-159">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="ba262-160">提供されている HTTPS URL をコピーします (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="ba262-160">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Visual Studio Code Teams ツールキットを使用して新しいアプリを作成する方法を示すスクリーンショット。":::
1. <span data-ttu-id="ba262-162">ディレクトリで `.publish` 、を開き `Development.env` ます。</span><span class="sxs-lookup"><span data-stu-id="ba262-162">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="ba262-163">値を `baseUrl0` コピーした URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ba262-163">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="ba262-164">(たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ba5.ngrok.io` します)。</span><span class="sxs-lookup"><span data-stu-id="ba262-164">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="ba262-165">アプリのマニフェストは、アプリをホストしている場所を指すようになります。</span><span class="sxs-lookup"><span data-stu-id="ba262-165">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="5-sideload-your-app-in-teams"></a><span data-ttu-id="ba262-166">5. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="ba262-166">5. Sideload your app in Teams</span></span>

<span data-ttu-id="ba262-167">アプリを実行し、HTTPS を介してアクセスできるようにすると、そのアプリを Teams にアップロードする準備ができました。</span><span class="sxs-lookup"><span data-stu-id="ba262-167">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="ba262-168">アプリのサイドロード前に、 [ツールキットの検証機能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)を使用して問題がないかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="ba262-168">Before sideloading your app, check for issues using the [toolkit's validation feature](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="ba262-169">アプリケーションを正常にサイドロードするには、エラーを修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ba262-169">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="ba262-170">アプリのサイドロードを許可するアカウントを使用して、Teams クライアントにログインします。</span><span class="sxs-lookup"><span data-stu-id="ba262-170">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="ba262-171">(あるかどうかがわからない場合は、 [Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)の取得についてを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="ba262-171">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="ba262-172">[ **アプリ**] を選択し、[ **カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ba262-172">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="ba262-173">アプリプロジェクトフォルダーに移動し `.publish` 、を選択し `Development.zip` ます。</span><span class="sxs-lookup"><span data-stu-id="ba262-173">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="ba262-174">インストールモーダルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ba262-174">An installation modal displays.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Visual Studio Code Teams ツールキットを使用して新しいアプリを作成する方法を示すスクリーンショット。":::
1. <span data-ttu-id="ba262-176">[ **追加** ] を選択してアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="ba262-176">Select **Add** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Visual Studio Code Teams ツールキットを使用して新しいアプリを作成する方法を示すスクリーンショット。":::

<span data-ttu-id="ba262-178">おめでとうございます🎉</span><span class="sxs-lookup"><span data-stu-id="ba262-178">🎉 Congratulations!</span></span> <span data-ttu-id="ba262-179">アプリは Teams で実行されています。</span><span class="sxs-lookup"><span data-stu-id="ba262-179">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="ba262-180">次のステップ</span><span class="sxs-lookup"><span data-stu-id="ba262-180">Next step</span></span>

<span data-ttu-id="ba262-181">作成したばかりの [個人] タブを展開するか、別の種類の Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="ba262-181">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="ba262-182">[[個人用] タブに追加する](../build-your-first-app/build-personal-tab.md)</span><span class="sxs-lookup"><span data-stu-id="ba262-182">[Add to your personal tab](../build-your-first-app/build-personal-tab.md)</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ba262-183">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="ba262-183">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="ba262-184">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="ba262-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)
