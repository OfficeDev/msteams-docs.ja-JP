---
title: "\"Hello, World!\" をビルドして実行します。 Teams アプリ"
author: heath-hamilton
description: 最初の Microsoft Teams アプリ、つまり "Hello, World!" を表示する個人用タブを作成して実行します。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 244a899670f71b9446c8c3d3e404c9fd7c7b510c
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237833"
---
# <a name="build-a-hello-world-teams-app"></a><span data-ttu-id="835c8-104">"Hello, World!" を作成します。</span><span class="sxs-lookup"><span data-stu-id="835c8-104">Build a "Hello, World!"</span></span> <span data-ttu-id="835c8-105">Teams アプリ</span><span class="sxs-lookup"><span data-stu-id="835c8-105">Teams app</span></span>

<span data-ttu-id="835c8-106">"Hello, World!" と表示される個人タブを作成することによって、Microsoft Teams プラットフォーム開発に直接ジャンプできます。</span><span class="sxs-lookup"><span data-stu-id="835c8-106">You can jump right into Microsoft Teams platform development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="835c8-107">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="835c8-107">1. Create your app project</span></span>

<span data-ttu-id="835c8-108">最初のアプリプロジェクトをセットアップするには、Visual Studio Code の Microsoft Teams ツールキットを使用します。</span><span class="sxs-lookup"><span data-stu-id="835c8-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Visual Studio Code Teams ツールキットを使用して新しいアプリを作成する方法を示すスクリーンショット。":::
1. <span data-ttu-id="835c8-111">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="835c8-111">Enter a name for your Teams app.</span></span> <span data-ttu-id="835c8-112">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="835c8-112">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="835c8-113">[ **機能の追加** ] 画面で、[ **タブ]** 、[ **次へ**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="835c8-113">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams Toolkit を使用してアプリプロジェクトを構成する方法を示すスクリーンショット。":::
1. <span data-ttu-id="835c8-115">[ **個人用] タブ** のオプションを確認し、画面の下部にある [ **完了** ] を選択してプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="835c8-115">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="835c8-116">2. 重要なアプリプロジェクトコンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="835c8-116">2. Understand important app project components</span></span>

<span data-ttu-id="835c8-117">ツールキットによってプロジェクトが構成されると、Teams 用の基本的な個人用タブを作成するためのコンポーネントが用意されます。</span><span class="sxs-lookup"><span data-stu-id="835c8-117">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="835c8-118">プロジェクトのディレクトリとファイルは、Visual Studio Code のエクスプローラー領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="835c8-118">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Visual Studio Code の [個人用] タブのアプリプロジェクトファイルを示すスクリーンショット。":::

<span data-ttu-id="835c8-120">Teams アプリ開発者が扱う主要なファイルのいくつかについて理解しておきましょう。</span><span class="sxs-lookup"><span data-stu-id="835c8-120">Let's take a moment to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="835c8-121">アプリマニフェスト ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="835c8-121">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="835c8-122">アプリケーションマニフェストは、ディレクトリに配置されており、 `.publish` アプリプロジェクトの開始点となります。</span><span class="sxs-lookup"><span data-stu-id="835c8-122">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="835c8-123">マニフェストは、アプリの基本属性を定義し、必要なリソースをポイントします。</span><span class="sxs-lookup"><span data-stu-id="835c8-123">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="835c8-124">アプリをインストールすると、チームはマニフェストを解析して、アプリをクライアントにレンダリングする方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="835c8-124">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="835c8-125">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="835c8-125">App scaffolding</span></span>

<span data-ttu-id="835c8-126">このツールキットは、 `src` セットアップ時に追加された機能に基づいてディレクトリ内に自動的にスキャフォールディングを作成します。</span><span class="sxs-lookup"><span data-stu-id="835c8-126">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="835c8-127">たとえば、セットアップ時にタブを作成した場合、 `App.js` ディレクトリ内のファイル `src/components` は、アプリの初期化とルーティングを処理するので重要です。</span><span class="sxs-lookup"><span data-stu-id="835c8-127">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="835c8-128">[Microsoft TEAMS SDK](../tabs/how-to/using-teams-client-sdk.md)を呼び出して、アプリと teams 間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="835c8-128">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="835c8-129">アプリパッケージ ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="835c8-129">App package (`Development.zip`)</span></span>

<span data-ttu-id="835c8-130">このディレクトリには、アプリパッケージを作成して、アプリ `.publish` を Teams に [サイドロード](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) する必要があります。</span><span class="sxs-lookup"><span data-stu-id="835c8-130">Located in the `.publish` directory, you need the app package to [sideload your app](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="835c8-131">このパッケージは、 [組織のアプリカタログ](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) または [appsource](../concepts/deploy-and-publish/appsource/publish.md)に発行するときにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="835c8-131">The package is also used when [publishing to your organization's app catalog](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="835c8-132">アプリパッケージファイルの詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="835c8-132">Here are some details about the app package files:</span></span>

|<span data-ttu-id="835c8-133">名前</span><span class="sxs-lookup"><span data-stu-id="835c8-133">Name</span></span>|<span data-ttu-id="835c8-134">種類</span><span class="sxs-lookup"><span data-stu-id="835c8-134">Type</span></span>|<span data-ttu-id="835c8-135">Size</span><span class="sxs-lookup"><span data-stu-id="835c8-135">Size</span></span>|<span data-ttu-id="835c8-136">マニフェストの場所</span><span class="sxs-lookup"><span data-stu-id="835c8-136">Manifest location</span></span>|<span data-ttu-id="835c8-137">ツールキットのファイル名</span><span class="sxs-lookup"><span data-stu-id="835c8-137">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="835c8-138">**アプリマニフェスト**</span><span class="sxs-lookup"><span data-stu-id="835c8-138">**App manifest**</span></span>|`.json`| <span data-ttu-id="835c8-139">—</span><span class="sxs-lookup"><span data-stu-id="835c8-139">—</span></span> | <span data-ttu-id="835c8-140">—</span><span class="sxs-lookup"><span data-stu-id="835c8-140">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="835c8-141">**色のロゴ**</span><span class="sxs-lookup"><span data-stu-id="835c8-141">**Color logo**</span></span>|`.png`|<span data-ttu-id="835c8-142">192 &times; 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="835c8-142">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="835c8-143">**アウトラインロゴ**</span><span class="sxs-lookup"><span data-stu-id="835c8-143">**Outline logo**</span></span>|`.png`|<span data-ttu-id="835c8-144">32 &times; 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="835c8-144">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="3-run-your-app"></a><span data-ttu-id="835c8-145">3. アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="835c8-145">3. Run your app</span></span>

<span data-ttu-id="835c8-146">時間の経過とともに、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="835c8-146">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="835c8-147">(この情報は、ツールキットでも利用でき `README` ます。)</span><span class="sxs-lookup"><span data-stu-id="835c8-147">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="835c8-148">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="835c8-148">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="835c8-149">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="835c8-149">Run `npm start`.</span></span> <span data-ttu-id="835c8-150">完了すると、**コンパイルに成功**しました。</span><span class="sxs-lookup"><span data-stu-id="835c8-150">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="835c8-151">ターミナルのメッセージ。</span><span class="sxs-lookup"><span data-stu-id="835c8-151">message in the terminal.</span></span>
1. <span data-ttu-id="835c8-152">ブラウザーを開き、に移動して、 `https://localhost:3000` **Microsoft Teams タブ**という名前の空の web ページを表示します。(ページ上にコンテンツが表示されないことを心配しないでください)。</span><span class="sxs-lookup"><span data-stu-id="835c8-152">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="実行中のアプリをブラウザーで表示するときの外観を示すスクリーンショット。":::

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="835c8-154">4. アプリへのセキュリティで保護されたトンネルをセットアップする</span><span class="sxs-lookup"><span data-stu-id="835c8-154">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="835c8-155">アプリは、ローカル web サーバー上で実行されています。</span><span class="sxs-lookup"><span data-stu-id="835c8-155">Your app is up and running on your local web server.</span></span> <span data-ttu-id="835c8-156">Teams でアプリを実行するには、HTTPS を介してアクセスできるようにする必要があり `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="835c8-156">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="835c8-157">[Ngrok](https://ngrok.com/download)をまだインストールしていない場合はインストールします。</span><span class="sxs-lookup"><span data-stu-id="835c8-157">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="835c8-158">このツールを実行すると、ローカル web サーバーを指す、グローバルに使用できる2つの Url が作成さ `http://localhost:3000` れます ()。</span><span class="sxs-lookup"><span data-stu-id="835c8-158">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="835c8-159">で始まる転送 URL が必要 `HTTPS` です。</span><span class="sxs-lookup"><span data-stu-id="835c8-159">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="835c8-160">新しいターミナルを開き、を実行 `ngrok http 3000` します。</span><span class="sxs-lookup"><span data-stu-id="835c8-160">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="835c8-161">提供されている HTTPS URL をコピーします (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="835c8-161">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Ngrok を実行しているターミナルを示すスクリーンショット。":::
1. <span data-ttu-id="835c8-163">ディレクトリで `.publish` 、を開き `Development.env` ます。</span><span class="sxs-lookup"><span data-stu-id="835c8-163">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="835c8-164">値を `baseUrl0` コピーした URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="835c8-164">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="835c8-165">(たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ba5.ngrok.io` します)。</span><span class="sxs-lookup"><span data-stu-id="835c8-165">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="835c8-166">アプリのマニフェストは、アプリをホストしている場所を指すようになります。</span><span class="sxs-lookup"><span data-stu-id="835c8-166">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="5-sideload-your-app-in-teams"></a><span data-ttu-id="835c8-167">5. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="835c8-167">5. Sideload your app in Teams</span></span>

<span data-ttu-id="835c8-168">アプリを実行し、HTTPS を介してアクセスできるようにすると、そのアプリを Teams にアップロードする準備ができました。</span><span class="sxs-lookup"><span data-stu-id="835c8-168">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="835c8-169">アプリのサイドロード前に、 [ツールキットの検証機能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)を使用して問題がないかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="835c8-169">Before sideloading your app, check for issues using the [toolkit's validation feature](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="835c8-170">アプリケーションを正常にサイドロードするには、エラーを修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="835c8-170">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="835c8-171">アプリのサイドロードを許可するアカウントを使用して、Teams クライアントにログインします。</span><span class="sxs-lookup"><span data-stu-id="835c8-171">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="835c8-172">(あるかどうかがわからない場合は、 [Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)の取得についてを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="835c8-172">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="835c8-173">[ **アプリ**] を選択し、[ **カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="835c8-173">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="835c8-174">アプリプロジェクトフォルダーに移動し `.publish` 、を選択し `Development.zip` ます。</span><span class="sxs-lookup"><span data-stu-id="835c8-174">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="835c8-175">インストールモーダルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="835c8-175">An installation modal displays.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Teams アプリのインストールモーダルの例を示すスクリーンショット。":::
1. <span data-ttu-id="835c8-177">[ **追加** ] を選択してアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="835c8-177">Select **Add** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で実行されている ' Hello, World! ' personal tab アプリの例を示すスクリーンショット。":::

<span data-ttu-id="835c8-179">おめでとうございます🎉</span><span class="sxs-lookup"><span data-stu-id="835c8-179">🎉 Congratulations!</span></span> <span data-ttu-id="835c8-180">アプリは Teams で実行されています。</span><span class="sxs-lookup"><span data-stu-id="835c8-180">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="835c8-181">次のステップ</span><span class="sxs-lookup"><span data-stu-id="835c8-181">Next step</span></span>

<span data-ttu-id="835c8-182">作成したばかりの [個人] タブを展開するか、別の種類の Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="835c8-182">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="835c8-183">[[個人用] タブに追加する](../build-your-first-app/build-personal-tab.md)</span><span class="sxs-lookup"><span data-stu-id="835c8-183">[Add to your personal tab](../build-your-first-app/build-personal-tab.md)</span></span>
> [!div class="nextstepaction"]
> <span data-ttu-id="835c8-184">[[チャネル] タブを作成する](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="835c8-184">[Build a channel tab](../build-your-first-app/build-channel-tab.md)</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="835c8-185">Bot を構築する</span><span class="sxs-lookup"><span data-stu-id="835c8-185">Build a bot</span></span>](../build-your-first-app/build-bot.md)
