---
title: Teams でのリソース固有の同意
description: Teams でのリソース固有の同意と、その利点を活用する方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: teams authorization OAuth SSO AAD rsc Graph
ms.openlocfilehash: cbeb1069f7f80608ec3a65710543b429e6f2908b
ms.sourcegitcommit: f6029c8ff0c5315613a3efcd86777aa4cede39e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "48995024"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="7ddd9-104">リソース固有の同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="7ddd9-104">Resource-specific consent (RSC)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="7ddd9-105">エンドポイントでは、これらの Api にアクセスでき https://graph.microsoft.com/beta ます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-105">These APIs are accessible in the https://graph.microsoft.com/beta endpoint.</span></span>  <span data-ttu-id="7ddd9-106">[ベータバージョン](/graph/versioning-and-support#beta-version)エンドポイントには、現在プレビュー段階の api が含まれており、通常は使用できません。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-106">The [beta version](/graph/versioning-and-support#beta-version) endpoint includes APIs that are currently in preview and are not yet generally available.</span></span> <span data-ttu-id="7ddd9-107">ベータ版エンドポイントの Api は変更される可能性があり、運用アプリで使用することはお勧めしません。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-107">The APIs in the beta endpoint are subject to change and we don't recommend that you use them in your production apps.</span></span> 

<span data-ttu-id="7ddd9-108">リソース固有の同意 (RSC) は Microsoft Teams と Graph API の統合で、アプリが API エンドポイントを使用して組織内の特定のチームを管理できるようにします。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-108">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="7ddd9-109">リソース固有の同意 (RSC) アクセス許可モデルを使用すると、チームの *所有者* は、チームのデータにアクセスしたり、変更したりするアプリケーションに同意を与えることができます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-109">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="7ddd9-110">きめ細かい、Teams 固有、RSC の各アクセス許可によって、アプリケーションが特定のチーム内で実行できる処理を定義します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-110">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="7ddd9-111">リソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="7ddd9-111">Resource-specific permissions</span></span>

