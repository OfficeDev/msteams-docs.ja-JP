---
title: アプリをテストおよびデバッグするためのセットアップの選択
description: Microsoft Teams アプリのテストとデバッグのオプションについて説明します。
keywords: チームはデバッグアプリを実行します
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 1f11834ad83e8bea7e4114d25d022df2f62c1700
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565159"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a><span data-ttu-id="a7c27-104">Microsoft Teams アプリをテストおよびデバッグするためのセットアップを選択する</span><span class="sxs-lookup"><span data-stu-id="a7c27-104">Choose a setup to test and debug your Microsoft Teams app</span></span>

<span data-ttu-id="a7c27-105">Microsoft Teamsアプリには 1 つ以上の機能が含まれ、アプリを実行する方法やホストする方法も異なります。</span><span class="sxs-lookup"><span data-stu-id="a7c27-105">Microsoft Teams apps contain one or more capabilities and the ways to run or even host them are different.</span></span> <span data-ttu-id="a7c27-106">デバッグには、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-106">For debugging, use one of the following ways:</span></span>

* <span data-ttu-id="a7c27-107">**純粋にローカル**: ボットの場合は、ボットエミュレータで体験をテストできます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-107">**Purely local**: For bots, you can test your experience in the Bot Emulator.</span></span> <span data-ttu-id="a7c27-108">その他のコンテンツについては、ブラウザでローカルに実行し、コンテンツをアドレス指定するには `http://localhost` 、 を使用します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-108">For other content, you can run locally in your browser and address content through `http://localhost`.</span></span>
* <span data-ttu-id="a7c27-109">**ローカルでホストされているTeams**: トンネリング ソフトウェアでローカルにアプリを実行し、Teamsに [アップロード](~/concepts/deploy-and-publish/apps-upload.md)する [パッケージを作成](~/concepts/build-and-test/apps-package.md)します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-109">**Locally hosted in Teams**: This involves running the app locally in tunneling software and [creating a package](~/concepts/build-and-test/apps-package.md) to [upload](~/concepts/deploy-and-publish/apps-upload.md) into Teams.</span></span> <span data-ttu-id="a7c27-110">これにより、Teams クライアント内でアプリを簡単に実行およびデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-110">This permits you to easily run and debug your app within the Teams client.</span></span>
* <span data-ttu-id="a7c27-111">**Teamsでクラウドホスト**: これは、Teams アプリの実稼働レベルのサポートを実際にシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="a7c27-111">**Cloud-hosted in Teams**: This truly simulates the production level support for a Teams app.</span></span> <span data-ttu-id="a7c27-112">ソリューションを外部からアクセス可能なサーバーまたはクラウド プロバイダーにアップロードし、Teamsに[アップロード](~/concepts/deploy-and-publish/apps-upload.md)する[パッケージを作成](~/concepts/build-and-test/apps-package.md)します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-112">It involves uploading your solution to your externally accessible server or cloud provider of choice and [creating a package](~/concepts/build-and-test/apps-package.md) to [upload](~/concepts/deploy-and-publish/apps-upload.md) into Teams.</span></span>

<span data-ttu-id="a7c27-113">ローカルまたはローカルのテストを行う場合は、自分のコンピュータからエクスペリエンスを実行Teams。</span><span class="sxs-lookup"><span data-stu-id="a7c27-113">Run the experience from your own computer for purely local or local Teams testing.</span></span> <span data-ttu-id="a7c27-114">これにより、統合開発環境内でコンパイルおよび実行し、ブレークポイントやステップ デバッグなどの手法を最大限に活用できます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-114">By doing this, you can compile and run within your integrated development environment and take full advantage of techniques, such as breakpoints and step debugging.</span></span> 

> [!NOTE]
> <span data-ttu-id="a7c27-115">運用環境規模のデバッグとテストでは、独自の会社のガイドラインに従って、独自のプロセスを通じてテスト、ステージング、および展開をサポートできることを確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a7c27-115">For production-scale debugging and testing, we recommend that you follow your own company guidelines to ensure you are able to support testing, staging, and deployment through your own processes.</span></span>

