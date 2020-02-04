---
title: Office 365 テナントの準備
description: Office 365 で Teams の使用を開始する方法
keywords: Office 365 テナントチームのアップロードを構成する
ms.openlocfilehash: 62cd640196631f50c72762253ff1bd75a143337d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674988"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="11b52-104">Office 365 テナントの準備</span><span class="sxs-lookup"><span data-stu-id="11b52-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="11b52-105">Microsoft Teams 用のアプリを開発するには、[次のいずれかのプランを使用して Office 365 お客様](https://products.office.com/business/compare-more-office-365-for-business-plans)になる必要があります。</span><span class="sxs-lookup"><span data-stu-id="11b52-105">To develop apps for Microsoft Teams, you need to be an [Office 365 customer with one of the following plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>

* <span data-ttu-id="11b52-106">Business Essentials</span><span class="sxs-lookup"><span data-stu-id="11b52-106">Business Essentials</span></span>
* <span data-ttu-id="11b52-107">Business Premium</span><span class="sxs-lookup"><span data-stu-id="11b52-107">Business Premium</span></span>
* <span data-ttu-id="11b52-108">Enterprise E1、E3、E5</span><span class="sxs-lookup"><span data-stu-id="11b52-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="11b52-109">Developer</span><span class="sxs-lookup"><span data-stu-id="11b52-109">Developer</span></span>
* <span data-ttu-id="11b52-110">教育、教育プラス、教育の E5</span><span class="sxs-lookup"><span data-stu-id="11b52-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="11b52-111">また、廃棄の前に E4 を購入したお客様も、Microsoft Teams を利用することができます。</span><span class="sxs-lookup"><span data-stu-id="11b52-111">Microsoft Teams will also be available to customers who purchased E4 prior to its retirement.</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="11b52-112">開発環境のみが必要ですか。</span><span class="sxs-lookup"><span data-stu-id="11b52-112">Just need a development environment?</span></span>

<span data-ttu-id="11b52-113">現在 Office 365 アカウントを持っていない場合は、office [365 開発者プログラム](https://dev.office.com/devprogram)にサインアップして、*無料*の90日間を取得できます (開発アクティビティに使用している間は更新できます) office 365 developer テナント。</span><span class="sxs-lookup"><span data-stu-id="11b52-113">If you don't currently have an Office 365 account, you can sign up for the [Office 365 Developer program](https://dev.office.com/devprogram) to get a *free* 90 days (can be renewed for as long as you're using it for development activity) Office 365 Developer Tenant.</span></span> <span data-ttu-id="11b52-114">このアカウントは、テスト目的にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="11b52-114">This account can only be used for testing purposes.</span></span> <span data-ttu-id="11b52-115">[テストアカウントの](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US)セットアップの詳細については、「」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="11b52-115">See more information on [setting up your test accounts](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="11b52-116">組織に対して Microsoft Teams を有効にする</span><span class="sxs-lookup"><span data-stu-id="11b52-116">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="11b52-117">Microsoft Teams が組織でまだ有効になっていない場合は、最初にその作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="11b52-117">If Microsoft Teams is not yet enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="11b52-118">[組織で Teams を有効](/microsoftteams/how-to-roll-out-teams)にするための詳細なガイダンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="11b52-118">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/how-to-roll-out-teams).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="11b52-119">カスタム Teams アプリを有効にし、カスタムアプリのアップロードをオンにする</span><span class="sxs-lookup"><span data-stu-id="11b52-119">Enable custom Teams apps and turn on custom app uploading</span></span>

> <span data-ttu-id="11b52-120">注: O365 開発者組織を使用してアプリを構築している場合は、アプリのビルド、アップロード、およびテストができるように、これらの設定を構成しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="11b52-120">Note: If you're using an O365 Developer Organization to build your app, these settings should already be configured to allow you to build, upload and test your app.</span></span>

<span data-ttu-id="11b52-121">カスタムアプリとカスタムアプリのアップロードを有効にするには、次の3つの設定が関係します。</span><span class="sxs-lookup"><span data-stu-id="11b52-121">There are three settings involved in enabling custom apps and custom app uploading:</span></span>

* <span data-ttu-id="11b52-122">組織**全体のカスタムアプリ設定**-この設定は、組織のカスタムアプリを有効または無効にします。</span><span class="sxs-lookup"><span data-stu-id="11b52-122">**Org-wide custom app setting** - This setting either enables or disables custom apps for your organization.</span></span> <span data-ttu-id="11b52-123">これをオンにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="11b52-123">It needs to be on.</span></span> 
* <span data-ttu-id="11b52-124">[ **Team custom app setting** ]-この設定は、Microsoft Teams 内の個々のチームに対して使用されます。</span><span class="sxs-lookup"><span data-stu-id="11b52-124">**Team custom app setting** - This setting is for each individual team inside Microsoft Teams.</span></span> <span data-ttu-id="11b52-125">特定のチームに対してアプリをインストールする場合は、そのチームに対してこれをオンにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="11b52-125">If you want to install your app for a specific team, this will need to be on for that team.</span></span>
* <span data-ttu-id="11b52-126">**User custom app policy** -この設定セットは、個々のユーザーのアクセス許可を制御します。</span><span class="sxs-lookup"><span data-stu-id="11b52-126">**User custom app policy** - This set of settings controls the permissions for an individual user.</span></span> <span data-ttu-id="11b52-127">カスタムアプリをアップロードする個人に対して、これを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="11b52-127">You'll need to enable this for individuals you want to upload custom apps.</span></span>

<span data-ttu-id="11b52-128">これらの設定の相互関係の詳細については[、「Microsoft Teams でカスタムアプリポリシーと設定を管理](/MicrosoftTeams/teams-custom-app-policies-and-settings)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="11b52-128">For complete information on how these settings interact see [Manage custom app policies and settings in Microsoft Teams](/MicrosoftTeams/teams-custom-app-policies-and-settings).</span></span>
