---
title: チュートリアル - C を使用して最初のアプリを作成する#
description: Microsoft Teams アプリの作成を開始する方法については、C# .NET を使用します。
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: ee90d07b9616d130f4c418427762f9531c203672
ms.sourcegitcommit: c9446200b8e76fbd434d012dc11dd9f191776d13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2021
ms.locfileid: "51403977"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="2098e-104">ユーザーまたは .NET を使用して最初C# Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="2098e-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="2098e-105">このチュートリアルでは、ユーザーまたは .NET を使用して Microsoft Teams C#作成できます。</span><span class="sxs-lookup"><span data-stu-id="2098e-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span> <span data-ttu-id="2098e-106">そのためには、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="2098e-106">To do this, you must:</span></span>

* <span data-ttu-id="2098e-107">環境を準備する</span><span class="sxs-lookup"><span data-stu-id="2098e-107">Prepare your environment</span></span>
* <span data-ttu-id="2098e-108">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="2098e-108">Get prerequisites</span></span>
* <span data-ttu-id="2098e-109">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="2098e-109">Download the sample</span></span>
* <span data-ttu-id="2098e-110">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="2098e-110">Build and run the sample</span></span>
* <span data-ttu-id="2098e-111">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="2098e-111">Host the sample app</span></span>
* <span data-ttu-id="2098e-112">ホストされたアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="2098e-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="2098e-113">[アプリ] タブの構成</span><span class="sxs-lookup"><span data-stu-id="2098e-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="2098e-114">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="2098e-114">Get prerequisites</span></span>

<span data-ttu-id="2098e-115">このチュートリアルを完了するには、次のツールをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2098e-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="2098e-116">Git のインストール</span><span class="sxs-lookup"><span data-stu-id="2098e-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="2098e-117">Visual Studio のインストール</span><span class="sxs-lookup"><span data-stu-id="2098e-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="2098e-118">無料のコミュニティ エディションの Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2098e-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="2098e-119">インストール中に、パスに追加するオプションがある `git` 場合は、パスを選択します。</span><span class="sxs-lookup"><span data-stu-id="2098e-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="2098e-120">ターミナル ウィンドウで、次のコマンドを実行してインストールを確認 `git` します。</span><span class="sxs-lookup"><span data-stu-id="2098e-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="2098e-121">プラットフォームで適切なターミナル ウィンドウを使用します。</span><span class="sxs-lookup"><span data-stu-id="2098e-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="2098e-122">これらの例では Git Bash を使用しますが、ほとんどのプラットフォームで実行できます。</span><span class="sxs-lookup"><span data-stu-id="2098e-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="2098e-123">最新バージョンの更新プログラムを開Visual Studio更新プログラムをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2098e-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="2098e-124">このチュートリアルでは、同じターミナル ウィンドウを使用してコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="2098e-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="2098e-125">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="2098e-125">Download the sample</span></span>

