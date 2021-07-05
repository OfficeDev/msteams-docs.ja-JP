---
title: チュートリアル - Yeoman ジェネレーターを使用して最初のアプリを作成する
description: Yeoman ジェネレーターを使用してアプリMicrosoft Teamsを開始する方法について学習します。
keywords: nodejs yeoman node.jsを開始する
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: a3519da1495dc51a811f4e95bc4ada9b11aa8292
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254360"
---
# <a name="build-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="3d32e-104">Yeoman ジェネレーターを使用Microsoft Teamsアプリをビルドする</span><span class="sxs-lookup"><span data-stu-id="3d32e-104">Build your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="3d32e-105">このチュートリアルは、Wiki の[Yeoman ジェネレーター Teamsです](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。</span><span class="sxs-lookup"><span data-stu-id="3d32e-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="3d32e-106">このチュートリアルでは、Yeoman ジェネレーターを使用して最初のアプリをMicrosoft TeamsするMicrosoft Teams説明します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-106">In this tutorial, you will learn how to build your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="3d32e-107">また、Yeoman ジェネレーターを使用してアプリケーションをアップグレードTeams手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="3d32e-108">開始する前に、アプリのサイドローディングをTeamsアカウント[を持っている必要があります](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="3d32e-108">Before you begin, you must have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![yeoman ジェネレーター git](~/assets/yeoman-demo.gif)

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="3d32e-110">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="3d32e-110">Get Prerequisites</span></span>

<span data-ttu-id="3d32e-111">Yeoman ジェネレーターの使用を開始する前に、コンピューターに以下をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-111">You need to install the following on your machine before starting to use the Yeoman generator:</span></span>

