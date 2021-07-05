---
title: 使用を開始する - React を使用した初めての Teams アプリのビルド
author: adrianhall
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 Microsoft Teams ツールキットおよび React を使用したメッセージ。"
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: c257bcd805a6b7b38ab657cb31cad961df1c4704
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254322"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="3342c-104">React を使用した最初の Microsoft Teams アプリのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="3342c-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="3342c-105">このチュートリアルでは、React で新しい Microsoft Teams アプリを作成し、Microsoft Graph から情報を取得する簡単な個人用アプリを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3342c-105">In this tutorial, you will learn how to create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="3342c-106">たとえば、個人用アプリ *には、* 個別に使用するタブのセットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3342c-106">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="3342c-107">チュートリアルでは、Teams アプリの構造、アプリをローカルで実行する方法、Azure にアプリを展開する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3342c-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="3342c-108">ビルドされたアプリは、現在のユーザーの基本的なユーザー情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="3342c-108">The app that is built displays basic user information for the current user.</span></span> <span data-ttu-id="3342c-109">許可が付与された場合、アプリは現在のユーザーとして Microsoft Graph に接続し、完全なプロフィールを取得します。</span><span class="sxs-lookup"><span data-stu-id="3342c-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3342c-110">始める前に</span><span class="sxs-lookup"><span data-stu-id="3342c-110">Before you begin</span></span>

<span data-ttu-id="3342c-111">前提条件をインストールして、開発環境がセットアップされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="3342c-111">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3342c-112">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="3342c-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="3342c-113">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="3342c-113">Create your project</span></span>

<span data-ttu-id="3342c-114">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3342c-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="3342c-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3342c-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="3342c-116">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="3342c-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="3342c-117">次のTeams Toolkitを開き、サイドバー Teamsアイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-117">Open the Teams Toolkit and select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="3342c-119">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="3342c-121">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="3342c-123">[機能 **の選択] セクション** で、[タブ] **が選択** されているを複数選択し **、[OK] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3342c-123">In the **Select capabilities** section, varify that **Tab** is selected and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="3342c-125">**[Frontend ホスティングの種類] セクションで\*\*\*\*、[Azure] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3342c-125">In the **Frontend hosting type** section, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="新規アプリのホスティングを選択する方法を示すスクリーンショット":::。

1. <span data-ttu-id="3342c-127">[クラウド リソース **] セクションで\*\*\*\*、[OK] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3342c-127">In the **Cloud resources** section, select **OK**.</span></span>  <span data-ttu-id="3342c-128">このチュートリアルでは、追加のクラウド リソースは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="3342c-128">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="新しいアプリにクラウド リソースを追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="3342c-130">[プログラミング **言語] セクションで\*\*\*\*、[JavaScript] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3342c-130">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. <span data-ttu-id="3342c-132">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-132">Select a workspace folder.</span></span> <span data-ttu-id="3342c-133">作成するプロジェクトのワークスペース フォルダー内にフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-133">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="3342c-134">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="3342c-134">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="3342c-135">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3342c-135">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="3342c-136">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="3342c-136">Press **Enter** to continue.</span></span>

   <span data-ttu-id="3342c-137">アプリTeams数秒で作成されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-137">Your Teams app is created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="3342c-138">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="3342c-138">Command line</span></span>](#tab/cli)