|<span data-ttu-id="7ddd9-112">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="7ddd9-112">Application permission</span></span>| <span data-ttu-id="7ddd9-113">アクション</span><span class="sxs-lookup"><span data-stu-id="7ddd9-113">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="7ddd9-114">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-114">TeamSettings.Read.Group</span></span> | <span data-ttu-id="7ddd9-115">このチームの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-115">Get the settings for this team.</span></span>|
|<span data-ttu-id="7ddd9-116">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-116">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="7ddd9-117">このチームの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-117">Update the settings for this team.</span></span>|
|<span data-ttu-id="7ddd9-118">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-118">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="7ddd9-119">このチームのチャネル名、チャネルの説明、およびチャネルの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-119">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="7ddd9-120">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-120">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="7ddd9-121">このチームのチャネル名、チャネルの説明、およびチャネルの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-121">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="7ddd9-122">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-122">Channel.Create.Group</span></span>|<span data-ttu-id="7ddd9-123">このチームのチャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-123">Create channels in this team.</span></span>|
|<span data-ttu-id="7ddd9-124">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-124">Channel.Delete.Group</span></span>|<span data-ttu-id="7ddd9-125">このチームのチャネルを削除します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-125">Delete channels in this team.</span></span>|
|<span data-ttu-id="7ddd9-126">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-126">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="7ddd9-127">このチームのチャネルメッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-127">Get this team's channel messages.</span></span>|
|<span data-ttu-id="7ddd9-128">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-128">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="7ddd9-129">このチームのインストール済みアプリのリストを取得します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-129">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="7ddd9-130">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-130">TeamsTab.Read.Group</span></span>|<span data-ttu-id="7ddd9-131">このチームのタブのリストを取得します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-131">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="7ddd9-132">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-132">TeamsTab.Create.Group</span></span>|<span data-ttu-id="7ddd9-133">このチームのタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-133">Create tabs in this team.</span></span>|
|<span data-ttu-id="7ddd9-134">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-134">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="7ddd9-135">このチームのタブを更新します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-135">Update this team's tabs.</span></span>|
|<span data-ttu-id="7ddd9-136">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-136">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="7ddd9-137">このチームのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-137">Delete this team's tabs.</span></span>|
|<span data-ttu-id="7ddd9-138">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="7ddd9-138">TeamMember.Read.Group</span></span>|<span data-ttu-id="7ddd9-139">このチームのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-139">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="7ddd9-140">リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリに対してのみ使用できます。現在、Azure Active Directory ポータルには含まれていません。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-140">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="7ddd9-141">アプリケーションでリソース固有の同意を有効にする</span><span class="sxs-lookup"><span data-stu-id="7ddd9-141">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="7ddd9-142">アプリケーションで RSC を有効にする手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-142">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="7ddd9-143">[Azure Active Directory ポータルでグループ所有者の同意設定を構成](#configure-group-owner-consent-settings-in-the-azure-ad-portal)します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-143">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="7ddd9-144">Azure AD ポータルを使用して、[アプリを Microsoft identity platform に登録](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-144">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. [<span data-ttu-id="7ddd9-145">Azure AD ポータルでアプリケーションのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="7ddd9-145">Review your application permissions in the Azure AD portal</span></span>](#review-your-application-permissions-in-the-azure-ad-portal)
1. <span data-ttu-id="7ddd9-146">[Microsoft Identity platform からアクセストークンを取得](#obtain-an-access-token-from-the-microsoft-identity-platform)します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-146">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="7ddd9-147">[Teams アプリマニフェストを更新](#update-your-teams-app-manifest)します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-147">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="7ddd9-148">[Teams にアプリを直接インストール](#install-your-app-directly-in-teams)します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-148">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="7ddd9-149">[アプリで RSC 権限が追加されているかどうかを確認](#check-your-app-for-added-rsc-permissions)します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-149">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="7ddd9-150">Azure AD ポータルでグループ所有者の同意設定を構成する</span><span class="sxs-lookup"><span data-stu-id="7ddd9-150">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="7ddd9-151">Azure portal で直接 [グループ所有者の同意](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) を有効または無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-151">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="7ddd9-152">[グローバル管理者または会社の管理者](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)として、 [Azure portal](https://portal.azure.com)にサインインします。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-152">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="7ddd9-153">[[](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory**  =>  **エンタープライズアプリケーション**  =>  の **同意とアクセス許可** ]  =>  **ユーザーの同意設定** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-153">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="7ddd9-154">[ **グループ所有者がデータにアクセスするためのアプリに対するグループ所有者の同意** を有効にする] (既定では、すべての **グループ所有者に対して [許可グループ所有者に同意** します)] というラベルが付けられます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-154">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners** ).</span></span> <span data-ttu-id="7ddd9-155">チーム所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-155">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![azure rsc 構成](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="7ddd9-157">PowerShell を使用して Azure portal でグループ所有者の同意を有効または無効にするには、「 [powershell を使用してグループ所有者の同意を構成](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)する」に記載されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-157">To enable or disable group owner consent within the Azure portal using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="7ddd9-158">Azure AD ポータルを使用してアプリを Microsoft identity platform に登録する</span><span class="sxs-lookup"><span data-stu-id="7ddd9-158">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="7ddd9-159">Azure Active Directory ポータルには、アプリを登録して構成するための一元的なプラットフォームが用意されています。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-159">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="7ddd9-160">アプリは、Microsoft identity platform および call Graph Api と統合するために、Azure AD ポータルに登録されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-160">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Graph APIs.</span></span> <span data-ttu-id="7ddd9-161">「 [Microsoft identity platform を使用してアプリケーションを登録する」を](/graph/auth-register-app-v2)*参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-161">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="7ddd9-162">複数の Teams アプリを同じ Azure AD アプリ id に登録しないでください。アプリ id は、アプリごとに一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-162">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="7ddd9-163">同じアプリ id に複数のアプリをインストールしようとすると失敗します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-163">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="7ddd9-164">Azure AD ポータルでアプリケーションのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="7ddd9-164">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="7ddd9-165">[ **ホーム**  =>  **アプリの登録** ] ページに移動して、RSC アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-165">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="7ddd9-166">左側のナビゲーションバーから [ **API アクセス許可** ] を選択し、アプリに対して構成されているアクセス許可の一覧を確認します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-166">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="7ddd9-167">アプリケーションが RSC Graph 呼び出しのみを行う場合は、そのページに対するすべてのアクセス許可を削除します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-167">If your app will only make RSC Graph calls, delete all the permission on that page.</span></span> <span data-ttu-id="7ddd9-168">アプリが非 RSC 呼び出しを行う場合は、必要に応じてそれらのアクセス許可を維持します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-168">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="7ddd9-169">Azure AD portal は、RSC のアクセス許可を要求するために使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-169">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="7ddd9-170">RSC のアクセス許可は、現在、Teams クライアントにインストールされ、アプリマニフェスト (JSON) ファイルで宣言されている Teams アプリケーションに対して排他的です。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-170">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="7ddd9-171">Microsoft identity platform からアクセストークンを取得する</span><span class="sxs-lookup"><span data-stu-id="7ddd9-171">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="7ddd9-172">Graph API の呼び出しを行うには、id プラットフォームからアプリのアクセストークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-172">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="7ddd9-173">アプリが Microsoft identity platform からトークンを取得する前に、Azure AD ポータルに登録されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-173">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="7ddd9-174">アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-174">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="7ddd9-175">Id プラットフォームからアクセストークンを取得するには、Azure AD 登録プロセスの次の値を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-175">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="7ddd9-176">アプリ登録ポータルによって割り当てられた **アプリケーション ID** 。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-176">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="7ddd9-177">アプリでシングルサインオン (SSO) がサポートされている場合は、アプリと SSO に対して同じアプリケーション ID を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-177">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="7ddd9-178">**クライアントシークレット/パスワード** 、または公開/秘密キーペア ( **証明書** )。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-178">The  **Client secret/password** or a public/private key pair ( **Certificate** ).</span></span> <span data-ttu-id="7ddd9-179">ネイティブ アプリの場合、これは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-179">This is not required for native apps.</span></span>
- <span data-ttu-id="7ddd9-180">Azure AD からの応答を受信するための、アプリの **リダイレクト URI** (または応答 URL)。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-180">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="7ddd9-181">ユーザー [の代理](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token)としてアクセスを取得し、 [ユーザーなしでアクセスを取得する](/graph/auth-v2-service)を *参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-181">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="7ddd9-182">Teams アプリマニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="7ddd9-182">Update your Teams app manifest</span></span>

<span data-ttu-id="7ddd9-183">RSC アクセス許可は、アプリマニフェスト (JSON) ファイルで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-183">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="7ddd9-184">次の値を使用して、 [Webapplicationinfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリのマニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-184">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="7ddd9-185">**id**  : azure ad アプリ Id。 *「* [azure ad ポータルでアプリを登録](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-185">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="7ddd9-186">**resource**  -任意の文字列。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-186">**resource**  — any string.</span></span> <span data-ttu-id="7ddd9-187">このフィールドは、RSC では操作を行いませんが、追加して、エラー応答が発生しないように値を設定する必要があります。任意の文字列が実行されます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-187">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="7ddd9-188">**アプリケーションのアクセス許可** -アプリの RSC アクセス許可。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-188">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="7ddd9-189">[リソース固有の権限](resource-specific-consent.md#resource-specific-permissions)を *参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-189">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="7ddd9-190">非 RSC アクセス許可は、Azure portal に格納されます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-190">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="7ddd9-191">アプリマニフェストに追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-191">Do not add them to the app manifest.</span></span>
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

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="7ddd9-192">Teams にアプリを直接インストールする</span><span class="sxs-lookup"><span data-stu-id="7ddd9-192">Install your app directly in Teams</span></span>

<span data-ttu-id="7ddd9-193">アプリを作成したら、 [アプリパッケージ](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) を特定のチームに直接アップロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-193">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="7ddd9-194">そのためには、カスタムアプリのセットアップポリシーの一部として、[ **カスタムアプリのアップロード** ] ポリシー設定を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-194">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="7ddd9-195">*「* [Custom App policy Settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-195">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="7ddd9-196">アプリで RSC 権限が追加されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="7ddd9-196">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="7ddd9-197">RSC のアクセス許可は、ユーザーには含まれません。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-197">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="7ddd9-198">呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可で行われます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-198">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="7ddd9-199">そのため、アプリは、チャネルの作成やタブの削除など、ユーザーができない操作を実行できる場合があります。RSC API 呼び出しを行う前に、ユースケースに対するチーム所有者の意図を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-199">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="7ddd9-200">*「* [Microsoft Teams API の概要](/graph/teams-concept-overview)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-200">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="7ddd9-201">アプリがチームにインストールされたら、 [Graph エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)  を使用して、チーム内のアプリに付与されているアクセス許可を表示できます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-201">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="7ddd9-202">Teams クライアントからチームの **groupId** を取得します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-202">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="7ddd9-203">Teams クライアントで、左端のナビゲーションバーにある [ **teams** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-203">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="7ddd9-204">アプリがインストールされているチームを、ドロップダウンメニューから選択します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-204">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="7ddd9-205">[ **その他のオプション** ] アイコン (&#8943;) を選択します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-205">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="7ddd9-206">[ **チームへのリンクの取得** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-206">Select **Get link to team**.</span></span>
> - <span data-ttu-id="7ddd9-207">文字列から **groupId** 値をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-207">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="7ddd9-208">**Graph エクスプローラー** にログインします。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-208">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="7ddd9-209">次のエンドポイントに対して **GET** を `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 呼び出します。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-209">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="7ddd9-210">応答の clientAppId フィールドは、Teams アプリマニフェストで指定されている appId にマップされます。</span><span class="sxs-lookup"><span data-stu-id="7ddd9-210">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="7ddd9-211">![通話を取得するための Graph エクスプローラーの応答。](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="7ddd9-211">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>
 
## <a name="test-resource-specific-consent"></a><span data-ttu-id="7ddd9-212">リソース固有の同意をテストする</span><span class="sxs-lookup"><span data-stu-id="7ddd9-212">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="7ddd9-213">**Teams でのリソース固有の同意権限をテストする**</span><span class="sxs-lookup"><span data-stu-id="7ddd9-213">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="7ddd9-214">Teams 管理者向けの関連トピック</span><span class="sxs-lookup"><span data-stu-id="7ddd9-214">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ddd9-215">**管理者のための Microsoft Teams でのリソース固有の同意**</span><span class="sxs-lookup"><span data-stu-id="7ddd9-215">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 
