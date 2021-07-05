---
title: まず始める - Blazor を使用してTeamsアプリをビルドする
author: adrianhall
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 と .NET Blazor をMicrosoft Teams Toolkitメッセージを表示します。"
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: c14f55d014af120cab88044d31ee8600017e3c57
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254308"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="03b1a-104">Blazor で最初のアプリをMicrosoft Teams実行する</span><span class="sxs-lookup"><span data-stu-id="03b1a-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="03b1a-105">このチュートリアルでは、.NET/Blazor で新しい Microsoft Teams アプリを作成し、Microsoft Graph から情報を取得するための簡単な個人用アプリを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-105">In this tutorial, you will learn how to create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="03b1a-106">たとえば、個人用アプリ *には、* 個別に使用するタブのセットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-106">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="03b1a-107">チュートリアルでは、Teams アプリの構造、アプリをローカルで実行する方法、Azure にアプリを展開する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="03b1a-108">ビルドされたアプリは、現在のユーザーの基本的なユーザー情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-108">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="03b1a-109">許可が付与された場合、アプリは現在のユーザーとして Microsoft Graph に接続し、完全なプロフィールを取得します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="03b1a-110">始める前に</span><span class="sxs-lookup"><span data-stu-id="03b1a-110">Before you begin</span></span>

<span data-ttu-id="03b1a-111">前提条件をインストールして、開発環境がセットアップされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-111">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="03b1a-112">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="03b1a-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="03b1a-113">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="03b1a-113">Create your project</span></span>

<span data-ttu-id="03b1a-114">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="03b1a-115">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="03b1a-115">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="03b1a-116">2019 Visual Studioを開きます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-116">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="03b1a-117">[新 **しいプロジェクトを作成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-117">Select **Create a new project**.</span></span>

