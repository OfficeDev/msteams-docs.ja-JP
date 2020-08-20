---
title: Microsoft Teams と Microsoft Teams のアプリをToolkitアプリをVisual Studio
description: Microsoft Teams アプリを使用して、Visual Studio 内で直接カスタム アプリを構築Toolkit
keywords: teams visual studio Toolkit
ms.topic: overview
ms.openlocfilehash: 79ea22cfd154313247132c22684d444c0813c66f
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819204"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="ac55f-104">Microsoft Teams と Microsoft Teams のアプリをToolkitアプリをVisual Studio</span><span class="sxs-lookup"><span data-stu-id="ac55f-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="ac55f-105">Microsoft Teams の展開Toolkitカスタムの Teams アプリをカスタム統合開発環境 (IDE) 内Visual Studio作成することができます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="ac55f-106">Microsoft Teams ツールキットには、プロセス全体が示され、Teams アプリの構築、デバッグ、起動に必要なものがすべて含まれます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac55f-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="ac55f-107">Prerequisites</span></span>

1. [<span data-ttu-id="ac55f-108">開発者プレビューを有効にする</span><span class="sxs-lookup"><span data-stu-id="ac55f-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="ac55f-109">このプロジェクト パーツ **<span>ASP.NE</span>と Web 開発モジュールが** ユーザーのクラス インスタンスに追加Visual Studioします。</span><span class="sxs-lookup"><span data-stu-id="ac55f-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="ac55f-110">ワークロードおよびコンポーネントのドキュメントを追加または削除する [Visual Studio手順を実行することで、確認](/visualstudio/install/modify-visual-studio?view=vs-2019) できます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019) documentation.</span></span>