<span data-ttu-id="3342c-139">`teamsfx` CLI を使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3342c-139">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="3342c-140">プロジェクト フォルダーを作成するフォルダーから開始します。</span><span class="sxs-lookup"><span data-stu-id="3342c-140">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="3342c-141">CLI では、プロジェクトを作成するためのいくつかの質問を行います。</span><span class="sxs-lookup"><span data-stu-id="3342c-141">The CLI walks through some questions to create the project.</span></span> <span data-ttu-id="3342c-142">各質問には、矢印キーを使用してオプションを選択する方法など、回答方法が示されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-142">Each question will tell you how to answer it, for example, use arrow keys to select an option.</span></span> <span data-ttu-id="3342c-143">質問に答えた後、**Enter** キーを押して選択を確認します。</span><span class="sxs-lookup"><span data-stu-id="3342c-143">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="3342c-144">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-144">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="3342c-145">タブ機能 **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="3342c-145">Select the **Tab** capability.</span></span>
1. <span data-ttu-id="3342c-146">**Azure** フロントエンド ホスティングを選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-146">Select **Azure** frontend hosting.</span></span> <span data-ttu-id="3342c-147">クラウド リソースは選択しないでください。</span><span class="sxs-lookup"><span data-stu-id="3342c-147">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="3342c-148">プログラミング言語として **[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-148">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="3342c-149">**Enter** キーを押して、既定のワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-149">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="3342c-150">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="3342c-150">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="3342c-151">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3342c-151">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="3342c-152">すべての質問に答えた後、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-152">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="3342c-153">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="3342c-153">Take a tour of the source code</span></span>

<span data-ttu-id="3342c-154">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="3342c-154">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="3342c-155">プロジェクトをTeams Toolkitした後、プロジェクト用の基本的な個人用アプリを構築するためのTeams。</span><span class="sxs-lookup"><span data-stu-id="3342c-155">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="3342c-156">プロジェクトのディレクトリとファイルには、Visual Studio Code の [エクスプローラー] 領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-156">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Visual Studio Code で個人用アプリ向けのアプリのプロジェクト ファイルを表示したスクリーンショット。":::

<span data-ttu-id="3342c-158">ツールキットは、セットアップ時に追加した機能に基づいて、プロジェクト ディレクトリにスキャフォールディングを自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="3342c-158">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="3342c-159">Teams ツールキットは、`.fx` ディレクトリにアプリの状態を保持します。</span><span class="sxs-lookup"><span data-stu-id="3342c-159">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="3342c-160">このディレクトリの他の項目の間では、以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="3342c-160">Among other items in this directory:</span></span>

- <span data-ttu-id="3342c-161">アプリ アイコンは PNG ファイルとして `color.png` と `outline.png` に格納されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-161">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="3342c-162">Developer Portal for Teams に公開するアプリのマニフェストは `manifest.source.json` に格納されています。</span><span class="sxs-lookup"><span data-stu-id="3342c-162">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="3342c-163">プロジェクト作成時に選択した設定が `settings.json` に保存されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-163">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="3342c-164">セットアップ時にタブ機能を選択したため、Teams ツールキットは基本的なタブに必要なコードをすべて `tabs` ディレクトリに格納します。</span><span class="sxs-lookup"><span data-stu-id="3342c-164">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="3342c-165">このディレクトリの中には、いくつかの重要なファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="3342c-165">Within this directory there are several important files:</span></span>

- <span data-ttu-id="3342c-166">`tabs/src/index.jsx` はフロントエンド アプリの入力ポイントで、メインの `App` コンポーネントは `ReactDOM.render()` でレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="3342c-166">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="3342c-167">`tabs/src/components/App.jsx` は、アプリの URL ルーティングを処理します。</span><span class="sxs-lookup"><span data-stu-id="3342c-167">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="3342c-168">[Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) を呼び出して、アプリと Teams の間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="3342c-168">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="3342c-169">`tabs/src/components/Tab.jsx` は、アプリの UI を実装するコードを含みます。</span><span class="sxs-lookup"><span data-stu-id="3342c-169">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="3342c-170">`tabs/src/components/TabConfig.jsx` は、アプリを構成する UI を実装するコードを含みます。</span><span class="sxs-lookup"><span data-stu-id="3342c-170">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="3342c-171">Teams ランタイムでは、プライバシー通知、利用規約、構成タブなど、いくつかのタブが必要となります。</span><span class="sxs-lookup"><span data-stu-id="3342c-171">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="3342c-172">プライバシーに関する通知と利用規約のコードは、同じディレクトリ内にあります。</span><span class="sxs-lookup"><span data-stu-id="3342c-172">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="3342c-173">クラウド機能を追加すると、プロジェクトにディレクトリが追加されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-173">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="3342c-174">最も重要なのは、`api` ディレクトリに、ユーザーが書き込んだ Azure Functions のコードが格納されていることです。</span><span class="sxs-lookup"><span data-stu-id="3342c-174">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="3342c-175">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="3342c-175">Run your app locally</span></span>

