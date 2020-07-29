---
title: Teams でのリソース固有の同意
description: Teams でのリソース固有の同意と、その利点を活用する方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams authorization OAuth SSO AAD rsc Graph
ms.openlocfilehash: bf449b338e8c0f42dfef776e533fb6b5ff591529
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434504"
---
# <a name="resource-specific-consent-rsc--developer-preview"></a><span data-ttu-id="da927-104">リソース固有の同意 (RSC)-開発者プレビュー</span><span class="sxs-lookup"><span data-stu-id="da927-104">Resource-specific consent (RSC) — Developer Preview</span></span>

>[!NOTE]

><span data-ttu-id="da927-105">開発者プレビューが有効になっている場合、リソース固有の同意アクセス許可は、デスクトップおよび web クライアントで使用できます。</span><span class="sxs-lookup"><span data-stu-id="da927-105">The resource-specific consent permissions are available in desktop and web clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="da927-106">詳細については、「[開発者プレビューを有効にする方法](../../resources/dev-preview/developer-preview-intro.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da927-106">See [How do I enable Developer Preview](../../resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

<span data-ttu-id="da927-107">リソース固有の同意 (RSC) は Microsoft Teams と Graph API の統合で、アプリが API エンドポイントを使用して組織内の特定のチームを管理できるようにします。</span><span class="sxs-lookup"><span data-stu-id="da927-107">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="da927-108">リソース固有の同意 (RSC) アクセス許可モデルを使用すると、チームの*所有者*は、チームのデータにアクセスしたり、変更したりするアプリケーションに同意を与えることができます。</span><span class="sxs-lookup"><span data-stu-id="da927-108">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="da927-109">きめ細かい、Teams 固有、RSC の各アクセス許可によって、アプリケーションが特定のチーム内で実行できる処理を定義します。</span><span class="sxs-lookup"><span data-stu-id="da927-109">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="da927-110">リソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="da927-110">Resource-specific permissions</span></span>

|<span data-ttu-id="da927-111">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="da927-111">Application permission</span></span>| <span data-ttu-id="da927-112">アクション</span><span class="sxs-lookup"><span data-stu-id="da927-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="da927-113">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="da927-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="da927-114">このチームの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="da927-114">Get the settings for this team.</span></span>|
|<span data-ttu-id="da927-115">TeamSettings. グループ</span><span class="sxs-lookup"><span data-stu-id="da927-115">TeamSettings.Edit.Group</span></span>|<span data-ttu-id="da927-116">このチームの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="da927-116">Update the settings for this team.</span></span>|
|<span data-ttu-id="da927-117">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="da927-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="da927-118">このチームのチャネル名、チャネルの説明、およびチャネルの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="da927-118">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="da927-119">ChannelSettings.Edit.Group</span><span class="sxs-lookup"><span data-stu-id="da927-119">ChannelSettings.Edit.Group</span></span>|<span data-ttu-id="da927-120">このチームのチャネル名、チャネルの説明、およびチャネルの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="da927-120">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="da927-121">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="da927-121">Channel.Create.Group</span></span>|<span data-ttu-id="da927-122">このチームのチャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="da927-122">Create channels in this team.</span></span>|
|<span data-ttu-id="da927-123">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="da927-123">Channel.Delete.Group</span></span>|<span data-ttu-id="da927-124">このチームのチャネルを削除します。</span><span class="sxs-lookup"><span data-stu-id="da927-124">Delete channels in this team.</span></span>|
|<span data-ttu-id="da927-125">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="da927-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="da927-126">このチームのチャネルメッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="da927-126">Get this team's channel messages.</span></span>|
|<span data-ttu-id="da927-127">TeamsApp.Read.Group</span><span class="sxs-lookup"><span data-stu-id="da927-127">TeamsApp.Read.Group</span></span>|<span data-ttu-id="da927-128">このチームのインストール済みアプリのリストを取得します。</span><span class="sxs-lookup"><span data-stu-id="da927-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="da927-129">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="da927-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="da927-130">このチームのタブのリストを取得します。</span><span class="sxs-lookup"><span data-stu-id="da927-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="da927-131">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="da927-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="da927-132">このチームのタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="da927-132">Create tabs in this team.</span></span>|
|<span data-ttu-id="da927-133">TeamsTab.Edit.Group</span><span class="sxs-lookup"><span data-stu-id="da927-133">TeamsTab.Edit.Group</span></span>|<span data-ttu-id="da927-134">このチームのタブを更新します。</span><span class="sxs-lookup"><span data-stu-id="da927-134">Update this team's tabs.</span></span>|
|<span data-ttu-id="da927-135">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="da927-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="da927-136">このチームのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="da927-136">Delete this team's tabs.</span></span>|
|<span data-ttu-id="da927-137">Member.Read.Group</span><span class="sxs-lookup"><span data-stu-id="da927-137">Member.Read.Group</span></span>|<span data-ttu-id="da927-138">このチームのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="da927-138">Get this team's members.</span></span>|
|<span data-ttu-id="da927-139">Owner.Read.Group</span><span class="sxs-lookup"><span data-stu-id="da927-139">Owner.Read.Group</span></span>|<span data-ttu-id="da927-140">このチームの所有者を取得します。</span><span class="sxs-lookup"><span data-stu-id="da927-140">Get this team's owners.</span></span>|

>[!NOTE]
><span data-ttu-id="da927-141">リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリに対してのみ使用できます。現在、Azure Active Directory ポータルには含まれていません。</span><span class="sxs-lookup"><span data-stu-id="da927-141">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="da927-142">アプリケーションでリソース固有の同意を有効にする</span><span class="sxs-lookup"><span data-stu-id="da927-142">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="da927-143">アプリケーションで RSC を有効にする手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="da927-143">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="da927-144">[Azure Active Directory ポータルでグループ所有者の同意設定を構成](#configure-group-owner-consent-settings-in-the-azure-ad-portal)します。</span><span class="sxs-lookup"><span data-stu-id="da927-144">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="da927-145">Azure AD ポータルを使用して、[アプリを Microsoft identity platform に登録](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)します。</span><span class="sxs-lookup"><span data-stu-id="da927-145">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. [<span data-ttu-id="da927-146">Azure AD ポータルでアプリケーションのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="da927-146">Review your application permissions in the Azure AD portal</span></span>](#review-your-application-permissions-in-the-azure-ad-portal)
1. <span data-ttu-id="da927-147">[Microsoft Identity platform からアクセストークンを取得](#obtain-an-access-token-from-the-microsoft-identity-platform)します。</span><span class="sxs-lookup"><span data-stu-id="da927-147">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="da927-148">[Teams アプリマニフェストを更新](#update-your-teams-app-manifest)します。</span><span class="sxs-lookup"><span data-stu-id="da927-148">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="da927-149">[Teams にアプリを直接インストール](#install-your-app-directly-in-teams)します。</span><span class="sxs-lookup"><span data-stu-id="da927-149">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="da927-150">[アプリで RSC 権限が追加されているかどうかを確認](#check-your-app-for-added-rsc-permissions)します。</span><span class="sxs-lookup"><span data-stu-id="da927-150">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="da927-151">Azure AD ポータルでグループ所有者の同意設定を構成する</span><span class="sxs-lookup"><span data-stu-id="da927-151">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="da927-152">Azure portal で直接[グループ所有者の同意](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data)を有効または無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="da927-152">You can enable or disable  [group owner consent](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="da927-153">[グローバル管理者または会社の管理者](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)として、 [Azure portal](https://portal.azure.com)にサインインします。</span><span class="sxs-lookup"><span data-stu-id="da927-153">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="da927-154">[ **Azure Active Directory**  => **エンタープライズアプリケーション**  => **ユーザー設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="da927-154">Select **Azure Active Directory** =>**Enterprise applications** =>**User settings**.</span></span>
> - <span data-ttu-id="da927-155">ユーザー**が所有するグループ**(この機能は既定で有効になっています) というラベルの付いたコントロールでユーザーの同意を有効化、無効化、または制限します。</span><span class="sxs-lookup"><span data-stu-id="da927-155">Enable, disable, or limit user consent with the control labeled **Users can consent to apps accessing company data for the groups they own** (This capability is enabled by default).</span></span>

![azure rsc 構成](../../assets/images/azure-rsc-configuration.svg)

| <span data-ttu-id="da927-157">値</span><span class="sxs-lookup"><span data-stu-id="da927-157">Value</span></span> | <span data-ttu-id="da927-158">説明</span><span class="sxs-lookup"><span data-stu-id="da927-158">Description</span></span>|
|--- | --- |
|<span data-ttu-id="da927-159">はい</span><span class="sxs-lookup"><span data-stu-id="da927-159">Yes</span></span> | <span data-ttu-id="da927-160">すべてのグループ所有者に対してグループ固有の同意を有効にします。</span><span class="sxs-lookup"><span data-stu-id="da927-160">Enable group-specific consent for all group owners.</span></span>|
|<span data-ttu-id="da927-161">いいえ</span><span class="sxs-lookup"><span data-stu-id="da927-161">No</span></span> |<span data-ttu-id="da927-162">すべてのユーザーのグループ固有の同意を無効にします。</span><span class="sxs-lookup"><span data-stu-id="da927-162">Disable group-specific consent for all users.</span></span>| 
|<span data-ttu-id="da927-163">いう</span><span class="sxs-lookup"><span data-stu-id="da927-163">Limited</span></span> | <span data-ttu-id="da927-164">選択したグループのメンバーのグループ固有の同意を有効にします。</span><span class="sxs-lookup"><span data-stu-id="da927-164">Enable group-specific consent for members of a selected group.</span></span>|

<span data-ttu-id="da927-165">PowerShell を使用して Azure portal でグループ所有者の同意を有効または無効にするには、「 [powershell を使用してグループ所有者の同意を構成](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)する」に記載されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="da927-165">To enable or disable group owner consent within the Azure portal using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="da927-166">Azure AD ポータルを使用してアプリを Microsoft identity platform に登録する</span><span class="sxs-lookup"><span data-stu-id="da927-166">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="da927-167">Azure Active Directory ポータルには、アプリを登録して構成するための一元的なプラットフォームが用意されています。</span><span class="sxs-lookup"><span data-stu-id="da927-167">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="da927-168">アプリは、Microsoft identity platform および call Graph Api と統合するために、Azure AD ポータルに登録されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="da927-168">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Graph APIs.</span></span> <span data-ttu-id="da927-169">「 [Microsoft identity platform を使用してアプリケーションを登録する」を](/graph/auth-register-app-v2)*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="da927-169">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="da927-170">複数の Teams アプリを同じ Azure AD アプリ id に登録しないでください。アプリ id は、アプリごとに一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="da927-170">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="da927-171">同じアプリ id に複数のアプリをインストールしようとすると失敗します。</span><span class="sxs-lookup"><span data-stu-id="da927-171">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="da927-172">Azure AD ポータルでアプリケーションのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="da927-172">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="da927-173">[**ホーム**  =>  **アプリの登録**] ページに移動して、RSC アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="da927-173">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="da927-174">左側のナビゲーションバーから [ **API アクセス許可**] を選択し、アプリに対して構成されているアクセス許可の一覧を確認します。</span><span class="sxs-lookup"><span data-stu-id="da927-174">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="da927-175">アプリケーションが RSC Graph 呼び出しのみを行う場合は、そのページに対するすべてのアクセス許可を削除します。</span><span class="sxs-lookup"><span data-stu-id="da927-175">If your app will only make RSC Graph calls, delete all the permission on that page.</span></span> <span data-ttu-id="da927-176">アプリが非 RSC 呼び出しを行う場合は、必要に応じてそれらのアクセス許可を維持します。</span><span class="sxs-lookup"><span data-stu-id="da927-176">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="da927-177">Azure AD portal は、RSC のアクセス許可を要求するために使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="da927-177">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="da927-178">RSC のアクセス許可は、現在、Teams クライアントにインストールされ、アプリマニフェスト (JSON) ファイルで宣言されている Teams アプリケーションに対して排他的です。</span><span class="sxs-lookup"><span data-stu-id="da927-178">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="da927-179">Microsoft identity platform からアクセストークンを取得する</span><span class="sxs-lookup"><span data-stu-id="da927-179">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="da927-180">Graph API の呼び出しを行うには、id プラットフォームからアプリのアクセストークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="da927-180">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="da927-181">アプリが Microsoft identity platform からトークンを取得する前に、Azure AD ポータルに登録されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="da927-181">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="da927-182">アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。</span><span class="sxs-lookup"><span data-stu-id="da927-182">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="da927-183">Id プラットフォームからアクセストークンを取得するには、Azure AD 登録プロセスの次の値を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="da927-183">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="da927-184">アプリ登録ポータルによって割り当てられた**アプリケーション ID** 。</span><span class="sxs-lookup"><span data-stu-id="da927-184">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="da927-185">アプリでシングルサインオン (SSO) がサポートされている場合は、アプリと SSO に対して同じアプリケーション ID を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="da927-185">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="da927-186">**クライアントシークレット/パスワード**、または公開/秘密キーペア (**証明書**)。</span><span class="sxs-lookup"><span data-stu-id="da927-186">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="da927-187">ネイティブ アプリの場合、これは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="da927-187">This is not required for native apps.</span></span>
- <span data-ttu-id="da927-188">Azure AD からの応答を受信するための、アプリの**リダイレクト URI** (または応答 URL)。</span><span class="sxs-lookup"><span data-stu-id="da927-188">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="da927-189">ユーザー[の代理](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token)としてアクセスを取得し、[ユーザーなしでアクセスを取得する](/graph/auth-v2-service)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="da927-189">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="da927-190">Teams アプリマニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="da927-190">Update your Teams app manifest</span></span>

<span data-ttu-id="da927-191">RSC アクセス許可は、アプリマニフェスト (JSON) ファイルで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="da927-191">The RSC permissions are declared in you app manifest (JSON) file.</span></span>  <span data-ttu-id="da927-192">次の値を使用して、 [Webapplicationinfo](../../resources/schema/manifest-schema.md#webapplicationinfo)キーをアプリのマニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="da927-192">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="da927-193">**id** : Azure AD アプリ id。*「* [Azure AD ポータルでアプリを登録](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da927-193">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="da927-194">**resource** -任意の文字列。</span><span class="sxs-lookup"><span data-stu-id="da927-194">**resource**  — any string.</span></span> <span data-ttu-id="da927-195">このフィールドは、RSC では操作を行いませんが、追加して、エラー応答が発生しないように値を設定する必要があります。任意の文字列が実行されます。</span><span class="sxs-lookup"><span data-stu-id="da927-195">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="da927-196">**アプリケーションのアクセス許可**-アプリの RSC アクセス許可。</span><span class="sxs-lookup"><span data-stu-id="da927-196">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="da927-197">[リソース固有の権限](resource-specific-consent.md#resource-specific-permissions)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="da927-197">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="da927-198">非 RSC アクセス許可は、Azure portal に格納されます。</span><span class="sxs-lookup"><span data-stu-id="da927-198">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="da927-199">アプリマニフェストに追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="da927-199">Do not add them to the app manifest.</span></span>
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="da927-200">Teams にアプリを直接インストールする</span><span class="sxs-lookup"><span data-stu-id="da927-200">Install your app directly in Teams</span></span>

<span data-ttu-id="da927-201">アプリを作成したら、[アプリパッケージ](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab)を特定のチームに直接アップロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="da927-201">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="da927-202">そのためには、カスタムアプリのセットアップポリシーの一部として、[**カスタムアプリのアップロード**] ポリシー設定を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="da927-202">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="da927-203">*「* [Custom App policy Settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da927-203">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="da927-204">アプリで RSC 権限が追加されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="da927-204">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="da927-205">RSC のアクセス許可は、ユーザーには含まれません。</span><span class="sxs-lookup"><span data-stu-id="da927-205">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="da927-206">呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可で行われます。</span><span class="sxs-lookup"><span data-stu-id="da927-206">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="da927-207">そのため、アプリは、チャネルの作成やタブの削除など、ユーザーができない操作を実行できる場合があります。RSC API 呼び出しを行う前に、ユースケースに対するチーム所有者の意図を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="da927-207">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="da927-208">*「* [Microsoft Teams API の概要](/graph/teams-concept-overview)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da927-208">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="da927-209">アプリがチームにインストールされたら、 [Graph エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を使用して、チーム内のアプリに付与されているアクセス許可を表示できます。</span><span class="sxs-lookup"><span data-stu-id="da927-209">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="da927-210">Teams クライアントからチームの**groupId**を取得します。</span><span class="sxs-lookup"><span data-stu-id="da927-210">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="da927-211">Teams クライアントで、左端のナビゲーションバーにある [ **teams** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="da927-211">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="da927-212">アプリがインストールされているチームを、ドロップダウンメニューから選択します。</span><span class="sxs-lookup"><span data-stu-id="da927-212">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="da927-213">[**その他のオプション**] アイコン (&#8943;) を選択します。</span><span class="sxs-lookup"><span data-stu-id="da927-213">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="da927-214">[**チームへのリンクの取得**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="da927-214">Select **Get link to team**.</span></span>
> - <span data-ttu-id="da927-215">文字列から**groupId**値をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="da927-215">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="da927-216">**Graph エクスプローラー**にログインします。</span><span class="sxs-lookup"><span data-stu-id="da927-216">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="da927-217">次のエンドポイントに対して**GET**を `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 呼び出します。</span><span class="sxs-lookup"><span data-stu-id="da927-217">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="da927-218">応答の clientAppId フィールドは、Teams アプリマニフェストで指定されている appId にマップされます。</span><span class="sxs-lookup"><span data-stu-id="da927-218">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>

 ![通話を取得するための Graph エクスプローラーの応答。](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a><span data-ttu-id="da927-220">リソース固有の同意をテストする</span><span class="sxs-lookup"><span data-stu-id="da927-220">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="da927-221">**Teams でのリソース固有の同意権限をテストする**</span><span class="sxs-lookup"><span data-stu-id="da927-221">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="da927-222">Teams 管理者向けの関連トピック</span><span class="sxs-lookup"><span data-stu-id="da927-222">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="da927-223">**管理者のための Microsoft Teams でのリソース固有の同意**</span><span class="sxs-lookup"><span data-stu-id="da927-223">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 
