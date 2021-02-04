---
title: Teams でのリソース固有の同意
description: Teams でのリソース固有の同意と、それを活用する方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: Teams 承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 1b5c0f645d93ed33c11bf3279e70133f35f53a2c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093930"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="b19fb-104">リソース固有の同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="b19fb-104">Resource-specific consent (RSC)</span></span>

<span data-ttu-id="b19fb-105">リソース固有の同意 (RSC) は、Microsoft Teams と Microsoft Graph API の統合であり、アプリで API エンドポイントを使用して組織内の特定のチームを管理できます。</span><span class="sxs-lookup"><span data-stu-id="b19fb-105">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="b19fb-106">リソース固有の同意 (RSC) アクセス許可モデルを使用すると、チーム所有者は、アプリケーションがチームのデータにアクセスしたり変更したりするための同意を付与できます。</span><span class="sxs-lookup"><span data-stu-id="b19fb-106">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="b19fb-107">詳細な Teams 固有の RSC アクセス許可は、アプリケーションが特定のチーム内で実行できる操作を定義します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-107">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="b19fb-108">リソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="b19fb-108">Resource-specific permissions</span></span>

|<span data-ttu-id="b19fb-109">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="b19fb-109">Application permission</span></span>| <span data-ttu-id="b19fb-110">操作</span><span class="sxs-lookup"><span data-stu-id="b19fb-110">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="b19fb-111">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-111">TeamSettings.Read.Group</span></span> | <span data-ttu-id="b19fb-112">このチームの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-112">Get the settings for this team.</span></span>|
|<span data-ttu-id="b19fb-113">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-113">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="b19fb-114">このチームの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-114">Update the settings for this team.</span></span>|
|<span data-ttu-id="b19fb-115">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-115">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="b19fb-116">このチームのチャネル名、チャネルの説明、チャネル設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-116">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="b19fb-117">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-117">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="b19fb-118">このチームのチャネル名、チャネルの説明、チャネル設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-118">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="b19fb-119">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-119">Channel.Create.Group</span></span>|<span data-ttu-id="b19fb-120">このチームのチャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-120">Create channels in this team.</span></span>|
|<span data-ttu-id="b19fb-121">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-121">Channel.Delete.Group</span></span>|<span data-ttu-id="b19fb-122">このチームのチャネルを削除します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-122">Delete channels in this team.</span></span>|
|<span data-ttu-id="b19fb-123">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-123">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="b19fb-124">このチームのチャネル メッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-124">Get this team's channel messages.</span></span>|
|<span data-ttu-id="b19fb-125">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-125">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="b19fb-126">このチームのインストール済みアプリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-126">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="b19fb-127">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-127">TeamsTab.Read.Group</span></span>|<span data-ttu-id="b19fb-128">このチームのタブの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-128">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="b19fb-129">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-129">TeamsTab.Create.Group</span></span>|<span data-ttu-id="b19fb-130">このチームのタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-130">Create tabs in this team.</span></span>|
|<span data-ttu-id="b19fb-131">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-131">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="b19fb-132">このチームのタブを更新します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-132">Update this team's tabs.</span></span>|
|<span data-ttu-id="b19fb-133">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-133">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="b19fb-134">このチームのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-134">Delete this team's tabs.</span></span>|
|<span data-ttu-id="b19fb-135">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="b19fb-135">TeamMember.Read.Group</span></span>|<span data-ttu-id="b19fb-136">このチームのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-136">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="b19fb-137">リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリでのみ使用できます。現在、Azure Active Directory ポータルには含められません。</span><span class="sxs-lookup"><span data-stu-id="b19fb-137">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="b19fb-138">アプリケーションでリソース固有の同意を有効にする</span><span class="sxs-lookup"><span data-stu-id="b19fb-138">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="b19fb-139">アプリケーションで RSC を有効にする手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b19fb-139">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="b19fb-140">[Azure Active Directory ポータルでグループ所有者の同意設定を構成します](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-140">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="b19fb-141">[Azure AD ポータルを使用して、Microsoft](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)ID プラットフォームにアプリを登録します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-141">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="b19fb-142">[Azure AD ポータルでアプリケーションのアクセス許可を確認します](#review-your-application-permissions-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-142">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="b19fb-143">[Microsoft Identity プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-143">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="b19fb-144">[Teams アプリ マニフェストを更新します](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-144">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="b19fb-145">[Teams に直接アプリをインストールします](#install-your-app-directly-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-145">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="b19fb-146">[RSC のアクセス許可が追加されていないかアプリを確認します](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-146">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="b19fb-147">Azure ポータルでグループ所有者の同意設定ADする</span><span class="sxs-lookup"><span data-stu-id="b19fb-147">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="b19fb-148">Azure Portal 内でグループ [所有者の同意を](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 直接有効または無効にできます。</span><span class="sxs-lookup"><span data-stu-id="b19fb-148">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="b19fb-149">グローバル管理者/ [会社管理者として Azure Portal](https://portal.azure.com) [にサインインします](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-149">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="b19fb-150">[[Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Active Directory Enterprise**  =>  **アプリケーションの同意とアクセス**  =>  **許可]** ユーザーの同意  =>  **設定を選択します**。</span><span class="sxs-lookup"><span data-stu-id="b19fb-150">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="b19fb-151">データにアクセスするアプリに対するグループ所有者の同意というラベルが付いたコントロールを使用して、ユーザーの同意を有効、無効、または制限します **(既定** では、すべてのグループ所有者に対するグループ所有者の同意 **を許可します**)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-151">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="b19fb-152">チーム所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b19fb-152">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![azure rsc の構成](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="b19fb-154">PowerShell を使用してグループ所有者の同意を有効または無効にするには、「PowerShell を使用してグループ所有者の同意を構成する」で説明 [されている手順に従います](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-154">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="b19fb-155">Azure AD ポータルを使用してアプリを Microsoft ID プラットフォームに登録する</span><span class="sxs-lookup"><span data-stu-id="b19fb-155">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="b19fb-156">Azure Active Directory ポータルは、アプリを登録および構成する中心的なプラットフォームを提供します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-156">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="b19fb-157">Microsoft ID プラットフォームと統合し、Microsoft Graph API を呼び出AD Azure AD ポータルにアプリを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b19fb-157">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="b19fb-158">*「Microsoft* [ID プラットフォームにアプリケーションを登録する」を参照してください](/graph/auth-register-app-v2)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-158">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="b19fb-159">複数の Teams アプリを同じ Azure アプリ id AD登録しない。アプリ ID は、アプリごとに一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="b19fb-159">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="b19fb-160">同じアプリ ID に複数のアプリをインストールしようとすると失敗します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-160">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="b19fb-161">Azure AD ポータルでアプリケーションのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="b19fb-161">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="b19fb-162">[ホーム アプリ **の**  =>  **登録] ページに移動し**、RSC アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-162">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="b19fb-163">左側 **のナビゲーション バーから API** のアクセス許可を選択し、アプリに対して構成されているアクセス許可の一覧を確認します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-163">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="b19fb-164">アプリで RSC Graph API 呼び出しのみを行う場合は、そのページのすべてのアクセス許可を削除します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-164">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="b19fb-165">アプリで RSC 以外の呼び出しも行う場合は、必要に応じてこれらのアクセス許可を保持します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-165">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b19fb-166">Azure AD ポータルを使用して RSC アクセス許可を要求することはできません。</span><span class="sxs-lookup"><span data-stu-id="b19fb-166">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="b19fb-167">RSC のアクセス許可は現在、Teams クライアントにインストールされている Teams アプリケーション専用であり、アプリ マニフェスト (JSON) ファイルで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="b19fb-167">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="b19fb-168">Microsoft ID プラットフォームからアクセス トークンを取得する</span><span class="sxs-lookup"><span data-stu-id="b19fb-168">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="b19fb-169">Graph API 呼び出しを行う場合は、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b19fb-169">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="b19fb-170">アプリが Microsoft ID プラットフォームからトークンを取得するには、その前に Azure AD ポータルに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b19fb-170">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="b19fb-171">アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。</span><span class="sxs-lookup"><span data-stu-id="b19fb-171">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="b19fb-172">ID プラットフォームからアクセス トークンを取得するには、Azure AD 登録プロセスから次の値を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b19fb-172">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="b19fb-173">アプリ **登録ポータルによって** 割り当てられたアプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="b19fb-173">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="b19fb-174">アプリでシングル サインオン (SSO) がサポートされている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b19fb-174">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="b19fb-175">クライアント  **シークレット/パスワード、** または公開/秘密キーのペア (**証明書**)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-175">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="b19fb-176">ネイティブ アプリの場合、これは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="b19fb-176">This is not required for native apps.</span></span>
- <span data-ttu-id="b19fb-177">Azure AD からの応答をアプリが受信するリダイレクト **URI** (または応答 URL)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-177">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="b19fb-178">*「ユーザー*[の代わりにアクセスを取得する」と「ユーザー](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)なしで [アクセスを取得する」を参照](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="b19fb-178">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="b19fb-179">Teams アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="b19fb-179">Update your Teams app manifest</span></span>

<span data-ttu-id="b19fb-180">RSC アクセス許可は、アプリ マニフェスト (JSON) ファイルで宣言されます。</span><span class="sxs-lookup"><span data-stu-id="b19fb-180">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="b19fb-181">次の [値を使用して、webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-181">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="b19fb-182">**id** — Azure ADアプリ ID。Azure AD ポータルにアプリ [を登録するを参照してください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-182">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="b19fb-183">**resource**  — 任意の文字列。</span><span class="sxs-lookup"><span data-stu-id="b19fb-183">**resource**  — any string.</span></span> <span data-ttu-id="b19fb-184">このフィールドは RSC では操作されませんが、エラー応答を回避するために値を追加する必要があります。任意の文字列で実行されます。</span><span class="sxs-lookup"><span data-stu-id="b19fb-184">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="b19fb-185">**アプリケーションのアクセス許可** — アプリの RSC アクセス許可。</span><span class="sxs-lookup"><span data-stu-id="b19fb-185">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="b19fb-186">*「リソース*[固有のアクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-186">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="b19fb-187">RSC 以外のアクセス許可は Azure portal に保存されます。</span><span class="sxs-lookup"><span data-stu-id="b19fb-187">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="b19fb-188">アプリ マニフェストに追加しません。</span><span class="sxs-lookup"><span data-stu-id="b19fb-188">Do not add them to the app manifest.</span></span>
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

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="b19fb-189">Teams に直接アプリをインストールする</span><span class="sxs-lookup"><span data-stu-id="b19fb-189">Install your app directly in Teams</span></span>

<span data-ttu-id="b19fb-190">アプリを作成したら、アプリ パッケージを特定の [チームに直接](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) アップロードできます。</span><span class="sxs-lookup"><span data-stu-id="b19fb-190">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="b19fb-191">これを行うには、カスタム アプリ **セットアップ** ポリシーの一部として [カスタム アプリのアップロード] ポリシー設定を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b19fb-191">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="b19fb-192">*「カスタム*[アプリ ポリシー設定」をご覧ください](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-192">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="b19fb-193">RSC のアクセス許可が追加されていないかアプリを確認する</span><span class="sxs-lookup"><span data-stu-id="b19fb-193">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="b19fb-194">RSC アクセス許可はユーザーに属性付けされません。</span><span class="sxs-lookup"><span data-stu-id="b19fb-194">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="b19fb-195">呼び出しは、ユーザーによって委任されたアクセス許可ではなく、アプリのアクセス許可で行います。</span><span class="sxs-lookup"><span data-stu-id="b19fb-195">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="b19fb-196">したがって、チャネルの作成やタブの削除など、ユーザーが実行できない操作をアプリで実行できる場合があります。RSC API 呼び出しを行う前に、チーム所有者の使用事例の意図を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b19fb-196">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="b19fb-197">*Microsoft* [Teams API の概要を参照してください](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-197">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="b19fb-198">アプリがチームにインストールされた後 [、Graph エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)  を使用して、チーム内のアプリに付与されているアクセス許可を表示できます。</span><span class="sxs-lookup"><span data-stu-id="b19fb-198">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="b19fb-199">Teams クライアントからチーム **の groupId** を取得します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-199">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="b19fb-200">Teams クライアントで、一 **方** の左側のナビゲーション バーから Teams を選択します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-200">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="b19fb-201">アプリがインストールされているチームをドロップダウン メニューから選択します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-201">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="b19fb-202">[その他 **のオプション]** アイコン (&#8943;)。</span><span class="sxs-lookup"><span data-stu-id="b19fb-202">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="b19fb-203">[チーム **へのリンクを取得する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="b19fb-203">Select **Get link to team**.</span></span>
> - <span data-ttu-id="b19fb-204">文字列から **groupId 値をコピー** して保存します。</span><span class="sxs-lookup"><span data-stu-id="b19fb-204">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="b19fb-205">Graph エクスプローラー **にログインします**。</span><span class="sxs-lookup"><span data-stu-id="b19fb-205">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="b19fb-206">次の **エンドポイントに対** して GET 呼び出しを行います `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 。</span><span class="sxs-lookup"><span data-stu-id="b19fb-206">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="b19fb-207">応答の clientAppId フィールドは、Teams アプリ マニフェストで指定された appId にマップされます。</span><span class="sxs-lookup"><span data-stu-id="b19fb-207">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="b19fb-208">![GET 呼び出しに対する Graph エクスプローラーの応答。](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="b19fb-208">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>
 
## <a name="test-resource-specific-consent"></a><span data-ttu-id="b19fb-209">リソース固有の同意をテストする</span><span class="sxs-lookup"><span data-stu-id="b19fb-209">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="b19fb-210">**Teams でリソース固有の同意のアクセス許可をテストする**</span><span class="sxs-lookup"><span data-stu-id="b19fb-210">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="b19fb-211">Teams 管理者向け関連トピック</span><span class="sxs-lookup"><span data-stu-id="b19fb-211">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b19fb-212">**管理者向け Microsoft Teams でのリソース固有の同意**</span><span class="sxs-lookup"><span data-stu-id="b19fb-212">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 
