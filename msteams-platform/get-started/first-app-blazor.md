---
title: まず始める - Blazor を使用してTeamsアプリをビルドする
author: adrianhall
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 と .NET Blazor をMicrosoft Teams Toolkitメッセージを表示します。"
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: 6a9c7e008e2fb6d77c3314286b09d006bd468c37
ms.sourcegitcommit: 25c02757fe207cdff916ba63aa215f88e24e1d6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2021
ms.locfileid: "52667455"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="65d78-104">Blazor で最初のアプリをMicrosoft Teams実行する</span><span class="sxs-lookup"><span data-stu-id="65d78-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="65d78-105">このチュートリアルでは、.NET/Blazor で新しい Microsoft Teams アプリを作成し、Microsoft クライアントから情報を取得するための簡単な個人用アプリを実装Graph。</span><span class="sxs-lookup"><span data-stu-id="65d78-105">In this tutorial, you will create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="65d78-106">(個人用 *アプリには、* 個々の使用を対象にした一連のタブが含まれます)。 チュートリアルでは、Teams アプリの構造、アプリをローカルで実行する方法、Azure にアプリを展開する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="65d78-106">(A *personal app* includes a set of tabs scoped for individual use.)  During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="65d78-107">作成されたアプリには、現在のユーザーの基本的なユーザー情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="65d78-108">アクセス許可が付与された場合、アプリは現在のユーザーとして Microsoft Graphに接続して、完全なプロファイルを取得します。</span><span class="sxs-lookup"><span data-stu-id="65d78-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="65d78-109">開始する前に</span><span class="sxs-lookup"><span data-stu-id="65d78-109">Before you begin</span></span>