<span data-ttu-id="3342c-176">Teams ツールキットでは、アプリをローカルで実行することができます。</span><span class="sxs-lookup"><span data-stu-id="3342c-176">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="3342c-177">これは、Teams が予想する正しいインフラを提供するために必要ないくつかのパーツで構成されています。</span><span class="sxs-lookup"><span data-stu-id="3342c-177">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="3342c-178">Azure Active Directory を使用してアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="3342c-178">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="3342c-179">このアプリケーションには、アプリケーションが読み込まれる場所や、アクセスするバックエンド リソースに関連するアクセス許可があります。</span><span class="sxs-lookup"><span data-stu-id="3342c-179">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="3342c-180">認証タスクを支援する Web API がホストされ、アプリと Azure Active Directory の間のプロキシとして機能します。</span><span class="sxs-lookup"><span data-stu-id="3342c-180">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="3342c-181">これは、Azure Functions Core Tools によって実行されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-181">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="3342c-182">これは、URL `https://localhost:5000` でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3342c-182">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="3342c-183">アプリのフロントエンドを構成する HTML、CSS、JavaScript のリソースは、ローカル サービスでホストされています。</span><span class="sxs-lookup"><span data-stu-id="3342c-183">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="3342c-184">これは、`https://localhost:3000` でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3342c-184">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="3342c-185">アプリのマニフェストは、Developer Portal for Teams で生成され存在します。</span><span class="sxs-lookup"><span data-stu-id="3342c-185">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="3342c-186">Teams はアプリ マニフェストを使用して、接続しているクライアントにアプリをロードする場所を伝達します。</span><span class="sxs-lookup"><span data-stu-id="3342c-186">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="3342c-187">その後、アプリをクライアント内で読みTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="3342c-187">After this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="3342c-188">Teams の Web クライアントを使用することで、標準的な Web 開発環境で HTML、CSS、JavaScript のコードを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="3342c-188">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="3342c-189">Visual Studio Code でアプリをローカルにビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="3342c-189">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="3342c-190">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="3342c-190">To build and run your app locally:</span></span>

1. <span data-ttu-id="3342c-191">Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="3342c-191">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="3342c-192">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="3342c-192">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="3342c-193">ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="3342c-193">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="3342c-194">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="3342c-194">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="3342c-195">必要にToolkitローカル証明書のインストールを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-195">The Toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="3342c-196">この証明書により、Teams は `https://localhost` からアプリケーションを読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="3342c-196">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="3342c-197">以下のダイアログが表示されたら、「はい」を選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-197">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. <span data-ttu-id="3342c-199">Web ブラウザーがアプリの実行を開始します。</span><span class="sxs-lookup"><span data-stu-id="3342c-199">Your web browser starts to run the app.</span></span> <span data-ttu-id="3342c-200">デスクトップを開くTeams場合は、[キャンセル] を **選択して** ブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="3342c-200">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="3342c-201">また、他の場合はデスクトップに切り替Teams表示される場合があります。この場合Teams Web アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="3342c-201">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. <span data-ttu-id="3342c-203">メッセージが表示されたら、M365 アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="3342c-203">Sign in with your M365 account when prompted.</span></span>
1. <span data-ttu-id="3342c-204">Teams へのアプリのインストールを促すメッセージが表示された場合は、**[追加]** を押してください。</span><span class="sxs-lookup"><span data-stu-id="3342c-204">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="3342c-205">これでアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-205">Your app is now displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="完了したアプリのスクリーンショット":::

