---
title: アプリとアプリのMicrosoft Teams ToolkitをVisual Studio
description: アプリを使用して、アプリ内で直接素晴らしいカスタム Visual Studioを構築Microsoft Teams Toolkit
keywords: teams visual studio ツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bf8250e42bdf96073d729a19e921c400f242c67a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020254"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="c818c-104">アプリとアプリのTeams ToolkitをVisual Studio</span><span class="sxs-lookup"><span data-stu-id="c818c-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="c818c-105">Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="c818c-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="c818c-106">Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="c818c-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c818c-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="c818c-107">Prerequisites</span></span>

1. [<span data-ttu-id="c818c-108">開発者プレビューを有効にする</span><span class="sxs-lookup"><span data-stu-id="c818c-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="c818c-109">T および web 開発 **<span>ASP.NE</span>モジュールが** インスタンスに追加Visual Studioします。</span><span class="sxs-lookup"><span data-stu-id="c818c-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="c818c-110">ワークロードとコンポーネントのドキュメントを追加または削除することで[、Visual Studioの手順に従って確認](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)できます。</span><span class="sxs-lookup"><span data-stu-id="c818c-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![visual studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="c818c-112">アプリを Visual Studio から展開してテストする場合は、IIS (インターネット インフォメーション サービス) を開発環境にインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c818c-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="c818c-113">Visual Studio IIS は含まれていないので、既定のバージョン 7 構成Windows 10、Windows 8、Windowsには含まれません。ただし、Microsoft ダウンロード センターから最新バージョン[をダウンロードできます](https://www.microsoft.com/download/details.aspx?id=48264)。</span><span class="sxs-lookup"><span data-stu-id="c818c-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="c818c-115">サーバーをインストールTeams Toolkit</span><span class="sxs-lookup"><span data-stu-id="c818c-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="c818c-116">このMicrosoft Teams ToolkitはVisual Studio[マーケット](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)プレースから、またはVisual Studio内の [拡張機能] メニューから直接ダウンロードVisual Studio。 </span><span class="sxs-lookup"><span data-stu-id="c818c-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="c818c-117">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="c818c-117">Using the toolkit</span></span>

- [<span data-ttu-id="c818c-118">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="c818c-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="c818c-119">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="c818c-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="c818c-120">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="c818c-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="c818c-121">アプリをアプリで実行Teams</span><span class="sxs-lookup"><span data-stu-id="c818c-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="c818c-122">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="c818c-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="c818c-123">アプリを公開する</span><span class="sxs-lookup"><span data-stu-id="c818c-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="c818c-124">新しいプロジェクトをTeamsする</span><span class="sxs-lookup"><span data-stu-id="c818c-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="c818c-125">[新 **しいプロジェクトを作成する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="c818c-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="c818c-126">[アプリ **Microsoft Teams選択し、[** 次へ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="c818c-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="c818c-127">[新しいプロジェクトの **構成]** 画面が表示され、新しいプロジェクト名、場所 **Project** ソリューション名を **選択できます**。</span><span class="sxs-lookup"><span data-stu-id="c818c-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="c818c-128">[ソリューションとプロジェクトを **同じディレクトリに配置する] というラベルのボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="c818c-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="c818c-129">[機能の追加] というラベル **の** 付いたポップアップ ウィンドウを使用すると、プロジェクトのセットアップに 1 つ以上の機能を選択できます。</span><span class="sxs-lookup"><span data-stu-id="c818c-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="c818c-130">[次へ **] ボタン** を選択して構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="c818c-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="c818c-131">[機能の追加] というラベル **の** 付いたポップアップ ウィンドウを使用すると、選択した各機能のプロパティを選択できます。</span><span class="sxs-lookup"><span data-stu-id="c818c-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="c818c-132">[**完了]** を選択すると、ランディング **ページ** Microsoft Teams Toolkitされます。</span><span class="sxs-lookup"><span data-stu-id="c818c-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="c818c-133">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="c818c-133">Configure your app</span></span>

<span data-ttu-id="c818c-134">このアプリの中核となるのは、Teams 3 つのコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="c818c-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="c818c-135">ユーザー Microsoft Teamsアプリを操作するクライアント (Web、デスクトップ、モバイル) を指定します。</span><span class="sxs-lookup"><span data-stu-id="c818c-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="c818c-136">HTML タブ コンテンツやボットアダプティブ カードなど、Teamsに表示されるコンテンツの要求に応答するサーバー。</span><span class="sxs-lookup"><span data-stu-id="c818c-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="c818c-137">次Teams [3 つのファイルで](/concepts/build-and-test/apps-package.md)構成されるアプリ パッケージです。</span><span class="sxs-lookup"><span data-stu-id="c818c-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="c818c-138">[manifest.js]</span><span class="sxs-lookup"><span data-stu-id="c818c-138">The manifest.json</span></span>
  > - <span data-ttu-id="c818c-139">パブリック [または組織の](../resources/schema/manifest-schema.md#icons) アプリ カタログに表示するアプリの色アイコン</span><span class="sxs-lookup"><span data-stu-id="c818c-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="c818c-140">アクティビティ[バーに](../resources/schema/manifest-schema.md#icons)表示するアウトライン Teamsアイコン。</span><span class="sxs-lookup"><span data-stu-id="c818c-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="c818c-141">アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="c818c-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="c818c-142">まだ実行していない場合は、開発プロセスを続行するには、Microsoft 365またはアカウントにサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c818c-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="c818c-143">ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションMicrosoft 365[サインアップ](https://developer.microsoft.com/microsoft-365/dev-program)できます。</span><span class="sxs-lookup"><span data-stu-id="c818c-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="c818c-144">これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="c818c-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="c818c-145">Visual Studio *Enterprise* または *Professional* サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。</span><span class="sxs-lookup"><span data-stu-id="c818c-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="c818c-146">「*Microsoft 365 開発者サブスクリプションを設定する*」[を参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="c818c-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="c818c-147">構成の手順</span><span class="sxs-lookup"><span data-stu-id="c818c-147">Configuration steps</span></span>

1. <span data-ttu-id="c818c-148">アプリを構成するには、ランディング **ページの**[Microsoft Teams Toolkit] で、[アプリ パッケージの編集 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="c818c-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="c818c-149">[自分の **環境] ドロップダウン** メニューから、[開発] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="c818c-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="c818c-150">[アプリの詳細] **ページに移動** し、アプリのプロパティ フィールドを編集できます。</span><span class="sxs-lookup"><span data-stu-id="c818c-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="c818c-151">[アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。</span><span class="sxs-lookup"><span data-stu-id="c818c-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="c818c-152">詳細情報</span><span class="sxs-lookup"><span data-stu-id="c818c-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="c818c-153">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="c818c-153">Package your app</span></span>

<span data-ttu-id="c818c-154">アプリの詳細 **ページを変更** したり、マニフェストを更新したり、アプリの .publish フォルダー内の **.env** ファイルを更新すると、アプリのファイルが自動的に **Development.zipされます。** </span><span class="sxs-lookup"><span data-stu-id="c818c-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="c818c-155">このDevelopment.zipには、3 つの必須ファイル (manifest.js **と 2** つのアイコン) [が含まれています](../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="c818c-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="c818c-156">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="c818c-156">Install and run your app locally</span></span>

1. <span data-ttu-id="c818c-157">[ソリューション構成 **] ドロップダウン メニューの** [展開] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="c818c-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![[ソリューション構成] メニュー](../assets/images/solution-configurations.png)

2. <span data-ttu-id="c818c-159">[+ **IIS Express] ボタンTeams** します。</span><span class="sxs-lookup"><span data-stu-id="c818c-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="c818c-160">Teams起動し、アプリのインストールダイアログがクライアントに表示Teamsします。</span><span class="sxs-lookup"><span data-stu-id="c818c-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="c818c-161">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="c818c-161">Validate your app</span></span>

<span data-ttu-id="c818c-162">[ **検証]** ページでは、アプリを AppSource に提出する前にアプリ パッケージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="c818c-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="c818c-163">マニフェスト パッケージをアップロードするだけで、検証ツールはアプリをマニフェスト関連のすべてのテスト ケースに対してチェックします。</span><span class="sxs-lookup"><span data-stu-id="c818c-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="c818c-164">失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。</span><span class="sxs-lookup"><span data-stu-id="c818c-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="c818c-165">自動化が難しいテストについては、最も一般的な失敗したテスト ケースの予備チェックリストの詳細 7 と、完全な提出チェックリストへのリンクを示します。</span><span class="sxs-lookup"><span data-stu-id="c818c-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="c818c-166">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="c818c-166">Publish your app to Teams</span></span>

<span data-ttu-id="c818c-167">✔ プロジェクトのホーム ページでは、チームにアプリをアップロードしたり、組織内のユーザー用に会社のカスタム アプリ ストアにアプリを提出したり、すべての Teams ユーザーのアプリ ソースにアプリを提出することができます。</span><span class="sxs-lookup"><span data-stu-id="c818c-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="c818c-168">✔ IT 管理者がこれらの申請を確認します。</span><span class="sxs-lookup"><span data-stu-id="c818c-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="c818c-169">✔ [発行] ページに戻り、申請の状態を確認し、アプリが IT 管理者によって承認または却下された場合に確認できます。また、アプリに更新プログラムを送信したり、現在アクティブな申請を取り消したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="c818c-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c818c-170">次の手順: 発行済みアプリの保守とサポート</span><span class="sxs-lookup"><span data-stu-id="c818c-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