<span data-ttu-id="2098e-126">簡単な Hello、 [World を使い始めよう!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="2098e-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="2098e-127">サンプルをC#。</span><span class="sxs-lookup"><span data-stu-id="2098e-127">sample in C#.</span></span> <span data-ttu-id="2098e-128">ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをコンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="2098e-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="2098e-129">このリポジトリ [をフォーク](https://help.github.com/articles/fork-a-repo/) して [、](https://github.com/OfficeDev/Microsoft-Teams-Samples) 変更を GitHub に変更して保存できます。</span><span class="sxs-lookup"><span data-stu-id="2098e-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="2098e-130">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="2098e-130">Build and run the sample</span></span>

<span data-ttu-id="2098e-131">リポジトリを複製した後、Visual Studio を使用して、サンプルの **Microsoft-Teams-Samples/samples/app-hello-world/csharp** ディレクトリからソリューション ファイル **Microsoft.Teams.Samples.HelloWorld.sln** を開きます。</span><span class="sxs-lookup"><span data-stu-id="2098e-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="2098e-132">次に、[ビルド] **メニューから [ソリューション** のビルド **] を** 選択します。</span><span class="sxs-lookup"><span data-stu-id="2098e-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="2098e-133">サンプルを実行するには **、F5 キーを押するか、[** デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="2098e-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="2098e-134">アプリが起動すると、ブラウザー ウィンドウが開き、アプリのルートが起動します。</span><span class="sxs-lookup"><span data-stu-id="2098e-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="2098e-135">次の URL に移動して、すべてのアプリ URL が読み込み中か確認できます。</span><span class="sxs-lookup"><span data-stu-id="2098e-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second](https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="2098e-136">エラーが発生した場合は `Could not find a part of the path … bin\roslyn\csc.exe` 、コマンドを使用してパッケージを更新します `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。</span><span class="sxs-lookup"><span data-stu-id="2098e-136">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="2098e-137">詳細については、「スタック オーバーフロー [」のこの質問を参照してください](https://stackoverflow.com/questions/32780315)。</span><span class="sxs-lookup"><span data-stu-id="2098e-137">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="2098e-138">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="2098e-138">Host the sample app</span></span>

<span data-ttu-id="2098e-139">Microsoft Teams のアプリは、1 つ以上の機能を提供する Web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="2098e-139">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="2098e-140">Teams プラットフォームでアプリを読み込むには、アプリをインターネットで利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="2098e-140">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="2098e-141">これを行うには、アプリをホストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2098e-141">To do this, you need to host your app.</span></span> <span data-ttu-id="2098e-142">Microsoft Azure で無料でホストするか、コンピューター上のローカル プロセスへのトンネルを作成します `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="2098e-142">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="2098e-143">アプリをホストした後、ルート URL (など) を `https://yourteamsapp.ngrok.io` メモします `https://yourteamsapp.azurewebsites.net` 。</span><span class="sxs-lookup"><span data-stu-id="2098e-143">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="2098e-144">ngrok を使用したトンネル</span><span class="sxs-lookup"><span data-stu-id="2098e-144">Tunnel using ngrok</span></span>

<span data-ttu-id="2098e-145">クイック テストでは、コンピューターでアプリを実行し、Web エンドポイントを介してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="2098e-145">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="2098e-146">[`ngrok`](https://ngrok.com) は、 などの Web アドレスを取得できる無料のツールです `https://d0ac14a5.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="2098e-146">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="2098e-147">ngrok [をダウンロードしてインストール](https://ngrok.com/download) し、それを自分の場所に追加できます `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="2098e-147">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="2098e-148">インストール後、 `ngrok` 新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2098e-148">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="2098e-149">`Ngrok` インターネットからの要求をリッスンし、ポート 44327 で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="2098e-149">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="2098e-150">確認するには、ブラウザーを開き、アプリの hello ページ `https://d0ac14a5.ngrok.io/hello` を読み込むに移動します。</span><span class="sxs-lookup"><span data-stu-id="2098e-150">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="2098e-151">この URL の代わりに、コンソール セッションに表示される転送 `ngrok` アドレスを使用します。</span><span class="sxs-lookup"><span data-stu-id="2098e-151">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="2098e-152">ビルドと実行の手順で別のポート[](#build-and-run-the-sample)を使用している場合は、同じポート番号を使用してトンネルをセットアップ `ngrok` してください。</span><span class="sxs-lookup"><span data-stu-id="2098e-152">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="2098e-153">別のターミナル ウィンドウで実行 `ngrok` すると良い考えです。</span><span class="sxs-lookup"><span data-stu-id="2098e-153">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="2098e-154">これは、アプリに干渉 `ngrok` することなく実行を維持するために行われます。</span><span class="sxs-lookup"><span data-stu-id="2098e-154">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="2098e-155">アプリを停止、再構築、再実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2098e-155">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="2098e-156">セッション `ngrok` は、このウィンドウで役立つデバッグ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="2098e-156">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="2098e-157">アプリは、コンピューター上の現在のセッション中にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="2098e-157">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="2098e-158">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="2098e-158">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="2098e-159">テスト用アプリを他のユーザーと共有する場合は、このことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="2098e-159">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="2098e-160">サービスを再起動する必要がある場合、アプリは新しいアドレスを返し、そのアドレスを使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2098e-160">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="2098e-161">有料版には `ngrok` 、この制限はありません。</span><span class="sxs-lookup"><span data-stu-id="2098e-161">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="2098e-162">Azure のホスト</span><span class="sxs-lookup"><span data-stu-id="2098e-162">Host in Azure</span></span>

<span data-ttu-id="2098e-163">Microsoft Azure は、共有インフラストラクチャを使用して無料層で .NET アプリケーションをホストします。</span><span class="sxs-lookup"><span data-stu-id="2098e-163">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="2098e-164">これは、サンプルを実行するのに十分 `Hello World` です。</span><span class="sxs-lookup"><span data-stu-id="2098e-164">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="2098e-165">詳細については、「新しい無料の [Azure アカウントの作成」を参照してください](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="2098e-165">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="2098e-166">Visual Studio Azure を含むさまざまなプロバイダーへのアプリ展開の組み込みのサポートがあります。</span><span class="sxs-lookup"><span data-stu-id="2098e-166">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="2098e-167">ホストされたアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="2098e-167">Update the credentials for your hosted app</span></span>

<span data-ttu-id="2098e-168">サンプル アプリでは、テキスト ファイルに保存した値に環境変数を設定する [必要があります](~/includes/get-started/get-started-use-app-studio.md#bots)。</span><span class="sxs-lookup"><span data-stu-id="2098e-168">The sample app requires the environment variables to be set to the values that you saved in the [text file](~/includes/get-started/get-started-use-app-studio.md#bots).</span></span>

<span data-ttu-id="2098e-169">ファイルのappsettings.js開きます。</span><span class="sxs-lookup"><span data-stu-id="2098e-169">Open the appsettings.json file.</span></span> <span data-ttu-id="2098e-170">テキスト ファイルに保存したボット ID で **MicrosoftAppId** 値を更新します。</span><span class="sxs-lookup"><span data-stu-id="2098e-170">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="2098e-171">保存した **ボット パスワードを使用して MicrosoftAppPassword** を更新します。</span><span class="sxs-lookup"><span data-stu-id="2098e-171">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="2098e-172">これらの変更が行われた後、アプリを再構築します。</span><span class="sxs-lookup"><span data-stu-id="2098e-172">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="2098e-173">ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合は、アプリを再展開します。</span><span class="sxs-lookup"><span data-stu-id="2098e-173">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="2098e-174">[アプリ] タブの構成</span><span class="sxs-lookup"><span data-stu-id="2098e-174">Configure the app tab</span></span>

<span data-ttu-id="2098e-175">アプリをチームにインストールしたら、コンテンツを表示するアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2098e-175">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="2098e-176">サンプル アプリをインストールしたチームのチャネルに移動し **、[+]** ボタンを選択して新しいタブを追加します。[ **タブの追加] リスト** から **[Hello World] を選択** します。</span><span class="sxs-lookup"><span data-stu-id="2098e-176">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="2098e-177">構成ダイアログ ボックスが表示され、このチャネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="2098e-177">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="2098e-178">タブを選択し、[タブを保存する] **を** `Hello World` 選択すると、タブが読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="2098e-178">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="2098e-179">Teams でボットをテストする</span><span class="sxs-lookup"><span data-stu-id="2098e-179">Test your bot in Teams</span></span>

<span data-ttu-id="2098e-180">これで、Teams でボットをテストできます。</span><span class="sxs-lookup"><span data-stu-id="2098e-180">Now you can test the bot in Teams.</span></span> <span data-ttu-id="2098e-181">アプリを登録して入力したチーム内のチャネルを選択します `@your-bot-name` 。</span><span class="sxs-lookup"><span data-stu-id="2098e-181">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="2098e-182">これはメンションと呼 **\@ ばれる.**</span><span class="sxs-lookup"><span data-stu-id="2098e-182">This is called an **\@mention**.</span></span> <span data-ttu-id="2098e-183">ボットは、送信したメッセージに返信します。</span><span class="sxs-lookup"><span data-stu-id="2098e-183">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="2098e-184">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="2098e-184">Test your messaging extension</span></span>

<span data-ttu-id="2098e-185">メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある **...** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2098e-185">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="2098e-186">「Hello **World」アプリを含むメニュー** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="2098e-186">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="2098e-187">選択すると、ランダムなテキストのセットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2098e-187">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="2098e-188">ランダムなテキストの 1 つを選択し、会話に挿入できます。</span><span class="sxs-lookup"><span data-stu-id="2098e-188">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="2098e-189">ランダムなテキストのいずれかを選択します。</span><span class="sxs-lookup"><span data-stu-id="2098e-189">Select one of the random text.</span></span> <span data-ttu-id="2098e-190">独自のメッセージを使用して送信する準備が整ったカードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2098e-190">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
