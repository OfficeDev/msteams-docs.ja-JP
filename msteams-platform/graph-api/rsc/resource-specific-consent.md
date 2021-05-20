---
title: Teamsにおけるリソース固有の同意
description: Teamsでのリソース固有の同意と、その利点を活かす方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: チーム承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: dabe0c33013fbb398eee7bf00ac2881cd86e6bc5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566133"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="638d7-104">リソース固有の同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="638d7-104">Resource-specific consent (RSC)</span></span>

<span data-ttu-id="638d7-105">リソース固有の同意 (RSC) は、アプリが API エンドポイントを使用して組織内の特定のチームを管理できるようにするMicrosoft Teamsと Microsoft Graph API 統合です。</span><span class="sxs-lookup"><span data-stu-id="638d7-105">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="638d7-106">リソース固有の同意 (RSC) のアクセス許可モデルを使用すると、 *チームの所有者* は、チームのデータにアクセスしたり、チームのデータを変更したりするための同意を付与できます。</span><span class="sxs-lookup"><span data-stu-id="638d7-106">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="638d7-107">詳細なTeams固有の RSC アクセス許可は、アプリケーションが特定のチーム内で実行できる操作を定義します。</span><span class="sxs-lookup"><span data-stu-id="638d7-107">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="638d7-108">リソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="638d7-108">Resource-specific permissions</span></span>

