---
title: 最初の Teams アプリを構築して実行する
author: heath-hamilton
description: 最初の Microsoft Teams アプリを実行します。
ms.openlocfilehash: 98af8d8d6d89007e36c24bd34661ec21b33cbdf1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652106"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="8af16-103">最初の Microsoft Teams アプリを構築して実行する</span><span class="sxs-lookup"><span data-stu-id="8af16-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="8af16-104">基本的なアプリをすばやく構築して実行することにより、Microsoft Teams プラットフォームでの開発にすぐにジャンプできます。</span><span class="sxs-lookup"><span data-stu-id="8af16-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic app.</span></span>

> [!NOTE]
> <span data-ttu-id="8af16-105">このチュートリアルを実行する際には、JavaScript (特に反応する) についての実用的な知識を持っていると便利です。</span><span class="sxs-lookup"><span data-stu-id="8af16-105">It's helpful to have working knowledge of JavaScript (specifically React) when following these tutorials.</span></span>

## <a name="set-up-your-development-account"></a><span data-ttu-id="8af16-106">開発アカウントをセットアップする</span><span class="sxs-lookup"><span data-stu-id="8af16-106">Set up your development account</span></span>

<span data-ttu-id="8af16-107">Teams 用のアプリを構築するには、サイドローディングを許可する Teams アカウントが必要です (アカウントで既に提供されている場合があります)。</span><span class="sxs-lookup"><span data-stu-id="8af16-107">To build apps for Teams, you need a Teams account that allows sideloading (your account may already provide this).</span></span> <span data-ttu-id="8af16-108">そうでない場合は、Microsoft 365 開発者向けサブスクリプションに登録して、テストテナントを取得できるようにします。</span><span class="sxs-lookup"><span data-stu-id="8af16-108">If it doesn't, register for a Microsoft 365 developer subscription so you can get a test tenant.</span></span>