<span data-ttu-id="a7c27-116">複数のマニフェストとパッケージを使用して、運用サービスと開発サービスの分離を維持します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-116">Use multiple manifests and packages to maintain separation between production and development services.</span></span> <span data-ttu-id="a7c27-117">たとえば、開発ボットと運用ボットを個別に登録し、適切なパッケージを作成して、テスト環境にアップロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-117">For example, you might choose to register separate development and production bots and create appropriate packages to upload them in your testing environment.</span></span> <span data-ttu-id="a7c27-118">また、アプリストアでの公開や顧客への配布のためにアプリを提出する前に、本番パッケージをアップロードしてテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a7c27-118">We also recommend, you upload and test your production package before submitting your app for publishing in our app store or distributing to customers.</span></span>

## <a name="purely-local"></a><span data-ttu-id="a7c27-119">純粋にローカル</span><span class="sxs-lookup"><span data-stu-id="a7c27-119">Purely local</span></span>

> [!NOTE]
> <span data-ttu-id="a7c27-120">ボットをローカルで実行しても、Teamsアプリ機能や、名簿呼び出しやその他のチャネル固有の機能などのTeams固有のボット機能にはアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="a7c27-120">Running the bot locally does not give you access to Teams app functionality or Teams-specific bot functions like roster calls and other channel-specific functionality.</span></span> <span data-ttu-id="a7c27-121">さらに、Microsoft Teamsで実行すると機能しない可能性がある Bot エミュレーターの Bot フレームワークで許可される機能もあります。</span><span class="sxs-lookup"><span data-stu-id="a7c27-121">In addition, some capabilities are permitted by the Bot Framework in the Bot Emulator that might not function when running in Microsoft Teams.</span></span>

<span data-ttu-id="a7c27-122">ボットはボット エミュレータ内で実行できます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-122">Your bot can run within the Bot Emulator.</span></span> <span data-ttu-id="a7c27-123">これにより、ボットのコア ロジックの一部をテストし、メッセージの大まかなレイアウトを確認し、簡単なテストを実行できます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-123">This enables you to test some of the core logic of the bot, see a rough layout of messages, and perform simple tests.</span></span> <span data-ttu-id="a7c27-124">以下の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-124">Following are the steps:</span></span>

1. <span data-ttu-id="a7c27-125">コードをローカルで実行します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-125">Run the code locally.</span></span>
2. <span data-ttu-id="a7c27-126">ボット エミュレーターを起動し、URL を設定します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-126">Launch the Bot Emulator and set the URL:</span></span>
   * <span data-ttu-id="a7c27-127">Node.js: `http://localhost:3978/api/messages`</span><span class="sxs-lookup"><span data-stu-id="a7c27-127">Node.js: `http://localhost:3978/api/messages`</span></span>
   * <span data-ttu-id="a7c27-128">.NET/C#: `http://localhost:3979/api/messages`</span><span class="sxs-lookup"><span data-stu-id="a7c27-128">.NET/C#: `http://localhost:3979/api/messages`</span></span>
3. <span data-ttu-id="a7c27-129">既定の環境変数と一致するように、Microsoft アプリ ID と Microsoft アプリ パスワードを空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="a7c27-129">Leave the Microsoft app ID and Microsoft app password blank, to match the default environment variables.</span></span>

## <a name="locally-hosted"></a><span data-ttu-id="a7c27-130">ローカルでホスト</span><span class="sxs-lookup"><span data-stu-id="a7c27-130">Locally hosted</span></span>

