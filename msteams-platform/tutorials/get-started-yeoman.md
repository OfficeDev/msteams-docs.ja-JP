---
title: Microsoft Teams 用のごみ箱のジェネレーターを使い始める
description: Microsoft Teams 用のごみ箱のジェネレーターでのすぐれたアプリの構築を開始する
keywords: js ノード js の概要
ms.openlocfilehash: 6318b51c29c673b0bf3504218100cf0d7aad7b97
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228088"
---
# <a name="build-your-first-microsoft-teams-app"></a><span data-ttu-id="76547-104">最初の Microsoft Teams アプリを構築する</span><span class="sxs-lookup"><span data-stu-id="76547-104">Build your First Microsoft Teams App</span></span>

>[!Note]
><span data-ttu-id="76547-105">このチュートリアルは、 [Teams wiki 用のごみ箱のジェネレーター](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)からのものです。</span><span class="sxs-lookup"><span data-stu-id="76547-105">This tutorial comes from the [yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span></span>

<span data-ttu-id="76547-106">このチュートリアルでは、Microsoft Teams を使用して初めて Microsoft Teams アプリを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="76547-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="76547-107">[Microsoft Teams アプリのサイドローディングが有効になっ](~/concepts/build-and-test/prepare-your-o365-tenant.md)ていることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="76547-107">It assumes that you have [enabled side-loading of Microsoft Teams apps](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![ごみ箱のジェネレーター git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="76547-109">コンピューターをセットアップして準備する</span><span class="sxs-lookup"><span data-stu-id="76547-109">Setup and prepare your machine</span></span>

<span data-ttu-id="76547-110">Teams ジェネレーターの使用を開始する前に、次のものをコンピューターにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="76547-110">You need to install the following on your machine before starting to use the Teams Generator.</span></span>

### <a name="install-node"></a><span data-ttu-id="76547-111">インストールノード</span><span class="sxs-lookup"><span data-stu-id="76547-111">Install Node</span></span>

<span data-ttu-id="76547-112">NodeJS がコンピューターにインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="76547-112">You need to have NodeJS installed on your machine.</span></span> <span data-ttu-id="76547-113">最新の[LTS バージョン](https://nodejs.org/dist/latest-v8.x/)を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="76547-113">You should use the latest [LTS version](https://nodejs.org/dist/latest-v8.x/).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="76547-114">コード エディターのインストール</span><span class="sxs-lookup"><span data-stu-id="76547-114">Install a code editor</span></span>

<span data-ttu-id="76547-115">コードエディターも必要ですが、任意のテキストエディターを自由に使用できます。</span><span class="sxs-lookup"><span data-stu-id="76547-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="76547-116">ただし、このドキュメントとスクリーンショットのほとんどは、 [Visual Studio Code](https://code.visualstudio.com)の使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="76547-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="76547-117">Gulp CLI をインストールする</span><span class="sxs-lookup"><span data-stu-id="76547-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="76547-118">Teams ジェネレーターを使用してプロジェクトをスキャフォールディングできるようにするには、Gulp CLI タスクマネージャーに加えて、その他のツールをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="76547-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="76547-119">コマンドプロンプトを開き、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="76547-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-microsoft-teams-apps-generator---yo-teams"></a><span data-ttu-id="76547-120">Microsoft Teams Apps generator-Yo Teams をインストールする</span><span class="sxs-lookup"><span data-stu-id="76547-120">Install the Microsoft Teams Apps generator - Yo Teams</span></span>

<span data-ttu-id="76547-121">Microsoft Teams アプリ用のごみ箱のジェネレーターは、次のコマンドを使用してインストールされます。</span><span class="sxs-lookup"><span data-stu-id="76547-121">The Yeoman generator for Microsoft Teams apps are installed with the following command:</span></span>

```bash
npm install generator-teams --global
```

#### <a name="install-preview-versions"></a><span data-ttu-id="76547-122">プレビューバージョンをインストールする</span><span class="sxs-lookup"><span data-stu-id="76547-122">Install preview versions</span></span>

<span data-ttu-id="76547-123">次のコマンドを使用して Teams ジェネレーターのプレビューバージョンをインストールする場合は、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="76547-123">If you want to install preview versions of the Teams generator with this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="76547-124">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="76547-124">Generate your project</span></span>

<span data-ttu-id="76547-125">コマンドプロンプトを開き、プロジェクトを作成する新しいディレクトリを作成し、そのディレクトリにコマンド`yo teams`を入力します。</span><span class="sxs-lookup"><span data-stu-id="76547-125">Open up a command prompt and create a new directory where you want to create your project and in that directory type the command `yo teams`.</span></span> <span data-ttu-id="76547-126">これにより Teams アプリジェネレーターが開始され、一連の質問が寄せられます。</span><span class="sxs-lookup"><span data-stu-id="76547-126">This will start the Teams Apps generator and you will be asked a set of questions.</span></span>

![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="76547-128">最初の質問はプロジェクト名についてのもので、enter キーを押してそのままにしておくことができます。</span><span class="sxs-lookup"><span data-stu-id="76547-128">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="76547-129">次の質問は、新しいディレクトリを作成するか、現在のディレクトリを使用するかを尋ねられます。</span><span class="sxs-lookup"><span data-stu-id="76547-129">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="76547-130">必要なディレクトリにあるように、enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="76547-130">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="76547-131">次の手順では、プロジェクトのタイトルを求めます。このタイトルは、アプリのマニフェストと説明で使用されます。</span><span class="sxs-lookup"><span data-stu-id="76547-131">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="76547-132">その後、会社名の入力を求められます。これはマニフェストでも使用されます。</span><span class="sxs-lookup"><span data-stu-id="76547-132">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="76547-133">5番目の質問では、使用するマニフェストのバージョンについて確認します。</span><span class="sxs-lookup"><span data-stu-id="76547-133">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="76547-134">このチュートリアルでは`v1.5`、[現在使用可能な汎用スキーマ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="76547-134">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="76547-135">その後、ジェネレーターはプロジェクトに追加するアイテムを要求します。</span><span class="sxs-lookup"><span data-stu-id="76547-135">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="76547-136">1つまたは複数のアイテムの組み合わせを選択できます。</span><span class="sxs-lookup"><span data-stu-id="76547-136">You can select a single one or any combination of items.</span></span> <span data-ttu-id="76547-137">ここでは、*タブを選択する*だけです。</span><span class="sxs-lookup"><span data-stu-id="76547-137">For now, just select *a Tab*.</span></span>

![アイテムの選択](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="76547-139">選択したアイテムに基づいて、一連のフォローアップ質問が表示されます。</span><span class="sxs-lookup"><span data-stu-id="76547-139">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="76547-140">ここで、ソリューションをホストする場所の URL を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="76547-140">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="76547-141">任意の URL を指定できますが、既定では、ジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="76547-141">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="76547-142">ジェネレーターには、オプトインまたはオプトアウトできる高度な機能が多数組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="76547-142">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="76547-143">URL の質問に従って、ソリューションの単体テストを含めるかどうかを尋ねられます。既定値は [はい] です。</span><span class="sxs-lookup"><span data-stu-id="76547-143">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="76547-144">このオプションを選択すると、生成されたプロジェクトには、スキャフォールディングされているさまざまなアイテムについて、単体テストフレームワークと既定の単体テストがあります。</span><span class="sxs-lookup"><span data-stu-id="76547-144">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="76547-145">このチュートリアルでは、テストフレームワークを含めないことを選択します。</span><span class="sxs-lookup"><span data-stu-id="76547-145">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="76547-146">ログ記録を簡単にするために、ログに Azure Application Insights を使用するかどうかを確認するメッセージも表示されます。</span><span class="sxs-lookup"><span data-stu-id="76547-146">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="76547-147">[はい] を選択した場合は、Azure Application Insights キーを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="76547-147">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="76547-148">このチュートリアルでは、Application Insights の使用のオプトアウトを行います。</span><span class="sxs-lookup"><span data-stu-id="76547-148">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="76547-149">次の一連の質問は、以前に選択したアイテムを基にしています。</span><span class="sxs-lookup"><span data-stu-id="76547-149">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="76547-150">タブの場合は、名前を指定するだけで、必要に応じて、このアプリを SharePoint Online web パーツとして使用できるようにするかどうかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="76547-150">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="76547-151">この名前を入力すると、ジェネレーターによってプロジェクトが生成され、すべての依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="76547-151">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="76547-152">これには 1 ~ 2 分かかります。</span><span class="sxs-lookup"><span data-stu-id="76547-152">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="76547-153">タブにコードを追加する</span><span class="sxs-lookup"><span data-stu-id="76547-153">Add some code to your tab</span></span>

<span data-ttu-id="76547-154">ジェネレーターが完了すると、任意のコードエディターでソリューションを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="76547-154">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="76547-155">時間をかけて、コードがどのように整理されているかを理解し、[プロジェクト構造](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)のドキュメントで詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="76547-155">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="76547-156">タブは`./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx`ファイル内に配置されます。</span><span class="sxs-lookup"><span data-stu-id="76547-156">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="76547-157">これは、タブの TypeScript に対応した基本クラスです`render()` 。メソッドを見つけ、 `<PanelBody>`コントロール内にコードの行を追加して、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="76547-157">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="76547-158">ファイルを保存し、コマンドプロンプトに戻ります。</span><span class="sxs-lookup"><span data-stu-id="76547-158">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="76547-159">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="76547-159">Build your app</span></span>

<span data-ttu-id="76547-160">これで、プロジェクトをビルドできるようになります。</span><span class="sxs-lookup"><span data-stu-id="76547-160">You can now build your project.</span></span> <span data-ttu-id="76547-161">これは、2つの手順 (または、次の手順を参照) で行われます。</span><span class="sxs-lookup"><span data-stu-id="76547-161">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="76547-162">最初に Teams アプリのマニフェストファイルを作成する必要があります。これにより、Microsoft Teams にサイドロードをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="76547-162">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="76547-163">これは、Gulp タスク`gulp manifest`によって実行されます。</span><span class="sxs-lookup"><span data-stu-id="76547-163">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="76547-164">これにより、マニフェストが検証され、 `./package`ディレクトリに zip ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="76547-164">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="76547-165">ソリューションを構築するには、 `gulp build`このコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="76547-165">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="76547-166">これにより、ソリューションが`./dist`フォルダーに transpile されます。</span><span class="sxs-lookup"><span data-stu-id="76547-166">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="76547-167">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="76547-167">Run your app</span></span>

<span data-ttu-id="76547-168">アプリを実行するには、 `gulp serve`このコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="76547-168">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="76547-169">これにより、アプリをテストするためのローカル web サーバーが構築および開始されます。</span><span class="sxs-lookup"><span data-stu-id="76547-169">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="76547-170">また、プロジェクトでファイルを保存するたびに、アプリケーションが再構築されます。</span><span class="sxs-lookup"><span data-stu-id="76547-170">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="76547-171">これで`http://localhost:3007/myFirstAppTab/` 、tab がレンダリングされていることを確認できるようになります。</span><span class="sxs-lookup"><span data-stu-id="76547-171">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="76547-172">ただし、Microsoft Teams ではまだありません。</span><span class="sxs-lookup"><span data-stu-id="76547-172">However, not in Microsoft Teams yet.</span></span>

![ブラウザーでサイトを表示する](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="76547-174">Microsoft Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="76547-174">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="76547-175">Microsoft Teams では、アプリを localhost でホストすることはできません。したがって、公開 URL に公開するか、ngrok などのプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="76547-175">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="76547-176">朗報として、スキャフォールディングプロジェクトにはこの組み込みがあります。</span><span class="sxs-lookup"><span data-stu-id="76547-176">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="76547-177">を実行`gulp ngrok-serve`すると、ngrok サービスはバックグラウンドで開始され、一意の DNS エントリとパブリック DNS エントリが作成されます。さらに、この一意の URL を使用して`gulp serve`マニフェストをパッケージ化して、とまったく同じことを行います。</span><span class="sxs-lookup"><span data-stu-id="76547-177">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="76547-178">を実行`gulp ngrok-serve`した後、新しい Microsoft Teams チームを作成して作成したら、チーム名をクリックして、Teams の設定に移動し、[*アプリ*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="76547-178">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="76547-179">右下隅に [*カスタムアプリをアップロード*する] というリンクが表示されたら、それを選択して、という名前`package`のプロジェクトフォルダーとサブフォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="76547-179">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="76547-180">そのフォルダー内の zip ファイルを選択し、[開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="76547-180">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="76547-181">これで、アプリが Microsoft Teams にサイドロードされました。</span><span class="sxs-lookup"><span data-stu-id="76547-181">Your App is now sideloaded into Microsoft Teams.</span></span>

![サイドロードアプリ](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="76547-183">*一般的な*チャネルに戻り、新しいタブ*+* を追加するには、を選択します。タブの一覧にタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="76547-183">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![[構成] タブ](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="76547-185">タブを選択し、指示に従って追加します。</span><span class="sxs-lookup"><span data-stu-id="76547-185">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="76547-186">ソースを編集できるカスタム構成ダイアログがあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="76547-186">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="76547-187">[*保存*] を選択して、タブをチャネルに追加します。</span><span class="sxs-lookup"><span data-stu-id="76547-187">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="76547-188">完了すると、Microsoft Teams 内でタブが読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="76547-188">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![teams での実行中のタブ](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="76547-190">**Congrats!最初の Microsoft Teams アプリを構築して展開した**</span><span class="sxs-lookup"><span data-stu-id="76547-190">**Congrats! You built and deployed your first Microsoft Teams App**</span></span>
