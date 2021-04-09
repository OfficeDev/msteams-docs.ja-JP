---
title: アプリをテストおよびデバッグするためのセットアップの選択
description: Microsoft Teams アプリのテストとデバッグのオプションについて説明します。
keywords: チームがデバッグ アプリを実行する
ms.topic: conceptual
ms.openlocfilehash: fde8a5907e0815ff798a3acc316cba8336ab8704
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634735"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a><span data-ttu-id="bb474-104">Microsoft Teams アプリをテストおよびデバッグするセットアップを選択する</span><span class="sxs-lookup"><span data-stu-id="bb474-104">Choose a setup to test and debug your Microsoft Teams app</span></span>

<span data-ttu-id="bb474-105">Microsoft Teams アプリには 1 つ以上の機能が含まれているので、それらを実行またはホストする方法は異なります。</span><span class="sxs-lookup"><span data-stu-id="bb474-105">Microsoft Teams apps contain one or more capabilities and the ways to run or even host them are different.</span></span> <span data-ttu-id="bb474-106">デバッグには、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="bb474-106">For debugging, use one of the following ways:</span></span>

* <span data-ttu-id="bb474-107">**純粋にローカル**: ボットの場合は、ボット エミュレーターでエクスペリエンスをテストできます。</span><span class="sxs-lookup"><span data-stu-id="bb474-107">**Purely local**: For bots, you can test your experience in the Bot Emulator.</span></span> <span data-ttu-id="bb474-108">その他のコンテンツについては、ブラウザーでローカルで実行し、コンテンツにアドレスを指定できます `http://localhost` 。</span><span class="sxs-lookup"><span data-stu-id="bb474-108">For other content, you can run locally in your browser and address content through `http://localhost`.</span></span>
* <span data-ttu-id="bb474-109">**Teams でローカルにホスト** される : これには、トンネリング ソフトウェアでアプリ [](~/concepts/build-and-test/apps-package.md)をローカルで実行し、Teams にアップロードするパッケージ [を作成する](~/concepts/deploy-and-publish/apps-upload.md)必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-109">**Locally hosted in Teams**: This involves running the app locally in tunneling software and [creating a package](~/concepts/build-and-test/apps-package.md) to [upload](~/concepts/deploy-and-publish/apps-upload.md) into Teams.</span></span> <span data-ttu-id="bb474-110">これにより、Teams クライアント内でアプリを簡単に実行およびデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="bb474-110">This permits you to easily run and debug your app within the Teams client.</span></span>
* <span data-ttu-id="bb474-111">**Teams でクラウドホスト**: Teams アプリの実稼働レベルのサポートを実際にシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="bb474-111">**Cloud-hosted in Teams**: This truly simulates the production level support for a Teams app.</span></span> <span data-ttu-id="bb474-112">ソリューションを外部からアクセス可能なサーバーまたはクラウド プロバイダーにアップロードし、Teams にアップロード[](~/concepts/build-and-test/apps-package.md)するパッケージを作成[する](~/concepts/deploy-and-publish/apps-upload.md)必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-112">It involves uploading your solution to your externally accessible server or cloud provider of choice and [creating a package](~/concepts/build-and-test/apps-package.md) to [upload](~/concepts/deploy-and-publish/apps-upload.md) into Teams.</span></span>

<span data-ttu-id="bb474-113">純粋にローカルまたはローカルの Teams テストのために、独自のコンピューターからエクスペリエンスを実行します。</span><span class="sxs-lookup"><span data-stu-id="bb474-113">Run the experience from your own computer for purely local or local Teams testing.</span></span> <span data-ttu-id="bb474-114">これにより、統合された開発環境内でコンパイルおよび実行し、ブレークポイントやステップ デバッグなどの手法を活用できます。</span><span class="sxs-lookup"><span data-stu-id="bb474-114">By doing this, you can compile and run within your integrated development environment and take full advantage of techniques, such as breakpoints and step debugging.</span></span> 

> [!NOTE]
> <span data-ttu-id="bb474-115">実稼働規模のデバッグとテストでは、独自のプロセスを通じてテスト、ステージング、および展開をサポートするために、独自の会社のガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-115">For production-scale debugging and testing, we recommend that you follow your own company guidelines to ensure you are able to support testing, staging, and deployment through your own processes.</span></span>