<span data-ttu-id="a7c27-131">Microsoft Teams完全にクラウドベースの製品であり、アクセスするすべてのサービスが HTTPS エンドポイントを使用してパブリックに利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7c27-131">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available publicly using HTTPS endpoints.</span></span> <span data-ttu-id="a7c27-132">したがって、アプリをTeams内で動作させるには、選択したクラウドにコードを発行するか、ローカルで実行しているインスタンスを外部からアクセスできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7c27-132">Therefore, to enable your app to work within Teams, you need to either publish the code to the cloud of your choice or make our local running instance externally accessible.</span></span> <span data-ttu-id="a7c27-133">私たちは、トンネリングソフトウェアで後者を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-133">We can do the latter with tunneling software.</span></span>

<span data-ttu-id="a7c27-134">任意のツールを使用できますが、使用するポートの外部アドレス指定可能な URL を作成する [ngrok](https://ngrok.com/download)を使用し、お勧めします。</span><span class="sxs-lookup"><span data-stu-id="a7c27-134">Although you can use any tool of your choice, we use and recommend [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span> 

<span data-ttu-id="a7c27-135">**Microsoft Teams アプリをローカルで実行する準備として ngrok をセットアップするには**</span><span class="sxs-lookup"><span data-stu-id="a7c27-135">**To set up ngrok in preparation for running your Microsoft Teams app locally**</span></span>

1. <span data-ttu-id="a7c27-136">ターミナル アプリケーションにインストールngrok.exeディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-136">Go to the directory where you have ngrok.exe installed in a terminal application.</span></span> <span data-ttu-id="a7c27-137">この手順を回避するために、パス変数として追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-137">You may want to add it as a path variable to avoid this step.</span></span>
2. <span data-ttu-id="a7c27-138">たとえば、 `ngrok http 3978 --host-header=localhost:3978` を実行するか、必要に応じてポート番号を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-138">Run, for example, `ngrok http 3978 --host-header=localhost:3978`, or replace the port number as needed.</span></span>
   <span data-ttu-id="a7c27-139">これにより、指定したポートに表示される ngrok が起動します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-139">This launches ngrok to list on the port you specify.</span></span> <span data-ttu-id="a7c27-140">その代わりに、ngrok が実行されている間有効な外部アドレス指定可能な URL が提供されます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-140">In return, it gives you an externally addressable URL valid for as long as ngrok is running.</span></span>

> [!NOTE]
> <span data-ttu-id="a7c27-141">ngrok を停止して再起動すると、URL が変更されます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-141">If you stop and restart ngrok, the URL changes.</span></span>

<span data-ttu-id="a7c27-142">使用している機能に基づいてプロジェクトで ngrok を使用するには、この URL エンドポイントを使用するために、コード、構成、およびファイルのmanifest.js内のすべての URL 参照を置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7c27-142">To use ngrok in your project based on the capabilities you are using, you must replace all URL references in your code, configuration, and manifest.json file to use this URL endpoint.</span></span>

<span data-ttu-id="a7c27-143">Microsoft Bot Frameworkに登録されているボットの場合は、この新しい ngrok エンドポイントを使用するようにボットのメッセージング エンドポイントを更新します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-143">For bots registered in the Microsoft Bot Framework, update the bot's messaging endpoint to use this new ngrok endpoint.</span></span> <span data-ttu-id="a7c27-144">たとえば、「 `https://2d1224fb.ngrok.io/api/messages` 」のように入力します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-144">For example, `https://2d1224fb.ngrok.io/api/messages`.</span></span> <span data-ttu-id="a7c27-145">ボットの応答を Bot Framework ポータルの [テスト チャット] ウィンドウでテストすることで、ngrok が動作していることを検証できます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-145">You can validate that ngrok is working by testing the bot response in the Bot Framework portal's Test chat window.</span></span> <span data-ttu-id="a7c27-146">この場合も、エミュレーターと同様に、このテストではTeams固有の機能にアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="a7c27-146">Again, like the emulator, this test does not permit you to access Teams-specific functionality.</span></span>

> [!NOTE]
> <span data-ttu-id="a7c27-147">ボットのメッセージング エンドポイントを更新するには、Bot Framework を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7c27-147">To update the messaging endpoint for a bot, you must use the Bot Framework.</span></span> <span data-ttu-id="a7c27-148">ボット フレームワーク の [ボットのリストでボットを](https://dev.botframework.com/bots)選択します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-148">Select your bot in [your list of bots in Bot Framework](https://dev.botframework.com/bots).</span></span> <span data-ttu-id="a7c27-149">ボットをMicrosoft Azureに移行する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a7c27-149">You do not need to migrate your bot to Microsoft Azure.</span></span> <span data-ttu-id="a7c27-150">[また、App Studio](~/concepts/build-and-test/app-studio-overview.md)を使用してメッセージング エンドポイントを更新することもできます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-150">You can also update your messaging endpoint through [App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="cloud-hosted"></a><span data-ttu-id="a7c27-151">クラウド ホスト型</span><span class="sxs-lookup"><span data-stu-id="a7c27-151">Cloud-hosted</span></span>

<span data-ttu-id="a7c27-152">外部でアドレス指定可能なサービスを使用して、開発コードと実稼働コード、および HTTPS エンドポイントをホストできます。</span><span class="sxs-lookup"><span data-stu-id="a7c27-152">You can use any externally addressable service to host your development and production code and their HTTPS endpoints.</span></span> <span data-ttu-id="a7c27-153">機能が同じサービスに存在するとは期待されません。</span><span class="sxs-lookup"><span data-stu-id="a7c27-153">There is no expectation that your capabilities reside on the same service.</span></span> <span data-ttu-id="a7c27-154">ファイル内のオブジェクトにリストされているMicrosoft Teamsアプリからすべてのドメインにアクセス [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) する必要 `manifest.json` があります。</span><span class="sxs-lookup"><span data-stu-id="a7c27-154">We require all domains to be accessed from your Microsoft Teams apps listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) object in the `manifest.json` file.</span></span>

> [!NOTE]
> <span data-ttu-id="a7c27-155">セキュリティで保護された環境を確保するには、参照する正確なドメインとサブドメインについて明確にし、それらのドメインを制御する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7c27-155">To ensure a secure environment, be explicit about the exact domain and subdomains you reference and those domains must be in your control.</span></span> <span data-ttu-id="a7c27-156">たとえば、 `*.azurewebsites.net` お勧 `contoso.azurewebsites.net` めできません。</span><span class="sxs-lookup"><span data-stu-id="a7c27-156">For example, `*.azurewebsites.net` is not recommended, however `contoso.azurewebsites.net` is recommended.</span></span>

## <a name="load-and-run-your-experience"></a><span data-ttu-id="a7c27-157">エクスペリエンスを読み込んで実行する</span><span class="sxs-lookup"><span data-stu-id="a7c27-157">Load and run your experience</span></span>

<span data-ttu-id="a7c27-158">Microsoft Teams内でエクスペリエンスを読み込んで実行するには、パッケージを作成してTeamsにアップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7c27-158">To load and run your experience within Microsoft Teams, you need to create a package and upload it into Teams.</span></span> <span data-ttu-id="a7c27-159">詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7c27-159">For more information, see:</span></span>

* <span data-ttu-id="a7c27-160">[Microsoft Teams アプリのパッケージを作成します](~/concepts/build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a7c27-160">[Create the package for your Microsoft Teams app](~/concepts/build-and-test/apps-package.md).</span></span>
* <span data-ttu-id="a7c27-161">[アプリを Microsoft Teams でアップロード](~/concepts/deploy-and-publish/apps-upload.md)します。</span><span class="sxs-lookup"><span data-stu-id="a7c27-161">[Upload your app in Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="a7c27-162">次の手順</span><span class="sxs-lookup"><span data-stu-id="a7c27-162">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="a7c27-163">テスト データを環境に追加する</span><span class="sxs-lookup"><span data-stu-id="a7c27-163">Add test data to your environment</span></span>](~/concepts/build-and-test/test-data.md)

