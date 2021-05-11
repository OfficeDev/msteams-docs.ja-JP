---
title: Microsoft 365 テナントを準備する
description: Microsoft 365 の Teams の概要
ms.topic: how-to
localization_priority: Normal
keywords: Microsoft 365 テナントTeams のアップロードの構成
ms.openlocfilehash: 45d6dfb57fd2faa5bb303aac1dff86be142d0dc2
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019945"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="dea51-104">Microsoft 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="dea51-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="dea51-105">Microsoft 365購読者は、次のいずれかの計画Microsoft Teamsアプリを開発できます。</span><span class="sxs-lookup"><span data-stu-id="dea51-105">Microsoft 365 subscribers can develop apps for Microsoft Teams with one of the following plans:</span></span>

* <span data-ttu-id="dea51-106">基本</span><span class="sxs-lookup"><span data-stu-id="dea51-106">Basic</span></span>
* <span data-ttu-id="dea51-107">標準</span><span class="sxs-lookup"><span data-stu-id="dea51-107">Standard</span></span>
* <span data-ttu-id="dea51-108">Enterprise E1、E3、E5</span><span class="sxs-lookup"><span data-stu-id="dea51-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="dea51-109">開発者</span><span class="sxs-lookup"><span data-stu-id="dea51-109">Developer</span></span>
* <span data-ttu-id="dea51-110">学歴, Education Plus, and Education E5</span><span class="sxs-lookup"><span data-stu-id="dea51-110">Education, Education Plus, and Education E5</span></span>

