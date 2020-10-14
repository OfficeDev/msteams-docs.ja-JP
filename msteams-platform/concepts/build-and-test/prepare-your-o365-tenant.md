---
title: Microsoft 365 テナントの準備
description: Microsoft 365 で Teams の使用を開始する方法
keywords: Microsoft 365 テナントチームのアップロードを構成する
ms.openlocfilehash: 67a0342a7e8605097eed53dd1b0bdf273d537c0e
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452766"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="3c3bb-104">Microsoft 365 テナントの準備</span><span class="sxs-lookup"><span data-stu-id="3c3bb-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="3c3bb-105">Microsoft 365 サブスクライバーの場合は、次のいずれかの [プラン](https://products.office.com/business/compare-more-office-365-for-business-plans)を使用して microsoft Teams 用アプリを開発できます。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-105">If you are a Microsoft 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="3c3bb-106">Basic</span><span class="sxs-lookup"><span data-stu-id="3c3bb-106">Basic</span></span>
* <span data-ttu-id="3c3bb-107">Standard</span><span class="sxs-lookup"><span data-stu-id="3c3bb-107">Standard</span></span>
* <span data-ttu-id="3c3bb-108">Enterprise E1、E3、E5</span><span class="sxs-lookup"><span data-stu-id="3c3bb-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="3c3bb-109">Developer</span><span class="sxs-lookup"><span data-stu-id="3c3bb-109">Developer</span></span>
* <span data-ttu-id="3c3bb-110">教育、教育プラス、教育の E5</span><span class="sxs-lookup"><span data-stu-id="3c3bb-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="3c3bb-111">また、 [退職](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前に、E4 をサブスクライブしたお客様も、Microsoft Teams を利用することができます。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="3c3bb-112">開発環境のみが必要ですか。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-112">Just need a development environment?</span></span>

<span data-ttu-id="3c3bb-113">現在 Microsoft 365 アカウントを持っていない場合は、 [microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) サブスクリプションにサインアップできます。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-113">If you don't currently have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="3c3bb-114">これは90日間 *無料* で、開発アクティビティに使用している間は継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="3c3bb-115">Visual Studio *Enterprise* または *Professional* サブスクリプションを所有している場合は、どちらのプログラムにも、visual studio サブスクリプションの有効期間中にアクティブな Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="3c3bb-116">*「* [Microsoft 365 developer サブスクリプションをセットアップする」を](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)参照してください。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="3c3bb-117">組織に対して Microsoft Teams を有効にする</span><span class="sxs-lookup"><span data-stu-id="3c3bb-117">Enable Microsoft Teams for your organization</span></span> 

<span data-ttu-id="3c3bb-118">Microsoft Teams が組織に対して有効になっていない場合は、最初にその作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="3c3bb-119">[組織で Teams を有効](/microsoftteams/enable-features-office-365)にするための詳細なガイダンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-119">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="3c3bb-120">カスタム Teams アプリを有効にし、カスタムアプリのアップロードをオンにする</span><span class="sxs-lookup"><span data-stu-id="3c3bb-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="3c3bb-121">開発者テナントのカスタムアプリのサイドロードを次のようにオンにします。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="3c3bb-122">管理者の資格情報を使用して [Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) にログインします。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="3c3bb-123">[**すべてのチームを表示**] を選択し  -->  **Teams**ます。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-123">Select **Show All** --> **Teams**.</span></span> 

![管理センターメニューの画像](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> <span data-ttu-id="3c3bb-125">"Teams" オプションが表示されるまでに最大24時間かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-125">It can take up to 24 hours for the "Teams" option to appear.</span></span> <span data-ttu-id="3c3bb-126">中間では、 [カスタムアプリを Teams 環境にアップロード](/microsoftteams/upload-custom-apps#validate) して、テストと検証を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-126">During interim, you can [Upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation.</span></span>

3. <span data-ttu-id="3c3bb-127">**Teams apps**  -->  **セットアップポリシー**  -->  **グローバル (組織全体の既定)** に移動する</span><span class="sxs-lookup"><span data-stu-id="3c3bb-127">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![サイドロード表示をオンにする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="3c3bb-129">[ **カスタムアプリのアップロード** を **オン** の位置に切り替える。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-129">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="3c3bb-130">するだけです。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-130">That's it!</span></span> <span data-ttu-id="3c3bb-131">テストテナントは、カスタムアプリのサイドロードを許可するようになります。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-131">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="3c3bb-132">サイドローディングが有効になるまで最大24時間かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-132">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="3c3bb-133">中間時に、**の \<your tenant> upload**を使用してアプリをテストできます。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-133">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![updload app ビュー](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="3c3bb-135">これらの設定がどのように影響するかの詳細については、「 [Microsoft teams のカスタムアプリポリシーと設定を管理](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)する」および「 [microsoft teams でアプリのセットアップポリシーを管理](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)する *」を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="3c3bb-135">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
