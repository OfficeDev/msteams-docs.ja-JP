---
title: C#/.NET を使用して作業を開始する
description: C#/.NET を使用して Microsoft Teams での高度なアプリの作成を始める
keywords: .net c# csharp の概要
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 61237cd3178fcb41357230536827f732faf65ee4
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550960"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-cnet-and-app-studio"></a><span data-ttu-id="85449-104">Microsoft Teams プラットフォームで C#/.NET とアプリ Studio を使用して作業を開始する</span><span class="sxs-lookup"><span data-stu-id="85449-104">Get started on the Microsoft Teams platform with C#/.NET and App Studio</span></span>

<span data-ttu-id="85449-105">[Microsoft teams](/microsoftteams/)開発者プラットフォームを使用すると、teams の拡張が容易になり、独自のアプリケーションやサービスを teams ワークスペースにシームレスに統合することができます。</span><span class="sxs-lookup"><span data-stu-id="85449-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="85449-106">これらのアプリは、企業または世界中の teams に配布できます。</span><span class="sxs-lookup"><span data-stu-id="85449-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="85449-107">Microsoft Teams を拡張するには、Microsoft Teams アプリを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85449-107">To extend Microsoft Teams, you will need to create a Microsoft Teams app.</span></span> <span data-ttu-id="85449-108">Microsoft Teams アプリは、ホストする web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="85449-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="85449-109">このアプリは、Teams のユーザーのワークスペースに統合できます。</span><span class="sxs-lookup"><span data-stu-id="85449-109">This app can then be integrated into the user's workspace in Teams.</span></span>

<span data-ttu-id="85449-110">このチュートリアルでは、.NET での C# を使用した Microsoft Teams アプリの作成を開始する際に役立つ情報が得られます。</span><span class="sxs-lookup"><span data-stu-id="85449-110">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span> <span data-ttu-id="85449-111">アプリをテストするには、アクセス許可を持っているチームに読み込むか、Office 開発者プログラムを使用して作成したテストテナントに取り込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="85449-111">You can test the app by loading it into a Team that you have permissions for, or into a test tenant created using the Office Developer Program.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="85449-112">前提条件を取得する</span><span class="sxs-lookup"><span data-stu-id="85449-112">Get prerequisites</span></span>

<span data-ttu-id="85449-113">このチュートリアルを完了するには、次のツールを入手する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85449-113">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="85449-114">Git をインストールする</span><span class="sxs-lookup"><span data-stu-id="85449-114">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="85449-115">[Visual Studio をインストール](https://www.visualstudio.com/downloads/)します。</span><span class="sxs-lookup"><span data-stu-id="85449-115">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="85449-116">無料のコミュニティエディションをインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="85449-116">You can install the free community edition.</span></span>

<span data-ttu-id="85449-117">インストール時にパスに追加`git`するオプションが表示された場合は、それを選択します。</span><span class="sxs-lookup"><span data-stu-id="85449-117">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="85449-118">これは便利です。</span><span class="sxs-lookup"><span data-stu-id="85449-118">It will be handy.</span></span>

<span data-ttu-id="85449-119">ターミナルウィンドウ`git`で次のように実行して、インストールを確認します。</span><span class="sxs-lookup"><span data-stu-id="85449-119">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="85449-120">ご使用のプラットフォームで最も快適なターミナルウィンドウを使用してください。</span><span class="sxs-lookup"><span data-stu-id="85449-120">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="85449-121">これらの例では Bash を使用していますが、ほとんどのプラットフォームで実行されます。</span><span class="sxs-lookup"><span data-stu-id="85449-121">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="85449-122">必要に応じて、最新バージョンの Visual Studio を起動し、更新プログラムをインストールします。</span><span class="sxs-lookup"><span data-stu-id="85449-122">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="85449-123">このターミナルウィンドウを引き続き使用して、このチュートリアルの後のコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="85449-123">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="85449-124">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="85449-124">Download the sample</span></span>