<span data-ttu-id="bb474-116">複数のマニフェストとパッケージを使用して、実稼働サービスと開発サービスの分離を維持します。</span><span class="sxs-lookup"><span data-stu-id="bb474-116">Use multiple manifests and packages to maintain separation between production and development services.</span></span> <span data-ttu-id="bb474-117">たとえば、個別の開発ボットと実稼働ボットを登録し、テスト環境でアップロードする適切なパッケージを作成できます。</span><span class="sxs-lookup"><span data-stu-id="bb474-117">For example, you might choose to register separate development and production bots and create appropriate packages to upload them in your testing environment.</span></span> <span data-ttu-id="bb474-118">また、アプリストアでの発行や顧客への配布のためにアプリを提出する前に、実稼働パッケージをアップロードしてテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bb474-118">We also recommend, you upload and test your production package before submitting your app for publishing in our app store or distributing to customers.</span></span>

## <a name="purely-local"></a><span data-ttu-id="bb474-119">純粋にローカル</span><span class="sxs-lookup"><span data-stu-id="bb474-119">Purely local</span></span>

> [!NOTE]
> <span data-ttu-id="bb474-120">ボットをローカルで実行しても、Teams アプリ機能や、名簿呼び出しや他のチャネル固有の機能などの Teams 固有のボット機能にアクセスできない。</span><span class="sxs-lookup"><span data-stu-id="bb474-120">Running the bot locally does not give you access to Teams app functionality or Teams-specific bot functions like roster calls and other channel-specific functionality.</span></span> <span data-ttu-id="bb474-121">さらに、一部の機能は、Microsoft Teams で実行するときに機能しない可能性があるボット エミュレーターのボット フレームワークによって許可されます。</span><span class="sxs-lookup"><span data-stu-id="bb474-121">In addition, some capabilities are permitted by the Bot Framework in the Bot Emulator that might not function when running in Microsoft Teams.</span></span>

<span data-ttu-id="bb474-122">ボットはボット エミュレーター内で実行できます。</span><span class="sxs-lookup"><span data-stu-id="bb474-122">Your bot can run within the Bot Emulator.</span></span> <span data-ttu-id="bb474-123">これにより、ボットのコア ロジックの一部をテストし、メッセージの大まかなレイアウトを確認し、簡単なテストを実行できます。</span><span class="sxs-lookup"><span data-stu-id="bb474-123">This enables you to test some of the core logic of the bot, see a rough layout of messages, and perform simple tests.</span></span> <span data-ttu-id="bb474-124">手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="bb474-124">Following are the steps:</span></span>

1. <span data-ttu-id="bb474-125">コードをローカルで実行します。</span><span class="sxs-lookup"><span data-stu-id="bb474-125">Run the code locally.</span></span>
2. <span data-ttu-id="bb474-126">ボット エミュレーターを起動し、URL を設定します。</span><span class="sxs-lookup"><span data-stu-id="bb474-126">Launch the Bot Emulator and set the URL:</span></span>
   * <span data-ttu-id="bb474-127">Node.js: `http://localhost:3978/api/messages`</span><span class="sxs-lookup"><span data-stu-id="bb474-127">Node.js: `http://localhost:3978/api/messages`</span></span>
   * <span data-ttu-id="bb474-128">.NET/C#: `http://localhost:3979/api/messages`</span><span class="sxs-lookup"><span data-stu-id="bb474-128">.NET/C#: `http://localhost:3979/api/messages`</span></span>
3. <span data-ttu-id="bb474-129">既定の環境変数と一致するには、Microsoft アプリ ID と Microsoft アプリのパスワードを空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="bb474-129">Leave the Microsoft app ID and Microsoft app password blank, to match the default environment variables.</span></span>

## <a name="locally-hosted"></a><span data-ttu-id="bb474-130">ローカルでホストされる</span><span class="sxs-lookup"><span data-stu-id="bb474-130">Locally hosted</span></span>

