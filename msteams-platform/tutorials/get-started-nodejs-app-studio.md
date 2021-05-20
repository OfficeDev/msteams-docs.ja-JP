---
title: チュートリアル - Node.jsを使用して最初のアプリを作成する
description: Node.jsを使用してMicrosoft Teamsアプリの構築を開始する方法について説明します。
keywords: nodejs アプリケーションスタジオnode.js始める
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 46272671443e07432513b667af424b5c5be05f2e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566542"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="729ff-104">Node.jsを使用して初めてのMicrosoft Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="729ff-104">Create your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="729ff-105">このチュートリアルでは、Node.jsを使用してMicrosoft Teams アプリの作成を開始できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-105">This tutorial helps you get started creating a Microsoft Teams app using Node.js.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="729ff-106">アプリをダウンロードしてホストする</span><span class="sxs-lookup"><span data-stu-id="729ff-106">Download and host your app</span></span>

<span data-ttu-id="729ff-107">Teamsでシンプルな「hello world」アプリをダウンロードしてホストするには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="729ff-107">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="729ff-108">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="729ff-108">Get prerequisites</span></span>

<span data-ttu-id="729ff-109">このチュートリアルを完了するには、次のツールが必要です。</span><span class="sxs-lookup"><span data-stu-id="729ff-109">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="729ff-110">まだお持ちの場合は、これらのリンクからインストールできます。</span><span class="sxs-lookup"><span data-stu-id="729ff-110">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="729ff-111">Git</span><span class="sxs-lookup"><span data-stu-id="729ff-111">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="729ff-112">Node.jsと NPM</span><span class="sxs-lookup"><span data-stu-id="729ff-112">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="729ff-113">任意のテキスト エディタまたは IDE を取得します。</span><span class="sxs-lookup"><span data-stu-id="729ff-113">Get any text editor or IDE.</span></span> <span data-ttu-id="729ff-114">[Visual Studio Code](https://code.visualstudio.com/download)を無料でインストールして使用できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-114">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="729ff-115">インストール時に 、 `git` 、 、 のインストール時に PATH に追加するオプションが表示された場合 `node` `npm` `code` は、このオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="729ff-115">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="729ff-116">それは便利になります。</span><span class="sxs-lookup"><span data-stu-id="729ff-116">It will be handy.</span></span>

<span data-ttu-id="729ff-117">ターミナル ウィンドウで次のツールを実行して、ツールが使用可能であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="729ff-117">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="729ff-118">プラットフォーム上で最も快適なターミナルウィンドウを使用します。</span><span class="sxs-lookup"><span data-stu-id="729ff-118">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="729ff-119">これらの例では Bash (Git に含まれています) を使用していますが、これらのスクリプトはほとんどのプラットフォームで実行されます。</span><span class="sxs-lookup"><span data-stu-id="729ff-119">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

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

<span data-ttu-id="729ff-120">これらのアプリケーションのバージョンが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-120">You may have a different version of these applications.</span></span> <span data-ttu-id="729ff-121">これは、gulp を除いて問題となるべきではありません。</span><span class="sxs-lookup"><span data-stu-id="729ff-121">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="729ff-122">gulp の場合は、バージョン 4.0.0 以降を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-122">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="729ff-123">gulp がインストールされていない場合(または間違ったバージョンがインストールされている場合)は、 `npm install gulp` ターミナルウィンドウで実行して実行してください。</span><span class="sxs-lookup"><span data-stu-id="729ff-123">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="729ff-124">Visual Studio Codeをインストールした場合は、次の手順を実行してインストールを確認できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-124">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="729ff-125">このターミナル ウィンドウを引き続き使用して、このチュートリアルのコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-125">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="729ff-126">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="729ff-126">Download the sample</span></span>

<span data-ttu-id="729ff-127">私たちは、シンプルな [こんにちは、世界を提供しています!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span><span class="sxs-lookup"><span data-stu-id="729ff-127">We have provided a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span></span> <span data-ttu-id="729ff-128">サンプルを使用して開始します。</span><span class="sxs-lookup"><span data-stu-id="729ff-128">sample to get you started.</span></span> <span data-ttu-id="729ff-129">ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル マシンに複製します。</span><span class="sxs-lookup"><span data-stu-id="729ff-129">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="729ff-130">今後の参照のために、GitHub[レポ](https://github.com/OfficeDev/Microsoft-Teams-Samples)への変更を変更してチェックインする場合は、このレポを[フォーク](https://help.github.com/articles/fork-a-repo/)できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-130">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="729ff-131">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="729ff-131">Build and run the sample</span></span>

<span data-ttu-id="729ff-132">リポジトリのクローンが作成されたら、サンプルを保持しているディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="729ff-132">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

<span data-ttu-id="729ff-133">サンプルをビルドするには、すべての依存関係をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-133">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="729ff-134">これを行うには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="729ff-134">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="729ff-135">インストールされる依存関係の一群が表示されます。</span><span class="sxs-lookup"><span data-stu-id="729ff-135">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="729ff-136">完了したら、アプリを実行できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-136">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="729ff-137">hello-world アプリが起動すると、 `App started listening on port 3333` ターミナル ウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="729ff-137">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="729ff-138">上記のメッセージに異なるポート番号が表示される場合は、PORT 環境変数が設定されているためです。</span><span class="sxs-lookup"><span data-stu-id="729ff-138">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="729ff-139">そのポートを引き続き使用するか、または環境変数を 3333 に変更できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-139">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="729ff-140">この時点で、ブラウザー ウィンドウを開き、次の URL に移動して、すべてのアプリ URL が読み込まれているかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-140">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="729ff-141">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="729ff-141">Host the sample app</span></span>

<span data-ttu-id="729ff-142">Microsoft Teamsのアプリは、1 つ以上の機能を公開する Web アプリケーションであることを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="729ff-142">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="729ff-143">アプリを読み込むTeamsプラットフォームでは、インターネットからアプリにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-143">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="729ff-144">インターネットからアプリにアクセスできるようにするには、アプリを *ホスト* する必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-144">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="729ff-145">ローカル テストの場合は、ローカル コンピューターでアプリを実行し、Web エンドポイントを使用してアプリへのトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-145">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="729ff-146">[ngrok](https://ngrok.com) は、あなたがそれを行うことができます無料のツールです。</span><span class="sxs-lookup"><span data-stu-id="729ff-146">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="729ff-147">*ngrok* を使用すると、( `https://d0ac14a5.ngrok.io` このURLは単なる例です)などのウェブアドレスを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="729ff-147">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="729ff-148">ご使用の環境に *合わせて ngrok* を [ダウンロードしてインストール](https://ngrok.com/download)できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-148">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="729ff-149">で、必ず その場所に追加してください `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="729ff-149">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="729ff-150">インストール後、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-150">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="729ff-151">サンプルではポート 3333 を使用するため、ここで指定してください。</span><span class="sxs-lookup"><span data-stu-id="729ff-151">The sample uses port 3333, so be sure to specify it here:</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="729ff-152">*Ngrok* はインターネットからのリクエストを聞き、ポート3333で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="729ff-152">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="729ff-153">ブラウザーを開いて `https://d0ac14a5.ngrok.io/hello` 、アプリの hello ページを読み込むことで確認できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-153">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="729ff-154">この URL ではなく、コンソール セッションで *ngrok* で表示される転送先アドレスを使用してください。</span><span class="sxs-lookup"><span data-stu-id="729ff-154">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="729ff-155">上記の [ビルドと実行](#build-and-run-the-sample) 手順で別のポートを使用している場合は *、ngrok* トンネルを設定するために同じポート番号を使用してください。</span><span class="sxs-lookup"><span data-stu-id="729ff-155">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="729ff-156">ngrok を別のターミナル ウィンドウで実行して、後で停止、再構築、再実行する必要があるノード アプリに干渉することなく *、ngrok* を実行し続けることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="729ff-156">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="729ff-157">*ngrok* セッションは、このウィンドウで有益なデバッグ情報を返します。</span><span class="sxs-lookup"><span data-stu-id="729ff-157">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="729ff-158">永続的な名前を許可する *ngrok* の有料版があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-158">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="729ff-159">無料版を使用する場合、アプリは開発マシン上の現在のセッション中にのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-159">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="729ff-160">マシンがシャットダウンされた場合、またはスリープ状態になると、サービスは利用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="729ff-160">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="729ff-161">他のユーザーによるテスト用アプリを共有する場合は、この点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="729ff-161">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="729ff-162">サービスを再起動する必要がある場合は、新しいアドレスを返し、そのアドレスを使用するすべての場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-162">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="729ff-163">アプリスタジオを使用してアプリを登録するときには後で必要になるので、アプリのURL Teams書き留めておいてください。</span><span class="sxs-lookup"><span data-stu-id="729ff-163">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="729ff-164">メモ帳は、この目的のために正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="729ff-164">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="729ff-165">アプリをMicrosoft Teamsに展開する</span><span class="sxs-lookup"><span data-stu-id="729ff-165">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="729ff-166">この時点で、インターネット上でホストされているアプリがありますが、Teamsに探す場所やアプリが呼び出される場所を伝える方法はまだありません。</span><span class="sxs-lookup"><span data-stu-id="729ff-166">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="729ff-167">これを行うには、アプリ パッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-167">To do this you now have to create an app package.</span></span> <span data-ttu-id="729ff-168">これは、アプリ マニフェストと、Teams クライアントがアプリを適切に表示およびブランド化するために使用するアイコンを含むテキスト ファイルに過ぎません。</span><span class="sxs-lookup"><span data-stu-id="729ff-168">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="729ff-169">このアプリ パッケージを手動で作成することも、アプリの登録プロセスを簡略化するTeamsで実行されるツールである App Studio を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="729ff-169">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="729ff-170">アプリの Studio は、アプリ パッケージを作成および更新する推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="729ff-170">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="729ff-171">どちらの方法でも、次のことが必要です。</span><span class="sxs-lookup"><span data-stu-id="729ff-171">For either method you will need the following:</span></span>

- <span data-ttu-id="729ff-172">インターネット上でアプリを見つけることができる URL。</span><span class="sxs-lookup"><span data-stu-id="729ff-172">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="729ff-173">アプリのブランド化に使用Teamsアイコン。</span><span class="sxs-lookup"><span data-stu-id="729ff-173">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="729ff-174">サンプルには、"src\static\images" にあるプレースホルダ アイコンが付属しています。</span><span class="sxs-lookup"><span data-stu-id="729ff-174">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="729ff-175">必要に応じて、アプリスタジオにもデフォルトのアイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="729ff-175">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="729ff-176">ホストされたアプリを更新する</span><span class="sxs-lookup"><span data-stu-id="729ff-176">Update your hosted app</span></span>

<span data-ttu-id="729ff-177">サンプル アプリでは、次の環境変数を、前にメモした値に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-177">The sample app requires the following environment variables to be set to the values you made a note of earlier:</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="729ff-178">アプリのホスト方法によって、その方法が異なります。</span><span class="sxs-lookup"><span data-stu-id="729ff-178">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="729ff-179">環境変数を使用する場合に重要なことは、これらの値が環境の一部であり、アプリのコードでアクセスできますが、サイトを構成するファイルを調べる可能性のあるサードパーティには公開されないことです。</span><span class="sxs-lookup"><span data-stu-id="729ff-179">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="729ff-180">ngrok を使用してアプリを実行している場合は、いくつかのローカル環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-180">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="729ff-181">これを行うには多くの方法がありますが、Visual Studio Codeを使用している場合は、[起動設定](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)を追加するのが最も簡単です。</span><span class="sxs-lookup"><span data-stu-id="729ff-181">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="729ff-182">ここで、</span><span class="sxs-lookup"><span data-stu-id="729ff-182">Where:</span></span>

<span data-ttu-id="729ff-183">MICROSOFT_APP_IDとMICROSOFT_APP_PASSWORDは、それぞれボットの ID とパスワードです。</span><span class="sxs-lookup"><span data-stu-id="729ff-183">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="729ff-184">NODE_DEBUGは、Visual Studio Codeデバッグコンソールでボットで何が起こっているかを示します。</span><span class="sxs-lookup"><span data-stu-id="729ff-184">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="729ff-185">NODE_CONFIG_DIRはリポジトリのルートにあるディレクトリを指します (既定では、アプリがローカルで実行されている場合は、src フォルダー内で検索されます)。</span><span class="sxs-lookup"><span data-stu-id="729ff-185">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="729ff-186">チュートリアルの前半で npm を停止していない場合は `npm stop` 、Visual Studio Code起動設定変数を正しくピックアップするために実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-186">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="729ff-187">アプリ タブを構成する</span><span class="sxs-lookup"><span data-stu-id="729ff-187">Configure the app tab</span></span>

<span data-ttu-id="729ff-188">チームにアプリをインストールしたら、コンテンツを表示するようにアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="729ff-188">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="729ff-189">チーム内のチャンネルに移動し **、'+'** ボタンをクリックして新しいタブを追加します。[ `Hello World` **タブの追加]** リストから選択できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-189">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="729ff-190">その後、構成ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="729ff-190">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="729ff-191">このダイアログでは、このチャンネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-191">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="729ff-192">タブを選択してクリックすると `Save` 、 `Hello World` 選択したタブがロードされたタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="729ff-192">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose:</span></span>

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="729ff-193">Teamsでボットをテストする</span><span class="sxs-lookup"><span data-stu-id="729ff-193">Test your bot in Teams</span></span>

<span data-ttu-id="729ff-194">これで、Teamsでボットと対話できます。</span><span class="sxs-lookup"><span data-stu-id="729ff-194">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="729ff-195">アプリを登録したチームのチャンネルを選択し、「」と入力 `@your-bot-name` し、メッセージを入力します。</span><span class="sxs-lookup"><span data-stu-id="729ff-195">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="729ff-196">これはメンションと呼 **\@ ばれます**。</span><span class="sxs-lookup"><span data-stu-id="729ff-196">This is called an **\@mention**.</span></span> <span data-ttu-id="729ff-197">ボットに送信したメッセージは、返信として返信されます。</span><span class="sxs-lookup"><span data-stu-id="729ff-197">Whatever message you send to the bot will be sent back to you as a reply:</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="729ff-198">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="729ff-198">Test your messaging extension</span></span>

<span data-ttu-id="729ff-199">メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。</span><span class="sxs-lookup"><span data-stu-id="729ff-199">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="729ff-200">メニューには **「ハローワールド」** アプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="729ff-200">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="729ff-201">クリックすると、ランダムなテキストが多数表示されます。</span><span class="sxs-lookup"><span data-stu-id="729ff-201">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="729ff-202">あなたはそれらのいずれかを選択することができ、それはあなたの会話にそれを挿入されます:</span><span class="sxs-lookup"><span data-stu-id="729ff-202">You can choose any one of them and it will be inserted it into your conversation:</span></span>

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="729ff-203">ランダムなテキストのいずれかを選択すると、カードがフォーマットされ、下部に独自のメッセージを送信する準備が整っています。</span><span class="sxs-lookup"><span data-stu-id="729ff-203">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom:</span></span>

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
