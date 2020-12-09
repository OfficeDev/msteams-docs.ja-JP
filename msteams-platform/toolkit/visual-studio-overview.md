---
title: Microsoft Teams Toolkit と Visual Studio を使用してアプリをビルドする
description: Microsoft Teams ツールキットを使用して、Visual Studio 内で魅力的なカスタムアプリを直接作成する
keywords: teams visual studio toolkit
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: a1221945659b2dd0f45bdd3a966d9b029ddcde09
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604488"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="6f209-104">Teams Toolkit と Visual Studio を使用してアプリをビルドする</span><span class="sxs-lookup"><span data-stu-id="6f209-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="6f209-105">Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="6f209-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="6f209-106">Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="6f209-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f209-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="6f209-107">Prerequisites</span></span>

1. [<span data-ttu-id="6f209-108">開発者プレビューを有効にする</span><span class="sxs-lookup"><span data-stu-id="6f209-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="6f209-109">**<span>ASP.NE</span>T および web 開発モジュール** が Visual Studio インスタンスに追加されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6f209-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="6f209-110">「Modify Visual Studio」の手順に従って確認するには、「 [ワークロードとコンポーネントのドキュメントを追加または削除](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6f209-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![visual studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="6f209-112">Visual Studio からアプリケーションを展開してテストする場合は、IIS (インターネットインフォメーションサービス) を開発環境にインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f209-112">If you would like test your app by deploy it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="6f209-113">Visual Studio には IIS は含まれていません。これは、既定の Windows 10、Windows 8、または Windows 7 の構成には含まれていません。ただし、最新バージョンは、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=48264)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="6f209-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS ダウンロードページビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="6f209-115">Teams ツールキットをインストールする</span><span class="sxs-lookup"><span data-stu-id="6f209-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="6f209-116">Microsoft Teams Toolkit for Visual Studio は、visual [Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) からダウンロードするか、visual studio の [ **拡張機能** ] メニューから直接ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="6f209-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="6f209-117">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="6f209-117">Using the toolkit</span></span>

