---
title: アプリスタジオと node.js を使い始める
description: Node.js とアプリ Studio を使用して Microsoft Teams での高度なアプリの構築を開始する
keywords: 初級ノード .js nodejs アプリ Studio
ms.date: 11/09/2018
ms.openlocfilehash: 36da6d7445ad7780f6bbbf52ccce3e558c76be72
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675056"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-nodejs-and-app-studio"></a><span data-ttu-id="02763-104">Node.js とアプリ Studio を使用して Microsoft Teams プラットフォームで作業を開始する</span><span class="sxs-lookup"><span data-stu-id="02763-104">Get started on the Microsoft Teams platform with Node.js and App Studio</span></span>

<span data-ttu-id="02763-105">[Microsoft teams](/microsoftteams/)開発者プラットフォームを使用すると、teams の拡張が容易になり、独自のアプリケーションやサービスを teams ワークスペースにシームレスに統合することができます。</span><span class="sxs-lookup"><span data-stu-id="02763-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="02763-106">これらのアプリは、企業または世界中の teams に配布できます。</span><span class="sxs-lookup"><span data-stu-id="02763-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="02763-107">Microsoft Teams を拡張するには、Microsoft Teams アプリを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-107">To extend Microsoft Teams, you need to create a Microsoft Teams app.</span></span> <span data-ttu-id="02763-108">Microsoft Teams アプリは、ホストする web アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="02763-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="02763-109">このアプリは、Teams のユーザーのワークスペースに統合できます。</span><span class="sxs-lookup"><span data-stu-id="02763-109">This app can then be integrated into the user's workspace in Teams.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="02763-110">アプリをダウンロードしてホストする</span><span class="sxs-lookup"><span data-stu-id="02763-110">Download and host your app</span></span>

<span data-ttu-id="02763-111">簡単な "hello world" アプリを Teams にダウンロードしてホストするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="02763-111">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="02763-112">前提条件を取得する</span><span class="sxs-lookup"><span data-stu-id="02763-112">Get prerequisites</span></span>