<span data-ttu-id="65d78-110">前提条件をインストールして、開発環境がセットアップされていることを確認 [する](prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="65d78-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="65d78-111">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="65d78-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="65d78-112">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="65d78-112">Create your project</span></span>

<span data-ttu-id="65d78-113">最初のプロジェクトTeams Toolkitを作成するには、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="65d78-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="65d78-114">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="65d78-114">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="65d78-115">2019 Visual Studioを開きます。</span><span class="sxs-lookup"><span data-stu-id="65d78-115">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="65d78-116">[新 **しいプロジェクトを作成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-116">Select **Create a new project**.</span></span>

1. <span data-ttu-id="65d78-117">[アプリ **Microsoft Teams選択し、[** 次へ] を **押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-117">Select **Microsoft Teams App**, then press **Next**.</span></span>  <span data-ttu-id="65d78-118">テンプレートを見つけるのに役立つには、プロジェクトの種類 **を使用** Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="65d78-118">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="65d78-119">プロジェクトとソリューションに良い名前を付け、[次へ] を **押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-119">Give the project and solution a good name, then press **Next**.</span></span>

1. <span data-ttu-id="65d78-120">アプリケーション名と会社名を入力し、[作成] を **押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-120">Provide the application name and company name, then press **Create**.</span></span>  <span data-ttu-id="65d78-121">アプリケーション名と会社名がエンド ユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-121">The application name and company name are displayed to your end users.</span></span>

1. <span data-ttu-id="65d78-122">アプリTeams数秒で作成されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-122">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="65d78-123">プロジェクトを作成したら、M365 でシングル サインオンを設定します。</span><span class="sxs-lookup"><span data-stu-id="65d78-123">Once the project is created, set up single sign-on with M365:</span></span>

   - <span data-ttu-id="65d78-124">[TeamsFx **Project**  >  **SSO 用**  >  **に構成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-124">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   - <span data-ttu-id="65d78-125">メッセージが表示されたら、M365 管理者アカウントにサインインします。</span><span class="sxs-lookup"><span data-stu-id="65d78-125">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="65d78-126">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="65d78-126">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="65d78-127">ターミナルを開き、プロジェクトを作成するディレクトリを選択します。</span><span class="sxs-lookup"><span data-stu-id="65d78-127">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="65d78-128">次 `dotnet new -i` のコマンドからテンプレートをインストールNuGet。</span><span class="sxs-lookup"><span data-stu-id="65d78-128">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="65d78-129">これを行う必要があるのは、初めて、またはテンプレートを更新する場合のみです。</span><span class="sxs-lookup"><span data-stu-id="65d78-129">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="65d78-130">この[NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/)の最新バージョンを確認します。</span><span class="sxs-lookup"><span data-stu-id="65d78-130">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="65d78-131">ディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="65d78-131">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="65d78-132">新 `dotnet new` しいプロジェクトを作成するには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="65d78-132">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="65d78-133">スキャフォールディングが完了したら、プロジェクトを次の展開Teams構成します。</span><span class="sxs-lookup"><span data-stu-id="65d78-133">Once scaffolded, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

<span data-ttu-id="65d78-134">これで、デバッグ用にソリューションをVisual Studio開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="65d78-134">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="65d78-135">ソース コードのツアーに参加する</span><span class="sxs-lookup"><span data-stu-id="65d78-135">Take a tour of the source code</span></span>

<span data-ttu-id="65d78-136">このセクションをスキップする場合は、アプリを [ローカルで実行できます](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="65d78-136">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="65d78-137">プロジェクトをTeams Toolkitしたら、プロジェクト用の基本的な個人用アプリを構築するためのTeams。</span><span class="sxs-lookup"><span data-stu-id="65d78-137">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="65d78-138">プロジェクト のディレクトリとファイルは、2019 年 2019 年のソリューション エクスプローラー Visual Studio表示されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-138">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="2019 年に個人用アプリのアプリ プロジェクト ファイルをVisual Studioスクリーンショット。":::

- <span data-ttu-id="65d78-140">アプリのアイコンは、PNG ファイルとして保存 `color.png` されます `outline.png` 。</span><span class="sxs-lookup"><span data-stu-id="65d78-140">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="65d78-141">開発者ポータルを通じて発行するアプリ マニフェストは、Teamsに格納されます `Properties/manifest.json` 。</span><span class="sxs-lookup"><span data-stu-id="65d78-141">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="65d78-142">認証を支援するためにバックエンド `Controllers/BackendController.cs` コントローラーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="65d78-142">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="65d78-143">セットアップ中にタブ アプリを作成したTeams Toolkit、基本的なタブに必要なすべてのコードが[Blazor Server としてスキャフォールディングされます](/aspnet/core/blazor)。</span><span class="sxs-lookup"><span data-stu-id="65d78-143">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="65d78-144">`Pages/Tab.razor` は、フロントエンド アプリケーションのエントリ ポイントです。</span><span class="sxs-lookup"><span data-stu-id="65d78-144">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="65d78-145">`TeamsFx.cs`ホスト `JS/src/index.js` との通信を初期化するためにTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="65d78-145">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="65d78-146">バックエンド機能を追加するには、アプリケーションに ASP.NET Coreを追加します。</span><span class="sxs-lookup"><span data-stu-id="65d78-146">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="65d78-147">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="65d78-147">Run your app locally</span></span>

<span data-ttu-id="65d78-148">Teams Toolkitアプリをローカルで実行できます。</span><span class="sxs-lookup"><span data-stu-id="65d78-148">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="65d78-149">これは、次に示す適切なインフラストラクチャを提供するために必要ないくつかのTeams構成されています。</span><span class="sxs-lookup"><span data-stu-id="65d78-149">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="65d78-150">アプリケーションがアプリケーションに登録Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="65d78-150">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="65d78-151">このアプリケーションには、アプリが読み込まれる場所とアクセスするバックエンド リソースに関連付けられたアクセス許可があります。</span><span class="sxs-lookup"><span data-stu-id="65d78-151">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="65d78-152">Web API は 、認証タスクを支援するために (IIS Express 経由で) ホストされ、アプリとアプリ間のプロキシとして機能Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="65d78-152">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="65d78-153">アプリ マニフェストが生成され、開発者ポータルのアプリ マニフェストにTeams。</span><span class="sxs-lookup"><span data-stu-id="65d78-153">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="65d78-154">Teamsマニフェストを使用して、接続されているクライアントにアプリの読み込み先を指定します。</span><span class="sxs-lookup"><span data-stu-id="65d78-154">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="65d78-155">これが完了すると、アプリをクライアント内で読みTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="65d78-155">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="65d78-156">標準の web Teams環境で HTML、CSS、JavaScript コードを表示するために、Web クライアントで使用します。</span><span class="sxs-lookup"><span data-stu-id="65d78-156">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="65d78-157">アプリをローカルでビルドして実行するには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="65d78-157">To build and run your app locally:</span></span>

1. <span data-ttu-id="65d78-158">次Visual Studio Code **F5 キーを押して**、デバッグ モードでアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="65d78-158">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

1. <span data-ttu-id="65d78-159">要求された場合は、ローカル デバッグ用の自己署名証明書 SSL 証明書をインストールします。</span><span class="sxs-lookup"><span data-stu-id="65d78-159">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="ローカル ホストからアプリケーションを読み込むTeams SSL 証明書をインストールするプロンプトを示すスクリーンショット。":::

1. <span data-ttu-id="65d78-161">Teams Web ブラウザーに読み込まれ、サインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-161">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="65d78-162">ブラウザーを開くメッセージが表示Microsoft Teamsブラウザー内に残る場合は、[キャンセル] を選択します。</span><span class="sxs-lookup"><span data-stu-id="65d78-162">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="65d78-163">M365 アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="65d78-163">Sign in with your M365 account.</span></span>
1. <span data-ttu-id="65d78-164">アプリをインストールするように求めるメッセージが表示されたら、[Teams] を **押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-164">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="65d78-165">これでアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-165">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="完成したアプリのスクリーンショット":::

<span data-ttu-id="65d78-167">通常のデバッグ アクティビティは、他の Web アプリケーション (ブレークポイントの設定など) と同様に実行できます。</span><span class="sxs-lookup"><span data-stu-id="65d78-167">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="65d78-168">アプリは、ホット リロードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="65d78-168">The app supports hot reloading.</span></span>  <span data-ttu-id="65d78-169">プロジェクト内のファイルを変更すると、ページが再読み込みされます。</span><span class="sxs-lookup"><span data-stu-id="65d78-169">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="65d78-170">デバッガーでアプリをローカルで実行するとどうなるかについて学習します。</span><span class="sxs-lookup"><span data-stu-id="65d78-170">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="65d78-171">F5 キーを押すと、次のTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="65d78-171">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="65d78-172">アプリケーションを Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="65d78-172">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="65d78-173">アプリケーションに"サイド ローディング" を登録Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="65d78-173">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="65d78-174">ローカルで実行されているアプリケーション バックエンドを開始しました。</span><span class="sxs-lookup"><span data-stu-id="65d78-174">Started your application backend running locally.</span></span>
1. <span data-ttu-id="65d78-175">ローカルでホストされるアプリケーションフロントエンドを開始しました。</span><span class="sxs-lookup"><span data-stu-id="65d78-175">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="65d78-176">アプリケーションMicrosoft Teams読み込むようTeamsコマンドを使用して Web ブラウザーで開始します (URL はアプリケーション マニフェスト内に登録されます)。</span><span class="sxs-lookup"><span data-stu-id="65d78-176">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="65d78-177">アプリをローカルで実行するときに一般的な問題をトラブルシューティングする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="65d78-177">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="65d78-178">アプリをアプリ側で正常にTeamsするには、アプリ側の読み込みをMicrosoft 365開発アカウントを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="65d78-178">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="65d78-179">アカウントを開く方法の詳細については、「前提条件」を [参照してください](prerequisites.md#enable-sideloading)。</span><span class="sxs-lookup"><span data-stu-id="65d78-179">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="65d78-180">アプリを Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="65d78-180">Deploy your app to Azure</span></span>

<span data-ttu-id="65d78-181">展開は 2 つの手順で構成されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-181">Deployment consists of two steps.</span></span>  <span data-ttu-id="65d78-182">まず、必要なクラウド リソース (プロビジョニングとも呼ばれる) が作成され、アプリを構成するコードが作成されたクラウド リソースにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="65d78-182">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

> <span data-ttu-id="65d78-183">**プレビュー**</span><span class="sxs-lookup"><span data-stu-id="65d78-183">**PREVIEW**</span></span>
>
> <span data-ttu-id="65d78-184">Blazor アプリのサポートは、新しいTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="65d78-184">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="65d78-185">プロビジョニングと展開は、2019 年と 2019 年Visual Studio開発者ポータルの組み合わせでTeams。</span><span class="sxs-lookup"><span data-stu-id="65d78-185">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="65d78-186">アプリのプロビジョニングと Azure App Service への展開</span><span class="sxs-lookup"><span data-stu-id="65d78-186">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="65d78-187">ソリューション エクスプローラーで、プロジェクト ノードを右クリックし、[発行] を **選択します**(または、[ビルド発行 **] メニュー項目**  >  **を** 使用します)。</span><span class="sxs-lookup"><span data-stu-id="65d78-187">In Solution Explorer, right-click the project node and choose **Publish** (or use the **Build** > **Publish** menu item).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="プロジェクトの発行操作を選択する":::

1. <span data-ttu-id="65d78-189">[発行]**ウィンドウで\*\*\*\*、[Azure] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-189">In the **Publish** window, select **Azure**.</span></span>  <span data-ttu-id="65d78-190">[次 **へ] を押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-190">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="発行ターゲットとして Azure を選択する":::

1. <span data-ttu-id="65d78-192">[Azure **App Service] (Windows) を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-192">Select **Azure App Service (Windows)**.</span></span>  <span data-ttu-id="65d78-193">[次 **へ] を押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-193">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="発行ターゲットとして Azure App Service を選択する":::

1. <span data-ttu-id="65d78-195">新 **+** しい App Service インスタンスを作成する場合に選択します。</span><span class="sxs-lookup"><span data-stu-id="65d78-195">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="新しいインスタンスを作成します。":::

1. <span data-ttu-id="65d78-197">[アプリ **サービスの作成 (Windows)** ダイアログボックスに、[名前] 、[サブスクリプション名]  、[**リソース** グループ]、および [ホスティング プラン] エントリ フィールドが設定されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-197">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="65d78-198">App Service が既に実行されている場合は、既存の設定が選択されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-198">If you have already got an App Service running, existing settings will be selected.</span></span>  <span data-ttu-id="65d78-199">新しいリソース グループとホスティング プランを作成することを選択できます (推奨)。</span><span class="sxs-lookup"><span data-stu-id="65d78-199">You can opt to create a new resource group and hosting plan (Recommended).</span></span>  <span data-ttu-id="65d78-200">準備ができたら、[作成] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-200">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="ホスティング プランとサブスクリプションの選択":::

1. <span data-ttu-id="65d78-202">[発行 **] ダイアログ** で、新しく作成されたインスタンスが自動的に選択されています。</span><span class="sxs-lookup"><span data-stu-id="65d78-202">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="65d78-203">準備ができたら、[完了] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-203">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="新しいインスタンスを選択します。":::

1. <span data-ttu-id="65d78-205">[展開モード **] の** 横にある [編集] (鉛筆) アイコン **を押** し、[自己格納 **型] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-205">Press the **Edit** (pencil) icon next to **Deployment Mode**, then select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="[自己格納型展開モード] を選択します。":::

1. <span data-ttu-id="65d78-207">[**発行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="65d78-207">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="アプリをアプリ サービスに発行する":::

<span data-ttu-id="65d78-209">Visual Studio Azure App Service にアプリを展開すると、Web アプリがブラウザーに読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="65d78-209">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="65d78-210">URL `/tab` の末尾に追加して、ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="65d78-210">Add `/tab` to the end of the URL to see your page.</span></span>

<span data-ttu-id="65d78-211">プロジェクトのプロパティ [ **発行] ウィンドウ** には、サイトの URL などの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-211">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="65d78-212">サイト URL をメモします。</span><span class="sxs-lookup"><span data-stu-id="65d78-212">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="65d78-213">アプリの環境を作成する</span><span class="sxs-lookup"><span data-stu-id="65d78-213">Create an environment for your app</span></span>

<span data-ttu-id="65d78-214">アプリのタブTeams環境を使用して読み込む場所を管理する開発者 **ポータル** です。</span><span class="sxs-lookup"><span data-stu-id="65d78-214">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  <span data-ttu-id="65d78-215">環境を作成するには、次の方法を実行します。</span><span class="sxs-lookup"><span data-stu-id="65d78-215">To create an environment:</span></span>

1. <span data-ttu-id="65d78-216">開発者ポータル[を開Teams。](https://dev.teams.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="65d78-216">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="65d78-217">M365 管理アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="65d78-217">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="65d78-218">サイドバーで 、[アプリ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-218">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="65d78-219">アプリが 1 つのみである場合は、自動的に選択されます。</span><span class="sxs-lookup"><span data-stu-id="65d78-219">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="65d78-220">表示されない場合は、一覧からアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="65d78-220">If not, select your app from the list.</span></span>

1. <span data-ttu-id="65d78-221">[環境 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-221">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="環境の選択":::

1. <span data-ttu-id="65d78-223">[最初 **の環境を作成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-223">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="65d78-224">環境の名前を入力し、[追加] を **押します**。たとえば、_実稼働 ._</span><span class="sxs-lookup"><span data-stu-id="65d78-224">Enter a name for your environment, then press **Add**; for example _Production_.</span></span>

1. <span data-ttu-id="65d78-225">新しく作成した環境が選択されている場合は、[最初の **環境変数を作成する] を押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-225">With the newly created environment selected, press **Create your first environment variable**.</span></span>

1. <span data-ttu-id="65d78-226">[名前 `azure_app_url` ] に入力 **します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-226">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="65d78-227">Azure サイトの URL (なし) を Value `https://` として入力 **します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-227">Enter your Azure site URL (without the `https://`) as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="環境変数の作成":::

   <span data-ttu-id="65d78-229">[追加 **] を押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-229">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="65d78-230">アプリ マニフェストを更新します。</span><span class="sxs-lookup"><span data-stu-id="65d78-230">Update the app manifest</span></span>

<span data-ttu-id="65d78-231">アプリ マニフェストが URL からタブを読み込 `localhost` み中です。</span><span class="sxs-lookup"><span data-stu-id="65d78-231">The app manifest is loading the tab from a `localhost` URL.</span></span>  <span data-ttu-id="65d78-232">このセクションでは、アプリ マニフェストを調整して、作成した環境内にリストされている URL からタブを読み込む。</span><span class="sxs-lookup"><span data-stu-id="65d78-232">In this section, you will adjust the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="65d78-233">サイドバーで、[基本情報] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-233">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="基本情報の選択":::

1. <span data-ttu-id="65d78-235">マニフェスト内には、URL の一部としてリスト `locahost:XXXXX` される場所が複数あります。</span><span class="sxs-lookup"><span data-stu-id="65d78-235">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="65d78-236">すべてのオカレンスを `{{azure_app_url}}` (中かっこを含む) に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="65d78-236">Replace all occurrences with `{{azure_app_url}}` (including the curly braces).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="環境の基本情報を調整する":::

1. <span data-ttu-id="65d78-238">完了したら、[保存] **を押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-238">When complete, press **Save**.</span></span>

1. <span data-ttu-id="65d78-239">サイドバーで、[機能] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-239">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="機能の選択":::

1. <span data-ttu-id="65d78-241">[個人用 **] タブを選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-241">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="65d78-242">[個人用] タブ **の横で**、3 つのドットを選択し、[編集] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-242">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="個人用タブ設定の編集":::

1. <span data-ttu-id="65d78-244">URL を [コンテンツ URL] フィールドと [Web サイト **URL]** フィールド内の **環境変数に置き換** えます。</span><span class="sxs-lookup"><span data-stu-id="65d78-244">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="個人用タブ URL の編集":::

1. <span data-ttu-id="65d78-246">[ **更新] を押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-246">Press **Update**.</span></span>

1. <span data-ttu-id="65d78-247">**[保存]** を押します。</span><span class="sxs-lookup"><span data-stu-id="65d78-247">Press **Save**.</span></span>

1. <span data-ttu-id="65d78-248">サイドバーで、[シングル サインオン **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-248">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="65d78-249">アプリケーション `localhost` ID URI 内の **値を . に置き** 換える `{{azure_app_url}}` 。</span><span class="sxs-lookup"><span data-stu-id="65d78-249">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="シングル サインオンアプリケーション ID URI の編集":::

1. <span data-ttu-id="65d78-251">**[保存]** を押します。</span><span class="sxs-lookup"><span data-stu-id="65d78-251">Press **Save**.</span></span>

1. <span data-ttu-id="65d78-252">サイドバーで[ドメイン] **を押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-252">From the sidebar, press **Domains**.</span></span>

1. <span data-ttu-id="65d78-253">[ドメイン **の追加] を押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-253">Press **Add a domain**.</span></span>

1. <span data-ttu-id="65d78-254">有効なドメインとしてリストされていない場合は、有効なドメインとして追加し、[追加] `{{azure_app_url}}` を **押します**。</span><span class="sxs-lookup"><span data-stu-id="65d78-254">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then press **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="ドメインの追加":::

<span data-ttu-id="65d78-256">ページの上部にある **[プレビュー] Teams** ボタンを使用して、アプリをアプリ内で起動Teams。</span><span class="sxs-lookup"><span data-stu-id="65d78-256">You can now use the **Preview in Teams** button at the top of the page to launch your app within Teams.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65d78-257">次のステップ</span><span class="sxs-lookup"><span data-stu-id="65d78-257">Next steps</span></span>

<span data-ttu-id="65d78-258">アプリを作成する他の方法Teamsします。</span><span class="sxs-lookup"><span data-stu-id="65d78-258">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="65d78-259">アプリを使用TeamsアプリをReact</span><span class="sxs-lookup"><span data-stu-id="65d78-259">Create a Teams app with React</span></span>](first-app-react.md)
- <span data-ttu-id="65d78-260">[Web パーツTeamsアプリをSharePointする](first-app-spfx.md)(Azure は必須ではありません)</span><span class="sxs-lookup"><span data-stu-id="65d78-260">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="65d78-261">会話型ボット アプリの作成</span><span class="sxs-lookup"><span data-stu-id="65d78-261">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="65d78-262">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="65d78-262">Create a messaging extension</span></span>](first-message-extension.md)
