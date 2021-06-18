---
title: 開始する - アプリを使用して最初のTeamsアプリをSPFx
author: zhenyasav
description: カスタム タブを作成する方法については、SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 23df721a28225a8c453274e6e77efa8f756e84f3
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994372"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a><span data-ttu-id="2ab56-103">アプリで最初のアプリをビルドMicrosoft Teams実行する (SharePoint Framework) (SPFx)</span><span class="sxs-lookup"><span data-stu-id="2ab56-103">Build and run your first Microsoft Teams app with SharePoint Framework (SPFx)</span></span>

<span data-ttu-id="2ab56-104">このチュートリアルでは、単純な個人用アプリを実装Microsoft Teams (SharePoint Framework) SPFx新しいアプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-104">In this tutorial, you will create a new Microsoft Teams app in SharePoint Framework (SPFx) that implements a simple personal app.</span></span> <span data-ttu-id="2ab56-105">(個人用 *アプリには、* 個々の使用を対象にした一連のタブが含まれます)。チュートリアルでは、Teams アプリの構造、アプリをローカルで実行する方法、およびアプリを SharePoint に展開する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-105">(A *personal app* includes a set of tabs scoped for individual use.) During the tutorial, you will learn about the structure of a Teams app, how to run the app locally, and how to deploy the app to SharePoint.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2ab56-106">始める前に</span><span class="sxs-lookup"><span data-stu-id="2ab56-106">Before you begin</span></span>

<span data-ttu-id="2ab56-107">[前提条件](prerequisites.md)をインストールして、開発環境が整っていることを確認する</span><span class="sxs-lookup"><span data-stu-id="2ab56-107">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ab56-108">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="2ab56-108">Install prerequisites</span></span>](prerequisites.md)

## <a name="get-organized"></a><span data-ttu-id="2ab56-109">すっきり整理しましょう。</span><span class="sxs-lookup"><span data-stu-id="2ab56-109">Get organized</span></span>

<span data-ttu-id="2ab56-110">前提条件に加えて、サイト コレクションの管理者SharePoint必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ab56-110">In addition to the prerequisites, you also need to be an Administrator for a SharePoint Site Collection.</span></span>  <span data-ttu-id="2ab56-111">ここで、ホスティング用にアプリを展開します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-111">This is where you will deploy your app for hosting.</span></span>  <span data-ttu-id="2ab56-112">M365 開発者プログラム テナントを使用している場合は、プログラムに登録するときに設定した管理者アカウントを使用します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-112">If you are using an M365 developer program tenant, use the administrator account you set up when you registered for the program.</span></span>  

## <a name="create-your-project"></a><span data-ttu-id="2ab56-113">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="2ab56-113">Create your project</span></span>

