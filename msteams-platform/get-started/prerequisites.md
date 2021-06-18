---
title: 開始方法 - 前提条件
author: adrianhall
description: Microsoft Teams アプリの開発を開始し、環境をセットアップする方法について説明します。
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 6496d238b3858c1df974732fa57c28eed7c54eb2
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994190"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="10747-103">前提条件: Microsoft Teams アプリ開発の開始</span><span class="sxs-lookup"><span data-stu-id="10747-103">Prerequisites: Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="10747-104">最初の Teams アプリを作成する前に、いくつかのツールをインストールし、開発環境をセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10747-104">Before your create your first Teams app, you must install a few tools and set up your development environment.</span></span>

## <a name="install-required-tools"></a><span data-ttu-id="10747-105">必要なツールのインストール</span><span class="sxs-lookup"><span data-stu-id="10747-105">Install required tools</span></span>

<span data-ttu-id="10747-106">必要なツールの一部は、Teams アプリの構築方法によって異なっています。</span><span class="sxs-lookup"><span data-stu-id="10747-106">Some of the tools you need depend on how you you prefer to build your Teams app:</span></span>

- <span data-ttu-id="10747-107">[Node.js](https://nodejs.org/en/download/) (最新の v14 LTS リリースを使用する)</span><span class="sxs-lookup"><span data-stu-id="10747-107">[Node.js](https://nodejs.org/en/download/) (use the latest v14 LTS release)</span></span>
- <span data-ttu-id="10747-108">Microsoft [Edge](https://www.microsoft.com/edge) (推奨) や[Google Chrome](https://www.google.com/chrome/)などの開発者ツールを含むブラウザー</span><span class="sxs-lookup"><span data-stu-id="10747-108">A browser with developer tools - such as [Microsoft Edge](https://www.microsoft.com/edge) (recommended) or [Google Chrome](https://www.google.com/chrome/)</span></span>
- <span data-ttu-id="10747-109">JavaScript、TypeScript、または SharePoint Framework (SPFx) を使用して開発する場合は、Visual Studio [コードバージョン](https://code.visualstudio.com/download)1.55 以降をインストールします。</span><span class="sxs-lookup"><span data-stu-id="10747-109">If you are developing with JavaScript, TypeScript, or the SharePoint Framework (SPFx), install [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 or later.</span></span>  
- <span data-ttu-id="10747-110">.NET を使用して開発する場合は [、2019 Visual Studioインストールします](https://visualstudio.com/download)。</span><span class="sxs-lookup"><span data-stu-id="10747-110">If you are developing with .NET, install [Visual Studio 2019](https://visualstudio.com/download).</span></span> <span data-ttu-id="10747-111">必ず、ASP.NET **Web 開発ワークロードまたは** **.NET Core クロスプラットフォーム開発ワークロードをインストール** します。</span><span class="sxs-lookup"><span data-stu-id="10747-111">Ensure you install the **ASP.NET and web development** or **.NET Core cross-platform development** workload.</span></span>

> [!WARNING]
> <span data-ttu-id="10747-112">Node v15 以降でパッケージ `npm@7` 化された既知の問題があります。</span><span class="sxs-lookup"><span data-stu-id="10747-112">There are known issues with `npm@7`, packaged with Node v15 and later.</span></span> <span data-ttu-id="10747-113">実行中に問題がある場合は `npm install` 、Node v14 (LTS) を使用している必要があります。</span><span class="sxs-lookup"><span data-stu-id="10747-113">If you have problems running `npm install`, ensure you're using Node v14 (LTS)</span></span>

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="10747-114">Teams サーバーをインストールToolkit</span><span class="sxs-lookup"><span data-stu-id="10747-114">Install the Teams Toolkit</span></span>

<span data-ttu-id="10747-115">Teams Toolkitは、アプリ用のクラウド リソースのプロビジョニングと展開、Teams ストアへの発行など、ツールを使用して開発プロセスを簡略化するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="10747-115">The Teams Toolkit helps simplify the development process with tools to provision and deploy cloud resources for your app, publish to the Teams store, and more.</span></span> <span data-ttu-id="10747-116">ツールキットは、コード、Visual Studio、または CLI (Visual Studio) として使用できます `teamsfx` 。</span><span class="sxs-lookup"><span data-stu-id="10747-116">You can use the toolkit with Visual Studio Code, Visual Studio, or as a CLI (called `teamsfx`).</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="10747-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="10747-117">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="10747-118">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="10747-118">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="10747-119">[拡張機能] ビューを選択します **(Ctrl + Shift +**  /   **>** X</span><span class="sxs-lookup"><span data-stu-id="10747-119">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="10747-120">検索ボックスに **、「Teams」と入力Toolkit。**</span><span class="sxs-lookup"><span data-stu-id="10747-120">In the search box, enter **Teams Toolkit**.</span></span>
1. <span data-ttu-id="10747-121">Teams サーバーの横にある緑色のインストール ボタンをToolkit。</span><span class="sxs-lookup"><span data-stu-id="10747-121">Select the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="10747-122">Teams ファイルは、コード マーケットプレースToolkitでVisual Studio [できます](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。</span><span class="sxs-lookup"><span data-stu-id="10747-122">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="10747-123">次のツールは、必要に応Visual Studioコード拡張機能によってインストールできます。</span><span class="sxs-lookup"><span data-stu-id="10747-123">The following tools can be installed by the Visual Studio Code extension when they are needed.</span></span> <span data-ttu-id="10747-124">既にインストールされている場合は、インストールされているバージョンを代わりに使用できます。</span><span class="sxs-lookup"><span data-stu-id="10747-124">If already installed, the installed version can be used instead.</span></span> <span data-ttu-id="10747-125">WSL を含む Linux を使用する場合は、使用する前に次のツールをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10747-125">If using Linux including WSL, you must install these tools before use:</span></span>

- [<span data-ttu-id="10747-126">Azure Functions コア ツール</span><span class="sxs-lookup"><span data-stu-id="10747-126">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="10747-127">Azure Functions Core Tools は、Azure でサービスを実行するときに必要な認証ヘルパーを含む、ローカル デバッグ実行時にバックエンド コンポーネントをローカルで実行するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="10747-127">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span> <span data-ttu-id="10747-128">プロジェクト ディレクトリ内にインストールされます (npm を使用 `devDependencies` )。</span><span class="sxs-lookup"><span data-stu-id="10747-128">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="10747-129">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="10747-129">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="10747-130">.NET SDK は、ローカル デバッグと Azure Functions アプリの展開用にカスタマイズされたバインドをインストールするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="10747-130">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span> <span data-ttu-id="10747-131">.NET 3.1 (以降) SDK をグローバルにインストールしていない場合は、ポータブル バージョンをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="10747-131">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version can be installed.</span></span>

- [<span data-ttu-id="10747-132">ngrok</span><span class="sxs-lookup"><span data-stu-id="10747-132">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="10747-133">Teams アプリの一部の機能 (会話型ボット、メッセージング拡張機能、受信 Webhook) では、受信接続が必要です。</span><span class="sxs-lookup"><span data-stu-id="10747-133">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span> <span data-ttu-id="10747-134">開発システムをトンネル経由で Teams に公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10747-134">You need to expose your development system to Teams through a tunnel.</span></span> <span data-ttu-id="10747-135">タブのみを含むアプリでは、トンネルは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="10747-135">A tunnel is not required for apps that only include tabs.</span></span> <span data-ttu-id="10747-136">このパッケージは、(npm を使用して) プロジェクト ディレクトリ内にインストールされます `devDependencies` 。</span><span class="sxs-lookup"><span data-stu-id="10747-136">This package is installed within the project directory (using npm `devDependencies`).</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="10747-137">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="10747-137">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="10747-138">2019 Visual Studioを使用して、.NET で Blazor Server を使用して Teams アプリを開発できます。</span><span class="sxs-lookup"><span data-stu-id="10747-138">You can use Visual Studio 2019 to develop Teams apps with Blazor Server in .NET.</span></span> <span data-ttu-id="10747-139">.NET で Teams アプリを開発する予定がない場合は、Teams アプリの Visual Studio コード バージョンをインストールToolkit。</span><span class="sxs-lookup"><span data-stu-id="10747-139">If you are not intending to develop Teams apps in .NET, install the Visual Studio Code version of Teams Toolkit.</span></span>

<span data-ttu-id="10747-140">Teams の拡張機能をToolkitするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="10747-140">To install the Teams Toolkit extension:</span></span>

1. <span data-ttu-id="10747-141">2019 Visual Studioを開きます。</span><span class="sxs-lookup"><span data-stu-id="10747-141">Open Visual Studio 2019.</span></span>
1. <span data-ttu-id="10747-142">[拡張機能 **の管理**  >  **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="10747-142">Select **Extensions** > **Manage Extensions**.</span></span>
1. <span data-ttu-id="10747-143">検索ボックスに **、「Teams」と入力Toolkit。**</span><span class="sxs-lookup"><span data-stu-id="10747-143">In the search box, enter **Teams Toolkit**.</span></span>
1. <span data-ttu-id="10747-144">Teams の拡張機能をToolkitし、[ダウンロード] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="10747-144">Select the Teams Toolkit extension and select **Download**.</span></span>

<span data-ttu-id="10747-145">拡張機能はダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="10747-145">The extension can be downloaded.</span></span> <span data-ttu-id="10747-146">2019 Visual Studio閉じて、拡張機能をインストールします。</span><span class="sxs-lookup"><span data-stu-id="10747-146">Close Visual Studio 2019 to install the extension.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="10747-147">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="10747-147">Command line</span></span>](#tab/cli)

<span data-ttu-id="10747-148">TeamsFx CLI をインストールするには、パッケージ マネージャーを `npm` 使用します。</span><span class="sxs-lookup"><span data-stu-id="10747-148">To install the TeamsFx CLI, use the `npm` package manager:</span></span>

``` bash
npm install -g @microsoft/teamsfx-cli
```

<span data-ttu-id="10747-149">構成によっては、CLI のインストールに使用 `sudo` する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="10747-149">Depending on your configuration, you may need to use `sudo` to install the CLI:</span></span>

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

<span data-ttu-id="10747-150">これは、Linux および macOS システムではより一般的です。</span><span class="sxs-lookup"><span data-stu-id="10747-150">This is more common on Linux and macOS systems.</span></span>

<span data-ttu-id="10747-151">npm グローバル キャッシュを PATH に追加してください。</span><span class="sxs-lookup"><span data-stu-id="10747-151">Ensure you add the npm global cache to your PATH.</span></span> <span data-ttu-id="10747-152">これは、通常、インストーラーの一部としてNode.jsされます。</span><span class="sxs-lookup"><span data-stu-id="10747-152">This is normally done as part of the Node.js installer.</span></span>  

<span data-ttu-id="10747-153">コマンドで CLI を使用 `teamsfx` できます。</span><span class="sxs-lookup"><span data-stu-id="10747-153">You can use the CLI with the `teamsfx` command.</span></span> <span data-ttu-id="10747-154">コマンドを実行して動作を確認します `teamsfx -h` 。</span><span class="sxs-lookup"><span data-stu-id="10747-154">Verify that the command is working by running `teamsfx -h`.</span></span>

> [!CAUTION]
> <span data-ttu-id="10747-155">PowerShell ターミナルで TeamsFx を実行する前に、PowerShell の "リモート署名済み" 実行ポリシーを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10747-155">Before you can run TeamsFx in PowerShell terminals, you must enable the "remote signed" execution policy for PowerShell.</span></span> <span data-ttu-id="10747-156">詳細については [、PowerShell のドキュメントを参照してください](/powershell/module/microsoft.powershell.core/about/about_signing)。</span><span class="sxs-lookup"><span data-stu-id="10747-156">For more information, refer to the [PowerShell documentation](/powershell/module/microsoft.powershell.core/about/about_signing).</span></span>

---

## <a name="install-optional-tools"></a><span data-ttu-id="10747-157">オプション のツールをインストールする</span><span class="sxs-lookup"><span data-stu-id="10747-157">Install optional tools</span></span>

<span data-ttu-id="10747-158">アプリ開発用のブラウザー ツールをインストールします。</span><span class="sxs-lookup"><span data-stu-id="10747-158">Install browser tools for app development.</span></span> <span data-ttu-id="10747-159">たとえば、アプリが React で記述されている場合は、React 開発者ツールを使用できます。</span><span class="sxs-lookup"><span data-stu-id="10747-159">For instance, if your app is written with React, you can use React Developer Tools:</span></span>

- [<span data-ttu-id="10747-160">React Developer Tools for Chrome</span><span class="sxs-lookup"><span data-stu-id="10747-160">React Developer Tools for Chrome</span></span>](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

<span data-ttu-id="10747-161">Azure に格納されているデータにアクセスするか、Azure で Teams アプリのクラウドベースのバックエンドを展開する場合は、次のツールをインストールします。</span><span class="sxs-lookup"><span data-stu-id="10747-161">If you want to access data stored in Azure or deploy a cloud-based backend for your Teams app in Azure, install these tools:</span></span>

- [<span data-ttu-id="10747-162">Azure Tools for Visual Studio コード</span><span class="sxs-lookup"><span data-stu-id="10747-162">Azure Tools for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [<span data-ttu-id="10747-163">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="10747-163">Azure CLI</span></span>](/cli/azure/install-azure-cli)

<span data-ttu-id="10747-164">Microsoft Graph データを使用する場合は、Microsoft Graph エクスプローラーについて説明し、ブックマークする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10747-164">If you work with Microsoft Graph data, you should learn about and bookmark the Microsoft Graph Explorer.</span></span> <span data-ttu-id="10747-165">このブラウザー ベースのツールを使用すると、アプリの外部で Microsoft Graph にクエリを実行できます。</span><span class="sxs-lookup"><span data-stu-id="10747-165">This browser-based tool allows you to query Microsoft Graph outside of an app.</span></span>

- [<span data-ttu-id="10747-166">Microsoft Graph Explorer</span><span class="sxs-lookup"><span data-stu-id="10747-166">Microsoft Graph Explorer</span></span>](https://developer.microsoft.com/graph/graph-explorer)

<span data-ttu-id="10747-167">Teams の開発者ポータルを使用すると、組織や Teams ストアを含む Teams アプリを構成、管理、配布できます。</span><span class="sxs-lookup"><span data-stu-id="10747-167">With the Developer Portal for Teams, you can configure, manage, and distribute your Teams app including to your organization or the Teams store.</span></span>

- [<span data-ttu-id="10747-168">Teams の開発者ポータル</span><span class="sxs-lookup"><span data-stu-id="10747-168">Developer Portal for Teams</span></span>](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a><span data-ttu-id="10747-169">サイドローディングを有効にする</span><span class="sxs-lookup"><span data-stu-id="10747-169">Enable sideloading</span></span>

<span data-ttu-id="10747-170">開発中は、配布せずに Teams 内でアプリを読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="10747-170">During development, you must load your app within Teams without distributing it.</span></span> <span data-ttu-id="10747-171">これは"サイドローディング" と呼ばれる。</span><span class="sxs-lookup"><span data-stu-id="10747-171">This is known as "sideloading".</span></span>

1. <span data-ttu-id="10747-172">Teams アカウントを持っている場合は、Teams でアプリをサイドロードできる場合を確認します。</span><span class="sxs-lookup"><span data-stu-id="10747-172">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>

    1. <span data-ttu-id="10747-173">Teams クライアントで、[アプリ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="10747-173">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="10747-174">カスタム アプリをアップロードする **オプションを探します**。</span><span class="sxs-lookup"><span data-stu-id="10747-174">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Teams でカスタム アプリをアップロードできる場所を示す図。":::

> [!NOTE]
> <span data-ttu-id="10747-176">アプリをサイドロードできない場合は、Teams 管理者に問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="10747-176">If you still cannot sideload apps, talk to your Teams administrator.</span></span> <span data-ttu-id="10747-177">詳細については [、「カスタム Teams アプリを有効にする」と「カスタム アプリのアップロードを有効にする」](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="10747-177">See [enable custom Teams apps and turn on custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for details.</span></span>

## <a name="get-a-free-teams-developer-tenant-optional"></a><span data-ttu-id="10747-178">無料の Teams 開発者テナントを取得する (オプション)</span><span class="sxs-lookup"><span data-stu-id="10747-178">Get a free Teams developer tenant (optional)</span></span>

<span data-ttu-id="10747-179">サイドロード オプションが表示されない場合、または Teams アカウントがない場合は、M365 開発者プログラムに参加することで、無料の Teams 開発者アカウントを取得できます。</span><span class="sxs-lookup"><span data-stu-id="10747-179">If you cannot see the sideload option, or you do not have a Teams account, you can get a free Teams developer account by joining the M365 developer program.</span></span>  <span data-ttu-id="10747-180">登録プロセスには約 2 分かかります。</span><span class="sxs-lookup"><span data-stu-id="10747-180">The registration process takes approximately two minutes.</span></span>

1. <span data-ttu-id="10747-181">[Microsoft 365 開発者プログラムに移動します](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="10747-181">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="10747-182">[今 **すぐ参加] を** 選択し、画面の指示に従います。</span><span class="sxs-lookup"><span data-stu-id="10747-182">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="10747-183">ようこそ画面にアクセスすると **、[E5 サブスクリプションの設定] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="10747-183">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="10747-184">管理者アカウントを設定します。</span><span class="sxs-lookup"><span data-stu-id="10747-184">Set up your administrator account.</span></span> <span data-ttu-id="10747-185">完了すると、次のような画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="10747-185">Once you finish, you should see a screen like this.</span></span>

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後に表示される例。":::

1. <span data-ttu-id="10747-187">セットアップした管理者アカウントを使用して Teams にサインインします。</span><span class="sxs-lookup"><span data-stu-id="10747-187">Sign in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="10747-188">[カスタム アプリをアップロードする **] オプションが追加されたのか確認** します。</span><span class="sxs-lookup"><span data-stu-id="10747-188">Verify if you now have the **Upload a custom app** option.</span></span>

## <a name="get-a-free-azure-account"></a><span data-ttu-id="10747-189">無料の Azure アカウントを取得する</span><span class="sxs-lookup"><span data-stu-id="10747-189">Get a free Azure account</span></span>

<span data-ttu-id="10747-190">アプリをホストするか、Azure 内のリソースにアクセスする場合は、Azure サブスクリプションが必要です。</span><span class="sxs-lookup"><span data-stu-id="10747-190">If you wish to host your app or access resources within Azure, you must have an Azure subscription.</span></span>  <span data-ttu-id="10747-191">開始する [前に無料アカウント](https://azure.microsoft.com/free/) を作成できます。</span><span class="sxs-lookup"><span data-stu-id="10747-191">You can [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a><span data-ttu-id="10747-192">Microsoft 365 および Azure アカウントにサインインする</span><span class="sxs-lookup"><span data-stu-id="10747-192">Sign in to your Microsoft 365 and Azure accounts</span></span>

<span data-ttu-id="10747-193">次の 2 つのアカウントにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="10747-193">You must have access to two accounts:</span></span>

- <span data-ttu-id="10747-194">Microsoft 365 アカウントの資格情報。</span><span class="sxs-lookup"><span data-stu-id="10747-194">Your Microsoft 365 account credentials.</span></span> <span data-ttu-id="10747-195">これは、Teams へのサインインに使用するアカウントです。</span><span class="sxs-lookup"><span data-stu-id="10747-195">This is the account that you use to sign in to Teams.</span></span> <span data-ttu-id="10747-196">Microsoft 365 開発者プログラム テナントを使用している場合は、プログラムの登録時に設定した管理者アカウントです。</span><span class="sxs-lookup"><span data-stu-id="10747-196">If you're using an Microsoft 365 developer program tenant, this is the admin account you set up when you registered for the program.</span></span>
- - <span data-ttu-id="10747-197">Azure 資格情報。</span><span class="sxs-lookup"><span data-stu-id="10747-197">Your Azure credentials.</span></span> <span data-ttu-id="10747-198">これは、Azure Portal へのアクセスと、アプリをサポートする新しいクラウド リソースのプロビジョニングに使用するアカウントです。</span><span class="sxs-lookup"><span data-stu-id="10747-198">This is the account that you use to access the Azure Portal and for provisioning new cloud resources to support your app.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="10747-199">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="10747-199">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="10747-200">Open Visual Studio コード</span><span class="sxs-lookup"><span data-stu-id="10747-200">Open Visual Studio Code</span></span>
1. <span data-ttu-id="10747-201">サイドバーでTeamsアイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="10747-201">Select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="10747-203">**[M365 にサインインする] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="10747-203">Select **Sign in to M365**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="サインインに使用する [アカウント] セクションの場所。":::

1. <span data-ttu-id="10747-205">サインイン プロセスは、通常の Web ブラウザーの使用を開始します。</span><span class="sxs-lookup"><span data-stu-id="10747-205">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="10747-206">M365 アカウントのサインイン プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="10747-206">Complete the sign-in process for your M365 account.</span></span> <span data-ttu-id="10747-207">ブラウザーを閉じて、ブラウザーに戻るメッセージが表示Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="10747-207">You are prompted when you can close the browser and return to Visual Studio Code.</span></span>
1. <span data-ttu-id="10747-208">データ内のTeams Toolkitに戻Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="10747-208">Return to the Teams Toolkit within Visual Studio Code.</span></span>
1. <span data-ttu-id="10747-209">[Azure **にサインインする] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="10747-209">Select **Sign in to Azure**.</span></span>

    > [!TIP]
    > <span data-ttu-id="10747-210">Azure Account 拡張機能がインストールされ、同じアカウントを使用している場合は、この手順を省略できます。</span><span class="sxs-lookup"><span data-stu-id="10747-210">If you have the Azure Account extension installed and are using the same account, you can skip this step.</span></span> <span data-ttu-id="10747-211">他の拡張機能で使用しているアカウントと同じアカウントを使用します。</span><span class="sxs-lookup"><span data-stu-id="10747-211">Use the same account as you are using in other extensions.</span></span>

1. <span data-ttu-id="10747-212">サインイン プロセスは、通常の Web ブラウザーの使用を開始します。</span><span class="sxs-lookup"><span data-stu-id="10747-212">The sign-in process starts using your normal web browser.</span></span>  <span data-ttu-id="10747-213">Azure アカウントのサインイン プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="10747-213">Complete the sign-in process for your Azure account.</span></span> <span data-ttu-id="10747-214">ブラウザーを閉じて、ブラウザーに戻るメッセージが表示Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="10747-214">You are prompted when you can close the browser and return to Visual Studio Code.</span></span>

<span data-ttu-id="10747-215">完了すると、 **サイドバーの [ACCOUNTS]** セクションには、使用可能な Azure サブスクリプションの数と共に、2 つのアカウントが個別に表示されます。</span><span class="sxs-lookup"><span data-stu-id="10747-215">When complete, the **ACCOUNTS** section of the sidebar shows the two accounts separately, together with the number of usable Azure subscriptions available to you.</span></span> <span data-ttu-id="10747-216">使用可能な Azure サブスクリプションが少なくとも 1 つ用意されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="10747-216">Ensure you have at least one usable Azure subscription available.</span></span> <span data-ttu-id="10747-217">サインインしていない場合は、サインアウトして別のアカウントを使用します。</span><span class="sxs-lookup"><span data-stu-id="10747-217">If not, sign out and use a different account.</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="10747-218">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="10747-218">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="10747-219">Visual Studio 2019 では、必要に応じて各サービスにログインするように求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="10747-219">Visual Studio 2019 prompts you to log in to each service as required.</span></span> <span data-ttu-id="10747-220">事前に M365 アカウントと Azure アカウントにサインインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="10747-220">You do not need to sign in to your M365 and Azure accounts in advance.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="10747-221">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="10747-221">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="10747-222">TeamsFx CLI を使用Microsoft 365サインインして、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="10747-222">Sign in to Microsoft 365 with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login m365
    ```

    <span data-ttu-id="10747-223">サインイン プロセスは、通常の Web ブラウザーの使用を開始します。</span><span class="sxs-lookup"><span data-stu-id="10747-223">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="10747-224">M365 アカウントのサインイン プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="10747-224">Complete the sign-in process for your M365 account.</span></span> <span data-ttu-id="10747-225">ブラウザーを閉じるときにメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="10747-225">You are prompted when you can close the browser.</span></span>

2. <span data-ttu-id="10747-226">TeamsFx CLI を使用して Azure にサインインします。</span><span class="sxs-lookup"><span data-stu-id="10747-226">Sign in to Azure with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login azure
    ```

    <span data-ttu-id="10747-227">サインイン プロセスは、通常の Web ブラウザーの使用を開始します。</span><span class="sxs-lookup"><span data-stu-id="10747-227">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="10747-228">Azure アカウントのサインイン プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="10747-228">Complete the sign-in process for your Azure account.</span></span> <span data-ttu-id="10747-229">ブラウザーを閉じるときにメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="10747-229">You are prompted when you can close the browser.</span></span>

<span data-ttu-id="10747-230">アカウント ログインは、ユーザーと TeamsFx CLI Visual Studio Code共有されます。</span><span class="sxs-lookup"><span data-stu-id="10747-230">The account logins are shared between Visual Studio Code and the TeamsFx CLI.</span></span>

---

<span data-ttu-id="10747-231">開発環境が構成されたので、最初のアプリを作成、ビルド、およびTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="10747-231">Now that your development environment is configured, you can create, build, and deploy your first Teams app.</span></span>

## <a name="see-also"></a><span data-ttu-id="10747-232">関連項目</span><span class="sxs-lookup"><span data-stu-id="10747-232">See also</span></span>

- [<span data-ttu-id="10747-233">Blazor を使用してTeamsアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="10747-233">Create your first Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="10747-234">アプリを使用してTeamsアプリをSharePoint Frameworkする (SPFx)</span><span class="sxs-lookup"><span data-stu-id="10747-234">Create your first Teams app using SharePoint Framework (SPFx)</span></span>](first-app-spfx.md)
- [<span data-ttu-id="10747-235">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="10747-235">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="10747-236">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="10747-236">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="10747-237">次の手順</span><span class="sxs-lookup"><span data-stu-id="10747-237">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="10747-238">アプリを使用してTeamsアプリをReact</span><span class="sxs-lookup"><span data-stu-id="10747-238">Create your first Teams app using React</span></span>](first-app-react.md)
