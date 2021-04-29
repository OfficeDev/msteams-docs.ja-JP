---
title: はじめに - 最初のアプリを構築して実行する
author: girliemac
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 Microsoft Teams のツールキットを使用したメッセージ。"
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: b34409919f073535c741a48edf30f3edd8c6bc8f
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068783"
---
# <a name="create-your-first-microsoft-teams-app"></a><span data-ttu-id="f7b97-104">最初の Microsoft Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="f7b97-104">Create your first Microsoft Teams app</span></span>

<span data-ttu-id="f7b97-105">このクイック スタートでは、"Hello, World! を表示する Microsoft Teams アプリをビルドして実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-105">This quickstart teaches you to build and run Microsoft Teams app that displays "Hello, World!"</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7b97-106">前提条件</span><span class="sxs-lookup"><span data-stu-id="f7b97-106">Prerequisites</span></span>

<span data-ttu-id="f7b97-107">開始する前に、Teams 開発テナント [をセットアップし、Teams](#set-up-your-teams-development-tenant) [開発ツールをインストールする必要があります](#install-your-development-tools)。</span><span class="sxs-lookup"><span data-stu-id="f7b97-107">Before you begin, you need to [set up your Teams development tenant](#set-up-your-teams-development-tenant) and [install your Teams development tools](#install-your-development-tools).</span></span>

### <a name="set-up-your-teams-development-tenant"></a><span data-ttu-id="f7b97-108">Teams 開発テナントをセットアップする</span><span class="sxs-lookup"><span data-stu-id="f7b97-108">Set up your Teams development tenant</span></span>

<span data-ttu-id="f7b97-109">テナント **は** 、組織のコンテナーに似たものになります。</span><span class="sxs-lookup"><span data-stu-id="f7b97-109">A **tenant** is like a container for an organization.</span></span> <span data-ttu-id="f7b97-110">Teams の用語では、テナントとは、その組織のチャット、ファイルの共有、会議の実行を行うユーザーです。</span><span class="sxs-lookup"><span data-stu-id="f7b97-110">In Teams terms, a tenant is where people from that org chat, share files, and run meetings.</span></span> <span data-ttu-id="f7b97-111">開発者は、構築する Teams アプリをサイドロードしてテストするテナントが必要です。</span><span class="sxs-lookup"><span data-stu-id="f7b97-111">As a developer, you need a tenant to sideload and test the Teams apps that you are building.</span></span>  

# <a name="do-not-have-a-tenant"></a>[<span data-ttu-id="f7b97-112">テナントを持たない</span><span class="sxs-lookup"><span data-stu-id="f7b97-112">Do not have a tenant</span></span>](#tab/do-not-have-a-tenant)

<span data-ttu-id="f7b97-113">Microsoft 365 開発者プログラムに参加することで、アプリのサイドローディングを許可するテナントを含む無料の Teams テスト アカウントを取得できます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-113">You can get a free Teams test account, which includes a tenant that allows app sideloading, by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="f7b97-114">登録プロセスには約 2 分かかります。</span><span class="sxs-lookup"><span data-stu-id="f7b97-114">The registration process takes approximately two minutes.</span></span>

<span data-ttu-id="f7b97-115">**テナントを取得するには**</span><span class="sxs-lookup"><span data-stu-id="f7b97-115">**To get a tenant**</span></span>

1. <span data-ttu-id="f7b97-116">[Microsoft 365 開発者プログラムに移動します](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="f7b97-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="f7b97-117">[今 **すぐ参加] を** 選択し、画面の指示に従います。</span><span class="sxs-lookup"><span data-stu-id="f7b97-117">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="f7b97-118">[ようこそ] 画面で **、[E5 サブスクリプションの設定] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f7b97-118">In the Welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="f7b97-119">Microsoft 365 開発者アカウントを設定します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-119">Set up your Microsoft 365 developer account.</span></span> 
   <span data-ttu-id="f7b97-120">完了すると、次の画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-120">After you finish, the following screen appears:</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後に表示される例。":::

1. <span data-ttu-id="f7b97-122">新しいアカウントで Teams にサインインします。</span><span class="sxs-lookup"><span data-stu-id="f7b97-122">Sign in to Teams with your new account.</span></span>
1. <span data-ttu-id="f7b97-123">Teams クライアントで、[アプリ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f7b97-123">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="f7b97-124">[カスタム アプリのアップロード] **オプションが表示されるのを確認** します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-124">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="f7b97-125">これを行う場合は、アプリをサイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-125">If you do, this means you can sideload apps.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams でカスタム アプリをアップロードできる場所を示す図。":::

# <a name="have-a-tenant"></a>[<span data-ttu-id="f7b97-127">テナントを持つ</span><span class="sxs-lookup"><span data-stu-id="f7b97-127">Have a tenant</span></span>](#tab/have-a-tenant)

<span data-ttu-id="f7b97-128">テナントが既にある場合は、Teams でアプリをサイドロードできるのか確認します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-128">If you already have a tenant, verify if you can sideload apps in Teams.</span></span>

<span data-ttu-id="f7b97-129">**アプリをサイドロードできると確認する**</span><span class="sxs-lookup"><span data-stu-id="f7b97-129">**Verify that you can sideload your apps**</span></span> 

1. <span data-ttu-id="f7b97-130">Teams クライアントで、[アプリ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f7b97-130">In the Teams Client, select **Apps**.</span></span> 
1.  <span data-ttu-id="f7b97-131">[カスタム アプリのアップロード] **オプションが表示されるのを確認** します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-131">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="f7b97-132">これを行う場合は、アプリをサイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-132">If you do, this means you can sideload apps.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams でカスタム アプリをアップロードできる場所を示す図。":::

---

### <a name="install-your-development-tools"></a><span data-ttu-id="f7b97-134">開発ツールのインストール</span><span class="sxs-lookup"><span data-stu-id="f7b97-134">Install your development tools</span></span>

<span data-ttu-id="f7b97-135">このアプリをビルドするには、Teams ToolkitコードVisual Studioすぐに開始します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-135">To build this app, you'll use the Teams Toolkit for Visual Studio Code to quickly get started.</span></span> <span data-ttu-id="f7b97-136">また、任意のプレファード ツールを使用して Teams アプリをビルドすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-136">You can also build Teams apps with any ofyour preffered tools.</span></span> 

> [!NOTE]
> <span data-ttu-id="f7b97-137">Teams は、HTTPS 接続を介してアプリのコンテンツのみを表示します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-137">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="f7b97-138">ボットなど、特定の種類のアプリをローカルでデバッグするには、ngrok を使用して Teams とアプリの間にセキュリティで保護されたトンネルを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-138">To debug certain types of apps locally, such as a bot, you'll learn how to use ngrok to set up a secure tunnel between Teams and your app.</span></span>
> 
> <span data-ttu-id="f7b97-139">Production Teams アプリはクラウドでホストされます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-139">Production Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="f7b97-140">**Microsoft Teams ツールをインストールするには**</span><span class="sxs-lookup"><span data-stu-id="f7b97-140">**To install Microsoft Teams tools**</span></span>

1. <span data-ttu-id="f7b97-141">[Node.js](https://nodejs.org/en/) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="f7b97-141">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="f7b97-142">ボットまたはメッセージング拡張機能を作成する場合は [、ngrok](https://ngrok.com/download) をインストールし [、ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)を使用してローカル ホストをインターネットに公開します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-142">If you plan to build a bot or messaging extension, install [ngrok](https://ngrok.com/download) and [expose your localhost to the Internet using ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="f7b97-143">最新バージョンのコードを [インストールVisual Studioします](https://code.visualstudio.com/download)。</span><span class="sxs-lookup"><span data-stu-id="f7b97-143">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f7b97-144">ツールキットは、以前のバージョンのコードをVisual Studioされていません。</span><span class="sxs-lookup"><span data-stu-id="f7b97-144">The toolkit does not support earlier versions of Visual Studio Code.</span></span>

1. 左側のアクティビティ バーで、[拡張機能] **を選択します** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: 。
1. <span data-ttu-id="f7b97-146">**[Microsoft Teams Toolkit]** で、[インストール] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f7b97-146">In **Microsoft Teams Toolkit**, select **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="コード内の Microsoft Teams Visual Studio拡張機能をインストールできる場所を示Toolkit図。":::

## <a name="1-create-your-app-project"></a><span data-ttu-id="f7b97-148">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="f7b97-148">1. Create your app project</span></span>

1. <span data-ttu-id="f7b97-149">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-149">Open Visual Studio Code.</span></span>
1. [Microsoft **Teams] を選択Toolkit** :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **Teams アプリを作成します**。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="アプリ プロジェクトを作成する方法を示Visual Studio Code Teams Toolkit。":::
   
1. <span data-ttu-id="f7b97-152">Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="f7b97-152">Sign in with your Microsoft 365 development account.</span></span> <span data-ttu-id="f7b97-153">作成したアカウントか、アプリのサイドローディングを許可するアカウントのどちらかです。</span><span class="sxs-lookup"><span data-stu-id="f7b97-153">Either the one you just created or the account you already had that allows app sideloading.</span></span>
1. <span data-ttu-id="f7b97-154">[プロジェクトの **選択] 画面** で、[個人用アプリ] に **移動し** 、[次へ] の **[JS** (JavaScript) > **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f7b97-154">On the **Select project** screen, go to **Personal app** and select **JS** (JavaScript) > **Next**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Visual Studio Code Teams ツールキットを使用して、アプリ プロジェクトを構成する方法を示すスクリーンショット。":::

1. <span data-ttu-id="f7b97-156">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-156">Enter a name for your Teams app.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="アプリ プロジェクトに名前を追加する方法を示すスクリーンショットで、コード Teams Visual StudioをToolkit。":::

1. <span data-ttu-id="f7b97-158">[**完了**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-158">Select **Finish**.</span></span> 
   <span data-ttu-id="f7b97-159">これで、プロジェクトが構成されます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-159">Your project is now configured.</span></span> 

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="f7b97-160">2. アプリ プロジェクト コンポーネントについて</span><span class="sxs-lookup"><span data-stu-id="f7b97-160">2. Understand your app project components</span></span>

<span data-ttu-id="f7b97-161">ツールキットでアプリ プロジェクトを構成した後、"Hello, World!</span><span class="sxs-lookup"><span data-stu-id="f7b97-161">After the toolkit configures your app project, you have the components to build your "Hello, World!"</span></span> <span data-ttu-id="f7b97-162">Teams アプリ。</span><span class="sxs-lookup"><span data-stu-id="f7b97-162">Teams app.</span></span> <span data-ttu-id="f7b97-163">プロジェクトのディレクトリとファイルは、コード エクスプローラー Visual Studioにあります。</span><span class="sxs-lookup"><span data-stu-id="f7b97-163">The project's directories and files are located in the Visual Studio Code Explorer.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="アプリ プロジェクトのスキャフォールディングを示すスクリーンショットと、Visual Studio Teams Toolkit。":::

<span data-ttu-id="f7b97-165">ツールキットは、セットアップ時に追加した機能に基づいて、ディレクトリにアプリスキャフォールディング `src` を自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-165">The toolkit automatically creates app scaffolding in the `src` directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="f7b97-166">セットアップ中にタブを作成したので、ディレクトリ内のファイルはアプリの初期化と `App.js` `src/components` ルーティングを処理します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-166">Since you created a tab during setup, the `App.js` file in the `src/components` directory handles the initialization and routing of your app.</span></span> <span data-ttu-id="f7b97-167">このファイルは、Microsoft Teams JavaScript クライアント SDK を呼び出して、アプリと Teams の間の通信を確立します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-167">The file also calls the Microsoft Teams JavaScript client SDK to establish communication between your app and Teams.</span></span> 

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="f7b97-168">3. アプリの構築と実行</span><span class="sxs-lookup"><span data-stu-id="f7b97-168">3. Build and run your app</span></span>

<span data-ttu-id="f7b97-169">アプリをローカルに構築して実行することで、時間を節約できます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-169">Build and run your app locally to save time.</span></span> 

<span data-ttu-id="f7b97-170">**アプリをビルドして実行するには**</span><span class="sxs-lookup"><span data-stu-id="f7b97-170">**To build and run your app**</span></span>

1. <span data-ttu-id="f7b97-171">[コードVisual Studioで、[ターミナルの表示 **] を**  >  **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f7b97-171">In Visual Studio Code, select **View** > **Terminal**.</span></span>
1. <span data-ttu-id="f7b97-172">`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-172">Run `npm install`.</span></span>
1. <span data-ttu-id="f7b97-173">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-173">Run `npm start`.</span></span>
  
  <span data-ttu-id="f7b97-174">コンパイル **が正常に完了しました。**</span><span class="sxs-lookup"><span data-stu-id="f7b97-174">A **Compiled successfully!**</span></span> <span data-ttu-id="f7b97-175">メッセージがターミナルに表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-175">message appears in the terminal.</span></span> <span data-ttu-id="f7b97-176">これで、アプリが localhost で実行されています `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="f7b97-176">Your app is now running on your localhost at `https://localhost:3000`.</span></span> 

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="f7b97-177">4. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="f7b97-177">4. Sideload your app in Teams</span></span>

<span data-ttu-id="f7b97-178">サイドローディングとは、管理者または Microsoft によって承認されていないアプリを Teams にインストールするプロセスです。</span><span class="sxs-lookup"><span data-stu-id="f7b97-178">Sideloading is the process of installing an app in Teams that hasn't been approved by your admin or Microsoft.</span></span> <span data-ttu-id="f7b97-179">サイドローディングは、Teams アプリのテストとデバッグを行う場合に一般的です。</span><span class="sxs-lookup"><span data-stu-id="f7b97-179">Sideloading is common when testing and debugging Teams apps.</span></span>

<span data-ttu-id="f7b97-180">既定では、Teams ではアプリのサイドローディングは許可されません。</span><span class="sxs-lookup"><span data-stu-id="f7b97-180">By default, Teams doesn't allow app sideloading.</span></span> <span data-ttu-id="f7b97-181">この設定は、Teams 管理センターで変更できます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-181">You can change this setting in the Teams admin center.</span></span>

<span data-ttu-id="f7b97-182">**Teams でアプリのサイドローディングを有効にするには**</span><span class="sxs-lookup"><span data-stu-id="f7b97-182">**To enable app sideloading in Teams**</span></span>

1. <span data-ttu-id="f7b97-183">管理者資格情報を [使用して Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) 管理センターにサインインします。</span><span class="sxs-lookup"><span data-stu-id="f7b97-183">Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>  
1. <span data-ttu-id="f7b97-184">[**すべての** > **Teams の表示**]を選択します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-184">Select **Show All** > **Teams**.</span></span> 

   ![管理センター メニューの画像](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > <span data-ttu-id="f7b97-186">Teams オプションが表示されるには、最大で 24 **時間かかる** 場合があります。</span><span class="sxs-lookup"><span data-stu-id="f7b97-186">It can take up to 24 hours for the **Teams** option to appear.</span></span> 

1. <span data-ttu-id="f7b97-187">[Teams アプリ **の**  >  **セットアップ ポリシー] グローバル**  >  (**組織** 全体の既定) に移動します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-187">Go to **Teams apps** > **Setup policies** > **Global** (Org-wide default).</span></span>

   ![sideload ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. <span data-ttu-id="f7b97-189">[カスタム アプリの **アップロード] トグルをオン** にします。</span><span class="sxs-lookup"><span data-stu-id="f7b97-189">Turn on the **upload custom apps** toggle.</span></span>

1. <span data-ttu-id="f7b97-190">[保存 **] を** 選択して変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-190">Select **Save** to save the changes.</span></span>

   <span data-ttu-id="f7b97-191">テスト テナントでカスタム アプリのサイドローディングが許可されます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-191">Your test tenant now allows custom app sideloading.</span></span>

   > [!Note]
   > <span data-ttu-id="f7b97-192">ツールキットに含まれている App Studio の検証機能を使用してアプリをサイドロードする前に問題を確認します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-192">Check for issues before sideloading your app using the validation feature in App Studio, which is included in the toolkit.</span></span> <span data-ttu-id="f7b97-193">エラーを修正して、アプリを正常にサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="f7b97-193">Fix the errors to successfully sideload the app.</span></span>


### <a name="sideload-your-app"></a><span data-ttu-id="f7b97-194">アプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="f7b97-194">Sideload your app</span></span>

1. <span data-ttu-id="f7b97-195">[Visual Studioコード] で、Teams ファイルを開Toolkit。</span><span class="sxs-lookup"><span data-stu-id="f7b97-195">In Visual Studio Code, open the Teams Toolkit.</span></span>
1. <span data-ttu-id="f7b97-196">[App **Studio] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="f7b97-196">Go to **App Studio**.</span></span>  
1. <span data-ttu-id="f7b97-197">[インストール **のテストと配布] を**  >  **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f7b97-197">Select **Test and Distribute** > **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="アプリを Teams クライアントにサイドロードする方法を示すスクリーンショットで、Visual Studio Teams Toolkit。":::

<span data-ttu-id="f7b97-199">**または、**</span><span class="sxs-lookup"><span data-stu-id="f7b97-199">**Alternatively**</span></span>

1. <span data-ttu-id="f7b97-200">**F5 キーを選択して** ブラウザー ウィンドウを開き、インストールします。</span><span class="sxs-lookup"><span data-stu-id="f7b97-200">Select the **F5** key to open browser window to install.</span></span> <span data-ttu-id="f7b97-201">これにより、ブラウザーの **App Studio** とラウチ Teams のインストール プロセスがスキップされます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-201">This will skip the installation process in the **App Studio** and lauch Teams in your browser.</span></span>
1. <span data-ttu-id="f7b97-202">インストール ダイアログで、[追加] を **選択** して、アプリを Teams にインストールします。</span><span class="sxs-lookup"><span data-stu-id="f7b97-202">In the installation dialog, select **Add** to install your app to Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="アプリを Teams クライアントにサイドロードする方法を示すスクリーンショット。":::

   > [!Note]
   > <span data-ttu-id="f7b97-204">App Studio は、Teams クライアント用のスタンドアロン アプリとして利用することもできます。</span><span class="sxs-lookup"><span data-stu-id="f7b97-204">App Studio is also available as a stand-alone app for Teams client.</span></span>

### <a name="troubleshoot-sideloading-issues"></a><span data-ttu-id="f7b97-205">サイドローディングの問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="f7b97-205">Troubleshoot sideloading issues</span></span>

<span data-ttu-id="f7b97-206">**インストールに失敗しました**</span><span class="sxs-lookup"><span data-stu-id="f7b97-206">**Installation failed**</span></span>

<span data-ttu-id="f7b97-207">アプリのインストール中にエラー メッセージが表示される場合は、アプリ `Manifest parsing has failed` 情報が正しく入力されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-207">If the `Manifest parsing has failed` error message appears while installing your app, verify that the app information is correctly entered.</span></span>

<span data-ttu-id="f7b97-208">**アプリ情報を確認するには**</span><span class="sxs-lookup"><span data-stu-id="f7b97-208">**To verify the app information**</span></span>

* <span data-ttu-id="f7b97-209">Teams の設定Toolkit App Studio **App** の詳細に移動し、必要なすべての情報が正しく  >  入力されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-209">In the Teams Toolkit, go to **App Studio** > **App details** and verify that all the required information is correctly entered.</span></span>
*  <span data-ttu-id="f7b97-210">ファイルを手動で編集した場合は、APP Studio のアプリ マニフェスト ツールで JSON が適切に定義 `manifest.json` されている必要があります。 </span><span class="sxs-lookup"><span data-stu-id="f7b97-210">If you manually edited the `manifest.json` file, verify that the JSON is well-defined in the **App Manifest** tool in App Studio.</span></span>

<span data-ttu-id="f7b97-211">**タブ コンテンツが表示されない**</span><span class="sxs-lookup"><span data-stu-id="f7b97-211">**Tab content not displayed**</span></span>

<span data-ttu-id="f7b97-212">アプリが実行されているのを確認します。</span><span class="sxs-lookup"><span data-stu-id="f7b97-212">Verify that your app is running.</span></span> <span data-ttu-id="f7b97-213">ない場合は、ターミナルに移動して実行します `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="f7b97-213">If it isn't, go to the terminal and run `npm start`.</span></span>

## <a name="see-also"></a><span data-ttu-id="f7b97-214">関連項目</span><span class="sxs-lookup"><span data-stu-id="f7b97-214">See also</span></span>

* [<span data-ttu-id="f7b97-215">Microsoft 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="f7b97-215">Prepare your Microsoft 365 tenant</span></span>](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [<span data-ttu-id="f7b97-216">Microsoft Teams アプリをテストおよびデバッグするためのセットアップの選択</span><span class="sxs-lookup"><span data-stu-id="f7b97-216">Choosing a setup to test and debug your Microsoft Teams app</span></span>](../concepts/build-and-test/debug.md)
* [<span data-ttu-id="f7b97-217">Microsoft Teams JavaScript クライアント SDK でタブやその他のホストされたエクスペリエンスを構築する</span><span class="sxs-lookup"><span data-stu-id="f7b97-217">Building tabs and other hosted experiences with the Microsoft Teams JavaScript client SDK</span></span>](../tabs/how-to/using-teams-client-sdk.md)
* [<span data-ttu-id="f7b97-218">AppSource 申請の準備</span><span class="sxs-lookup"><span data-stu-id="f7b97-218">Prepare for AppSource submission</span></span>](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [<span data-ttu-id="f7b97-219">Microsoft Teams 用の App Studio を使用してアプリをすばやく開発する</span><span class="sxs-lookup"><span data-stu-id="f7b97-219">Quickly develop apps with App Studio for Microsoft Teams</span></span>](../concepts/build-and-test/app-studio-overview.md)
* [<span data-ttu-id="f7b97-220">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="f7b97-220">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a><span data-ttu-id="f7b97-221">次の手順</span><span class="sxs-lookup"><span data-stu-id="f7b97-221">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7b97-222">Microsoft Teams の個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="f7b97-222">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
