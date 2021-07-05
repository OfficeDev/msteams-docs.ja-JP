---
title: 開始方法 - 前提条件
author: adrianhall
description: アプリ開発の開始と環境Microsoft Teamsする方法について学習します。
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 4796d37aa0ef904805fbfe2956f9e1d49960bfe9
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254267"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="e3a53-103">前提条件: アプリ開発Microsoft Teams開始する</span><span class="sxs-lookup"><span data-stu-id="e3a53-103">Prerequisites: Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="e3a53-104">最初のアプリの作成を開始するTeams、いくつかのツールをインストールして、開発環境をセットアップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-104">Before you begin with creating your first Teams app, you must install a few tools and set up your development environment.</span></span>

## <a name="install-required-tools"></a><span data-ttu-id="e3a53-105">必要なツールのインストール</span><span class="sxs-lookup"><span data-stu-id="e3a53-105">Install required tools</span></span>

<span data-ttu-id="e3a53-106">必要なツールの一部は、アプリのビルド方法によってTeamsがあります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-106">Some of the tools you need depend on how you prefer to build your Teams app:</span></span>

- <span data-ttu-id="e3a53-107">[Node.js](https://nodejs.org/en/download/) (最新の v14 LTS リリースを使用する)</span><span class="sxs-lookup"><span data-stu-id="e3a53-107">[Node.js](https://nodejs.org/en/download/) (use the latest v14 LTS release)</span></span>
- <span data-ttu-id="e3a53-108">開発者ツール (推奨) や[](https://www.microsoft.com/edge)Google [Chrome](https://www.google.com/chrome/)などのMicrosoft Edgeブラウザー</span><span class="sxs-lookup"><span data-stu-id="e3a53-108">A browser with developer tools, such as, [Microsoft Edge](https://www.microsoft.com/edge) (recommended) or [Google Chrome](https://www.google.com/chrome/)</span></span>
- <span data-ttu-id="e3a53-109">JavaScript、TypeScript、または SharePoint Framework (SPFx) を使用して開発する場合は、Visual Studio Code[バージョン](https://code.visualstudio.com/download)1.55 以降をインストールします。</span><span class="sxs-lookup"><span data-stu-id="e3a53-109">If you are developing with JavaScript, TypeScript, or the SharePoint Framework (SPFx), install [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 or later.</span></span>  
- <span data-ttu-id="e3a53-110">.NET を使用して開発している場合は[、2019 Visual Studioインストールします](https://visualstudio.com/download)。</span><span class="sxs-lookup"><span data-stu-id="e3a53-110">If you are developing with .NET, install [Visual Studio 2019](https://visualstudio.com/download).</span></span> <span data-ttu-id="e3a53-111">必ず、ASP.NET **Web 開発ワークロードまたは** **.NET Core クロス** プラットフォーム開発ワークロードをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e3a53-111">Ensure you install the **ASP.NET and web development** or **.NET Core cross-platform development** workload.</span></span>

> [!WARNING]
> <span data-ttu-id="e3a53-112">Node v15 以降でパッケージ `npm@7` 化された既知の問題があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-112">There are known issues with `npm@7`, packaged with Node v15 and later.</span></span> <span data-ttu-id="e3a53-113">実行中に問題がある場合は `npm install` 、Node v14 (LTS) を使用している必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-113">If you have problems running `npm install`, ensure you're using Node v14 (LTS)</span></span>

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="e3a53-114">サーバーをインストールTeams Toolkit</span><span class="sxs-lookup"><span data-stu-id="e3a53-114">Install the Teams Toolkit</span></span>

<span data-ttu-id="e3a53-115">このTeams Toolkitは、アプリのクラウド リソースをプロビジョニングおよび展開するツール、アプリ ストアに発行するツールを使用して開発プロセスを簡略化Teams役立ちます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-115">The Teams Toolkit helps simplify the development process with tools to provision and deploy cloud resources for your app, publish to the Teams store, and more.</span></span> <span data-ttu-id="e3a53-116">このツールキットは、Visual Studio Code、Visual Studio CLI (呼び出し) として使用できます `teamsfx` 。</span><span class="sxs-lookup"><span data-stu-id="e3a53-116">You can use the toolkit with Visual Studio Code, Visual Studio, or as a CLI (called `teamsfx`).</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="e3a53-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e3a53-117">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="e3a53-118">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-118">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="e3a53-119">[拡張機能 **] ビューを選択** します **(Ctrl + Shift + X**  /  **の場合は 、2** つ以上の拡張子を>**します**)。</span><span class="sxs-lookup"><span data-stu-id="e3a53-119">Select the **Extensions** view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="e3a53-120">検索ボックスに「Teams Toolkit」**と入力します**。</span><span class="sxs-lookup"><span data-stu-id="e3a53-120">In the search box, enter **Teams Toolkit**.</span></span>
1. <span data-ttu-id="e3a53-121">[インストール **] の** 横にある [インストール] をTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="e3a53-121">Select **Install** next to the Teams Toolkit.</span></span>

<span data-ttu-id="e3a53-122">また、マーケットプレースでTeams ToolkitをVisual Studio Code[できます](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。</span><span class="sxs-lookup"><span data-stu-id="e3a53-122">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="e3a53-123">次のツールは、必要に応Visual Studio Code拡張機能によってインストールできます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-123">The following tools can be installed by the Visual Studio Code extension when they are needed.</span></span> <span data-ttu-id="e3a53-124">既にインストールされている場合は、インストールされているバージョンを代わりに使用できます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-124">If already installed, the installed version can be used instead.</span></span> <span data-ttu-id="e3a53-125">WSL を含む Linux を使用する場合は、使用する前に次のツールをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-125">If using Linux including WSL, you must install these tools before use:</span></span>

- [<span data-ttu-id="e3a53-126">Azure Functions コア ツール</span><span class="sxs-lookup"><span data-stu-id="e3a53-126">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="e3a53-127">Azure Functions Core Tools は、Azure でサービスを実行するときに必要な認証ヘルパーを含む、ローカル デバッグ実行時にバックエンド コンポーネントをローカルで実行するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-127">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span> <span data-ttu-id="e3a53-128">プロジェクト ディレクトリ内にインストールされます (npm を使用 `devDependencies` )。</span><span class="sxs-lookup"><span data-stu-id="e3a53-128">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="e3a53-129">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="e3a53-129">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="e3a53-130">.NET SDK は、ローカル デバッグと Azure Functions アプリの展開用にカスタマイズされたバインドをインストールするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-130">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span> <span data-ttu-id="e3a53-131">.NET 3.1 (以降) SDK をグローバルにインストールしていない場合は、ポータブル バージョンをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-131">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version can be installed.</span></span>

- [<span data-ttu-id="e3a53-132">ngrok</span><span class="sxs-lookup"><span data-stu-id="e3a53-132">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="e3a53-133">一部Teamsアプリ機能 (会話型ボット、メッセージング拡張機能、受信 Webhook) では、受信接続が必要です。</span><span class="sxs-lookup"><span data-stu-id="e3a53-133">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span> <span data-ttu-id="e3a53-134">開発システムをトンネル経由でTeamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-134">You need to expose your development system to Teams through a tunnel.</span></span> <span data-ttu-id="e3a53-135">タブのみを含むアプリでは、トンネルは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="e3a53-135">A tunnel is not required for apps that only include tabs.</span></span> <span data-ttu-id="e3a53-136">このパッケージは、(npm を使用して) プロジェクト ディレクトリ内にインストールされます `devDependencies` 。</span><span class="sxs-lookup"><span data-stu-id="e3a53-136">This package is installed within the project directory (using npm `devDependencies`).</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="e3a53-137">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="e3a53-137">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="e3a53-138">2019 Visual Studioを使用して、.NET Teams Blazor Server を使用してアプリを開発できます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-138">You can use Visual Studio 2019 to develop Teams apps with Blazor Server in .NET.</span></span> <span data-ttu-id="e3a53-139">.NET でアプリを開発するTeams場合は、Visual Studio CodeバージョンをインストールTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="e3a53-139">If you are not intending to develop Teams apps in .NET, install the Visual Studio Code version of Teams Toolkit.</span></span>

<span data-ttu-id="e3a53-140">拡張機能をインストールTeams Toolkitするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-140">To install the Teams Toolkit extension:</span></span>

1. <span data-ttu-id="e3a53-141">2019 Visual Studioを開きます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-141">Open Visual Studio 2019.</span></span>
1. <span data-ttu-id="e3a53-142">[拡張機能 **の管理**  >  **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="e3a53-142">Select **Extensions** > **Manage Extensions**.</span></span>
1. <span data-ttu-id="e3a53-143">検索ボックスに「Teams Toolkit」**と入力します**。</span><span class="sxs-lookup"><span data-stu-id="e3a53-143">In the search box, enter **Teams Toolkit**.</span></span>
1. <span data-ttu-id="e3a53-144">拡張機能を選択Teams Toolkitし、[ダウンロード] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="e3a53-144">Select the Teams Toolkit extension and select **Download**.</span></span> <span data-ttu-id="e3a53-145">拡張機能がダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-145">The extension is downloaded.</span></span>
1. <span data-ttu-id="e3a53-146">2019 Visual Studio閉じて、拡張機能をインストールします。</span><span class="sxs-lookup"><span data-stu-id="e3a53-146">Close Visual Studio 2019 to install the extension.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="e3a53-147">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="e3a53-147">Command line</span></span>](#tab/cli)

<span data-ttu-id="e3a53-148">TeamsFx CLI をインストールするには、パッケージ マネージャーを `npm` 使用します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-148">To install the TeamsFx CLI, use the `npm` package manager:</span></span>

``` bash
npm install -g @microsoft/teamsfx-cli
```

<span data-ttu-id="e3a53-149">構成によっては、CLI のインストールに使用 `sudo` する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-149">Depending on your configuration, you may need to use `sudo` to install the CLI:</span></span>

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

<span data-ttu-id="e3a53-150">これは、Linux および macOS システムではより一般的です。</span><span class="sxs-lookup"><span data-stu-id="e3a53-150">This is more common on Linux and macOS systems.</span></span>

<span data-ttu-id="e3a53-151">npm グローバル キャッシュを PATH に追加してください。</span><span class="sxs-lookup"><span data-stu-id="e3a53-151">Ensure you add the npm global cache to your PATH.</span></span> <span data-ttu-id="e3a53-152">これは、通常、インストーラーの一部としてNode.jsされます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-152">This is normally done as part of the Node.js installer.</span></span>  

<span data-ttu-id="e3a53-153">コマンドで CLI を使用 `teamsfx` できます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-153">You can use the CLI with the `teamsfx` command.</span></span> <span data-ttu-id="e3a53-154">コマンドを実行して動作を確認します `teamsfx -h` 。</span><span class="sxs-lookup"><span data-stu-id="e3a53-154">Verify that the command is working by running `teamsfx -h`.</span></span>

> [!CAUTION]
> <span data-ttu-id="e3a53-155">PowerShell ターミナルで TeamsFx を実行する前に、PowerShell の "リモート署名済み" 実行ポリシーを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-155">Before you can run TeamsFx in PowerShell terminals, you must enable the "remote signed" execution policy for PowerShell.</span></span> <span data-ttu-id="e3a53-156">詳細については [、PowerShell のドキュメントを参照してください](/powershell/module/microsoft.powershell.core/about/about_signing)。</span><span class="sxs-lookup"><span data-stu-id="e3a53-156">For more information, refer to the [PowerShell documentation](/powershell/module/microsoft.powershell.core/about/about_signing).</span></span>

---

## <a name="install-optional-tools"></a><span data-ttu-id="e3a53-157">オプション のツールをインストールする</span><span class="sxs-lookup"><span data-stu-id="e3a53-157">Install optional tools</span></span>

<span data-ttu-id="e3a53-158">アプリ開発用のブラウザー ツールをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e3a53-158">Install browser tools for app development.</span></span> <span data-ttu-id="e3a53-159">たとえば、アプリがアプリを使用して作成されている場合React開発者ツールReact使用できます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-159">For instance, if your app is written with React, you can use React Developer Tools:</span></span>

- [<span data-ttu-id="e3a53-160">ReactChrome の開発者向けツール</span><span class="sxs-lookup"><span data-stu-id="e3a53-160">React Developer Tools for Chrome</span></span>](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

<span data-ttu-id="e3a53-161">Azure に格納されているデータにアクセスする場合、または Azure のアプリ用にクラウドベースのバックエンドを展開Teams、次のツールをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e3a53-161">If you want to access data stored in Azure or deploy a cloud-based backend for your Teams app in Azure, install these tools:</span></span>

- [<span data-ttu-id="e3a53-162">Azure Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e3a53-162">Azure Tools for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [<span data-ttu-id="e3a53-163">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e3a53-163">Azure CLI</span></span>](/cli/azure/install-azure-cli)

<span data-ttu-id="e3a53-164">Microsoft のデータをGraphする場合は、Microsoft データベース エクスプローラーについて説明し、ブックマークGraph必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-164">If you work with Microsoft Graph data, you should learn about and bookmark the Microsoft Graph Explorer.</span></span> <span data-ttu-id="e3a53-165">このブラウザー ベースのツールを使用すると、アプリの外部で Microsoft Graphクエリを実行できます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-165">This browser-based tool allows you to query Microsoft Graph outside of an app.</span></span>

- [<span data-ttu-id="e3a53-166">Microsoft Graph Explorer</span><span class="sxs-lookup"><span data-stu-id="e3a53-166">Microsoft Graph Explorer</span></span>](https://developer.microsoft.com/graph/graph-explorer)

<span data-ttu-id="e3a53-167">開発者ポータル for Teamsを使用すると、Teams アプリを構成、管理、および配布できます。組織または Teams ストアにTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-167">With the Developer Portal for Teams, you can configure, manage, and distribute your Teams app including to your organization or the Teams store.</span></span>

- [<span data-ttu-id="e3a53-168">Teams の開発者ポータル</span><span class="sxs-lookup"><span data-stu-id="e3a53-168">Developer Portal for Teams</span></span>](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a><span data-ttu-id="e3a53-169">サイドローディングを有効にする</span><span class="sxs-lookup"><span data-stu-id="e3a53-169">Enable sideloading</span></span>

<span data-ttu-id="e3a53-170">開発中は、アプリを配布せずにアプリTeams読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-170">During development, you must load your app within Teams without distributing it.</span></span> <span data-ttu-id="e3a53-171">これはサイドローディングと呼ばれる。</span><span class="sxs-lookup"><span data-stu-id="e3a53-171">This is known as sideloading.</span></span>

<span data-ttu-id="e3a53-172">アプリ アカウントをお持Teams、アプリをサイドロードできるアプリを次Teams。</span><span class="sxs-lookup"><span data-stu-id="e3a53-172">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>

1. <span data-ttu-id="e3a53-173">クライアントで、[Teams] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="e3a53-173">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="e3a53-174">カスタム **アプリアップロードを選択します**。</span><span class="sxs-lookup"><span data-stu-id="e3a53-174">Select **Upload a custom app**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="カスタム アプリをアップロードTeams場所を示す図。":::

> [!NOTE]
> <span data-ttu-id="e3a53-176">アプリをサイドロードできない場合は、管理者にTeamsしてください。</span><span class="sxs-lookup"><span data-stu-id="e3a53-176">If you still cannot sideload apps, talk to your Teams administrator.</span></span> <span data-ttu-id="e3a53-177">詳細[については、「カスタム Teamsアプリを有効](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)にする」を参照し、カスタム アプリのアップロードを有効にするを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e3a53-177">See [enable custom Teams apps and turn on custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for details.</span></span>

## <a name="get-a-free-teams-developer-tenant-optional"></a><span data-ttu-id="e3a53-178">開発者テナントの無料Teams取得 (オプション)</span><span class="sxs-lookup"><span data-stu-id="e3a53-178">Get a free Teams developer tenant (optional)</span></span>

<span data-ttu-id="e3a53-179">サイドロード オプションが表示されない場合、または Teams アカウントがない場合は、M365 開発者プログラムに参加することで無料の Teams 開発者アカウントを取得できます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-179">If you cannot see the sideload option, or you do not have a Teams account, you can get a free Teams developer account by joining the M365 developer program.</span></span>  <span data-ttu-id="e3a53-180">登録プロセスには約 2 分かかります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-180">The registration process takes approximately two minutes.</span></span>

1. <span data-ttu-id="e3a53-181">開発者プログラムの[Microsoft 365に移動します](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="e3a53-181">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="e3a53-182">[今 **すぐ参加] を** 選択し、画面の指示に従います。</span><span class="sxs-lookup"><span data-stu-id="e3a53-182">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="e3a53-183">ようこそ画面で **、[E5 サブスクリプションの設定] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="e3a53-183">In the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="e3a53-184">管理者アカウントを設定します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-184">Set up your administrator account.</span></span> <span data-ttu-id="e3a53-185">完了すると、次のような画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-185">After you finish, you should see a screen like this.</span></span>

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="開発者プログラムにサインアップした後に表示されるMicrosoft 365例。":::

1. <span data-ttu-id="e3a53-187">セットアップしTeams管理者アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="e3a53-187">Sign in to Teams using the administrator account you just set up.</span></span> <span data-ttu-id="e3a53-188">カスタム アプリ オプションのアップロード **確認** します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-188">Verify that you have the **Upload a custom app** option.</span></span>

## <a name="get-a-free-azure-account"></a><span data-ttu-id="e3a53-189">無料の Azure アカウントを取得する</span><span class="sxs-lookup"><span data-stu-id="e3a53-189">Get a free Azure account</span></span>

<span data-ttu-id="e3a53-190">アプリをホストするか、Azure 内のリソースにアクセスする場合は、Azure サブスクリプションが必要です。</span><span class="sxs-lookup"><span data-stu-id="e3a53-190">If you wish to host your app or access resources within Azure, you must have an Azure subscription.</span></span>  <span data-ttu-id="e3a53-191">開始する [前に無料アカウント](https://azure.microsoft.com/free/) を作成できます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-191">You can [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a><span data-ttu-id="e3a53-192">アカウントと Azure アカウントMicrosoft 365サインインする</span><span class="sxs-lookup"><span data-stu-id="e3a53-192">Sign in to your Microsoft 365 and Azure accounts</span></span>

<span data-ttu-id="e3a53-193">次の 2 つのアカウントにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-193">You must have access to two accounts:</span></span>

- <span data-ttu-id="e3a53-194">アカウントMicrosoft 365資格情報。</span><span class="sxs-lookup"><span data-stu-id="e3a53-194">Your Microsoft 365 account credentials.</span></span> <span data-ttu-id="e3a53-195">これは、アカウントにサインインするために使用するアカウントTeams。</span><span class="sxs-lookup"><span data-stu-id="e3a53-195">This is the account that you use to sign in to Teams.</span></span> <span data-ttu-id="e3a53-196">開発者プログラム のテナントMicrosoft 365場合、これはプログラムの登録時に設定した管理者アカウントです。</span><span class="sxs-lookup"><span data-stu-id="e3a53-196">If you're using a Microsoft 365 developer program tenant, this is the admin account you set up when you registered for the program.</span></span>
- <span data-ttu-id="e3a53-197">Azure 資格情報。</span><span class="sxs-lookup"><span data-stu-id="e3a53-197">Your Azure credentials.</span></span> <span data-ttu-id="e3a53-198">これは、Azure Portal へのアクセスと、アプリをサポートする新しいクラウド リソースのプロビジョニングに使用するアカウントです。</span><span class="sxs-lookup"><span data-stu-id="e3a53-198">This is the account that you use to access the Azure Portal and for provisioning new cloud resources to support your app.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="e3a53-199">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e3a53-199">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="e3a53-200">開Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e3a53-200">Open Visual Studio Code</span></span>
1. <span data-ttu-id="e3a53-201">サイドバーでTeamsアイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-201">Select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="e3a53-203">**[M365 にサインインする] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="e3a53-203">Select **Sign in to M365**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="サインインに使用する [アカウント] セクションの場所。":::

    <span data-ttu-id="e3a53-205">サインイン プロセスは、通常の Web ブラウザーの使用を開始します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-205">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="e3a53-206">M365 アカウントのサインイン プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-206">Complete the sign-in process for your M365 account.</span></span> <span data-ttu-id="e3a53-207">プロンプトが表示されたら、ブラウザーを閉じて、ブラウザーに戻Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="e3a53-207">When you are prompted, you can close the browser and return to Visual Studio Code.</span></span>
1. <span data-ttu-id="e3a53-208">データ内のTeams Toolkitに戻Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="e3a53-208">Return to the Teams Toolkit within Visual Studio Code.</span></span>
1. <span data-ttu-id="e3a53-209">[Azure **にサインインする] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="e3a53-209">Select **Sign in to Azure**.</span></span>

    > [!TIP]
    > <span data-ttu-id="e3a53-210">Azure Account 拡張機能がインストールされ、同じアカウントを使用している場合は、この手順を省略できます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-210">If you have the Azure Account extension installed and are using the same account, you can skip this step.</span></span> <span data-ttu-id="e3a53-211">他の拡張機能で使用しているアカウントと同じアカウントを使用します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-211">Use the same account as you are using in other extensions.</span></span>

1. <span data-ttu-id="e3a53-212">サインイン プロセスは、通常の Web ブラウザーの使用を開始します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-212">The sign-in process starts using your normal web browser.</span></span>  <span data-ttu-id="e3a53-213">Azure アカウントのサインイン プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-213">Complete the sign-in process for your Azure account.</span></span> <span data-ttu-id="e3a53-214">プロンプトが表示されたら、ブラウザーを閉じて、ブラウザーに戻Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="e3a53-214">When are prompted, you can close the browser and return to Visual Studio Code.</span></span>

    <span data-ttu-id="e3a53-215">完了すると、 **サイドバーの [ACCOUNTS]** セクションには、使用可能な Azure サブスクリプションの数と共に、2 つのアカウントが個別に表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-215">When complete, the **ACCOUNTS** section of the sidebar shows the two accounts separately, together with the number of usable Azure subscriptions available to you.</span></span> <span data-ttu-id="e3a53-216">使用可能な Azure サブスクリプションが少なくとも 1 つ用意されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a53-216">Ensure you have at least one usable Azure subscription available.</span></span> <span data-ttu-id="e3a53-217">サインインしていない場合は、サインアウトして別のアカウントを使用します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-217">If not, sign out and use a different account.</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="e3a53-218">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="e3a53-218">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="e3a53-219">Visual Studio 2019 では、必要に応じて各サービスにログインするように求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-219">Visual Studio 2019 prompts you to log in to each service as required.</span></span> <span data-ttu-id="e3a53-220">事前に M365 アカウントと Azure アカウントにサインインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="e3a53-220">You do not need to sign in to your M365 and Azure accounts in advance.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="e3a53-221">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="e3a53-221">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="e3a53-222">TeamsFx CLI を使用Microsoft 365サインインして、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-222">Sign in to Microsoft 365 with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login m365
    ```

    <span data-ttu-id="e3a53-223">サインイン プロセスは、通常の Web ブラウザーの使用を開始します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-223">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="e3a53-224">M365 アカウントのサインイン プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-224">Complete the sign-in process for your M365 account.</span></span> <span data-ttu-id="e3a53-225">ブラウザーを閉じるときにメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-225">You are prompted when you can close the browser.</span></span>

2. <span data-ttu-id="e3a53-226">TeamsFx CLI を使用して Azure にサインインします。</span><span class="sxs-lookup"><span data-stu-id="e3a53-226">Sign in to Azure with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login azure
    ```

    <span data-ttu-id="e3a53-227">サインイン プロセスは、通常の Web ブラウザーの使用を開始します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-227">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="e3a53-228">Azure アカウントのサインイン プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="e3a53-228">Complete the sign-in process for your Azure account.</span></span> <span data-ttu-id="e3a53-229">ブラウザーを閉じるときにメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-229">You are prompted when you can close the browser.</span></span>

    <span data-ttu-id="e3a53-230">アカウント ログインは、ユーザーと TeamsFx CLI Visual Studio Code共有されます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-230">The account logins are shared between Visual Studio Code and the TeamsFx CLI.</span></span>



    <span data-ttu-id="e3a53-231">開発環境が構成されたので、最初のアプリを作成、ビルド、およびTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="e3a53-231">Now that your development environment is configured, you can create, build, and deploy your first Teams app.</span></span>

## <a name="see-also"></a><span data-ttu-id="e3a53-232">関連項目</span><span class="sxs-lookup"><span data-stu-id="e3a53-232">See also</span></span>

* [<span data-ttu-id="e3a53-233">チュートリアルの概要</span><span class="sxs-lookup"><span data-stu-id="e3a53-233">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="e3a53-234">アプリを使用してアプリを作成React</span><span class="sxs-lookup"><span data-stu-id="e3a53-234">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="e3a53-235">Blazor を使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="e3a53-235">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="e3a53-236">アプリを使用してアプリを作成SPFx</span><span class="sxs-lookup"><span data-stu-id="e3a53-236">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="e3a53-237">C# を使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="e3a53-237">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="e3a53-238">Node.js を使ってアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="e3a53-238">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="e3a53-239">Yeoman ジェネレーターを使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="e3a53-239">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="e3a53-240">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="e3a53-240">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="e3a53-241">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="e3a53-241">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="e3a53-242">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="e3a53-242">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
