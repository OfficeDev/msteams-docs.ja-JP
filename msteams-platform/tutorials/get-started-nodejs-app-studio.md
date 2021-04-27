---
title: チュートリアル - アプリを使用して最初のアプリをNode.js
description: Microsoft Teams アプリの作成を開始する方法については、Node.js。
keywords: nodejs App Studio node.jsの開始方法
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: ae1b8b2b5b671488ff6f86a3a3295f448ebb6006
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020962"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="3866d-104">ユーザー設定を使用して最初の Microsoft Teams アプリをNode.js</span><span class="sxs-lookup"><span data-stu-id="3866d-104">Create your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="3866d-105">このチュートリアルでは、アプリを使用して Microsoft Teams アプリの作成を開始Node.js。</span><span class="sxs-lookup"><span data-stu-id="3866d-105">This tutorial helps you get started creating a Microsoft Teams app using Node.js.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="3866d-106">アプリをダウンロードしてホストする</span><span class="sxs-lookup"><span data-stu-id="3866d-106">Download and host your app</span></span>

<span data-ttu-id="3866d-107">Teams で簡単な "hello world" アプリをダウンロードしてホストするには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="3866d-107">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="3866d-108">前提条件の取得</span><span class="sxs-lookup"><span data-stu-id="3866d-108">Get prerequisites</span></span>

