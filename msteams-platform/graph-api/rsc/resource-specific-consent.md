---
title: リソース固有の同意 (Teams
description: リソース固有の同意について、Teams活用する方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: teams 承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 215b528310137da331b0aef6ab004e0448dbfadf
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994321"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="4782f-104">リソース固有の同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="4782f-104">Resource-specific consent (RSC)</span></span>

> [!NOTE]
> <span data-ttu-id="4782f-105">チャット スコープに対するリソース固有の同意は、パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="4782f-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="4782f-106">リソース固有の同意 (RSC) は、Microsoft Teams API と Microsoft Graph API の統合であり、アプリは API エンドポイントを使用して、組織内の特定のリソース (チームまたはチャット) を管理できます。</span><span class="sxs-lookup"><span data-stu-id="4782f-106">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific resources—either teams or chats—within an organization.</span></span> <span data-ttu-id="4782f-107">リソース固有の同意 (RSC) アクセス許可モデルを使用すると、チームの所有者とチャット所有者は、アプリケーションがチームのデータとチャットのデータにそれぞれアクセスしたり、変更したりするための同意を付与できます。</span><span class="sxs-lookup"><span data-stu-id="4782f-107">The resource-specific consent (RSC) permissions model enables *team owners* and *chat owners* to grant consent for an application to access and/or modify a team's data and a chat's data, respectively.</span></span> <span data-ttu-id="4782f-108">詳細で、Teams固有の RSC アクセス許可は、アプリケーションが特定のリソース内で実行できる操作を定義します。</span><span class="sxs-lookup"><span data-stu-id="4782f-108">The granular, Teams-specific, RSC permissions define what an application can do within a specific resource:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="4782f-109">リソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="4782f-109">Resource-specific permissions</span></span>

### <a name="resource-specific-permissions-for-a-team"></a><span data-ttu-id="4782f-110">チームのリソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="4782f-110">Resource-specific permissions for a team</span></span>
|<span data-ttu-id="4782f-111">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="4782f-111">Application permission</span></span>| <span data-ttu-id="4782f-112">アクション</span><span class="sxs-lookup"><span data-stu-id="4782f-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="4782f-113">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="4782f-114">このチームの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-114">Get this team's settings.</span></span>|
|<span data-ttu-id="4782f-115">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-115">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="4782f-116">このチームの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="4782f-116">Update this team's settings.</span></span>|
|<span data-ttu-id="4782f-117">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="4782f-118">このチームのチャネル名、チャネルの説明、チャネル設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-118">Get this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="4782f-119">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-119">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="4782f-120">このチームのチャネル名、チャネルの説明、チャネル設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="4782f-120">Update this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="4782f-121">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-121">Channel.Create.Group</span></span>|<span data-ttu-id="4782f-122">このチームのチャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="4782f-122">Create channels in this team.</span></span>|
|<span data-ttu-id="4782f-123">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-123">Channel.Delete.Group</span></span>|<span data-ttu-id="4782f-124">このチームのチャネルを削除します。</span><span class="sxs-lookup"><span data-stu-id="4782f-124">Delete channels in this team.</span></span>|
|<span data-ttu-id="4782f-125">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="4782f-126">このチームのチャネル メッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-126">Get this team's channel messages.</span></span>|
|<span data-ttu-id="4782f-127">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-127">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="4782f-128">このチームのインストール済みアプリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="4782f-129">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="4782f-130">このチームのタブの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="4782f-131">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="4782f-132">このチームのタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="4782f-132">Create tabs in this team.</span></span>|
|<span data-ttu-id="4782f-133">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-133">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="4782f-134">このチームのタブを更新します。</span><span class="sxs-lookup"><span data-stu-id="4782f-134">Update this team's tabs.</span></span>|
|<span data-ttu-id="4782f-135">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="4782f-136">このチームのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="4782f-136">Delete this team's tabs.</span></span>|
|<span data-ttu-id="4782f-137">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="4782f-137">TeamMember.Read.Group</span></span>|<span data-ttu-id="4782f-138">このチームのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-138">Get this team's members.</span></span>|

<span data-ttu-id="4782f-139">詳細については、「リソース固有[のTeamsアクセス許可」を参照してください](/graph/permissions-reference#teams-resource-specific-consent-permissions)。</span><span class="sxs-lookup"><span data-stu-id="4782f-139">For more details, see [Teams resource-specific consent permissions](/graph/permissions-reference#teams-resource-specific-consent-permissions).</span></span>

### <a name="resource-specific-permissions-for-a-chat"></a><span data-ttu-id="4782f-140">チャットのリソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="4782f-140">Resource-specific permissions for a chat</span></span>
|<span data-ttu-id="4782f-141">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="4782f-141">Application permission</span></span>| <span data-ttu-id="4782f-142">アクション</span><span class="sxs-lookup"><span data-stu-id="4782f-142">Action</span></span> |
| ----- | ----- |
| <span data-ttu-id="4782f-143">ChatSettings.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-143">ChatSettings.Read.Chat</span></span>         | <span data-ttu-id="4782f-144">このチャットの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-144">Get this chat's settings.</span></span>                                    |
| <span data-ttu-id="4782f-145">ChatSettings.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-145">ChatSettings.ReadWrite.Chat</span></span>    | <span data-ttu-id="4782f-146">このチャットの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="4782f-146">Update this chat's settings.</span></span>                          |
| <span data-ttu-id="4782f-147">ChatMessage.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-147">ChatMessage.Read.Chat</span></span>          | <span data-ttu-id="4782f-148">このチャットのメッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-148">Get this chat's messages.</span></span>                                    |
| <span data-ttu-id="4782f-149">ChatMember.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-149">ChatMember.Read.Chat</span></span>           | <span data-ttu-id="4782f-150">このチャットのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-150">Get this chat's members.</span></span>                                     |
| <span data-ttu-id="4782f-151">Chat.Manage.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-151">Chat.Manage.Chat</span></span>               | <span data-ttu-id="4782f-152">このチャットを管理します。</span><span class="sxs-lookup"><span data-stu-id="4782f-152">Manage this chat.</span></span>                                             |
| <span data-ttu-id="4782f-153">TeamsTab.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-153">TeamsTab.Read.Chat</span></span>             | <span data-ttu-id="4782f-154">このチャットのタブを取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-154">Get this chat's tabs.</span></span>                                        |
| <span data-ttu-id="4782f-155">TeamsTab.Create.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-155">TeamsTab.Create.Chat</span></span>           | <span data-ttu-id="4782f-156">このチャットでタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="4782f-156">Create tabs in this chat.</span></span>                                     |
| <span data-ttu-id="4782f-157">TeamsTab.Delete.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-157">TeamsTab.Delete.Chat</span></span>           | <span data-ttu-id="4782f-158">このチャットのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="4782f-158">Delete this chat's tabs.</span></span>                                      |
| <span data-ttu-id="4782f-159">TeamsTab.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-159">TeamsTab.ReadWrite.Chat</span></span>        | <span data-ttu-id="4782f-160">このチャットのタブを管理します。</span><span class="sxs-lookup"><span data-stu-id="4782f-160">Manage this chat's tabs.</span></span>                                      |
| <span data-ttu-id="4782f-161">TeamsAppInstallation.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-161">TeamsAppInstallation.Read.Chat</span></span> | <span data-ttu-id="4782f-162">このチャットにインストールされているアプリを取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-162">Get which apps are installed in this chat.</span></span>                   |
| <span data-ttu-id="4782f-163">OnlineMeeting.ReadBasic.Chat</span><span class="sxs-lookup"><span data-stu-id="4782f-163">OnlineMeeting.ReadBasic.Chat</span></span>   | <span data-ttu-id="4782f-164">このチャットに関連付けられた会議の基本的なプロパティ (名前、スケジュール、開催者、参加リンクなど) を取得します。</span><span class="sxs-lookup"><span data-stu-id="4782f-164">Get basic properties—such as name, schedule, organizer, and join link—of a meeting associated with this chat.</span></span> |

<span data-ttu-id="4782f-165">詳細については、「Chat リソース固有の [同意のアクセス許可」を参照してください](/graph/permissions-reference#chat-resource-specific-consent-permissions)。</span><span class="sxs-lookup"><span data-stu-id="4782f-165">For more details, see [Chat resource-specific consent permissions](/graph/permissions-reference#chat-resource-specific-consent-permissions).</span></span>

>[!NOTE]
><span data-ttu-id="4782f-166">リソース固有のアクセス許可は、Teams クライアントにインストールTeamsアプリでのみ使用できます。現在は、Azure Active Directory ポータルの一部ではありません。</span><span class="sxs-lookup"><span data-stu-id="4782f-166">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="4782f-167">アプリケーションでリソース固有の同意を有効にする</span><span class="sxs-lookup"><span data-stu-id="4782f-167">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="4782f-168">アプリケーションで RSC を有効にする手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="4782f-168">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="4782f-169">[ポータルで同意の設定をAzure Active Directoryします](#configure-consent-settings-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="4782f-169">[Configure consent settings in the Azure Active Directory portal](#configure-consent-settings-in-the-azure-ad-portal).</span></span>
    1. <span data-ttu-id="4782f-170">[チーム内の RSC のグループ所有者の同意設定を構成します](#configure-group-owner-consent-settings-for-rsc-in-a-team)。</span><span class="sxs-lookup"><span data-stu-id="4782f-170">[Configure group owner consent settings for RSC in a team](#configure-group-owner-consent-settings-for-rsc-in-a-team).</span></span>
    1. <span data-ttu-id="4782f-171">[チャットで RSC のユーザー同意設定を構成します](#configure-user-consent-settings-for-rsc-in-a-chat)。</span><span class="sxs-lookup"><span data-stu-id="4782f-171">[Configure user consent settings for RSC in a chat](#configure-user-consent-settings-for-rsc-in-a-chat).</span></span>
1. <span data-ttu-id="4782f-172">[Azure Microsoft ID プラットフォーム ポータルをADします](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="4782f-172">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="4782f-173">[Azure ADポータルでアプリケーションのアクセス許可を確認します](#review-your-application-permissions-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="4782f-173">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="4782f-174">[Microsoft Identity プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="4782f-174">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="4782f-175">[アプリ マニフェストTeams更新します](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="4782f-175">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="4782f-176">[アプリをアプリに直接インストールTeams。](#sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="4782f-176">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="4782f-177">[アプリで追加された RSC アクセス許可を確認します](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="4782f-177">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>
    1. <span data-ttu-id="4782f-178">[チームに追加された RSC アクセス許可をアプリで確認します](#check-your-app-for-added-rsc-permissions-in-a-team)。</span><span class="sxs-lookup"><span data-stu-id="4782f-178">[Check your app for added RSC permissions in a team](#check-your-app-for-added-rsc-permissions-in-a-team).</span></span>
    1. <span data-ttu-id="4782f-179">[チャットで追加された RSC アクセス許可をアプリで確認します](#check-your-app-for-added-rsc-permissions-in-a-chat)。</span><span class="sxs-lookup"><span data-stu-id="4782f-179">[Check your app for added RSC permissions in a chat](#check-your-app-for-added-rsc-permissions-in-a-chat).</span></span>

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="4782f-180">Azure AD ポータルで同意の設定を構成する</span><span class="sxs-lookup"><span data-stu-id="4782f-180">Configure consent settings in the Azure AD portal</span></span>

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a><span data-ttu-id="4782f-181">チームで RSC のグループ所有者の同意設定を構成する</span><span class="sxs-lookup"><span data-stu-id="4782f-181">Configure group owner consent settings for RSC in a team</span></span>

<span data-ttu-id="4782f-182">Azure portal 内でグループ所有者 [の同意を直接](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 有効または無効にできます。</span><span class="sxs-lookup"><span data-stu-id="4782f-182">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="4782f-183">グローバル管理者/ [会社管理者として Azure](https://portal.azure.com) portal [にサインインします](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="4782f-183">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>  
 > - <span data-ttu-id="4782f-184">[[アプリケーション](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)  =>  **Azure Active Directory Enterpriseと** アクセス許可ユーザー  =>  **の同意設定**  =>  **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="4782f-184">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="4782f-185">データにアクセスするアプリに対するグループ所有者の同意というラベルが付いたコントロールを使用して、ユーザーの同意を有効、無効、または制限します **(既定** では、すべてのグループ所有者にグループ所有者の同意 **を許可します**)。</span><span class="sxs-lookup"><span data-stu-id="4782f-185">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="4782f-186">チームの所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4782f-186">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![azure rsc チーム構成](../../assets/images/azure-rsc-team-configuration.png)

<span data-ttu-id="4782f-188">PowerShell を使用してグループ所有者の同意を有効または無効にするには、「PowerShell を使用してグループ所有者の同意を構成する」で説明 [されている手順に従います](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="4782f-188">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a><span data-ttu-id="4782f-189">チャットで RSC のユーザー同意設定を構成する</span><span class="sxs-lookup"><span data-stu-id="4782f-189">Configure user consent settings for RSC in a chat</span></span>

<span data-ttu-id="4782f-190">Azure portal 内でユーザーの [同意を直接](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) 有効または無効にできます。</span><span class="sxs-lookup"><span data-stu-id="4782f-190">You can enable or disable [user consent](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="4782f-191">グローバル管理者/ [会社管理者として Azure](https://portal.azure.com) portal [にサインインします](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="4782f-191">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>  
 > - <span data-ttu-id="4782f-192">[[アプリケーション](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)  =>  **Azure Active Directory Enterpriseと** アクセス許可ユーザー  =>  **の同意設定**  =>  **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="4782f-192">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="4782f-193">[アプリケーションに対するユーザーの同意] というラベルの付いたコントロールを使用して、ユーザーの同意を有効、無効、または制限します **(既定値** は [アプリの **ユーザーの同意を** 許可する] です)。</span><span class="sxs-lookup"><span data-stu-id="4782f-193">Enable, disable, or limit user consent with the control labeled **User consent for applications** (The default is **Allow user consent for apps**).</span></span> <span data-ttu-id="4782f-194">チャット メンバーが RSC を使用してアプリをインストールするには、そのユーザーに対してユーザーの同意を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4782f-194">For a chat member to install an app using RSC, user consent must be enabled for that user.</span></span>

![azure rsc チャット構成](../../assets/images/azure-rsc-chat-configuration.png)

<span data-ttu-id="4782f-196">PowerShell を使用してユーザーの同意を有効または無効にするには、「PowerShell を使用してユーザーの同意を構成する」で説明 [されている手順に従います](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="4782f-196">To enable or disable user consent using PowerShell, follow the steps outlined in [Configure user consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell).</span></span>


## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="4782f-197">Azure Microsoft ID プラットフォーム ポータルを使用してアプリをADする</span><span class="sxs-lookup"><span data-stu-id="4782f-197">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="4782f-198">このAzure Active Directoryは、アプリを登録および構成する中心的なプラットフォームを提供します。</span><span class="sxs-lookup"><span data-stu-id="4782f-198">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="4782f-199">アプリを Azure ADポータルに登録して、アプリと統合し、Microsoft Microsoft ID プラットフォーム API Graphする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4782f-199">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="4782f-200">詳細については、「アプリケーションを[アプリケーションに登録する」を参照Microsoft ID プラットフォーム。](/graph/auth-register-app-v2)</span><span class="sxs-lookup"><span data-stu-id="4782f-200">For more information, see [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="4782f-201">Azure アプリ ID AD複数のアプリ間で共有Teamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4782f-201">An Azure AD app ID should not be shared across multiple Teams apps.</span></span> <span data-ttu-id="4782f-202">1 つのアプリと Azure アプリの間に 1:1 TeamsマッピングがADがあります。</span><span class="sxs-lookup"><span data-stu-id="4782f-202">There should be a 1:1 mapping between a Teams App and an Azure AD app.</span></span> <span data-ttu-id="4782f-203">同じ Azure TEAMSに関連付けられている複数のアプリをインストールしようとすると、AD/ランタイムエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="4782f-203">Attempts to install multiple Teams apps which are associated with the same Azure AD app ID will cause installation/runtime failures.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="4782f-204">Azure AD ポータルでアプリケーションのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="4782f-204">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="4782f-205">[ホーム アプリの **登録**  =>  **] ページに移動し**、RSC アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="4782f-205">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="4782f-206">左側 **のナビゲーション バーから API** アクセス許可を選択し、アプリに対して構成されているアクセス許可の一覧を確認します。</span><span class="sxs-lookup"><span data-stu-id="4782f-206">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="4782f-207">アプリが API 呼び出しでのみ RSC Graphする場合は、そのページのすべてのアクセス許可を削除します。</span><span class="sxs-lookup"><span data-stu-id="4782f-207">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="4782f-208">アプリで RSC 以外の呼び出しを行う場合は、必要に応じてこれらのアクセス許可を保持します。</span><span class="sxs-lookup"><span data-stu-id="4782f-208">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="4782f-209">Azure ADポータルを使用して RSC アクセス許可を要求することはできません。</span><span class="sxs-lookup"><span data-stu-id="4782f-209">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="4782f-210">RSC アクセス許可は現在、Teams クライアントにインストールされている Teams アプリケーション専用であり、Teams アプリ マニフェスト (JSON) ファイルで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="4782f-210">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the Teams app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="4782f-211">サーバーからアクセス トークンを取得Microsoft ID プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="4782f-211">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="4782f-212">API 呼びGraphするには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4782f-212">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="4782f-213">アプリがアプリからトークンを取得するには、Microsoft ID プラットフォーム Azure ポータルに登録するADがあります。</span><span class="sxs-lookup"><span data-stu-id="4782f-213">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="4782f-214">アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。</span><span class="sxs-lookup"><span data-stu-id="4782f-214">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="4782f-215">ID プラットフォームからアクセス トークンを取得するには、Azure AD登録プロセスから次の値を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4782f-215">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="4782f-216">アプリ **登録ポータルによって** 割り当てられたアプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="4782f-216">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="4782f-217">アプリがシングル サインオン (SSO) をサポートしている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4782f-217">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="4782f-218">クライアント  **シークレット/パスワード、** または公開/秘密キーのペア (**証明書**)。</span><span class="sxs-lookup"><span data-stu-id="4782f-218">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="4782f-219">ネイティブ アプリの場合、これは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="4782f-219">This is not required for native apps.</span></span>
- <span data-ttu-id="4782f-220">Azure **サーバーから応答** を受信するアプリのリダイレクト URI (または返信 URL) AD。</span><span class="sxs-lookup"><span data-stu-id="4782f-220">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="4782f-221">*「*[ユーザーに代わってアクセスを取得する」および](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)「[ユーザーなしでアクセスを取得する」を参照してください。](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="4782f-221">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="4782f-222">アプリ マニフェストTeams更新する</span><span class="sxs-lookup"><span data-stu-id="4782f-222">Update your Teams app manifest</span></span>

<span data-ttu-id="4782f-223">RSC アクセス許可は、アプリ マニフェスト (JSON) ファイルで宣言されます。</span><span class="sxs-lookup"><span data-stu-id="4782f-223">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="4782f-224">次の [値を使用して、WebApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="4782f-224">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="4782f-225">**id**  — Azure ADアプリ ID。</span><span class="sxs-lookup"><span data-stu-id="4782f-225">**id**  — your Azure AD app ID.</span></span> <span data-ttu-id="4782f-226">詳細については、「Azure AD ポータルにアプリを [登録する」を参照してください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="4782f-226">For more information, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="4782f-227">**resource**  — 任意の文字列。</span><span class="sxs-lookup"><span data-stu-id="4782f-227">**resource**  — any string.</span></span> <span data-ttu-id="4782f-228">このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加して値を指定する必要があります。任意の文字列が実行します。</span><span class="sxs-lookup"><span data-stu-id="4782f-228">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="4782f-229">**アプリケーションのアクセス許可** - アプリの RSC アクセス許可。</span><span class="sxs-lookup"><span data-stu-id="4782f-229">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="4782f-230">詳細については、「リソース固有 [のアクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="4782f-230">For more information, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="4782f-231">RSC 以外のアクセス許可は Azure portal に格納されます。</span><span class="sxs-lookup"><span data-stu-id="4782f-231">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="4782f-232">アプリ マニフェストに追加しません。</span><span class="sxs-lookup"><span data-stu-id="4782f-232">Do not add them to the app manifest.</span></span>
>

### <a name="example-for-rsc-in-a-team"></a><span data-ttu-id="4782f-233">チームの RSC の例</span><span class="sxs-lookup"><span data-stu-id="4782f-233">Example for RSC in a team</span></span>
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

### <a name="example-for-rsc-in-a-chat"></a><span data-ttu-id="4782f-234">チャット内の RSC の例</span><span class="sxs-lookup"><span data-stu-id="4782f-234">Example for RSC in a chat</span></span>
```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "ChatSettings.Read.Chat",
      "ChatSettings.ReadWrite.Chat",
      "ChatMessage.Read.Chat",
      "ChatMember.Read.Chat",
      "Chat.Manage.Chat",
      "TeamsTab.Read.Chat",
      "TeamsTab.Create.Chat",
      "TeamsTab.Delete.Chat",
      "TeamsTab.ReadWrite.Chat",
      "TeamsAppInstallation.Read.Chat",
      "OnlineMeeting.ReadBasic.Chat"
    ]
  }
```

>[!NOTE]
><span data-ttu-id="4782f-235">アプリがチームスコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を同じマニフェストで指定できます `applicationPermissions` 。</span><span class="sxs-lookup"><span data-stu-id="4782f-235">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="4782f-236">アプリをサイドロードTeams</span><span class="sxs-lookup"><span data-stu-id="4782f-236">Sideload your app in Teams</span></span>

<span data-ttu-id="4782f-237">管理者がTeamsアプリのアップロードを許可している場合は、アプリを特定[](~/concepts/deploy-and-publish/apps-upload.md)のチームまたはチャットに直接サイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="4782f-237">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team or chat.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="4782f-238">アプリで追加された RSC アクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="4782f-238">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="4782f-239">RSC アクセス許可は、ユーザーに属性付けされません。</span><span class="sxs-lookup"><span data-stu-id="4782f-239">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="4782f-240">呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可を使用して行います。</span><span class="sxs-lookup"><span data-stu-id="4782f-240">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="4782f-241">したがって、アプリは、タブの削除など、ユーザーが実行できない操作を実行できる場合があります。RSC API 呼び出しを行う前に、チーム所有者またはチャット所有者の使用例の意図を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4782f-241">Thus, the app may be allowed to perform actions that the user cannot, such as deleting a tab. You should review the team owner's or chat owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="4782f-242">詳細については、「API の概要[Microsoft Teamsを参照してください](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="4782f-242">For more information, see [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="4782f-243">アプリがリソースにインストールされた後、Graph[エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を使用して、リソース内のアプリに付与されたアクセス許可を表示できます。</span><span class="sxs-lookup"><span data-stu-id="4782f-243">Once the app has been installed to a resource, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in the resource:</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a><span data-ttu-id="4782f-244">チームに追加された RSC アクセス許可をアプリで確認する</span><span class="sxs-lookup"><span data-stu-id="4782f-244">Check your app for added RSC permissions in a team</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="4782f-245">チームの **groupId** をクライアントから取得Teamsします。</span><span class="sxs-lookup"><span data-stu-id="4782f-245">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="4782f-246">クライアントで、Teams **ナビゲーション** バー Teamsを選択します。</span><span class="sxs-lookup"><span data-stu-id="4782f-246">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="4782f-247">ドロップダウン メニューからアプリがインストールされているチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="4782f-247">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="4782f-248">[その他 **のオプション]** アイコンを選択します (&#8943;)。</span><span class="sxs-lookup"><span data-stu-id="4782f-248">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="4782f-249">[チーム **へのリンクを取得する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="4782f-249">Select **Get link to team**.</span></span>
> - <span data-ttu-id="4782f-250">文字列から **groupId 値をコピー** して保存します。</span><span class="sxs-lookup"><span data-stu-id="4782f-250">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="4782f-251">エクスプローラーに **Graphします**。</span><span class="sxs-lookup"><span data-stu-id="4782f-251">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="4782f-252">次の **エンドポイントに対** して GET 呼び出しを行います `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` 。</span><span class="sxs-lookup"><span data-stu-id="4782f-252">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="4782f-253">応答 `clientAppId` のフィールドは、アプリ マニフェスト `webApplicationInfo.id` で指定されたTeamsマップされます。</span><span class="sxs-lookup"><span data-stu-id="4782f-253">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>
  <span data-ttu-id="4782f-254">![Graph RSC アクセス許可の GET 呼び出しに対するエクスプローラーの応答を確認します。](../../assets/images/team-graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="4782f-254">![Graph explorer response to GET call for team RSC permissions.](../../assets/images/team-graph-permissions.png)</span></span>

<span data-ttu-id="4782f-255">特定のチームにインストールされているアプリの詳細を取得する方法については、「指定したチームにインストールされているアプリの名前と他の詳細を取得する」 [を参照してください](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)。</span><span class="sxs-lookup"><span data-stu-id="4782f-255">For information about how to get details about apps installed in a specific team, see [Get the names and other details of apps installed in the specified team](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a><span data-ttu-id="4782f-256">チャットで追加された RSC アクセス許可をアプリで確認する</span><span class="sxs-lookup"><span data-stu-id="4782f-256">Check your app for added RSC permissions in a chat</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="4782f-257">Web クライアントからチャット スレッド ID を *Teamsします。*</span><span class="sxs-lookup"><span data-stu-id="4782f-257">Get the chat thread ID from the Teams *web* client.</span></span>
> - <span data-ttu-id="4782f-258">Web クライアントTeams、左側 **のナビゲーション** バーから [チャット] を選択します。</span><span class="sxs-lookup"><span data-stu-id="4782f-258">In the Teams web client, select **Chat** from the far left nav bar.</span></span>
> - <span data-ttu-id="4782f-259">アプリがインストールされているチャットをドロップダウン メニューから選択します。</span><span class="sxs-lookup"><span data-stu-id="4782f-259">Select the chat where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="4782f-260">Web URL をコピーし、文字列からチャット スレッド ID を保存します。</span><span class="sxs-lookup"><span data-stu-id="4782f-260">Copy the web URL and save the chat thread ID from the string.</span></span>
<span data-ttu-id="4782f-261">![Web URL からのチャット スレッド ID。](../../assets/images/chat-thread-id.png)</span><span class="sxs-lookup"><span data-stu-id="4782f-261">![Chat thread id from web URL.](../../assets/images/chat-thread-id.png)</span></span>
> - <span data-ttu-id="4782f-262">エクスプローラーに **Graphします**。</span><span class="sxs-lookup"><span data-stu-id="4782f-262">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="4782f-263">次の **エンドポイントに対** して GET 呼び出しを行います `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` 。</span><span class="sxs-lookup"><span data-stu-id="4782f-263">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`.</span></span> <span data-ttu-id="4782f-264">応答 `clientAppId` のフィールドは、アプリ マニフェスト `webApplicationInfo.id` で指定されたTeamsマップされます。</span><span class="sxs-lookup"><span data-stu-id="4782f-264">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>
  <span data-ttu-id="4782f-265">![Graph RSC アクセス許可の GET 呼び出しに対するエクスプローラーの応答を確認します。](../../assets/images/chat-graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="4782f-265">![Graph explorer response to GET call for chat RSC permissions.](../../assets/images/chat-graph-permissions.png)</span></span>

<span data-ttu-id="4782f-266">特定のチャットにインストールされているアプリの詳細を取得する方法については、「指定したチャットにインストールされているアプリの名前と他の詳細を取得する」 [を参照してください](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)。</span><span class="sxs-lookup"><span data-stu-id="4782f-266">For information about how to get details about apps installed in a specific chat, see [Get the names and other details of apps installed in the specified chat](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat).</span></span>

## <a name="code-sample"></a><span data-ttu-id="4782f-267">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="4782f-267">Code sample</span></span>
| <span data-ttu-id="4782f-268">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="4782f-268">**Sample name**</span></span> | <span data-ttu-id="4782f-269">**説明**</span><span class="sxs-lookup"><span data-stu-id="4782f-269">**Description**</span></span> | <span data-ttu-id="4782f-270">**.NET**</span><span class="sxs-lookup"><span data-stu-id="4782f-270">**.NET**</span></span> |<span data-ttu-id="4782f-271">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="4782f-271">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="4782f-272">リソース固有の同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="4782f-272">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="4782f-273">RSC を使用して API Graph呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4782f-273">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="4782f-274">View</span><span class="sxs-lookup"><span data-stu-id="4782f-274">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="4782f-275">View</span><span class="sxs-lookup"><span data-stu-id="4782f-275">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a><span data-ttu-id="4782f-276">関連項目</span><span class="sxs-lookup"><span data-stu-id="4782f-276">See also</span></span>
 
* [<span data-ttu-id="4782f-277">リソース固有の同意のアクセス許可をテストTeams</span><span class="sxs-lookup"><span data-stu-id="4782f-277">Test resource-specific consent permissions in Teams</span></span>](test-resource-specific-consent.md)
* [<span data-ttu-id="4782f-278">管理者向けリソース固有Microsoft Teams同意</span><span class="sxs-lookup"><span data-stu-id="4782f-278">Resource-specific consent in Microsoft Teams for admins</span></span>](/MicrosoftTeams/resource-specific-consent)