<span data-ttu-id="85449-125">シンプルな Hello を提供してい[ます。](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="85449-125">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="85449-126">開始する方法については、C# のサンプルをご確認ください。</span><span class="sxs-lookup"><span data-stu-id="85449-126">sample in C# to get you started.</span></span> <span data-ttu-id="85449-127">ターミナルウィンドウで、次のコマンドを実行して、サンプルリポジトリをローカルコンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="85449-127">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="85449-128">後で参照できるように GitHub への変更を変更してチェックインする場合は、この[リポジトリ](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)を[fork](https://help.github.com/articles/fork-a-repo/)することができます。</span><span class="sxs-lookup"><span data-stu-id="85449-128">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="85449-129">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="85449-129">Build and run the sample</span></span>

<span data-ttu-id="85449-130">リポジトリのクローンを作成したら、Visual Studio を使用して`Microsoft.Teams.Samples.HelloWorld.sln` 、サンプルのルートディレクトリからソリューションファイルを`Build Solution`開き、 `Build`メニューから [] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="85449-130">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="85449-131">このサンプルを実行するには`F5` 、メニュー `Start Debugging`から [ `Debug` ] を押すか、選択します。</span><span class="sxs-lookup"><span data-stu-id="85449-131">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="85449-132">アプリが開始すると、アプリのルートが起動されたブラウザーウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="85449-132">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="85449-133">次の Url に移動して、すべてのアプリ Url が読み込まれていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="85449-133">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="85449-134">そのような`Could not find a part of the path … bin\roslyn\csc.exe`エラーが表示された場合は、コマンド`Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`を使用してパッケージを更新してみてください。</span><span class="sxs-lookup"><span data-stu-id="85449-134">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="85449-135">詳細については、[スタックオーバーフローでこの質問](https://stackoverflow.com/questions/32780315)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85449-135">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="85449-136">サンプルアプリをホストする</span><span class="sxs-lookup"><span data-stu-id="85449-136">Host the sample app</span></span>

<span data-ttu-id="85449-137">Microsoft Teams のアプリは、1つまたは複数の機能を公開している web アプリケーションであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="85449-137">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="85449-138">Teams プラットフォームでアプリを読み込むには、インターネットからアプリにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="85449-138">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="85449-139">アプリをインターネットからアクセスできるようにするには、アプリをホストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="85449-139">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="85449-140">Microsoft Azure で無料でホストすることも、を使用`ngrok`して開発用コンピューター上のローカルプロセスへのトンネルを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="85449-140">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="85449-141">アプリのホストが終了したら、ルート URL を書き留めておきます。</span><span class="sxs-lookup"><span data-stu-id="85449-141">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="85449-142">これは、 `https://yourteamsapp.ngrok.io`または`https://yourteamsapp.azurewebsites.net`というようになります。</span><span class="sxs-lookup"><span data-stu-id="85449-142">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="85449-143">Ngrok を使用したトンネル</span><span class="sxs-lookup"><span data-stu-id="85449-143">Tunnel using ngrok</span></span>

<span data-ttu-id="85449-144">迅速なテストのために、ローカルコンピューター上でアプリを実行し、web エンドポイント経由でそのアプリケーションへのトンネルを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="85449-144">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="85449-145">[ngrok](https://ngrok.com)は、そのようなことを可能にする無償のツールです。</span><span class="sxs-lookup"><span data-stu-id="85449-145">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="85449-146">Ngrok を使用すると`https://d0ac14a5.ngrok.io` 、などの web アドレスを取得できます (この URL は例にすぎません)。</span><span class="sxs-lookup"><span data-stu-id="85449-146">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="85449-147">環境の ngrok を[ダウンロードしてインストール](https://ngrok.com/download)することができます。</span><span class="sxs-lookup"><span data-stu-id="85449-147">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="85449-148">がの場所に追加さ`PATH`れていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="85449-148">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="85449-149">インストールすると、新しいターミナルウィンドウを開き、次のコマンドを実行してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="85449-149">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="85449-150">このサンプルではポート3333を使用しているため、ここで必ず指定してください。</span><span class="sxs-lookup"><span data-stu-id="85449-150">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="85449-151">Ngrok は、インターネットからの要求をリスンし、ポート3333で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="85449-151">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="85449-152">ブラウザー `https://d0ac14a5.ngrok.io/hello`を開き、アプリの hello ページを読み込むことによって確認できます。</span><span class="sxs-lookup"><span data-stu-id="85449-152">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="85449-153">この URL ではなく、コンソールセッションで ngrok によって表示される転送アドレスを使用してください。</span><span class="sxs-lookup"><span data-stu-id="85449-153">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="85449-154">上記の[ビルド](#build-and-run-the-sample)で別のポートを使用している場合は、同じポート番号を使用して`ngrok`トンネルを設定してください。</span><span class="sxs-lookup"><span data-stu-id="85449-154">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="85449-155">後で停止して再構築`ngrok`して再実行する必要があるアプリケーションに影響を与えることなく、別のターミナルウィンドウで実行して、そのまま実行することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="85449-155">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="85449-156">この`ngrok`ウィンドウでは、セッションが有用なデバッグ情報を返します。</span><span class="sxs-lookup"><span data-stu-id="85449-156">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="85449-157">アプリは、開発コンピューター上の現在のセッション中にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="85449-157">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="85449-158">コンピューターがシャットダウンされるかスリープ状態になると、サービスは使用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="85449-158">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="85449-159">他のユーザーによるテスト用にアプリを共有する場合は、この点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="85449-159">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="85449-160">サービスを再起動する必要がある場合は、新しいアドレスを返し、そのアドレスを使用するすべての場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85449-160">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="85449-161">Ngrok の有料バージョンには、この制限はありません。</span><span class="sxs-lookup"><span data-stu-id="85449-161">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="85449-162">Azure でのホスト</span><span class="sxs-lookup"><span data-stu-id="85449-162">Host in Azure</span></span>

<span data-ttu-id="85449-163">Microsoft Azure を使用すると、共有インフラストラクチャを使用して、.NET アプリケーションを自由層でホストできます。</span><span class="sxs-lookup"><span data-stu-id="85449-163">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="85449-164">この`Hello World`サンプルを実行するには、この方法で十分です。</span><span class="sxs-lookup"><span data-stu-id="85449-164">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="85449-165">詳細について[は、「新しい無料アカウントの作成](https://azure.microsoft.com/free/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85449-165">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="85449-166">Visual Studio には、Azure を含むさまざまなプロバイダーへのアプリ展開のサポートが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="85449-166">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" src="~/assets/images/get-started/publishtoazure1.png" title="Visual Studio"/>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="85449-168">ホストされているアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="85449-168">Update the credentials for your hosted app</span></span>

<span data-ttu-id="85449-169">サンプルアプリでは、以下の環境変数を事前にメモした値に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85449-169">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="85449-170">Web.config ファイルを開き、 *appSettings*セクションを見つけます。</span><span class="sxs-lookup"><span data-stu-id="85449-170">Open up the web.config file and find the *appSettings* section.</span></span> <span data-ttu-id="85449-171">以前に保存した Bot ID を使用して、 *Microsoft appid*の値を更新します。</span><span class="sxs-lookup"><span data-stu-id="85449-171">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="85449-172">以前に保存した Bot パスワードを使用して、 *Microsoft Apppassword*を更新します。</span><span class="sxs-lookup"><span data-stu-id="85449-172">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" src="~/assets/images/get-started/get-started-net-azure-add-keys.png" title="キーの設定"/>

<span data-ttu-id="85449-174">これらの変更を行った後、アプリを再構築します。</span><span class="sxs-lookup"><span data-stu-id="85449-174">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="85449-175">Ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再展開します。</span><span class="sxs-lookup"><span data-stu-id="85449-175">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="85449-176">[アプリ] タブを構成する</span><span class="sxs-lookup"><span data-stu-id="85449-176">Configure the app tab</span></span>

<span data-ttu-id="85449-177">アプリをチームにインストールしたら、コンテンツを表示するように構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85449-177">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="85449-178">サンプルアプリをインストールしたチームのチャネルに移動し、[ **+** ] ボタンをクリックして新しいタブを追加します。その後、[ `Hello World` **タブの追加]** ボックスの一覧から選択できます。</span><span class="sxs-lookup"><span data-stu-id="85449-178">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="85449-179">構成ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="85449-179">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="85449-180">このダイアログボックスを使用すると、このチャネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="85449-180">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="85449-181">タブを選択して、[] `Save`をクリックすると、 `Hello World`選択したタブが読み込まれたタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="85449-181">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" src="~/assets/images/samples-hello-world-tab-configure.png" title="構成のスクリーンショット" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="85449-183">Teams でボットをテストする</span><span class="sxs-lookup"><span data-stu-id="85449-183">Test your bot in Teams</span></span>

<span data-ttu-id="85449-184">Teams で bot と対話できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="85449-184">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="85449-185">アプリを登録したチームでチャネルを選択し、と入力`@your-bot-name`します。</span><span class="sxs-lookup"><span data-stu-id="85449-185">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="85449-186">これは、 \*\* \@メンション\*\*と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="85449-186">This is called an **\@mention**.</span></span> <span data-ttu-id="85449-187">Bot に送信するすべてのメッセージは、返信として返送されます。</span><span class="sxs-lookup"><span data-stu-id="85449-187">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" title="ボット応答" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="85449-189">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="85449-189">Test your messaging extension</span></span>

<span data-ttu-id="85449-190">メッセージング拡張機能をテストするには、スレッドビューの入力ボックスの下にある3つのドットをクリックします。</span><span class="sxs-lookup"><span data-stu-id="85449-190">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="85449-191">**' Hello World '** アプリが含まれるメニューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="85449-191">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="85449-192">これをクリックすると、一連のランダムなテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="85449-192">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="85449-193">いずれかを選択して、会話に挿入することができます。</span><span class="sxs-lookup"><span data-stu-id="85449-193">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" title="メッセージング拡張メニュー" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" title="メッセージング拡張機能の結果" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="85449-196">ランダムなテキストの1つを選択すると、カードが書式設定されており、メッセージの下部に自分のメッセージで送信する準備ができます。</span><span class="sxs-lookup"><span data-stu-id="85449-196">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" title="メッセージング拡張送信" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
