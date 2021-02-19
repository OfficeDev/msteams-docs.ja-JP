---
title: チュートリアル - C を使用して最初のアプリを作成する#
description: C# または .NET を使用して Microsoft Teams アプリの構築を開始する方法について説明します。
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 29cc4e0f434bf9ece9c6073af84627acc048b628
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294755"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="ecb03-104">C# または .NET を使用して最初の Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="ecb03-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="ecb03-105">このチュートリアルでは、C# または .NET を使用して Microsoft Teams アプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="ecb03-106">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="ecb03-106">Get prerequisites</span></span>

<span data-ttu-id="ecb03-107">このチュートリアルを完了するには、次のツールを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ecb03-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="ecb03-108">Git のインストール</span><span class="sxs-lookup"><span data-stu-id="ecb03-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="ecb03-109">[インストールVisual Studio.](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="ecb03-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="ecb03-110">無料のコミュニティ エディションをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-110">You can install the free community edition.</span></span>

<span data-ttu-id="ecb03-111">インストール中に、PATH に追加するオプションがある `git` 場合は、それを選択します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-111">During installation, if there is an option to add `git` to the PATH, choose it.</span></span>

<span data-ttu-id="ecb03-112">ターミナル ウィンドウで、次のコマンドを実行してインストールを確認 `git` します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-112">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="ecb03-113">プラットフォームで適切なターミナル ウィンドウを使用します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-113">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="ecb03-114">これらの例では Bash を使用しますが、ほとんどのプラットフォームで実行されます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-114">These examples use Bash but run on most platforms.</span></span>

<span data-ttu-id="ecb03-115">更新プログラムの最新バージョンを起動しVisual Studioインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="ecb03-115">Make sure to launch the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="ecb03-116">このチュートリアルでは、同じターミナル ウィンドウを使用してコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-116">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="ecb03-117">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="ecb03-117">Download the sample</span></span>

