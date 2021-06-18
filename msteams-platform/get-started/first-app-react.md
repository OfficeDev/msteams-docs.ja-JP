---
title: 使用を開始する - React を使用した初めての Teams アプリのビルド
author: adrianhall
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 Microsoft Teams ツールキットおよび React を使用したメッセージ。"
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: edd7cf8048dd89156b4b91afecb329d91baf3f53
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994115"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="d7f94-104">React を使用した最初の Microsoft Teams アプリのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="d7f94-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="d7f94-105">このチュートリアルでは、React で新しい Microsoft Teams アプリを作成し、Microsoft Graph から情報を引き出すシンプルな個人用アプリを実装します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-105">In this tutorial, you will create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="d7f94-106">たとえば、個人用アプリ *には、* 個々の使用を対象にした一連のタブが含まれます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-106">For example, a *personal app* includes a set of tabs scoped for individual use.</span></span> <span data-ttu-id="d7f94-107">チュートリアルでは、Teams アプリの構造、アプリをローカルで実行する方法、Azure にアプリを展開する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="d7f94-108">ビルドされたアプリは、現在のユーザーの基本的なユーザー情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-108">The app that is built displays basic user information for the current user.</span></span> <span data-ttu-id="d7f94-109">許可が付与された場合、アプリは現在のユーザーとして Microsoft Graph に接続し、完全なプロフィールを取得します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d7f94-110">始める前に</span><span class="sxs-lookup"><span data-stu-id="d7f94-110">Before you begin</span></span>