<span data-ttu-id="2ab56-114">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="2ab56-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2ab56-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="2ab56-116">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="2ab56-117">サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-117">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="2ab56-119">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="2ab56-121">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="2ab56-123">**[機能の選択]** 手順では、**[タブ]** 機能がすでに選択されています。</span><span class="sxs-lookup"><span data-stu-id="2ab56-123">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="2ab56-124">**[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-124">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="2ab56-126">Frontend **ホスティングの種類の手順で**、[SharePoint Framework **] (SPFx) を選択します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-126">On the **Frontend hosting type** step, select **SharePoint Framework (SPFx)**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="新規アプリのホスティングを選択する方法を示すスクリーンショット":::。

1. <span data-ttu-id="2ab56-128">[フレームワーク]**ステップで**、[設定]**をReact。**</span><span class="sxs-lookup"><span data-stu-id="2ab56-128">On the **Framework** step, select **React**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Select Framework":::

1. <span data-ttu-id="2ab56-130">Web パーツ名を求める **メッセージが表示された場合** は **、Enter キーを押** して既定値を受け入れる。</span><span class="sxs-lookup"><span data-stu-id="2ab56-130">When asked for a **Webpart Name**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="2ab56-131">Web パーツの説明を求める **メッセージが表示された** 場合は **、Enter キーを押** して既定値を受け入れる。</span><span class="sxs-lookup"><span data-stu-id="2ab56-131">When asked for the **Webpart Description**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="2ab56-132">プログラミング言語の入力を求 **めるメッセージが表示された場合は、Enter\*\*\*\*キーを押** して既定値を受け入れる。</span><span class="sxs-lookup"><span data-stu-id="2ab56-132">When asked for the **Programming Language**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="2ab56-133">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-133">Select a workspace folder.</span></span>  <span data-ttu-id="2ab56-134">ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-134">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="2ab56-135">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-135">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="2ab56-136">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ab56-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="2ab56-137">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-137">Press **Enter** to continue.</span></span>

<span data-ttu-id="2ab56-138">数秒後に Teams アプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-138">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="2ab56-139">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="2ab56-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="2ab56-140">`teamsfx` CLI を使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="2ab56-141">プロジェクト フォルダーを作成するフォルダーから開始します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="2ab56-142">CLI では、プロジェクトを作成するためのいくつかの質問を行います。</span><span class="sxs-lookup"><span data-stu-id="2ab56-142">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="2ab56-143">各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。</span><span class="sxs-lookup"><span data-stu-id="2ab56-143">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="2ab56-144">質問に答えた後、**Enter** キーを押して選択を確認します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="2ab56-145">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="2ab56-146">**[タブ]** 機能を選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-146">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="2ab56-147">[SharePoint Framework **(SPFx)** フロントエンド ホスティング] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-147">Select **SharePoint Framework (SPFx)** frontend hosting.</span></span>
1. <span data-ttu-id="2ab56-148">[フレームワーク **React** 選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-148">Select **React** framework.</span></span>
1. <span data-ttu-id="2ab56-149">Web **パーツ名の Enter** **キーを押します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-149">Press **Enter** for the **Webpart Name**.</span></span>
1. <span data-ttu-id="2ab56-150">Web **パーツの説明** に **対して Enter キーを押します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-150">Press **Enter** for the **Webpart Description**.</span></span>
1. <span data-ttu-id="2ab56-151">プログラミング **言語の Enter** **キーを押します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-151">Press **Enter** for the **Programming Language**.</span></span>
1. <span data-ttu-id="2ab56-152">**Enter** キーを押して、既定のワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-152">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="2ab56-153">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-153">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="2ab56-154">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ab56-154">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="2ab56-155">すべての質問に答えると、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-155">Once all the questions have been answered, your project will be created.</span></span>

---

- [<span data-ttu-id="2ab56-156">ユーザー向け開発の詳細については、SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="2ab56-156">Learn more about developing for SharePoint Framework</span></span>](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="2ab56-157">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="2ab56-157">Take a tour of the source code</span></span>

<span data-ttu-id="2ab56-158">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-158">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="2ab56-159">プロジェクトをTeams Toolkitしたら、コンポーネントを使用して、Teams 内でホストされているユーザー用の基本的な個人用アプリをSharePoint Framework。</span><span class="sxs-lookup"><span data-stu-id="2ab56-159">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams that is hosted within the SharePoint Framework.</span></span>  <span data-ttu-id="2ab56-160">プロジェクトのディレクトリとファイルには、Visual Studio Code の [エクスプローラー] 領域に表示されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-160">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Visual Studio Code で個人用アプリ向けのアプリのプロジェクト ファイルを表示したスクリーンショット。":::

<span data-ttu-id="2ab56-162">ツールキットは、セットアップ時に追加した機能に基づいて、プロジェクト ディレクトリにスキャフォールディングを自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-162">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="2ab56-163">Teams ツールキットは、`.fx` ディレクトリにアプリの状態を保持します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-163">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="2ab56-164">このディレクトリの他の項目の間では、以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="2ab56-164">Among other items in this directory:</span></span>

- <span data-ttu-id="2ab56-165">アプリ アイコンは PNG ファイルとして `color.png` と `outline.png` に格納されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-165">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="2ab56-166">開発者ポータルに発行するアプリ マニフェストは、Teamsに格納されます `manifest.source.json` 。</span><span class="sxs-lookup"><span data-stu-id="2ab56-166">The app manifest for publishing to Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="2ab56-167">プロジェクト作成時に選択した設定が `settings.json` に保存されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-167">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="2ab56-168">Webpart プロジェクトでSPFxしたので、次のファイルは UI に関連します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-168">Since you selected an SPFx Webpart project, the following files are relevant to your UI:</span></span>

- <span data-ttu-id="2ab56-169">フォルダーには `SPFx/src/webparts/{webpart}` 、webpart のSPFxされます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-169">The folder `SPFx/src/webparts/{webpart}` contains your SPFx webpart.</span></span>
- <span data-ttu-id="2ab56-170">このファイル `.vscode/launch.json` には、デバッグ パレットで使用できるデバッグ構成が記述されています。</span><span class="sxs-lookup"><span data-stu-id="2ab56-170">The file `.vscode/launch.json` describes the debugging configurations available in the debug palette.</span></span>

<span data-ttu-id="2ab56-171">Webparts for SharePointのTeamsについては、次の[ドキュメントをSharePointしてください](/sharepoint/dev/spfx/build-for-teams-overview)。</span><span class="sxs-lookup"><span data-stu-id="2ab56-171">For more information about SharePoint Webparts for Teams, [refer to the SharePoint documentation](/sharepoint/dev/spfx/build-for-teams-overview).</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="2ab56-172">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="2ab56-172">Run your app locally</span></span>

<span data-ttu-id="2ab56-173">Teams Toolkitを使用すると、アプリをローカルでホストし、ワークベンチから実行SharePoint Framework[できます](/sharepoint/dev/spfx/debug-in-vscode)。</span><span class="sxs-lookup"><span data-stu-id="2ab56-173">Teams Toolkit allows you to host your app locally and run it through the [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="2ab56-174">Visual Studio Code でアプリをローカルにビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="2ab56-174">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="2ab56-175">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="2ab56-175">To build and run your app locally:</span></span>

1. <span data-ttu-id="2ab56-176">[Visual Studio Code F5]**を押します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-176">From Visual Studio Code, press **F5**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="ローカル ワークベンチでアプリをSPFxする方法を示すスクリーンショット。":::

   > [!NOTE]
   > <span data-ttu-id="2ab56-178">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-178">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="2ab56-179">ビルドが完了すると、ブラウザー ウィンドウが自動的に開SharePointワークベンチが読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-179">A browser window automatically opens and loads the SharePoint Workbench when the build is complete.</span></span>  <span data-ttu-id="2ab56-180">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="2ab56-180">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="2ab56-181">ワークベンチがSharePointしたら。</span><span class="sxs-lookup"><span data-stu-id="2ab56-181">Once the SharePoint Workbench is loaded.</span></span>

   >[!NOTE]
   > <span data-ttu-id="2ab56-182">ツールキットでは、必要に応じてローカル証明書をインストールするようメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-182">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="2ab56-183">この証明書により、Teams は `https://localhost` からアプリケーションを読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="2ab56-184">以下のダイアログが表示されたら、「はい」を選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. <span data-ttu-id="2ab56-186">[Web パーツの追加 **]** (+) アイコンのいずれかを押して、Web パーツを追加します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-186">Press one of the **Add Webpart** (+) icons to add your webpart.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="ポップアップで実行されているSPFxを示すスクリーンショットを示し、Web パーツを表示します。":::

1. <span data-ttu-id="2ab56-188">メニューから Web パーツを選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-188">Choose your webpart from the menu.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="ポップアップと一緒にSPFxワークベンチで Web パーツの選択を追加する方法を示すスクリーンショット。":::

<span data-ttu-id="2ab56-190">アプリが実行されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ab56-190">Your app should now be running.</span></span>  <span data-ttu-id="2ab56-191">通常のデバッグ アクティビティは、他の web パーツ (ブレークポイントの設定など) と同様SPFx実行できます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-191">You can do normal debugging activities as if this were any other SPFx webpart (such as setting breakpoints).</span></span>

> [!TIP]
> <span data-ttu-id="2ab56-192">ブラウザー ウィンドウの render メソッドにブレークポイントを配置し `SPFx/src/webparts/{webpart}/{webpart}.ts` 、再読み込みしてみてください。</span><span class="sxs-lookup"><span data-stu-id="2ab56-192">Try placing breakpoints in the render method of `SPFx/src/webparts/{webpart}/{webpart}.ts` and reloading the browser window.</span></span> <span data-ttu-id="2ab56-193">VS Codeコード内のブレークポイントで停止します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-193">VS Code will stop on breakpoints in your code.</span></span>

## <a name="deploy-your-app-to-sharepoint"></a><span data-ttu-id="2ab56-194">アプリをアプリに展開SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ab56-194">Deploy your app to SharePoint</span></span>

<span data-ttu-id="2ab56-195">展開にSharePointアプリ カタログが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-195">Ensure a SharePoint App Catalog exists in your deployment.</span></span>  <span data-ttu-id="2ab56-196">存在しない場合は、作成 [します](/sharepoint/use-app-catalog)。</span><span class="sxs-lookup"><span data-stu-id="2ab56-196">If one does not exist, [create one](/sharepoint/use-app-catalog).</span></span>  <span data-ttu-id="2ab56-197">アプリ カタログを完全に作成するには、最大で 15 分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="2ab56-197">It may take up to 15 minutes for the app catalog to be fully created.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="2ab56-198">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2ab56-198">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="2ab56-199">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-199">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="2ab56-200">サイドバーからTeams Toolkitアイコンを選択してTeamsします。</span><span class="sxs-lookup"><span data-stu-id="2ab56-200">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="2ab56-201">[クラウド **でプロビジョニング] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-201">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="プロビジョニング コマンドを示すスクリーンショット":::

1. <span data-ttu-id="2ab56-203">右下隅のダイアログを見て、進行状況を監視できます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-203">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="2ab56-204">数秒後に、次の通知が表示されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-204">After a few seconds, you will see the following notice:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="プロビジョニング完了ダイアログを示すスクリーンショット。":::

1. <span data-ttu-id="2ab56-206">プロビジョニングが完了したら、[クラウドに **展開する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-206">Once provisioning is complete, select **Deploy to the cloud**.</span></span>

1. <span data-ttu-id="2ab56-207">現在、自動展開は使用できません。</span><span class="sxs-lookup"><span data-stu-id="2ab56-207">Currently, automated deployment is not available.</span></span>  <span data-ttu-id="2ab56-208">手動でビルドして展開するように求めるダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-208">A dialog will pop up prompting you to build and deploy manually.</span></span> <span data-ttu-id="2ab56-209">[**ビルド] パッケージをSharePoint押します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-209">Press **Build SharePoint Package**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="[Sharepoint パッケージのビルド] ダイアログのスクリーンショット":::

# <a name="command-line"></a>[<span data-ttu-id="2ab56-211">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="2ab56-211">Command line</span></span>](#tab/cli)

<span data-ttu-id="2ab56-212">ターミナル ウィンドウで次の設定を行います。</span><span class="sxs-lookup"><span data-stu-id="2ab56-212">In your terminal window:</span></span>

1. <span data-ttu-id="2ab56-213">`teamsfx provision` を実行します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-213">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="2ab56-214">Azure サブスクリプションにログインするように求めるメッセージが表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="2ab56-214">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="2ab56-215">必要に応じて、Azure リソースに使用する Azure サブスクリプションを選択するように求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-215">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2ab56-216">アプリのホスティングに使用される Azure リソースは常にいくつかある。</span><span class="sxs-lookup"><span data-stu-id="2ab56-216">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="2ab56-217">`teamsfx deploy` を実行します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-217">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

1. <span data-ttu-id="2ab56-218">メッセージが表示されたら、[パッケージの **ビルドSharePoint選択します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-218">When prompted, select **Build SharePoint Package**.</span></span>

---

<span data-ttu-id="2ab56-219">パッケージSharePointプロジェクト内 `SPFx/sharepoint/solution` に保存されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-219">The SharePoint package is located in `SPFx/sharepoint/solution` within your project.</span></span>  <span data-ttu-id="2ab56-220">アップロードを次の方法でSharePoint。</span><span class="sxs-lookup"><span data-stu-id="2ab56-220">Upload the package to SharePoint:</span></span>

1. <span data-ttu-id="2ab56-221">M365 管理コンソールにログインし、アプリ カタログSharePoint移動します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-221">Log into the M365 Admin Console, then navigate to the SharePoint App Catalog.</span></span>

   - <span data-ttu-id="2ab56-222">を `https://admin.microsoft.com/AdminPortal/Home` 開きます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-222">Open `https://admin.microsoft.com/AdminPortal/Home`.</span></span>
   - <span data-ttu-id="2ab56-223">[**管理センター] で**、**管理センター** SharePoint選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-223">Under **Admin centers**, select the **SharePoint** admin center.</span></span>
   - <span data-ttu-id="2ab56-224">サイドバー メニュー **から [その他の** 機能] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-224">Select **More features** from the sidebar menu.</span></span>
   - <span data-ttu-id="2ab56-225">[アプリ **] で [開く** ] **を押します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-225">Press **Open** under **Apps**.</span></span>
   - <span data-ttu-id="2ab56-226">[アプリ **カタログ] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-226">Select **App Catalog**.</span></span>

1. <span data-ttu-id="2ab56-227">[アプリ **の配布] を選択SharePoint。**</span><span class="sxs-lookup"><span data-stu-id="2ab56-227">Select **Distribute apps for SharePoint**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="アプリを配布SharePoint。":::

1. <span data-ttu-id="2ab56-229">[アップロード]**を選択します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-229">Select **Upload**.</span></span>

1. <span data-ttu-id="2ab56-230">[ファイル **の選択] を押します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-230">Press **Choose File**.</span></span>

1. <span data-ttu-id="2ab56-231">プロジェクト内 `{project}.sppkg` のフォルダーにあるファイル `SPFx/sharepoint/solution` を探します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-231">Locate your `{project}.sppkg` file, located in the `SPFx/sharepoint/solution` folder within your project.</span></span>  <span data-ttu-id="2ab56-232">[開 **く] を押します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-232">Press **Open**.</span></span>

1. <span data-ttu-id="2ab56-233">**[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-233">Press **OK**.</span></span>

1. <span data-ttu-id="2ab56-234">展開SharePoint自動的に開始されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-234">The SharePoint deployment process will automatically start.</span></span>  <span data-ttu-id="2ab56-235">[ **組織内のすべてのサイトでこのソリューション** を使用できる] チェック ボックスをオンにし、[展開] を **押します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-235">Ensure **Make this solution available to all sites in the organization** is checked, then press **Deploy**.</span></span>

1. <span data-ttu-id="2ab56-236">[ファイル] **タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="2ab56-236">Select the **FILES** tab.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="[アプリ カタログ] の [ファイル] タブSharePoint選択します。":::

1. <span data-ttu-id="2ab56-238">展開したパッケージを選択し、[同期] を押 **してリボンTeams** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2ab56-238">select the package you deployed, then press **Sync to Teams** in the ribbon.</span></span>

    > [!Note]
    > <span data-ttu-id="2ab56-239">同期プロセスTeams数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="2ab56-239">The Sync to Teams process can take a couple of minutes.</span></span>  <span data-ttu-id="2ab56-240">ブラウザーの右側に、アプリが正常に同期されたことを示すメッセージが表示Teams。</span><span class="sxs-lookup"><span data-stu-id="2ab56-240">You will see a message on the right-hand side of the browser indicating that the app has successfully synchronized to Teams.</span></span>

<span data-ttu-id="2ab56-241">アプリケーションを開Teams (またはサインイン時 `https://teams.microsoft.com` )。</span><span class="sxs-lookup"><span data-stu-id="2ab56-241">Open the Teams application (or sign in at `https://teams.microsoft.com`).</span></span>  <span data-ttu-id="2ab56-242">サイドバーのトリプルドットを押し、[すべてのアプリ] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="2ab56-242">Press the triple-dot on the sidebar, then select **All apps**.</span></span>  <span data-ttu-id="2ab56-243">アプリは、組織カテゴリ用 **に構築されたアプリに配置** されます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-243">The app will be placed in the **Apps built for your org** category.</span></span>  <span data-ttu-id="2ab56-244">そこからアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="2ab56-244">You can add the app from there.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="アプリ内のアプリを示すスクリーンショットTeams":::

## <a name="see-also"></a><span data-ttu-id="2ab56-246">関連項目</span><span class="sxs-lookup"><span data-stu-id="2ab56-246">See also</span></span>

- [<span data-ttu-id="2ab56-247">React を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="2ab56-247">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="2ab56-248">Blazor を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="2ab56-248">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="2ab56-249">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="2ab56-249">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="2ab56-250">次の手順</span><span class="sxs-lookup"><span data-stu-id="2ab56-250">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ab56-251">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="2ab56-251">Create a conversational bot app</span></span>](first-app-bot.md)