<span data-ttu-id="ecb03-118">簡単な Hello、 [World を使い始めよう!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="ecb03-118">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="ecb03-119">C# のサンプル。</span><span class="sxs-lookup"><span data-stu-id="ecb03-119">sample in C#.</span></span> <span data-ttu-id="ecb03-120">ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-120">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="ecb03-121">このリポジトリ [をフォーク](https://help.github.com/articles/fork-a-repo/) して [変更](https://github.com/OfficeDev/Microsoft-Teams-Samples) を変更し、GitHub に保存して参照することができます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-121">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub for reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="ecb03-122">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="ecb03-122">Build and run the sample</span></span>

<span data-ttu-id="ecb03-123">リポジトリを複製した後、Visual Studio を使用して、サンプルの `Microsoft.Teams.Samples.HelloWorld.sln` **Microsoft-Teams-Samples/samples/app-hello-world/csharp** ディレクトリからソリューション ファイルを開き、メニューから選択します `Build Solution` `Build` 。</span><span class="sxs-lookup"><span data-stu-id="ecb03-123">After the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample and select `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="ecb03-124">サンプルを実行するには、メニュー `F5` を押す `Start Debugging` または選択 `Debug` します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-124">To run the sample press `F5` or choose `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="ecb03-125">アプリが起動すると、ブラウザー ウィンドウが開き、アプリのルートが起動します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-125">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="ecb03-126">次の URL に移動して、すべてのアプリ URL が読み込み中か確認できます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-126">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- <span data-ttu-id="ecb03-127">[https://localhost:44327/second]https://localhost:44327/second)</span><span class="sxs-lookup"><span data-stu-id="ecb03-127">[https://localhost:44327/second]https://localhost:44327/second)</span></span>

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="ecb03-128">エラーが発生した場合は `Could not find a part of the path … bin\roslyn\csc.exe` 、コマンドを使用してパッケージを更新します `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。</span><span class="sxs-lookup"><span data-stu-id="ecb03-128">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="ecb03-129">詳細については [、StackOverflow のこの質問を参照してください](https://stackoverflow.com/questions/32780315)。</span><span class="sxs-lookup"><span data-stu-id="ecb03-129">For more information, see [this question on StackOverflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="ecb03-130">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="ecb03-130">Host the sample app</span></span>

<span data-ttu-id="ecb03-131">Microsoft Teams のアプリは、1 つ以上の機能を提供する Web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="ecb03-131">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="ecb03-132">Teams プラットフォームでアプリを読み込むには、アプリにインターネットからアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="ecb03-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="ecb03-133">インターネットからアプリにアクセスするには、アプリをホストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ecb03-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="ecb03-134">Microsoft Azure で無料でホストするか、開発マシンのローカル プロセスへのトンネルを作成します `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="ecb03-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="ecb03-135">アプリのホストが完了したら、そのルート URL に注意してください。</span><span class="sxs-lookup"><span data-stu-id="ecb03-135">When you finish hosting your app, note its root URL.</span></span> <span data-ttu-id="ecb03-136">たとえば、`https://yourteamsapp.ngrok.io` または `https://yourteamsapp.azurewebsites.net` などです。</span><span class="sxs-lookup"><span data-stu-id="ecb03-136">For example, `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="ecb03-137">ngrok を使用したトンネル</span><span class="sxs-lookup"><span data-stu-id="ecb03-137">Tunnel using ngrok</span></span>

<span data-ttu-id="ecb03-138">クイック テストでは、ローカル コンピューターでアプリを実行し、Web エンドポイントを介してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-138">For quick testing, you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="ecb03-139">[ngrok](https://ngrok.com) は、次のような Web アドレスを取得できる無料のツールです `https://d0ac14a5.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="ecb03-139">[ngrok](https://ngrok.com) is a free tool with which you can get a web address such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="ecb03-140">ngrok [をダウンロードして](https://ngrok.com/download) インストールできます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-140">You can [download and install](https://ngrok.com/download) ngrok.</span></span> <span data-ttu-id="ecb03-141">必ず、このファイルを自分の場所に追加してください `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="ecb03-141">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="ecb03-142">ngrok をインストールした後、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-142">After you install ngrok, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="ecb03-143">このサンプルでは、ポート 44327 を使用します。必ず指定してください。</span><span class="sxs-lookup"><span data-stu-id="ecb03-143">The sample uses port 44327 be sure to specify it.</span></span>

<span data-ttu-id="ecb03-144">Ngrok はインターネットからの要求をリッスンし、ポート 44327 で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="ecb03-144">Ngrok listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="ecb03-145">確認するには、ブラウザーを開き、アプリの hello ページ `https://d0ac14a5.ngrok.io/hello` を読み込むに移動します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-145">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="ecb03-146">この URL の代わりに、コンソール セッションで ngrok によって表示される転送アドレスを使用します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-146">Instead of this URL, use the forwarding address displayed by ngrok in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="ecb03-147">ビルドと実行の手順で別のポート[](#build-and-run-the-sample)を使用している場合は、同じポート番号を使用してトンネルをセットアップ `ngrok` してください。</span><span class="sxs-lookup"><span data-stu-id="ecb03-147">If you have used a different port in the [build and run](#build-and-run-the-sample) step, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="ecb03-148">別のターミナル ウィンドウで実行 `ngrok` すると良い考えです。</span><span class="sxs-lookup"><span data-stu-id="ecb03-148">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="ecb03-149">これは、停止、再構築、再実行が必要なアプリに干渉することなく ngrok を実行し続ける場合に行います。</span><span class="sxs-lookup"><span data-stu-id="ecb03-149">This is done to keep ngrok from running without interfering with the app, which you have to stop, rebuild, and rerun.</span></span> <span data-ttu-id="ecb03-150">セッション `ngrok` は、このウィンドウで役立つデバッグ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-150">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="ecb03-151">アプリは、開発マシン上の現在のセッション中にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-151">The app is only available during the current session on your development machine.</span></span> <span data-ttu-id="ecb03-152">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="ecb03-152">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="ecb03-153">テスト用アプリを他のユーザーと共有する場合は、このことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="ecb03-153">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="ecb03-154">サービスを再起動する必要がある場合、アプリは新しいアドレスを返し、そのアドレスを使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ecb03-154">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="ecb03-155">有料バージョンの ngrok には、この制限はありません。</span><span class="sxs-lookup"><span data-stu-id="ecb03-155">The paid version of ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="ecb03-156">Azure のホスト</span><span class="sxs-lookup"><span data-stu-id="ecb03-156">Host in Azure</span></span>

<span data-ttu-id="ecb03-157">Microsoft Azure は、共有インフラストラクチャを使用して無料層で .NET アプリケーションをホストします。</span><span class="sxs-lookup"><span data-stu-id="ecb03-157">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="ecb03-158">これは、サンプルを実行するのに十分 `Hello World` です。</span><span class="sxs-lookup"><span data-stu-id="ecb03-158">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="ecb03-159">詳細については、「新しい無料アカウント [の作成」を参照してください](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="ecb03-159">For more information, see [creating a new free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="ecb03-160">Visual Studio Azure を含むさまざまなプロバイダーへのアプリ展開の組み込みのサポートがあります。</span><span class="sxs-lookup"><span data-stu-id="ecb03-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="ecb03-161">ホストされたアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="ecb03-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="ecb03-162">サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ecb03-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="ecb03-163">ファイルのappsettings.js開きます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="ecb03-164">以前に *保存したボット* ID で MicrosoftAppId 値を更新します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="ecb03-165">以前に *保存したボット パスワードを使用して MicrosoftAppPassword* を更新します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="ecb03-166">これらの変更が行われたら、アプリを再構築します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="ecb03-167">ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再展開します。</span><span class="sxs-lookup"><span data-stu-id="ecb03-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="ecb03-168">[アプリ] タブの構成</span><span class="sxs-lookup"><span data-stu-id="ecb03-168">Configure the app tab</span></span>

<span data-ttu-id="ecb03-169">アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ecb03-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="ecb03-170">サンプル アプリをインストールしたチームのチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。次に、[タブ `Hello World` の追加 **] リストから選択** できます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="ecb03-171">その後、構成ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="ecb03-172">このダイアログでは、このチャネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="ecb03-173">タブを選択してクリックすると、選択したタブが読 `Save` `Hello World` み込まれたタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="ecb03-174">Teams でボットをテストする</span><span class="sxs-lookup"><span data-stu-id="ecb03-174">Test your bot in Teams</span></span>

<span data-ttu-id="ecb03-175">Teams でボットを操作できます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="ecb03-176">アプリを登録したチーム内のチャネルを選択し、入力します `@your-bot-name` 。</span><span class="sxs-lookup"><span data-stu-id="ecb03-176">Choose a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="ecb03-177">これはメンションと呼 **\@ ばれる.**</span><span class="sxs-lookup"><span data-stu-id="ecb03-177">This is called an **\@mention**.</span></span> <span data-ttu-id="ecb03-178">ボットに送信したメッセージは、返信として返されます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="ecb03-179">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="ecb03-179">Test your messaging extension</span></span>

<span data-ttu-id="ecb03-180">メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ecb03-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="ecb03-181">メニューに「Hello **World」アプリが** 表示されます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="ecb03-182">クリックすると、ランダムなテキストの束が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="ecb03-183">任意の 1 つを選択すると、会話に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="ecb03-183">You can choose any one of them and it is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="ecb03-184">ランダムなテキストのいずれかを選択すると、カードが書式設定され、下部に独自のメッセージを送信する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="ecb03-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