> [!NOTE]
> * <span data-ttu-id="dea51-111">サブスクリプションの詳細については、「Microsoft 365プラン」を[参照してください](https://products.office.com/business/compare-more-office-365-for-business-plans)。</span><span class="sxs-lookup"><span data-stu-id="dea51-111">For more information on Microsoft 365 subscriptions, see [plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>
> * <span data-ttu-id="dea51-112">Teamsは、退職前に E4 を購読しているお客様にも利用[できます](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)。</span><span class="sxs-lookup"><span data-stu-id="dea51-112">Teams is also available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="create-your-development-environment"></a><span data-ttu-id="dea51-113">開発環境の作成</span><span class="sxs-lookup"><span data-stu-id="dea51-113">Create your development environment</span></span>

<span data-ttu-id="dea51-114">ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションにMicrosoft 365[必要](https://developer.microsoft.com/microsoft-365/dev-program)があります。</span><span class="sxs-lookup"><span data-stu-id="dea51-114">If you do not have a Microsoft 365 account, you must sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="dea51-115">サブスクリプションは 90 日間無料で、開発アクティビティに使用している限り更新を続行します。</span><span class="sxs-lookup"><span data-stu-id="dea51-115">The subscription is free for 90 days and continues to renew as long as you are using it for development activity.</span></span> <span data-ttu-id="dea51-116">ユーザーがサブスクリプションをVisual Studio EnterpriseまたはProfessional場合、両方のプログラムに無料の開発者サブスクリプションMicrosoft 365[含まれます](https://aka.ms/MyVisualStudioBenefits)。</span><span class="sxs-lookup"><span data-stu-id="dea51-116">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits).</span></span> <span data-ttu-id="dea51-117">サブスクリプションがアクティブである限りVisual Studioアクティブです。</span><span class="sxs-lookup"><span data-stu-id="dea51-117">It is active as long as your Visual Studio subscription is active.</span></span> <span data-ttu-id="dea51-118">詳細については、「開発者向けサブスクリプション[のセットアップ」Microsoft 365参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="dea51-118">For more information, see [set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-teams-for-your-organization"></a><span data-ttu-id="dea51-119">組織Teamsを有効にする</span><span class="sxs-lookup"><span data-stu-id="dea51-119">Enable Teams for your organization</span></span>

<span data-ttu-id="dea51-120">組織のTeamsを有効にする、および詳細については、「組織のTeams[を有効にする」を参照してください](/microsoftteams/enable-features-office-365)。</span><span class="sxs-lookup"><span data-stu-id="dea51-120">Enable Teams for your organization and for more information, see [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="dea51-121">カスタム Teams アプリを有効にして、カスタム アプリのアップロードを有効にする</span><span class="sxs-lookup"><span data-stu-id="dea51-121">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="dea51-122">**開発者テナントのカスタム アプリのアップロードまたはサイドローディングを有効にする**</span><span class="sxs-lookup"><span data-stu-id="dea51-122">**To turn on the custom app uploading or sideloading for your developer tenant**</span></span>

1. <span data-ttu-id="dea51-123">管理者資格情報を[使用Microsoft 365管理](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)センターにサインインします。</span><span class="sxs-lookup"><span data-stu-id="dea51-123">Sign in to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>

2. <span data-ttu-id="dea51-124">[**すべての** > **Teams の表示**]を選択します。</span><span class="sxs-lookup"><span data-stu-id="dea51-124">Select **Show All** > **Teams**.</span></span>

    ![管理センター メニュー](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > <span data-ttu-id="dea51-126">このオプションを表示するには、最大で 24 **Teams** かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="dea51-126">It can take up to 24 hours for the **Teams** option to appear.</span></span> <span data-ttu-id="dea51-127">カスタム アプリ[をテストおよび検証Teams環境](/microsoftteams/upload-custom-apps#validate)にアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="dea51-127">You can [upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation in that time.</span></span>

3. <span data-ttu-id="dea51-128">[アプリの **セットアップ Teams**  >  **グローバル] に**  >  **移動します**。</span><span class="sxs-lookup"><span data-stu-id="dea51-128">Navigate to **Teams apps** > **Setup Policies** > **Global**.</span></span>

   ![サイドロード ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="dea51-130">カスタム **アップロードを On** の位置に **切り替** える。</span><span class="sxs-lookup"><span data-stu-id="dea51-130">Toggle **Upload custom apps** to the **On** position.</span></span>

5. <span data-ttu-id="dea51-131">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="dea51-131">Select **Save**.</span></span> <span data-ttu-id="dea51-132">テスト テナントは、カスタム アプリのサイドローディングを許可できます。</span><span class="sxs-lookup"><span data-stu-id="dea51-132">Your test tenant can permit custom app sideloading.</span></span>

    > [!Note]
    > <span data-ttu-id="dea51-133">サイドローディングがアクティブになるには、最大 24 時間かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="dea51-133">It can take up to 24 hours for the sideloading to be active.</span></span> <span data-ttu-id="dea51-134">暫定的には、アップロードを **使用してアプリ \<your tenant>** をテストできます。</span><span class="sxs-lookup"><span data-stu-id="dea51-134">In the interim, you can use **upload for \<your tenant>** to test your app.</span></span> <span data-ttu-id="dea51-135">アプリのパッケージ .zipをアップロードするには、「カスタム アプリのアップロード [」を参照してください](/microsoftteams/upload-custom-apps#upload)。</span><span class="sxs-lookup"><span data-stu-id="dea51-135">To upload the .zip package file of the app, see [upload custom apps](/microsoftteams/upload-custom-apps#upload).</span></span>

    ![アップロードアプリ ビュー](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="dea51-137">これらの設定の操作方法の詳細については、「Teams[](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)のカスタム アプリ ポリシーと設定を管理する」および「Teams でアプリセットアップ ポリシー[を管理する」を参照してください](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)。</span><span class="sxs-lookup"><span data-stu-id="dea51-137">For complete information on how these settings interact, see [manage custom app policies and settings in Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [manage app setup policies in Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>

## <a name="next-step"></a><span data-ttu-id="dea51-138">次の手順</span><span class="sxs-lookup"><span data-stu-id="dea51-138">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="dea51-139">テスト セットアップの選択</span><span class="sxs-lookup"><span data-stu-id="dea51-139">Choose a test setup</span></span>](~/concepts/build-and-test/debug.md)

