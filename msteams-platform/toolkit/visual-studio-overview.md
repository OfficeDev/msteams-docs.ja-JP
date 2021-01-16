---
title: Microsoft Teams を使用してアプリを構築ToolkitとVisual Studio
description: Microsoft Teams を使用して、アプリ内で直接、Visual Studioカスタム アプリの構築を開始Toolkit
keywords: Teams Visual Studio ツールキット
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 08df1d3907a1a3683eb42222e247cd7fd6c0177b
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875008"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="9700a-104">Teams を使用してアプリを構築ToolkitとVisual Studio</span><span class="sxs-lookup"><span data-stu-id="9700a-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="9700a-105">Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="9700a-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="9700a-106">Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="9700a-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9700a-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="9700a-107">Prerequisites</span></span>

1. [<span data-ttu-id="9700a-108">開発者プレビューを有効にする</span><span class="sxs-lookup"><span data-stu-id="9700a-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="9700a-109">新しい ASP.NE **<span></span>T と Web 開発** モジュールが新しいインスタンスに追加Visual Studioします。</span><span class="sxs-lookup"><span data-stu-id="9700a-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="9700a-110">ワークロードとコンポーネントのドキュメントを追加または削除することで、Visual Studioの手順 [に従って確認](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) できます。</span><span class="sxs-lookup"><span data-stu-id="9700a-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![Visual Studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="9700a-112">Visual Studio から展開してアプリをテストする場合は、IIS (インターネット インフォメーション サービス) をご使用の環境にインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9700a-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="9700a-113">Visual Studio IIS は含まれていないので、既定の Windows 10、Windows 8、または Windows 7 の構成には含まれません。ただし、Microsoft ダウンロード センターから最新バージョン [をダウンロードできます](https://www.microsoft.com/download/details.aspx?id=48264)。</span><span class="sxs-lookup"><span data-stu-id="9700a-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="9700a-115">Teams のインストールToolkit</span><span class="sxs-lookup"><span data-stu-id="9700a-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="9700a-116">Microsoft Teams Toolkit Visual Studioは、Visual Studio [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)から、または Visual Studio 内の [拡張機能]メニューから直接ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="9700a-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="9700a-117">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="9700a-117">Using the toolkit</span></span>

- [<span data-ttu-id="9700a-118">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="9700a-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="9700a-119">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="9700a-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="9700a-120">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="9700a-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="9700a-121">Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="9700a-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="9700a-122">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="9700a-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="9700a-123">アプリを公開する</span><span class="sxs-lookup"><span data-stu-id="9700a-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="9700a-124">新しい Teams プロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="9700a-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="9700a-125">[新 **しいプロジェクトの作成] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="9700a-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="9700a-126">**Microsoft Teams アプリを選択し、[** 次へ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="9700a-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="9700a-127">[新しいプロジェクトの **構成**] 画面に移動し、[プロジェクト名]、[場所]、および [ソリューション名] を **選択できます**。</span><span class="sxs-lookup"><span data-stu-id="9700a-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="9700a-128">[ソリューションとプロジェクトを **同じディレクトリに配置する] チェック ボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="9700a-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="9700a-129">[機能の追加] という名前のポップアップ ウィンドウでは、プロジェクトのセットアップに 1 つ以上の機能を選択できます。</span><span class="sxs-lookup"><span data-stu-id="9700a-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="9700a-130">[次へ **] ボタン** を選択して、構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="9700a-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="9700a-131">[機能の追加] というラベルの付いたポップアップ ウィンドウでは、選択した各機能のプロパティを選択できます。</span><span class="sxs-lookup"><span data-stu-id="9700a-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="9700a-132">[ **完了]** を選択すると **、Microsoft Teams** Toolkitランディング ページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9700a-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="9700a-133">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="9700a-133">Configure your app</span></span>

<span data-ttu-id="9700a-134">その中核をなす Teams アプリには、次の 3 つのコンポーネントが含されています。</span><span class="sxs-lookup"><span data-stu-id="9700a-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="9700a-135">ユーザーがアプリを操作する Microsoft Teams クライアント (Web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="9700a-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="9700a-136">Html タブ コンテンツやボット アダプティブ カードなど、Teams に表示されるコンテンツの要求に応答するサーバー。</span><span class="sxs-lookup"><span data-stu-id="9700a-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="9700a-137">次の 3 [つのファイルで構成](/concepts/build-and-test/apps-package.md) される Teams アプリ パッケージ。</span><span class="sxs-lookup"><span data-stu-id="9700a-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="9700a-138">the manifest.json</span><span class="sxs-lookup"><span data-stu-id="9700a-138">The manifest.json</span></span>
  > - <span data-ttu-id="9700a-139">パブリック [または組織](../resources/schema/manifest-schema.md#icons) のアプリ カタログに表示するアプリの色アイコン</span><span class="sxs-lookup"><span data-stu-id="9700a-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="9700a-140">Teams [アクティビティ バー](../resources/schema/manifest-schema.md#icons) に表示するアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="9700a-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="9700a-141">アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="9700a-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="9700a-142">まだサインインしていない場合は、Microsoft 365 またはアカウントにサインインして、開発プロセスを続行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9700a-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="9700a-143">Microsoft 365 アカウントをお持ちない場合は [、Microsoft 365 Developer Program サブスクリプションにサインアップ](https://developer.microsoft.com/microsoft-365/dev-program) できます。</span><span class="sxs-lookup"><span data-stu-id="9700a-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="9700a-144">これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="9700a-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="9700a-145">Visual Studio *Enterprise* または *Professional* サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。</span><span class="sxs-lookup"><span data-stu-id="9700a-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="9700a-146">「*Microsoft 365 開発者サブスクリプションを設定する*」[を参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="9700a-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="9700a-147">構成の手順</span><span class="sxs-lookup"><span data-stu-id="9700a-147">Configuration steps</span></span>

1. <span data-ttu-id="9700a-148">アプリを構成するには **、Microsoft Teams** Toolkitランディング ページで、[アプリ パッケージの編集 **] を選択します** 。</span><span class="sxs-lookup"><span data-stu-id="9700a-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="9700a-149">[マイ環境 **] ドロップダウン メニュー** から [開発] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="9700a-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="9700a-150">アプリのプロパティ フィールド **を編集** できる [アプリの詳細] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9700a-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="9700a-151">[アプリの詳細] ページのフィールドを編集すると、最終的にアプリ パッケージの一部として出荷される manifest.jsのコンテンツが更新されます。</span><span class="sxs-lookup"><span data-stu-id="9700a-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="9700a-152">詳細情報</span><span class="sxs-lookup"><span data-stu-id="9700a-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="9700a-153">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="9700a-153">Package your app</span></span>

<span data-ttu-id="9700a-154">アプリの詳細 **ページを変更** したり、マニフェストを更新したり、アプリの .publish フォルダー内の **.env** ファイルを更新したりすると、アプリのファイル **Development.zipされます。** </span><span class="sxs-lookup"><span data-stu-id="9700a-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="9700a-155">The Development.zip file includes three required files— **themanifest.json** and two [icons](../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="9700a-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="9700a-156">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="9700a-156">Install and run your app locally</span></span>

1. <span data-ttu-id="9700a-157">[ソリューション構成 **] ドロップダウン メニューの [** 展開] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="9700a-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![[ソリューション構成] メニュー](../assets/images/solution-configurations.png)

2. <span data-ttu-id="9700a-159">**[IIS Express + Teams] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="9700a-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="9700a-160">Teams が起動し、アプリのインストールダイアログが Teams クライアントに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9700a-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="9700a-161">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="9700a-161">Validate your app</span></span>

<span data-ttu-id="9700a-162">[ **検証** ] ページでは、AppSource にアプリを提出する前にアプリ パッケージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="9700a-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="9700a-163">マニフェスト パッケージをアップロードするだけで、検証ツールはマニフェストに関連するテスト ケースすべてについてアプリをチェックします。</span><span class="sxs-lookup"><span data-stu-id="9700a-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="9700a-164">失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。</span><span class="sxs-lookup"><span data-stu-id="9700a-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="9700a-165">自動化が難しいテストについては、暫定チェックリストで、最も一般的なテスト ケースの 7 を詳しく示し、完全な提出チェックリストへのリンクを示します。</span><span class="sxs-lookup"><span data-stu-id="9700a-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="9700a-166">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="9700a-166">Publish your app to Teams</span></span>

<span data-ttu-id="9700a-167">✔ホーム ページでは、チームにアプリをアップロードしたり、組織内のユーザー用に会社のカスタム アプリ ストアにアプリを提出したり、すべての Teams ユーザーのアプリ ソースにアプリを提出することができます。</span><span class="sxs-lookup"><span data-stu-id="9700a-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="9700a-168">✔ IT 管理者がこれらの提出を確認します。</span><span class="sxs-lookup"><span data-stu-id="9700a-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="9700a-169">✔発行ページに戻り、申請の状態を確認し、アプリが IT 管理者によって承認または拒否されたのか確認できます。また、アプリに更新プログラムを提出したり、現在アクティブな申請を取り消したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="9700a-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9700a-170">次の手順: 公開されたアプリの保守とサポート</span><span class="sxs-lookup"><span data-stu-id="9700a-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
