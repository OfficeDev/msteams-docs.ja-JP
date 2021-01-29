---
title: チュートリアル - C を使用して最初のアプリを作成する#
description: C#/.NET を使用して Microsoft Teams アプリの構築を開始する方法について説明します。
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037040"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a><span data-ttu-id="f0281-104">C を使用して最初の Microsoft Teams アプリを作成する#</span><span class="sxs-lookup"><span data-stu-id="f0281-104">Create your first Microsoft Teams app using C#</span></span>

<span data-ttu-id="f0281-105">このチュートリアルは、.NET で C# を使用して Microsoft Teams アプリの作成を開始する際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="f0281-105">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="f0281-106">前提条件を取得する</span><span class="sxs-lookup"><span data-stu-id="f0281-106">Get prerequisites</span></span>

<span data-ttu-id="f0281-107">このチュートリアルを完了するには、次のツールを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f0281-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="f0281-108">Git をインストールする</span><span class="sxs-lookup"><span data-stu-id="f0281-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="f0281-109">[インストールVisual Studio](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="f0281-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="f0281-110">無料のコミュニティ エディションをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="f0281-110">You can install the free community edition.</span></span>

<span data-ttu-id="f0281-111">インストール中に PATH に追加するオプションが表示された場合は、 `git` そのオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="f0281-111">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="f0281-112">便利です。</span><span class="sxs-lookup"><span data-stu-id="f0281-112">It will be handy.</span></span>

<span data-ttu-id="f0281-113">ターミナル ウィンドウ `git` で次のコマンドを実行して、インストールを確認します。</span><span class="sxs-lookup"><span data-stu-id="f0281-113">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="f0281-114">プラットフォームで最も使いやすいターミナル ウィンドウを使用します。</span><span class="sxs-lookup"><span data-stu-id="f0281-114">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="f0281-115">これらの例では Bash を使用していますが、ほとんどのプラットフォームで実行されます。</span><span class="sxs-lookup"><span data-stu-id="f0281-115">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="f0281-116">最新バージョンの更新プログラムを必ず起動し、表示Visual Studio更新プログラムをインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="f0281-116">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="f0281-117">このターミナル ウィンドウを引き続き使用して、このチュートリアルに従うコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="f0281-117">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="f0281-118">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="f0281-118">Download the sample</span></span>