<span data-ttu-id="3342c-207">ブレークポイントの設定など、他の Web アプリケーションである場合と同様に、通常のデバッグ アクティビティを実行できます。</span><span class="sxs-lookup"><span data-stu-id="3342c-207">You can do normal debugging activities as if this were any other web application, such as setting breakpoints.</span></span> <span data-ttu-id="3342c-208">このアプリはホット リロードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="3342c-208">The app supports hot reloading.</span></span> <span data-ttu-id="3342c-209">プロジェクト内のファイルを変更すると、ページが再読み込みされます。</span><span class="sxs-lookup"><span data-stu-id="3342c-209">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="3342c-210">デバッガーでアプリをローカルに実行した場合に発生することを説明します。</span><span class="sxs-lookup"><span data-stu-id="3342c-210">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="3342c-211">**F5** キーを押すと、次のTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="3342c-211">When you press the **F5** key, the Teams Toolkit:</span></span>

* <span data-ttu-id="3342c-212">アプリケーションをアプリケーションに登録Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="3342c-212">Registers your application with Azure Active Directory.</span></span>
* <span data-ttu-id="3342c-213">*アプリをサイド* ロードTeams。</span><span class="sxs-lookup"><span data-stu-id="3342c-213">*Sideloads* your app in Teams.</span></span>
* <span data-ttu-id="3342c-214">Azure Function Core Tools を使用してローカルで実行されている [アプリケーション バックエンドを開始します](/azure/azure-functions/functions-run-local?#start)。</span><span class="sxs-lookup"><span data-stu-id="3342c-214">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
* <span data-ttu-id="3342c-215">ローカルでホストされているアプリケーションフロントエンドを開始します。</span><span class="sxs-lookup"><span data-stu-id="3342c-215">Starts your application front-end hosted locally.</span></span>
* <span data-ttu-id="3342c-216">アプリケーションMicrosoft Teams読み込む側に指示するコマンドTeams Web ブラウザーで開始します `https://localhost:3000/tab` 。</span><span class="sxs-lookup"><span data-stu-id="3342c-216">Starts Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab`.</span></span> <span data-ttu-id="3342c-217">これは、アプリケーション マニフェストに登録されている URL です。</span><span class="sxs-lookup"><span data-stu-id="3342c-217">This is the URL registered in the application manifest.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="3342c-218">アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3342c-218">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="3342c-219">Teams でアプリを正常に実行するには、アプリのサイドロードを許可する Microsoft 365 Teams アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="3342c-219">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="3342c-220">アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3342c-220">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="3342c-221">アプリを Azure に展開した場合に発生することを説明します</span><span class="sxs-lookup"><span data-stu-id="3342c-221">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="3342c-222">展開前は、このアプリケーションは以下のようにローカルで動作しています。</span><span class="sxs-lookup"><span data-stu-id="3342c-222">Before deployment, the application has been running locally:</span></span>

* <span data-ttu-id="3342c-223">バックエンドは、**Azure Functions Core Tools** を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="3342c-223">The backend runs using **Azure Functions Core Tools**.</span></span>
* <span data-ttu-id="3342c-224">アプリケーションの HTTP エンドポイントは、Microsoft Teams がアプリケーションを読み込む場所でローカルに実行されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-224">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="3342c-225">展開には、アクティブな Azure サブスクリプションでリソースをプロビジョニングし、アプリケーションのバックエンド コードとフロントエンド コードを Azure に展開またはアップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3342c-225">Deployment involves provisioning resources on an active Azure subscription and deploying or uploading the backend and frontend code for the application to Azure.</span></span>

* <span data-ttu-id="3342c-226">構成されている場合、バックエンドでは、Azure App Service や Azure App Service などのさまざまな Azure サービスを使用Azure Storage。</span><span class="sxs-lookup"><span data-stu-id="3342c-226">The backend if configured uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
* <span data-ttu-id="3342c-227">フロントエンド アプリケーションは、静的な Web ホスティング用に構成された Azure Storage アカウントに展開されます。</span><span class="sxs-lookup"><span data-stu-id="3342c-227">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="3342c-228">関連項目</span><span class="sxs-lookup"><span data-stu-id="3342c-228">See also</span></span>

* [<span data-ttu-id="3342c-229">チュートリアルの概要</span><span class="sxs-lookup"><span data-stu-id="3342c-229">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="3342c-230">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="3342c-230">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="3342c-231">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="3342c-231">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="3342c-232">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="3342c-232">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
