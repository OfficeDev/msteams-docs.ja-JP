---
title: Teams でのリソース固有の同意
description: Teams でのリソース固有の同意とその活用方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams 承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 7e3fc3faa111f4ba982c1c79e6b5b873b8773aef
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819183"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="07425-104">リソース固有の同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="07425-104">Resource-specific consent (RSC)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="07425-105">これらの API にはエンドポイントからアクセス https://graph.microsoft.com/beta できます。</span><span class="sxs-lookup"><span data-stu-id="07425-105">These APIs are accessible in the https://graph.microsoft.com/beta endpoint.</span></span>  <span data-ttu-id="07425-106">ベ [ータ版](/graph/versioning-and-support#beta-version) のエンドポイントには、現在プレビュー段階であり、まだ一般公開されていない API が含まれます。</span><span class="sxs-lookup"><span data-stu-id="07425-106">The [beta version](/graph/versioning-and-support#beta-version) endpoint includes APIs that are currently in preview and are not yet generally available.</span></span> <span data-ttu-id="07425-107">ベータ版のエンドポイントの API は変更されることがあります。運用アプリ内で使用することはお勧めしません。</span><span class="sxs-lookup"><span data-stu-id="07425-107">The APIs in the beta endpoint are subject to change and we don't recommend that you use them in your production apps.</span></span> 

<span data-ttu-id="07425-108">リソース固有の同意 (RSC) は、アプリで API エンドポイントを使用して組織内の特定のチームを管理できる Microsoft Teams と Graph API 統合です。</span><span class="sxs-lookup"><span data-stu-id="07425-108">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="07425-109">リソース固有の同意 (RSC) 許可モデルを *使用すると* 、アプリケーションに対する同意をチーム所有者がチームのデータにアクセスしたり、変更したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="07425-109">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="07425-110">細かい Teams 固有の RSC アクセス許可によって、アプリケーションが特定のチーム内で実行できる操作が定義されます。</span><span class="sxs-lookup"><span data-stu-id="07425-110">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="07425-111">リソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="07425-111">Resource-specific permissions</span></span>

|<span data-ttu-id="07425-112">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="07425-112">Application permission</span></span>| <span data-ttu-id="07425-113">Action</span><span class="sxs-lookup"><span data-stu-id="07425-113">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="07425-114">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="07425-114">TeamSettings.Read.Group</span></span> | <span data-ttu-id="07425-115">このチームの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="07425-115">Get the settings for this team.</span></span>|
|<span data-ttu-id="07425-116">TeamSettings.Edit.Group</span><span class="sxs-lookup"><span data-stu-id="07425-116">TeamSettings.Edit.Group</span></span>|<span data-ttu-id="07425-117">このチームの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="07425-117">Update the settings for this team.</span></span>|
|<span data-ttu-id="07425-118">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="07425-118">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="07425-119">このチームのチャネル名、チャネルの説明、チャネルの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="07425-119">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="07425-120">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="07425-120">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="07425-121">このチームのチャネルの名前、チャネルの説明、チャネルの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="07425-121">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="07425-122">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="07425-122">Channel.Create.Group</span></span>|<span data-ttu-id="07425-123">このチームのチャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="07425-123">Create channels in this team.</span></span>|
|<span data-ttu-id="07425-124">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="07425-124">Channel.Delete.Group</span></span>|<span data-ttu-id="07425-125">このチームのチャネルを削除します。</span><span class="sxs-lookup"><span data-stu-id="07425-125">Delete channels in this team.</span></span>|
|<span data-ttu-id="07425-126">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="07425-126">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="07425-127">このチームのチャネル メッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="07425-127">Get this team's channel messages.</span></span>|
|<span data-ttu-id="07425-128">TeamsApp.Read.Group</span><span class="sxs-lookup"><span data-stu-id="07425-128">TeamsApp.Read.Group</span></span>|<span data-ttu-id="07425-129">このチームがインストールしたアプリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="07425-129">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="07425-130">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="07425-130">TeamsTab.Read.Group</span></span>|<span data-ttu-id="07425-131">このチームのタブの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="07425-131">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="07425-132">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="07425-132">TeamsTab.Create.Group</span></span>|<span data-ttu-id="07425-133">このチームのタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="07425-133">Create tabs in this team.</span></span>|
|<span data-ttu-id="07425-134">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="07425-134">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="07425-135">このチームのタブを更新します。</span><span class="sxs-lookup"><span data-stu-id="07425-135">Update this team's tabs.</span></span>|
|<span data-ttu-id="07425-136">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="07425-136">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="07425-137">このチームのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="07425-137">Delete this team's tabs.</span></span>|
|<span data-ttu-id="07425-138">Member.Read.Group</span><span class="sxs-lookup"><span data-stu-id="07425-138">Member.Read.Group</span></span>|<span data-ttu-id="07425-139">このチームのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="07425-139">Get this team's members.</span></span>|
|<span data-ttu-id="07425-140">Owner.Read.Group</span><span class="sxs-lookup"><span data-stu-id="07425-140">Owner.Read.Group</span></span>|<span data-ttu-id="07425-141">このチームの所有者を取得します。</span><span class="sxs-lookup"><span data-stu-id="07425-141">Get this team's owners.</span></span>|