<span data-ttu-id="3866d-109">このチュートリアルを完了するには、次のツールが必要です。</span><span class="sxs-lookup"><span data-stu-id="3866d-109">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="3866d-110">まだインストールしていない場合は、これらのリンクからインストールできます。</span><span class="sxs-lookup"><span data-stu-id="3866d-110">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="3866d-111">Git</span><span class="sxs-lookup"><span data-stu-id="3866d-111">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="3866d-112">Node.js NPM</span><span class="sxs-lookup"><span data-stu-id="3866d-112">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="3866d-113">任意のテキスト エディターまたは IDE を取得します。</span><span class="sxs-lookup"><span data-stu-id="3866d-113">Get any text editor or IDE.</span></span> <span data-ttu-id="3866d-114">コードを無料でインストール [Visual Studio使用](https://code.visualstudio.com/download) できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-114">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="3866d-115">インストール中に、追加、および PATH のオプションが表示される場合は `git` `node` `npm` `code` 、そのオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="3866d-115">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="3866d-116">便利です。</span><span class="sxs-lookup"><span data-stu-id="3866d-116">It will be handy.</span></span>

<span data-ttu-id="3866d-117">ターミナル ウィンドウで次のコマンドを実行して、ツールが使用可能な状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="3866d-117">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="3866d-118">プラットフォームで最も快適なターミナル ウィンドウを使用します。</span><span class="sxs-lookup"><span data-stu-id="3866d-118">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="3866d-119">これらの例では Bash (Git に含まれています) を使用しますが、これらのスクリプトはほとんどのプラットフォームで実行されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-119">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

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

<span data-ttu-id="3866d-120">これらのアプリケーションのバージョンが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-120">You may have a different version of these applications.</span></span> <span data-ttu-id="3866d-121">gulp を除き、これは問題ではありません。</span><span class="sxs-lookup"><span data-stu-id="3866d-121">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="3866d-122">gulp の場合は、バージョン 4.0.0 以降を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-122">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="3866d-123">gulp がインストールされていない (または正しいバージョンがインストールされている) 場合は、ターミナル ウィンドウで `npm install gulp` 実行します。</span><span class="sxs-lookup"><span data-stu-id="3866d-123">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="3866d-124">コードをインストールしたVisual Studio、次のコマンドを実行してインストールを確認できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-124">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="3866d-125">このターミナル ウィンドウを引き続き使用して、このチュートリアルに従うコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-125">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="3866d-126">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="3866d-126">Download the sample</span></span>

<span data-ttu-id="3866d-127">シンプルな Hello, [World を提供しました。](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span><span class="sxs-lookup"><span data-stu-id="3866d-127">We have provided a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span></span> <span data-ttu-id="3866d-128">サンプルを使用して開始します。</span><span class="sxs-lookup"><span data-stu-id="3866d-128">sample to get you started.</span></span> <span data-ttu-id="3866d-129">ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="3866d-129">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="3866d-130">今後の [参照のために](https://help.github.com/articles/fork-a-repo/) [GitHub](https://github.com/OfficeDev/Microsoft-Teams-Samples) リポジトリへの変更を変更してチェックインする場合は、このリポジトリをフォークできます。</span><span class="sxs-lookup"><span data-stu-id="3866d-130">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="3866d-131">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="3866d-131">Build and run the sample</span></span>

<span data-ttu-id="3866d-132">リポジトリが複製された後、サンプルを保持するディレクトリに変更します。</span><span class="sxs-lookup"><span data-stu-id="3866d-132">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

<span data-ttu-id="3866d-133">サンプルをビルドするには、すべての依存関係をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-133">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="3866d-134">これを行うには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="3866d-134">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="3866d-135">多くの依存関係がインストールされているのが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-135">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="3866d-136">完了したら、アプリを実行できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-136">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="3866d-137">hello-world アプリが起動すると、ターミナル `App started listening on port 3333` ウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-137">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="3866d-138">上記のメッセージに別のポート番号が表示される場合は、PORT 環境変数が設定されているためです。</span><span class="sxs-lookup"><span data-stu-id="3866d-138">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="3866d-139">引き続きそのポートを使用するか、環境変数を 3333 に変更できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-139">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="3866d-140">この時点で、ブラウザー ウィンドウを開き、次の URL に移動して、すべてのアプリ URL が読み込まれるか確認できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-140">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="3866d-141">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="3866d-141">Host the sample app</span></span>

<span data-ttu-id="3866d-142">Microsoft Teams のアプリは、1 つ以上の機能を公開する Web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="3866d-142">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="3866d-143">Teams プラットフォームでアプリを読み込むには、アプリにインターネットからアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-143">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="3866d-144">インターネットからアプリにアクセスするには、アプリを *ホストする* 必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-144">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="3866d-145">ローカル テストでは、ローカル コンピューターでアプリを実行し、Web エンドポイントを使用してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-145">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="3866d-146">[ngrok](https://ngrok.com) は無料のツールで、それを実行できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-146">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="3866d-147">*ngrok を使用* すると、次のような Web アドレスを取得できます `https://d0ac14a5.ngrok.io` (この URL は単なる例です)。</span><span class="sxs-lookup"><span data-stu-id="3866d-147">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="3866d-148">環境に [合った](https://ngrok.com/download) *ngrok をダウンロード* してインストールできます。</span><span class="sxs-lookup"><span data-stu-id="3866d-148">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="3866d-149">必ず、このファイルを自分の場所に追加してください `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="3866d-149">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="3866d-150">インストールしたら、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-150">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="3866d-151">このサンプルではポート 3333 を使用します。</span><span class="sxs-lookup"><span data-stu-id="3866d-151">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="3866d-152">*Ngrok は* インターネットからの要求をリッスンし、ポート 3333 で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="3866d-152">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="3866d-153">ブラウザーを開き、アプリの hello ページを読み込 `https://d0ac14a5.ngrok.io/hello` む方法で確認できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-153">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="3866d-154">この URL ではなく、コンソール セッションで *ngrok* によって表示される転送アドレスを必ず使用してください。</span><span class="sxs-lookup"><span data-stu-id="3866d-154">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="3866d-155">上記のビルドと実行手順で別の [](#build-and-run-the-sample)ポートを使用している場合は、同じポート番号を使用して *ngrok トンネルをセットアップ* してください。</span><span class="sxs-lookup"><span data-stu-id="3866d-155">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="3866d-156">別のターミナル ウィンドウで *ngrok* を実行して、後で停止、再構築、再実行が必要になるノード アプリを妨げることなく実行し続けるのをお考えください。</span><span class="sxs-lookup"><span data-stu-id="3866d-156">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="3866d-157">*ngrok セッションは*、このウィンドウで有用なデバッグ情報を返します。</span><span class="sxs-lookup"><span data-stu-id="3866d-157">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="3866d-158">永続的な名前を許可する *有料バージョンの ngrok* があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-158">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="3866d-159">無料版を使用する場合、アプリは開発マシンの現在のセッション中にのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-159">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="3866d-160">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="3866d-160">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="3866d-161">他のユーザーがテスト用にアプリを共有する場合は、このことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="3866d-161">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="3866d-162">サービスを再起動する必要がある場合は、新しいアドレスが返され、そのアドレスを使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-162">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="3866d-163">アプリを Teams に登録するときに後で必要になるアプリの URL をメモしてください。</span><span class="sxs-lookup"><span data-stu-id="3866d-163">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="3866d-164">メモ帳は、この目的のために正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="3866d-164">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="3866d-165">アプリを Microsoft Teams に展開する</span><span class="sxs-lookup"><span data-stu-id="3866d-165">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="3866d-166">この時点で、アプリはインターネット上でホストされますが、検索場所やアプリの呼び出し先を Teams にまだ伝える方法はありません。</span><span class="sxs-lookup"><span data-stu-id="3866d-166">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="3866d-167">これを行うには、アプリ パッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-167">To do this you now have to create an app package.</span></span> <span data-ttu-id="3866d-168">これは、アプリ マニフェストと、Teams クライアントがアプリを適切に表示およびブランド化するために使用するアイコンを含むテキスト ファイルにすら及びしません。</span><span class="sxs-lookup"><span data-stu-id="3866d-168">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="3866d-169">このアプリ パッケージを手動で作成するか、アプリの登録プロセスを簡略化する Teams で実行されるツールである App Studio を使用できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-169">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="3866d-170">App Studio は、アプリ パッケージを作成および更新する推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="3866d-170">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="3866d-171">どちらの方法でも、次の値が必要です。</span><span class="sxs-lookup"><span data-stu-id="3866d-171">For either method you will need the following:</span></span>

- <span data-ttu-id="3866d-172">アプリがインターネット上で見つかる URL。</span><span class="sxs-lookup"><span data-stu-id="3866d-172">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="3866d-173">Teams がアプリのブランド化に使用するアイコン。</span><span class="sxs-lookup"><span data-stu-id="3866d-173">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="3866d-174">サンプルには、"src\static\images" にあるプレースホルダー アイコンが付属しています。</span><span class="sxs-lookup"><span data-stu-id="3866d-174">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="3866d-175">App Studio では、必要に応じて既定のアイコンも表示されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-175">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="3866d-176">ホストされたアプリを更新する</span><span class="sxs-lookup"><span data-stu-id="3866d-176">Update your hosted app</span></span>

<span data-ttu-id="3866d-177">サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-177">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="3866d-178">その方法は、アプリのホスト方法によって異なります。</span><span class="sxs-lookup"><span data-stu-id="3866d-178">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="3866d-179">環境変数を使用する重要な点は、これらの値は環境の一部であり、アプリのコードからアクセスできますが、サイトを構成するファイルを調べるサードパーティには公開されません。</span><span class="sxs-lookup"><span data-stu-id="3866d-179">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="3866d-180">ngrok を使用してアプリを実行している場合は、いくつかのローカル環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-180">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="3866d-181">これを行うには多くの方法がありますが、コードを使用している場合は、Visual Studio起動構成を [追加するのが最も簡単です](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)。</span><span class="sxs-lookup"><span data-stu-id="3866d-181">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="3866d-182">ここで、</span><span class="sxs-lookup"><span data-stu-id="3866d-182">Where:</span></span>

<span data-ttu-id="3866d-183">MICROSOFT_APP_IDとMICROSOFT_APP_PASSWORDは、ボットの ID とパスワードです。</span><span class="sxs-lookup"><span data-stu-id="3866d-183">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="3866d-184">NODE_DEBUGコード デバッグ コンソールでボットで何が起こっているかVisual Studio表示されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-184">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="3866d-185">NODE_CONFIG_DIRリポジトリのルートにあるディレクトリをポイントします (既定では、アプリをローカルで実行すると、src フォルダーで検索されます)。</span><span class="sxs-lookup"><span data-stu-id="3866d-185">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="3866d-186">チュートリアルの前のバージョンから npm を停止していない場合は、Visual Studio コードで起動構成変数を正しく取得するために実行する `npm stop` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-186">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="3866d-187">[アプリ] タブの構成</span><span class="sxs-lookup"><span data-stu-id="3866d-187">Configure the app tab</span></span>

<span data-ttu-id="3866d-188">アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3866d-188">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="3866d-189">チーム内のチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。次に、[タブ `Hello World` の追加 **] リストから選択** できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-189">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="3866d-190">その後、構成ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-190">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="3866d-191">このダイアログでは、このチャネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-191">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="3866d-192">タブを選択してクリックすると `Save` 、選択したタブが読 `Hello World` み込まれたタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-192">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="3866d-193">Teams でボットをテストする</span><span class="sxs-lookup"><span data-stu-id="3866d-193">Test your bot in Teams</span></span>

<span data-ttu-id="3866d-194">Teams でボットを操作できます。</span><span class="sxs-lookup"><span data-stu-id="3866d-194">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="3866d-195">アプリを登録したチーム内のチャネルを選択し、「」と入力し `@your-bot-name` 、その後にメッセージを入力します。</span><span class="sxs-lookup"><span data-stu-id="3866d-195">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="3866d-196">これはメンションと呼 **\@ ばれる.**</span><span class="sxs-lookup"><span data-stu-id="3866d-196">This is called an **\@mention**.</span></span> <span data-ttu-id="3866d-197">ボットに送信したメッセージは、返信として返されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-197">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="3866d-198">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="3866d-198">Test your messaging extension</span></span>

<span data-ttu-id="3866d-199">メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。</span><span class="sxs-lookup"><span data-stu-id="3866d-199">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="3866d-200">メニューに「Hello **World」アプリが** 表示されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-200">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="3866d-201">クリックすると、ランダムなテキストが多数表示されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-201">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="3866d-202">任意の 1 つを選択すると、会話に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="3866d-202">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="3866d-203">ランダムなテキストのいずれかを選択すると、カードが書式設定され、下部に独自のメッセージを送信する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="3866d-203">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
