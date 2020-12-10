---
title: Microsoft 365 テナントを準備する
description: Microsoft 365 の Teams の概要
keywords: Microsoft 365 テナントTeams のアップロードの構成
ms.openlocfilehash: 67a0342a7e8605097eed53dd1b0bdf273d537c0e
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452766"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="358eb-104">Microsoft 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="358eb-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="358eb-105">Microsoft 365 のサブスクライバーである場合は、 次のいずれかの[プラン](https://products.office.com/business/compare-more-office-365-for-business-plans) を使用して、Microsoft Teams のアプリを開発できます。</span><span class="sxs-lookup"><span data-stu-id="358eb-105">If you are a Microsoft 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="358eb-106">基本</span><span class="sxs-lookup"><span data-stu-id="358eb-106">Basic</span></span>
* <span data-ttu-id="358eb-107">標準</span><span class="sxs-lookup"><span data-stu-id="358eb-107">Standard</span></span>
* <span data-ttu-id="358eb-108">Enterprise E1、E3、E5</span><span class="sxs-lookup"><span data-stu-id="358eb-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="358eb-109">開発者</span><span class="sxs-lookup"><span data-stu-id="358eb-109">Developer</span></span>
* <span data-ttu-id="358eb-110">学歴, Education Plus, and Education E5</span><span class="sxs-lookup"><span data-stu-id="358eb-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="358eb-111">またMicrosoft Teamsは、 [廃止](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前に E4 以前を購読していた客様も利用できます。</span><span class="sxs-lookup"><span data-stu-id="358eb-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="358eb-112">開発環境が必要ですか?</span><span class="sxs-lookup"><span data-stu-id="358eb-112">Just need a development environment?</span></span>

<span data-ttu-id="358eb-113">現在 Microsoft 365 アカウントを使用していない場合は、 [Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program) サブスクリプションにサイン アップできます。</span><span class="sxs-lookup"><span data-stu-id="358eb-113">If you don't currently have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="358eb-114">これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="358eb-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="358eb-115">Visual Studio *Enterprise* または *Professional* サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。</span><span class="sxs-lookup"><span data-stu-id="358eb-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="358eb-116">「*Microsoft 365 開発者サブスクリプションを設定する*」[を参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="358eb-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="358eb-117">組織用に Microsoft Teams を有効にする</span><span class="sxs-lookup"><span data-stu-id="358eb-117">Enable Microsoft Teams for your organization</span></span> 

<span data-ttu-id="358eb-118">組織に対して Microsoft Teams が有効になっていない場合は、最初に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="358eb-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="358eb-119">詳しい説明は、「[組織での Teams を有効にする](/microsoftteams/enable-features-office-365)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="358eb-119">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="358eb-120">カスタム Teams アプリを有効にして、カスタム アプリのアップロードを有効にする</span><span class="sxs-lookup"><span data-stu-id="358eb-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="358eb-121">開発者テナントのカスタムアプリのサイドローディングを次のようにオンにします。</span><span class="sxs-lookup"><span data-stu-id="358eb-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="358eb-122">管理者の資格情報を使用して[ Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にサイン インします。</span><span class="sxs-lookup"><span data-stu-id="358eb-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="358eb-123">[**すべての** --> **Teams の表示**]を選択します。</span><span class="sxs-lookup"><span data-stu-id="358eb-123">Select **Show All** --> **Teams**.</span></span> 

![管理センター メニューの画像](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> <span data-ttu-id="358eb-125">"Teams" オプションが表示されるまで、最大で24時間かかります。</span><span class="sxs-lookup"><span data-stu-id="358eb-125">It can take up to 24 hours for the "Teams" option to appear.</span></span> <span data-ttu-id="358eb-126">その間、テストおよび検証用に[カスタムアプリをTeams 環境にアップロード](/microsoftteams/upload-custom-apps#validate) することができます。</span><span class="sxs-lookup"><span data-stu-id="358eb-126">During interim, you can [Upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation.</span></span>

3. <span data-ttu-id="358eb-127">**Teams アプリ** --> **セット アップ ポリシー** --> **グローバル (組織全体の既定)** に移動する</span><span class="sxs-lookup"><span data-stu-id="358eb-127">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![sideload ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="358eb-129">**カスタム アプリのアップロード** を切り替え **オン** の位置にします。</span><span class="sxs-lookup"><span data-stu-id="358eb-129">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="358eb-130">手順は以上です。</span><span class="sxs-lookup"><span data-stu-id="358eb-130">That's it!</span></span> <span data-ttu-id="358eb-131">テスト テナントで、カスタムアプリのサイドローディングができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="358eb-131">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="358eb-132">サイドローディングが有効になるまでに 24 時間かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="358eb-132">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="358eb-133">その間、[**アップロード\<your tenant>**] を使用して、アプリをテストできます。</span><span class="sxs-lookup"><span data-stu-id="358eb-133">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![updload アプリ ビュー](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="358eb-135">これらの設定がどのように機能するかの詳細については、「[Microsoft Teams のカスタム アプリ ポリシーと設定の管理](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)」 および「[Microsoft Teams のアプリ セットアップ ポリシーの管理](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)」を *参照してください*。</span><span class="sxs-lookup"><span data-stu-id="358eb-135">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
