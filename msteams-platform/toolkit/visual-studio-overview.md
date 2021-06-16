---
title: アプリとアプリのTeams ToolkitをVisual Studio
description: アプリを使用して、アプリ内で直接素晴らしいカスタム Visual Studioを構築Microsoft Teams Toolkit
keywords: teams visual studio ツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 996037f5bb1caaa2493e1eebe51039724822fef9
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949717"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="229f3-104">アプリとアプリのTeams ToolkitをVisual Studio</span><span class="sxs-lookup"><span data-stu-id="229f3-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="229f3-105">Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="229f3-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="229f3-106">Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="229f3-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="229f3-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="229f3-107">Prerequisites</span></span>

1. <span data-ttu-id="229f3-108">[開発者プレビューを有効にする](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)。</span><span class="sxs-lookup"><span data-stu-id="229f3-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="229f3-109">T および web 開発 **<span>ASP.NE</span>モジュールが** インスタンスに追加Visual Studioします。</span><span class="sxs-lookup"><span data-stu-id="229f3-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="229f3-110">ワークロードとコンポーネントのドキュメントを追加または削除することで、Visual Studioの手順[に従って確認](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)できます。</span><span class="sxs-lookup"><span data-stu-id="229f3-110">You can check by following the steps in the [modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![Visual studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="229f3-112">アプリをアプリから展開してテストする場合は、Visual Studio環境にインターネット インフォメーション サービス (IIS)) がインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="229f3-112">If you want to test your app by deploying it from Visual Studio, you must have Internet Information Services (IIS)) installed in your development environment.</span></span> <span data-ttu-id="229f3-113">Visual Studio IIS は含まれていないので、既定の構成、Windows 10、Windows 8、または 7 Windowsには含まれません。ただし、Microsoft ダウンロード センターから最新バージョン[をダウンロードできます](https://www.microsoft.com/download/details.aspx?id=48264)。</span><span class="sxs-lookup"><span data-stu-id="229f3-113">Visual Studio does not include IIS and it is not included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="229f3-115">サーバーをインストールTeams Toolkit</span><span class="sxs-lookup"><span data-stu-id="229f3-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="229f3-116">このMicrosoft Teams ToolkitはVisual Studio[マーケット](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)プレースから、またはVisual Studio内の [拡張機能] メニューから直接ダウンロードVisual Studio。 </span><span class="sxs-lookup"><span data-stu-id="229f3-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span> <span data-ttu-id="229f3-117">また、Visual Studio Marketplace から[2019 Teams ToolkitのVisual Studioダウンロードします](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit)。</span><span class="sxs-lookup"><span data-stu-id="229f3-117">From the Visual Studio Marketplace also download [Teams Toolkit for Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit).</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="229f3-118">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="229f3-118">Using the toolkit</span></span>

- [<span data-ttu-id="229f3-119">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="229f3-119">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="229f3-120">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="229f3-120">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="229f3-121">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="229f3-121">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="229f3-122">アプリをインストールして実行Teams</span><span class="sxs-lookup"><span data-stu-id="229f3-122">Install and run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="229f3-123">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="229f3-123">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="229f3-124">アプリを公開する</span><span class="sxs-lookup"><span data-stu-id="229f3-124">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="229f3-125">新しいプロジェクトをTeamsする</span><span class="sxs-lookup"><span data-stu-id="229f3-125">Set up a new Teams project</span></span>

![Teamsツールキットのインストール](../assets/images/teamstoolkiticon.png)

1. <span data-ttu-id="229f3-127">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="229f3-127">Select **Create New Project**.</span></span>

    ![新しいプロジェクトを作成する](../assets/images/createnewproject.png)

1. <span data-ttu-id="229f3-129">アプリのクイック スタート ツールを選択し **、[Microsoft Teams]** を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="229f3-129">Choose the quickstart tool for **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="229f3-130">[新しい **プロジェクトの構成]** ページで、名前 **、** 場所Project **ソリューション名** を **入力します**。</span><span class="sxs-lookup"><span data-stu-id="229f3-130">In the **Configure your new project** page, enter the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="229f3-131">[ソリューションと **プロジェクトを同じディレクトリに配置する] チェック ボックスをオン** にします。</span><span class="sxs-lookup"><span data-stu-id="229f3-131">Select the **Place solution and project in the same directory** checkbox.</span></span>
1. <span data-ttu-id="229f3-132">[機能 **の追加] ポップアップ** ウィンドウで、プロジェクトのセットアップに使用する 1 つ以上の機能を選択します。</span><span class="sxs-lookup"><span data-stu-id="229f3-132">In the **Add Capabilities** pop-up window, choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="229f3-133">[次へ **] ボタン** を選択して構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="229f3-133">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="229f3-134">[機能 **の追加] ポップアップ** ウィンドウで、選択した各機能のプロパティを選択します。</span><span class="sxs-lookup"><span data-stu-id="229f3-134">In the **Add Capabilities** pop-up window, choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="229f3-135">[**完了**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="229f3-135">Select **Finish**.</span></span> <span data-ttu-id="229f3-136">ランディング **Microsoft Teams Toolkit** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="229f3-136">The **Microsoft Teams Toolkit** landing page is shown.</span></span>

    ![Teamsツールキットのランディング ページ](../assets/images/Teamstoolkitpage.png)

## <a name="configure-your-app"></a><span data-ttu-id="229f3-138">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="229f3-138">Configure your app</span></span>

<span data-ttu-id="229f3-139">このアプリの中核となるのは、Teams 3 つのコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="229f3-139">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="229f3-140">ユーザー Microsoft Teamsアプリを操作する Web、デスクトップ、またはモバイルを含むクライアントです。</span><span class="sxs-lookup"><span data-stu-id="229f3-140">The Microsoft Teams client including web, desktop, or mobile, where users interact with your app.</span></span>
  1. <span data-ttu-id="229f3-141">HTML タブ コンテンツやボットアダプティブ カードなど、Teamsに表示されるコンテンツの要求に応答するサーバー。</span><span class="sxs-lookup"><span data-stu-id="229f3-141">A server that responds to requests for content that is displayed in Teams, for example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="229f3-142">アプリ Teamsは、次の 3 つのファイルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="229f3-142">A Teams app package consists of three files:</span></span>

      - <span data-ttu-id="229f3-143">[manifest.js]</span><span class="sxs-lookup"><span data-stu-id="229f3-143">The manifest.json</span></span>
      - <span data-ttu-id="229f3-144">パブリック [または組織](../resources/schema/manifest-schema.md#icons) のアプリ カタログに表示するアプリの色アイコン。</span><span class="sxs-lookup"><span data-stu-id="229f3-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      - <span data-ttu-id="229f3-145">アクティビティ[バーに](../resources/schema/manifest-schema.md#icons)表示するアウトライン Teamsアイコン。</span><span class="sxs-lookup"><span data-stu-id="229f3-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="229f3-146">アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="229f3-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="229f3-147">まだ実行していない場合は、開発プロセスを続行するには、Microsoft 365アカウントにサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="229f3-147">If you have not done so already, you must sign in to your Microsoft 365 account to continue with the development process.</span></span>
>
> <span data-ttu-id="229f3-148">ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションMicrosoft 365[サインアップ](https://developer.microsoft.com/microsoft-365/dev-program)できます。</span><span class="sxs-lookup"><span data-stu-id="229f3-148">If you do not have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="229f3-149">90 日間無料で、開発アクティビティに使用している限り更新されます。</span><span class="sxs-lookup"><span data-stu-id="229f3-149">It's free for 90 days and renews as long as you are using it for development activity.</span></span> <span data-ttu-id="229f3-150">Visual Studio Enterprise または Professional サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。</span><span class="sxs-lookup"><span data-stu-id="229f3-150">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="229f3-151">詳細については、「開発者向けサブスクリプション[のセットアップ」Microsoft 365参照してください](/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="229f3-151">For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="229f3-152">構成の手順</span><span class="sxs-lookup"><span data-stu-id="229f3-152">Configuration steps</span></span>

1. <span data-ttu-id="229f3-153">アプリを構成するには、ランディング **ページの**[Microsoft Teams Toolkit] で、[アプリ パッケージの編集 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="229f3-153">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="229f3-154">[自分の **環境] ドロップダウン** メニューから、[開発] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="229f3-154">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="229f3-155">[アプリ **の詳細] ページ** で、アプリのプロパティ フィールドを編集します。</span><span class="sxs-lookup"><span data-stu-id="229f3-155">In the **App details** page, edit your app's property fields.</span></span>
    
    <span data-ttu-id="229f3-156">[アプリの詳細] ページでフィールドを編集すると、アプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。</span><span class="sxs-lookup"><span data-stu-id="229f3-156">Editing the fields in the App details page updates the contents of the manifest.json file that will ship as part of the app package.</span></span> <span data-ttu-id="229f3-157">詳細については、「マニフェストのTeams Toolkit[してください](https://aka.ms/teams-toolkit-manifest)。</span><span class="sxs-lookup"><span data-stu-id="229f3-157">For more information, see [Teams Toolkit manifest](https://aka.ms/teams-toolkit-manifest).</span></span>

## <a name="package-your-app"></a><span data-ttu-id="229f3-158">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="229f3-158">Package your app</span></span>

<span data-ttu-id="229f3-159">アプリの詳細 **ページを変更** したり、マニフェストを更新したり、アプリの .publish フォルダー内の **.env** ファイルを更新すると、アプリのファイルが自動的に **Development.zipされます。** </span><span class="sxs-lookup"><span data-stu-id="229f3-159">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="229f3-160">このDevelopment.zipには、3 つの必須ファイル、manifest.js **アイコン** が [含まれます](../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="229f3-160">The Development.zip file includes three required files, the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="229f3-161">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="229f3-161">Install and run your app locally</span></span>

1. <span data-ttu-id="229f3-162">[ソリューション **構成] ドロップダウン メニュー** から、次の **図に示** すように [展開] を選択します。</span><span class="sxs-lookup"><span data-stu-id="229f3-162">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    ![[ソリューション構成] メニュー](../assets/images/solution-configurations.png)

1. <span data-ttu-id="229f3-164">[+ **IIS Express] ボタンTeams** します。</span><span class="sxs-lookup"><span data-stu-id="229f3-164">Select the **IIS Express + Teams** button.</span></span>

    <span data-ttu-id="229f3-165">[アプリのインストール] ダイアログ ボックスがクライアントのTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="229f3-165">The app installation dialog box appears in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="229f3-166">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="229f3-166">Validate your app</span></span>

<span data-ttu-id="229f3-167">[ **検証]** ページでは、アプリを AppSource に提出する前にアプリ パッケージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="229f3-167">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="229f3-168">マニフェスト パッケージをアップロードするだけで、検証ツールはアプリをマニフェスト関連のすべてのテスト ケースに対してチェックします。</span><span class="sxs-lookup"><span data-stu-id="229f3-168">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="229f3-169">失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。</span><span class="sxs-lookup"><span data-stu-id="229f3-169">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="229f3-170">自動化が難しいテストについては、最も一般的な失敗したテスト ケースの予備チェックリストの詳細 7 と、完全な提出チェックリストへのリンクを示します。</span><span class="sxs-lookup"><span data-stu-id="229f3-170">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="229f3-171">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="229f3-171">Publish your app to Teams</span></span>

* <span data-ttu-id="229f3-172">プロジェクトのホーム ページでは、アプリをチーム向けにアップロードしたり、組織内のユーザー向けに会社のカスタム App Store に提出したり、すべての Teams ユーザー向けに App Source に提出したりできます。</span><span class="sxs-lookup"><span data-stu-id="229f3-172">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

* <span data-ttu-id="229f3-173">これらの送信内容は、IT 管理者によって審査されます。</span><span class="sxs-lookup"><span data-stu-id="229f3-173">Your IT admin will review these submissions.</span></span>

* <span data-ttu-id="229f3-174">[発行] ページ **に戻り** 、申請の状態を確認し、アプリが IT 管理者によって承認または却下された場合に確認できます。また、アプリに更新プログラムを送信したり、現在アクティブな申請を取り消したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="229f3-174">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you can submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="229f3-175">次の手順</span><span class="sxs-lookup"><span data-stu-id="229f3-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="229f3-176">発行済みアプリの保守とサポート</span><span class="sxs-lookup"><span data-stu-id="229f3-176">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
