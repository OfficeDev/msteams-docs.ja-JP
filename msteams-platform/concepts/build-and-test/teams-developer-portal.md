---
title: 開発者ポータルでアプリを管理する
description: 開発者ポータルを使用してアプリを管理する方法について説明Microsoft Teams。
keywords: 開発者ポータル チームの開始
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 857d2069c4f67bf15e1d3435af55a684a918df87
ms.sourcegitcommit: d972953994e405c6afc42e4d4a76b48c6d4cfb5f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52635095"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a><span data-ttu-id="f6c17-104">開発者ポータルを使用してアプリを管理Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f6c17-104">Manage your apps with the Developer Portal for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="f6c17-105">開発者向け開発者ポータル Teamsパブリック開発者[プレビュー中です](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="f6c17-105">The Developer Portal for Teams is currently in [public developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

<span data-ttu-id="f6c17-106">開発者ポータルは、Teamsアプリを構成、配布、および管理するための主要Microsoft Teamsです。</span><span class="sxs-lookup"><span data-stu-id="f6c17-106">The Developer Portal for Teams is the primary tool for configuring, distributing, and managing your Microsoft Teams apps.</span></span> <span data-ttu-id="f6c17-107">開発者ポータルを使用すると、アプリの同僚と共同作業を行い、ランタイム環境をセットアップできます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-107">With the Developer Portal, you can collaborate with colleagues on your app, set up runtime environments, and much more.</span></span>

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="開発者ポータルのホーム ページを示すスクリーンショットTeams。":::

## <a name="register-an-app"></a><span data-ttu-id="f6c17-109">アプリを登録します</span><span class="sxs-lookup"><span data-stu-id="f6c17-109">Register an app</span></span>

<span data-ttu-id="f6c17-110">開発者ポータルには、アプリを登録するためのいくつかのTeamsがあります。</span><span class="sxs-lookup"><span data-stu-id="f6c17-110">The Developer Portal provides a couple ways to register a Teams app:</span></span>

* <span data-ttu-id="f6c17-111">ブランドの新しいアプリを登録する</span><span class="sxs-lookup"><span data-stu-id="f6c17-111">Register a brand new app</span></span>
* <span data-ttu-id="f6c17-112">既存のアプリ パッケージをインポートする</span><span class="sxs-lookup"><span data-stu-id="f6c17-112">Import an existing app package</span></span>

> [!NOTE]
> <span data-ttu-id="f6c17-113">アプリを作成する場合は、Microsoft Teams Toolkit[を](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)Visual Studio Code、開発者ポータルでそのアプリを管理できます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-113">If you create an app using the [Microsoft Teams Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), you can manage that app in the Developer Portal.</span></span>

## <a name="set-up-an-environment"></a><span data-ttu-id="f6c17-114">環境のセットアップ</span><span class="sxs-lookup"><span data-stu-id="f6c17-114">Set up an environment</span></span>

<span data-ttu-id="f6c17-115">環境とグローバル変数を構成して、アプリをローカル ランタイムから実稼働環境に移行できます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-115">You can configure environments and global variables to help transition your app from your local runtime to production.</span></span> <span data-ttu-id="f6c17-116">グローバル変数は、すべての環境で使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-116">Global variables are used across all environments.</span></span>

<span data-ttu-id="f6c17-117">**環境をセットアップするには**</span><span class="sxs-lookup"><span data-stu-id="f6c17-117">**To set up an environment**</span></span>

1. <span data-ttu-id="f6c17-118">開発者ポータルで、作業しているアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="f6c17-118">In the Developer Portal, select the app you're working on.</span></span>
2. <span data-ttu-id="f6c17-119">[環境] ページ **に移動し** 、[+ 環境 **の追加] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f6c17-119">Go to the **Environments** page and select **+ Add an environment**.</span></span>
3. <span data-ttu-id="f6c17-120">[+ **変数の追加] を** 選択して、環境の構成変数を作成します。</span><span class="sxs-lookup"><span data-stu-id="f6c17-120">Select **+ Add a variable** to create configuration variables for your environment.</span></span>

<span data-ttu-id="f6c17-121">**変数を使用するには**</span><span class="sxs-lookup"><span data-stu-id="f6c17-121">**To use variables**</span></span>

<span data-ttu-id="f6c17-122">アプリの構成を設定するには、ハードコードされた値の代わりに変数名を使用します。</span><span class="sxs-lookup"><span data-stu-id="f6c17-122">Use the variable names instead of hard-coded values to set your app configurations.</span></span>

1. <span data-ttu-id="f6c17-123">開発者 `{{` ポータルの任意のフィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="f6c17-123">Enter `{{` in any field in the Developer Portal.</span></span> <span data-ttu-id="f6c17-124">選択した環境に対して作成した変数とグローバル変数のドロップダウンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-124">A dropdown with all the variables you've created for the chosen environment along with the global variables appears.</span></span>  
1. <span data-ttu-id="f6c17-125">アプリ パッケージをダウンロードする前に (たとえば、Teams ストアに発行する準備が整った場合)、使用する環境を選択します。</span><span class="sxs-lookup"><span data-stu-id="f6c17-125">Before downloading your app package (for example, when getting ready to publish to the Teams store), select the environment you want to use.</span></span> <span data-ttu-id="f6c17-126">アプリの構成は、環境に基づいて自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-126">Your app configurations update automatically based on the environment.</span></span> 

## <a name="identify-app-owners"></a><span data-ttu-id="f6c17-127">アプリの所有者を特定する</span><span class="sxs-lookup"><span data-stu-id="f6c17-127">Identify app owners</span></span>

<span data-ttu-id="f6c17-128">各アプリには **[所有者] ページが** 含まれています。このページでは、組織の同僚とアプリ登録を共有できます。 **共同作成者の** 役割は、アプリを削除する機能を除き **、所有者** ロールと同じアクセス許可を持っています。</span><span class="sxs-lookup"><span data-stu-id="f6c17-128">Each app includes an **Owners** page, where you can share your app registration with colleagues in your org. The **Contributor** role has the same permissions as the **Owner** role except the ability to delete an app.</span></span>

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a><span data-ttu-id="f6c17-129">アプリの機能と他の重要なメタデータを構成する</span><span class="sxs-lookup"><span data-stu-id="f6c17-129">Configure your app's capabilities and other important metadata</span></span>

<span data-ttu-id="f6c17-130">アプリTeams Web アプリです。</span><span class="sxs-lookup"><span data-stu-id="f6c17-130">A Teams app is a web app.</span></span> <span data-ttu-id="f6c17-131">すべての Web アプリと同様に、ソース コードは通常、IDE またはコード エディターで開発され、クラウドのどこか (Azure など) でホストされます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-131">Like all web apps, its source code is typically developed in an IDE or code editor and hosted somewhere in the cloud (like Azure).</span></span>

<span data-ttu-id="f6c17-132">アプリをインストールしてレンダリングするには、Teams認識する一連の構成Teams必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6c17-132">To install and render your app in Teams, you must include a set of configurations that Teams recognizes.</span></span> <span data-ttu-id="f6c17-133">これは、アプリ のコンテンツを表示するために必要なすべてのメタデータを含む JSON ファイルであるアプリ マニフェストTeams作成することで行われ始めでした。</span><span class="sxs-lookup"><span data-stu-id="f6c17-133">This has traditionally been done by crafting an app manifest, a JSON file that contains all the metadata Teams needs to display your app content.</span></span> <span data-ttu-id="f6c17-134">開発者ポータルでは、このプロセスを抽象化し、より成功するための新機能とツールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f6c17-134">The Developer Portal abstracts this process and includes new features and tooling to help you be more successful.</span></span>

## <a name="test-your-app-directly-in-teams"></a><span data-ttu-id="f6c17-135">アプリをアプリで直接テストTeams</span><span class="sxs-lookup"><span data-stu-id="f6c17-135">Test your app directly in Teams</span></span>

<span data-ttu-id="f6c17-136">開発者ポータルには、アプリをテストおよびデバッグするためのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="f6c17-136">The Developer Portal provides options for testing and debugging your app:</span></span>

* <span data-ttu-id="f6c17-137">[概要 **] ページ** では、アプリの構成がストア テスト ケースに対して検証Teams確認できます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-137">On the **Overview** page, you can see a snapshot of whether your app's configurations validate against Teams store test cases.</span></span>
* <span data-ttu-id="f6c17-138">[**プレビューイン Teams]** ボタンを使用すると、デバッグ用にアプリを Teamsすぐに起動できます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-138">The **Preview in Teams** button lets you launch your app quickly in the Teams client for debugging.</span></span>

## <a name="distribute-your-app"></a><span data-ttu-id="f6c17-139">アプリを配布する</span><span class="sxs-lookup"><span data-stu-id="f6c17-139">Distribute your app</span></span>

<span data-ttu-id="f6c17-140">開発者ポータルから、[配布]ボタンを使用して、アプリ パッケージをダウンロードしたり、組織に発行したり、組織に発行したり、Teamsします。</span><span class="sxs-lookup"><span data-stu-id="f6c17-140">From the Developer Portal, use the **Distribute** button to download an app package, publish to your org, or publish to the Teams store.</span></span>

<span data-ttu-id="f6c17-141">詳細については、「アプリの[配布」をTeamsしてください](~/concepts/deploy-and-publish/apps-publish-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f6c17-141">For more information, see [distribute your Teams app](~/concepts/deploy-and-publish/apps-publish-overview.md).</span></span>

## <a name="analyze-your-apps-usage"></a><span data-ttu-id="f6c17-142">アプリの使用状況を分析する</span><span class="sxs-lookup"><span data-stu-id="f6c17-142">Analyze your app's usage</span></span>

<span data-ttu-id="f6c17-143">[概要 **] ページ** で、アプリのアクティブなユーザーの総数を確認できます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-143">On the **Overview** page, you can see the total number of active users for your app.</span></span> <span data-ttu-id="f6c17-144">これらの指標は、開発者ポータルを通じて Teamsストアまたは組織のアプリ カタログに発行され、アプリ ID にスコープを設定したアプリで使用できます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-144">These metrics are available for apps published to the Teams store or an org's app catalog through Developer Portal and scoped to the app ID.</span></span>

| <span data-ttu-id="f6c17-145">測定基準</span><span class="sxs-lookup"><span data-stu-id="f6c17-145">Metric</span></span> | <span data-ttu-id="f6c17-146">定義</span><span class="sxs-lookup"><span data-stu-id="f6c17-146">Definition</span></span> |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f6c17-147">*月次 R30*</span><span class="sxs-lookup"><span data-stu-id="f6c17-147">*Monthly R30*</span></span> | <span data-ttu-id="f6c17-148">既定の使用状況メトリック。</span><span class="sxs-lookup"><span data-stu-id="f6c17-148">The default usage metric.</span></span> <span data-ttu-id="f6c17-149">UTC の 30 日間のローリング ウィンドウ内でアプリを使用した一意のアクティブ ユーザーの数が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-149">It shows you the count of unique active users that used your app within that rolling 30-day window in UTC.</span></span> |
| <span data-ttu-id="f6c17-150">*毎日*</span><span class="sxs-lookup"><span data-stu-id="f6c17-150">*Daily*</span></span> | <span data-ttu-id="f6c17-151">UTC で特定の日にアプリを使用した一意のアクティブ ユーザーの数を示します。</span><span class="sxs-lookup"><span data-stu-id="f6c17-151">Shows you the count of unique active users that used your app in a given day in UTC.</span></span> |
| <span data-ttu-id="f6c17-152">*履歴*</span><span class="sxs-lookup"><span data-stu-id="f6c17-152">*History*</span></span> | <span data-ttu-id="f6c17-153">過去 7 日間、30 日間、および 60 日間の月次および毎日の使用状況が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-153">Monthly and daily usage is shown for the past seven, 30 days, and 60 days.</span></span> |
| <span data-ttu-id="f6c17-154">*Latency*</span><span class="sxs-lookup"><span data-stu-id="f6c17-154">*Latency*</span></span> | <span data-ttu-id="f6c17-155">24 ~ 48 時間以内に、特定の日の使用状況が反映されます。</span><span class="sxs-lookup"><span data-stu-id="f6c17-155">You should see usage reflected for a given day within 24-48 hours.</span></span> <span data-ttu-id="f6c17-156">新しいアプリの使用状況は、表示に最大で 3 ~ 5 日かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="f6c17-156">Usage for new apps can take up to 3-5 days to display.</span></span>|

## <a name="use-tools-to-create-app-features"></a><span data-ttu-id="f6c17-157">ツールを使用してアプリ機能を作成する</span><span class="sxs-lookup"><span data-stu-id="f6c17-157">Use tools to create app features</span></span>

<span data-ttu-id="f6c17-158">また、開発者ポータルには、アプリの主要な機能を構築するためのTeamsがあります。</span><span class="sxs-lookup"><span data-stu-id="f6c17-158">The Developer Portal also includes tools to help you build some key features of Teams apps.</span></span> <span data-ttu-id="f6c17-159">これらのツールの一部は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="f6c17-159">Some of these tools include:</span></span>

* <span data-ttu-id="f6c17-160">**シーン スタジオ**: 会議のカスタム一緒にモード シーンをTeamsします。</span><span class="sxs-lookup"><span data-stu-id="f6c17-160">**Scene studio**: Design custom Together mode scenes for Teams meetings.</span></span>
* <span data-ttu-id="f6c17-161">**アダプティブ カード エディター**: アプリに含めるアダプティブ カードを作成およびプレビューします。</span><span class="sxs-lookup"><span data-stu-id="f6c17-161">**Adaptive Cards editor**: Create and preview Adaptive Cards to include with your apps.</span></span>
* <span data-ttu-id="f6c17-162">**Microsoft ID プラットフォーム管理**: アプリを Azure Active Directory (Azure AD) に登録して、ユーザーがサインインして API へのアクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="f6c17-162">**Microsoft identity platform management**: Register your apps with Azure Active Directory (Azure AD) to help users sign in and provide access to APIs.</span></span>
