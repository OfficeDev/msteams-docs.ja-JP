---
title: チュートリアル - アプリを使用して最初のアプリをNode.js
description: Microsoft Teams アプリの構築を開始する方法について説明Node.js。
keywords: nodejs App Studio node.jsの開始
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 03dcf79a46266321e54c7e99bf01cdd2a87075fa
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037047"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="9c98d-104">アプリを使用して最初の Microsoft Teams アプリをNode.js</span><span class="sxs-lookup"><span data-stu-id="9c98d-104">Create your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="9c98d-105">このチュートリアルでは、Microsoft Teams アプリの作成を開始する際に役立つNode.js。</span><span class="sxs-lookup"><span data-stu-id="9c98d-105">This tutorial helps you get started creating a Microsoft Teams app using Node.js.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="9c98d-106">アプリをダウンロードしてホストする</span><span class="sxs-lookup"><span data-stu-id="9c98d-106">Download and host your app</span></span>

<span data-ttu-id="9c98d-107">次の手順に従って、Teams で簡単な "hello world" アプリをダウンロードしてホストします。</span><span class="sxs-lookup"><span data-stu-id="9c98d-107">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="9c98d-108">前提条件を取得する</span><span class="sxs-lookup"><span data-stu-id="9c98d-108">Get prerequisites</span></span>

