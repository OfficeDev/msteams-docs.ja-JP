---
title: 使用を開始する - React を使用した初めての Teams アプリのビルド
author: adrianhall
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 Microsoft Teams ツールキットおよび React を使用したメッセージ。"
ms.author: adhal
ms.date: 05/18/2021
ms.topic: quickstart
ms.openlocfilehash: 4560e332834fec7b681a6b2babf3e881b5e472f7
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2021
ms.locfileid: "52698138"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="72d01-104">React を使用した最初の Microsoft Teams アプリのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="72d01-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="72d01-105">このチュートリアルでは、React で新しい Microsoft Teams アプリを作成し、Microsoft Graph から情報を引き出すシンプルな個人用アプリを実装します。</span><span class="sxs-lookup"><span data-stu-id="72d01-105">In this tutorial, you will create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="72d01-106">(*個人用アプリ* には、個人ユーザーを対象にした一連のタブが含まれます。) チュートリアルでは、Teams アプリの構造、アプリをローカルで実行する方法、さらにはアプリを Azure に展開する方法について学びます。</span><span class="sxs-lookup"><span data-stu-id="72d01-106">(A *personal app* includes a set of tabs scoped for individual use.) During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="72d01-107">ビルドされたアプリは、現在のユーザーの基本的なユーザー情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="72d01-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="72d01-108">許可が付与された場合、アプリは現在のユーザーとして Microsoft Graph に接続し、完全なプロフィールを取得します。</span><span class="sxs-lookup"><span data-stu-id="72d01-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="72d01-109">始める前に</span><span class="sxs-lookup"><span data-stu-id="72d01-109">Before you begin</span></span>

<span data-ttu-id="72d01-110">[前提条件](prerequisites.md)をインストールして、開発環境が整っていることを確認する</span><span class="sxs-lookup"><span data-stu-id="72d01-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="72d01-111">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="72d01-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="72d01-112">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="72d01-112">Create your project</span></span>