|<span data-ttu-id="638d7-109">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="638d7-109">Application permission</span></span>| <span data-ttu-id="638d7-110">Action</span><span class="sxs-lookup"><span data-stu-id="638d7-110">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="638d7-111">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-111">TeamSettings.Read.Group</span></span> | <span data-ttu-id="638d7-112">このチームの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="638d7-112">Get the settings for this team.</span></span>|
|<span data-ttu-id="638d7-113">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-113">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="638d7-114">このチームの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="638d7-114">Update the settings for this team.</span></span>|
|<span data-ttu-id="638d7-115">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-115">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="638d7-116">このチームのチャネル名、チャネルの説明、およびチャネル設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="638d7-116">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="638d7-117">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-117">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="638d7-118">このチームのチャネル名、チャネルの説明、およびチャネル設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="638d7-118">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="638d7-119">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-119">Channel.Create.Group</span></span>|<span data-ttu-id="638d7-120">このチームのチャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="638d7-120">Create channels in this team.</span></span>|
|<span data-ttu-id="638d7-121">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-121">Channel.Delete.Group</span></span>|<span data-ttu-id="638d7-122">このチームのチャンネルを削除します。</span><span class="sxs-lookup"><span data-stu-id="638d7-122">Delete channels in this team.</span></span>|
|<span data-ttu-id="638d7-123">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-123">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="638d7-124">このチームのチャンネルメッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="638d7-124">Get this team's channel messages.</span></span>|
|<span data-ttu-id="638d7-125">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-125">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="638d7-126">このチームがインストールしたアプリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="638d7-126">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="638d7-127">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-127">TeamsTab.Read.Group</span></span>|<span data-ttu-id="638d7-128">このチームのタブのリストを取得します。</span><span class="sxs-lookup"><span data-stu-id="638d7-128">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="638d7-129">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-129">TeamsTab.Create.Group</span></span>|<span data-ttu-id="638d7-130">このチームのタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="638d7-130">Create tabs in this team.</span></span>|
|<span data-ttu-id="638d7-131">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-131">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="638d7-132">このチームのタブを更新します。</span><span class="sxs-lookup"><span data-stu-id="638d7-132">Update this team's tabs.</span></span>|
|<span data-ttu-id="638d7-133">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-133">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="638d7-134">このチームのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="638d7-134">Delete this team's tabs.</span></span>|
|<span data-ttu-id="638d7-135">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="638d7-135">TeamMember.Read.Group</span></span>|<span data-ttu-id="638d7-136">このチームのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="638d7-136">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="638d7-137">リソース固有のアクセス許可は、Teams クライアントにインストールされているTeamsアプリでのみ使用でき、現在はAzure Active Directory ポータルには含まれていません。</span><span class="sxs-lookup"><span data-stu-id="638d7-137">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="638d7-138">アプリケーションでリソース固有の同意を有効にする</span><span class="sxs-lookup"><span data-stu-id="638d7-138">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="638d7-139">アプリケーションで RSC を有効にする手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="638d7-139">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="638d7-140">[Azure Active Directory ポータル でグループ所有者の同意設定を構成](#configure-group-owner-consent-settings-in-the-azure-ad-portal)する 。</span><span class="sxs-lookup"><span data-stu-id="638d7-140">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="638d7-141">[Azure AD ポータル を介して Microsoft ID プラットフォーム にアプリを登録](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)します。</span><span class="sxs-lookup"><span data-stu-id="638d7-141">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="638d7-142">[Azure AD ポータル でアプリケーションのアクセス許可を確認](#review-your-application-permissions-in-the-azure-ad-portal)します。</span><span class="sxs-lookup"><span data-stu-id="638d7-142">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="638d7-143">[Microsoft ID プラットフォームからアクセス トークンを取得](#obtain-an-access-token-from-the-microsoft-identity-platform)する 。</span><span class="sxs-lookup"><span data-stu-id="638d7-143">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="638d7-144">[Teams アプリ マニフェストを更新](#update-your-teams-app-manifest)する 。</span><span class="sxs-lookup"><span data-stu-id="638d7-144">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="638d7-145">[アプリを Teams に直接インストールします](#sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="638d7-145">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="638d7-146">[追加された RSC 権限のアプリを確認](#check-your-app-for-added-rsc-permissions)します。</span><span class="sxs-lookup"><span data-stu-id="638d7-146">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="638d7-147">Azure AD ポータルでグループ所有者の同意の設定を構成する</span><span class="sxs-lookup"><span data-stu-id="638d7-147">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="638d7-148">[グループ所有者の同意](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal)を Azure ポータル内で直接有効または無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="638d7-148">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="638d7-149">[グローバル管理者または会社管理者](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)として[Azure ポータル](https://portal.azure.com)にサインインします。</span><span class="sxs-lookup"><span data-stu-id="638d7-149">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="638d7-150">[[](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)**アプリケーション Azure Active Directory Enterprise同意**  =>    =>  **とアクセス許可**  =>  **] [ユーザーの同意の設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="638d7-150">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="638d7-151">[グループ所有者の同意] というラベルの付いたコントロールで、 **データにアクセスするアプリのユーザーの同意を** 有効、無効、または制限します (既定では **、すべてのグループ所有者に対するグループ所有者の同意を許可** します)。</span><span class="sxs-lookup"><span data-stu-id="638d7-151">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="638d7-152">チーム所有者が RSC を使用してアプリをインストールするには、そのユーザーのグループ所有者の同意を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="638d7-152">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![azure rsc 構成](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="638d7-154">PowerShell を使用してグループ所有者の同意を有効または無効にするには [、「PowerShell を使用してグループ所有者の同意を構成する](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)」で説明されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="638d7-154">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="638d7-155">Azure AD ポータル経由でアプリをMicrosoft ID プラットフォームに登録する</span><span class="sxs-lookup"><span data-stu-id="638d7-155">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="638d7-156">Azure Active Directory ポータルは、アプリを登録および構成するための中央プラットフォームを提供します。</span><span class="sxs-lookup"><span data-stu-id="638d7-156">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="638d7-157">アプリを Azure AD ポータルに登録して、Microsoft ID プラットフォームと統合し、Microsoft Graph API を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="638d7-157">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="638d7-158">詳細については、「[アプリケーションの Microsoft ID プラットフォーム への登録](/graph/auth-register-app-v2)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="638d7-158">For more information, see [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="638d7-159">同じ Azure AD アプリ ID に複数のTeamsアプリを登録しないでください。アプリ ID は、アプリごとに一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="638d7-159">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="638d7-160">同じアプリ ID に複数のアプリをインストールしようとすると失敗します。</span><span class="sxs-lookup"><span data-stu-id="638d7-160">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="638d7-161">Azure AD ポータルでアプリケーションのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="638d7-161">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="638d7-162">**[ホーム**  =>  **アプリの登録**] ページに移動し、RSC アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="638d7-162">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="638d7-163">左側のナビゲーション バーから **[API のアクセス許可** ] を選択し、アプリに構成されているアクセス許可の一覧を確認します。</span><span class="sxs-lookup"><span data-stu-id="638d7-163">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="638d7-164">アプリが RSC Graph API 呼び出しのみを行う場合は、そのページのすべてのアクセス許可を削除します。</span><span class="sxs-lookup"><span data-stu-id="638d7-164">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="638d7-165">アプリが RSC 以外の呼び出しを行う場合は、必要に応じてアクセス許可を保持します。</span><span class="sxs-lookup"><span data-stu-id="638d7-165">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="638d7-166">Azure AD ポータルを使用して RSC アクセス許可を要求することはできません。</span><span class="sxs-lookup"><span data-stu-id="638d7-166">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="638d7-167">RSC のアクセス許可は、現在、Teams クライアントにインストールされているアプリケーションTeams排他的であり、アプリ マニフェスト (JSON) ファイルで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="638d7-167">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="638d7-168">Microsoft ID プラットフォームからアクセス トークンを取得する</span><span class="sxs-lookup"><span data-stu-id="638d7-168">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="638d7-169">API 呼び出しGraphするには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="638d7-169">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="638d7-170">アプリがMicrosoft ID プラットフォームからトークンを取得するには、Azure AD ポータルに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="638d7-170">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="638d7-171">アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。</span><span class="sxs-lookup"><span data-stu-id="638d7-171">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="638d7-172">ID プラットフォームからアクセス トークンを取得するには、Azure AD 登録プロセスから次の値を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="638d7-172">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="638d7-173">アプリ登録ポータルによって割り当てられたアプリケーション **ID。**</span><span class="sxs-lookup"><span data-stu-id="638d7-173">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="638d7-174">アプリがシングル サインオン (SSO) をサポートしている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="638d7-174">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="638d7-175">**クライアント シークレットとパスワード**、または公開キーと秘密キーのペア (**証明書**)</span><span class="sxs-lookup"><span data-stu-id="638d7-175">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="638d7-176">ネイティブ アプリの場合、これは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="638d7-176">This is not required for native apps.</span></span>
- <span data-ttu-id="638d7-177">Azure AD からの応答を受信するアプリの **リダイレクト URI** (または応答 URL)。</span><span class="sxs-lookup"><span data-stu-id="638d7-177">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="638d7-178">[「ユーザーの代わりにアクセスを取得する](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)」および「[ユーザーなしでアクセスを取得する」を](/graph/auth-v2-service)*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="638d7-178">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="638d7-179">Teams アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="638d7-179">Update your Teams app manifest</span></span>

<span data-ttu-id="638d7-180">RSC のアクセス許可は、アプリ マニフェスト (JSON) ファイルで宣言されます。</span><span class="sxs-lookup"><span data-stu-id="638d7-180">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="638d7-181">次の値を使用して、アプリ マニフェストに [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーを追加します。</span><span class="sxs-lookup"><span data-stu-id="638d7-181">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="638d7-182">**id**  — Azure AD アプリ ID。詳細については [、「Azure AD ポータルでのアプリの登録](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="638d7-182">**id**  — your Azure AD app id. For more information, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="638d7-183">**リソース**  — 任意の文字列。</span><span class="sxs-lookup"><span data-stu-id="638d7-183">**resource**  — any string.</span></span> <span data-ttu-id="638d7-184">このフィールドには RSC に操作はありませんが、エラー応答を避けるために値を追加し、値を指定する必要があります。任意の文字列が実行されます。</span><span class="sxs-lookup"><span data-stu-id="638d7-184">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="638d7-185">**アプリケーションのアクセス許可** — アプリの RSC アクセス許可。</span><span class="sxs-lookup"><span data-stu-id="638d7-185">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="638d7-186">詳細については、「 [リソース固有のアクセス許可](resource-specific-consent.md#resource-specific-permissions)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="638d7-186">For more information, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="638d7-187">RSC 以外のアクセス許可は、Azure ポータルに格納されます。</span><span class="sxs-lookup"><span data-stu-id="638d7-187">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="638d7-188">アプリ マニフェストに追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="638d7-188">Do not add them to the app manifest.</span></span>
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

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="638d7-189">Teamsでアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="638d7-189">Sideload your app in Teams</span></span>

<span data-ttu-id="638d7-190">管理者Teamsカスタム アプリのアップロードを許可している場合は、特定のチームに直接[アプリをサイドロード](~/concepts/deploy-and-publish/apps-upload.md)できます。</span><span class="sxs-lookup"><span data-stu-id="638d7-190">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="638d7-191">追加された RSC 権限のアプリを確認する</span><span class="sxs-lookup"><span data-stu-id="638d7-191">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="638d7-192">RSC 権限はユーザーに帰属しません。</span><span class="sxs-lookup"><span data-stu-id="638d7-192">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="638d7-193">呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可を使用して行われます。</span><span class="sxs-lookup"><span data-stu-id="638d7-193">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="638d7-194">したがって、アプリでは、チャネルの作成やタブの削除など、ユーザーが実行できないアクションを実行できる場合があります。RSC API 呼び出しを行う前に、ユース ケースに対するチーム所有者の意図を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="638d7-194">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="638d7-195">詳細については[、「API の概要Microsoft Teams」](/graph/teams-concept-overview)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="638d7-195">For more information, see [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="638d7-196">アプリをチームにインストールしたら[、Graph エクスプローラーを](https://developer.microsoft.com/graph/graph-explorer)使用して、チーム内のアプリに付与されているアクセス許可を表示できます。</span><span class="sxs-lookup"><span data-stu-id="638d7-196">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="638d7-197">Teamsクライアントからチームの **groupId** を取得します。</span><span class="sxs-lookup"><span data-stu-id="638d7-197">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="638d7-198">Teamsクライアントで、左端のナビゲーション バーから **Teams** を選択します。</span><span class="sxs-lookup"><span data-stu-id="638d7-198">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="638d7-199">ドロップダウン メニューからアプリがインストールされているチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="638d7-199">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="638d7-200">[ **その他のオプション]** アイコン(&#8943;)を選択します。</span><span class="sxs-lookup"><span data-stu-id="638d7-200">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="638d7-201">[ **チームへのリンクを取得]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="638d7-201">Select **Get link to team**.</span></span>
> - <span data-ttu-id="638d7-202">文字列から **groupId** 値をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="638d7-202">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="638d7-203">**エクスプローラにログインGraph。**</span><span class="sxs-lookup"><span data-stu-id="638d7-203">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="638d7-204">次のエンドポイントに **GET** 呼び出しを行います `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 。</span><span class="sxs-lookup"><span data-stu-id="638d7-204">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="638d7-205">応答の clientAppId フィールドは、Teams アプリ マニフェストで指定された appId にマップされます。</span><span class="sxs-lookup"><span data-stu-id="638d7-205">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="638d7-206">![GET 呼び出しに対するGraphの応答。](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="638d7-206">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="638d7-207">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="638d7-207">Code sample</span></span>
| <span data-ttu-id="638d7-208">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="638d7-208">**Sample name**</span></span> | <span data-ttu-id="638d7-209">**説明**</span><span class="sxs-lookup"><span data-stu-id="638d7-209">**Description**</span></span> | <span data-ttu-id="638d7-210">**.NET**</span><span class="sxs-lookup"><span data-stu-id="638d7-210">**.NET**</span></span> |<span data-ttu-id="638d7-211">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="638d7-211">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="638d7-212">リソース固有の同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="638d7-212">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="638d7-213">RSC を使用して api を呼び出Graph。</span><span class="sxs-lookup"><span data-stu-id="638d7-213">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="638d7-214">View</span><span class="sxs-lookup"><span data-stu-id="638d7-214">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="638d7-215">View</span><span class="sxs-lookup"><span data-stu-id="638d7-215">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a><span data-ttu-id="638d7-216">関連項目</span><span class="sxs-lookup"><span data-stu-id="638d7-216">See also</span></span>
 
* [<span data-ttu-id="638d7-217">Teamsでリソース固有の同意アクセス許可をテストする</span><span class="sxs-lookup"><span data-stu-id="638d7-217">Test resource-specific consent permissions in Teams</span></span>](test-resource-specific-consent.md)
* [<span data-ttu-id="638d7-218">管理者のMicrosoft Teamsでのリソース固有の同意</span><span class="sxs-lookup"><span data-stu-id="638d7-218">Resource-specific consent in Microsoft Teams for admins</span></span>](/MicrosoftTeams/resource-specific-consent)


