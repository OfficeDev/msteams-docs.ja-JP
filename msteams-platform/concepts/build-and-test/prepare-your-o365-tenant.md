---
title: Office 365 テナントを準備する
description: Office 365 で Teams の使用を開始する方法
keywords: Office 365 テナントチームのアップロードを構成する
ms.openlocfilehash: e07ffe7f5325be1293a49934669f36c81613278b
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914568"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="4f080-104">Office 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="4f080-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="4f080-105">Office 365 サブスクライバーの場合は、次のいずれかの[プラン](https://products.office.com/business/compare-more-office-365-for-business-plans)を使用して Microsoft Teams 用アプリを開発できます。</span><span class="sxs-lookup"><span data-stu-id="4f080-105">If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="4f080-106">Business Essentials</span><span class="sxs-lookup"><span data-stu-id="4f080-106">Business Essentials</span></span>
* <span data-ttu-id="4f080-107">Business Premium</span><span class="sxs-lookup"><span data-stu-id="4f080-107">Business Premium</span></span>
* <span data-ttu-id="4f080-108">Enterprise E1、E3、E5</span><span class="sxs-lookup"><span data-stu-id="4f080-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="4f080-109">Developer</span><span class="sxs-lookup"><span data-stu-id="4f080-109">Developer</span></span>
* <span data-ttu-id="4f080-110">教育、教育プラス、教育の E5</span><span class="sxs-lookup"><span data-stu-id="4f080-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="4f080-111">また、[退職](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前に、E4 をサブスクライブしたお客様も、Microsoft Teams を利用することができます。</span><span class="sxs-lookup"><span data-stu-id="4f080-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="4f080-112">開発環境のみが必要ですか。</span><span class="sxs-lookup"><span data-stu-id="4f080-112">Just need a development environment?</span></span>

<span data-ttu-id="4f080-113">現在 Office 365 アカウントを持っていない場合は、 [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program)サブスクリプションにサインアップできます。</span><span class="sxs-lookup"><span data-stu-id="4f080-113">If you don't currently have an Office 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="4f080-114">これは90日間*無料*で、開発アクティビティに使用している間は継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="4f080-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="4f080-115">Visual Studio *Enterprise*または*Professional*サブスクリプションを所有している場合は、どちらのプログラムにも、visual studio サブスクリプションの有効期間中にアクティブな Microsoft 365[開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="4f080-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="4f080-116">*「* [Microsoft 365 developer サブスクリプションをセットアップする」を](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)参照してください。</span><span class="sxs-lookup"><span data-stu-id="4f080-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="4f080-117">組織に対して Microsoft Teams を有効にする</span><span class="sxs-lookup"><span data-stu-id="4f080-117">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="4f080-118">Microsoft Teams が組織に対して有効になっていない場合は、最初にその作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4f080-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="4f080-119">[組織で Teams を有効](https://docs.microsoft.com/microsoftteams/enable-features-office-365)にするための詳細なガイダンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4f080-119">Take a look at our detailed guidance for [enabling Teams for your organization](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="4f080-120">カスタム Teams アプリを有効にし、カスタムアプリのアップロードをオンにする</span><span class="sxs-lookup"><span data-stu-id="4f080-120">Enable custom Teams apps and turn on custom app uploading</span></span>

> [!Note] 
> <span data-ttu-id="4f080-121">Office 365 developer platform を使用してアプリをビルドしている場合は、アプリのビルド、アップロード、およびテストができるように、これらの設定を構成しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="4f080-121">If you're using the Office 365 developer platform to build your app, these settings should already be configured to allow you to build, upload, and test your app.</span></span>

<span data-ttu-id="4f080-122">カスタムアプリとカスタムアプリのアップロードを有効にするには、次の3つの設定が関係します。</span><span class="sxs-lookup"><span data-stu-id="4f080-122">There are three settings relevant to enabling custom apps and custom app uploading:</span></span>

* <span data-ttu-id="4f080-123">**組織全体のカスタムアプリ設定** => **で**カスタム => **アプリを使用することができ**ます—この設定では、組織のカスタムアプリを有効または無効にできます。</span><span class="sxs-lookup"><span data-stu-id="4f080-123">**Org-wide custom app setting** => **Allow interaction with custom apps** => **On** — This setting enables or disables custom apps for your organization.</span></span> <span data-ttu-id="4f080-124">これをオンにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4f080-124">It needs to be on.</span></span> 
* <span data-ttu-id="4f080-125">**チームカスタムアプリ設定** => を使用すると、**メンバーがカスタムアプリ** => **のオン/オフ**をアップロードできるようになります。この設定は、Microsoft Teams 内の個々のチームに適用されます。</span><span class="sxs-lookup"><span data-stu-id="4f080-125">**Team custom app setting** => **Allow members to upload custom apps** => **On/Off** — This setting applies to each individual team inside Microsoft Teams.</span></span> <span data-ttu-id="4f080-126">特定のチームに対してアプリをインストールする場合は、そのチームに対してこれをオンにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4f080-126">If you want to install your app for a specific team, this will need to be on for that team.</span></span>
* <span data-ttu-id="4f080-127">**User custom app policy** => **user はカスタムアプリ** => **をオン/オフに**することができます。この設定により、個々のユーザーのアクセス許可が制御されます。</span><span class="sxs-lookup"><span data-stu-id="4f080-127">**User custom app policy** => **User can upload custom apps** => **On/Off** — This setting controls the permissions for an individual user.</span></span> <span data-ttu-id="4f080-128">これは、カスタムアプリのアップロードが許可されている個人に対して有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4f080-128">You'll need to enable this for individuals that are allowed to upload custom apps.</span></span>

<span data-ttu-id="4f080-129">これらの設定がどのように影響するかの詳細については、「 [Microsoft teams でカスタムアプリポリシーと設定を管理](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)する」および「 [microsoft teams でアプリのセットアップポリシーを管理](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)する *」を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="4f080-129">For complete information on how these settings interact, *see* [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