<span data-ttu-id="72d01-113">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="72d01-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="72d01-114">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="72d01-114">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="72d01-115">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="72d01-115">Open Visual Studio code.</span></span>
1. <span data-ttu-id="72d01-116">サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。</span><span class="sxs-lookup"><span data-stu-id="72d01-116">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="72d01-118">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-118">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="72d01-120">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-120">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="72d01-122">**[機能の選択]** 手順では、**[タブ]** 機能がすでに選択されています。</span><span class="sxs-lookup"><span data-stu-id="72d01-122">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="72d01-123">**[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="72d01-123">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="72d01-125">**[フロントエンド ホストの種類]** 手順で、**[Azure]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-125">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="新規アプリのホスティングを選択する方法を示すスクリーンショット":::。

1. <span data-ttu-id="72d01-127">**クラウド リソース** 手順で **[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="72d01-127">On the **Cloud resources** step, press **OK**.</span></span>  <span data-ttu-id="72d01-128">このチュートリアルでは、追加のクラウド リソースは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="72d01-128">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="新しいアプリにクラウド リソースを追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="72d01-130">**プログラミング言語** の手順で、**[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-130">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. <span data-ttu-id="72d01-132">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-132">Select a workspace folder.</span></span>  <span data-ttu-id="72d01-133">ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-133">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="72d01-134">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="72d01-134">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="72d01-135">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="72d01-135">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="72d01-136">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="72d01-136">Press **Enter** to continue.</span></span>

<span data-ttu-id="72d01-137">数秒後に Teams アプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-137">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="72d01-138">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="72d01-138">Command line</span></span>](#tab/cli)

<span data-ttu-id="72d01-139">`teamsfx` CLI を使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="72d01-139">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="72d01-140">プロジェクト フォルダーを作成するフォルダーから開始します。</span><span class="sxs-lookup"><span data-stu-id="72d01-140">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="72d01-141">CLI では、プロジェクトを作成するためのいくつかの質問を行います。</span><span class="sxs-lookup"><span data-stu-id="72d01-141">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="72d01-142">各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。</span><span class="sxs-lookup"><span data-stu-id="72d01-142">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="72d01-143">質問に答えた後、**Enter** キーを押して選択を確認します。</span><span class="sxs-lookup"><span data-stu-id="72d01-143">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="72d01-144">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-144">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="72d01-145">**[タブ]** 機能を選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-145">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="72d01-146">**Azure** フロントエンド ホスティングを選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-146">Select **Azure** frontend hosting.</span></span>
1. <span data-ttu-id="72d01-147">クラウド リソースは選択しないでください。</span><span class="sxs-lookup"><span data-stu-id="72d01-147">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="72d01-148">プログラミング言語として **[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-148">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="72d01-149">**Enter** キーを押して、既定のワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-149">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="72d01-150">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="72d01-150">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="72d01-151">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="72d01-151">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="72d01-152">すべての質問に答えると、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-152">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="72d01-153">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="72d01-153">Take a tour of the source code</span></span>

<span data-ttu-id="72d01-154">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="72d01-154">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="72d01-155">Teams ツールキットでプロジェクトを構成すると、Teams 向けの基本的な個人用タブを構築するためのコンポーネントがあります。</span><span class="sxs-lookup"><span data-stu-id="72d01-155">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="72d01-156">プロジェクトのディレクトリとファイルには、Visual Studio Code の [エクスプローラー] 領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-156">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Visual Studio Code で個人用アプリ向けのアプリのプロジェクト ファイルを表示したスクリーンショット。":::

<span data-ttu-id="72d01-158">ツールキットは、セットアップ時に追加した機能に基づいて、プロジェクト ディレクトリにスキャフォールディングを自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="72d01-158">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="72d01-159">Teams ツールキットは、`.fx` ディレクトリにアプリの状態を保持します。</span><span class="sxs-lookup"><span data-stu-id="72d01-159">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="72d01-160">このディレクトリの他の項目の間では、以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="72d01-160">Among other items in this directory:</span></span>

- <span data-ttu-id="72d01-161">アプリ アイコンは PNG ファイルとして `color.png` と `outline.png` に格納されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-161">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="72d01-162">Developer Portal for Teams に公開するアプリのマニフェストは `manifest.source.json` に格納されています。</span><span class="sxs-lookup"><span data-stu-id="72d01-162">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="72d01-163">プロジェクト作成時に選択した設定が `settings.json` に保存されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-163">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="72d01-164">セットアップ時にタブ機能を選択したため、Teams ツールキットは基本的なタブに必要なコードをすべて `tabs` ディレクトリに格納します。</span><span class="sxs-lookup"><span data-stu-id="72d01-164">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="72d01-165">このディレクトリの中には、いくつかの重要なファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="72d01-165">Within this directory there are several important files:</span></span>

- <span data-ttu-id="72d01-166">`tabs/src/index.jsx` はフロントエンド アプリの入力ポイントで、メインの `App` コンポーネントは `ReactDOM.render()` でレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="72d01-166">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="72d01-167">`tabs/src/components/App.jsx` は、アプリの URL ルーティングを処理します。</span><span class="sxs-lookup"><span data-stu-id="72d01-167">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="72d01-168">[Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) を呼び出して、アプリと Teams の間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="72d01-168">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="72d01-169">`tabs/src/components/Tab.jsx` は、アプリの UI を実装するコードを含みます。</span><span class="sxs-lookup"><span data-stu-id="72d01-169">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="72d01-170">`tabs/src/components/TabConfig.jsx` は、アプリを構成する UI を実装するコードを含みます。</span><span class="sxs-lookup"><span data-stu-id="72d01-170">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="72d01-171">Teams ランタイムでは、プライバシー通知、利用規約、構成タブなど、いくつかのタブが必要となります。</span><span class="sxs-lookup"><span data-stu-id="72d01-171">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="72d01-172">プライバシーに関する通知と利用規約のコードは、同じディレクトリ内にあります。</span><span class="sxs-lookup"><span data-stu-id="72d01-172">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="72d01-173">クラウド機能を追加すると、プロジェクトにディレクトリが追加されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-173">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="72d01-174">最も重要なのは、`api` ディレクトリに、ユーザーが書き込んだ Azure Functions のコードが格納されていることです。</span><span class="sxs-lookup"><span data-stu-id="72d01-174">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="72d01-175">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="72d01-175">Run your app locally</span></span>

<span data-ttu-id="72d01-176">Teams ツールキットでは、アプリをローカルで実行することができます。</span><span class="sxs-lookup"><span data-stu-id="72d01-176">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="72d01-177">これは、Teams が予想する正しいインフラを提供するために必要ないくつかのパーツで構成されています。</span><span class="sxs-lookup"><span data-stu-id="72d01-177">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="72d01-178">Azure Active Directory を使用してアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="72d01-178">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="72d01-179">このアプリケーションには、アプリケーションが読み込まれる場所や、アクセスするバックエンド リソースに関連するアクセス許可があります。</span><span class="sxs-lookup"><span data-stu-id="72d01-179">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="72d01-180">認証タスクを支援する Web API がホストされ、アプリと Azure Active Directory の間のプロキシとして機能します。</span><span class="sxs-lookup"><span data-stu-id="72d01-180">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="72d01-181">これは、Azure Functions Core Tools によって実行されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-181">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="72d01-182">これは、URL `https://localhost:5000` でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="72d01-182">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="72d01-183">アプリのフロントエンドを構成する HTML、CSS、JavaScript のリソースは、ローカル サービスでホストされています。</span><span class="sxs-lookup"><span data-stu-id="72d01-183">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="72d01-184">これは、`https://localhost:3000` でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="72d01-184">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="72d01-185">アプリのマニフェストは、Developer Portal for Teams で生成され存在します。</span><span class="sxs-lookup"><span data-stu-id="72d01-185">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="72d01-186">Teams はアプリ マニフェストを使用して、接続しているクライアントにアプリをロードする場所を伝達します。</span><span class="sxs-lookup"><span data-stu-id="72d01-186">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="72d01-187">この作業が完了すると、Teams クライアント内でアプリを読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="72d01-187">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="72d01-188">Teams の Web クライアントを使用することで、標準的な Web 開発環境で HTML、CSS、JavaScript のコードを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="72d01-188">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

[!INCLUDE [Adjust your browser launch settings](~/includes/get-started/browser-private-launch.md)]

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="72d01-189">Visual Studio Code でアプリをローカルにビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="72d01-189">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="72d01-190">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="72d01-190">To build and run your app locally:</span></span>

1. <span data-ttu-id="72d01-191">Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="72d01-191">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="72d01-192">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="72d01-192">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="72d01-193">ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="72d01-193">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="72d01-194">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="72d01-194">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="72d01-195">ツールキットでは、必要に応じてローカル証明書をインストールするようメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-195">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="72d01-196">この証明書により、Teams は `https://localhost` からアプリケーションを読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="72d01-196">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="72d01-197">以下のダイアログが表示されたら、「はい」を選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-197">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. <span data-ttu-id="72d01-199">アプリケーションを実行するために Web ブラウザーが起動します。</span><span class="sxs-lookup"><span data-stu-id="72d01-199">Your web browser is started to run the application.</span></span> <span data-ttu-id="72d01-200">Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="72d01-200">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="72d01-201">メッセージが表示されたら、**[代わりに Web アプリケーションを使用する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="72d01-201">When prompted, select **Use the web app instead**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. <span data-ttu-id="72d01-203">サインインするように求めるメッセージが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="72d01-203">You may be prompted to sign in.</span></span>  <span data-ttu-id="72d01-204">その場合は、M365 アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="72d01-204">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="72d01-205">Teams へのアプリのインストールを促すメッセージが表示された場合は、**[追加]** を押してください。</span><span class="sxs-lookup"><span data-stu-id="72d01-205">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="72d01-206">これでご使用のアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-206">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="完了したアプリのスクリーンショット":::

<span data-ttu-id="72d01-208">他の Web アプリケーションと同様に、通常のデバッグ作業を行うことができます (ブレークポイントの設定など)。</span><span class="sxs-lookup"><span data-stu-id="72d01-208">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="72d01-209">このアプリはホット リロードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="72d01-209">The app supports hot reloading.</span></span>  <span data-ttu-id="72d01-210">プロジェクト内のファイルを変更すると、ページが再読み込みされます。</span><span class="sxs-lookup"><span data-stu-id="72d01-210">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="72d01-211">デバッガーでアプリをローカルに実行した場合に発生することを説明します。</span><span class="sxs-lookup"><span data-stu-id="72d01-211">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="72d01-212">F5 を押すと、以下のように Teams ツールキットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-212">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="72d01-213">Azure Active Directory を使用してアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="72d01-213">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="72d01-214">Teams でアプリを *サイドロード* しました。</span><span class="sxs-lookup"><span data-stu-id="72d01-214">*Sideloaded* your app in Teams.</span></span>
1. <span data-ttu-id="72d01-215">[Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start) を使用して、アプリケーション バックエンドのローカルでの実行を開始しました。</span><span class="sxs-lookup"><span data-stu-id="72d01-215">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="72d01-216">アプリケーションのフロント エンドがローカルでホストされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="72d01-216">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="72d01-217">Microsoft Teams を Web ブラウザーで起動し、`https://localhost:3000/tab` でアプリケーションをサイドロードするよう Teams に指示するコマンドを実行します (URL はアプリケーション マニフェスト内に登録されています)。</span><span class="sxs-lookup"><span data-stu-id="72d01-217">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab` (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="72d01-218">アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="72d01-218">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="72d01-219">Teams でアプリを正常に実行するには、アプリのサイドロードを許可する Microsoft 365 Teams アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="72d01-219">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="72d01-220">アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="72d01-220">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="72d01-221">アプリを Azure に展開した場合に発生することを説明します</span><span class="sxs-lookup"><span data-stu-id="72d01-221">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="72d01-222">展開前は、このアプリケーションは以下のようにローカルで動作しています。</span><span class="sxs-lookup"><span data-stu-id="72d01-222">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="72d01-223">バックエンドは、_Azure Functions Core Tools_ を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="72d01-223">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="72d01-224">アプリケーションの HTTP エンドポイントは、Microsoft Teams がアプリケーションを読み込む場所でローカルに実行されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-224">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="72d01-225">展開では、アクティブな Azure サブスクリプションにリソースをプロビジョニングし、アプリケーションのバックエンドとフロントエンドのコードを Azure に展開 (アップロード) します。</span><span class="sxs-lookup"><span data-stu-id="72d01-225">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span>

1. <span data-ttu-id="72d01-226">バックエンドには (構成済みの場合) 、Azure App Service や Azure Storage など、さまざまな Azure のサービスが使用されています。</span><span class="sxs-lookup"><span data-stu-id="72d01-226">The backend (if configured) uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
1. <span data-ttu-id="72d01-227">フロントエンド アプリケーションは、静的な Web ホスティング用に構成された Azure Storage アカウントに展開されます。</span><span class="sxs-lookup"><span data-stu-id="72d01-227">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="next-steps"></a><span data-ttu-id="72d01-228">次の手順</span><span class="sxs-lookup"><span data-stu-id="72d01-228">Next steps</span></span>

<span data-ttu-id="72d01-229">Teams アプリを作成する他の方法についてご紹介します。</span><span class="sxs-lookup"><span data-stu-id="72d01-229">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="72d01-230">Blazor を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="72d01-230">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="72d01-231">[SharePoint Web パーツとして Teams アプリを作成する](first-app-spfx.md) (Azure は必要なし)</span><span class="sxs-lookup"><span data-stu-id="72d01-231">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="72d01-232">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="72d01-232">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="72d01-233">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="72d01-233">Create a messaging extension</span></span>](first-message-extension.md)