<span data-ttu-id="d7f94-111">前提条件をインストールして、開発環境がセットアップされていることを確認 [します](prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="d7f94-111">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7f94-112">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="d7f94-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="d7f94-113">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="d7f94-113">Create your project</span></span>

<span data-ttu-id="d7f94-114">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="d7f94-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d7f94-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="d7f94-116">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="d7f94-117">サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-117">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="d7f94-119">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="d7f94-121">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="d7f94-123">[機能 **の選択] ステップ** で、[ **タブ] 機能** が既に選択されています。</span><span class="sxs-lookup"><span data-stu-id="d7f94-123">On the **Select capabilities** step, the **Tab** capability is already selected.</span></span> <span data-ttu-id="d7f94-124">**[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-124">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="d7f94-126">**[フロントエンド ホストの種類]** 手順で、**[Azure]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-126">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="新規アプリのホスティングを選択する方法を示すスクリーンショット":::。

1. <span data-ttu-id="d7f94-128">**クラウド リソース** 手順で **[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-128">On the **Cloud resources** step, press **OK**.</span></span>  <span data-ttu-id="d7f94-129">このチュートリアルでは、追加のクラウド リソースは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="d7f94-129">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="新しいアプリにクラウド リソースを追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="d7f94-131">**プログラミング言語** の手順で、**[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-131">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. <span data-ttu-id="d7f94-133">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-133">Select a workspace folder.</span></span> <span data-ttu-id="d7f94-134">作成するプロジェクトのワークスペース フォルダー内にフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-134">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="d7f94-135">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-135">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="d7f94-136">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="d7f94-137">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-137">Press **Enter** to continue.</span></span>

<span data-ttu-id="d7f94-138">アプリTeams数秒で作成されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-138">Your Teams app is created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="d7f94-139">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="d7f94-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="d7f94-140">`teamsfx` CLI を使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="d7f94-141">プロジェクト フォルダーを作成するフォルダーから開始します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="d7f94-142">CLI では、プロジェクトを作成するためのいくつかの質問を行います。</span><span class="sxs-lookup"><span data-stu-id="d7f94-142">The CLI walks through some questions to create the project.</span></span> <span data-ttu-id="d7f94-143">各質問には、矢印キーを使用してオプションを選択する方法など、回答方法が示されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-143">Each question will tell you how to answer it, for example, use arrow keys to select an option.</span></span> <span data-ttu-id="d7f94-144">質問に答えた後、**Enter** キーを押して選択を確認します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="d7f94-145">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="d7f94-146">**[タブ]** 機能を選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-146">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="d7f94-147">**Azure** フロントエンド ホスティングを選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-147">Select **Azure** frontend hosting.</span></span>
1. <span data-ttu-id="d7f94-148">クラウド リソースは選択しないでください。</span><span class="sxs-lookup"><span data-stu-id="d7f94-148">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="d7f94-149">プログラミング言語として **[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-149">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="d7f94-150">**Enter** キーを押して、既定のワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-150">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="d7f94-151">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-151">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="d7f94-152">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-152">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="d7f94-153">すべての質問に回答すると、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-153">Once all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="d7f94-154">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="d7f94-154">Take a tour of the source code</span></span>

<span data-ttu-id="d7f94-155">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-155">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="d7f94-156">Teams ツールキットでプロジェクトを構成すると、Teams 向けの基本的な個人用タブを構築するためのコンポーネントがあります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-156">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="d7f94-157">プロジェクトのディレクトリとファイルには、Visual Studio Code の [エクスプローラー] 領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-157">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Visual Studio Code で個人用アプリ向けのアプリのプロジェクト ファイルを表示したスクリーンショット。":::

<span data-ttu-id="d7f94-159">ツールキットは、セットアップ時に追加した機能に基づいて、プロジェクト ディレクトリにスキャフォールディングを自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-159">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="d7f94-160">Teams ツールキットは、`.fx` ディレクトリにアプリの状態を保持します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-160">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="d7f94-161">このディレクトリの他の項目の間では、以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-161">Among other items in this directory:</span></span>

- <span data-ttu-id="d7f94-162">アプリ アイコンは PNG ファイルとして `color.png` と `outline.png` に格納されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-162">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="d7f94-163">Developer Portal for Teams に公開するアプリのマニフェストは `manifest.source.json` に格納されています。</span><span class="sxs-lookup"><span data-stu-id="d7f94-163">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="d7f94-164">プロジェクト作成時に選択した設定が `settings.json` に保存されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-164">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="d7f94-165">セットアップ時にタブ機能を選択したため、Teams ツールキットは基本的なタブに必要なコードをすべて `tabs` ディレクトリに格納します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-165">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="d7f94-166">このディレクトリの中には、いくつかの重要なファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-166">Within this directory there are several important files:</span></span>

- <span data-ttu-id="d7f94-167">`tabs/src/index.jsx` はフロントエンド アプリの入力ポイントで、メインの `App` コンポーネントは `ReactDOM.render()` でレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-167">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="d7f94-168">`tabs/src/components/App.jsx` は、アプリの URL ルーティングを処理します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-168">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="d7f94-169">[Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) を呼び出して、アプリと Teams の間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-169">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="d7f94-170">`tabs/src/components/Tab.jsx` は、アプリの UI を実装するコードを含みます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-170">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="d7f94-171">`tabs/src/components/TabConfig.jsx` は、アプリを構成する UI を実装するコードを含みます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-171">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="d7f94-172">Teams ランタイムでは、プライバシー通知、利用規約、構成タブなど、いくつかのタブが必要となります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-172">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="d7f94-173">プライバシーに関する通知と利用規約のコードは、同じディレクトリ内にあります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-173">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="d7f94-174">クラウド機能を追加すると、プロジェクトにディレクトリが追加されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-174">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="d7f94-175">最も重要なのは、`api` ディレクトリに、ユーザーが書き込んだ Azure Functions のコードが格納されていることです。</span><span class="sxs-lookup"><span data-stu-id="d7f94-175">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="d7f94-176">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="d7f94-176">Run your app locally</span></span>

<span data-ttu-id="d7f94-177">Teams ツールキットでは、アプリをローカルで実行することができます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-177">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="d7f94-178">これは、Teams が予想する正しいインフラを提供するために必要ないくつかのパーツで構成されています。</span><span class="sxs-lookup"><span data-stu-id="d7f94-178">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="d7f94-179">Azure Active Directory を使用してアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="d7f94-179">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="d7f94-180">このアプリケーションには、アプリケーションが読み込まれる場所や、アクセスするバックエンド リソースに関連するアクセス許可があります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-180">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="d7f94-181">認証タスクを支援する Web API がホストされ、アプリと Azure Active Directory の間のプロキシとして機能します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-181">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="d7f94-182">これは、Azure Functions Core Tools によって実行されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-182">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="d7f94-183">これは、URL `https://localhost:5000` でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-183">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="d7f94-184">アプリのフロントエンドを構成する HTML、CSS、JavaScript のリソースは、ローカル サービスでホストされています。</span><span class="sxs-lookup"><span data-stu-id="d7f94-184">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="d7f94-185">これは、`https://localhost:3000` でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-185">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="d7f94-186">アプリのマニフェストは、Developer Portal for Teams で生成され存在します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-186">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="d7f94-187">Teams はアプリ マニフェストを使用して、接続しているクライアントにアプリをロードする場所を伝達します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-187">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="d7f94-188">この作業が完了すると、Teams クライアント内でアプリを読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-188">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="d7f94-189">Teams の Web クライアントを使用することで、標準的な Web 開発環境で HTML、CSS、JavaScript のコードを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-189">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="d7f94-190">Visual Studio Code でアプリをローカルにビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="d7f94-190">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="d7f94-191">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="d7f94-191">To build and run your app locally:</span></span>

1. <span data-ttu-id="d7f94-192">Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-192">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="d7f94-193">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-193">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="d7f94-194">ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-194">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="d7f94-195">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-195">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="d7f94-196">必要にToolkitローカル証明書のインストールを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-196">The Toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="d7f94-197">この証明書により、Teams は `https://localhost` からアプリケーションを読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-197">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="d7f94-198">以下のダイアログが表示されたら、「はい」を選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-198">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. <span data-ttu-id="d7f94-200">Web ブラウザーがアプリの実行を開始します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-200">Your web browser starts to run the app.</span></span> <span data-ttu-id="d7f94-201">デスクトップを開くTeams場合は、[キャンセル] を **選択して** ブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-201">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="d7f94-202">また、他の場合はデスクトップに切り替Teams表示される場合があります。この場合Teams Web アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-202">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. <span data-ttu-id="d7f94-204">サインインするように求めるメッセージが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-204">You may be prompted to sign in.</span></span>  <span data-ttu-id="d7f94-205">その場合は、M365 アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="d7f94-205">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="d7f94-206">Teams へのアプリのインストールを促すメッセージが表示された場合は、**[追加]** を押してください。</span><span class="sxs-lookup"><span data-stu-id="d7f94-206">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="d7f94-207">これでアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-207">Your app is now displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="完了したアプリのスクリーンショット":::

<span data-ttu-id="d7f94-209">ブレークポイントの設定など、他の Web アプリケーションである場合と同様に、通常のデバッグ アクティビティを実行できます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-209">You can do normal debugging activities as if this were any other web application, such as setting breakpoints.</span></span> <span data-ttu-id="d7f94-210">このアプリはホット リロードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d7f94-210">The app supports hot reloading.</span></span> <span data-ttu-id="d7f94-211">プロジェクト内のファイルを変更すると、ページが再読み込みされます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-211">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="d7f94-212">デバッガーでアプリをローカルに実行した場合に発生することを説明します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-212">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="d7f94-213">F5 を押すと、以下のように Teams ツールキットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-213">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="d7f94-214">Azure Active Directory を使用してアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="d7f94-214">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="d7f94-215">Teams でアプリを *サイドロード* しました。</span><span class="sxs-lookup"><span data-stu-id="d7f94-215">*Sideloaded* your app in Teams.</span></span>
1. <span data-ttu-id="d7f94-216">[Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start) を使用して、アプリケーション バックエンドのローカルでの実行を開始しました。</span><span class="sxs-lookup"><span data-stu-id="d7f94-216">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="d7f94-217">アプリケーションのフロント エンドがローカルでホストされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="d7f94-217">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="d7f94-218">アプリケーションMicrosoft Teams読み込むよう指示するコマンドを使用して web ブラウザーでTeamsを開始しました `https://localhost:3000/tab` 。</span><span class="sxs-lookup"><span data-stu-id="d7f94-218">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab`.</span></span> <span data-ttu-id="d7f94-219">これは、アプリケーション マニフェストに登録されている URL です。</span><span class="sxs-lookup"><span data-stu-id="d7f94-219">This is the URL registered in the application manifest.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="d7f94-220">アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-220">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="d7f94-221">Teams でアプリを正常に実行するには、アプリのサイドロードを許可する Microsoft 365 Teams アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="d7f94-221">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="d7f94-222">アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d7f94-222">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="d7f94-223">アプリを Azure に展開した場合に発生することを説明します</span><span class="sxs-lookup"><span data-stu-id="d7f94-223">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="d7f94-224">展開前は、このアプリケーションは以下のようにローカルで動作しています。</span><span class="sxs-lookup"><span data-stu-id="d7f94-224">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="d7f94-225">バックエンドは、**Azure Functions Core Tools** を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="d7f94-225">The backend runs using **Azure Functions Core Tools**.</span></span>
1. <span data-ttu-id="d7f94-226">アプリケーションの HTTP エンドポイントは、Microsoft Teams がアプリケーションを読み込む場所でローカルに実行されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-226">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="d7f94-227">展開には、アクティブな Azure サブスクリプションでリソースをプロビジョニングし、アプリケーションのバックエンド コードとフロントエンド コードを Azure に展開またはアップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7f94-227">Deployment involves provisioning resources on an active Azure subscription and deploying or uploading the backend and frontend code for the application to Azure.</span></span>

1. <span data-ttu-id="d7f94-228">構成されている場合、バックエンドでは、Azure App Service や Azure App Service などのさまざまな Azure サービスを使用Azure Storage。</span><span class="sxs-lookup"><span data-stu-id="d7f94-228">The backend if configured uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
1. <span data-ttu-id="d7f94-229">フロントエンド アプリケーションは、静的な Web ホスティング用に構成された Azure Storage アカウントに展開されます。</span><span class="sxs-lookup"><span data-stu-id="d7f94-229">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="d7f94-230">関連項目</span><span class="sxs-lookup"><span data-stu-id="d7f94-230">See also</span></span>

- [<span data-ttu-id="d7f94-231">Blazor を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="d7f94-231">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="d7f94-232">[SharePoint Web パーツとして Teams アプリを作成する](first-app-spfx.md) (Azure は必要なし)</span><span class="sxs-lookup"><span data-stu-id="d7f94-232">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="d7f94-233">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="d7f94-233">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="d7f94-234">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="d7f94-234">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="d7f94-235">次の手順</span><span class="sxs-lookup"><span data-stu-id="d7f94-235">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7f94-236">Blazor を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="d7f94-236">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
