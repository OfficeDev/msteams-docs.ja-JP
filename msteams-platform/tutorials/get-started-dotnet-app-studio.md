---
title: チュートリアル - C を使用して最初のアプリを作成します。#
description: C# または .NET を使用してMicrosoft Teams アプリの構築を開始する方法について説明します。
keywords: .net c# csharp の開始
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: eaa37f1ccb7944ee18bb62ae47882dc4a715b165
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566888"
---
# <a name="create-your-first-teams-app-using-c"></a><span data-ttu-id="9f50e-104">C を使用して最初のTeams アプリを作成する#</span><span class="sxs-lookup"><span data-stu-id="9f50e-104">Create your first Teams app using C#</span></span>

<span data-ttu-id="9f50e-105">このチュートリアルでは、C# を使用してMicrosoft Teamsアプリを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-105">This tutorial helps you to create a Microsoft Teams app using C#.</span></span> <span data-ttu-id="9f50e-106">そのためには、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f50e-106">To do this, you must:</span></span>

* <span data-ttu-id="9f50e-107">環境を準備する</span><span class="sxs-lookup"><span data-stu-id="9f50e-107">Prepare your environment</span></span>
* <span data-ttu-id="9f50e-108">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="9f50e-108">Get prerequisites</span></span>
* <span data-ttu-id="9f50e-109">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="9f50e-109">Download the sample</span></span>
* <span data-ttu-id="9f50e-110">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="9f50e-110">Build and run the sample</span></span>
* <span data-ttu-id="9f50e-111">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="9f50e-111">Host the sample app</span></span>
* <span data-ttu-id="9f50e-112">ホストされたアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="9f50e-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="9f50e-113">アプリ タブを構成する</span><span class="sxs-lookup"><span data-stu-id="9f50e-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="9f50e-114">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="9f50e-114">Get prerequisites</span></span>

<span data-ttu-id="9f50e-115">このチュートリアルを完了するには、次のツールをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f50e-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="9f50e-116">Git をインストールする</span><span class="sxs-lookup"><span data-stu-id="9f50e-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="9f50e-117">Visual Studio のインストール</span><span class="sxs-lookup"><span data-stu-id="9f50e-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="9f50e-118">無料のコミュニティ版のVisual Studioをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="9f50e-119">インストール中にパスに追加するオプションがある場合 `git` は、パスを選択します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="9f50e-120">ターミナル ウィンドウで、次のコマンドを実行してインストールを確認 `git` します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="9f50e-121">プラットフォーム上で適切なターミナルウィンドウを使用します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="9f50e-122">これらの例では Git Bash を使用していますが、ほとんどのプラットフォームで実行できます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="9f50e-123">最新バージョンのVisual Studioを開き、更新プログラムをインストールします。</span><span class="sxs-lookup"><span data-stu-id="9f50e-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="9f50e-124">同じターミナル ウィンドウを使用して、このチュートリアルのコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="9f50e-125">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="9f50e-125">Download the sample</span></span>