* <span data-ttu-id="3d32e-112">Node.js</span><span class="sxs-lookup"><span data-stu-id="3d32e-112">Node.js</span></span>

   <span data-ttu-id="3d32e-113">コンピューターにインストールNode.js必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="3d32e-114">最新の [LTS バージョンを使用する必要があります](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="3d32e-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

* <span data-ttu-id="3d32e-115">コード エディター</span><span class="sxs-lookup"><span data-stu-id="3d32e-115">A code editor</span></span>

   <span data-ttu-id="3d32e-116">コード エディターが必要です。</span><span class="sxs-lookup"><span data-stu-id="3d32e-116">You need a code editor.</span></span> <span data-ttu-id="3d32e-117">このドキュメントと画像の大部分は、このドキュメントを使用[Visual Studio Code。](https://code.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="3d32e-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="3d32e-118">ただし、必要なテキスト エディターを自由に使用できます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-118">However, feel free to use whatever text editor you prefer.</span></span>

* <span data-ttu-id="3d32e-119">Yeoman と Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="3d32e-119">Yeoman and Gulp CLI</span></span>

   <span data-ttu-id="3d32e-120">ジェネレーターを使用してプロジェクトをスキャフォールディングするには、Yeoman ツールと Gulp CLI タスク マネージャーをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

   <span data-ttu-id="3d32e-121">コマンド プロンプトを開き、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-121">Open up a command prompt and type the following:</span></span>

   ```bash
   npm install yo gulp-cli --global
   ```

## <a name="install-the-generator"></a><span data-ttu-id="3d32e-122">ジェネレーターのインストール</span><span class="sxs-lookup"><span data-stu-id="3d32e-122">Install the generator</span></span>

<span data-ttu-id="3d32e-123">次のコマンドTeams Yeoman ジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="3d32e-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm init yo teams
```

<span data-ttu-id="3d32e-124">次のコマンドを使用して、ジェネレーターのプレビュー バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="3d32e-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm init yo teams@preview
```

## <a name="generate-your-project"></a><span data-ttu-id="3d32e-125">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="3d32e-125">Generate your project</span></span>

<span data-ttu-id="3d32e-126">このセクションでは、プロジェクトを生成する手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-126">This section walks you through the steps to generate your project.</span></span>

<span data-ttu-id="3d32e-127">**プロジェクトを生成するには**</span><span class="sxs-lookup"><span data-stu-id="3d32e-127">**To generate your project**</span></span>

1. <span data-ttu-id="3d32e-128">コマンド プロンプトを開き、プロジェクトを作成する新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-128">Open a command prompt and create a new directory where you want to create your project.</span></span>
1. <span data-ttu-id="3d32e-129">ディレクトリに移動し、コマンドを実行します `yo teams` 。</span><span class="sxs-lookup"><span data-stu-id="3d32e-129">Go to the directory, and run the command `yo teams`.</span></span> <span data-ttu-id="3d32e-130">ジェネレーターが起動します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-130">The generator starts.</span></span>
1. <span data-ttu-id="3d32e-131">ジェネレーターから求める一連の質問に応答します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-131">Respond to the set of questions prompted by the generator:</span></span>

   ![yo チーム](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="3d32e-133">プロジェクトの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-133">Enter a name for your project.</span></span> <span data-ttu-id="3d32e-134">Enter キーを押すとそのままにできます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-134">You can leave it as is by pressing Enter.</span></span>
   1. <span data-ttu-id="3d32e-135">新しいディレクトリを作成する場合は、新しいディレクトリのパスを入力します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-135">Enter a path for the new directory if you want to create a new directory.</span></span> <span data-ttu-id="3d32e-136">必要なディレクトリに既に存在する場合は、Enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-136">As you are already in the directory you want, just press Enter.</span></span>
   1. <span data-ttu-id="3d32e-137">プロジェクトのタイトルを入力します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-137">Enter the title of your project.</span></span> <span data-ttu-id="3d32e-138">このタイトルは、アプリのマニフェストと説明で使用されます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-138">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="3d32e-139">マニフェストでも使用する会社名を入力します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-139">Enter a company name which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="3d32e-140">使用するマニフェストのバージョンを入力します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-140">Enter the version of the manifest you want to use.</span></span> <span data-ttu-id="3d32e-141">このチュートリアルでは、 `v1.5` 現在利用可能な一般的なスキーマを選択します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-141">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="3d32e-142">プロジェクトに追加するアイテムを選択します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-142">Select the items you want to add to your project.</span></span> <span data-ttu-id="3d32e-143">アイテムの 1 つまたは任意の組み合わせを選択できます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-143">You can select a single one or any combination of items.</span></span> <span data-ttu-id="3d32e-144">このチュートリアルでは、タブを *選択します*。</span><span class="sxs-lookup"><span data-stu-id="3d32e-144">For this tutorials, just select *a Tab*:</span></span>

    ![アイテムの選択](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="3d32e-146">手順 2 で選択した項目に基づいて表示される次のフォローアップ質問のセットに応答します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-146">Respond to the next set of follow-up questions that appear based on the items you selected in Step 2.</span></span>
1. <span data-ttu-id="3d32e-147">ソリューションをホストする場所の URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-147">Enter a URL for the location where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="3d32e-148">URL には任意の URL を指定できますが、既定ではジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-148">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="3d32e-149">ソリューションに単体テストを含める必要がある場合は、確認します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-149">Confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="3d32e-150">既定の応答は Yes **です**。</span><span class="sxs-lookup"><span data-stu-id="3d32e-150">The default response is **Yes**.</span></span> <span data-ttu-id="3d32e-151">単体テストを含める場合、生成されたプロジェクトには単体テスト フレームワークと、スキャフォールディングされるさまざまなアイテムに対する既定の単体テストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-151">If you opt to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="3d32e-152">このチュートリアルでは、テスト フレームワークを含めないを選択します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-152">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="3d32e-153">ジェネレーターには、オプトインまたはオプトアウトできる多くの組み込みの高度な機能があります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-153">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="3d32e-154">サインインを簡単に行う場合は、Azure Application インサイトを使用インサイトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-154">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="3d32e-155">[はい]**を選択** した場合は、Azure アプリケーション キーを指定インサイトがあります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-155">If you select **Yes**, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="3d32e-156">このチュートリアルでは、Application インサイト を使用インサイト。</span><span class="sxs-lookup"><span data-stu-id="3d32e-156">For this tutorial opt-out of using Application Insights.</span></span>

   <span data-ttu-id="3d32e-157">次の質問のセットは、以前に選択したアイテムに基づいて行います。</span><span class="sxs-lookup"><span data-stu-id="3d32e-157">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="3d32e-158">タブの場合は、名前を指定し、必要に応じて、このアプリをオンライン Web パーツとして使用SharePoint選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-158">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="3d32e-159">名前を指定すると、ジェネレーターはプロジェクトを生成し、すべての依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="3d32e-159">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="3d32e-160">これには 1 分または 2 分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-160">This will take a minute or two.</span></span>

## <a name="add-code-to-your-tab"></a><span data-ttu-id="3d32e-161">タブにコードを追加する</span><span class="sxs-lookup"><span data-stu-id="3d32e-161">Add code to your tab</span></span>

<span data-ttu-id="3d32e-162">ジェネレーターが完了したら、お気に入りのコード エディターでソリューションを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-162">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="3d32e-163">1 分か 2 分で、コードの整理方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-163">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="3d32e-164">詳細については、「構造」[のドキュメントProject参照](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)してください。</span><span class="sxs-lookup"><span data-stu-id="3d32e-164">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="3d32e-165">タブがファイル内 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` にあります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-165">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="3d32e-166">これは、タブの typeScript Reactベースのクラスです。</span><span class="sxs-lookup"><span data-stu-id="3d32e-166">This is the TypeScript React-based class for your tab.</span></span> 

1. <span data-ttu-id="3d32e-167">メソッドを `render()` 見つけて、コントロール内にコード行を追加して `<PanelBody>` 、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="3d32e-167">Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

   ``` TypeScript
   <PanelBody>
      <div style={styles.section}>
      Hello World! Yo Teams rocks!
      </div>
   </PanelBody>
   ```
1. <span data-ttu-id="3d32e-168">ファイルを保存し、コマンド プロンプトに戻します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-168">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="3d32e-169">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="3d32e-169">Build your app</span></span>

<span data-ttu-id="3d32e-170">これで、プロジェクトをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-170">You can now build your project.</span></span> <span data-ttu-id="3d32e-171">これは 2 つの手順で行います。</span><span class="sxs-lookup"><span data-stu-id="3d32e-171">This is done in two steps.</span></span>

1. <span data-ttu-id="3d32e-172">アプリにTeamsしたアプリのアプリ マニフェスト ファイルを作成Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="3d32e-172">Create the Teams App manifest file for the app that you uploaded into Microsoft Teams.</span></span> <span data-ttu-id="3d32e-173">これは Gulp タスクによって実行されます `gulp manifest` 。</span><span class="sxs-lookup"><span data-stu-id="3d32e-173">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="3d32e-174">これにより、マニフェストが検証され、ディレクトリに zip ファイルが作成 `./package` されます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-174">This will validate the manifest and create a zip file in the `./package` directory.</span></span>
1. <span data-ttu-id="3d32e-175">コマンドを `gulp build` 実行してソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="3d32e-175">Run the `gulp build` command to build the solution.</span></span> <span data-ttu-id="3d32e-176">これにより、ソリューションがフォルダーに変換 `./dist` されます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-176">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="3d32e-177">アプリの実行</span><span class="sxs-lookup"><span data-stu-id="3d32e-177">Run your app</span></span>

<span data-ttu-id="3d32e-178">アプリを実行するには、コマンドを使用 `gulp serve` します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-178">To run your app, use the `gulp serve` command.</span></span> <span data-ttu-id="3d32e-179">これにより、アプリをテストするためのローカル Web サーバーが構築され、開始されます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-179">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="3d32e-180">また、プロジェクトにファイルを保存するたびに、このコマンドはアプリケーションを再構築します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-180">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="3d32e-181">次に移動し、タブ `http://localhost:3007/myFirstAppTab/` がレンダリングされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-181">You should now be go to `http://localhost:3007/myFirstAppTab/` and ensure that your tab is rendering.</span></span> <span data-ttu-id="3d32e-182">ただし、まだMicrosoft Teamsされていません。</span><span class="sxs-lookup"><span data-stu-id="3d32e-182">However, it is not in Microsoft Teams yet.</span></span> 

<span data-ttu-id="3d32e-183">**タブをレンダリングするには、Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="3d32e-183">**To render your tab in Microsoft Teams**</span></span>

![ブラウザーでサイトを表示する](~/assets/yeoman-images/teams-first-app-3.png)

### <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="3d32e-185">アプリをアプリで実行Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3d32e-185">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="3d32e-186">Microsoft Teamsアプリを localhost でホストすることはできませんので、パブリック URL に公開するか、ngrok などのプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-186">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span> <span data-ttu-id="3d32e-187">良いニュースは、スキャフォールディングされたプロジェクトにこの組み込みがあります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-187">Good news is that the scaffolded project has this built-in.</span></span> 

<span data-ttu-id="3d32e-188">**アプリをアプリで実行Teams**</span><span class="sxs-lookup"><span data-stu-id="3d32e-188">**To run your app in Teams**</span></span>

1. <span data-ttu-id="3d32e-189">ターミナル `gulp ngrok-serve` で実行します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-189">Run `gulp ngrok-serve` in Terminal.</span></span> <span data-ttu-id="3d32e-190">ngrok サービスを実行すると、一意のパブリック DNS エントリを使用してバックグラウンドで開始され、その一意の URL でマニフェストがパッケージ化され、その後とまったく同じ処理を実行 `gulp ngrok-serve` します `gulp serve` 。</span><span class="sxs-lookup"><span data-stu-id="3d32e-190">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>
1. <span data-ttu-id="3d32e-191">新しいチームをMicrosoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="3d32e-191">Create a new Microsoft Teams team.</span></span>
1. <span data-ttu-id="3d32e-192">[アプリ] で [チーム名> Teams 設定 >選択します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-192">Select the Team name > Teams Settings > Apps.</span></span>
1. <span data-ttu-id="3d32e-193">右下隅から、カスタム アプリアップロード **選択します**。</span><span class="sxs-lookup"><span data-stu-id="3d32e-193">From the lower right corner, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="3d32e-194">プロジェクト フォルダーの `package` 下のフォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-194">Go to the `package` folder under your project folder.</span></span> 
1. <span data-ttu-id="3d32e-195">そのフォルダー内の zip ファイルを選択し、[開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-195">Select the zip file in that folder and select open.</span></span> 
   <span data-ttu-id="3d32e-196">これで、アプリは次の方法でサイドMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="3d32e-196">Your App is now sideloaded into Microsoft Teams:</span></span>

   ![サイドロードされたアプリ](~/assets/yeoman-images/teams-first-app-4.png)
1. <span data-ttu-id="3d32e-198">[全般] チャネルに **戻り** 、新 **+** しいタブを追加します。タブの一覧にタブが表示されます。タブ ![ の構成](~/assets/yeoman-images/teams-first-app-5.png)</span><span class="sxs-lookup"><span data-stu-id="3d32e-198">Go back to the **General** channel and select **+** to add a new Tab. You should see your tab in the list of tabs: ![configure tab](~/assets/yeoman-images/teams-first-app-5.png)</span></span>
1. <span data-ttu-id="3d32e-199">タブを選択し、指示に従って追加します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-199">Select your tab and follow the instructions to add it.</span></span> <span data-ttu-id="3d32e-200">カスタム構成ダイアログが表示され、ソースを編集できます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-200">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="3d32e-201">[保存 *] を* 選択して、タブをチャネルに追加します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-201">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="3d32e-202">これで、タブが読み込Microsoft Teams!</span><span class="sxs-lookup"><span data-stu-id="3d32e-202">Your tab is now loaded inside Microsoft Teams!</span></span>

   ![teams でタブを実行する](~/assets/yeoman-images/teams-first-app-6.png)

### <a name="upgrade-microsoft-teams"></a><span data-ttu-id="3d32e-204">アップグレード Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3d32e-204">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="3d32e-205">Yeoman ジェネレーターを使用してMicrosoft Teamsバージョンを最新バージョンにアップグレードMicrosoft Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="3d32e-205">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="3d32e-206">**アップグレードするにはMicrosoft Teams**</span><span class="sxs-lookup"><span data-stu-id="3d32e-206">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="3d32e-207">次のコマンドを使用してTeamsのバージョンを取得します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-207">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="3d32e-208">ジェネレーターを選択して更新するには、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-208">Use the following command to select and update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="3d32e-209">矢印キーを使用して [ **ジェネレーターの更新] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3d32e-209">Use the  arrow keys to select **Update your Generators**:</span></span>

   ![YoSelectUpdatGen の画像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="3d32e-211">ジェネレーターの一覧から必要なジェネレーターを選択します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-211">Select the generator you want from the list of generators:</span></span>
   > [!NOTE]
   > <span data-ttu-id="3d32e-212">スペース バーを使用して、使用可能なオプションから選択したTeamsを選択または解除します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-212">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![UseSpaceToSelectGenerators のイメージ](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="3d32e-214">インストールが完了するには、数秒からTeams分かかります。</span><span class="sxs-lookup"><span data-stu-id="3d32e-214">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="3d32e-215">インストールが完了したら、次のコマンドを使用してインストールされているバージョンを確認します。</span><span class="sxs-lookup"><span data-stu-id="3d32e-215">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   <span data-ttu-id="3d32e-216">おめでとう!</span><span class="sxs-lookup"><span data-stu-id="3d32e-216">Congrats!</span></span> <span data-ttu-id="3d32e-217">最初のアプリをビルドしてMicrosoft Teamsしました。</span><span class="sxs-lookup"><span data-stu-id="3d32e-217">You built and deployed your first Microsoft Teams app.</span></span> <span data-ttu-id="3d32e-218">また、アップグレードMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="3d32e-218">You also upgraded Microsoft Teams.</span></span>

 ## <a name="see-also"></a><span data-ttu-id="3d32e-219">関連項目</span><span class="sxs-lookup"><span data-stu-id="3d32e-219">See also</span></span>

* [<span data-ttu-id="3d32e-220">チュートリアルの概要</span><span class="sxs-lookup"><span data-stu-id="3d32e-220">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="3d32e-221">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="3d32e-221">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="3d32e-222">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="3d32e-222">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="3d32e-223">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="3d32e-223">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)