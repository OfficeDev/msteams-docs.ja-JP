---
title: Microsoft Teams Toolkit と Visual Studio を使用してアプリをビルドする
description: Microsoft Teams ツールキットを使用して、Visual Studio 内で魅力的なカスタムアプリを直接作成する
keywords: teams visual studio toolkit
ms.date: 06/30/2020
ms.openlocfilehash: e5715cf23cfd221b65afe0e6258ce06ff98770aa
ms.sourcegitcommit: 694babb79d379360a20cf928a9d2b88dd6d3bdd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "45051721"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="efd49-104">Microsoft Teams Toolkit と Visual Studio を使用してアプリをビルドする</span><span class="sxs-lookup"><span data-stu-id="efd49-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="efd49-105">Microsoft Teams Toolkit を使用すると、カスタム Teams アプリを Visual Studio 環境内で直接作成することができます。</span><span class="sxs-lookup"><span data-stu-id="efd49-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio environment.</span></span> <span data-ttu-id="efd49-106">このツールキットは、このプロセスを順を追って説明しており、Teams アプリを構築、デバッグ、および起動するために必要なすべての情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="efd49-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="efd49-107">Teams ツールキットをインストールする</span><span class="sxs-lookup"><span data-stu-id="efd49-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="efd49-108">Microsoft Teams Toolkit for Visual Studio は、visual [Studio Marketplace](https://aka.ms/teams-toolkit)からダウンロードするか、visual studio 内の拡張機能として直接ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="efd49-108">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="efd49-109">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="efd49-109">Using the toolkit</span></span>

- [<span data-ttu-id="efd49-110">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="efd49-110">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="efd49-111">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="efd49-111">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="efd49-112">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="efd49-112">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="efd49-113">Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="efd49-113">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="efd49-114">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="efd49-114">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="efd49-115">アプリを発行する</span><span class="sxs-lookup"><span data-stu-id="efd49-115">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="efd49-116">新しい Teams プロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="efd49-116">Set up a new Teams project</span></span>

1. <span data-ttu-id="efd49-117">新しいプロジェクトを作成し、Microsoft Terams Toolkit テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="efd49-117">Create a new project and select the Microsoft Terams Toolkit template.</span></span>
1. <span data-ttu-id="efd49-118">[**機能の追加**] 画面が表示され、新しいアプリのプロパティを構成します。</span><span class="sxs-lookup"><span data-stu-id="efd49-118">You will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="efd49-119">[**完了**] ボタンを選択して、構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="efd49-119">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="efd49-120">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="efd49-120">Configure your app</span></span>

<span data-ttu-id="efd49-121">主に、Teams アプリは3つのコンポーネントをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="efd49-121">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="efd49-122">ユーザーがアプリを操作する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="efd49-122">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="efd49-123">Teams に表示されるコンテンツの要求に応答するサーバー。たとえば、HTML タブのコンテンツや bot のアダプティブカード。</span><span class="sxs-lookup"><span data-stu-id="efd49-123">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="efd49-124">3つのファイルで構成される Teams[アプリパッケージ](/concepts/build-and-test/apps-package.md):</span><span class="sxs-lookup"><span data-stu-id="efd49-124">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="efd49-125">manifest.js</span><span class="sxs-lookup"><span data-stu-id="efd49-125">The manifest.json</span></span> 
  > - <span data-ttu-id="efd49-126">パブリックまたは組織のアプリカタログに表示するための、アプリの[カラーアイコン](../resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="efd49-126">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="efd49-127">Teams アクティビティバーに表示するための[アウトラインアイコン](../resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="efd49-127">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="efd49-128">アプリがインストールされると、Teams クライアントはマニフェストファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="efd49-128">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="efd49-129">アプリを構成するには、 **Microsoft Teams ツールキット**拡張ウィンドウに移動します。</span><span class="sxs-lookup"><span data-stu-id="efd49-129">To configure your app, navigate to the **Microsoft Teams Toolkit** extension window.</span></span>
1. <span data-ttu-id="efd49-130">[**アプリパッケージの編集**] を選択して、[**アプリの詳細**] ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="efd49-130">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="efd49-131">[アプリの詳細] ページのフィールドを編集すると、最終的にアプリパッケージの一部として配布されるファイルの manifest.jsの内容が更新されます。</span><span class="sxs-lookup"><span data-stu-id="efd49-131">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="efd49-132">詳細情報</span><span class="sxs-lookup"><span data-stu-id="efd49-132">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="efd49-133">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="efd49-133">Package your app</span></span>

<span data-ttu-id="efd49-134">**アプリの詳細**ページを変更するか、**マニフェスト**を更新するか、またはアプリの**publish**フォルダー内の**env**ファイルを変更すると、 **Development.zip**ファイルが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="efd49-134">Modifying your the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="efd49-135">同じフォルダーに[2 つのアイコン](../concepts/build-and-test/apps-package.md#icons)を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="efd49-135">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="efd49-136">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="efd49-136">Install and run your app locally</span></span>

<span data-ttu-id="efd49-137">[*ソリューションの構成*] ドロップダウンメニューで、[*展開*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="efd49-137">From the *Solutions Configurations* dropdown menu, select *Deploy*.</span></span> <span data-ttu-id="efd49-138">[ *ISS Express + Teams* ] ボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="efd49-138">Press the *ISS Express + Teams* button.</span></span> <span data-ttu-id="efd49-139">Teams が起動し、アプリのインストールダイアログが Teams クライアントに表示されます。</span><span class="sxs-lookup"><span data-stu-id="efd49-139">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="efd49-140">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="efd49-140">Validate your app</span></span>

<span data-ttu-id="efd49-141">[**検証**] ページでは、アプリを appsource に提出する前にアプリパッケージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="efd49-141">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="efd49-142">マニフェストパッケージをアップロードすると、検証ツールによって、マニフェスト関連のすべてのテストケースに対してアプリがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="efd49-142">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="efd49-143">失敗した各テストの説明には、エラーを解決するためのドキュメントリンクが記載されています。</span><span class="sxs-lookup"><span data-stu-id="efd49-143">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="efd49-144">自動化が困難なテストの場合、最も一般的な失敗したテストケースの7つの**事前チェックリスト**と、完全な提出チェックリストへのリンクがあります。</span><span class="sxs-lookup"><span data-stu-id="efd49-144">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="efd49-145">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="efd49-145">Publish your app to Teams</span></span>

<span data-ttu-id="efd49-146">プロジェクトのホームページでは、アプリをチームにアップロードしたり、アプリを組織内のユーザーに対して会社のカスタムアプリストアに提出したり、アプリをアプリソースに提出してすべての Teams ユーザーに提供したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="efd49-146">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="efd49-147">IT 管理者は、これらの送信を確認します。</span><span class="sxs-lookup"><span data-stu-id="efd49-147">Your IT admin will review these submissions.</span></span> <span data-ttu-id="efd49-148">[*発行*] ページに戻り、送信の状態を確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認することができます。これは、アプリに更新を送信するか、現在アクティブな提出を取り消すこともできます。</span><span class="sxs-lookup"><span data-stu-id="efd49-148">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="efd49-149">次のステップ: 公開アプリの管理とサポート</span><span class="sxs-lookup"><span data-stu-id="efd49-149">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
