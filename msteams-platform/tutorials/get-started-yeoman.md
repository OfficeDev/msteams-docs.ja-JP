---
title: チュートリアル - Yeoman ジェネレーターを使用して最初のアプリを作成する
description: Yeoman ジェネレーターを使用してアプリMicrosoft Teamsを開始する方法について学習します。
keywords: nodejs yeoman node.jsを開始する
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 9efbe6f6e6502120f1afdadb9b538182f1406c56
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018433"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="f9c44-104">Yeoman ジェネレーターをMicrosoft Teams最初のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="f9c44-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="f9c44-105">このチュートリアルは、Wiki の[Yeoman ジェネレーター Teamsです](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。</span><span class="sxs-lookup"><span data-stu-id="f9c44-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="f9c44-106">このチュートリアルでは、Yeoman ジェネレーターを使用して、Microsoft TeamsアプリMicrosoft Teams説明します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-106">In this tutorial, we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="f9c44-107">また、Yeoman ジェネレーターを使用してアプリケーションをアップグレードTeams手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="f9c44-108">このチュートリアルから始める前提条件は、アプリのサイドローディングをTeamsアカウント[を持っているという前提です](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="f9c44-108">The prerequisite to start with this tutorial is that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![yeoman ジェネレーター git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="f9c44-110">コンピューターのセットアップと準備</span><span class="sxs-lookup"><span data-stu-id="f9c44-110">Setup and prepare your machine</span></span>

<span data-ttu-id="f9c44-111">Yeoman ジェネレーターの使用を開始する前に、コンピューターに以下をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-111">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="f9c44-112">Node.js. のインストール</span><span class="sxs-lookup"><span data-stu-id="f9c44-112">Install Node.js</span></span>

<span data-ttu-id="f9c44-113">コンピューターにインストールNode.js必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="f9c44-114">最新の [LTS バージョンを使用する必要があります](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="f9c44-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="f9c44-115">コード エディターのインストール</span><span class="sxs-lookup"><span data-stu-id="f9c44-115">Install a code editor</span></span>

<span data-ttu-id="f9c44-116">コード エディターが必要です。</span><span class="sxs-lookup"><span data-stu-id="f9c44-116">You need a code editor.</span></span> <span data-ttu-id="f9c44-117">このドキュメントと画像の大部分は、このドキュメントを使用[Visual Studio Code。](https://code.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="f9c44-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="f9c44-118">ただし、必要なテキスト エディターを自由に使用できます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-118">However, feel free to use whatever text editor you prefer.</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="f9c44-119">Yeoman と Gulp CLI をインストールする</span><span class="sxs-lookup"><span data-stu-id="f9c44-119">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="f9c44-120">ジェネレーターを使用してプロジェクトをスキャフォールディングするには、Yeoman ツールと Gulp CLI タスク マネージャーをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

<span data-ttu-id="f9c44-121">コマンド プロンプトを開き、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-121">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="f9c44-122">ジェネレーターのインストール</span><span class="sxs-lookup"><span data-stu-id="f9c44-122">Install the generator</span></span>

<span data-ttu-id="f9c44-123">次のコマンドTeams Yeoman ジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f9c44-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="f9c44-124">次のコマンドを使用して、ジェネレーターのプレビュー バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f9c44-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="f9c44-125">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="f9c44-125">Generate your project</span></span>

<span data-ttu-id="f9c44-126">このセクションでは、プロジェクトを生成する手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-126">This section walks you through the steps for generating your project.</span></span>

<span data-ttu-id="f9c44-127">**プロジェクトを生成するには**</span><span class="sxs-lookup"><span data-stu-id="f9c44-127">**To generate your project**</span></span>

1. <span data-ttu-id="f9c44-128">コマンド プロンプトを開き、プロジェクトを作成する新しいディレクトリを作成し、そのディレクトリでコマンドを実行します `yo teams` 。</span><span class="sxs-lookup"><span data-stu-id="f9c44-128">Open up a command prompt and create a new directory where you want to create your project, and in that directory run the command `yo teams`.</span></span> <span data-ttu-id="f9c44-129">ジェネレーターが起動します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-129">The generator starts.</span></span>
1. <span data-ttu-id="f9c44-130">ジェネレーターから求める一連の質問に応答します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-130">Respond to the set of questions prompted by the generator.</span></span>

   ![yo チーム](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="f9c44-132">最初の質問はプロジェクト名に関する質問で、Enter キーを押すことでそのままにできます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-132">The first question is about your project name, you can leave it as is by pressing enter.</span></span>
   1. <span data-ttu-id="f9c44-133">次の質問では、新しいディレクトリを作成するか、現在のディレクトリを使用するかが問い合されます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-133">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="f9c44-134">必要なディレクトリに既に存在する場合は、Enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-134">As you are already in the directory you want, just press enter.</span></span>
   1. <span data-ttu-id="f9c44-135">次の質問で、プロジェクトのタイトルを入力します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-135">In the next question, type the title of your project.</span></span> <span data-ttu-id="f9c44-136">このタイトルは、アプリのマニフェストと説明で使用されます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-136">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="f9c44-137">次に、マニフェストでも使用される会社名を求める質問が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-137">Next, you will be asked for a company name, which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="f9c44-138">5 番目の質問では、使用するマニフェストのバージョンについて質問されます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-138">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="f9c44-139">このチュートリアルでは、 `v1.5` 現在利用可能な一般的なスキーマを選択します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-139">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="f9c44-140">次に、ジェネレーターは、プロジェクトに追加するアイテムを確認します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-140">Next, the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="f9c44-141">アイテムの 1 つまたは任意の組み合わせを選択できます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-141">You can select a single one or any combination of items.</span></span> <span data-ttu-id="f9c44-142">このチュートリアルでは、[タブ] *を選択します*。</span><span class="sxs-lookup"><span data-stu-id="f9c44-142">For this tutorials, just select *a Tab*.</span></span>

    ![アイテムの選択](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="f9c44-144">手順 2 で選択したアイテムに基づいて表示される次のフォローアップ質問のセットに応答します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-144">Respond to the next set of follow-up questions that appear based on the items you selected in step 2.</span></span>
1. <span data-ttu-id="f9c44-145">ソリューションをホストする場所の URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-145">Enter a URL of where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="f9c44-146">URL には任意の URL を指定できますが、既定ではジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-146">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="f9c44-147">次の質問で、ソリューションに単体テストを含める必要がある場合に確認します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-147">In the next question, confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="f9c44-148">既定の応答は yes *です*。</span><span class="sxs-lookup"><span data-stu-id="f9c44-148">The default response is *yes*.</span></span> <span data-ttu-id="f9c44-149">単体テストを含める場合、生成されたプロジェクトには単体テスト フレームワークと、スキャフォールディングされるさまざまなアイテムに対する既定の単体テストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-149">If you choose to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="f9c44-150">このチュートリアルでは、テスト フレームワークを含めないを選択します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-150">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="f9c44-151">ジェネレーターには、オプトインまたはオプトアウトできる多くの組み込みの高度な機能があります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-151">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="f9c44-152">サインインを簡単に行う場合は、サインインに Azure Application Insights を使用する必要がある場合も尋ねられるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-152">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="f9c44-153">[はい] *を選択* した場合は、Azure Application Insights キーを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-153">If you choose *Yes*, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="f9c44-154">このチュートリアルでは、Application Insights の使用をオプトアウトします。</span><span class="sxs-lookup"><span data-stu-id="f9c44-154">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="f9c44-155">次の質問のセットは、以前に選択したアイテムに基づいて行います。</span><span class="sxs-lookup"><span data-stu-id="f9c44-155">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="f9c44-156">タブの場合は、名前を指定し、必要に応じて、このアプリをオンライン Web パーツとして使用SharePoint選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-156">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="f9c44-157">名前を指定すると、ジェネレーターはプロジェクトを生成し、すべての依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="f9c44-157">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="f9c44-158">これには 1 分または 2 分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-158">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="f9c44-159">タブにコードを追加する</span><span class="sxs-lookup"><span data-stu-id="f9c44-159">Add some code to your tab</span></span>

<span data-ttu-id="f9c44-160">ジェネレーターが完了したら、お気に入りのコード エディターでソリューションを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-160">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="f9c44-161">1 分か 2 分で、コードの整理方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-161">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="f9c44-162">詳細については、「構造」[のドキュメントProject参照](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)してください。</span><span class="sxs-lookup"><span data-stu-id="f9c44-162">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="f9c44-163">タブがファイル内 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` にあります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-163">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="f9c44-164">これは、タブの typeScript Reactベースのクラスです。メソッドを `render()` 見つけて、コントロール内にコード行を追加して `<PanelBody>` 、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="f9c44-164">This is the TypeScript React-based class for your tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="f9c44-165">ファイルを保存し、コマンド プロンプトに戻します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-165">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="f9c44-166">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="f9c44-166">Build your app</span></span>

<span data-ttu-id="f9c44-167">これで、プロジェクトをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-167">You can now build your project.</span></span> <span data-ttu-id="f9c44-168">これは、2 つの手順 (または 1 つの手順を参照) で行います。</span><span class="sxs-lookup"><span data-stu-id="f9c44-168">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="f9c44-169">まず、アプリ マニフェスト ファイルをTeams、アプリ マニフェスト ファイルにアップロードまたはサイドロードする必要Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="f9c44-169">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="f9c44-170">これは Gulp タスクによって実行されます `gulp manifest` 。</span><span class="sxs-lookup"><span data-stu-id="f9c44-170">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="f9c44-171">これにより、マニフェストが検証され、ディレクトリに zip ファイルが作成 `./package` されます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-171">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="f9c44-172">ソリューションをビルドするには、コマンドを使用 `gulp build` します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-172">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="f9c44-173">これにより、ソリューションがフォルダーに変換 `./dist` されます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-173">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="f9c44-174">アプリの実行</span><span class="sxs-lookup"><span data-stu-id="f9c44-174">Run your app</span></span>

<span data-ttu-id="f9c44-175">アプリを実行するには、コマンドを使用 `gulp serve` します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-175">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="f9c44-176">これにより、アプリをテストするためのローカル Web サーバーが構築され、開始されます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-176">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="f9c44-177">また、プロジェクトにファイルを保存するたびに、このコマンドはアプリケーションを再構築します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-177">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="f9c44-178">これで、タブがレンダリングされる `http://localhost:3007/myFirstAppTab/` のを確認するために参照できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-178">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="f9c44-179">ただし、まだMicrosoft Teamsはありません。</span><span class="sxs-lookup"><span data-stu-id="f9c44-179">However, not in Microsoft Teams yet.</span></span>

![ブラウザーでサイトを表示する](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="f9c44-181">アプリをアプリで実行Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f9c44-181">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="f9c44-182">Microsoft Teamsアプリを localhost でホストすることはできませんので、パブリック URL に公開するか、ngrok などのプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-182">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="f9c44-183">良いニュースは、スキャフォールディングされたプロジェクトにこの組み込みがあります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-183">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="f9c44-184">ngrok サービスを実行すると、一意のパブリック DNS エントリを使用してバックグラウンドで開始され、その一意の URL でマニフェストがパッケージ化され、その後とまったく同じ処理を実行 `gulp ngrok-serve` します `gulp serve` 。</span><span class="sxs-lookup"><span data-stu-id="f9c44-184">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="f9c44-185">実行後、新しいチームMicrosoft Teams作成し、チーム名をクリックしてチームの設定に移動し、[アプリ] `gulp ngrok-serve` を *選択します*。</span><span class="sxs-lookup"><span data-stu-id="f9c44-185">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="f9c44-186">右下にカスタム アプリのリンクが表示アップロード選択し、プロジェクト フォルダーとというサブフォルダーを参照します `package` 。</span><span class="sxs-lookup"><span data-stu-id="f9c44-186">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="f9c44-187">そのフォルダー内の zip ファイルを選択し、[開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-187">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="f9c44-188">これで、アプリはアプリにサイドロードMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="f9c44-188">Your App is now sideloaded into Microsoft Teams.</span></span>

![サイドロードされたアプリ](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="f9c44-190">[全般] チャネルに *戻り* 、新 *+* しいタブを追加します。タブの一覧にタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-190">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![[構成] タブ](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="f9c44-192">タブを選択し、指示に従って追加します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-192">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="f9c44-193">カスタム構成ダイアログが表示され、ソースを編集できます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-193">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="f9c44-194">[保存 *] を* 選択して、タブをチャネルに追加します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-194">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="f9c44-195">完了したら、タブを内部に読み込Microsoft Teams!</span><span class="sxs-lookup"><span data-stu-id="f9c44-195">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![teams でタブを実行する](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a><span data-ttu-id="f9c44-197">アップグレード Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f9c44-197">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="f9c44-198">Yeoman ジェネレーターを使用してMicrosoft Teamsバージョンを最新バージョンにアップグレードMicrosoft Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="f9c44-198">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="f9c44-199">**アップグレードするにはMicrosoft Teams**</span><span class="sxs-lookup"><span data-stu-id="f9c44-199">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="f9c44-200">次のコマンドを使用してTeamsのバージョンを取得します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-200">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="f9c44-201">次のコマンドを使用して、ジェネレーターの更新を選択します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-201">Use the following command to select update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="f9c44-202">矢印キーを使用して [ **ジェネレーターの更新] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f9c44-202">Use the  arrow keys to choose **Update your Generators**.</span></span>

   ![YoSelectUpdatGen の画像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="f9c44-204">ジェネレーターの一覧から目的のジェネレーターを選択します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-204">Select the generator you want from the list of generators.</span></span>
   > [!NOTE]
   > <span data-ttu-id="f9c44-205">スペース バーを使用して、使用可能なオプションから選択したTeamsを選択または解除します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-205">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![UseSpaceToSelectGenerators のイメージ](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="f9c44-207">インストールが完了するには、数秒からTeams分かかります。</span><span class="sxs-lookup"><span data-stu-id="f9c44-207">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="f9c44-208">インストールが完了したら、次のコマンドを使用してインストールされているバージョンを確認します。</span><span class="sxs-lookup"><span data-stu-id="f9c44-208">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   
<span data-ttu-id="f9c44-209">**おめでとう!最初のアプリをビルドしてMicrosoft Teamsしました。また、アップグレードMicrosoft Teams。**</span><span class="sxs-lookup"><span data-stu-id="f9c44-209">**Congrats! You built and deployed your first Microsoft Teams app. You also upgraded Microsoft Teams.**</span></span>