<span data-ttu-id="f0281-119">シンプルな [Hello, World が用意されています。](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="f0281-119">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="f0281-120">C# のサンプルを使用して開始してください。</span><span class="sxs-lookup"><span data-stu-id="f0281-120">sample in C# to get you started.</span></span> <span data-ttu-id="f0281-121">ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="f0281-121">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="f0281-122">今後の[参照のために](https://help.github.com/articles/fork-a-repo/) [](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) GitHub への変更を変更してチェックインする場合は、このリポジトリをフォークできます。</span><span class="sxs-lookup"><span data-stu-id="f0281-122">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="f0281-123">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="f0281-123">Build and run the sample</span></span>

<span data-ttu-id="f0281-124">リポジトリを複製したら、Visual Studio を使用して、サンプルのルート ディレクトリからソリューション ファイルを開き、メニュー `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` からクリック `Build` します。</span><span class="sxs-lookup"><span data-stu-id="f0281-124">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="f0281-125">メニューを押したり、メニューから選択したりすることで `F5` 、サンプル `Start Debugging` を実行 `Debug` できます。</span><span class="sxs-lookup"><span data-stu-id="f0281-125">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="f0281-126">アプリが起動すると、アプリのルートが表示されたブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="f0281-126">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="f0281-127">次の URL に移動して、すべてのアプリの URL が読み込み中か確認できます。</span><span class="sxs-lookup"><span data-stu-id="f0281-127">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="f0281-128">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe` like, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` .</span><span class="sxs-lookup"><span data-stu-id="f0281-128">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="f0281-129">[StackOverflow の詳細については、この](https://stackoverflow.com/questions/32780315)質問を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f0281-129">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="f0281-130">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="f0281-130">Host the sample app</span></span>

<span data-ttu-id="f0281-131">Microsoft Teams のアプリは、1 つ以上の機能を公開する Web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="f0281-131">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="f0281-132">Teams プラットフォームでアプリを読み込むには、インターネットからアプリにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="f0281-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="f0281-133">インターネットからアプリにアクセスするには、アプリをホストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f0281-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="f0281-134">Microsoft Azure で無料でホストするか、開発マシンで使用するローカル プロセスへのトンネルを作成できます `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="f0281-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="f0281-135">アプリのホストが終了したら、そのルート URL をメモします。</span><span class="sxs-lookup"><span data-stu-id="f0281-135">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="f0281-136">次のように表示 `https://yourteamsapp.ngrok.io` されます `https://yourteamsapp.azurewebsites.net` 。</span><span class="sxs-lookup"><span data-stu-id="f0281-136">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="f0281-137">ngrok を使用したトンネル</span><span class="sxs-lookup"><span data-stu-id="f0281-137">Tunnel using ngrok</span></span>

<span data-ttu-id="f0281-138">迅速なテストを行う場合は、ローカル コンピューターでアプリを実行し、Web エンドポイント経由でトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f0281-138">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="f0281-139">[ngrok は](https://ngrok.com) 、それを実行できる無料のツールです。</span><span class="sxs-lookup"><span data-stu-id="f0281-139">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="f0281-140">ngrok を使用すると、次のような Web アドレス `https://d0ac14a5.ngrok.io` を取得できます (この URL は単なる例です)。</span><span class="sxs-lookup"><span data-stu-id="f0281-140">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="f0281-141">環境に [合った](https://ngrok.com/download) ngrok をダウンロードしてインストールできます。</span><span class="sxs-lookup"><span data-stu-id="f0281-141">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="f0281-142">自分の場所に追加してください `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="f0281-142">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="f0281-143">インストールしたら、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f0281-143">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="f0281-144">サンプルではポート 3333 を使用します。そのため、ここで指定してください。</span><span class="sxs-lookup"><span data-stu-id="f0281-144">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="f0281-145">Ngrok はインターネットからの要求をリッスンし、ポート 3333 で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="f0281-145">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="f0281-146">確認するには、ブラウザーを開き、アプリの Hello ページを読 `https://d0ac14a5.ngrok.io/hello` み込む方法があります。</span><span class="sxs-lookup"><span data-stu-id="f0281-146">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="f0281-147">この URL の代わりに、コンソール セッションで ngrok によって表示される転送アドレスを使用してください。</span><span class="sxs-lookup"><span data-stu-id="f0281-147">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="f0281-148">ビルドで別のポートを使用し、[](#build-and-run-the-sample)上記の手順を実行した場合は、必ず同じポート番号を使用してトンネルをセットアップ `ngrok` してください。</span><span class="sxs-lookup"><span data-stu-id="f0281-148">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="f0281-149">後で停止、リビルド、再実行が必要になる可能性があるアプリを妨げることなく、別のターミナル ウィンドウで実行し続けます `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="f0281-149">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="f0281-150">セッション `ngrok` は、このウィンドウで有用なデバッグ情報を返します。</span><span class="sxs-lookup"><span data-stu-id="f0281-150">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="f0281-151">アプリは、開発用コンピューター上の現在のセッション中にのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="f0281-151">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="f0281-152">コンピューターがシャットダウンするか、スリープ状態になった場合、サービスは利用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="f0281-152">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="f0281-153">他のユーザーがテスト用にアプリを共有する場合は、このことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="f0281-153">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="f0281-154">サービスを再起動する必要がある場合は、新しいアドレスが返され、そのアドレスを使用する場所ごとに更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f0281-154">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="f0281-155">Ngrok の有料版には、この制限はありません。</span><span class="sxs-lookup"><span data-stu-id="f0281-155">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="f0281-156">Azure でのホスト</span><span class="sxs-lookup"><span data-stu-id="f0281-156">Host in Azure</span></span>

<span data-ttu-id="f0281-157">Microsoft Azure では、共有インフラストラクチャを使用して無料の階層で .NET アプリケーションをホストできます。</span><span class="sxs-lookup"><span data-stu-id="f0281-157">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="f0281-158">このサンプルを実行するにはこれで十分 `Hello World` です。</span><span class="sxs-lookup"><span data-stu-id="f0281-158">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="f0281-159">詳 [しくは、新しい無料アカウントの作成](https://azure.microsoft.com/free/) に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f0281-159">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="f0281-160">Visual Studioには、Azure を含むさまざまなプロバイダーへのアプリ展開のサポートが組み込みされています。</span><span class="sxs-lookup"><span data-stu-id="f0281-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="f0281-161">ホストされているアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="f0281-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="f0281-162">サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f0281-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="f0281-163">ファイルのappsettings.js開きます。</span><span class="sxs-lookup"><span data-stu-id="f0281-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="f0281-164">*MicrosoftAppId の値を*、以前に保存したボット ID で更新します。</span><span class="sxs-lookup"><span data-stu-id="f0281-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="f0281-165">*MicrosoftAppPassword を、以前* に保存した Bot パスワードで更新します。</span><span class="sxs-lookup"><span data-stu-id="f0281-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="f0281-166">これらの変更が行われたら、アプリをリビルドします。</span><span class="sxs-lookup"><span data-stu-id="f0281-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="f0281-167">ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再展開します。</span><span class="sxs-lookup"><span data-stu-id="f0281-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="f0281-168">[アプリ] タブを構成する</span><span class="sxs-lookup"><span data-stu-id="f0281-168">Configure the app tab</span></span>

<span data-ttu-id="f0281-169">アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f0281-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="f0281-170">サンプル アプリをインストールしたチームのチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。その後、[タブ `Hello World` の追加] **ボックスの一覧から選択** できます。</span><span class="sxs-lookup"><span data-stu-id="f0281-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="f0281-171">構成ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f0281-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="f0281-172">このダイアログでは、このチャネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="f0281-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="f0281-173">タブを選択してクリックすると、選択したタブと一緒に読み込 `Save` `Hello World` まれたタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f0281-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="f0281-174">Teams でボットをテストする</span><span class="sxs-lookup"><span data-stu-id="f0281-174">Test your bot in Teams</span></span>

<span data-ttu-id="f0281-175">Teams でボットを操作できます。</span><span class="sxs-lookup"><span data-stu-id="f0281-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="f0281-176">アプリを登録したチームのチャネルを選択し、「」と入力します `@your-bot-name` 。</span><span class="sxs-lookup"><span data-stu-id="f0281-176">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="f0281-177">これはメンションと呼 **\@ ばれる。**</span><span class="sxs-lookup"><span data-stu-id="f0281-177">This is called an **\@mention**.</span></span> <span data-ttu-id="f0281-178">ボットに送信したメッセージは、返信として返送されます。</span><span class="sxs-lookup"><span data-stu-id="f0281-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="f0281-179">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="f0281-179">Test your messaging extension</span></span>

<span data-ttu-id="f0281-180">メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f0281-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="f0281-181">メニューに **"Hello World"** アプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f0281-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="f0281-182">クリックすると、一連のランダムなテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f0281-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="f0281-183">You can choose any one of them and it will be inserted it into your conversation.</span><span class="sxs-lookup"><span data-stu-id="f0281-183">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="f0281-184">ランダムなテキストのいずれかを選択すると、カードがフォーマットされ、下部に独自のメッセージと一緒に送信する準備が整っているのが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f0281-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
