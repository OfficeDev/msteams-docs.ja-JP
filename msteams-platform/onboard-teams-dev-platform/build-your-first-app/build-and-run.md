---
title: 最初の Teams アプリを構築して実行する
author: heath-hamilton
ms.author: lajanuar
description: 最初の Microsoft Teams アプリを実行します。
ms.date: 08/31/2020
ms.topic: quickstart
ms.openlocfilehash: 441b70480d9c177e9c6140342df8c9ea29494a29
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964693"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="6fd46-103">最初の Microsoft Teams アプリを構築して実行する</span><span class="sxs-lookup"><span data-stu-id="6fd46-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="6fd46-104">基本的な個人タブをすばやく作成して実行することにより、Microsoft Teams プラットフォームでの開発に直接ジャンプできます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic personal tab.</span></span>

## <a name="create-your-app-project"></a><span data-ttu-id="6fd46-105">アプリプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="6fd46-105">Create your app project</span></span>

<span data-ttu-id="6fd46-106">最初のアプリプロジェクトをセットアップするには、Visual Studio Code の Microsoft Teams ツールキットを使用します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-106">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
:::image type="content" source="../doc-links/images/create-teams-app.png" alt-text="teams アプリイメージの作成":::
1. <span data-ttu-id="6fd46-109">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-109">Enter a name for your Teams app.</span></span> <span data-ttu-id="6fd46-110">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="6fd46-110">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="6fd46-111">[ **機能の追加** ] 画面で、[ **タブ]** 、[ **次へ**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-111">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../doc-links/images/choose-tab.png" alt-text="teams アプリイメージビューの作成":::
1. <span data-ttu-id="6fd46-113">[ **個人用] タブ** のオプションを確認し、画面の下部にある [ **完了** ] を選択してプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-113">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="understand-important-app-project-components"></a><span data-ttu-id="6fd46-114">重要なアプリプロジェクトコンポーネントについて理解する</span><span class="sxs-lookup"><span data-stu-id="6fd46-114">Understand important app project components</span></span>

<span data-ttu-id="6fd46-115">ツールキットによってプロジェクトが構成されると、Teams 用の基本的な個人用タブを作成するためのコンポーネントが用意されます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-115">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="6fd46-116">プロジェクトのディレクトリとファイルは、Visual Studio Code のエクスプローラー領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-116">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../doc-links/images/app-project-files.png" alt-text="Visual Studio Code 内のアプリプロジェクトファイル。":::

<span data-ttu-id="6fd46-118">Teams アプリ開発者が扱う主要なファイルのいくつかを理解してみましょう。</span><span class="sxs-lookup"><span data-stu-id="6fd46-118">Let's take time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="6fd46-119">アプリマニフェスト ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="6fd46-119">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="6fd46-120">アプリケーションマニフェストは、ディレクトリに配置されており、 `.publish` アプリプロジェクトの開始点となります。</span><span class="sxs-lookup"><span data-stu-id="6fd46-120">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="6fd46-121">マニフェストは、アプリの基本属性を定義し、必要なリソースをポイントします。</span><span class="sxs-lookup"><span data-stu-id="6fd46-121">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="6fd46-122">アプリをインストールすると、チームはマニフェストを解析して、アプリをクライアントにレンダリングする方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-122">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="6fd46-123">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="6fd46-123">App scaffolding</span></span>