<span data-ttu-id="9c98d-109">このチュートリアルを完了するには、次のツールが必要です。</span><span class="sxs-lookup"><span data-stu-id="9c98d-109">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="9c98d-110">まだインストールしていない場合は、これらのリンクからインストールできます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-110">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="9c98d-111">Git</span><span class="sxs-lookup"><span data-stu-id="9c98d-111">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="9c98d-112">Node.js NPM</span><span class="sxs-lookup"><span data-stu-id="9c98d-112">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="9c98d-113">任意のテキスト エディターまたは IDE を取得します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-113">Get any text editor or IDE.</span></span> <span data-ttu-id="9c98d-114">このコードは、無料で [Visual Studioして](https://code.visualstudio.com/download) 使用できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-114">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="9c98d-115">インストール中に PATH を追加するオプションが表示された場合は、追加 `git` `node` `npm` `code` するオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-115">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="9c98d-116">便利です。</span><span class="sxs-lookup"><span data-stu-id="9c98d-116">It will be handy.</span></span>

<span data-ttu-id="9c98d-117">ターミナル ウィンドウで次のコマンドを実行して、ツールが利用可能な状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-117">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="9c98d-118">プラットフォームで最も使いやすいターミナル ウィンドウを使用します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-118">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="9c98d-119">これらの例では Bash (Git に含まれています) を使用していますが、これらのスクリプトはほとんどのプラットフォームで実行されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-119">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

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

<span data-ttu-id="9c98d-120">これらのアプリケーションのバージョンが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-120">You may have a different version of these applications.</span></span> <span data-ttu-id="9c98d-121">gulp を除き、これは問題ではありません。</span><span class="sxs-lookup"><span data-stu-id="9c98d-121">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="9c98d-122">gulp の場合は、バージョン 4.0.0 以降を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-122">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="9c98d-123">gulp がインストールされていない場合 (または正しいバージョンがインストールされていない場合) は、ターミナル ウィンドウで実行して `npm install gulp` 、今すぐインストールします。</span><span class="sxs-lookup"><span data-stu-id="9c98d-123">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="9c98d-124">コードをインストールしたVisual Studio、次のコマンドを実行してインストールを確認できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-124">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="9c98d-125">このターミナル ウィンドウを引き続き使用して、このチュートリアルに従うコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-125">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="9c98d-126">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="9c98d-126">Download the sample</span></span>

<span data-ttu-id="9c98d-127">シンプルな [Hello, World が用意されています。](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span><span class="sxs-lookup"><span data-stu-id="9c98d-127">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span></span> <span data-ttu-id="9c98d-128">サンプルを使用して開始してください。</span><span class="sxs-lookup"><span data-stu-id="9c98d-128">sample to get you started.</span></span> <span data-ttu-id="9c98d-129">ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-129">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> <span data-ttu-id="9c98d-130">今後の[参照のために](https://help.github.com/articles/fork-a-repo/) [](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) GitHub リポジトリの変更を変更してチェックインする場合は、このリポジトリをフォークできます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-130">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="9c98d-131">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="9c98d-131">Build and run the sample</span></span>

<span data-ttu-id="9c98d-132">リポジトリを複製したら、サンプルを保持するディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-132">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd msteams-samples-hello-world-nodejs
```

<span data-ttu-id="9c98d-133">サンプルをビルドするには、すべての依存関係をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-133">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="9c98d-134">これを行うには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-134">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="9c98d-135">一連の依存関係がインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-135">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="9c98d-136">完了したら、アプリを実行できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-136">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="9c98d-137">hello-world アプリが起動すると、ターミナル `App started listening on port 3333` ウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-137">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="9c98d-138">上記のメッセージに別のポート番号が表示される場合は、PORT 環境変数が設定されているためです。</span><span class="sxs-lookup"><span data-stu-id="9c98d-138">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="9c98d-139">引き続きそのポートを使用するか、環境変数を 3333 に変更できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-139">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="9c98d-140">この時点で、ブラウザー ウィンドウを開き、次の URL に移動して、すべてのアプリ URL が読み込み中か確認できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-140">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="9c98d-141">サンプル アプリをホストする</span><span class="sxs-lookup"><span data-stu-id="9c98d-141">Host the sample app</span></span>

<span data-ttu-id="9c98d-142">Microsoft Teams のアプリは、1 つ以上の機能を公開する Web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="9c98d-142">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="9c98d-143">Teams プラットフォームでアプリを読み込むには、インターネットからアプリにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-143">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="9c98d-144">インターネットからアプリにアクセスするには、アプリをホスト *する* 必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-144">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="9c98d-145">ローカル テストでは、ローカル コンピューターでアプリを実行し、Web エンドポイントを使用してそのコンピューターへのトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-145">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="9c98d-146">[ngrok は](https://ngrok.com) 、それを実行できる無料のツールです。</span><span class="sxs-lookup"><span data-stu-id="9c98d-146">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="9c98d-147">*ngrok を使用* すると、次のような Web アドレス `https://d0ac14a5.ngrok.io` を取得できます (この URL は単なる例です)。</span><span class="sxs-lookup"><span data-stu-id="9c98d-147">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="9c98d-148">環境に [合った](https://ngrok.com/download) *ngrok をダウンロード* してインストールできます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-148">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="9c98d-149">自分の場所に追加してください `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="9c98d-149">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="9c98d-150">インストールしたら、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-150">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="9c98d-151">サンプルではポート 3333 を使用します。そのため、ここで指定してください。</span><span class="sxs-lookup"><span data-stu-id="9c98d-151">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="9c98d-152">*Ngrok は* インターネットからの要求をリッスンし、ポート 3333 で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="9c98d-152">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="9c98d-153">確認するには、ブラウザーを開き、アプリの Hello ページを読 `https://d0ac14a5.ngrok.io/hello` み込む方法があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-153">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="9c98d-154">この URL の代わりに、コンソール セッションで *ngrok* によって表示される転送アドレスを使用してください。</span><span class="sxs-lookup"><span data-stu-id="9c98d-154">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="9c98d-155">ビルドで別のポートを使用して上記 [](#build-and-run-the-sample)の手順を実行した場合は、同じポート番号を使用して *ngrok トンネルをセットアップ* してください。</span><span class="sxs-lookup"><span data-stu-id="9c98d-155">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="9c98d-156">*ngrok* を別のターミナル ウィンドウで実行し、後で停止、リビルド、再実行が必要になる可能性があるノード アプリを妨げずに実行し続けます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-156">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="9c98d-157">*ngrok セッションは*、このウィンドウで役立つデバッグ情報を返します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-157">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="9c98d-158">永続的な名前を許可する *有料版の ngrok* があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-158">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="9c98d-159">無料版を使う場合は、開発用コンピューターの現在のセッション中にのみアプリを利用できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-159">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="9c98d-160">コンピューターがシャットダウンするか、スリープ状態になった場合、サービスは利用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="9c98d-160">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="9c98d-161">他のユーザーがテスト用にアプリを共有する場合は、このことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="9c98d-161">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="9c98d-162">サービスを再起動する必要がある場合は、新しいアドレスが返され、そのアドレスを使用する場所ごとに更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-162">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="9c98d-163">アプリの URL は、後で App Studio を使用して Teams に登録するときに必要になりますので、メモに書き込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-163">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="9c98d-164">メモ帳は、この目的に合った機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-164">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="9c98d-165">アプリを Microsoft Teams に展開する</span><span class="sxs-lookup"><span data-stu-id="9c98d-165">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="9c98d-166">この時点で、アプリはインターネットでホストされますが、検索する場所やアプリの呼び出し先を Teams にまだ伝える方法はありません。</span><span class="sxs-lookup"><span data-stu-id="9c98d-166">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="9c98d-167">これを行うには、アプリ パッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-167">To do this you now have to create an app package.</span></span> <span data-ttu-id="9c98d-168">これは、アプリ マニフェストと、Teams クライアントがアプリを適切に表示およびブランド化するために使用する一部のアイコンを含むテキスト ファイルに近いファイルです。</span><span class="sxs-lookup"><span data-stu-id="9c98d-168">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="9c98d-169">このアプリ パッケージを手動で作成するか、アプリを登録するプロセスを簡素化する Teams で実行されるツールである App Studio を使用できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-169">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="9c98d-170">App Studio は、アプリ パッケージの作成と更新を行う場合に推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="9c98d-170">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="9c98d-171">どちらの方法でも、以下が必要です。</span><span class="sxs-lookup"><span data-stu-id="9c98d-171">For either method you will need the following:</span></span>

- <span data-ttu-id="9c98d-172">アプリがインターネット上で見つかる URL。</span><span class="sxs-lookup"><span data-stu-id="9c98d-172">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="9c98d-173">Teams がアプリのブランド化に使用するアイコン。</span><span class="sxs-lookup"><span data-stu-id="9c98d-173">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="9c98d-174">サンプルには、"src\static\images" にあるプレースホルダー アイコンが付属しています。</span><span class="sxs-lookup"><span data-stu-id="9c98d-174">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="9c98d-175">App Studio では、必要に応じて既定のアイコンも提供されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-175">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="9c98d-176">ホストされているアプリを更新する</span><span class="sxs-lookup"><span data-stu-id="9c98d-176">Update your hosted app</span></span>

<span data-ttu-id="9c98d-177">サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-177">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="9c98d-178">その方法は、アプリのホスト方法によって異なります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-178">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="9c98d-179">環境変数の使用に関する重要な点は、これらの値は環境の一部であり、アプリのコードからアクセスできますが、サイトを構成するファイルを調べるサード パーティには公開されません。</span><span class="sxs-lookup"><span data-stu-id="9c98d-179">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="9c98d-180">ngrok を使ってアプリを実行している場合は、ローカル環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-180">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="9c98d-181">これを行うには多くの方法がありますが、Visual Studio Code を使用している場合は、起動構成を [追加するのが最も簡単です](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)。</span><span class="sxs-lookup"><span data-stu-id="9c98d-181">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="9c98d-182">ここで、</span><span class="sxs-lookup"><span data-stu-id="9c98d-182">Where:</span></span>

<span data-ttu-id="9c98d-183">MICROSOFT_APP_IDとMICROSOFT_APP_PASSWORDは、ボットの ID とパスワードです。</span><span class="sxs-lookup"><span data-stu-id="9c98d-183">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="9c98d-184">NODE_DEBUGコード デバッグ コンソールでボットで何が起きているVisual Studio表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-184">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="9c98d-185">NODE_CONFIG_DIRリポジトリのルートにあるディレクトリをポイントします (既定では、アプリがローカルで実行されている場合は、src フォルダーで検索されます)。</span><span class="sxs-lookup"><span data-stu-id="9c98d-185">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="9c98d-186">このチュートリアルの前の方から npm を停止していない場合は、Visual Studio Code が起動構成変数を正しくピックアップするために実行する `npm stop` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-186">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="9c98d-187">[アプリ] タブを構成する</span><span class="sxs-lookup"><span data-stu-id="9c98d-187">Configure the app tab</span></span>

<span data-ttu-id="9c98d-188">アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c98d-188">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="9c98d-189">チーム内のチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。その後、[タブ `Hello World` の追加] **ボックスの一覧から選択** できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-189">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="9c98d-190">構成ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-190">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="9c98d-191">このダイアログでは、このチャネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-191">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="9c98d-192">タブを選択してクリックすると、選択したタブと一緒に読み `Save` `Hello World` 込まれたタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-192">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" alt-text="Screenshot of configure" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="9c98d-193">Teams でボットをテストする</span><span class="sxs-lookup"><span data-stu-id="9c98d-193">Test your bot in Teams</span></span>

<span data-ttu-id="9c98d-194">Teams でボットを操作できます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-194">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="9c98d-195">アプリを登録したチームのチャネルを選択し、メッセージを入力して `@your-bot-name` 入力します。</span><span class="sxs-lookup"><span data-stu-id="9c98d-195">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="9c98d-196">これはメンションと呼 **\@ ばれる。**</span><span class="sxs-lookup"><span data-stu-id="9c98d-196">This is called an **\@mention**.</span></span> <span data-ttu-id="9c98d-197">ボットに送信したメッセージは、返信として返送されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-197">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt-text="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="9c98d-198">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="9c98d-198">Test your messaging extension</span></span>

<span data-ttu-id="9c98d-199">メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。</span><span class="sxs-lookup"><span data-stu-id="9c98d-199">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="9c98d-200">メニューに **"Hello World"** アプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-200">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="9c98d-201">クリックすると、ランダムなテキストが多数表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-201">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="9c98d-202">You can choose any one of them and it will be inserted it into your conversation.</span><span class="sxs-lookup"><span data-stu-id="9c98d-202">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" alt-text="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt-text="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="9c98d-203">ランダムなテキストのいずれかを選択すると、カードがフォーマットされ、下部に独自のメッセージと一緒に送信する準備が整っているのが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c98d-203">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" alt-text="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