>[!NOTE]
><span data-ttu-id="07425-142">リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリのみで利用できます。現時点では、Azure Active Directory ポータルの一部には含ていません。</span><span class="sxs-lookup"><span data-stu-id="07425-142">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="07425-143">リソースに固有のアプリケーションの同意を有効にする</span><span class="sxs-lookup"><span data-stu-id="07425-143">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="07425-144">アプリケーションで RSC を有効にする手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="07425-144">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="07425-145">[Azure Active Directory ポータルでグループ所有者の同意設定を構成します](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="07425-145">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="07425-146">[Azure ポータルポータルから Microsoft ID プラットフォームにアプリを登録ADします](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="07425-146">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. [<span data-ttu-id="07425-147">Azure ポータルでアプリケーションのアクセス許可をADする</span><span class="sxs-lookup"><span data-stu-id="07425-147">Review your application permissions in the Azure AD portal</span></span>](#review-your-application-permissions-in-the-azure-ad-portal)
1. <span data-ttu-id="07425-148">[Microsoft ID プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="07425-148">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="07425-149">[Teams アプリ マニフェストを更新します](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="07425-149">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="07425-150">[アプリを Teams に直接インストールします](#install-your-app-directly-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="07425-150">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="07425-151">[追加の RSC アクセス許可がアプリに付与されているか確認します](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="07425-151">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="07425-152">Azure ポータルでグループ所有者の同意設定ADする</span><span class="sxs-lookup"><span data-stu-id="07425-152">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="07425-153">グループ所有者の同意  [は、Azure ポータルで](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) 直接有効または無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="07425-153">You can enable or disable  [group owner consent](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="07425-154">グローバル管理者または会社 [管理者として Azure](https://portal.azure.com) [portal にサインインします](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。</span><span class="sxs-lookup"><span data-stu-id="07425-154">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="07425-155">**Azure Active Directory Enterprise アプリケーション**  => **のユーザー設定**  => **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="07425-155">Select **Azure Active Directory** =>**Enterprise applications** =>**User settings**.</span></span>
> - <span data-ttu-id="07425-156">ユーザーのラベルが付いた管理ラベルが付いたユーザーによる同意の許可 **に同意する、無効化、または制限を、所有グループの企業データにアクセスするアプリに同意することができます** (既定ではこの機能は有効です)。</span><span class="sxs-lookup"><span data-stu-id="07425-156">Enable, disable, or limit user consent with the control labeled **Users can consent to apps accessing company data for the groups they own** (This capability is enabled by default).</span></span>

![Azure Rsc の構成](../../assets/images/azure-rsc-configuration.svg)

| <span data-ttu-id="07425-158">値</span><span class="sxs-lookup"><span data-stu-id="07425-158">Value</span></span> | <span data-ttu-id="07425-159">説明</span><span class="sxs-lookup"><span data-stu-id="07425-159">Description</span></span>|
|--- | --- |
|<span data-ttu-id="07425-160">はい</span><span class="sxs-lookup"><span data-stu-id="07425-160">Yes</span></span> | <span data-ttu-id="07425-161">グループ固有の同意をすべてのグループ所有者に対して有効にします。</span><span class="sxs-lookup"><span data-stu-id="07425-161">Enable group-specific consent for all group owners.</span></span>|
|<span data-ttu-id="07425-162">いいえ</span><span class="sxs-lookup"><span data-stu-id="07425-162">No</span></span> |<span data-ttu-id="07425-163">すべてのユーザーに対してグループ固有の同意を無効にします。</span><span class="sxs-lookup"><span data-stu-id="07425-163">Disable group-specific consent for all users.</span></span>| 
|<span data-ttu-id="07425-164">制限付き</span><span class="sxs-lookup"><span data-stu-id="07425-164">Limited</span></span> | <span data-ttu-id="07425-165">選択したグループのメンバーに対してグループ固有の同意を有効にします。</span><span class="sxs-lookup"><span data-stu-id="07425-165">Enable group-specific consent for members of a selected group.</span></span>|

<span data-ttu-id="07425-166">PowerShell を使用して Azure portal 内でグループ所有者の同意を有効または無効にするには、PowerShell を使用してグループ所有者 [の同意を構成する手順に従います](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)。</span><span class="sxs-lookup"><span data-stu-id="07425-166">To enable or disable group owner consent within the Azure portal using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="07425-167">Azure AD ポータルから Microsoft ID プラットフォームにアプリを登録する</span><span class="sxs-lookup"><span data-stu-id="07425-167">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="07425-168">Azure Active Directory ポータルは、アプリを登録および構成するための中央プラットフォームを提供します。</span><span class="sxs-lookup"><span data-stu-id="07425-168">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="07425-169">Microsoft ID プラットフォームと統合し、Graph API を呼び出すには、アプリを Azure AD ポータルに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="07425-169">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Graph APIs.</span></span> <span data-ttu-id="07425-170">*「*[アプリケーションを Microsoft ID プラットフォームに登録する」を参照してください](/graph/auth-register-app-v2)。</span><span class="sxs-lookup"><span data-stu-id="07425-170">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="07425-171">複数の Teams アプリを同じ Azure アプリ ID にADしないようにします。アプリ ID は、アプリごとに一意にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="07425-171">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="07425-172">同じアプリ ID に対して複数のアプリをインストールしようとすると失敗します。</span><span class="sxs-lookup"><span data-stu-id="07425-172">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="07425-173">Azure ポータルでアプリケーションのアクセス許可をADする</span><span class="sxs-lookup"><span data-stu-id="07425-173">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="07425-174">ホーム アプリの**登録ページ**  =>  **に移動し、RSC**アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="07425-174">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="07425-175">左側 **のナビゲーション バー** から API アクセス許可を選択し、アプリに構成されているアクセス許可の一覧を確認します。</span><span class="sxs-lookup"><span data-stu-id="07425-175">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="07425-176">アプリが RSC グラフ呼び出しのみを行う場合は、そのページですべてのアクセス許可を削除します。</span><span class="sxs-lookup"><span data-stu-id="07425-176">If your app will only make RSC Graph calls, delete all the permission on that page.</span></span> <span data-ttu-id="07425-177">アプリで RSC 以外の呼び出しを行う場合は、必要に応じてこれらのアクセス許可を保持します。</span><span class="sxs-lookup"><span data-stu-id="07425-177">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="07425-178">Azure ADは RSC アクセス許可を要求するために使用できません。</span><span class="sxs-lookup"><span data-stu-id="07425-178">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="07425-179">RSC アクセス許可は、現在 Teams クライアントにインストールされている Teams アプリケーションに対してのみで、アプリ マニフェスト (JSON) ファイルで宣言されます。</span><span class="sxs-lookup"><span data-stu-id="07425-179">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="07425-180">Microsoft ID プラットフォームからアクセス トークンを取得する</span><span class="sxs-lookup"><span data-stu-id="07425-180">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="07425-181">Graph API を呼び出すには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="07425-181">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="07425-182">アプリが Microsoft ID プラットフォームからトークンを取得するには、その前に Azure ポータルに登録しておくADがあります。</span><span class="sxs-lookup"><span data-stu-id="07425-182">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="07425-183">アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。</span><span class="sxs-lookup"><span data-stu-id="07425-183">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="07425-184">ID プラットフォームからアクセス トークンを取得するには、Azure AD の登録プロセスから次に示す値が必要になります。</span><span class="sxs-lookup"><span data-stu-id="07425-184">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="07425-185">アプリ **登録ポータルによって** 割り当てられたアプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="07425-185">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="07425-186">アプリがシングル サインオン (SSO) をサポートする場合は、アプリと SSO で同じアプリケーション ID を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="07425-186">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="07425-187">クライアント  **シークレット/パスワード** 、または公開/秘密キーのペア (**証明書)** です。</span><span class="sxs-lookup"><span data-stu-id="07425-187">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="07425-188">ネイティブ アプリの場合、これは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="07425-188">This is not required for native apps.</span></span>
- <span data-ttu-id="07425-189">Azure **アプリからの** 応答を受信するためのリダイレクト URI (またはAD。</span><span class="sxs-lookup"><span data-stu-id="07425-189">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="07425-190">*ユーザー*[に代わって取得するアクセスと、ユーザーなし](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token)[の Get アクセスの表示](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="07425-190">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="07425-191">Teams アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="07425-191">Update your Teams app manifest</span></span>

<span data-ttu-id="07425-192">RSC アクセス許可はアプリ マニフェスト ファイル (JSON) で宣言されます。</span><span class="sxs-lookup"><span data-stu-id="07425-192">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="07425-193">次の [値を使用して](../../resources/schema/manifest-schema.md#webapplicationinfo) 、アプリ マニフェストに webApplicationInfo キーを追加します。</span><span class="sxs-lookup"><span data-stu-id="07425-193">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="07425-194">**id**  — Azure AD アプリ ID。 *Azure* [ポータルのアプリの登録AD覧ください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="07425-194">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="07425-195">**resource**  — 任意の文字列。</span><span class="sxs-lookup"><span data-stu-id="07425-195">**resource**  — any string.</span></span> <span data-ttu-id="07425-196">このフィールドは RSC では操作を実行できませんが、追加されたものである必要があります。また、エラー応答を回避するためにはその値が設定されている必要があります。任意の文字列を使用します。</span><span class="sxs-lookup"><span data-stu-id="07425-196">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="07425-197">**アプリケーションのアクセス** 許可 — アプリ用の RSC 権限。</span><span class="sxs-lookup"><span data-stu-id="07425-197">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="07425-198">*リソース固有*[のアクセス許可を参照してください](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="07425-198">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="07425-199">RSC 以外のアクセス許可は Azure portal に格納されます。</span><span class="sxs-lookup"><span data-stu-id="07425-199">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="07425-200">アプリ マニフェストには追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="07425-200">Do not add them to the app manifest.</span></span>
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.ReadWrite.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.ReadWrite.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="07425-201">アプリを Teams に直接インストールする</span><span class="sxs-lookup"><span data-stu-id="07425-201">Install your app directly in Teams</span></span>

<span data-ttu-id="07425-202">アプリを作成したら、アプリ パッケージ [を特定のチーム](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) に直接アップロードできます。</span><span class="sxs-lookup"><span data-stu-id="07425-202">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="07425-203">この操作を行うには、[ **カスタム アプリのアップロード]** ポリシーの一部として、カスタム アプリのアップロード ポリシー設定を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="07425-203">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="07425-204">*カスタム アプリ*[ポリシー設定をご覧ください](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。</span><span class="sxs-lookup"><span data-stu-id="07425-204">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="07425-205">追加の RSC アクセス許可がアプリに付与されているか確認する</span><span class="sxs-lookup"><span data-stu-id="07425-205">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="07425-206">RSC のアクセス許可はユーザーに属性が設定されません。</span><span class="sxs-lookup"><span data-stu-id="07425-206">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="07425-207">呼び出しは、ユーザーに委任されたアクセス許可で行われません。</span><span class="sxs-lookup"><span data-stu-id="07425-207">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="07425-208">そのため、アプリは、チャネルの作成やタブの削除など、ユーザーが操作できないアクションを実行できる場合があります。RSC API 呼び出しを行う前に、チーム所有者の使用目的を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="07425-208">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="07425-209">*Microsoft* [Teams API の概要を参照してください](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="07425-209">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="07425-210">アプリがチームにインストールされると [、Graph エクスプローラ](https://developer.microsoft.com/graph/graph-explorer)  ーを使用して、チーム内のアプリに付与されているアクセス許可を表示できます。</span><span class="sxs-lookup"><span data-stu-id="07425-210">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="07425-211">Teams クライアントからチーム **の groupId** を取得します。</span><span class="sxs-lookup"><span data-stu-id="07425-211">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="07425-212">Teams クライアントで、左のナビゲーション バーから **Teams** を選択します。</span><span class="sxs-lookup"><span data-stu-id="07425-212">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="07425-213">ドロップダウン メニューから、アプリがインストールされているチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="07425-213">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="07425-214">[その他 **のオプション] アイコン** (タスク&#8943;)。</span><span class="sxs-lookup"><span data-stu-id="07425-214">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="07425-215">[ **チームへのリンクを取得] を選します**。</span><span class="sxs-lookup"><span data-stu-id="07425-215">Select **Get link to team**.</span></span>
> - <span data-ttu-id="07425-216">文字列から **groupId 値をコピー** して保存します。</span><span class="sxs-lookup"><span data-stu-id="07425-216">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="07425-217">Graph エクスプローラ **ーにログインします**。</span><span class="sxs-lookup"><span data-stu-id="07425-217">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="07425-218">次のエンド **ポイントに** 対して GET を呼び出します `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` : 。</span><span class="sxs-lookup"><span data-stu-id="07425-218">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="07425-219">応答の clientAppId フィールドは、Teams アプリ マニフェストで指定された appId にマップされます。</span><span class="sxs-lookup"><span data-stu-id="07425-219">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="07425-220">![Get 呼び出しに対する Graph エクスプローラーの応答。](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="07425-220">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>
 
## <a name="test-resource-specific-consent"></a><span data-ttu-id="07425-221">リソース固有の同意をテストする</span><span class="sxs-lookup"><span data-stu-id="07425-221">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="07425-222">**Teams でリソース固有の同意のアクセス許可をテストする**</span><span class="sxs-lookup"><span data-stu-id="07425-222">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="07425-223">Teams 管理者向けの関連トピック</span><span class="sxs-lookup"><span data-stu-id="07425-223">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07425-224">**管理者向けに Microsoft Teams でのリソース固有の同意**</span><span class="sxs-lookup"><span data-stu-id="07425-224">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 
