---
title: はじめに - 最初のアプリを構築して実行する
author: girliemac
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 Microsoft Teams のツールキットを使用したメッセージ。"
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: 6c3d215a3f2c1aa89a9a2bf28aad081d98c6dc33
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101724"
---
# <a name="create-your-first-microsoft-teams-app"></a><span data-ttu-id="407fd-104">最初のアプリをMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="407fd-104">Create your first Microsoft Teams app</span></span>

<span data-ttu-id="407fd-105">このクイック スタートでは、"Hello, World! を表示Microsoft Teamsアプリをビルドして実行する方法について教えています。</span><span class="sxs-lookup"><span data-stu-id="407fd-105">This quickstart teaches you to build and run Microsoft Teams app that displays "Hello, World!"</span></span>

## <a name="prerequisites"></a><span data-ttu-id="407fd-106">前提条件</span><span class="sxs-lookup"><span data-stu-id="407fd-106">Prerequisites</span></span>

<span data-ttu-id="407fd-107">開始する前に、開発テナント[をセットアップし、Teams開発](#set-up-your-teams-development-tenant)ツール[をインストールTeams必要があります](#install-your-development-tools)。</span><span class="sxs-lookup"><span data-stu-id="407fd-107">Before you begin, you need to [set up your Teams development tenant](#set-up-your-teams-development-tenant) and [install your Teams development tools](#install-your-development-tools).</span></span>

### <a name="set-up-your-teams-development-tenant"></a><span data-ttu-id="407fd-108">開発テナントTeams設定する</span><span class="sxs-lookup"><span data-stu-id="407fd-108">Set up your Teams development tenant</span></span>

<span data-ttu-id="407fd-109">テナント **は** 、組織のコンテナーに似たものになります。</span><span class="sxs-lookup"><span data-stu-id="407fd-109">A **tenant** is like a container for an organization.</span></span> <span data-ttu-id="407fd-110">つまりTeamsテナントとは、その組織のチャット、ファイルの共有、会議の実行を行う場所です。</span><span class="sxs-lookup"><span data-stu-id="407fd-110">In Teams terms, a tenant is where people from that org chat, share files, and run meetings.</span></span> <span data-ttu-id="407fd-111">開発者は、構築中のアプリをサイドロードしてテストTeamsテナントが必要です。</span><span class="sxs-lookup"><span data-stu-id="407fd-111">As a developer, you need a tenant to sideload and test the Teams apps that you are building.</span></span>  

# <a name="do-not-have-a-tenant"></a>[<span data-ttu-id="407fd-112">テナントを持たない</span><span class="sxs-lookup"><span data-stu-id="407fd-112">Do not have a tenant</span></span>](#tab/do-not-have-a-tenant)

<span data-ttu-id="407fd-113">アプリのサイドローディングをTeamsするテナントを含む無料のテスト アカウントを取得するには、開発者プログラムMicrosoft 365参加します。</span><span class="sxs-lookup"><span data-stu-id="407fd-113">You can get a free Teams test account, which includes a tenant that allows app sideloading, by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="407fd-114">登録プロセスには約 2 分かかります。</span><span class="sxs-lookup"><span data-stu-id="407fd-114">The registration process takes approximately two minutes.</span></span>

<span data-ttu-id="407fd-115">**テナントを取得するには**</span><span class="sxs-lookup"><span data-stu-id="407fd-115">**To get a tenant**</span></span>

1. <span data-ttu-id="407fd-116">開発者プログラムの[Microsoft 365に移動します](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="407fd-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="407fd-117">[今 **すぐ参加] を** 選択し、画面の指示に従います。</span><span class="sxs-lookup"><span data-stu-id="407fd-117">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="407fd-118">[ようこそ] 画面で **、[E5 サブスクリプションの設定] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="407fd-118">In the Welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="407fd-119">開発者アカウントMicrosoft 365設定します。</span><span class="sxs-lookup"><span data-stu-id="407fd-119">Set up your Microsoft 365 developer account.</span></span> 
   <span data-ttu-id="407fd-120">完了すると、次の画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="407fd-120">After you finish, the following screen appears:</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="開発者プログラムにサインアップした後に表示されるMicrosoft 365例。":::

1. <span data-ttu-id="407fd-122">新しいアカウントでTeamsサインインします。</span><span class="sxs-lookup"><span data-stu-id="407fd-122">Sign in to Teams with your new account.</span></span>
1. <span data-ttu-id="407fd-123">クライアントで、[Teams] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="407fd-123">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="407fd-124">カスタム アプリ オプションのアップロード **確認** します。</span><span class="sxs-lookup"><span data-stu-id="407fd-124">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="407fd-125">これを行う場合は、アプリをサイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="407fd-125">If you do, this means you can sideload apps.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="カスタム アプリをアップロードTeams場所を示す図。":::

# <a name="have-a-tenant"></a>[<span data-ttu-id="407fd-127">テナントを持つ</span><span class="sxs-lookup"><span data-stu-id="407fd-127">Have a tenant</span></span>](#tab/have-a-tenant)

<span data-ttu-id="407fd-128">テナントが既に存在する場合は、アプリをアプリにサイドロードできるTeams。</span><span class="sxs-lookup"><span data-stu-id="407fd-128">If you already have a tenant, verify if you can sideload apps in Teams.</span></span>

<span data-ttu-id="407fd-129">**アプリをサイドロードできると確認する**</span><span class="sxs-lookup"><span data-stu-id="407fd-129">**Verify that you can sideload your apps**</span></span> 

1. <span data-ttu-id="407fd-130">[クライアント] Teams[アプリ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="407fd-130">In the Teams Client, select **Apps**.</span></span> 
1.  <span data-ttu-id="407fd-131">カスタム アプリ オプションのアップロード **確認** します。</span><span class="sxs-lookup"><span data-stu-id="407fd-131">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="407fd-132">これを行う場合は、アプリをサイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="407fd-132">If you do, this means you can sideload apps.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="カスタム アプリをアップロードTeams場所を示す図。":::

---

### <a name="install-your-development-tools"></a><span data-ttu-id="407fd-134">開発ツールのインストール</span><span class="sxs-lookup"><span data-stu-id="407fd-134">Install your development tools</span></span>

<span data-ttu-id="407fd-135">このアプリをビルドするには、アプリのTeams ToolkitをVisual Studio Code開始します。</span><span class="sxs-lookup"><span data-stu-id="407fd-135">To build this app, you'll use the Teams Toolkit for Visual Studio Code to quickly get started.</span></span> <span data-ttu-id="407fd-136">また、任意のTeamsアプリをビルドすることもできます。</span><span class="sxs-lookup"><span data-stu-id="407fd-136">You can also build Teams apps with any of your preffered tools.</span></span> 

> [!NOTE]
> <span data-ttu-id="407fd-137">Teams HTTPS 接続経由でのみアプリ コンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="407fd-137">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="407fd-138">ボットなど、特定の種類のアプリをローカルでデバッグするには、ngrok を使用して、Teams とアプリの間にセキュリティで保護されたトンネルを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="407fd-138">To debug certain types of apps locally, such as a bot, you'll learn how to use ngrok to set up a secure tunnel between Teams and your app.</span></span>
> 
> <span data-ttu-id="407fd-139">実稼働Teamsはクラウドでホストされます。</span><span class="sxs-lookup"><span data-stu-id="407fd-139">Production Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="407fd-140">**ツールをMicrosoft Teamsするには**</span><span class="sxs-lookup"><span data-stu-id="407fd-140">**To install Microsoft Teams tools**</span></span>

1. <span data-ttu-id="407fd-141">[Node.js](https://nodejs.org/en/) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="407fd-141">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="407fd-142">ボットまたはメッセージング拡張機能を作成する場合は [、ngrok](https://ngrok.com/download) をインストールし [、ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)を使用してローカル ホストをインターネットに公開します。</span><span class="sxs-lookup"><span data-stu-id="407fd-142">If you plan to build a bot or messaging extension, install [ngrok](https://ngrok.com/download) and [expose your localhost to the Internet using ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="407fd-143">最新バージョンのファイルを[インストールVisual Studio Code。](https://code.visualstudio.com/download)</span><span class="sxs-lookup"><span data-stu-id="407fd-143">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="407fd-144">このツールキットは、以前のバージョンのアプリケーションをVisual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="407fd-144">The toolkit does not support earlier versions of Visual Studio Code.</span></span>

1. 左側のアクティビティ バーで、[拡張機能] **を選択します** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: 。
1. <span data-ttu-id="407fd-146">[インストール **Microsoft Teams Toolkit]** を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="407fd-146">In **Microsoft Teams Toolkit**, select **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="拡張機能をインストールVisual Studio Codeする場所を示Microsoft Teams Toolkit図。":::

## <a name="1-create-your-app-project"></a><span data-ttu-id="407fd-148">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="407fd-148">1. Create your app project</span></span>

1. <span data-ttu-id="407fd-149">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="407fd-149">Open Visual Studio Code.</span></span>
1. [新 **Microsoft Teams Toolkit** :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **アプリを作成する] をTeamsします**。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="アプリ プロジェクトを作成する方法を示すスクリーンショットをVisual Studio Code Teams Toolkit。":::
   
1. <span data-ttu-id="407fd-152">開発アカウントでサインインMicrosoft 365します。</span><span class="sxs-lookup"><span data-stu-id="407fd-152">Sign in with your Microsoft 365 development account.</span></span> <span data-ttu-id="407fd-153">作成したアカウントか、アプリのサイドローディングを許可するアカウントのどちらかです。</span><span class="sxs-lookup"><span data-stu-id="407fd-153">Either the one you just created or the account you already had that allows app sideloading.</span></span>
1. <span data-ttu-id="407fd-154">[プロジェクトの **選択] 画面** で、[個人用アプリ] に **移動し** 、[次へ] の **[JS** (JavaScript) > **選択します**。</span><span class="sxs-lookup"><span data-stu-id="407fd-154">On the **Select project** screen, go to **Personal app** and select **JS** (JavaScript) > **Next**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Visual Studio Code Teams ツールキットを使用して、アプリ プロジェクトを構成する方法を示すスクリーンショット。":::

1. <span data-ttu-id="407fd-156">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="407fd-156">Enter a name for your Teams app.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="アプリ プロジェクトに名前を追加する方法を示すスクリーンショットで、Visual Studio Code Teams Toolkit。":::

1. <span data-ttu-id="407fd-158">[**完了**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="407fd-158">Select **Finish**.</span></span> 
   <span data-ttu-id="407fd-159">これで、プロジェクトが構成されます。</span><span class="sxs-lookup"><span data-stu-id="407fd-159">Your project is now configured.</span></span> 

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="407fd-160">2. アプリ プロジェクト コンポーネントについて</span><span class="sxs-lookup"><span data-stu-id="407fd-160">2. Understand your app project components</span></span>

<span data-ttu-id="407fd-161">ツールキットでアプリ プロジェクトを構成した後、"Hello, World!</span><span class="sxs-lookup"><span data-stu-id="407fd-161">After the toolkit configures your app project, you have the components to build your "Hello, World!"</span></span> <span data-ttu-id="407fd-162">Teamsアプリ。</span><span class="sxs-lookup"><span data-stu-id="407fd-162">Teams app.</span></span> <span data-ttu-id="407fd-163">プロジェクトのディレクトリとファイルは、プロジェクト エクスプローラー Visual Studio Codeされます。</span><span class="sxs-lookup"><span data-stu-id="407fd-163">The project's directories and files are located in the Visual Studio Code Explorer.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="アプリ プロジェクトのスキャフォールディングを示すスクリーンショットと、Visual Studio Code Teams Toolkit。":::

<span data-ttu-id="407fd-165">ツールキットは、セットアップ時に追加した機能に基づいて、ディレクトリにアプリスキャフォールディング `src` を自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="407fd-165">The toolkit automatically creates app scaffolding in the `src` directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="407fd-166">セットアップ中にタブを作成したので、ディレクトリ内のファイルはアプリの初期化と `App.js` `src/components` ルーティングを処理します。</span><span class="sxs-lookup"><span data-stu-id="407fd-166">Since you created a tab during setup, the `App.js` file in the `src/components` directory handles the initialization and routing of your app.</span></span> <span data-ttu-id="407fd-167">また、このファイルは JavaScript クライアント SDK Microsoft Teams呼び出して、アプリとアプリ間の通信を確立Teams。</span><span class="sxs-lookup"><span data-stu-id="407fd-167">The file also calls the Microsoft Teams JavaScript client SDK to establish communication between your app and Teams.</span></span> 

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="407fd-168">3. アプリの構築と実行</span><span class="sxs-lookup"><span data-stu-id="407fd-168">3. Build and run your app</span></span>

<span data-ttu-id="407fd-169">アプリをローカルに構築して実行することで、時間を節約できます。</span><span class="sxs-lookup"><span data-stu-id="407fd-169">Build and run your app locally to save time.</span></span> 

<span data-ttu-id="407fd-170">**アプリをビルドして実行するには**</span><span class="sxs-lookup"><span data-stu-id="407fd-170">**To build and run your app**</span></span>

1. <span data-ttu-id="407fd-171">[Visual Studio Code] で、[ターミナルの表示 **] を**  >  **選択します**。</span><span class="sxs-lookup"><span data-stu-id="407fd-171">In Visual Studio Code, select **View** > **Terminal**.</span></span>
1. <span data-ttu-id="407fd-172">`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="407fd-172">Run `npm install`.</span></span>
1. <span data-ttu-id="407fd-173">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="407fd-173">Run `npm start`.</span></span>
  
  <span data-ttu-id="407fd-174">コンパイル **が正常に完了しました。**</span><span class="sxs-lookup"><span data-stu-id="407fd-174">A **Compiled successfully!**</span></span> <span data-ttu-id="407fd-175">メッセージがターミナルに表示されます。</span><span class="sxs-lookup"><span data-stu-id="407fd-175">message appears in the terminal.</span></span> <span data-ttu-id="407fd-176">これで、アプリが localhost で実行されています `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="407fd-176">Your app is now running on your localhost at `https://localhost:3000`.</span></span> 

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="407fd-177">4. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="407fd-177">4. Sideload your app in Teams</span></span>

<span data-ttu-id="407fd-178">サイドローディングは、管理者または Microsoft によって承認されていないアプリをTeamsアプリをインストールするプロセスです。</span><span class="sxs-lookup"><span data-stu-id="407fd-178">Sideloading is the process of installing an app in Teams that hasn't been approved by your admin or Microsoft.</span></span> <span data-ttu-id="407fd-179">サイドローディングは、アプリのテストとデバッグを行うTeamsです。</span><span class="sxs-lookup"><span data-stu-id="407fd-179">Sideloading is common when testing and debugging Teams apps.</span></span>

<span data-ttu-id="407fd-180">既定では、Teamsアプリのサイドローディングは許可されません。</span><span class="sxs-lookup"><span data-stu-id="407fd-180">By default, Teams doesn't allow app sideloading.</span></span> <span data-ttu-id="407fd-181">この設定は、管理センター Teams変更できます。</span><span class="sxs-lookup"><span data-stu-id="407fd-181">You can change this setting in the Teams admin center.</span></span>

<span data-ttu-id="407fd-182">**アプリのサイドローディングを有効にするには、Teams**</span><span class="sxs-lookup"><span data-stu-id="407fd-182">**To enable app sideloading in Teams**</span></span>

1. <span data-ttu-id="407fd-183">管理者資格情報を使用[Microsoft 365管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にサインインします。</span><span class="sxs-lookup"><span data-stu-id="407fd-183">Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>  
1. <span data-ttu-id="407fd-184">[**すべての** > **Teams の表示**]を選択します。</span><span class="sxs-lookup"><span data-stu-id="407fd-184">Select **Show All** > **Teams**.</span></span> 

   ![管理センター メニューの画像](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > <span data-ttu-id="407fd-186">このオプションを表示するには、最大で 24 **Teams** かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="407fd-186">It can take up to 24 hours for the **Teams** option to appear.</span></span> 

1. <span data-ttu-id="407fd-187">[アプリの **Teamsグローバル ]**(組織全体の既定)  >    >  に移動します。</span><span class="sxs-lookup"><span data-stu-id="407fd-187">Go to **Teams apps** > **Setup policies** > **Global** (Org-wide default).</span></span>

   ![sideload ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. <span data-ttu-id="407fd-189">[カスタム アプリの **アップロード] トグルをオン** にします。</span><span class="sxs-lookup"><span data-stu-id="407fd-189">Turn on the **upload custom apps** toggle.</span></span>

1. <span data-ttu-id="407fd-190">[保存 **] を** 選択して変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="407fd-190">Select **Save** to save the changes.</span></span>

   <span data-ttu-id="407fd-191">テスト テナントでカスタム アプリのサイドローディングが許可されます。</span><span class="sxs-lookup"><span data-stu-id="407fd-191">Your test tenant now allows custom app sideloading.</span></span>

   > [!Note]
   > <span data-ttu-id="407fd-192">ツールキットに含まれている App Studio の検証機能を使用してアプリをサイドロードする前に問題を確認します。</span><span class="sxs-lookup"><span data-stu-id="407fd-192">Check for issues before sideloading your app using the validation feature in App Studio, which is included in the toolkit.</span></span> <span data-ttu-id="407fd-193">エラーを修正して、アプリを正常にサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="407fd-193">Fix the errors to successfully sideload the app.</span></span>


### <a name="sideload-your-app"></a><span data-ttu-id="407fd-194">アプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="407fd-194">Sideload your app</span></span>

1. <span data-ttu-id="407fd-195">[Visual Studio Code] で、ファイルを開Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="407fd-195">In Visual Studio Code, open the Teams Toolkit.</span></span>
1. <span data-ttu-id="407fd-196">[App **Studio] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="407fd-196">Go to **App Studio**.</span></span>  
1. <span data-ttu-id="407fd-197">[インストール **のテストと配布] を**  >  **選択します**。</span><span class="sxs-lookup"><span data-stu-id="407fd-197">Select **Test and Distribute** > **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="アプリをクライアントにサイドロードする方法を示TeamsスクリーンショットをVisual Studio Code Teams Toolkit。":::

<span data-ttu-id="407fd-199">**または、**</span><span class="sxs-lookup"><span data-stu-id="407fd-199">**Alternatively**</span></span>

1. <span data-ttu-id="407fd-200">**F5 キーを選択して** ブラウザー ウィンドウを開き、インストールします。</span><span class="sxs-lookup"><span data-stu-id="407fd-200">Select the **F5** key to open browser window to install.</span></span> <span data-ttu-id="407fd-201">これにより、App **Studio** のインストール プロセスがスキップされ、ブラウザー Teamsが表示されます。</span><span class="sxs-lookup"><span data-stu-id="407fd-201">This will skip the installation process in the **App Studio** and lauch Teams in your browser.</span></span>
1. <span data-ttu-id="407fd-202">インストール ダイアログで、[追加]**を選択** して、アプリをインストールTeams。</span><span class="sxs-lookup"><span data-stu-id="407fd-202">In the installation dialog, select **Add** to install your app to Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="アプリをクライアントにサイドロードする方法を示Teamsスクリーンショット。":::

   > [!Note]
   > <span data-ttu-id="407fd-204">App Studio は、クライアントのスタンドアロン アプリTeamsもあります。</span><span class="sxs-lookup"><span data-stu-id="407fd-204">App Studio is also available as a stand-alone app for Teams client.</span></span>

### <a name="troubleshoot-sideloading-issues"></a><span data-ttu-id="407fd-205">サイドローディングの問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="407fd-205">Troubleshoot sideloading issues</span></span>

<span data-ttu-id="407fd-206">**インストールに失敗しました**</span><span class="sxs-lookup"><span data-stu-id="407fd-206">**Installation failed**</span></span>

<span data-ttu-id="407fd-207">アプリのインストール中にエラー メッセージが表示される場合は、アプリ `Manifest parsing has failed` 情報が正しく入力されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="407fd-207">If the `Manifest parsing has failed` error message appears while installing your app, verify that the app information is correctly entered.</span></span>

<span data-ttu-id="407fd-208">**アプリ情報を確認するには**</span><span class="sxs-lookup"><span data-stu-id="407fd-208">**To verify the app information**</span></span>

* <span data-ttu-id="407fd-209">次のTeams Toolkit **App Studio App** の詳細に移動し、必要なすべての情報が正しく  >  入力されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="407fd-209">In the Teams Toolkit, go to **App Studio** > **App details** and verify that all the required information is correctly entered.</span></span>
*  <span data-ttu-id="407fd-210">ファイルを手動で編集した場合は、APP Studio のアプリ マニフェスト ツールで JSON が適切に定義 `manifest.json` されている必要があります。 </span><span class="sxs-lookup"><span data-stu-id="407fd-210">If you manually edited the `manifest.json` file, verify that the JSON is well-defined in the **App Manifest** tool in App Studio.</span></span>

<span data-ttu-id="407fd-211">**タブ コンテンツが表示されない**</span><span class="sxs-lookup"><span data-stu-id="407fd-211">**Tab content not displayed**</span></span>

<span data-ttu-id="407fd-212">アプリが実行されているのを確認します。</span><span class="sxs-lookup"><span data-stu-id="407fd-212">Verify that your app is running.</span></span> <span data-ttu-id="407fd-213">ない場合は、ターミナルに移動して実行します `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="407fd-213">If it isn't, go to the terminal and run `npm start`.</span></span>

## <a name="see-also"></a><span data-ttu-id="407fd-214">関連項目</span><span class="sxs-lookup"><span data-stu-id="407fd-214">See also</span></span>

* [<span data-ttu-id="407fd-215">Microsoft 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="407fd-215">Prepare your Microsoft 365 tenant</span></span>](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [<span data-ttu-id="407fd-216">アプリのテストとデバッグを行うセットアップMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="407fd-216">Choosing a setup to test and debug your Microsoft Teams app</span></span>](../concepts/build-and-test/debug.md)
* [<span data-ttu-id="407fd-217">JavaScript クライアント SDK を使用してタブやその他のホストMicrosoft Teamsエクスペリエンスを構築する</span><span class="sxs-lookup"><span data-stu-id="407fd-217">Building tabs and other hosted experiences with the Microsoft Teams JavaScript client SDK</span></span>](../tabs/how-to/using-teams-client-sdk.md)
* [<span data-ttu-id="407fd-218">AppSource 申請の準備</span><span class="sxs-lookup"><span data-stu-id="407fd-218">Prepare for AppSource submission</span></span>](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [<span data-ttu-id="407fd-219">Microsoft Teams 用の App Studio を使用してアプリをすばやく開発する</span><span class="sxs-lookup"><span data-stu-id="407fd-219">Quickly develop apps with App Studio for Microsoft Teams</span></span>](../concepts/build-and-test/app-studio-overview.md)
* [<span data-ttu-id="407fd-220">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="407fd-220">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a><span data-ttu-id="407fd-221">次の手順</span><span class="sxs-lookup"><span data-stu-id="407fd-221">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="407fd-222">ユーザーの個人用タブを作成Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="407fd-222">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