1. <span data-ttu-id="8af16-109">Teams でアプリをサイドロードできるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="8af16-109">Verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="8af16-110">Teams クライアントで、[**アプリ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8af16-110">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="8af16-111">**カスタムアプリをアップロード**するオプションを探します。</span><span class="sxs-lookup"><span data-stu-id="8af16-111">Look for an option to **Upload a custom app**.</span></span>
1. <span data-ttu-id="8af16-112">このオプションを使用している場合は、作成を開始できます。</span><span class="sxs-lookup"><span data-stu-id="8af16-112">If you have this option, you can start building.</span></span> <span data-ttu-id="8af16-113">そうでない場合は、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="8af16-113">If not, do the following:</span></span>
    1. <span data-ttu-id="8af16-114">[Microsoft 365 開発者向けサブスクリプション](../doc-links/prepare-your-o365-tenant.md)に登録します。</span><span class="sxs-lookup"><span data-stu-id="8af16-114">Register for a [Microsoft 365 developer subscription](../doc-links/prepare-your-o365-tenant.md).</span></span>
    1. <span data-ttu-id="8af16-115">テストアカウントの[カスタムアプリのサイドロードを有効に](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)します。</span><span class="sxs-lookup"><span data-stu-id="8af16-115">[Enable custom app sideloading](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for your test account.</span></span>

## <a name="get-your-development-tools"></a><span data-ttu-id="8af16-116">開発ツールを入手する</span><span class="sxs-lookup"><span data-stu-id="8af16-116">Get your development tools</span></span>

<span data-ttu-id="8af16-117">好みのツールで Teams アプリを構築することができますが、ここでは、Visual Studio Code と Microsoft Teams Toolkit を使用してすぐに作業を開始するために必要な情報を紹介します。</span><span class="sxs-lookup"><span data-stu-id="8af16-117">You can build Teams apps with your preferred tools, but here's what you need to get started quickly with Visual Studio Code and the Microsoft Teams Toolkit.</span></span>

1. <span data-ttu-id="8af16-118">[Visual Studio Code](https://code.visualstudio.com/download)の最新バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="8af16-118">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span>
1. <span data-ttu-id="8af16-119">Visual Studio Code で、 **Extensions** ![ 左側のアクティビティバーにある [visual studio ツールキットビュー] を選択し、 ](../doc-links/images/vs-code-extensions.png) **Microsoft Teams toolkit**をインストールします。</span><span class="sxs-lookup"><span data-stu-id="8af16-119">In Visual Studio Code, select **Extensions** ![visual studio toolkit view](../doc-links/images/vs-code-extensions.png) on the left Activity Bar and install the **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="8af16-120">[Node.js](https://nodejs.org/en/) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="8af16-120">Install [Node.js](https://nodejs.org/en/).</span></span>

## <a name="create-an-app-project"></a><span data-ttu-id="8af16-121">アプリプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="8af16-121">Create an app project</span></span>

<span data-ttu-id="8af16-122">Microsoft Teams Toolkit は、最初のアプリプロジェクトをセットアップするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="8af16-122">The Microsoft Teams Toolkit can help you set up your first app project.</span></span>

1. <span data-ttu-id="8af16-123">Visual Studio Code で、[Teams] アイコンを選択してツールキットを開きます。</span><span class="sxs-lookup"><span data-stu-id="8af16-123">In Visual Studio Code, open the toolkit by selecting the Teams icon</span></span> ![teams アイコン](../doc-links/images/favicon-16x16.png) <span data-ttu-id="8af16-125">左側のアクティビティバー</span><span class="sxs-lookup"><span data-stu-id="8af16-125">on the left Activity Bar.</span></span>
1. <span data-ttu-id="8af16-126">[**新しい Teams アプリの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8af16-126">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="8af16-127">メッセージが表示されたら、アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="8af16-127">When prompted, enter a name for your app.</span></span> <span data-ttu-id="8af16-128">これは、アプリの既定の名前であり、ローカルコンピューター上のプロジェクトディレクトリの名前でもあります。</span><span class="sxs-lookup"><span data-stu-id="8af16-128">This is the default name for your app and also the name of the project directory on your local machine.</span></span>
1. <span data-ttu-id="8af16-129">[**機能の追加**] 画面で、[**タブ]** 、[**次へ**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="8af16-129">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="8af16-130">[**個人用] タブ**のオプションを確認し、[**完了**] を選択してプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="8af16-130">Check the **Personal tab** option and select **Finish** to configure your project.</span></span>

![ツールキットのタブの追加ビュー](../doc-links/images/toolkit-add-tabs.PNG)

<span data-ttu-id="8af16-132">完了したら、個人タブを作成するためのアプリのスキャフォールディングコンポーネントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="8af16-132">Once complete, you have the app scaffolding components for building a personal tab.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="8af16-133">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="8af16-133">Run your app</span></span>

<span data-ttu-id="8af16-134">プロジェクトの「」の手順に従って、 `README.md` アプリを作成、実行、および展開します。</span><span class="sxs-lookup"><span data-stu-id="8af16-134">Follow the `README.md` in your project to build, run, and deploy your app to Teams.</span></span> <span data-ttu-id="8af16-135">一般的に、次の手順を実行するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="8af16-135">In general, these instructions help you do the following:</span></span>

* <span data-ttu-id="8af16-136">アプリをホスト `localhost` します。</span><span class="sxs-lookup"><span data-stu-id="8af16-136">Host your app on `localhost`.</span></span>
* <span data-ttu-id="8af16-137">Teams がアプリにアクセスできるように、 [ngrok を使用してセキュリティで保護されたトンネルを設定](../doc-links/debug.md#locally-hosted)します。</span><span class="sxs-lookup"><span data-stu-id="8af16-137">[Set up a secure tunnel with ngrok](../doc-links/debug.md#locally-hosted) so that Teams can access your app.</span></span> <span data-ttu-id="8af16-138">( [Ngrok](https://ngrok.com/download)をインストールします。)</span><span class="sxs-lookup"><span data-stu-id="8af16-138">(Install [ngrok](https://ngrok.com/download).)</span></span>
* <span data-ttu-id="8af16-139">フォルダーのを使用して、アプリを Teams クライアントで[サイドロード](../doc-links/apps-upload.md)し `Development.zip` `.publish` ます。</span><span class="sxs-lookup"><span data-stu-id="8af16-139">[Sideload your app](../doc-links/apps-upload.md) in the Teams client using the `Development.zip` in the `.publish` folder.</span></span>

<span data-ttu-id="8af16-140">アプリのサイドロードが完了すると、Teams クライアントでこのように表示されます。</span><span class="sxs-lookup"><span data-stu-id="8af16-140">Once you sideload your app, it should look like this in the Teams client.</span></span>

![Hello world の例タブ](../doc-links/images/tab-running.png)

## <a name="important-app-project-files"></a><span data-ttu-id="8af16-142">重要なアプリプロジェクトファイル</span><span class="sxs-lookup"><span data-stu-id="8af16-142">Important app project files</span></span>

<span data-ttu-id="8af16-143">アプリプロジェクトとスキャフォールディングを設定したら、Teams アプリ開発者が扱う主要なファイルの一部について理解しておきましょう。</span><span class="sxs-lookup"><span data-stu-id="8af16-143">With your app project and scaffolding set up, take some time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="8af16-144">アプリマニフェスト ( `manifest.json` )</span><span class="sxs-lookup"><span data-stu-id="8af16-144">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="8af16-145">アプリケーションマニフェストは、ディレクトリに配置されており、 `.publish` アプリプロジェクトの開始点となります。</span><span class="sxs-lookup"><span data-stu-id="8af16-145">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="8af16-146">マニフェストは、アプリの基本属性を定義し、必要なリソースをポイントします。</span><span class="sxs-lookup"><span data-stu-id="8af16-146">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="8af16-147">アプリをインストールすると、チームはマニフェストを解析して、アプリをクライアントにレンダリングする方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="8af16-147">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

<span data-ttu-id="8af16-148">次のチュートリアルでは、個人およびチャネルのタブを作成するためのアプリマニフェストのセクションに重点を置いて説明します。</span><span class="sxs-lookup"><span data-stu-id="8af16-148">In the following tutorials, you'll focus on the sections of the app manifest for building personal and channel tabs.</span></span>

### <a name="package-developmentzip"></a><span data-ttu-id="8af16-149">Package ( `Development.zip` )</span><span class="sxs-lookup"><span data-stu-id="8af16-149">Package (`Development.zip`)</span></span>

<span data-ttu-id="8af16-150">また、ディレクトリにあるアプリパッケージを使用して、 `.publish` アプリを Teams に[サイドロード](../../overview.md#how-can-you-share-your-teams-app)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8af16-150">Also located in the `.publish` directory, you need the app package to [sideload your app](../../overview.md#how-can-you-share-your-teams-app) in Teams.</span></span> <span data-ttu-id="8af16-151">[組織のアプリカタログ](../../overview.md#how-can-you-share-your-teams-app)または[appsource](../../concepts/deploy-and-publish/appsource/publish.md)に発行するときにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="8af16-151">It's also used when [publishing to your organization's app catalog](../../overview.md#how-can-you-share-your-teams-app) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="8af16-152">アプリパッケージファイルの詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8af16-152">Here are some details about the app package files:</span></span>

|<span data-ttu-id="8af16-153">Name</span><span class="sxs-lookup"><span data-stu-id="8af16-153">Name</span></span>|<span data-ttu-id="8af16-154">型</span><span class="sxs-lookup"><span data-stu-id="8af16-154">Type</span></span>|<span data-ttu-id="8af16-155">Size</span><span class="sxs-lookup"><span data-stu-id="8af16-155">Size</span></span>|<span data-ttu-id="8af16-156">マニフェストの場所</span><span class="sxs-lookup"><span data-stu-id="8af16-156">Manifest location</span></span>|<span data-ttu-id="8af16-157">ツールキットのファイル名</span><span class="sxs-lookup"><span data-stu-id="8af16-157">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="8af16-158">**アプリマニフェスト**</span><span class="sxs-lookup"><span data-stu-id="8af16-158">**App manifest**</span></span>|`.json`| <span data-ttu-id="8af16-159">—</span><span class="sxs-lookup"><span data-stu-id="8af16-159">—</span></span> | <span data-ttu-id="8af16-160">—</span><span class="sxs-lookup"><span data-stu-id="8af16-160">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="8af16-161">**色のロゴ**</span><span class="sxs-lookup"><span data-stu-id="8af16-161">**Color logo**</span></span>|`.png`|<span data-ttu-id="8af16-162">192 &times; 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="8af16-162">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="8af16-163">**アウトラインロゴ**</span><span class="sxs-lookup"><span data-stu-id="8af16-163">**Outline logo**</span></span>|`.png`|<span data-ttu-id="8af16-164">32 &times; 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="8af16-164">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

### <a name="scaffolding-src"></a><span data-ttu-id="8af16-165">スキャフォールディング ( `src` )</span><span class="sxs-lookup"><span data-stu-id="8af16-165">Scaffolding (`src`)</span></span>

<span data-ttu-id="8af16-166">このツールキットは、 `src` セットアップ時に追加された機能に基づいてディレクトリ内に自動的にスキャフォールディングを作成します。</span><span class="sxs-lookup"><span data-stu-id="8af16-166">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="8af16-167">ただし、どのような種類のアプリであっても、どのような種類のファイルも作成されません。</span><span class="sxs-lookup"><span data-stu-id="8af16-167">Some files are created no matter what kind of app you have, though.</span></span> <span data-ttu-id="8af16-168">たとえば、 `App.js` ディレクトリ内のファイル `src/components` は、アプリの初期化とルーティングを処理するので重要です。</span><span class="sxs-lookup"><span data-stu-id="8af16-168">For example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="8af16-169">最も重要なのは、 [Microsoft TEAMS SDK](../doc-links/using-teams-client-sdk.md)を呼び出して、アプリと teams 間の通信を確立することです。</span><span class="sxs-lookup"><span data-stu-id="8af16-169">Most importantly, it calls the [Microsoft Teams SDK](../doc-links/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

<span data-ttu-id="8af16-170">スキャフォールディングの詳細については、「個人用およびチャネルのタブを作成するためのチュートリアル」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8af16-170">You can learn more about scaffolding in the tutorials for creating personal and channel tabs.</span></span>

## <a name="next-step"></a><span data-ttu-id="8af16-171">次の手順</span><span class="sxs-lookup"><span data-stu-id="8af16-171">Next step</span></span>

<span data-ttu-id="8af16-172">おめでとうございます🎉</span><span class="sxs-lookup"><span data-stu-id="8af16-172">🎉 Congratulations!</span></span> <span data-ttu-id="8af16-173">Teams アプリが実行されている。</span><span class="sxs-lookup"><span data-stu-id="8af16-173">You have a running Teams app.</span></span> <span data-ttu-id="8af16-174">実際の機能を追加する方法については、次のボタンを選択してください。</span><span class="sxs-lookup"><span data-stu-id="8af16-174">Select the following button to learn how to add a real-world feature to it.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="8af16-175">[[個人用] タブを作成する](add-personal-tab.md)</span><span class="sxs-lookup"><span data-stu-id="8af16-175">[Build a personal tab](add-personal-tab.md)</span></span>