1. <span data-ttu-id="03b1a-118">[アプリ **Microsoft Teams選択し、[** 次へ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-118">Select **Microsoft Teams App**, then select **Next**.</span></span>  <span data-ttu-id="03b1a-119">テンプレートを見つけるのに役立つには、プロジェクトの種類 **を使用** Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="03b1a-119">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="03b1a-120">名前を入力し、[次へ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-120">Enter a name and select **Next**.</span></span>

1. <span data-ttu-id="03b1a-121">アプリケーション名と会社名を入力します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-121">Enter the application name and company name.</span></span>

1. <span data-ttu-id="03b1a-122">**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-122">Select **Create**.</span></span>  <span data-ttu-id="03b1a-123">アプリケーション名と会社名がエンド ユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-123">The application name and company name are displayed to your end users.</span></span> <span data-ttu-id="03b1a-124">数秒後に Teams アプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-124">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="03b1a-125">プロジェクトが作成された後、M365 でシングル サインオンを設定します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-125">After the project is created, set up single sign-on with M365:</span></span>

   1. <span data-ttu-id="03b1a-126">[TeamsFx **Project**  >  **SSO 用**  >  **に構成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-126">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   1. <span data-ttu-id="03b1a-127">メッセージが表示されたら、M365 管理者アカウントにサインインします。</span><span class="sxs-lookup"><span data-stu-id="03b1a-127">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="03b1a-128">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="03b1a-128">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="03b1a-129">ターミナルを開き、プロジェクトを作成するディレクトリを選択します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-129">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="03b1a-130">次 `dotnet new -i` のコマンドからテンプレートをインストールNuGet。</span><span class="sxs-lookup"><span data-stu-id="03b1a-130">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="03b1a-131">これを行う必要があるのは、初めて、またはテンプレートを更新する場合のみです。</span><span class="sxs-lookup"><span data-stu-id="03b1a-131">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="03b1a-132">この[NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/)の最新バージョンを確認します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-132">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="03b1a-133">ディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-133">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="03b1a-134">新 `dotnet new` しいプロジェクトを作成するには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-134">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="03b1a-135">スキャフォールディングが完了した後、次の手順にTeams構成します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-135">After scaffolding, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

   <span data-ttu-id="03b1a-136">これで、デバッグ用にソリューションをVisual Studio開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="03b1a-136">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="03b1a-137">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="03b1a-137">Take a tour of the source code</span></span>

<span data-ttu-id="03b1a-138">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-138">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="03b1a-139">プロジェクトをTeams Toolkitした後、プロジェクト用の基本的な個人用アプリを構築するためのTeams。</span><span class="sxs-lookup"><span data-stu-id="03b1a-139">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="03b1a-140">プロジェクト のディレクトリとファイルは、2019 年 2019 年のソリューション エクスプローラー Visual Studio表示されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-140">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="2019 年に個人用アプリのアプリ プロジェクト ファイルをVisual Studioスクリーンショット。":::

- <span data-ttu-id="03b1a-142">アプリ アイコンは PNG ファイルとして `color.png` と `outline.png` に格納されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-142">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="03b1a-143">開発者ポータルを通じて発行するアプリ マニフェストは、Teamsに格納されます `Properties/manifest.json` 。</span><span class="sxs-lookup"><span data-stu-id="03b1a-143">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="03b1a-144">認証を支援するためにバックエンド `Controllers/BackendController.cs` コントローラーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="03b1a-144">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="03b1a-145">セットアップ中にタブ アプリを作成したTeams Toolkit、基本的なタブに必要なすべてのコードが[Blazor Server としてスキャフォールディングされます](/aspnet/core/blazor)。</span><span class="sxs-lookup"><span data-stu-id="03b1a-145">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="03b1a-146">`Pages/Tab.razor` は、フロントエンド アプリケーションのエントリ ポイントです。</span><span class="sxs-lookup"><span data-stu-id="03b1a-146">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="03b1a-147">`TeamsFx.cs`ホスト `JS/src/index.js` との通信を初期化するためにTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-147">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="03b1a-148">バックエンド機能を追加するには、アプリケーションに ASP.NET Coreを追加します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-148">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="03b1a-149">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="03b1a-149">Run your app locally</span></span>

<span data-ttu-id="03b1a-150">Teams ツールキットでは、アプリをローカルで実行することができます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-150">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="03b1a-151">これは、Teams が予想する正しいインフラを提供するために必要ないくつかのパーツで構成されています。</span><span class="sxs-lookup"><span data-stu-id="03b1a-151">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="03b1a-152">Azure Active Directory を使用してアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="03b1a-152">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="03b1a-153">このアプリケーションには、アプリケーションが読み込まれる場所や、アクセスするバックエンド リソースに関連するアクセス許可があります。</span><span class="sxs-lookup"><span data-stu-id="03b1a-153">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="03b1a-154">Web API は 、認証タスクを支援するために (IIS Express 経由で) ホストされ、アプリとアプリ間のプロキシとして機能Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="03b1a-154">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="03b1a-155">アプリのマニフェストは、Developer Portal for Teams で生成され存在します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-155">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="03b1a-156">Teams はアプリ マニフェストを使用して、接続しているクライアントにアプリをロードする場所を伝達します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-156">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="03b1a-157">その後、アプリをクライアント内で読みTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-157">After this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="03b1a-158">Teams の Web クライアントを使用することで、標準的な Web 開発環境で HTML、CSS、JavaScript のコードを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-158">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="03b1a-159">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="03b1a-159">To build and run your app locally:</span></span>


1. <span data-ttu-id="03b1a-160">次Visual Studio Code **F5** キーを押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-160">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>


1. <span data-ttu-id="03b1a-161">要求された場合は、ローカル デバッグ用の自己署名証明書 SSL 証明書をインストールします。</span><span class="sxs-lookup"><span data-stu-id="03b1a-161">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. <span data-ttu-id="03b1a-163">Teams が Web ブラウザーに読み込まれ、サインインするようメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-163">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="03b1a-164">Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="03b1a-164">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="03b1a-165">M365 アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="03b1a-165">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="03b1a-166">アプリをインストールするように求めるメッセージが表示されたら、[Teams] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-166">When prompted to install the app onto Teams, select **Add**.</span></span>

   <span data-ttu-id="03b1a-167">これでご使用のアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-167">Your app will now be displayed:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="完了したアプリのスクリーンショット":::

   <span data-ttu-id="03b1a-169">デバッグ アクティビティは、ブレークポイントの設定などの他の Web アプリケーションである場合と同様に実行できます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-169">You can perform the debugging activities as if this were any other web application like setting breakpoints.</span></span> <span data-ttu-id="03b1a-170">このアプリはホット リロードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="03b1a-170">The app supports hot reloading.</span></span>  <span data-ttu-id="03b1a-171">プロジェクト内のファイルを変更すると、ページが再読み込みされます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-171">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="03b1a-172">デバッガーでアプリをローカルに実行した場合に発生することを説明します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-172">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="03b1a-173">**F5** キーを押すと、次のTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="03b1a-173">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="03b1a-174">アプリケーションをアプリケーションに登録Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="03b1a-174">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="03b1a-175">アプリケーションを"サイド ローディング" に登録Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="03b1a-175">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="03b1a-176">ローカルで実行されているアプリケーション バックエンドを開始します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-176">Starts your application backend running locally.</span></span>
1. <span data-ttu-id="03b1a-177">ローカルでホストされているアプリケーションフロントエンドを開始します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-177">Starts your application front-end hosted locally.</span></span>
1. <span data-ttu-id="03b1a-178">アプリケーションMicrosoft Teams読み込むよう指示するコマンドTeams Web ブラウザーで開始します (URL はアプリケーション マニフェスト内に登録されます)。</span><span class="sxs-lookup"><span data-stu-id="03b1a-178">Starts Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="03b1a-179">アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-179">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="03b1a-180">アプリをアプリ側で正常にTeamsするには、アプリ側の読み込みをMicrosoft 365開発アカウントを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="03b1a-180">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="03b1a-181">アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="03b1a-181">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="03b1a-182">アプリを Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="03b1a-182">Deploy your app to Azure</span></span>

<span data-ttu-id="03b1a-183">展開は、次の 2 つの手順で構成されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-183">Deployment consists of two steps:</span></span> 

1. <span data-ttu-id="03b1a-184">必要なクラウド リソースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-184">Necessary cloud resources are created.</span></span> <span data-ttu-id="03b1a-185">これはプロビジョニングとも呼ばれる。</span><span class="sxs-lookup"><span data-stu-id="03b1a-185">This is also known as provisioning.</span></span>
1. <span data-ttu-id="03b1a-186">コーディングを開始し、作成したクラウド リソースにアプリをコピーします。</span><span class="sxs-lookup"><span data-stu-id="03b1a-186">Start coding and copy your app into the created cloud resources.</span></span>

> <span data-ttu-id="03b1a-187">**プレビュー**</span><span class="sxs-lookup"><span data-stu-id="03b1a-187">**PREVIEW**</span></span>
>
> <span data-ttu-id="03b1a-188">Blazor アプリのサポートは、新しいTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="03b1a-188">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="03b1a-189">プロビジョニングと展開は、2019 年と 2019 年Visual Studio開発者ポータルの組み合わせでTeams。</span><span class="sxs-lookup"><span data-stu-id="03b1a-189">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="03b1a-190">アプリのプロビジョニングと Azure App Service への展開</span><span class="sxs-lookup"><span data-stu-id="03b1a-190">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="03b1a-191">ソリューション エクスプローラーで、プロジェクト ノードを右クリックし、[発行] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-191">In Solution Explorer, right-click the project node and select **Publish**.</span></span> <span data-ttu-id="03b1a-192">[発行のビルド]**メニュー項目**  >  **を** 使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-192">You can also use the **Build** > **Publish** menu item.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="プロジェクトの発行操作を選択する":::

1. <span data-ttu-id="03b1a-194">[発行 **] ウィンドウで\*\*\*\*、[Azure] と [次** へ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-194">In the **Publish** window, select **Azure** and selct **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="発行ターゲットとして Azure を選択する":::

1. <span data-ttu-id="03b1a-196">[Azure **App Service] (Windows) を選択し、[次へ]** を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-196">Select **Azure App Service (Windows)** and select **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="発行ターゲットとして Azure App Service を選択する":::

1. <span data-ttu-id="03b1a-198">新 **+** しい App Service インスタンスを作成する場合に選択します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-198">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="新しいインスタンスを作成します。":::

1. <span data-ttu-id="03b1a-200">[アプリ **サービスの作成 (Windows)** ダイアログボックスに、[名前] 、[サブスクリプション名]  、[**リソース** グループ]、および [ホスティング プラン] エントリ フィールドが設定されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-200">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="03b1a-201">App Service が既に実行されている場合は、既存の設定が選択されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-201">If you have already got an App Service running, existing settings are selected.</span></span>  <span data-ttu-id="03b1a-202">新しいリソース グループとホスティング プランを作成できます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-202">You can opt to create a new resource group and hosting plan.</span></span>  <span data-ttu-id="03b1a-203">準備ができたら、[作成] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-203">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="ホスティング プランとサブスクリプションの選択":::

1. <span data-ttu-id="03b1a-205">[発行 **] ダイアログ** で、新しく作成されたインスタンスが自動的に選択されています。</span><span class="sxs-lookup"><span data-stu-id="03b1a-205">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="03b1a-206">準備ができたら、[完了] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-206">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="新しいインスタンスを選択します。":::

1. <span data-ttu-id="03b1a-208">[展開モード **] の** 横にある [編集] (鉛筆) アイコン **を選択** し、[自己格納 **型] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-208">Select the **Edit** (pencil) icon next to **Deployment Mode**, and select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="[自己格納型展開モード] を選択します。":::

1. <span data-ttu-id="03b1a-210">[**発行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-210">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="アプリをアプリ サービスに発行する":::

   <span data-ttu-id="03b1a-212">Visual Studio Azure App Service にアプリを展開すると、Web アプリがブラウザーに読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-212">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="03b1a-213">URL `/tab` の末尾に追加して、ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-213">Add `/tab` to the end of the URL to see your page.</span></span>

   <span data-ttu-id="03b1a-214">プロジェクトのプロパティ [ **発行] ウィンドウ** には、サイトの URL などの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-214">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="03b1a-215">サイト URL をメモします。</span><span class="sxs-lookup"><span data-stu-id="03b1a-215">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="03b1a-216">アプリの環境を作成する</span><span class="sxs-lookup"><span data-stu-id="03b1a-216">Create an environment for your app</span></span>

<span data-ttu-id="03b1a-217">アプリのタブTeams環境を使用して読み込む場所を管理する開発者 **ポータル** です。</span><span class="sxs-lookup"><span data-stu-id="03b1a-217">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  

<span data-ttu-id="03b1a-218">**環境を作成するには、次の方法を実行します。**</span><span class="sxs-lookup"><span data-stu-id="03b1a-218">**To create an environment:**</span></span>

1. <span data-ttu-id="03b1a-219">開発者ポータル[を開Teams。](https://dev.teams.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="03b1a-219">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="03b1a-220">M365 管理アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="03b1a-220">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="03b1a-221">サイドバーで 、[アプリ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-221">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="03b1a-222">アプリが 1 つのみである場合は、自動的に選択されます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-222">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="03b1a-223">表示されない場合は、一覧からアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-223">If not, select your app from the list.</span></span>

1. <span data-ttu-id="03b1a-224">[環境 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-224">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="環境の選択":::

1. <span data-ttu-id="03b1a-226">[最初 **の環境を作成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-226">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="03b1a-227">環境の名前を入力し、[追加] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-227">Enter a name for your environment and select **Add**.</span></span> <span data-ttu-id="03b1a-228">たとえば、`_Production_` などです。</span><span class="sxs-lookup"><span data-stu-id="03b1a-228">For example, `_Production_`.</span></span>

1. <span data-ttu-id="03b1a-229">[最初 **の環境変数を作成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-229">Select **Create your first environment variable**.</span></span>

1. <span data-ttu-id="03b1a-230">[名前 `azure_app_url` ] に入力 **します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-230">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="03b1a-231">値を指定せずに Azure サイトの URL `https://` を **入力します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-231">Enter your Azure site URL without the `https://` as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="環境変数の作成":::

   <span data-ttu-id="03b1a-233">[追加 **] を押します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-233">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="03b1a-234">アプリ マニフェストを更新します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-234">Update the app manifest</span></span>

<span data-ttu-id="03b1a-235">アプリ マニフェストは、URL からタブを読み込 `localhost` む。</span><span class="sxs-lookup"><span data-stu-id="03b1a-235">The app manifest loads the tab from a `localhost` URL.</span></span>  <span data-ttu-id="03b1a-236">このセクションでは、作成した環境内にリストされている URL からタブを読み込むアプリ マニフェストを構成します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-236">In this section, you will configure the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="03b1a-237">サイドバーで、[基本情報] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-237">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="基本情報の選択":::

1. <span data-ttu-id="03b1a-239">マニフェスト内には、URL の一部としてリスト `locahost:XXXXX` される場所が複数あります。</span><span class="sxs-lookup"><span data-stu-id="03b1a-239">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="03b1a-240">中かっこを含む `{{azure_app_url}}` 、すべての出現箇所を置き換える。</span><span class="sxs-lookup"><span data-stu-id="03b1a-240">Replace all occurrences with `{{azure_app_url}}`, including the curly braces.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="環境の基本情報を調整する":::

1. <span data-ttu-id="03b1a-242">完了したら、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-242">When complete, select **Save**.</span></span>

1. <span data-ttu-id="03b1a-243">サイドバーで、[機能] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-243">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="機能の選択":::

1. <span data-ttu-id="03b1a-245">[個人用 **] タブを選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-245">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="03b1a-246">[個人用] タブ **の横で**、3 つのドットを選択し、[編集] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-246">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="個人用タブ設定の編集":::

1. <span data-ttu-id="03b1a-248">URL を [コンテンツ URL] フィールドと [Web サイト **URL]** フィールド内の **環境変数に置き換** えます。</span><span class="sxs-lookup"><span data-stu-id="03b1a-248">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="個人用タブ URL の編集":::

1. <span data-ttu-id="03b1a-250">**[更新]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-250">Select **Update**.</span></span>

1. <span data-ttu-id="03b1a-251">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-251">Select **Save**.</span></span>

1. <span data-ttu-id="03b1a-252">サイドバーで、[シングル サインオン **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-252">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="03b1a-253">アプリケーション `localhost` ID URI 内の **値を . に置き** 換える `{{azure_app_url}}` 。</span><span class="sxs-lookup"><span data-stu-id="03b1a-253">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="シングル サインオンアプリケーション ID URI の編集":::

1. <span data-ttu-id="03b1a-255">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-255">Select **Save**.</span></span>

1. <span data-ttu-id="03b1a-256">サイドバーで、[ドメイン] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-256">From the sidebar, select **Domains**.</span></span>

1. <span data-ttu-id="03b1a-257">[**ドメインの追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="03b1a-257">Select **Add a domain**.</span></span>

1. <span data-ttu-id="03b1a-258">有効なドメインとしてリストされていない場合は、有効なドメインとして追加し、[追加] `{{azure_app_url}}` を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="03b1a-258">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then select **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="ドメインの追加":::

   <span data-ttu-id="03b1a-260">ページの上部にある **[プレビュー] Teams** を使用して、アプリをアプリ内で起動Teams。</span><span class="sxs-lookup"><span data-stu-id="03b1a-260">You can now use the **Preview in Teams** option at the top of the page to launch your app within Teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="03b1a-261">関連項目</span><span class="sxs-lookup"><span data-stu-id="03b1a-261">See also</span></span>

* [<span data-ttu-id="03b1a-262">チュートリアルの概要</span><span class="sxs-lookup"><span data-stu-id="03b1a-262">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="03b1a-263">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="03b1a-263">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="03b1a-264">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="03b1a-264">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="03b1a-265">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="03b1a-265">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
