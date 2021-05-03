---
title: リソース固有の同意 (Teams
description: リソース固有の同意について、Teams活用する方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: teams 承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 39e5c1bb8375fb5b5a3bd3900cb6ad870a3ff677
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101794"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="7022d-104">リソース固有の同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="7022d-104">Resource-specific consent (RSC)</span></span>

<span data-ttu-id="7022d-105">リソース固有の同意 (RSC) は、アプリが API エンドポイントを使用して組織内の特定のチームを管理できる Microsoft Teams API と Microsoft Graph API 統合です。</span><span class="sxs-lookup"><span data-stu-id="7022d-105">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="7022d-106">リソース固有の同意 (RSC) アクセス許可モデルを使用すると、チーム所有者は、アプリケーションがチームのデータにアクセスしたり変更したりするための同意を付与できます。</span><span class="sxs-lookup"><span data-stu-id="7022d-106">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="7022d-107">詳細で、Teams固有の RSC アクセス許可は、特定のチーム内でアプリケーションが実行できる操作を定義します。</span><span class="sxs-lookup"><span data-stu-id="7022d-107">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="7022d-108">リソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="7022d-108">Resource-specific permissions</span></span>

|<span data-ttu-id="7022d-109">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="7022d-109">Application permission</span></span>| <span data-ttu-id="7022d-110">Action</span><span class="sxs-lookup"><span data-stu-id="7022d-110">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="7022d-111">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-111">TeamSettings.Read.Group</span></span> | <span data-ttu-id="7022d-112">このチームの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="7022d-112">Get the settings for this team.</span></span>|
|<span data-ttu-id="7022d-113">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-113">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="7022d-114">このチームの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="7022d-114">Update the settings for this team.</span></span>|
|<span data-ttu-id="7022d-115">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-115">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="7022d-116">このチームのチャネル名、チャネルの説明、チャネル設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="7022d-116">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="7022d-117">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-117">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="7022d-118">このチームのチャネル名、チャネルの説明、チャネル設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="7022d-118">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="7022d-119">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-119">Channel.Create.Group</span></span>|<span data-ttu-id="7022d-120">このチームのチャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="7022d-120">Create channels in this team.</span></span>|
|<span data-ttu-id="7022d-121">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-121">Channel.Delete.Group</span></span>|<span data-ttu-id="7022d-122">このチームのチャネルを削除します。</span><span class="sxs-lookup"><span data-stu-id="7022d-122">Delete channels in this team.</span></span>|
|<span data-ttu-id="7022d-123">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-123">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="7022d-124">このチームのチャネル メッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="7022d-124">Get this team's channel messages.</span></span>|
|<span data-ttu-id="7022d-125">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-125">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="7022d-126">このチームのインストール済みアプリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="7022d-126">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="7022d-127">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-127">TeamsTab.Read.Group</span></span>|<span data-ttu-id="7022d-128">このチームのタブの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="7022d-128">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="7022d-129">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-129">TeamsTab.Create.Group</span></span>|<span data-ttu-id="7022d-130">このチームのタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="7022d-130">Create tabs in this team.</span></span>|
|<span data-ttu-id="7022d-131">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-131">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="7022d-132">このチームのタブを更新します。</span><span class="sxs-lookup"><span data-stu-id="7022d-132">Update this team's tabs.</span></span>|
|<span data-ttu-id="7022d-133">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-133">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="7022d-134">このチームのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="7022d-134">Delete this team's tabs.</span></span>|
|<span data-ttu-id="7022d-135">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7022d-135">TeamMember.Read.Group</span></span>|<span data-ttu-id="7022d-136">このチームのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="7022d-136">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="7022d-137">リソース固有のアクセス許可は、Teams クライアントにインストールTeamsアプリでのみ使用できます。現在は、Azure Active Directory ポータルの一部ではありません。</span><span class="sxs-lookup"><span data-stu-id="7022d-137">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="7022d-138">アプリケーションでリソース固有の同意を有効にする</span><span class="sxs-lookup"><span data-stu-id="7022d-138">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="7022d-139">アプリケーションで RSC を有効にする手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7022d-139">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="7022d-140">[ポータルでグループ所有者の同意設定をAzure Active Directoryします](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="7022d-140">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="7022d-141">[Azure Microsoft ID プラットフォーム ポータルをADします](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="7022d-141">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="7022d-142">[Azure ADポータルでアプリケーションのアクセス許可を確認します](#review-your-application-permissions-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="7022d-142">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="7022d-143">[Microsoft Identity プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="7022d-143">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="7022d-144">[アプリ マニフェストTeams更新します](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="7022d-144">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="7022d-145">[アプリをアプリに直接インストールTeams。](#sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="7022d-145">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="7022d-146">[アプリで追加された RSC アクセス許可を確認します](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="7022d-146">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="7022d-147">Azure AD ポータルでグループ所有者の同意設定を構成する</span><span class="sxs-lookup"><span data-stu-id="7022d-147">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="7022d-148">Azure portal 内でグループ所有者 [の同意を直接](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 有効または無効にできます。</span><span class="sxs-lookup"><span data-stu-id="7022d-148">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="7022d-149">グローバル管理者/ [会社管理者として Azure](https://portal.azure.com) portal [にサインインします](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。</span><span class="sxs-lookup"><span data-stu-id="7022d-149">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="7022d-150">[[アプリケーション](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)  =>  **Azure Active Directory Enterpriseと** アクセス許可ユーザー  =>  **の同意設定**  =>  **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="7022d-150">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="7022d-151">データにアクセスするアプリに対するグループ所有者の同意というラベルが付いたコントロールを使用して、ユーザーの同意を有効、無効、または制限します **(既定** では、すべてのグループ所有者にグループ所有者の同意 **を許可します**)。</span><span class="sxs-lookup"><span data-stu-id="7022d-151">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="7022d-152">チームの所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7022d-152">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![azure rsc 構成](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="7022d-154">PowerShell を使用してグループ所有者の同意を有効または無効にするには、「PowerShell を使用してグループ所有者の同意を構成する」で説明 [されている手順に従います](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="7022d-154">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="7022d-155">Azure Microsoft ID プラットフォーム ポータルを使用してアプリをADする</span><span class="sxs-lookup"><span data-stu-id="7022d-155">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="7022d-156">このAzure Active Directoryは、アプリを登録および構成する中心的なプラットフォームを提供します。</span><span class="sxs-lookup"><span data-stu-id="7022d-156">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="7022d-157">アプリを Azure ADポータルに登録して、アプリと統合し、Microsoft Microsoft ID プラットフォーム API Graphする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7022d-157">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="7022d-158">*「*[アプリケーションをアプリケーションに登録する」を参照Microsoft ID プラットフォーム。](/graph/auth-register-app-v2)</span><span class="sxs-lookup"><span data-stu-id="7022d-158">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="7022d-159">複数のアプリを同Teams Azure アプリ ID に登録ADしない。アプリ ID は、アプリごとに一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="7022d-159">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="7022d-160">同じアプリ ID に複数のアプリをインストールしようとすると失敗します。</span><span class="sxs-lookup"><span data-stu-id="7022d-160">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="7022d-161">Azure AD ポータルでアプリケーションのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="7022d-161">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="7022d-162">[ホーム アプリの **登録**  =>  **] ページに移動し**、RSC アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="7022d-162">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="7022d-163">左側 **のナビゲーション バーから API** アクセス許可を選択し、アプリに対して構成されているアクセス許可の一覧を確認します。</span><span class="sxs-lookup"><span data-stu-id="7022d-163">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="7022d-164">アプリが API 呼び出しでのみ RSC Graphする場合は、そのページのすべてのアクセス許可を削除します。</span><span class="sxs-lookup"><span data-stu-id="7022d-164">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="7022d-165">アプリで RSC 以外の呼び出しを行う場合は、必要に応じてこれらのアクセス許可を保持します。</span><span class="sxs-lookup"><span data-stu-id="7022d-165">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="7022d-166">Azure ADポータルを使用して RSC アクセス許可を要求することはできません。</span><span class="sxs-lookup"><span data-stu-id="7022d-166">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="7022d-167">RSC アクセス許可は現在、Teams クライアントにインストールされているアプリケーションTeams専用であり、アプリ マニフェスト (JSON) ファイルで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="7022d-167">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="7022d-168">サーバーからアクセス トークンを取得Microsoft ID プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="7022d-168">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="7022d-169">API 呼びGraphするには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7022d-169">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="7022d-170">アプリがアプリからトークンを取得するには、Microsoft ID プラットフォーム Azure ポータルに登録するADがあります。</span><span class="sxs-lookup"><span data-stu-id="7022d-170">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="7022d-171">アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。</span><span class="sxs-lookup"><span data-stu-id="7022d-171">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="7022d-172">ID プラットフォームからアクセス トークンを取得するには、Azure AD登録プロセスから次の値を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7022d-172">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="7022d-173">アプリ **登録ポータルによって** 割り当てられたアプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="7022d-173">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="7022d-174">アプリがシングル サインオン (SSO) をサポートしている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7022d-174">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="7022d-175">クライアント  **シークレット/パスワード、** または公開/秘密キーのペア (**証明書**)。</span><span class="sxs-lookup"><span data-stu-id="7022d-175">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="7022d-176">ネイティブ アプリの場合、これは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="7022d-176">This is not required for native apps.</span></span>
- <span data-ttu-id="7022d-177">Azure **サーバーから応答** を受信するアプリのリダイレクト URI (または返信 URL) AD。</span><span class="sxs-lookup"><span data-stu-id="7022d-177">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="7022d-178">*「*[ユーザーに代わってアクセスを取得する」および](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)「[ユーザーなしでアクセスを取得する」を参照してください。](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="7022d-178">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="7022d-179">アプリ マニフェストTeams更新する</span><span class="sxs-lookup"><span data-stu-id="7022d-179">Update your Teams app manifest</span></span>

<span data-ttu-id="7022d-180">RSC アクセス許可は、アプリ マニフェスト (JSON) ファイルで宣言されます。</span><span class="sxs-lookup"><span data-stu-id="7022d-180">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="7022d-181">次の [値を使用して、WebApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="7022d-181">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="7022d-182">**id**  — Azure ADアプリ *ID。「Azure* AD ポータルにアプリ [を登録する」を参照してください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="7022d-182">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="7022d-183">**resource**  — 任意の文字列。</span><span class="sxs-lookup"><span data-stu-id="7022d-183">**resource**  — any string.</span></span> <span data-ttu-id="7022d-184">このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加して値を指定する必要があります。任意の文字列が実行します。</span><span class="sxs-lookup"><span data-stu-id="7022d-184">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="7022d-185">**アプリケーションのアクセス許可** - アプリの RSC アクセス許可。</span><span class="sxs-lookup"><span data-stu-id="7022d-185">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="7022d-186">*「*[リソース固有のアクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="7022d-186">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="7022d-187">RSC 以外のアクセス許可は Azure portal に格納されます。</span><span class="sxs-lookup"><span data-stu-id="7022d-187">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="7022d-188">アプリ マニフェストに追加しません。</span><span class="sxs-lookup"><span data-stu-id="7022d-188">Do not add them to the app manifest.</span></span>
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

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="7022d-189">アプリをサイドロードTeams</span><span class="sxs-lookup"><span data-stu-id="7022d-189">Sideload your app in Teams</span></span>

<span data-ttu-id="7022d-190">管理者がTeamsアプリのアップロードを許可している場合は、アプリを特定[](~/concepts/deploy-and-publish/apps-upload.md)のチームに直接サイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="7022d-190">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="7022d-191">アプリで追加された RSC アクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="7022d-191">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="7022d-192">RSC アクセス許可は、ユーザーに属性付けされません。</span><span class="sxs-lookup"><span data-stu-id="7022d-192">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="7022d-193">呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可を使用して行います。</span><span class="sxs-lookup"><span data-stu-id="7022d-193">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="7022d-194">したがって、アプリは、チャネルの作成やタブの削除など、ユーザーが実行できない操作を実行できる場合があります。RSC API 呼び出しを行う前に、チーム所有者の使用例の意図を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7022d-194">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="7022d-195">*「API* [Microsoft Teams」を参照してください](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="7022d-195">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="7022d-196">アプリをチームにインストールしたら、Graph[エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を使用して、チーム内のアプリに付与されたアクセス許可を表示できます。</span><span class="sxs-lookup"><span data-stu-id="7022d-196">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="7022d-197">チームの **groupId** をクライアントから取得Teamsします。</span><span class="sxs-lookup"><span data-stu-id="7022d-197">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="7022d-198">クライアントで、Teams **ナビゲーション** バー Teamsを選択します。</span><span class="sxs-lookup"><span data-stu-id="7022d-198">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="7022d-199">ドロップダウン メニューからアプリがインストールされているチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="7022d-199">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="7022d-200">[その他 **のオプション]** アイコンを選択します (&#8943;)。</span><span class="sxs-lookup"><span data-stu-id="7022d-200">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="7022d-201">[チーム **へのリンクを取得する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="7022d-201">Select **Get link to team**.</span></span>
> - <span data-ttu-id="7022d-202">文字列から **groupId 値をコピー** して保存します。</span><span class="sxs-lookup"><span data-stu-id="7022d-202">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="7022d-203">エクスプローラーに **Graphします**。</span><span class="sxs-lookup"><span data-stu-id="7022d-203">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="7022d-204">次の **エンドポイントに対** して GET 呼び出しを行います `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 。</span><span class="sxs-lookup"><span data-stu-id="7022d-204">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="7022d-205">応答の clientAppId フィールドは、アプリ マニフェストで指定された appId にTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="7022d-205">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="7022d-206">![Graphに対するエクスプローラーの応答を確認します。](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="7022d-206">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="7022d-207">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="7022d-207">Code sample</span></span>
| <span data-ttu-id="7022d-208">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="7022d-208">**Sample name**</span></span> | <span data-ttu-id="7022d-209">**説明**</span><span class="sxs-lookup"><span data-stu-id="7022d-209">**Description**</span></span> | <span data-ttu-id="7022d-210">**.NET**</span><span class="sxs-lookup"><span data-stu-id="7022d-210">**.NET**</span></span> |<span data-ttu-id="7022d-211">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="7022d-211">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="7022d-212">リソース固有の同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="7022d-212">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="7022d-213">RSC を使用して API Graph呼び出します。</span><span class="sxs-lookup"><span data-stu-id="7022d-213">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="7022d-214">View</span><span class="sxs-lookup"><span data-stu-id="7022d-214">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="7022d-215">View</span><span class="sxs-lookup"><span data-stu-id="7022d-215">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="test-resource-specific-consent"></a><span data-ttu-id="7022d-216">リソース固有の同意をテストする</span><span class="sxs-lookup"><span data-stu-id="7022d-216">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="7022d-217">**リソース固有の同意のアクセス許可をテストTeams**</span><span class="sxs-lookup"><span data-stu-id="7022d-217">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="7022d-218">管理者向けTeamsトピック</span><span class="sxs-lookup"><span data-stu-id="7022d-218">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7022d-219">**管理者向けリソース固有Microsoft Teams同意**</span><span class="sxs-lookup"><span data-stu-id="7022d-219">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 

