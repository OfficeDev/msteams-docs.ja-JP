---
title: チュートリアル - C を使用して最初のアプリを作成する#
description: アプリまたは .NET を使用してアプリMicrosoft TeamsをC#する方法について学習します。
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 58e11312e61124bf09fcb55d2bcd0fc475e75a49
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114616"
---
# <a name="build-your-first-teams-app-using-c"></a><span data-ttu-id="2c4b1-104">C を使用してTeamsアプリをビルドする#</span><span class="sxs-lookup"><span data-stu-id="2c4b1-104">Build your first Teams app using C#</span></span>

<span data-ttu-id="2c4b1-105">このチュートリアルでは、.NET またはアプリを使用して最初のアプリをMicrosoft Teamsする方法をC#。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-105">In this tutorial, you will learn how to build your very first Microsoft Teams app using .NET or C#.</span></span> <span data-ttu-id="2c4b1-106">また、以下の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-106">It also walks you through the steps to:</span></span>

1. [<span data-ttu-id="2c4b1-107">環境を準備する</span><span class="sxs-lookup"><span data-stu-id="2c4b1-107">Prepare your environment</span></span>](#prepare-your-environment)
1. [<span data-ttu-id="2c4b1-108">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="2c4b1-108">Get prerequisites</span></span>](#GetPrerequisites)
1. [<span data-ttu-id="2c4b1-109">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="2c4b1-109">Download the sample</span></span>](#DownloadSample)
1. [<span data-ttu-id="2c4b1-110">サンプルのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="2c4b1-110">Build and run the sample</span></span>](#BuildRun)
1. [<span data-ttu-id="2c4b1-111">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="2c4b1-111">Host the sample app</span></span>](#hostsample)
1. [<span data-ttu-id="2c4b1-112">ホストされたアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="2c4b1-112">Update the credentials for your hosted app</span></span>](#updatecredentials)
1. <span data-ttu-id="2c4b1-113">[[アプリ] タブの構成](#configureapptab)</span><span class="sxs-lookup"><span data-stu-id="2c4b1-113">[Configure the app tab](#configureapptab)</span></span>

<a name="prepare-your-environment"></a>
[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="2c4b1-114">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="2c4b1-114">Get prerequisites</span></span>

<span data-ttu-id="2c4b1-115">このチュートリアルを完了するには、次のツールをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="2c4b1-116">Git のインストール</span><span class="sxs-lookup"><span data-stu-id="2c4b1-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="2c4b1-117">Visual Studio のインストール</span><span class="sxs-lookup"><span data-stu-id="2c4b1-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="2c4b1-118">無料のコミュニティ エディションの Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="2c4b1-119">インストール中に、パスに追加するオプションがある `git` 場合は、パスを選択します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="2c4b1-120">ターミナル ウィンドウで、次のコマンドを実行してインストールを確認 `git` します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="2c4b1-121">プラットフォームで適切なターミナル ウィンドウを使用します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="2c4b1-122">これらの例では Git Bash を使用しますが、ほとんどのプラットフォームで実行できます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="2c4b1-123">最新バージョンの更新プログラムを開Visual Studio更新プログラムをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="2c4b1-124">このチュートリアルでは、同じターミナル ウィンドウを使用してコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="2c4b1-125">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="2c4b1-125">Download the sample</span></span>

<span data-ttu-id="2c4b1-126">簡単な Hello、 [World を使い始めよう!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="2c4b1-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="2c4b1-127">サンプルをC#。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-127">sample in C#.</span></span> <span data-ttu-id="2c4b1-128">ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをコンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="2c4b1-129">このレ[ポをフォーク](https://help.github.com/articles/fork-a-repo/)して[変更](https://github.com/OfficeDev/Microsoft-Teams-Samples)を変更し、変更を保存GitHub。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="2c4b1-130">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="2c4b1-130">Build and run the sample</span></span>

<span data-ttu-id="2c4b1-131">smaple は、複製後にビルドして実行できます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-131">You can build and run the smaple after it is cloned.</span></span> 

<span data-ttu-id="2c4b1-132">**複製されたサンプルをビルドして実行するには**</span><span class="sxs-lookup"><span data-stu-id="2c4b1-132">**To build and run the cloned sample**</span></span>

1. <span data-ttu-id="2c4b1-133">ソリューション ファイル **Microsoft.Teams を開きます。サンプルの** **Microsoft-Teams-Samples/samples/app-hello-world/csharp** ディレクトリの Samples.HelloWorld.sln。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-133">Open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span>
1. <span data-ttu-id="2c4b1-134">[ビルド **] メニューから [** ソリューションの **ビルド] を** 選択します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-134">Select **Build Solution** from the **Build** menu.</span></span>
1. <span data-ttu-id="2c4b1-135">**F5 キーを選択** するか、[**デバッグ]** メニューから [デバッグの開始] を **選択** してサンプルを実行します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-135">Select the **F5** key, or select **Start Debugging** from the **Debug** menu to run the sample.</span></span>

<span data-ttu-id="2c4b1-136">アプリが起動すると、ブラウザー ウィンドウが開き、アプリのルートが起動します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-136">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="2c4b1-137">次の URL に移動して、すべてのアプリ URL が読み込み中か確認できます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-137">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

> [!Note]
> <span data-ttu-id="2c4b1-138">エラーが発生した場合は `Could not find a part of the path … bin\roslyn\csc.exe` 、コマンドを使用してパッケージを更新します `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-138">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="2c4b1-139">詳細については、「スタック オーバーフロー [」のこの質問を参照してください](https://stackoverflow.com/questions/32780315)。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-139">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

<a name="hostsample"></a>
## <a name="deploy-your-sample-app"></a><span data-ttu-id="2c4b1-140">サンプル アプリの展開</span><span class="sxs-lookup"><span data-stu-id="2c4b1-140">Deploy your sample app</span></span>

<span data-ttu-id="2c4b1-141">アプリはMicrosoft Teams 1 つ以上の機能を提供する Web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-141">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="2c4b1-142">アプリをTeamsするには、アプリをインターネットで利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-142">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="2c4b1-143">これを行うには、アプリをホストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-143">To do this, you need to host your app.</span></span> <span data-ttu-id="2c4b1-144">無料でホストするかMicrosoft Azureを使用して、コンピューター上のローカル プロセスへのトンネルを作成できます `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-144">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="2c4b1-145">アプリをホストした後、ルート URL (またはなど) をメモ `https://yourteamsapp.ngrok.io` します `https://yourteamsapp.azurewebsites.net` 。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-145">After you host your app, make a note of its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="2c4b1-146">Tunnel ngrok の使用</span><span class="sxs-lookup"><span data-stu-id="2c4b1-146">Tunnel using ngrok</span></span>

<span data-ttu-id="2c4b1-147">クイック テストでは、コンピューターでアプリを実行し、Web エンドポイントを介してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-147">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="2c4b1-148">[`ngrok`](https://ngrok.com) は、 などの Web アドレスを取得できる無料のツールです `https://d0ac14a5.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-148">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="2c4b1-149">ngrok [をダウンロードしてインストール](https://ngrok.com/download) し、それを自分の場所に追加できます `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-149">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="2c4b1-150">インストール後、 `ngrok` 新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-150">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="2c4b1-151">`Ngrok` インターネットからの要求に応答し、ポート 44327 で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-151">`Ngrok` responds to requests from the internet and routes them to your app running on port 44327.</span></span> 

<span data-ttu-id="2c4b1-152">**応答を確認するには**</span><span class="sxs-lookup"><span data-stu-id="2c4b1-152">**To verify the response**</span></span>

1. <span data-ttu-id="2c4b1-153">ブラウザーを開き、`https://d0ac14a5.ngrok.io/hello` に移動します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-153">Open your browser and go to `https://d0ac14a5.ngrok.io/hello`.</span></span> <span data-ttu-id="2c4b1-154">これにより、アプリの Hello ページが読み込まれる。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-154">This will load your app's Hello page.</span></span>
1. <span data-ttu-id="2c4b1-155">手順 1 で説明した URL の代わりに、コンソール セッションに表示される転送 `ngrok` アドレスを使用します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-155">Instead of the URL mentioned in Step 1, use the forwarding address displayed by `ngrok` in your console session.</span></span>
    > [!NOTE]
    > <span data-ttu-id="2c4b1-156">ビルドと実行の手順で別のポート[](#build-and-run-the-sample)を使用している場合は、同じポート番号を使用してトンネルをセットアップ `ngrok` してください。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-156">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>
    > [!TIP]
    > <span data-ttu-id="2c4b1-157">別のターミナル ウィンドウで実行 `ngrok` すると良い考えです。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-157">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="2c4b1-158">これは、アプリに干渉 `ngrok` することなく実行を維持するために行われます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-158">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="2c4b1-159">アプリを停止、再構築、再実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-159">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="2c4b1-160">セッション `ngrok` は、このウィンドウで役立つデバッグ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-160">The `ngrok` session provides useful debugging information in this window.</span></span>

    <span data-ttu-id="2c4b1-161">アプリは、コンピューター上の現在のセッション中にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-161">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="2c4b1-162">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-162">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="2c4b1-163">テスト用アプリを他のユーザーと共有する場合は、このことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-163">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="2c4b1-164">サービスを再起動する必要がある場合、アプリは新しいアドレスを返し、そのアドレスを使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-164">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="2c4b1-165">有料版には `ngrok` 、この制限はありません。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-165">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="2c4b1-166">Azure のホスト</span><span class="sxs-lookup"><span data-stu-id="2c4b1-166">Host in Azure</span></span>

<span data-ttu-id="2c4b1-167">Microsoft Azure共有インフラストラクチャを使用して、.NET アプリケーションを無料層でホストします。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-167">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="2c4b1-168">これは、サンプルを実行するのに十分 `Hello World` です。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-168">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="2c4b1-169">詳細については、「新しい無料の [Azure アカウントの作成」を参照してください](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-169">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="2c4b1-170">Visual Studio Azure を含むさまざまなプロバイダーへのアプリ展開の組み込みのサポートがあります。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-170">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

<span data-ttu-id="2c4b1-171">**アプリ パッケージを更新する**</span><span class="sxs-lookup"><span data-stu-id="2c4b1-171">**Update the app package**</span></span>

# <a name="app-studio"></a>[<span data-ttu-id="2c4b1-172">App Studio</span><span class="sxs-lookup"><span data-stu-id="2c4b1-172">App Studio</span></span>](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[<span data-ttu-id="2c4b1-173">開発者ポータル</span><span class="sxs-lookup"><span data-stu-id="2c4b1-173">Developer Portal</span></span>](#tab/DP)

<span data-ttu-id="2c4b1-174">**開発者ポータル (プレビュー) をインストールするには、Teams**</span><span class="sxs-lookup"><span data-stu-id="2c4b1-174">**To install Developer Portal (preview) in Teams**</span></span>


1. <span data-ttu-id="2c4b1-175">左側の **バーの** 下部にある [アプリ] アイコンを選択し、[開発者ポータル] **を検索します**。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-175">Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.</span></span>

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. <span data-ttu-id="2c4b1-176">[開発者 **ポータル] を選択し** 、[開く] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-176">Select **Developer Portal** and select **Open**.</span></span>

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. <span data-ttu-id="2c4b1-177">[アプリ] タブを選択し、[ **既存のアプリのインポート] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-177">Select the Apps tab and select **Import an existing app**.</span></span>

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. <span data-ttu-id="2c4b1-178">[Hello **World] を選択し** 、[インポート] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-178">Select **Hello World** and select **Import**.</span></span> <span data-ttu-id="2c4b1-179">**Hello World アプリ** は開発者ポータルにインポートされます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-179">The **Hello World** app is imported in Developer Portal.</span></span> 

    <span data-ttu-id="2c4b1-180">開発者ポータルを使用してアプリTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-180">You can configure your app using the Teams Developer Portal.</span></span> <span data-ttu-id="2c4b1-181">マニフェストは [配布] の下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-181">The Manifest is found under Distribute.</span></span> <span data-ttu-id="2c4b1-182">マニフェストを使用して、アプリの機能、必要なリソース、その他の重要な属性を構成できます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-182">You can use the Manifest to configure capabilities, required resources, and other important attributes for your app.</span></span> <span data-ttu-id="2c4b1-183">開発者ポータルを使用してアプリを構成する方法の詳細については、「開発者ポータル」[を参照Teamsしてください](../concepts/build-and-test/teams-developer-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-183">For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span></span>

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>
---

<a name="updatecredentials"></a>
## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="2c4b1-184">ホストされたアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="2c4b1-184">Update the credentials for your hosted app</span></span>

<span data-ttu-id="2c4b1-185">サンプル アプリでは、テキスト ファイルに保存した値に環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-185">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="2c4b1-186">**ホストされているアプリの資格情報を更新するには**</span><span class="sxs-lookup"><span data-stu-id="2c4b1-186">**To update the credentials for your hosted app**</span></span>

1. <span data-ttu-id="2c4b1-187">`appsettings.json` ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-187">Open the `appsettings.json` file.</span></span> 
1. <span data-ttu-id="2c4b1-188">テキスト ファイルに保存したボット ID で **MicrosoftAppId** 値を更新します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-188">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> 
1. <span data-ttu-id="2c4b1-189">保存した **ボット パスワードを使用して MicrosoftAppPassword** を更新します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-189">Update the **MicrosoftAppPassword** with the bot password that you saved.</span></span>

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    <span data-ttu-id="2c4b1-190">これらの変更が行われた後、アプリを再構築します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-190">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="2c4b1-191">ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合は、アプリを再展開します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-191">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a><span data-ttu-id="2c4b1-192">[アプリ] タブの構成</span><span class="sxs-lookup"><span data-stu-id="2c4b1-192">Configure the app tab</span></span>

<span data-ttu-id="2c4b1-193">アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-193">After you have installed the app into teams, you must configure it to display the content.</span></span> 

<span data-ttu-id="2c4b1-194">**アプリ タブを構成するには**</span><span class="sxs-lookup"><span data-stu-id="2c4b1-194">**To configure the app tab**</span></span>

1. <span data-ttu-id="2c4b1-195">サンプル アプリをインストールしたチームのチャネルに移動し **、[+]** ボタンを選択して新しいタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-195">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab.</span></span>
1. <span data-ttu-id="2c4b1-196">[ **タブの追加] リスト** から **[Hello World] を選択** します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-196">Select **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="2c4b1-197">構成ダイアログ ボックスが表示され、このチャネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-197">A configuration dialog box is displayed that enables you to select the tab to display in this channel.</span></span> 
1. <span data-ttu-id="2c4b1-198">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-198">Select **Save**.</span></span> <span data-ttu-id="2c4b1-199">タブ `Hello World` はタブと一緒に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-199">The `Hello World` tab is loaded with the tab.</span></span>

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="2c4b1-200">ボットをテストTeams</span><span class="sxs-lookup"><span data-stu-id="2c4b1-200">Test your bot in Teams</span></span>

<span data-ttu-id="2c4b1-201">これで、ボットをテストできます。Teams。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-201">You can now test the bot in Teams.</span></span> 

<span data-ttu-id="2c4b1-202">**ボットをテストするには**</span><span class="sxs-lookup"><span data-stu-id="2c4b1-202">**To test your bot**</span></span>

* <span data-ttu-id="2c4b1-203">アプリを登録して入力したチーム内のチャネルを選択します `@your-bot-name` 。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-203">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="2c4b1-204">これはメンションと呼 **\@ ばれる.**</span><span class="sxs-lookup"><span data-stu-id="2c4b1-204">This is called an **\@mention**.</span></span> <span data-ttu-id="2c4b1-205">ボットは、送信したメッセージに返信します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-205">The bot replies to any message that you send.</span></span>

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="2c4b1-206">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="2c4b1-206">Test your messaging extension</span></span>

<span data-ttu-id="2c4b1-207">メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある **...** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-207">To test your messaging extension, select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="2c4b1-208">「Hello **World」アプリを含むメニュー** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-208">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="2c4b1-209">選択すると、ランダムなテキストのセットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-209">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="2c4b1-210">ランダムなテキストの 1 つを選択し、会話に挿入できます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-210">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

<span data-ttu-id="2c4b1-211">ランダムなテキストのいずれかを選択します。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-211">Select one of the random text.</span></span> <span data-ttu-id="2c4b1-212">独自のメッセージを使用して送信する準備が整ったカードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2c4b1-212">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a><span data-ttu-id="2c4b1-213">関連項目</span><span class="sxs-lookup"><span data-stu-id="2c4b1-213">See also</span></span>

* [<span data-ttu-id="2c4b1-214">チュートリアルの概要</span><span class="sxs-lookup"><span data-stu-id="2c4b1-214">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="2c4b1-215">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="2c4b1-215">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)