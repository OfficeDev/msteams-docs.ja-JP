---
title: チュートリアル - Yeomanジェネレータを使用して最初のアプリを作成します
description: Yeoman ジェネレータを使用してMicrosoft Teamsアプリの構築を開始する方法について説明します。
keywords: ノードス・ヨーマンnode.js始める
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 96a4f64d487e1d16bf25abd978759fedeac1061c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566825"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="10dec-104">ヨーマンジェネレータを使用して、あなたの最初のMicrosoft Teamsアプリを作成します</span><span class="sxs-lookup"><span data-stu-id="10dec-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="10dec-105">このチュートリアルでは、[ウィキのヨーマンジェネレータTeams提供しています](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。</span><span class="sxs-lookup"><span data-stu-id="10dec-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="10dec-106">このチュートリアルでは、Microsoft Teams Yeoman ジェネレータを使用して、非常に最初のMicrosoft Teamsアプリを作成する手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="10dec-106">In this tutorial, we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="10dec-107">また、Yeoman ジェネレータを使用してTeamsをアップグレードするプロセスについても説明します。</span><span class="sxs-lookup"><span data-stu-id="10dec-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="10dec-108">このチュートリアルで開始する前提条件は、[アプリのサイドローディング](~/concepts/build-and-test/prepare-your-o365-tenant.md)を可能にするTeamsアカウントを持っているということです。</span><span class="sxs-lookup"><span data-stu-id="10dec-108">The prerequisite to start with this tutorial is that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![ヨーマンジェネレータギット](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="10dec-110">マシンのセットアップと準備</span><span class="sxs-lookup"><span data-stu-id="10dec-110">Setup and prepare your machine</span></span>

<span data-ttu-id="10dec-111">Yeoman ジェネレータを使用する前に、次の機器をマシンにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10dec-111">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="10dec-112">Node.js. のインストール</span><span class="sxs-lookup"><span data-stu-id="10dec-112">Install Node.js</span></span>

<span data-ttu-id="10dec-113">マシンにNode.jsをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10dec-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="10dec-114">最新の [LTS バージョン](https://nodejs.org)を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10dec-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="10dec-115">コード エディターのインストール</span><span class="sxs-lookup"><span data-stu-id="10dec-115">Install a code editor</span></span>

<span data-ttu-id="10dec-116">コード エディターが必要です。</span><span class="sxs-lookup"><span data-stu-id="10dec-116">You need a code editor.</span></span> <span data-ttu-id="10dec-117">このドキュメントとイメージのほとんどは、 [Visual Studio Code](https://code.visualstudio.com)を使用して参照しています。</span><span class="sxs-lookup"><span data-stu-id="10dec-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="10dec-118">ただし、好きなテキスト エディタを自由に使用してください。</span><span class="sxs-lookup"><span data-stu-id="10dec-118">However, feel free to use whatever text editor you prefer.</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="10dec-119">ヨーマンとGulp CLIをインストールする</span><span class="sxs-lookup"><span data-stu-id="10dec-119">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="10dec-120">ジェネレータを使用してプロジェクトをスキャフォールディングするには、Yeoman ツールと Gulp CLI タスクマネージャーをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10dec-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

<span data-ttu-id="10dec-121">コマンド プロンプトを開き、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="10dec-121">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="10dec-122">ジェネレーターをインストールする</span><span class="sxs-lookup"><span data-stu-id="10dec-122">Install the generator</span></span>

<span data-ttu-id="10dec-123">次のコマンドで Teams Yeoman ジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="10dec-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="10dec-124">次のコマンドを使用して、ジェネレータのプレビュー バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="10dec-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="10dec-125">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="10dec-125">Generate your project</span></span>

<span data-ttu-id="10dec-126">このセクションでは、プロジェクトを生成する手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="10dec-126">This section walks you through the steps for generating your project.</span></span>

<span data-ttu-id="10dec-127">**プロジェクトを生成するには**</span><span class="sxs-lookup"><span data-stu-id="10dec-127">**To generate your project**</span></span>

1. <span data-ttu-id="10dec-128">コマンド プロンプトを開き、プロジェクトを作成するディレクトリを新しく作成し、そのディレクトリでコマンドを実行 `yo teams` します。</span><span class="sxs-lookup"><span data-stu-id="10dec-128">Open up a command prompt and create a new directory where you want to create your project, and in that directory run the command `yo teams`.</span></span> <span data-ttu-id="10dec-129">ジェネレータが起動します。</span><span class="sxs-lookup"><span data-stu-id="10dec-129">The generator starts.</span></span>
1. <span data-ttu-id="10dec-130">ジェネレータによって促される一連の質問に答えます。</span><span class="sxs-lookup"><span data-stu-id="10dec-130">Respond to the set of questions prompted by the generator:</span></span>

   ![ヨーチーム](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="10dec-132">最初の質問は、プロジェクト名についてです、あなたはEnterキーを押すことによって、そのままにしておくことができます。</span><span class="sxs-lookup"><span data-stu-id="10dec-132">The first question is about your project name, you can leave it as is by pressing enter.</span></span>
   1. <span data-ttu-id="10dec-133">次の質問では、新しいディレクトリを作成するか、現在のディレクトリを使用するかを尋ねます。</span><span class="sxs-lookup"><span data-stu-id="10dec-133">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="10dec-134">あなたが望むディレクトリにすでにあるので、単にEnterキーを押してください。</span><span class="sxs-lookup"><span data-stu-id="10dec-134">As you are already in the directory you want, just press enter.</span></span>
   1. <span data-ttu-id="10dec-135">次の質問で、プロジェクトのタイトルを入力します。</span><span class="sxs-lookup"><span data-stu-id="10dec-135">In the next question, type the title of your project.</span></span> <span data-ttu-id="10dec-136">このタイトルは、アプリのマニフェストと説明で使用されます。</span><span class="sxs-lookup"><span data-stu-id="10dec-136">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="10dec-137">次に、マニフェストでも使用される会社名を尋ねられます。</span><span class="sxs-lookup"><span data-stu-id="10dec-137">Next, you will be asked for a company name, which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="10dec-138">5 番目の質問では、使用するマニフェストのバージョンについて尋ねられています。</span><span class="sxs-lookup"><span data-stu-id="10dec-138">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="10dec-139">このチュートリアルでは、 `v1.5` 現在使用可能な一般的なスキーマである を選択します。</span><span class="sxs-lookup"><span data-stu-id="10dec-139">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="10dec-140">次に、ジェネレータは、プロジェクトに追加する項目を尋ねます。</span><span class="sxs-lookup"><span data-stu-id="10dec-140">Next, the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="10dec-141">1 つまたは任意の組み合わせの項目を選択できます。</span><span class="sxs-lookup"><span data-stu-id="10dec-141">You can select a single one or any combination of items.</span></span> <span data-ttu-id="10dec-142">このチュートリアルでは、 *タブを* 選択するだけです:</span><span class="sxs-lookup"><span data-stu-id="10dec-142">For this tutorials, just select *a Tab*:</span></span>

    ![品目の選択](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="10dec-144">手順 2 で選択した項目に基づいて表示される、次のフォローアップの質問に回答します。</span><span class="sxs-lookup"><span data-stu-id="10dec-144">Respond to the next set of follow-up questions that appear based on the items you selected in step 2.</span></span>
1. <span data-ttu-id="10dec-145">ソリューションをホストする URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="10dec-145">Enter a URL of where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="10dec-146">URL は任意の URL にすることができますが、既定では、ジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="10dec-146">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="10dec-147">次の質問では、ソリューションの単体テストを含めるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="10dec-147">In the next question, confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="10dec-148">デフォルトの応答は *yes* です。</span><span class="sxs-lookup"><span data-stu-id="10dec-148">The default response is *yes*.</span></span> <span data-ttu-id="10dec-149">単体テストを含める場合、生成されたプロジェクトには、スキャフォールディングされるさまざまな項目に対して単体テスト フレームワークと既定の単体テストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="10dec-149">If you choose to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="10dec-150">このチュートリアルでは、テスト フレームワークを含めないように選択します。</span><span class="sxs-lookup"><span data-stu-id="10dec-150">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="10dec-151">ジェネレーターには、オプトインまたはオプトアウトできる多くの拡張機能が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="10dec-151">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="10dec-152">サインインを簡単にするために、サインインに Azure アプリケーション インサイトを使用するかどうかも確認されます。</span><span class="sxs-lookup"><span data-stu-id="10dec-152">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="10dec-153">*[はい*] を選択した場合は、Azure アプリケーションの洞察キーを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10dec-153">If you choose *Yes*, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="10dec-154">このチュートリアルでは、アプリケーションインサイトの使用をオプトアウトします。</span><span class="sxs-lookup"><span data-stu-id="10dec-154">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="10dec-155">次の質問セットは、以前に選択した項目に基づいて行われます。</span><span class="sxs-lookup"><span data-stu-id="10dec-155">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="10dec-156">タブの場合は、名前を指定するだけで、必要に応じてこのアプリをSharePointオンライン Web パーツとして使用できるようにする場合に選択します。</span><span class="sxs-lookup"><span data-stu-id="10dec-156">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="10dec-157">名前を指定すると、ジェネレータはプロジェクトを生成し、すべての依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="10dec-157">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="10dec-158">これには1、2分かかります。</span><span class="sxs-lookup"><span data-stu-id="10dec-158">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="10dec-159">タブにコードを追加する</span><span class="sxs-lookup"><span data-stu-id="10dec-159">Add some code to your tab</span></span>

<span data-ttu-id="10dec-160">ジェネレーターが完了したら、お気に入りのコード エディターでソリューションを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="10dec-160">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="10dec-161">1、2 分かかると、コードの構成方法に慣れ親しみます。</span><span class="sxs-lookup"><span data-stu-id="10dec-161">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="10dec-162">詳細については、構造体のドキュメント[Project](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)参照してください。</span><span class="sxs-lookup"><span data-stu-id="10dec-162">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="10dec-163">タブがファイル内にあります `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` 。</span><span class="sxs-lookup"><span data-stu-id="10dec-163">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="10dec-164">これは、タブの TypeScript React ベースのクラスです。メソッドを見つけて `render()` 、次のようにコントロール内にコード行 `<PanelBody>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="10dec-164">This is the TypeScript React-based class for your tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="10dec-165">ファイルを保存し、コマンド プロンプトに戻ります。</span><span class="sxs-lookup"><span data-stu-id="10dec-165">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="10dec-166">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="10dec-166">Build your app</span></span>

<span data-ttu-id="10dec-167">これで、プロジェクトをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="10dec-167">You can now build your project.</span></span> <span data-ttu-id="10dec-168">これは 2 つのステップ (または 1 つのステップ、 以下を参照) で行われます。</span><span class="sxs-lookup"><span data-stu-id="10dec-168">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="10dec-169">まず、アップロード/サイドロードをMicrosoft TeamsするTeamsアプリマニフェストファイルを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10dec-169">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="10dec-170">これは Gulp タスクによって行われます `gulp manifest` 。</span><span class="sxs-lookup"><span data-stu-id="10dec-170">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="10dec-171">これにより、マニフェストが検証され、ディレクトリに zip ファイルが作成 `./package` されます。</span><span class="sxs-lookup"><span data-stu-id="10dec-171">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="10dec-172">ソリューションをビルドするには、コマンドを使用 `gulp build` します。</span><span class="sxs-lookup"><span data-stu-id="10dec-172">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="10dec-173">これにより、ソリューションがフォルダに入 `./dist` り込みます。</span><span class="sxs-lookup"><span data-stu-id="10dec-173">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="10dec-174">アプリの実行</span><span class="sxs-lookup"><span data-stu-id="10dec-174">Run your app</span></span>

<span data-ttu-id="10dec-175">アプリを実行するには、コマンドを使用 `gulp serve` します。</span><span class="sxs-lookup"><span data-stu-id="10dec-175">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="10dec-176">これにより、アプリをテストするためのローカル Web サーバーが構築され、起動されます。</span><span class="sxs-lookup"><span data-stu-id="10dec-176">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="10dec-177">このコマンドは、プロジェクトにファイルを保存するたびにアプリケーションを再構築します。</span><span class="sxs-lookup"><span data-stu-id="10dec-177">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="10dec-178">`http://localhost:3007/myFirstAppTab/`これで、タブがレンダリングされていることを確認するために参照できるようになります。</span><span class="sxs-lookup"><span data-stu-id="10dec-178">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="10dec-179">しかし、まだMicrosoft Teamsではありません:</span><span class="sxs-lookup"><span data-stu-id="10dec-179">However, not in Microsoft Teams yet:</span></span>

![ブラウザでサイトを表示する](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="10dec-181">Microsoft Teamsでアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="10dec-181">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="10dec-182">Microsoft Teamsでは、アプリを localhost でホストすることはできませんので、パブリック URL に発行するか、ngrok などのプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10dec-182">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="10dec-183">良いニュースは、足場のプロジェクトにはこの組み込みがあるということです。</span><span class="sxs-lookup"><span data-stu-id="10dec-183">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="10dec-184">`gulp ngrok-serve`ngrok サービスを実行すると、一意のパブリック DNS エントリを使用してバックグラウンドで開始され、その一意の URL を持つマニフェストもパッケージ化され、 とまったく同じ処理が行われます `gulp serve` 。</span><span class="sxs-lookup"><span data-stu-id="10dec-184">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="10dec-185">を実行した後 `gulp ngrok-serve` 、新しいMicrosoft Teamsチームを作成し、作成したら [チーム名] をクリックしてチームの設定に移動し、[*アプリ*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="10dec-185">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="10dec-186">右下隅に *カスタム アプリアップロード* リンクが表示されます `package` 。</span><span class="sxs-lookup"><span data-stu-id="10dec-186">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="10dec-187">そのフォルダの zip ファイルを選択し、[開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="10dec-187">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="10dec-188">アプリがMicrosoft Teamsにサイドロードされました。</span><span class="sxs-lookup"><span data-stu-id="10dec-188">Your App is now sideloaded into Microsoft Teams:</span></span>

![サイドロードアプリ](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="10dec-190">*[全般*] チャネルに戻り、 *+* 新しいタブを追加します。タブのリストにタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="10dec-190">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs:</span></span>

![[構成] タブ](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="10dec-192">タブを選択し、指示に従って追加します。</span><span class="sxs-lookup"><span data-stu-id="10dec-192">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="10dec-193">カスタム構成ダイアログがあり、ソースを編集できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="10dec-193">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="10dec-194">[ *保存]* を選択して、チャンネルにタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="10dec-194">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="10dec-195">一度あなたのタブは、Microsoft Teamsの中にロードする必要があります!</span><span class="sxs-lookup"><span data-stu-id="10dec-195">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![チーム内での実行中のタブ](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a><span data-ttu-id="10dec-197">Microsoft Teamsのアップグレード</span><span class="sxs-lookup"><span data-stu-id="10dec-197">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="10dec-198">また、Microsoft TeamsのYeomanジェネレータを使用して、現在のMicrosoft Teamsバージョンを最新バージョンにアップグレードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="10dec-198">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="10dec-199">**Microsoft Teamsをアップグレードするには**</span><span class="sxs-lookup"><span data-stu-id="10dec-199">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="10dec-200">次のコマンドを使用して、Teamsの現在のバージョンを取得します。</span><span class="sxs-lookup"><span data-stu-id="10dec-200">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="10dec-201">次のコマンドを使用して、ジェネレータの更新を選択します。</span><span class="sxs-lookup"><span data-stu-id="10dec-201">Use the following command to select update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="10dec-202">矢印キーを使用して **、[ジェネレータを更新] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="10dec-202">Use the  arrow keys to choose **Update your Generators**:</span></span>

   ![ヨセレクトアップダットゲンの画像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="10dec-204">ジェネレータのリストから、必要なジェネレータを選択します。</span><span class="sxs-lookup"><span data-stu-id="10dec-204">Select the generator you want from the list of generators:</span></span>
   > [!NOTE]
   > <span data-ttu-id="10dec-205">スペースバーを使用して、選択したTeamsバージョンを選択または選択解除します。</span><span class="sxs-lookup"><span data-stu-id="10dec-205">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![使用スペースのイメージを選択するジェネレータ](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="10dec-207">インストールが完了するまで数秒から数分Teamsかかります。</span><span class="sxs-lookup"><span data-stu-id="10dec-207">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="10dec-208">インストールが完了したら、次のコマンドを使用してインストール済みバージョンを確認します。</span><span class="sxs-lookup"><span data-stu-id="10dec-208">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   
<span data-ttu-id="10dec-209">**おめでとう！最初のMicrosoft Teams アプリを構築して展開しました。Microsoft Teamsもアップグレードしました。**</span><span class="sxs-lookup"><span data-stu-id="10dec-209">**Congrats! You built and deployed your first Microsoft Teams app. You also upgraded Microsoft Teams.**</span></span>