<span data-ttu-id="bb474-131">Microsoft Teams は完全にクラウドベースの製品です。アクセスするサービスはすべて HTTPS エンドポイントを使用して一般公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-131">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available publicly using HTTPS endpoints.</span></span> <span data-ttu-id="bb474-132">そのため、アプリが Teams 内で動作するには、コードを選択したクラウドに発行するか、ローカル実行中のインスタンスに外部からアクセス可能にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-132">Therefore, to enable your app to work within Teams, you need to either publish the code to the cloud of your choice or make our local running instance externally accessible.</span></span> <span data-ttu-id="bb474-133">トンネリング ソフトウェアを使用して後者を実行できます。</span><span class="sxs-lookup"><span data-stu-id="bb474-133">We can do the latter with tunneling software.</span></span>

<span data-ttu-id="bb474-134">任意のツールを使用することもできますが、コンピューター上でローカルで開くポートの外部アドレス指定可能な URL を作成する [ngrok](https://ngrok.com/download)を使用して推奨します。</span><span class="sxs-lookup"><span data-stu-id="bb474-134">Although you can use any tool of your choice, we use and recommend [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span> 

<span data-ttu-id="bb474-135">**Microsoft Teams アプリをローカルで実行する準備として ngrok を設定するには**</span><span class="sxs-lookup"><span data-stu-id="bb474-135">**To set up ngrok in preparation for running your Microsoft Teams app locally**</span></span>

1. <span data-ttu-id="bb474-136">ターミナル アプリケーションにインストールされているディレクトリngrok.exe移動します。</span><span class="sxs-lookup"><span data-stu-id="bb474-136">Go to the directory where you have ngrok.exe installed in a terminal application.</span></span> <span data-ttu-id="bb474-137">この手順を回避するために、パス変数として追加できます。</span><span class="sxs-lookup"><span data-stu-id="bb474-137">You may want to add it as a path variable to avoid this step.</span></span>
2. <span data-ttu-id="bb474-138">たとえば、ポート番号を `ngrok http 3978 --host-header=localhost:3978` 必要に応じて実行するか、置換します。</span><span class="sxs-lookup"><span data-stu-id="bb474-138">Run, for example, `ngrok http 3978 --host-header=localhost:3978`, or replace the port number as needed.</span></span>
   <span data-ttu-id="bb474-139">これにより、指定したポートのリストに ngrok が起動します。</span><span class="sxs-lookup"><span data-stu-id="bb474-139">This launches ngrok to list on the port you specify.</span></span> <span data-ttu-id="bb474-140">その代り、ngrok が実行されている限り、外部でアドレス指定可能な URL が有効になります。</span><span class="sxs-lookup"><span data-stu-id="bb474-140">In return, it gives you an externally addressable URL valid for as long as ngrok is running.</span></span>

> [!NOTE]
> <span data-ttu-id="bb474-141">ngrok を停止して再起動すると、URL が変更されます。</span><span class="sxs-lookup"><span data-stu-id="bb474-141">If you stop and restart ngrok, the URL changes.</span></span>

<span data-ttu-id="bb474-142">使用している機能に基づいてプロジェクトで ngrok を使用するには、この URL エンドポイントを使用するには、コード、構成、および manifest.json ファイル内のすべての URL 参照を置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-142">To use ngrok in your project based on the capabilities you are using, you must replace all URL references in your code, configuration, and manifest.json file to use this URL endpoint.</span></span>

<span data-ttu-id="bb474-143">Microsoft Bot Framework に登録されているボットの場合は、ボットのメッセージング エンドポイントを更新して、この新しい ngrok エンドポイントを使用します。</span><span class="sxs-lookup"><span data-stu-id="bb474-143">For bots registered in the Microsoft Bot Framework, update the bot's messaging endpoint to use this new ngrok endpoint.</span></span> <span data-ttu-id="bb474-144">たとえば、`https://2d1224fb.ngrok.io/api/messages` などです。</span><span class="sxs-lookup"><span data-stu-id="bb474-144">For example, `https://2d1224fb.ngrok.io/api/messages`.</span></span> <span data-ttu-id="bb474-145">ボット フレームワーク ポータルの [テスト チャット] ウィンドウでボット応答をテストすることで、ngrok が動作しているのを検証できます。</span><span class="sxs-lookup"><span data-stu-id="bb474-145">You can validate that ngrok is working by testing the bot response in the Bot Framework portal's Test chat window.</span></span> <span data-ttu-id="bb474-146">エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="bb474-146">Again, like the emulator, this test does not permit you to access Teams-specific functionality.</span></span>

> [!NOTE]
> <span data-ttu-id="bb474-147">ボットのメッセージング エンドポイントを更新するには、ボット フレームワークを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-147">To update the messaging endpoint for a bot, you must use the Bot Framework.</span></span> <span data-ttu-id="bb474-148">ボット フレームワークのボット [の一覧でボットを選択します](https://dev.botframework.com/bots)。</span><span class="sxs-lookup"><span data-stu-id="bb474-148">Select your bot in [your list of bots in Bot Framework](https://dev.botframework.com/bots).</span></span> <span data-ttu-id="bb474-149">ボットを Microsoft Azure に移行する必要はない。</span><span class="sxs-lookup"><span data-stu-id="bb474-149">You do not need to migrate your bot to Microsoft Azure.</span></span> <span data-ttu-id="bb474-150">また、App Studio を使用してメッセージング エンドポイント [を更新することもできます](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bb474-150">You can also update your messaging endpoint through [App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="cloud-hosted"></a><span data-ttu-id="bb474-151">クラウド ホスト型</span><span class="sxs-lookup"><span data-stu-id="bb474-151">Cloud-hosted</span></span>

<span data-ttu-id="bb474-152">外部アドレス指定可能なサービスを使用して、開発および実稼働コードとその HTTPS エンドポイントをホストできます。</span><span class="sxs-lookup"><span data-stu-id="bb474-152">You can use any externally addressable service to host your development and production code and their HTTPS endpoints.</span></span> <span data-ttu-id="bb474-153">機能が同じサービスに存在する期待はありません。</span><span class="sxs-lookup"><span data-stu-id="bb474-153">There is no expectation that your capabilities reside on the same service.</span></span> <span data-ttu-id="bb474-154">ファイル内のオブジェクトに一覧表示されている Microsoft Teams アプリからすべてのドメイン [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) にアクセスする必要 `manifest.json` があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-154">We require all domains to be accessed from your Microsoft Teams apps listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) object in the `manifest.json` file.</span></span>

> [!NOTE]
> <span data-ttu-id="bb474-155">安全な環境を確保するには、参照する正確なドメインとサブドメインについて明示的に説明し、それらのドメインを制御する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-155">To ensure a secure environment, be explicit about the exact domain and subdomains you reference and those domains must be in your control.</span></span> <span data-ttu-id="bb474-156">たとえば、お `*.azurewebsites.net` 勧めできませんが、 `contoso.azurewebsites.net` お勧めします。</span><span class="sxs-lookup"><span data-stu-id="bb474-156">For example, `*.azurewebsites.net` is not recommended, however `contoso.azurewebsites.net` is recommended.</span></span>

## <a name="load-and-run-your-experience"></a><span data-ttu-id="bb474-157">エクスペリエンスの読み込みと実行</span><span class="sxs-lookup"><span data-stu-id="bb474-157">Load and run your experience</span></span>

<span data-ttu-id="bb474-158">Microsoft Teams 内でエクスペリエンスを読み込み、実行するには、パッケージを作成して Teams にアップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb474-158">To load and run your experience within Microsoft Teams, you need to create a package and upload it into Teams.</span></span> <span data-ttu-id="bb474-159">詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bb474-159">For more information, see:</span></span>

* [<span data-ttu-id="bb474-160">Microsoft Teams アプリのパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="bb474-160">Create the package for your Microsoft Teams app</span></span>](~/concepts/build-and-test/apps-package.md)
* [<span data-ttu-id="bb474-161">Microsoft Teams でアプリをアップロードする</span><span class="sxs-lookup"><span data-stu-id="bb474-161">Upload your app in Microsoft Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)

## <a name="next-step"></a><span data-ttu-id="bb474-162">次の手順</span><span class="sxs-lookup"><span data-stu-id="bb474-162">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="bb474-163">テスト データを環境に追加する</span><span class="sxs-lookup"><span data-stu-id="bb474-163">Add test data to your environment</span></span>](~/concepts/build-and-test/test-data.md)

