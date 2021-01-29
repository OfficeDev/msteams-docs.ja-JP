---
title: チュートリアル - Yeoman ジェネレーターを使用して最初のアプリを作成する
description: Yeoman ジェネレーターを使用して Microsoft Teams アプリの構築を開始する方法について説明します。
keywords: nodejs yeoman node.jsの開始
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f7f0fb3ba1be28dfa7d343be3af9d122b4ad090d
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037005"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="6e530-104">Yeoman ジェネレーターを使用して最初の Microsoft Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="6e530-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

>[!Note]
><span data-ttu-id="6e530-105">このチュートリアルは [、Teams Wiki 用の Yeoman ジェネレーターから提供されます](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。</span><span class="sxs-lookup"><span data-stu-id="6e530-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="6e530-106">このチュートリアルでは、Microsoft Teams Yeoman ジェネレーターを使用して最初の Microsoft Teams アプリを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6e530-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="6e530-107">アプリのサイドローディングを許可する Teams アカウント [を持っている必要があります](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="6e530-107">It assumes that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![yeoman ジェネレーター git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="6e530-109">コンピューターのセットアップと準備</span><span class="sxs-lookup"><span data-stu-id="6e530-109">Setup and prepare your machine</span></span>

<span data-ttu-id="6e530-110">Yeoman ジェネレーターの使用を開始する前に、コンピューターに以下をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-110">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="6e530-111">Node.js. のインストール</span><span class="sxs-lookup"><span data-stu-id="6e530-111">Install Node.js</span></span>

<span data-ttu-id="6e530-112">コンピューターにインストールNode.js必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-112">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="6e530-113">最新の [LTS バージョンを使用する必要があります](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="6e530-113">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="6e530-114">コード エディターのインストール</span><span class="sxs-lookup"><span data-stu-id="6e530-114">Install a code editor</span></span>

<span data-ttu-id="6e530-115">コード エディターも必要です。好きなテキスト エディターを自由に使用できます。</span><span class="sxs-lookup"><span data-stu-id="6e530-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="6e530-116">ただし、このドキュメントとスクリーンショットの大部分は、コードのVisual Studio [しています](https://code.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="6e530-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="6e530-117">Yeoman と Gulp CLI をインストールする</span><span class="sxs-lookup"><span data-stu-id="6e530-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="6e530-118">Teams ジェネレーターを使用してプロジェクトをスキャフォールディングするには、Yeoman ツールと Gulp CLI タスク マネージャーをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="6e530-119">コマンド プロンプトを開き、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="6e530-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="6e530-120">ジェネレーターをインストールする</span><span class="sxs-lookup"><span data-stu-id="6e530-120">Install the generator</span></span>

<span data-ttu-id="6e530-121">次のコマンドを使用して、Teams Yeoman ジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="6e530-121">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="6e530-122">ジェネレーターのプレビュー バージョンをインストールするには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="6e530-122">To install preview versions of the generator, run this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="6e530-123">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="6e530-123">Generate your project</span></span>

<span data-ttu-id="6e530-124">コマンド プロンプトを開き、プロジェクトを作成する新しいディレクトリを作成し、そのディレクトリでコマンドを実行します `yo teams` 。</span><span class="sxs-lookup"><span data-stu-id="6e530-124">Open up a command prompt and create a new directory where you want to create your project and in that directory run the command `yo teams`.</span></span>

<span data-ttu-id="6e530-125">これによりジェネレーターが起動し、一連の質問を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-125">This starts the generator, which prompts you with a set of questions.</span></span>

![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="6e530-127">最初の質問はプロジェクト名に関する質問です。Enter キーを押すとそのまま残しておきます。</span><span class="sxs-lookup"><span data-stu-id="6e530-127">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="6e530-128">次の質問では、新しいディレクトリを作成するか、現在のディレクトリを使用するかが問い合されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-128">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="6e530-129">必要なディレクトリに既に存在する場合は、Enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="6e530-129">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="6e530-130">次の手順では、プロジェクトのタイトルを求めるメッセージが表示されます。このタイトルは、アプリのマニフェストと説明で使用されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-130">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="6e530-131">次に、会社名を入力する必要があります。この名前はマニフェストでも使用されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-131">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="6e530-132">5 番目の質問では、使用するマニフェストのバージョンについて確認します。</span><span class="sxs-lookup"><span data-stu-id="6e530-132">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="6e530-133">このチュートリアルでは、現在 `v1.5` 一般に使用可能なスキーマを選択します。</span><span class="sxs-lookup"><span data-stu-id="6e530-133">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="6e530-134">この後、ジェネレーターはプロジェクトに追加するアイテムを求めるダイアログを表示します。</span><span class="sxs-lookup"><span data-stu-id="6e530-134">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="6e530-135">1 つのアイテムまたはアイテムの任意の組み合わせを選択できます。</span><span class="sxs-lookup"><span data-stu-id="6e530-135">You can select a single one or any combination of items.</span></span> <span data-ttu-id="6e530-136">For now, just select *a Tab*.</span><span class="sxs-lookup"><span data-stu-id="6e530-136">For now, just select *a Tab*.</span></span>

![項目の選択](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="6e530-138">選択した項目に基づいて、一連のフォローアップ質問が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-138">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="6e530-139">次に、ソリューションをホストする場所の URL を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-139">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="6e530-140">任意の URL を使用できますが、既定ではジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="6e530-140">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="6e530-141">ジェネレーターには、オプトインまたはオプトアウトできる多くの組み込みの高度な機能があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-141">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="6e530-142">ソリューションに単体テストを含める場合は、URL に関する質問に従って、既定値は yes です。</span><span class="sxs-lookup"><span data-stu-id="6e530-142">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="6e530-143">これを選択すると、生成されたプロジェクトには単体テスト フレームワークと、スキャフォールディングされるさまざまなアイテムに対する既定の単体テストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="6e530-143">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="6e530-144">このチュートリアルでは、テスト フレームワークを含めない選択をします。</span><span class="sxs-lookup"><span data-stu-id="6e530-144">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="6e530-145">ログを簡単に作成するために、ログに Azure Application Insights を使用する必要がある場合も尋ねられる必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-145">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="6e530-146">[はい] を選択した場合は、Azure Application Insights キーを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-146">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="6e530-147">このチュートリアルでは、Application Insights の使用をオプトアウトします。</span><span class="sxs-lookup"><span data-stu-id="6e530-147">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="6e530-148">次の質問のセットは、以前に選択した項目に基づいて行います。</span><span class="sxs-lookup"><span data-stu-id="6e530-148">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="6e530-149">タブの場合は、名前を指定し、必要に応じて、このアプリを SharePoint Online Web パーツとして使用する場合に選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-149">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="6e530-150">この名前を指定すると、ジェネレーターはプロジェクトを生成し、すべての依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="6e530-150">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="6e530-151">これには 1 分から 2 分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-151">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="6e530-152">タブにコードを追加する</span><span class="sxs-lookup"><span data-stu-id="6e530-152">Add some code to your tab</span></span>

<span data-ttu-id="6e530-153">ジェネレーターが完了したら、お気に入りのコード エディターでソリューションを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="6e530-153">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="6e530-154">少し時間を取って、コードの編成方法を理解してください。詳細については、「プロジェクト構造」のドキュメントを [参照](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) してください。</span><span class="sxs-lookup"><span data-stu-id="6e530-154">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="6e530-155">Tab キーはファイルに保存 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-155">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="6e530-156">これは、Tab の TypeScript React ベースのクラスです。次のように、メソッドを見つけて、コントロール内にコード行 `render()` `<PanelBody>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="6e530-156">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="6e530-157">ファイルを保存し、コマンド プロンプトに戻る。</span><span class="sxs-lookup"><span data-stu-id="6e530-157">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="6e530-158">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="6e530-158">Build your app</span></span>

<span data-ttu-id="6e530-159">これで、プロジェクトをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="6e530-159">You can now build your project.</span></span> <span data-ttu-id="6e530-160">これは、2 つの手順 (または 1 つの手順、以下を参照) で行います。</span><span class="sxs-lookup"><span data-stu-id="6e530-160">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="6e530-161">まず、Microsoft Teams にアップロードまたはサイドロードする Teams アプリ マニフェスト ファイルを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-161">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="6e530-162">これは、Gulp タスクによって行われます `gulp manifest` 。</span><span class="sxs-lookup"><span data-stu-id="6e530-162">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="6e530-163">これにより、マニフェストが検証され、ディレクトリに zip ファイルが作成 `./package` されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-163">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="6e530-164">ソリューションをビルドするには、コマンドを使用 `gulp build` します。</span><span class="sxs-lookup"><span data-stu-id="6e530-164">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="6e530-165">これにより、ソリューションがフォルダーにトランスピタイル `./dist` されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-165">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="6e530-166">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="6e530-166">Run your app</span></span>

<span data-ttu-id="6e530-167">アプリを実行するには、コマンドを使用 `gulp serve` します。</span><span class="sxs-lookup"><span data-stu-id="6e530-167">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="6e530-168">これにより、アプリをテストするためのローカル Web サーバーが構築され、開始されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-168">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="6e530-169">また、プロジェクトにファイルを保存するたびに、このコマンドによってアプリケーションが再構築されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-169">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="6e530-170">これで、タブが表示されているの `http://localhost:3007/myFirstAppTab/` を確認するために参照できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-170">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="6e530-171">ただし、Microsoft Teams にはまだありません。</span><span class="sxs-lookup"><span data-stu-id="6e530-171">However, not in Microsoft Teams yet.</span></span>

![ブラウザーでサイトを表示する](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="6e530-173">Microsoft Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="6e530-173">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="6e530-174">Microsoft Teams では、アプリを localhost でホストすることはできません。そのため、アプリをパブリック URL に公開するか、ngrok などのプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e530-174">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="6e530-175">良いニュースは、スキャフォールディングされたプロジェクトにこの組み込みがあります。</span><span class="sxs-lookup"><span data-stu-id="6e530-175">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="6e530-176">ngrok サービスを実行すると、一意のパブリック DNS エントリを使用してバックグラウンドで開始され、その一意の URL でマニフェストがパッケージ化され、同じことを実行 `gulp ngrok-serve` します `gulp serve` 。</span><span class="sxs-lookup"><span data-stu-id="6e530-176">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="6e530-177">After `gulp ngrok-serve` running, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span><span class="sxs-lookup"><span data-stu-id="6e530-177">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="6e530-178">右下隅に[カスタム アプリをアップロードする] リンクが表示されます。それを選択して、プロジェクト フォルダーと呼ばれるサブフォルダーを参照します `package` 。</span><span class="sxs-lookup"><span data-stu-id="6e530-178">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="6e530-179">そのフォルダー内の zip ファイルを選択し、[開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6e530-179">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="6e530-180">これで、アプリは Microsoft Teams にサイドローディングされます。</span><span class="sxs-lookup"><span data-stu-id="6e530-180">Your App is now sideloaded into Microsoft Teams.</span></span>

![サイドローディングされたアプリ](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="6e530-182">[全般] チャネル *に戻* り、選択して *+* 新しいタブを追加します。タブの一覧にタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6e530-182">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![タブを構成する](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="6e530-184">タブを選択し、指示に従って追加します。</span><span class="sxs-lookup"><span data-stu-id="6e530-184">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="6e530-185">ソースを編集できるカスタム構成ダイアログがあります。</span><span class="sxs-lookup"><span data-stu-id="6e530-185">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="6e530-186">[ *保存] を* 選択して、チャネルにタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="6e530-186">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="6e530-187">完了すると、Microsoft Teams 内にタブが読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="6e530-187">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![チームでのタブの実行](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="6e530-189">**おめでとうおめでとう!最初の Microsoft Teams アプリを構築して展開した**</span><span class="sxs-lookup"><span data-stu-id="6e530-189">**Congrats! You built and deployed your first Microsoft Teams app**</span></span>