<span data-ttu-id="6fd46-124">このツールキットは、 `src` セットアップ時に追加された機能に基づいてディレクトリ内に自動的にスキャフォールディングを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-124">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="6fd46-125">たとえば、セットアップ時にタブを作成した場合、 `App.js` ディレクトリ内のファイル `src/components` は、アプリの初期化とルーティングを処理するので重要です。</span><span class="sxs-lookup"><span data-stu-id="6fd46-125">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="6fd46-126">[Microsoft TEAMS SDK](../../tabs/how-to/using-teams-client-sdk.md)を呼び出して、アプリと teams 間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-126">It calls the [Microsoft Teams SDK](../../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="6fd46-127">アプリパッケージ ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="6fd46-127">App package (`Development.zip`)</span></span>

<span data-ttu-id="6fd46-128">このディレクトリには、アプリパッケージを作成して、アプリ `.publish` を Teams に [サイドロード](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fd46-128">Located in the `.publish` directory, you need the app package to [sideload your app](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="6fd46-129">このパッケージは、 [組織のアプリカタログ](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) または [appsource](../../concepts/deploy-and-publish/appsource/publish.md)に発行するときにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-129">The package is also used when [publishing to your organization's app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="6fd46-130">アプリパッケージファイルの詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6fd46-130">Here are some details about the app package files:</span></span>

|<span data-ttu-id="6fd46-131">Name</span><span class="sxs-lookup"><span data-stu-id="6fd46-131">Name</span></span>|<span data-ttu-id="6fd46-132">種類</span><span class="sxs-lookup"><span data-stu-id="6fd46-132">Type</span></span>|<span data-ttu-id="6fd46-133">Size</span><span class="sxs-lookup"><span data-stu-id="6fd46-133">Size</span></span>|<span data-ttu-id="6fd46-134">マニフェストの場所</span><span class="sxs-lookup"><span data-stu-id="6fd46-134">Manifest location</span></span>|<span data-ttu-id="6fd46-135">ツールキットのファイル名</span><span class="sxs-lookup"><span data-stu-id="6fd46-135">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="6fd46-136">**アプリマニフェスト**</span><span class="sxs-lookup"><span data-stu-id="6fd46-136">**App manifest**</span></span>|`.json`| <span data-ttu-id="6fd46-137">—</span><span class="sxs-lookup"><span data-stu-id="6fd46-137">—</span></span> | <span data-ttu-id="6fd46-138">—</span><span class="sxs-lookup"><span data-stu-id="6fd46-138">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="6fd46-139">**色のロゴ**</span><span class="sxs-lookup"><span data-stu-id="6fd46-139">**Color logo**</span></span>|`.png`|<span data-ttu-id="6fd46-140">192 &times; 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="6fd46-140">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="6fd46-141">**アウトラインロゴ**</span><span class="sxs-lookup"><span data-stu-id="6fd46-141">**Outline logo**</span></span>|`.png`|<span data-ttu-id="6fd46-142">32 &times; 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="6fd46-142">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a><span data-ttu-id="6fd46-143">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="6fd46-143">Run your app</span></span>

<span data-ttu-id="6fd46-144">時間の経過とともに、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-144">In the interest of time, you'll build and run your app locally.</span></span> <span data-ttu-id="6fd46-145">運用レベルの Teams アプリは、クラウドでホストされます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-145">Production-level Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="6fd46-146">(この情報は、ツールキットでも利用でき `README` ます。)</span><span class="sxs-lookup"><span data-stu-id="6fd46-146">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="6fd46-147">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-147">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="6fd46-148">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-148">Run `npm start`.</span></span> <span data-ttu-id="6fd46-149">完了すると、**コンパイルに成功**しました。</span><span class="sxs-lookup"><span data-stu-id="6fd46-149">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="6fd46-150">ターミナルのメッセージ。</span><span class="sxs-lookup"><span data-stu-id="6fd46-150">message in the terminal.</span></span>
1. <span data-ttu-id="6fd46-151">ブラウザーを開き、に移動して、 `https://localhost:3000` **Microsoft Teams タブ**という名前の空の web ページを表示します。(ページ上にコンテンツが表示されないことを心配しないでください)。</span><span class="sxs-lookup"><span data-stu-id="6fd46-151">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../doc-links/images/local-host-tab.png" alt-text="ブラウザーでアプリを表示します。":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="6fd46-153">アプリへのセキュリティで保護されたトンネルの設定</span><span class="sxs-lookup"><span data-stu-id="6fd46-153">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="6fd46-154">アプリは、ローカル web サーバー上で実行されています。</span><span class="sxs-lookup"><span data-stu-id="6fd46-154">Your app is up and running on your local web server.</span></span> <span data-ttu-id="6fd46-155">Teams でアプリを実行するには、HTTPS を介してアクセスできるようにする必要があり `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-155">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="6fd46-156">[Ngrok](https://ngrok.com/download)をまだインストールしていない場合はインストールします。</span><span class="sxs-lookup"><span data-stu-id="6fd46-156">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="6fd46-157">このツールを実行すると、ローカル web サーバーを指す、グローバルに使用できる2つの Url が作成さ `http://localhost:3000` れます ()。</span><span class="sxs-lookup"><span data-stu-id="6fd46-157">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="6fd46-158">で始まる転送 URL が必要 `HTTPS` です。</span><span class="sxs-lookup"><span data-stu-id="6fd46-158">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="6fd46-159">新しいターミナルを開き、を実行 `ngrok http 3000` します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-159">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="6fd46-160">提供されている HTTPS URL をコピーします (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="6fd46-160">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../doc-links/images/ngrok-running.png" alt-text="ngrok の実行中の画像":::
1. <span data-ttu-id="6fd46-162">ディレクトリで `.publish` 、を開き `Development.env` ます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-162">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="6fd46-163">値を `baseUrl0` コピーした URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-163">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="6fd46-164">(たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ba5.ngrok.io` します)。</span><span class="sxs-lookup"><span data-stu-id="6fd46-164">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="6fd46-165">アプリのマニフェストは、アプリをホストしている場所を指すようになります。</span><span class="sxs-lookup"><span data-stu-id="6fd46-165">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="6fd46-166">Teams でのアプリのサイドロード</span><span class="sxs-lookup"><span data-stu-id="6fd46-166">Sideload your app in Teams</span></span>

<span data-ttu-id="6fd46-167">アプリを実行し、HTTPS を介してアクセスできるようにすると、そのアプリを Teams にアップロードする準備ができました。</span><span class="sxs-lookup"><span data-stu-id="6fd46-167">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="6fd46-168">アプリのサイドロード前に、 [ツールキットの検証機能](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)を使用して問題がないかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-168">Before sideloading your app, check for issues using the [toolkit's validation feature](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="6fd46-169">アプリケーションを正常にサイドロードするには、エラーを修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fd46-169">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="6fd46-170">アプリのサイドロードを許可するアカウントを使用して、Teams クライアントにログインします。</span><span class="sxs-lookup"><span data-stu-id="6fd46-170">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="6fd46-171">(あるかどうかがわからない場合は、 [Teams 開発アカウント](../build-your-first-app/building-real-world-app.md#set-up-your-development-account)の取得についてを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="6fd46-171">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/building-real-world-app.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="6fd46-172">[ **アプリ**] を選択し、[ **カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-172">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="6fd46-173">アプリプロジェクトフォルダーに移動し `.publish` 、を選択し `Development.zip` ます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-173">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="6fd46-174">インストールモーダルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6fd46-174">An install modal displays.</span></span>
:::image type="content" source="../doc-links/images/add-teams-app.png" alt-text="teams アプリを追加する":::
1. <span data-ttu-id="6fd46-176">[ **追加** ] を選択してアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="6fd46-176">Select **Add** to install your app.</span></span>
:::image type="content" source="../doc-links/images/tab-running.png" alt-text="Hello, World の例を示すスクリーンショットTeams のアプリ。":::

<span data-ttu-id="6fd46-178">おめでとうございます🎉</span><span class="sxs-lookup"><span data-stu-id="6fd46-178">🎉 Congratulations!</span></span> <span data-ttu-id="6fd46-179">アプリは Teams で実行されています。</span><span class="sxs-lookup"><span data-stu-id="6fd46-179">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="6fd46-180">次の手順</span><span class="sxs-lookup"><span data-stu-id="6fd46-180">Next step</span></span>

<span data-ttu-id="6fd46-181">作成したばかりの [個人] タブを展開するか、別の種類の Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fd46-181">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="6fd46-182">[[個人用] タブに追加する](../build-your-first-app/add-personal-tab.md)</span><span class="sxs-lookup"><span data-stu-id="6fd46-182">[Add to your personal tab](../build-your-first-app/add-personal-tab.md)</span></span>
> [!div class="nextstepaction"]
> <span data-ttu-id="6fd46-183">[[チャネル] タブを作成する](../build-your-first-app/add-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="6fd46-183">[Build a channel tab](../build-your-first-app/add-channel-tab.md)</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6fd46-184">Bot を構築する</span><span class="sxs-lookup"><span data-stu-id="6fd46-184">Build a bot</span></span>](../build-your-first-app/add-bot.md)