- [<span data-ttu-id="6f209-118">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="6f209-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="6f209-119">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="6f209-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="6f209-120">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="6f209-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="6f209-121">Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="6f209-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="6f209-122">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="6f209-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="6f209-123">アプリを発行する</span><span class="sxs-lookup"><span data-stu-id="6f209-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="6f209-124">新しい Teams プロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="6f209-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="6f209-125">[ **新しいプロジェクトを作成する**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6f209-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="6f209-126">[ **Microsoft Teams アプリ** ] を選択し、[ **次へ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6f209-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="6f209-127">[ **新しいプロジェクトの構成** ] 画面が表示されるので、 **プロジェクトの名前**、 **場所**、および **ソリューションの名前** を選択できます。</span><span class="sxs-lookup"><span data-stu-id="6f209-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="6f209-128">[ **ソリューションとプロジェクトを同じディレクトリに配置** する] というボックスをチェックします。</span><span class="sxs-lookup"><span data-stu-id="6f209-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="6f209-129">[ **機能の追加** ] という名前のポップアップウィンドウでは、プロジェクトのセットアップに対して1つ以上の機能を選択できます。</span><span class="sxs-lookup"><span data-stu-id="6f209-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="6f209-130">[ **次へ** ] ボタンを選択して、構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="6f209-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="6f209-131">[ **機能の追加** ] という名前のポップアップウィンドウでは、選択した各機能のプロパティを選択できます。</span><span class="sxs-lookup"><span data-stu-id="6f209-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="6f209-132">[ **完了** ] を選択すると、 **Microsoft Teams Toolkit** のランディングページに着陸できます。</span><span class="sxs-lookup"><span data-stu-id="6f209-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="6f209-133">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="6f209-133">Configure your app</span></span>

<span data-ttu-id="6f209-134">主に、Teams アプリは3つのコンポーネントをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="6f209-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="6f209-135">ユーザーがアプリを操作する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="6f209-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="6f209-136">Teams に表示されるコンテンツの要求に応答するサーバー。たとえば、HTML タブのコンテンツや bot のアダプティブカード。</span><span class="sxs-lookup"><span data-stu-id="6f209-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="6f209-137">3つのファイルで構成される Teams [アプリパッケージ](/concepts/build-and-test/apps-package.md) :</span><span class="sxs-lookup"><span data-stu-id="6f209-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="6f209-138">manifest.js</span><span class="sxs-lookup"><span data-stu-id="6f209-138">The manifest.json</span></span>
  > - <span data-ttu-id="6f209-139">パブリックまたは組織のアプリカタログに表示するための、アプリの[カラーアイコン](../resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="6f209-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="6f209-140">Teams アクティビティバーに表示するための [アウトラインアイコン](../resources/schema/manifest-schema.md#icons) 。</span><span class="sxs-lookup"><span data-stu-id="6f209-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="6f209-141">アプリがインストールされると、Teams クライアントはマニフェストファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="6f209-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="6f209-142">まだ行っていない場合は、Microsoft 365 またはアカウントにサインインして、開発プロセスを続行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f209-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="6f209-143">Microsoft 365 アカウントを持っていない場合は、 [microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) サブスクリプションにサインアップできます。</span><span class="sxs-lookup"><span data-stu-id="6f209-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="6f209-144">これは90日間 *無料* で、開発アクティビティに使用している間は継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="6f209-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="6f209-145">Visual Studio *Enterprise* または *Professional* サブスクリプションを所有している場合は、どちらのプログラムにも、visual studio サブスクリプションの有効期間中にアクティブな Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="6f209-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="6f209-146">*「* [Microsoft 365 developer サブスクリプションをセットアップする」を](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)参照してください。</span><span class="sxs-lookup"><span data-stu-id="6f209-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="6f209-147">構成の手順</span><span class="sxs-lookup"><span data-stu-id="6f209-147">Configuration steps</span></span>

1. <span data-ttu-id="6f209-148">アプリを構成するには、 **Microsoft Teams ツールキット** のランディングページで、[ **アプリパッケージの編集** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6f209-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="6f209-149">**[マイ環境**] ドロップダウンメニューから、[**開発**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6f209-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="6f209-150">アプリの **詳細** ページには、アプリのプロパティフィールドを編集することができます。</span><span class="sxs-lookup"><span data-stu-id="6f209-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="6f209-151">[アプリの詳細] ページのフィールドを編集すると、最終的にアプリパッケージの一部として配布されるファイルの manifest.jsの内容が更新されます。</span><span class="sxs-lookup"><span data-stu-id="6f209-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="6f209-152">詳細情報</span><span class="sxs-lookup"><span data-stu-id="6f209-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="6f209-153">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="6f209-153">Package your app</span></span>

<span data-ttu-id="6f209-154">アプリの **詳細** ページを変更するか、**マニフェスト**、またはアプリの **publish** フォルダー内の **env** ファイルを更新すると、 **Development.zip** ファイルが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="6f209-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="6f209-155">Development.zip ファイルには、3つの必須ファイル ( **manifest.js** と [2 つのアイコン](../concepts/build-and-test/apps-package.md#app-icons)) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6f209-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="6f209-156">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="6f209-156">Install and run your app locally</span></span>

1. <span data-ttu-id="6f209-157">[ **ソリューションの構成** ] ドロップダウンメニューで、[ **展開**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6f209-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![[ソリューションの構成] メニュー](../assets/images/solution-configurations.png)

2. <span data-ttu-id="6f209-159">[ **ISS Express + Teams** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="6f209-159">Select the **ISS Express + Teams** button.</span></span>

1. <span data-ttu-id="6f209-160">Teams が起動し、アプリのインストールダイアログが Teams クライアントに表示されます。</span><span class="sxs-lookup"><span data-stu-id="6f209-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="6f209-161">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="6f209-161">Validate your app</span></span>

<span data-ttu-id="6f209-162">[ **検証** ] ページでは、アプリを appsource に提出する前にアプリパッケージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="6f209-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="6f209-163">マニフェストパッケージをアップロードすると、検証ツールによって、マニフェスト関連のすべてのテストケースに対してアプリがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="6f209-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="6f209-164">失敗した各テストの説明には、エラーを解決するためのドキュメントリンクが記載されています。</span><span class="sxs-lookup"><span data-stu-id="6f209-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="6f209-165">自動化が困難なテストの場合、最も一般的な失敗したテストケースの7つの **事前チェックリスト** と、完全な提出チェックリストへのリンクがあります。</span><span class="sxs-lookup"><span data-stu-id="6f209-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="6f209-166">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="6f209-166">Publish your app to Teams</span></span>

<span data-ttu-id="6f209-167">✔プロジェクトのホームページでは、アプリをチームにアップロードしたり、アプリを組織内のユーザーのために会社のカスタムアプリストアに提出したり、アプリをアプリソースに提出してすべての Teams ユーザーに提供したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="6f209-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="6f209-168">✔ IT 管理者は、これらの送信を確認します。</span><span class="sxs-lookup"><span data-stu-id="6f209-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="6f209-169">✔ **発行** ページに戻り、送信の状態を確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認できます。これは、アプリに更新を送信するか、現在アクティブな提出を取り消すこともできます。</span><span class="sxs-lookup"><span data-stu-id="6f209-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6f209-170">次のステップ: 公開アプリの管理とサポート</span><span class="sxs-lookup"><span data-stu-id="6f209-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