<span data-ttu-id="9f50e-126">あなたは簡単な [こんにちは、世界で始めることができます!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="9f50e-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="9f50e-127">C# のサンプル。</span><span class="sxs-lookup"><span data-stu-id="9f50e-127">sample in C#.</span></span> <span data-ttu-id="9f50e-128">ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをコンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="9f50e-129">この[レポ](https://github.com/OfficeDev/Microsoft-Teams-Samples)[をフォーク](https://help.github.com/articles/fork-a-repo/)して変更を変更し、GitHubに保存することができます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="9f50e-130">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="9f50e-130">Build and run the sample</span></span>

<span data-ttu-id="9f50e-131">リポジトリの複製が作成されたら、Visual Studioを使用してソリューション ファイル **Microsoft.Teamsを開きます。サンプルの\*\*\*\*マイクロソフトTeamsサンプル/サンプル/アプリ-hello-world/csharp** ディレクトリから.sln。</span><span class="sxs-lookup"><span data-stu-id="9f50e-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="9f50e-132">次に、[ビルド] メニューの **[ソリューションのビルド** ] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="9f50e-133">サンプルを実行するには **、F5** キーを押すか、[**デバッグ**] メニューから **[デバッグの開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="9f50e-134">アプリが起動すると、起動したアプリのルートを示すブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="9f50e-135">次の URL に移動して、すべてのアプリ URL が読み込まれているかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="9f50e-136">エラーが表示された場合は、 `Could not find a part of the path … bin\roslyn\csc.exe` コマンドを使用してパッケージを更新 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-136">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="9f50e-137">詳細については、 [この「スタック オーバーフロー」の質問を](https://stackoverflow.com/questions/32780315)参照してください。</span><span class="sxs-lookup"><span data-stu-id="9f50e-137">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="9f50e-138">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="9f50e-138">Host the sample app</span></span>

<span data-ttu-id="9f50e-139">Microsoft Teamsのアプリは、1 つ以上の機能を提供する Web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="9f50e-139">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="9f50e-140">Teams プラットフォームでアプリを読み込むには、アプリがインターネット上で利用可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f50e-140">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="9f50e-141">これを行うには、アプリをホストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f50e-141">To do this, you need to host your app.</span></span> <span data-ttu-id="9f50e-142">無料でホストMicrosoft Azure、または を使用してコンピュータ上のローカル プロセスへのトンネルを作成することができます `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="9f50e-142">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="9f50e-143">アプリをホストしたら、そのルート URL (または など) `https://yourteamsapp.ngrok.io` `https://yourteamsapp.azurewebsites.net` をメモします。</span><span class="sxs-lookup"><span data-stu-id="9f50e-143">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="9f50e-144">ngrok を使用したTunnel</span><span class="sxs-lookup"><span data-stu-id="9f50e-144">Tunnel using ngrok</span></span>

<span data-ttu-id="9f50e-145">迅速なテストを行うために、コンピューターでアプリを実行し、Web エンドポイントを介してアプリへのトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-145">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="9f50e-146">[`ngrok`](https://ngrok.com) は、Web アドレスを取得できる無料ツールです `https://d0ac14a5.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="9f50e-146">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="9f50e-147">ngrok [をダウンロードしてインストール](https://ngrok.com/download) し、それを `PATH` .</span><span class="sxs-lookup"><span data-stu-id="9f50e-147">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="9f50e-148">をインストールした後 `ngrok` 、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-148">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="9f50e-149">`Ngrok` インターネットからのリクエストをリッスンし、ポート 44327 で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="9f50e-149">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="9f50e-150">確認するには、ブラウザーを開き、 `https://d0ac14a5.ngrok.io/hello` に移動してアプリの hello ページを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-150">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="9f50e-151">この URL の代わりに、コンソール セッションで表示される転送先アドレス `ngrok` を使用します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-151">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="9f50e-152">[ビルドと実行](#build-and-run-the-sample)の手順で別のポートを使用している場合は、トンネルをセットアップするのに同じポート番号を使用することを確認します `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="9f50e-152">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="9f50e-153">別のターミナル ウィンドウで実行することをお勧めします `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="9f50e-153">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="9f50e-154">これは、 `ngrok` アプリに干渉することなく実行されないようにするために行われます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-154">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="9f50e-155">アプリを停止、再構築、再実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f50e-155">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="9f50e-156">`ngrok`セッションは、このウィンドウでデバッグに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-156">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="9f50e-157">アプリは、コンピューター上の現在のセッション中にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-157">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="9f50e-158">マシンがシャットダウンまたはスリープ状態になった場合、サービスは利用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="9f50e-158">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="9f50e-159">テスト用のアプリを他のユーザーと共有する場合は、この点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="9f50e-159">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="9f50e-160">サービスを再起動する必要がある場合は、アプリは新しいアドレスを返し、そのアドレスを使用するすべての場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f50e-160">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="9f50e-161">有料版のの場合 `ngrok` 、この制限はありません。</span><span class="sxs-lookup"><span data-stu-id="9f50e-161">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="9f50e-162">Azure でホストする</span><span class="sxs-lookup"><span data-stu-id="9f50e-162">Host in Azure</span></span>

<span data-ttu-id="9f50e-163">Microsoft Azureは、共有インフラストラクチャを使用して、無料のレベルで .NET アプリケーションをホストします。</span><span class="sxs-lookup"><span data-stu-id="9f50e-163">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="9f50e-164">この方法でサンプルを実行できます `Hello World` 。</span><span class="sxs-lookup"><span data-stu-id="9f50e-164">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="9f50e-165">詳細については、「 [無料の Azure アカウントを新しく作成する](https://azure.microsoft.com/free/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9f50e-165">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="9f50e-166">Visual Studioには、Azure を含むさまざまなプロバイダーへのアプリのデプロイが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="9f50e-166">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="9f50e-167">ホストされたアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="9f50e-167">Update the credentials for your hosted app</span></span>

<span data-ttu-id="9f50e-168">サンプル アプリでは、テキスト ファイルに保存した値に設定する環境変数が必要です。</span><span class="sxs-lookup"><span data-stu-id="9f50e-168">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="9f50e-169">`appsettings.json` ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-169">Open the `appsettings.json` file.</span></span> <span data-ttu-id="9f50e-170">テキスト ファイルに保存したボット ID で **MicrosoftAppId** 値を更新します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-170">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="9f50e-171">保存したボット **パスワードでアプリ パスワード** を更新します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-171">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="9f50e-172">これらの変更が行われた後、アプリを再構築します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-172">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="9f50e-173">ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再デプロイします。</span><span class="sxs-lookup"><span data-stu-id="9f50e-173">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="9f50e-174">アプリ タブを構成する</span><span class="sxs-lookup"><span data-stu-id="9f50e-174">Configure the app tab</span></span>

<span data-ttu-id="9f50e-175">チームにアプリをインストールしたら、コンテンツを表示するように構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f50e-175">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="9f50e-176">サンプル アプリをインストールしたチームのチャンネルに移動し **、[+]** ボタンを選択して新しいタブを追加します。**[タブの追加]** ボックスの一覧から **[Hello World]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-176">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="9f50e-177">このチャネルに表示するタブを選択できる構成ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-177">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="9f50e-178">タブを選択し、[ **保存]** を選択すると `Hello World` 、タブがタブに読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-178">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="9f50e-179">Teamsでボットをテストする</span><span class="sxs-lookup"><span data-stu-id="9f50e-179">Test your bot in Teams</span></span>

<span data-ttu-id="9f50e-180">これで、Teamsでボットをテストできます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-180">Now you can test the bot in Teams.</span></span> <span data-ttu-id="9f50e-181">アプリを登録したチームのチャンネルを選択し、「 」と入力 `@your-bot-name` します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-181">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="9f50e-182">これはメンションと呼 **\@ ばれます**。</span><span class="sxs-lookup"><span data-stu-id="9f50e-182">This is called an **\@mention**.</span></span> <span data-ttu-id="9f50e-183">ボットは、送信したメッセージに返信します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-183">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="9f50e-184">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="9f50e-184">Test your messaging extension</span></span>

<span data-ttu-id="9f50e-185">メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある **[.]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-185">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="9f50e-186">**「ハローワールド」** アプリを使ったメニューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-186">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="9f50e-187">選択すると、ランダムなテキストのセットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-187">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="9f50e-188">ランダムテキストの 1 つを選択して、会話に挿入できます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-188">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="9f50e-189">ランダムテキストの 1 つを選択します。</span><span class="sxs-lookup"><span data-stu-id="9f50e-189">Select one of the random text.</span></span> <span data-ttu-id="9f50e-190">独自のメッセージを使用してフォーマットされ、送信できる状態のカードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9f50e-190">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
