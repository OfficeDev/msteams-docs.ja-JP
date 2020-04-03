---
title: Office 365 テナントの準備
description: Office 365 で Teams の使用を開始する方法
keywords: Office 365 テナントチームのアップロードを構成する
ms.openlocfilehash: 35f102223a5f8e6a8e12268e22aedca07a61b1fa
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120270"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="1d00d-104">Office 365 テナントの準備</span><span class="sxs-lookup"><span data-stu-id="1d00d-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="1d00d-105">Office 365 サブスクライバーの場合は、次のいずれかの[プラン](https://products.office.com/business/compare-more-office-365-for-business-plans)を使用して Microsoft Teams 用アプリを開発できます。</span><span class="sxs-lookup"><span data-stu-id="1d00d-105">If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="1d00d-106">Business Essentials</span><span class="sxs-lookup"><span data-stu-id="1d00d-106">Business Essentials</span></span>
* <span data-ttu-id="1d00d-107">Business Premium</span><span class="sxs-lookup"><span data-stu-id="1d00d-107">Business Premium</span></span>
* <span data-ttu-id="1d00d-108">Enterprise E1、E3、E5</span><span class="sxs-lookup"><span data-stu-id="1d00d-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="1d00d-109">Developer</span><span class="sxs-lookup"><span data-stu-id="1d00d-109">Developer</span></span>
* <span data-ttu-id="1d00d-110">教育、教育プラス、教育の E5</span><span class="sxs-lookup"><span data-stu-id="1d00d-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="1d00d-111">また、[退職](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前に、E4 をサブスクライブしたお客様も、Microsoft Teams を利用することができます。</span><span class="sxs-lookup"><span data-stu-id="1d00d-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="1d00d-112">開発環境のみが必要ですか。</span><span class="sxs-lookup"><span data-stu-id="1d00d-112">Just need a development environment?</span></span>

<span data-ttu-id="1d00d-113">現在 Office 365 アカウントを持っていない場合は、 [office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program)サブスクリプションにサインアップできます。</span><span class="sxs-lookup"><span data-stu-id="1d00d-113">If you don't currently have an Office 365 account, you can sign up for an [Office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="1d00d-114">これは90日間*無料*で、開発アクティビティに使用している間は継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="1d00d-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="1d00d-115">Visual Studio *Enterprise*または*Professional*サブスクリプションを所有している場合は、両方のプログラムに無料の Office 365[開発者サブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、visual studio サブスクリプションの有効期間中にアクティブになります。</span><span class="sxs-lookup"><span data-stu-id="1d00d-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Office 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="1d00d-116">*「* [Microsoft 365 developer サブスクリプションをセットアップする」を](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)参照してください。</span><span class="sxs-lookup"><span data-stu-id="1d00d-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="1d00d-117">組織に対して Microsoft Teams を有効にする</span><span class="sxs-lookup"><span data-stu-id="1d00d-117">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="1d00d-118">Microsoft Teams が組織に対して有効になっていない場合は、最初にその作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d00d-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="1d00d-119">[組織で Teams を有効](https://docs.microsoft.com/microsoftteams/enable-features-office-365)にするための詳細なガイダンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1d00d-119">Take a look at our detailed guidance for [enabling Teams for your organization](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="1d00d-120">カスタム Teams アプリを有効にし、カスタムアプリのアップロードをオンにする</span><span class="sxs-lookup"><span data-stu-id="1d00d-120">Enable custom Teams apps and turn on custom app uploading</span></span>

> [!Note] 
> <span data-ttu-id="1d00d-121">Office 365 developer platform を使用してアプリをビルドしている場合は、アプリのビルド、アップロード、およびテストができるように、これらの設定を構成しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d00d-121">If you're using the Office 365 developer platform to build your app, these settings should already be configured to allow you to build, upload, and test your app.</span></span>

<span data-ttu-id="1d00d-122">カスタムアプリとカスタムアプリのアップロードを有効にするには、次の3つの設定が関係します。</span><span class="sxs-lookup"><span data-stu-id="1d00d-122">There are three settings relevant to enabling custom apps and custom app uploading:</span></span>

* <span data-ttu-id="1d00d-123">**組織全体のカスタムアプリ設定** => **で**カスタム => **アプリを使用することができ**ます—この設定では、組織のカスタムアプリを有効または無効にできます。</span><span class="sxs-lookup"><span data-stu-id="1d00d-123">**Org-wide custom app setting** => **Allow interaction with custom apps** => **On** — This setting enables or disables custom apps for your organization.</span></span> <span data-ttu-id="1d00d-124">これをオンにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d00d-124">It needs to be on.</span></span> 
* <span data-ttu-id="1d00d-125">**チームカスタムアプリ設定** => を使用すると、**メンバーがカスタムアプリ** => **のオン/オフ**をアップロードできるようになります。この設定は、Microsoft Teams 内の個々のチームに適用されます。</span><span class="sxs-lookup"><span data-stu-id="1d00d-125">**Team custom app setting** => **Allow members to upload custom apps** => **On/Off** — This setting applies to each individual team inside Microsoft Teams.</span></span> <span data-ttu-id="1d00d-126">特定のチームに対してアプリをインストールする場合は、そのチームに対してこれをオンにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d00d-126">If you want to install your app for a specific team, this will need to be on for that team.</span></span>
* <span data-ttu-id="1d00d-127">**User custom app policy** => **user はカスタムアプリ** => **をオン/オフに**することができます。この設定により、個々のユーザーのアクセス許可が制御されます。</span><span class="sxs-lookup"><span data-stu-id="1d00d-127">**User custom app policy** => **User can upload custom apps** => **On/Off** — This setting controls the permissions for an individual user.</span></span> <span data-ttu-id="1d00d-128">これは、カスタムアプリのアップロードが許可されている個人に対して有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d00d-128">You'll need to enable this for individuals that are allowed to upload custom apps.</span></span>

<span data-ttu-id="1d00d-129">これらの設定がどのように影響するかの詳細については、「 [Microsoft teams でカスタムアプリポリシーと設定を管理](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)する」および「 [microsoft teams でアプリのセットアップポリシーを管理](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)する *」を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="1d00d-129">For complete information on how these settings interact, *see* [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