<span data-ttu-id="02763-113">このチュートリアルを完了するには、次のツールが必要です。</span><span class="sxs-lookup"><span data-stu-id="02763-113">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="02763-114">これらのリンクからインストールすることはできません。</span><span class="sxs-lookup"><span data-stu-id="02763-114">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="02763-115">Git</span><span class="sxs-lookup"><span data-stu-id="02763-115">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="02763-116">Node.js および NPM</span><span class="sxs-lookup"><span data-stu-id="02763-116">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="02763-117">任意のテキストエディターまたは IDE を取得します。</span><span class="sxs-lookup"><span data-stu-id="02763-117">Get any text editor or IDE.</span></span> <span data-ttu-id="02763-118">[Visual Studio コード](https://code.visualstudio.com/download)を無料でインストールして使用することができます。</span><span class="sxs-lookup"><span data-stu-id="02763-118">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="02763-119">インストール時に、、、 `git` `node` `npm`、および`code`のパスを追加するオプションが表示されたら、それを選択します。</span><span class="sxs-lookup"><span data-stu-id="02763-119">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="02763-120">これは便利です。</span><span class="sxs-lookup"><span data-stu-id="02763-120">It will be handy.</span></span>

<span data-ttu-id="02763-121">ターミナルウィンドウで次のように実行して、ツールが使用可能であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="02763-121">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="02763-122">ご使用のプラットフォームで最も快適なターミナルウィンドウを使用してください。</span><span class="sxs-lookup"><span data-stu-id="02763-122">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="02763-123">これらの例では、Bash (Git に含まれています) を使用していますが、これらのスクリプトはほとんどのプラットフォームで実行されます。</span><span class="sxs-lookup"><span data-stu-id="02763-123">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 4.0.2
```

<span data-ttu-id="02763-124">これらのアプリケーションのバージョンが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="02763-124">You may have a different version of these applications.</span></span> <span data-ttu-id="02763-125">これは、gulp を除き、問題になりません。</span><span class="sxs-lookup"><span data-stu-id="02763-125">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="02763-126">Gulp の場合は、バージョン4.0.0 以降を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-126">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="02763-127">Gulp がインストールされていない (または、バージョンが正しくない) 場合は、 `npm install gulp`ターミナルウィンドウでを実行して、これを実行します。</span><span class="sxs-lookup"><span data-stu-id="02763-127">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="02763-128">Visual Studio Code をインストールした場合は、インストールを確認するには、次のように実行します。</span><span class="sxs-lookup"><span data-stu-id="02763-128">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="02763-129">このターミナルウィンドウを引き続き使用して、このチュートリアルの後のコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="02763-129">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="02763-130">サンプルをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="02763-130">Download the sample</span></span>

<span data-ttu-id="02763-131">シンプルな Hello を提供してい[ます。](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span><span class="sxs-lookup"><span data-stu-id="02763-131">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span></span> <span data-ttu-id="02763-132">開始するためのサンプルです。</span><span class="sxs-lookup"><span data-stu-id="02763-132">sample to get you started.</span></span> <span data-ttu-id="02763-133">ターミナルウィンドウで、次のコマンドを実行して、サンプルリポジトリをローカルコンピューターに複製します。</span><span class="sxs-lookup"><span data-stu-id="02763-133">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> <span data-ttu-id="02763-134">後で参照できるように GitHub リポジトリに加えた変更を変更してチェックインする場合は、この[リポジトリ](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)を[fork](https://help.github.com/articles/fork-a-repo/)することができます。</span><span class="sxs-lookup"><span data-stu-id="02763-134">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="02763-135">サンプルの構築と実行</span><span class="sxs-lookup"><span data-stu-id="02763-135">Build and run the sample</span></span>

<span data-ttu-id="02763-136">リポジトリが複製されたら、サンプルを保持するディレクトリに変更します。</span><span class="sxs-lookup"><span data-stu-id="02763-136">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd msteams-samples-hello-world-nodejs
```

<span data-ttu-id="02763-137">サンプルをビルドするには、そのすべての依存関係をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-137">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="02763-138">これを行うには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="02763-138">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="02763-139">一連の依存関係がインストールされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-139">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="02763-140">完了したら、アプリを実行することができます。</span><span class="sxs-lookup"><span data-stu-id="02763-140">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="02763-141">Hello world アプリが開始すると、ターミナルウィンドウ`App started listening on port 3333`に表示されます。</span><span class="sxs-lookup"><span data-stu-id="02763-141">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="02763-142">上記のメッセージに別のポート番号が表示されている場合は、ポート環境変数が設定されているためです。</span><span class="sxs-lookup"><span data-stu-id="02763-142">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="02763-143">そのポートを引き続き使用するか、環境変数を3333に変更することができます。</span><span class="sxs-lookup"><span data-stu-id="02763-143">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="02763-144">この時点で、ブラウザーウィンドウを開き、次の Url に移動して、すべてのアプリ Url が読み込まれていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="02763-144">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="02763-145">サンプルアプリをホストする</span><span class="sxs-lookup"><span data-stu-id="02763-145">Host the sample app</span></span>

<span data-ttu-id="02763-146">Microsoft Teams のアプリは、1つまたは複数の機能を公開している web アプリケーションであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="02763-146">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="02763-147">Teams プラットフォームでアプリを読み込むには、インターネットからアプリにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-147">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="02763-148">アプリをインターネットからアクセスできるようにするには、アプリを*ホスト*する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-148">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="02763-149">ローカルテストでは、ローカルコンピューター上でアプリを実行し、web エンドポイントを使用してそのアプリケーションへのトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="02763-149">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="02763-150">[ngrok](https://ngrok.com)は、そのようなことを可能にする無償のツールです。</span><span class="sxs-lookup"><span data-stu-id="02763-150">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="02763-151">*Ngrok*を使用すると`https://d0ac14a5.ngrok.io` 、などの web アドレスを取得できます (この URL は例にすぎません)。</span><span class="sxs-lookup"><span data-stu-id="02763-151">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="02763-152">環境の*ngrok*を[ダウンロードしてインストール](https://ngrok.com/download)することができます。</span><span class="sxs-lookup"><span data-stu-id="02763-152">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="02763-153">がの場所に追加さ`PATH`れていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="02763-153">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="02763-154">インストールすると、新しいターミナルウィンドウを開き、次のコマンドを実行してトンネルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="02763-154">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="02763-155">このサンプルではポート3333を使用しているため、ここで必ず指定してください。</span><span class="sxs-lookup"><span data-stu-id="02763-155">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="02763-156">*Ngrok*は、インターネットからの要求をリスンし、ポート3333で実行されているアプリにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="02763-156">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="02763-157">ブラウザー `https://d0ac14a5.ngrok.io/hello`を開き、アプリの hello ページを読み込むことによって確認できます。</span><span class="sxs-lookup"><span data-stu-id="02763-157">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="02763-158">この URL ではなく、コンソールセッションで*ngrok*によって表示される転送アドレスを使用してください。</span><span class="sxs-lookup"><span data-stu-id="02763-158">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="02763-159">上記の[ビルド](#build-and-run-the-sample)で別のポートを使用している場合は、同じポート番号を使用して*ngrok*トンネルをセットアップしてください。</span><span class="sxs-lookup"><span data-stu-id="02763-159">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="02763-160">*Ngrok*を別のターミナルウィンドウで実行して、ノードアプリに影響を及ぼすことなく、後で停止、再構築、再実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-160">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="02763-161">*Ngrok*セッションは、このウィンドウで役に立つデバッグ情報を返します。</span><span class="sxs-lookup"><span data-stu-id="02763-161">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="02763-162">固定名を許可する有料版の*ngrok*があります。</span><span class="sxs-lookup"><span data-stu-id="02763-162">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="02763-163">無料バージョンを使用する場合、アプリは開発用コンピューター上の現在のセッション中にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="02763-163">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="02763-164">コンピューターがシャットダウンされるかスリープ状態になると、サービスは使用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="02763-164">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="02763-165">他のユーザーによるテスト用にアプリを共有する場合は、この点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="02763-165">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="02763-166">サービスを再起動する必要がある場合は、新しいアドレスを返し、そのアドレスを使用するすべての場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-166">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="02763-167">アプリをアプリを使用して Teams に登録するときに必要になるため、後でアプリの URL を書き留めておいてください。</span><span class="sxs-lookup"><span data-stu-id="02763-167">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="02763-168">このため、メモ帳は正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="02763-168">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="02763-169">アプリを Microsoft Teams に展開する</span><span class="sxs-lookup"><span data-stu-id="02763-169">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="02763-170">この時点では、インターネット上でホストされているアプリがありますが、チームに対して、またはアプリの呼び出しについての情報を提供する方法はありません。</span><span class="sxs-lookup"><span data-stu-id="02763-170">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="02763-171">これを行うには、アプリパッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-171">To do this you now have to create an app package.</span></span> <span data-ttu-id="02763-172">これは、アプリマニフェストと、Teams クライアントがアプリを適切に表示およびブランド化するために使用するいくつかのアイコンを含むテキストファイルに比べてわずかです。</span><span class="sxs-lookup"><span data-stu-id="02763-172">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="02763-173">このアプリパッケージを手動で作成するか、アプリを登録するプロセスを簡略化する Teams で実行されるツールである App Studio を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="02763-173">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="02763-174">アプリのパッケージを作成および更新する方法として、アプリ Studio が推奨されています。</span><span class="sxs-lookup"><span data-stu-id="02763-174">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="02763-175">どちらの方法でも、次のものが必要になります。</span><span class="sxs-lookup"><span data-stu-id="02763-175">For either method you will need the following:</span></span>

- <span data-ttu-id="02763-176">アプリをインターネット上で見つけることができる URL。</span><span class="sxs-lookup"><span data-stu-id="02763-176">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="02763-177">Teams がアプリをブランド化するために使用するアイコン。</span><span class="sxs-lookup"><span data-stu-id="02763-177">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="02763-178">サンプルには、"src\static\images." にあるプレースホルダーアイコンが付属しています。</span><span class="sxs-lookup"><span data-stu-id="02763-178">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="02763-179">アプリ Studio では、必要に応じて既定のアイコンも提供されます。</span><span class="sxs-lookup"><span data-stu-id="02763-179">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="02763-180">ホストされているアプリを更新する</span><span class="sxs-lookup"><span data-stu-id="02763-180">Update your hosted app</span></span>

<span data-ttu-id="02763-181">サンプルアプリでは、以下の環境変数を事前にメモした値に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-181">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="02763-182">その方法は、アプリをホストした方法によって異なります。</span><span class="sxs-lookup"><span data-stu-id="02763-182">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="02763-183">環境変数を使用する場合の重要な点は、これらの値は環境の一部であり、アプリのコードからアクセスできますが、サイトを構成するファイルを調べる可能性がある第三者には公開されません。</span><span class="sxs-lookup"><span data-stu-id="02763-183">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="02763-184">Ngrok を使用してアプリを実行している場合は、いくつかのローカル環境変数を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-184">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="02763-185">これを行うには多くの方法がありますが、Visual Studio Code を使用している場合は、[起動構成](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)を追加するのが最も簡単です。</span><span class="sxs-lookup"><span data-stu-id="02763-185">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="02763-186">ここで、</span><span class="sxs-lookup"><span data-stu-id="02763-186">Where:</span></span>

<span data-ttu-id="02763-187">MICROSOFT_APP_ID と MICROSOFT_APP_PASSWORD は、それぞれの bot の ID とパスワードです。</span><span class="sxs-lookup"><span data-stu-id="02763-187">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="02763-188">NODE_DEBUG は、Visual Studio Code デバッグコンソールで bot で起こっていることを示します。</span><span class="sxs-lookup"><span data-stu-id="02763-188">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="02763-189">NODE_CONFIG_DIR リポジトリのルートにあるディレクトリを指します (既定では、アプリがローカルで実行されている場合は、そのフォルダーが src フォルダーで検索されます)。</span><span class="sxs-lookup"><span data-stu-id="02763-189">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="02763-190">チュートリアルの前半で npm を停止していない場合は、Visual Studio Code `npm stop`が起動構成変数を正しくピックアップするために実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-190">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="02763-191">[アプリ] タブを構成する</span><span class="sxs-lookup"><span data-stu-id="02763-191">Configure the app tab</span></span>

<span data-ttu-id="02763-192">アプリをチームにインストールしたら、コンテンツを表示するように構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02763-192">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="02763-193">チーム内のチャネルに移動し、[ **+** ] ボタンをクリックして新しいタブを追加します。その後、[ `Hello World` **タブの追加]** ボックスの一覧から選択できます。</span><span class="sxs-lookup"><span data-stu-id="02763-193">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="02763-194">構成ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="02763-194">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="02763-195">このダイアログボックスを使用すると、このチャネルに表示するタブを選択できます。</span><span class="sxs-lookup"><span data-stu-id="02763-195">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="02763-196">タブを選択して [] を`Save`クリックすると、 `Hello World`選択したタブに読み込まれたタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="02763-196">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" title="構成のスクリーンショット" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="02763-198">Teams でボットをテストする</span><span class="sxs-lookup"><span data-stu-id="02763-198">Test your bot in Teams</span></span>

<span data-ttu-id="02763-199">Teams で bot と対話できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="02763-199">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="02763-200">アプリを登録したチームでチャネルを選択し、「」 `@your-bot-name`と入力して、その後にメッセージを入力します。</span><span class="sxs-lookup"><span data-stu-id="02763-200">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="02763-201">これは、 \*\* \@メンション\*\*と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="02763-201">This is called an **\@mention**.</span></span> <span data-ttu-id="02763-202">Bot に送信するすべてのメッセージは、返信として返送されます。</span><span class="sxs-lookup"><span data-stu-id="02763-202">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" title="ボット応答" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="02763-204">メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="02763-204">Test your messaging extension</span></span>

<span data-ttu-id="02763-205">メッセージング拡張機能をテストするには、スレッドビューの入力ボックスの下にある3つのドットをクリックします。</span><span class="sxs-lookup"><span data-stu-id="02763-205">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="02763-206">**' Hello World '** アプリが含まれるメニューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="02763-206">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="02763-207">これをクリックすると、いくつかのランダムなテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="02763-207">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="02763-208">いずれかを選択して、会話に挿入することができます。</span><span class="sxs-lookup"><span data-stu-id="02763-208">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" title="メッセージング拡張メニュー" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" title="メッセージング拡張機能の結果" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="02763-211">ランダムなテキストの1つを選択すると、カードが書式設定されており、メッセージの下部に自分のメッセージで送信する準備ができます。</span><span class="sxs-lookup"><span data-stu-id="02763-211">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" title="メッセージング拡張送信" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
