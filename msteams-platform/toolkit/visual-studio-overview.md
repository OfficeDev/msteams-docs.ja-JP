---
title: Microsoft Teams ToolkitとVisual Studioを使用してアプリを構築する
description: Microsoft Teams Toolkitを使用して、Visual Studio内で優れたカスタム アプリを直接構築し始める
keywords: チームビジュアルスタジオツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: eb94a8de0355283344ebe890a6fa3a3050e243ea
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566552"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="91f68-104">Teams ToolkitとVisual Studioを使用してアプリを構築する</span><span class="sxs-lookup"><span data-stu-id="91f68-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="91f68-105">Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="91f68-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="91f68-106">Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="91f68-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91f68-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="91f68-107">Prerequisites</span></span>

1. <span data-ttu-id="91f68-108">[開発者プレビューを有効に](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)する :</span><span class="sxs-lookup"><span data-stu-id="91f68-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="91f68-109">**<span>ASP.NE</span>T と Web 開発モジュール** がVisual Studioインスタンスに追加されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="91f68-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="91f68-110">ワークロードおよびコンポーネントのドキュメントを[追加または削除して、変更Visual Studio](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)の手順に従って確認できます。</span><span class="sxs-lookup"><span data-stu-id="91f68-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![ビジュアルスタジオ asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="91f68-112">Visual Studioからアプリを展開してテストする場合は、開発環境に IIS (インターネット インフォメーション サービス) をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="91f68-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="91f68-113">Visual Studioには IIS は含まれておらず、既定のWindows 10、Windows 8、または Windows 7 の構成には含まれません。ただし、最新バージョンは Microsoft ダウンロード[センター](https://www.microsoft.com/download/details.aspx?id=48264)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="91f68-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="91f68-115">Teams Toolkitをインストールする</span><span class="sxs-lookup"><span data-stu-id="91f68-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="91f68-116">Visual StudioのMicrosoft Teams Toolkitは [、Visual Studioマーケットプレース](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)から、またはVisual Studio内の **拡張機能** メニューから直接ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="91f68-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="91f68-117">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="91f68-117">Using the toolkit</span></span>

- [<span data-ttu-id="91f68-118">新しいプロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="91f68-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="91f68-119">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="91f68-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="91f68-120">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="91f68-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="91f68-121">Teamsでアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="91f68-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="91f68-122">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="91f68-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="91f68-123">アプリを公開する</span><span class="sxs-lookup"><span data-stu-id="91f68-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="91f68-124">新しいTeams プロジェクトを設定する</span><span class="sxs-lookup"><span data-stu-id="91f68-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="91f68-125">[ **新しいプロジェクトの作成 ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="91f68-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="91f68-126">[Microsoft Teams **アプリ] を** 選択し、[**次へ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="91f68-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="91f68-127">[**新しいプロジェクトの構成]** 画面で **、[Project名**]、[**場所**]、および **[ソリューション名**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="91f68-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="91f68-128">[ **ソリューションとプロジェクトを同じディレクトリに配置]** というラベルの付いたチェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="91f68-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="91f68-129">[ **機能の追加]** というラベルのポップアップ ウィンドウを使用すると、プロジェクトのセットアップに使用する 1 つ以上の機能を選択できます。</span><span class="sxs-lookup"><span data-stu-id="91f68-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="91f68-130">[ **次へ** ] を選択して、構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="91f68-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="91f68-131">[ **機能の追加]** というラベルのポップアップ ウィンドウを使用すると、選択した各機能のプロパティを選択できます。</span><span class="sxs-lookup"><span data-stu-id="91f68-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="91f68-132">[**完了] を** 選択すると **、Microsoft Teams Toolkit** ランディング ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="91f68-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="91f68-133">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="91f68-133">Configure your app</span></span>

<span data-ttu-id="91f68-134">その中核となるTeamsアプリには、次の 3 つのコンポーネントが含まれます。</span><span class="sxs-lookup"><span data-stu-id="91f68-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="91f68-135">ユーザーがアプリを操作するクライアント (web、デスクトップ、モバイル) をMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="91f68-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="91f68-136">html タブコンテンツやボットアダプティブカードなど、Teamsに表示されるコンテンツの要求に応答するサーバー。</span><span class="sxs-lookup"><span data-stu-id="91f68-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="91f68-137">Teams アプリ パッケージは、次の 3 つのファイルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="91f68-137">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="91f68-138">上のmanifest.js</span><span class="sxs-lookup"><span data-stu-id="91f68-138">The manifest.json</span></span>
      > - <span data-ttu-id="91f68-139">アプリがパブリックまたは組織のアプリ カタログに表示される[色のアイコン](../resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="91f68-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
      > - <span data-ttu-id="91f68-140">Teamsアクティビティ バーに表示する[アウトライン アイコン](../resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="91f68-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="91f68-141">アプリがインストールされると、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を判断します。</span><span class="sxs-lookup"><span data-stu-id="91f68-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="91f68-142">まだ行っていない場合は、Microsoft 365またはアカウントにサインインして開発プロセスを続行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91f68-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="91f68-143">Microsoft 365アカウントをお持ちの場合は[、Microsoft 365デベロッパー プログラム](https://developer.microsoft.com/microsoft-365/dev-program)のサブスクリプションにサインアップできます。</span><span class="sxs-lookup"><span data-stu-id="91f68-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="91f68-144">これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="91f68-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="91f68-145">Visual Studio *Enterprise* または *Professional* サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。</span><span class="sxs-lookup"><span data-stu-id="91f68-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="91f68-146">詳細については、「 [Microsoft 365開発者サブスクリプションの設定](/office/developer-program/office-365-developer-program-get-started)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="91f68-146">For more information, See [Set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="91f68-147">構成の手順</span><span class="sxs-lookup"><span data-stu-id="91f68-147">Configuration steps</span></span>

1. <span data-ttu-id="91f68-148">アプリを構成するには **、Microsoft Teams Toolkit** のランディング ページで、[**アプリ パッケージの編集**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="91f68-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="91f68-149">[ **マイ環境]** ドロップダウン メニューから [ **開発**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="91f68-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="91f68-150">**[アプリの詳細**] ページに移動して、アプリのプロパティ フィールドを編集できます。</span><span class="sxs-lookup"><span data-stu-id="91f68-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="91f68-151">[アプリの詳細] ページのフィールドを編集すると、最終的にアプリ パッケージの一部として出荷されるファイル上のmanifest.jsの内容が更新されます。</span><span class="sxs-lookup"><span data-stu-id="91f68-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="91f68-152">詳細情報</span><span class="sxs-lookup"><span data-stu-id="91f68-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="91f68-153">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="91f68-153">Package your app</span></span>

<span data-ttu-id="91f68-154">**アプリの詳細** ページを変更するか、アプリの .publish フォルダー内の **マニフェスト**、または **.env** ファイルを更新すると **、Development.zip** ファイルが自動的に生成されます。 </span><span class="sxs-lookup"><span data-stu-id="91f68-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="91f68-155">Development.zip ファイルには **、manifest.js** と [2 つのアイコン](../concepts/build-and-test/apps-package.md#app-icons)という 3 つの必須ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="91f68-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="91f68-156">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="91f68-156">Install and run your app locally</span></span>

1. <span data-ttu-id="91f68-157">次の図に示すように、[ **ソリューション構成]** ドロップダウン メニューから [ **展開** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="91f68-157">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    ![ソリューション構成メニュー](../assets/images/solution-configurations.png)

2. <span data-ttu-id="91f68-159">[IIS Express **+ Teams]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="91f68-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="91f68-160">Teamsが起動し、アプリのインストールダイアログがTeamsクライアントに表示されます。</span><span class="sxs-lookup"><span data-stu-id="91f68-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="91f68-161">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="91f68-161">Validate your app</span></span>

<span data-ttu-id="91f68-162">[ **検証]** ページでは、アプリを AppSource に提出する前にアプリ パッケージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="91f68-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="91f68-163">マニフェスト パッケージをアップロードするだけで、検証ツールは、マニフェスト関連のすべてのテスト ケースに対してアプリをチェックします。</span><span class="sxs-lookup"><span data-stu-id="91f68-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="91f68-164">失敗した各テストについて、説明にエラーの修正に役立つドキュメント リンクが記載されています。</span><span class="sxs-lookup"><span data-stu-id="91f68-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="91f68-165">自動化が困難なテストの場合、 **暫定チェックリスト** の詳細 7 最も一般的な失敗したテスト ケースの詳細と、完全なサブミッション チェックリストへのリンク。</span><span class="sxs-lookup"><span data-stu-id="91f68-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="91f68-166">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="91f68-166">Publish your app to Teams</span></span>

<span data-ttu-id="91f68-167">✔プロジェクトのホーム ページで、アプリをチームにアップロードしたり、組織のユーザー用に会社のカスタム アプリ ストアにアプリを提出したり、すべてのTeamsユーザーのアプリ ソースにアプリを送信したりできます。</span><span class="sxs-lookup"><span data-stu-id="91f68-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="91f68-168">✔ IT 管理者がこれらの提出を確認します。</span><span class="sxs-lookup"><span data-stu-id="91f68-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="91f68-169">✔ **[発行** ] ページに戻って、申請の状態を確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認できます。また、アプリの更新を送信したり、現在アクティブな提出をキャンセルしたりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="91f68-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="91f68-170">次の手順</span><span class="sxs-lookup"><span data-stu-id="91f68-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="91f68-171">公開済みアプリの保守とサポート</span><span class="sxs-lookup"><span data-stu-id="91f68-171">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