![Visual Studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="ac55f-112">アプリを Visual Studio から展開してテストする場合は、開発環境で IIS (インターネット インフォメーション サービス) をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ac55f-112">If you would like test your app by deploy it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="ac55f-113">Visual Studioは IIS を含まれていません。既定の Windows 10 構成、Windows 8 構成、Windows 7 構成には含まれていません。ただし、最新バージョンは、Microsoft ダウンロード センター [からダウンロードできます](https://www.microsoft.com/download/details.aspx?id=48264)。</span><span class="sxs-lookup"><span data-stu-id="ac55f-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="ac55f-115">Teams モードをインストールToolkit</span><span class="sxs-lookup"><span data-stu-id="ac55f-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="ac55f-116">Microsoft Teams Toolkit for Visual Studioは [、Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) からダウンロードするか、Visual Studio に含まれる **[拡張機能]** メニューから直接ダウンロードVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="ac55f-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="ac55f-117">ツールキットを使用する</span><span class="sxs-lookup"><span data-stu-id="ac55f-117">Using the toolkit</span></span>

- [<span data-ttu-id="ac55f-118">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="ac55f-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="ac55f-119">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="ac55f-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="ac55f-120">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="ac55f-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="ac55f-121">Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="ac55f-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="ac55f-122">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="ac55f-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="ac55f-123">アプリの発行</span><span class="sxs-lookup"><span data-stu-id="ac55f-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="ac55f-124">新しい Teams プロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="ac55f-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="ac55f-125">[新 **しいプロジェクトの作成] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="ac55f-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="ac55f-126">**[Microsoft Teams アプリ] を選択し、[** 次へ] を**選択します**。</span><span class="sxs-lookup"><span data-stu-id="ac55f-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="ac55f-127">[新しいプロジェクトを構成**します] 画面に表示**されます。この画面では、プロジェクト名、**場所、\*\*\*\*および**ソリューション名**を選択できます**。</span><span class="sxs-lookup"><span data-stu-id="ac55f-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="ac55f-128">同じディレクトリ内の **"Place solution" ボックスと "Project" というボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="ac55f-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="ac55f-129">[機能の追加] という **ポップアップ** ウィンドウを使用すると、プロジェクトのセットアップに関する 1 つ以上の機能を選択できます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="ac55f-130">[次へ **] ボタン** を選択して構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="ac55f-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="ac55f-131">ポップアップ ウィンドウの [機能の **追加]** が表示されていると、選択した各機能のプロパティを選択できます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="ac55f-132">[ **完了]** を選択すると **、Microsoft Teams** のランToolkit表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="ac55f-133">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="ac55f-133">Configure your app</span></span>

<span data-ttu-id="ac55f-134">Teams アプリの中心には、Teams アプリは 3 つのコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="ac55f-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="ac55f-135">ユーザーがアプリを操作する Microsoft Teams クライアント (Web、デスクトップ、モバイル)。</span><span class="sxs-lookup"><span data-stu-id="ac55f-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="ac55f-136">TEAMS に表示されるコンテンツの要求に応答するサーバー(HTML タブ コンテンツ、ボット アダプティブ カードなど)。</span><span class="sxs-lookup"><span data-stu-id="ac55f-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="ac55f-137">3 つの [ファイルで](/concepts/build-and-test/apps-package.md) 構成される Teams アプリ パッケージ:</span><span class="sxs-lookup"><span data-stu-id="ac55f-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="ac55f-138">メッセージmanifest.jsオン</span><span class="sxs-lookup"><span data-stu-id="ac55f-138">The manifest.json</span></span>
  > - <span data-ttu-id="ac55f-139">アプリ [がパブリック](../resources/schema/manifest-schema.md#icons) または組織のアプリ カタログに表示するための色アイコン</span><span class="sxs-lookup"><span data-stu-id="ac55f-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="ac55f-140">Teams [のアクティビティ](../resources/schema/manifest-schema.md#icons) バーに表示されるアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="ac55f-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="ac55f-141">アプリがインストールされると、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を判断します。</span><span class="sxs-lookup"><span data-stu-id="ac55f-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="ac55f-142">Microsoft 365 またはアカウントにサインインしていない場合は、開発プロセスを続行するには Microsoft 365 またはアカウントにサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ac55f-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="ac55f-143">Microsoft 365 アカウントをお持ての場合は [、Microsoft 365 開発者プログラム サブスクリプションにサインアップ](https://developer.microsoft.com/microsoft-365/dev-program) できます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="ac55f-144">無料版 *は* 90 日間無料で、開発アクティビティに使用している限り、引き続き更新されます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="ac55f-145">Visual Studio *Enterprise* または *Professional* サブスクリプションをお持つの場合、両方のプログラムに無料の Microsoft 365 [開発者サブスクリプションが含](https://aka.ms/MyVisualStudioBenefits)まれており、そのサブスクリプションの期間Visual Studioアクティブになります。</span><span class="sxs-lookup"><span data-stu-id="ac55f-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="ac55f-146">*Microsoft* [365 開発者サブスクリプションのセットアップを参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="ac55f-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="ac55f-147">構成の手順</span><span class="sxs-lookup"><span data-stu-id="ac55f-147">Configuration steps</span></span>

1. <span data-ttu-id="ac55f-148">アプリを構成するには **、[Microsoft Teams およびランド処理] Toolkit ページで、[アプリ パッケージの** 編集 **] を選択します** 。</span><span class="sxs-lookup"><span data-stu-id="ac55f-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="ac55f-149">[My **Environments] ドロップダウン メニュー** から [開発] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="ac55f-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="ac55f-150">アプリの詳細ページが **表示され** 、アプリのプロパティ フィールドを編集できます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="ac55f-151">アプリの詳細ページのフィールドを編集すると、ファイルに保存されている manifest.jsの内容が更新されます。この内容は、最終的にはアプリ パッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="ac55f-152">詳細情報</span><span class="sxs-lookup"><span data-stu-id="ac55f-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="ac55f-153">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="ac55f-153">Package your app</span></span>

<span data-ttu-id="ac55f-154">アプリの詳細 **ページを変更** したり、マニフェスト **を更新**したり **、アプリの .publish** フォルダーにある  **.env** ファイルを更新したりすると、ファイルが自動的 **Development.zip** されます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="ac55f-155">ファイルDevelopment.zipは、3 つの必須ファイル (オンおよび 2**つのアイコン ファイルmanifest.js含**[まれています](../concepts/build-and-test/apps-package.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="ac55f-155">The Development.zip file includes three required files — the **manifest.json** and [two icon files](../concepts/build-and-test/apps-package.md#icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="ac55f-156">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="ac55f-156">Install and run your app locally</span></span>

1. <span data-ttu-id="ac55f-157">[ソリューション構成 **] ドロップダウン メニュー** から、[展開] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="ac55f-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![[ソリューション構成] メニュー](../assets/images/solution-configurations.png)

2. <span data-ttu-id="ac55f-159">**[ISS Express + Teams] ボタンを選択**します。</span><span class="sxs-lookup"><span data-stu-id="ac55f-159">Select the **ISS Express + Teams** button.</span></span>

1. <span data-ttu-id="ac55f-160">Teams が起動し、アプリのインストール ダイアログが Teams クライアントに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="ac55f-161">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="ac55f-161">Validate your app</span></span>

<span data-ttu-id="ac55f-162">[ **検証]** ページでは、AppSource にアプリを提出する前にアプリ パッケージをチェックすることができます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="ac55f-163">マニフェスト パッケージと検証ツールは、単にマニフェストに関連するすべてのテスト ケースに対してアプリをチェックします。</span><span class="sxs-lookup"><span data-stu-id="ac55f-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="ac55f-164">失敗した各テストについて、説明にはエラーの修正に役立つドキュメントへのリンクが示されています。</span><span class="sxs-lookup"><span data-stu-id="ac55f-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="ac55f-165">自動化が簡単なテストの場合、テストが**Preliminary checklist**失敗する最も一般的なテスト ケースの暫定的なチェックリストの詳細 7 と、提出チェックリスト全体へのリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ac55f-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="ac55f-166">アプリを Teams に発行する</span><span class="sxs-lookup"><span data-stu-id="ac55f-166">Publish your app to Teams</span></span>

<span data-ttu-id="ac55f-167">✔ ホーム ページで、アプリをチームにアップロードしたり、組織内のユーザー用にアプリを会社のカスタム アプリ ストアに提出したり、すべての Teams ユーザーのアプリ ソースにアプリを提出したりできます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="ac55f-168">✔の IT 管理者がこれらの申請を確認します。</span><span class="sxs-lookup"><span data-stu-id="ac55f-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="ac55f-169">✔ページに戻り **、提出** のステータスを確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認できます。これは、アプリに更新プログラムを提出したり、現在アクティブな提出を取り消す場合にも使用できます。</span><span class="sxs-lookup"><span data-stu-id="ac55f-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac55f-170">次の手順: 公開されたアプリの管理とサポート</span><span class="sxs-lookup"><span data-stu-id="ac55f-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
