---
title: チュートリアル - アプリを使用して最初のアプリをNode.js
description: アプリの作成を開始する方法Microsoft TeamsをNode.js。
keywords: nodejs App Studio node.jsの開始方法
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 84c3452c739f67c2908d698b627b5651ff9d5d7a
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254373"
---
# <a name="build-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="fbe47-104">アプリを使用してMicrosoft TeamsアプリをNode.js</span><span class="sxs-lookup"><span data-stu-id="fbe47-104">Build your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="fbe47-105">このチュートリアルでは、アプリを使用して最初のアプリをMicrosoft Teamsする方法Node.js。</span><span class="sxs-lookup"><span data-stu-id="fbe47-105">In this tutorial, you will learn how to build your very first Microsoft Teams app using Node.js.</span></span> <span data-ttu-id="fbe47-106">また、以下の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-106">It also walks you through the steps to:</span></span> 

1. [<span data-ttu-id="fbe47-107">環境を準備する</span><span class="sxs-lookup"><span data-stu-id="fbe47-107">Prepare your environment</span></span>](#prepare-environment)
1. [<span data-ttu-id="fbe47-108">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="fbe47-108">Get prerequisites</span></span>](#GetPrerequisites)
1. [<span data-ttu-id="fbe47-109">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="fbe47-109">Download the sample</span></span>](#DownloadSample)
1. [<span data-ttu-id="fbe47-110">サンプルのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="fbe47-110">Build and run the sample</span></span>](#BuildRun)
1. [<span data-ttu-id="fbe47-111">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="fbe47-111">Host the sample app</span></span>](#HostSample)
1. [<span data-ttu-id="fbe47-112">ホストされたアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="fbe47-112">Update the credentials for your hosted app</span></span>](#updatecredentials)
1. <span data-ttu-id="fbe47-113">[[アプリ] タブの構成](#ConfigureTheAppTab)</span><span class="sxs-lookup"><span data-stu-id="fbe47-113">[Configure the app tab](#ConfigureTheAppTab)</span></span>

<a name="prepare-environment"></a>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

### <a name="download-and-host-your-app"></a><span data-ttu-id="fbe47-114">アプリをダウンロードしてホストする</span><span class="sxs-lookup"><span data-stu-id="fbe47-114">Download and host your app</span></span>

<span data-ttu-id="fbe47-115">次の手順に従って、シンプルな "hello world" アプリをダウンロードしてホストTeams。</span><span class="sxs-lookup"><span data-stu-id="fbe47-115">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="fbe47-116">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="fbe47-116">Get prerequisites</span></span>

<span data-ttu-id="fbe47-117">このチュートリアルを完了するには、次のツールが必要です。</span><span class="sxs-lookup"><span data-stu-id="fbe47-117">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="fbe47-118">まだインストールしていない場合は、これらのリンクからインストールできます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-118">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="fbe47-119">Git</span><span class="sxs-lookup"><span data-stu-id="fbe47-119">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="fbe47-120">Node.js NPM</span><span class="sxs-lookup"><span data-stu-id="fbe47-120">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="fbe47-121">任意のテキスト エディターまたは IDE を取得します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-121">Get any text editor or IDE.</span></span> <span data-ttu-id="fbe47-122">無料でインストール[して使用Visual Studio Code](https://code.visualstudio.com/download)できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-122">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="fbe47-123">インストール中に、追加、および PATH のオプションが表示される場合は `git` `node` `npm` `code` 、オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-123">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, select the options.</span></span> 

<span data-ttu-id="fbe47-124">ターミナル ウィンドウで次のコマンドを実行して、ツールが使用可能な状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-124">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="fbe47-125">プラットフォームで最も快適なターミナル ウィンドウを使用します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-125">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="fbe47-126">これらの例では Bash (Git に含まれています) を使用しますが、これらのスクリプトはほとんどのプラットフォームで実行されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-126">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

<span data-ttu-id="fbe47-127">これらのアプリケーションのバージョンが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-127">You may have a different version of these applications.</span></span> <span data-ttu-id="fbe47-128">gulp を除き、これは問題ではありません。</span><span class="sxs-lookup"><span data-stu-id="fbe47-128">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="fbe47-129">gulp の場合は、バージョン 4.0.0 以降を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-129">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="fbe47-130">gulp がインストールされていない (または正しいバージョンがインストールされている) 場合は、ターミナル ウィンドウで `npm install gulp` 実行します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-130">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="fbe47-131">インストール済みファイルをVisual Studio Code、次のコマンドを実行してインストールを確認できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-131">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="fbe47-132">このターミナル ウィンドウを引き続き使用して、このチュートリアルに従うコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-132">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="fbe47-133">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="fbe47-133">Download the sample</span></span>

<span data-ttu-id="fbe47-134">シンプルな Hello, [World を提供しました。](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span><span class="sxs-lookup"><span data-stu-id="fbe47-134">We have provided a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span></span> <span data-ttu-id="fbe47-135">サンプルを使用して開始します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-135">sample to get you started.</span></span> <span data-ttu-id="fbe47-136">ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-136">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="fbe47-137">このレ[ポを](https://help.github.com/articles/fork-a-repo/)フォーク[すると](https://github.com/OfficeDev/Microsoft-Teams-Samples)、将来の参照のために変更を加え、GitHubを確認できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-137">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="fbe47-138">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="fbe47-138">Build and run the sample</span></span>

<span data-ttu-id="fbe47-139">リポジトリが複製された後、ターミナルでディレクトリの変更コマンドを実行して、ディレクトリをサンプルに変更します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-139">After the repository is cloned, run the change directory command in terminal to change the directory to the sample:</span></span>

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

<span data-ttu-id="fbe47-140">サンプルをビルドするには、すべての依存関係をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-140">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="fbe47-141">これを行うには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-141">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="fbe47-142">多くの依存関係がインストールされているのが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-142">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="fbe47-143">インストール後、次のコマンドを使用してアプリを実行できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-143">After installation you can run the app with the following command:</span></span>

```bash
npm start
```

<span data-ttu-id="fbe47-144">hello-world アプリが起動すると、ターミナル `App started listening on port 3333` ウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-144">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="fbe47-145">上記のメッセージに別のポート番号が表示される場合は、PORT 環境変数が設定されているためです。</span><span class="sxs-lookup"><span data-stu-id="fbe47-145">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="fbe47-146">引き続きそのポートを使用するか、環境変数を 3333 に変更できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-146">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="fbe47-147">この時点で、ブラウザー ウィンドウを開き、次の URL に移動して、すべてのアプリ URL が読み込まれるか確認できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-147">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

## <a name="deploy-your-sample-app"></a><span data-ttu-id="fbe47-148">サンプル アプリの展開</span><span class="sxs-lookup"><span data-stu-id="fbe47-148">Deploy your sample app</span></span>

<span data-ttu-id="fbe47-149">アプリケーション内のアプリMicrosoft Teams 1 つ以上の機能を公開する Web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="fbe47-149">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="fbe47-150">アプリをTeamsするには、アプリにインターネットからアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-150">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="fbe47-151">インターネットからアプリにアクセスするには、アプリを *ホストする* 必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-151">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="fbe47-152">ローカル テストでは、ローカル コンピューターでアプリを実行し、Web エンドポイントを使用してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-152">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="fbe47-153">[ngrok](https://ngrok.com) は無料のツールで、それを実行できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-153">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="fbe47-154">*ngrok を使用* すると、次のような Web アドレスを取得できます `https://d0ac14a5.ngrok.io` (この URL は単なる例です)。</span><span class="sxs-lookup"><span data-stu-id="fbe47-154">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="fbe47-155">環境に [合った](https://ngrok.com/download) *ngrok をダウンロード* してインストールできます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-155">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="fbe47-156">必ず、このファイルを自分の場所に追加してください `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="fbe47-156">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="fbe47-157">インストール後、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-157">After you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="fbe47-158">このサンプルではポート 3333 を使用します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-158">The sample uses port 3333, so be sure to specify it here:</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="fbe47-159">*Ngrok は* インターネットからの要求をリッスンし、ポート 3333 で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="fbe47-159">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="fbe47-160">ブラウザーを開き、アプリの hello ページを読み込 `https://d0ac14a5.ngrok.io/hello` む方法で確認できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-160">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="fbe47-161">この URL ではなく、コンソール セッションで *ngrok* によって表示される転送アドレスを必ず使用してください。</span><span class="sxs-lookup"><span data-stu-id="fbe47-161">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="fbe47-162">上記のビルドと実行手順で別の [](#build-and-run-the-sample)ポートを使用している場合は、同じポート番号を使用して *ngrok トンネルをセットアップ* してください。</span><span class="sxs-lookup"><span data-stu-id="fbe47-162">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="fbe47-163">別のターミナル ウィンドウで *ngrok* を実行して、後で停止、再構築、再実行が必要になるノード アプリを妨げることなく実行し続けるのをお考えください。</span><span class="sxs-lookup"><span data-stu-id="fbe47-163">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="fbe47-164">*ngrok セッションは*、このウィンドウで有用なデバッグ情報を返します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-164">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="fbe47-165">永続的な名前を許可する *有料バージョンの ngrok* があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-165">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="fbe47-166">無料版を使用する場合、アプリは開発マシンの現在のセッション中にのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-166">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="fbe47-167">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="fbe47-167">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="fbe47-168">他のユーザーがテスト用にアプリを共有する場合は、このことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="fbe47-168">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="fbe47-169">サービスを再起動する必要がある場合は、新しいアドレスが返され、そのアドレスを使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-169">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="fbe47-170">アプリの URL をメモします。</span><span class="sxs-lookup"><span data-stu-id="fbe47-170">Make a note of the URL of your app.</span></span> <span data-ttu-id="fbe47-171">アプリをアプリ スタジオまたは開発者ポータルを使用してアプリをTeams後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-171">You will need this later when you register the app with Teams using App studio or Developer Portal.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="fbe47-172">アプリをアプリに展開Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fbe47-172">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="fbe47-173">この時点で、アプリはインターネット上でホストされますが、Teams に検索場所やアプリの呼び出しを伝える方法はまだありません。</span><span class="sxs-lookup"><span data-stu-id="fbe47-173">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="fbe47-174">これを行うには、アプリ パッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-174">To do this you now have to create an app package.</span></span> <span data-ttu-id="fbe47-175">これは、アプリ マニフェストと、Teams クライアントがアプリを適切に表示およびブランド化するために使用するアイコンを含むテキスト ファイルにすら及びしません。</span><span class="sxs-lookup"><span data-stu-id="fbe47-175">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="fbe47-176">このアプリ パッケージを手動で作成するか、Teams で実行する App Studio または Developer Portal ツールを使用すると、アプリの登録プロセスが簡略化されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-176">You can manually create this app package, or you can use App Studio or Developer Portal, tools that run in Teams, that will simplify the process of registering the app.</span></span> <span data-ttu-id="fbe47-177">App Studio と Developer Portal は、アプリ パッケージを作成および更新するための推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="fbe47-177">App Studio and Developer Portal are the recommended ways of creating and updating the app package.</span></span>

<span data-ttu-id="fbe47-178">どちらの方法でも、次の値が必要です。</span><span class="sxs-lookup"><span data-stu-id="fbe47-178">For either method you will need the following:</span></span>

- <span data-ttu-id="fbe47-179">アプリがインターネット上で見つかる URL。</span><span class="sxs-lookup"><span data-stu-id="fbe47-179">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="fbe47-180">アプリのTeamsに使用するアイコン。</span><span class="sxs-lookup"><span data-stu-id="fbe47-180">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="fbe47-181">サンプルには、"src\static\images" にあるプレースホルダー アイコンが付属しています。</span><span class="sxs-lookup"><span data-stu-id="fbe47-181">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="fbe47-182">App Studio では、必要に応じて既定のアイコンも表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-182">App Studio also will provide default icons if needed.</span></span>

<span data-ttu-id="fbe47-183">**アプリ パッケージを更新する**</span><span class="sxs-lookup"><span data-stu-id="fbe47-183">**Update the app package**</span></span>

# <a name="app-studio"></a>[<span data-ttu-id="fbe47-184">App Studio</span><span class="sxs-lookup"><span data-stu-id="fbe47-184">App Studio</span></span>](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[<span data-ttu-id="fbe47-185">開発者ポータル</span><span class="sxs-lookup"><span data-stu-id="fbe47-185">Developer Portal</span></span>](#tab/DP)

<span data-ttu-id="fbe47-186">**開発者ポータル (プレビュー) をインストールするには、Teams**</span><span class="sxs-lookup"><span data-stu-id="fbe47-186">**To install Developer Portal (preview) in Teams**</span></span>

1. <span data-ttu-id="fbe47-187">左側の **バーの** 下部にある [アプリ] アイコンを選択し、[開発者ポータル] **を検索します**。</span><span class="sxs-lookup"><span data-stu-id="fbe47-187">Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.</span></span>

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. <span data-ttu-id="fbe47-188">[開発者 **ポータル] を選択し** 、[開く] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="fbe47-188">Select **Developer Portal** and select **Open**.</span></span>

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. <span data-ttu-id="fbe47-189">[アプリ] タブを選択し、[ **既存のアプリのインポート] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="fbe47-189">Select the Apps tab and select **Import an existing app**.</span></span>

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. <span data-ttu-id="fbe47-190">[Hello **World] を選択し** 、[インポート] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="fbe47-190">Select **Hello World** and select **Import**.</span></span> <span data-ttu-id="fbe47-191">**Hello World アプリ** は開発者ポータルにインポートされます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-191">The **Hello World** app is imported in Developer Portal.</span></span> 

    <span data-ttu-id="fbe47-192">開発者ポータルを使用してアプリTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-192">You can configure your app using the Teams Developer Portal.</span></span> <span data-ttu-id="fbe47-193">マニフェストは [配布] の下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-193">The Manifest is found under Distribute.</span></span> <span data-ttu-id="fbe47-194">マニフェストを使用して、アプリの機能、必要なリソース、その他の重要な属性を構成できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-194">You can use the Manifest to configure capabilities, required resources, and other important attributes for your app.</span></span> <span data-ttu-id="fbe47-195">開発者ポータルを使用してアプリを構成する方法の詳細については、「開発者ポータル」[を参照Teamsしてください](../concepts/build-and-test/teams-developer-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fbe47-195">For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span></span>

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>

---
<a name="updatecredentials"></a>

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="fbe47-196">ホストされたアプリの資格情報を更新する</span><span class="sxs-lookup"><span data-stu-id="fbe47-196">Update the credentials for your hosted app</span></span>

<span data-ttu-id="fbe47-197">サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-197">The sample app requires the following environment variables to be set to the values you made a note of earlier:</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="fbe47-198">その方法は、アプリのホスト方法によって異なります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-198">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="fbe47-199">環境変数を使用する重要な点は、これらの値は環境の一部であり、アプリのコードからアクセスできますが、サイトを構成するファイルを調べるサードパーティには公開されません。</span><span class="sxs-lookup"><span data-stu-id="fbe47-199">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="fbe47-200">ngrok を使用してアプリを実行している場合は、いくつかのローカル環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-200">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="fbe47-201">これを行うには多くの方法がありますが、最も簡単な方法は、Visual Studio Code起動構成を[追加する方法です](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)。</span><span class="sxs-lookup"><span data-stu-id="fbe47-201">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

<span data-ttu-id="fbe47-202">ここで、</span><span class="sxs-lookup"><span data-stu-id="fbe47-202">Where:</span></span>

<span data-ttu-id="fbe47-203">MICROSOFT_APP_IDとMICROSOFT_APP_PASSWORDは、ボットの ID とパスワードです。</span><span class="sxs-lookup"><span data-stu-id="fbe47-203">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="fbe47-204">NODE_DEBUGデバッグ コンソールでボットで何が起こっているかVisual Studio Code表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-204">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="fbe47-205">NODE_CONFIG_DIRリポジトリのルートにあるディレクトリをポイントします (既定では、アプリをローカルで実行すると、src フォルダーで検索されます)。</span><span class="sxs-lookup"><span data-stu-id="fbe47-205">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="fbe47-206">チュートリアルの前のバージョンから npm を停止していない場合は、起動構成変数を正しく取得Visual Studio Code実行 `npm stop` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-206">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="fbe47-207">[アプリ] タブの構成</span><span class="sxs-lookup"><span data-stu-id="fbe47-207">Configure the app tab</span></span>

<span data-ttu-id="fbe47-208">アプリをチームにインストールした後、コンテンツを表示するためにアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbe47-208">After you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="fbe47-209">チーム内のチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。次に、[タブ `Hello World` の追加 **] リストから選択** できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-209">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="fbe47-210">その後、構成ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-210">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="fbe47-211">このダイアログでは、このチャネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-211">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="fbe47-212">タブを選択して [保存] を **クリック** すると、選択したタブが読 `Hello World` み込まれたタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-212">After you select the tab and click **Save** you can see the `Hello World` tab loaded with the tab you chose:</span></span>

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="fbe47-213">ボットをテストTeams</span><span class="sxs-lookup"><span data-stu-id="fbe47-213">Test your bot in Teams</span></span>

<span data-ttu-id="fbe47-214">これで、ボットと対話できます。Teams。</span><span class="sxs-lookup"><span data-stu-id="fbe47-214">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="fbe47-215">アプリを登録したチーム内のチャネルを選択し、「」と入力し `@your-bot-name` 、その後にメッセージを入力します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-215">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="fbe47-216">これはメンションと呼 **\@ ばれる.**</span><span class="sxs-lookup"><span data-stu-id="fbe47-216">This is called an **\@mention**.</span></span> <span data-ttu-id="fbe47-217">ボットに送信するメッセージは、返信として返されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-217">Whatever message you send to the bot will be sent back to you as a reply:</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="fbe47-218">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="fbe47-218">Test your messaging extension</span></span>

<span data-ttu-id="fbe47-219">**メッセージング拡張機能をテストするには**</span><span class="sxs-lookup"><span data-stu-id="fbe47-219">**To test your messaging extension**</span></span>
1. <span data-ttu-id="fbe47-220">会話ビューの入力ボックスの下にある 3 つのドットを選択します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-220">Select the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="fbe47-221">「Hello **World」アプリを含むメニュー** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-221">A menu with the **'Hello World'** app is displayed.</span></span>
1. <span data-ttu-id="fbe47-222">メニューを選択します。</span><span class="sxs-lookup"><span data-stu-id="fbe47-222">Select the menu.</span></span> <span data-ttu-id="fbe47-223">ランダムなテキストのセットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-223">A set of random texts is displayed.</span></span> <span data-ttu-id="fbe47-224">ランダムなテキストの 1 つを選択し、会話に挿入できます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-224">You can select one of the random text and that is inserted into your conversation.</span></span>

    <img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. <span data-ttu-id="fbe47-225">ランダムなテキストのいずれかを選択すると、カードがフォーマットされ、下部に独自のメッセージを送信する準備ができているのが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbe47-225">Select one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom:</span></span>

    <img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

 ## <a name="see-also"></a><span data-ttu-id="fbe47-226">関連項目</span><span class="sxs-lookup"><span data-stu-id="fbe47-226">See also</span></span>

* [<span data-ttu-id="fbe47-227">チュートリアルの概要</span><span class="sxs-lookup"><span data-stu-id="fbe47-227">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="fbe47-228">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="fbe47-228">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="fbe47-229">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="fbe47-229">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="fbe47-230">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="fbe47-230">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)