---
title: リソース固有の同意を有効Teams
description: リソース固有の同意について、Teams活用する方法について説明します。
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: teams 承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: ce4076ff8cb9945f3b7dd1a7e809391292ec314a
ms.sourcegitcommit: c145d52b2d4daa7655e6c3ddfa739fa1beeb8d6a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2021
ms.locfileid: "53455221"
---
# <a name="resource-specific-consent"></a><span data-ttu-id="1337c-104">リソース固有の同意</span><span class="sxs-lookup"><span data-stu-id="1337c-104">Resource-specific consent</span></span>

> [!NOTE]
> <span data-ttu-id="1337c-105">チャット スコープに対するリソース固有の同意は、パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="1337c-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="1337c-106">リソース固有の同意 (RSC) は、Microsoft Teams と Microsoft Graph API の統合であり、アプリは API エンドポイントを使用して、組織内のチームまたはチャットのいずれかの特定のリソースを管理できます。</span><span class="sxs-lookup"><span data-stu-id="1337c-106">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific resources, either teams or chats, within an organization.</span></span> <span data-ttu-id="1337c-107">RSC アクセス許可モデルを使用すると、チームの所有者とチャットの所有者は、アプリケーションがチームのデータとチャットのデータにそれぞれアクセスおよび変更するための同意を付与できます。</span><span class="sxs-lookup"><span data-stu-id="1337c-107">The RSC permissions model enables *team owners* and *chat owners* to grant consent for an application to access and modify a team's data and a chat's data, respectively.</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="1337c-108">リソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="1337c-108">Resource-specific permissions</span></span>

<span data-ttu-id="1337c-109">詳細で、Teams固有の RSC アクセス許可は、アプリケーションが特定のリソース内で実行できる操作を定義します。</span><span class="sxs-lookup"><span data-stu-id="1337c-109">The granular, Teams-specific, RSC permissions define what an application can do within a specific resource.</span></span>

### <a name="resource-specific-permissions-for-a-team"></a><span data-ttu-id="1337c-110">チームのリソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="1337c-110">Resource-specific permissions for a team</span></span>

|<span data-ttu-id="1337c-111">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="1337c-111">Application permission</span></span>| <span data-ttu-id="1337c-112">操作</span><span class="sxs-lookup"><span data-stu-id="1337c-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="1337c-113">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="1337c-114">このチームの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-114">Get this team's settings.</span></span>|
|<span data-ttu-id="1337c-115">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-115">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="1337c-116">このチームの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="1337c-116">Update this team's settings.</span></span>|
|<span data-ttu-id="1337c-117">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="1337c-118">このチームのチャネル名、チャネルの説明、チャネル設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-118">Get this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="1337c-119">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-119">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="1337c-120">このチームのチャネル名、チャネルの説明、チャネル設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="1337c-120">Update this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="1337c-121">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-121">Channel.Create.Group</span></span>|<span data-ttu-id="1337c-122">このチームのチャネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="1337c-122">Create channels in this team.</span></span> |
|<span data-ttu-id="1337c-123">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-123">Channel.Delete.Group</span></span>|<span data-ttu-id="1337c-124">このチームのチャネルを削除します。</span><span class="sxs-lookup"><span data-stu-id="1337c-124">Delete channels in this team.</span></span> |
|<span data-ttu-id="1337c-125">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="1337c-126">このチームのチャネル メッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-126">Get this team's channel messages.</span></span> |
|<span data-ttu-id="1337c-127">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-127">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="1337c-128">このチームのインストール済みアプリの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="1337c-129">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="1337c-130">このチームのタブの一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="1337c-131">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="1337c-132">このチームのタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="1337c-132">Create tabs in this team.</span></span> |
|<span data-ttu-id="1337c-133">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-133">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="1337c-134">このチームのタブを更新します。</span><span class="sxs-lookup"><span data-stu-id="1337c-134">Update this team's tabs.</span></span> |
|<span data-ttu-id="1337c-135">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="1337c-136">このチームのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="1337c-136">Delete this team's tabs.</span></span> |
|<span data-ttu-id="1337c-137">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="1337c-137">TeamMember.Read.Group</span></span>|<span data-ttu-id="1337c-138">このチームのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-138">Get this team's members.</span></span> |

<span data-ttu-id="1337c-139">詳細については、「チーム リソース固有 [の同意のアクセス許可」を参照してください](/graph/permissions-reference#teams-resource-specific-consent-permissions)。</span><span class="sxs-lookup"><span data-stu-id="1337c-139">For more details, see [team resource-specific consent permissions](/graph/permissions-reference#teams-resource-specific-consent-permissions).</span></span>

### <a name="resource-specific-permissions-for-a-chat"></a><span data-ttu-id="1337c-140">チャットのリソース固有のアクセス許可</span><span class="sxs-lookup"><span data-stu-id="1337c-140">Resource-specific permissions for a chat</span></span>

<span data-ttu-id="1337c-141">次の表に、チャットのリソース固有のアクセス許可を示します。</span><span class="sxs-lookup"><span data-stu-id="1337c-141">The following table provides resource-specific permissions for a chat:</span></span>

|<span data-ttu-id="1337c-142">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="1337c-142">Application permission</span></span>| <span data-ttu-id="1337c-143">操作</span><span class="sxs-lookup"><span data-stu-id="1337c-143">Action</span></span> |
| ----- | ----- |
| <span data-ttu-id="1337c-144">ChatSettings.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-144">ChatSettings.Read.Chat</span></span>         | <span data-ttu-id="1337c-145">このチャットの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-145">Get this chat's settings.</span></span>                                    |
| <span data-ttu-id="1337c-146">ChatSettings.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-146">ChatSettings.ReadWrite.Chat</span></span>    | <span data-ttu-id="1337c-147">このチャットの設定を更新します。</span><span class="sxs-lookup"><span data-stu-id="1337c-147">Update this chat's settings.</span></span>                          |
| <span data-ttu-id="1337c-148">ChatMessage.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-148">ChatMessage.Read.Chat</span></span>          | <span data-ttu-id="1337c-149">このチャットのメッセージを取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-149">Get this chat's messages.</span></span>                                    |
| <span data-ttu-id="1337c-150">ChatMember.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-150">ChatMember.Read.Chat</span></span>           | <span data-ttu-id="1337c-151">このチャットのメンバーを取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-151">Get this chat's members.</span></span>                                     |
| <span data-ttu-id="1337c-152">Chat.Manage.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-152">Chat.Manage.Chat</span></span>               | <span data-ttu-id="1337c-153">このチャットを管理します。</span><span class="sxs-lookup"><span data-stu-id="1337c-153">Manage this chat.</span></span>                                             |
| <span data-ttu-id="1337c-154">TeamsTab.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-154">TeamsTab.Read.Chat</span></span>             | <span data-ttu-id="1337c-155">このチャットのタブを取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-155">Get this chat's tabs.</span></span>                                        |
| <span data-ttu-id="1337c-156">TeamsTab.Create.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-156">TeamsTab.Create.Chat</span></span>           | <span data-ttu-id="1337c-157">このチャットでタブを作成します。</span><span class="sxs-lookup"><span data-stu-id="1337c-157">Create tabs in this chat.</span></span>                                     |
| <span data-ttu-id="1337c-158">TeamsTab.Delete.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-158">TeamsTab.Delete.Chat</span></span>           | <span data-ttu-id="1337c-159">このチャットのタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="1337c-159">Delete this chat's tabs.</span></span>                                      |
| <span data-ttu-id="1337c-160">TeamsTab.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-160">TeamsTab.ReadWrite.Chat</span></span>        | <span data-ttu-id="1337c-161">このチャットのタブを管理します。</span><span class="sxs-lookup"><span data-stu-id="1337c-161">Manage this chat's tabs.</span></span>                                      |
| <span data-ttu-id="1337c-162">TeamsAppInstallation.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-162">TeamsAppInstallation.Read.Chat</span></span> | <span data-ttu-id="1337c-163">このチャットにインストールされているアプリを取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-163">Get which apps are installed in this chat.</span></span>                   |
| <span data-ttu-id="1337c-164">OnlineMeeting.ReadBasic.Chat</span><span class="sxs-lookup"><span data-stu-id="1337c-164">OnlineMeeting.ReadBasic.Chat</span></span>   | <span data-ttu-id="1337c-165">このチャットに関連付けられた会議の名前、スケジュール、開催者、参加リンクなどの基本的なプロパティを取得します。</span><span class="sxs-lookup"><span data-stu-id="1337c-165">Get basic properties, such as name, schedule, organizer, and join link of a meeting associated with this chat.</span></span> |

<span data-ttu-id="1337c-166">詳細については、「チャット リソース [固有の同意のアクセス許可」を参照してください](/graph/permissions-reference#chat-resource-specific-consent-permissions)。</span><span class="sxs-lookup"><span data-stu-id="1337c-166">For more details, see [chat resource-specific consent permissions](/graph/permissions-reference#chat-resource-specific-consent-permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="1337c-167">リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリでのみ使用できます。現在は Azure Active Directory (AAD) ポータルの一部ではありません。</span><span class="sxs-lookup"><span data-stu-id="1337c-167">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory (AAD) portal.</span></span>

## <a name="enable-rsc-in-your-application"></a><span data-ttu-id="1337c-168">アプリケーションで RSC を有効にする</span><span class="sxs-lookup"><span data-stu-id="1337c-168">Enable RSC in your application</span></span>

1. <span data-ttu-id="1337c-169">[AAD ポータルで同意設定を構成します](#configure-consent-settings-in-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="1337c-169">[Configure consent settings in the AAD portal](#configure-consent-settings-in-the-aad-portal).</span></span>
    1. <span data-ttu-id="1337c-170">[チーム内の RSC のグループ所有者の同意設定を構成します](#configure-group-owner-consent-settings-for-rsc-in-a-team)。</span><span class="sxs-lookup"><span data-stu-id="1337c-170">[Configure group owner consent settings for RSC in a team](#configure-group-owner-consent-settings-for-rsc-in-a-team).</span></span>
    1. <span data-ttu-id="1337c-171">[チャットで RSC のユーザー同意設定を構成します](#configure-user-consent-settings-for-rsc-in-a-chat)。</span><span class="sxs-lookup"><span data-stu-id="1337c-171">[Configure user consent settings for RSC in a chat](#configure-user-consent-settings-for-rsc-in-a-chat).</span></span>
1. <span data-ttu-id="1337c-172">[AAD ポータルを使用Microsoft ID プラットフォームアプリをアプリに登録します](#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="1337c-172">[Register your app with Microsoft identity platform using the AAD portal](#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).</span></span>
1. <span data-ttu-id="1337c-173">[AAD ポータルでアプリケーションのアクセス許可を確認します](#review-your-application-permissions-in-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="1337c-173">[Review your application permissions in the AAD portal](#review-your-application-permissions-in-the-aad-portal).</span></span>
1. <span data-ttu-id="1337c-174">[ID プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="1337c-174">[Obtain an access token from the identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="1337c-175">[アプリ マニフェストTeams更新します](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="1337c-175">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="1337c-176">[アプリをアプリに直接インストールTeams。](#sideload-your-app-in-teams)</span><span class="sxs-lookup"><span data-stu-id="1337c-176">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="1337c-177">[アプリで追加された RSC アクセス許可を確認します](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="1337c-177">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>
    1. <span data-ttu-id="1337c-178">[チームに追加された RSC アクセス許可をアプリで確認します](#check-your-app-for-added-rsc-permissions-in-a-team)。</span><span class="sxs-lookup"><span data-stu-id="1337c-178">[Check your app for added RSC permissions in a team](#check-your-app-for-added-rsc-permissions-in-a-team).</span></span>
    1. <span data-ttu-id="1337c-179">[チャットで追加された RSC アクセス許可をアプリで確認します](#check-your-app-for-added-rsc-permissions-in-a-chat)。</span><span class="sxs-lookup"><span data-stu-id="1337c-179">[Check your app for added RSC permissions in a chat](#check-your-app-for-added-rsc-permissions-in-a-chat).</span></span>

## <a name="configure-consent-settings-in-the-aad-portal"></a><span data-ttu-id="1337c-180">AAD ポータルで同意設定を構成する</span><span class="sxs-lookup"><span data-stu-id="1337c-180">Configure consent settings in the AAD portal</span></span>

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a><span data-ttu-id="1337c-181">チームで RSC のグループ所有者の同意設定を構成する</span><span class="sxs-lookup"><span data-stu-id="1337c-181">Configure group owner consent settings for RSC in a team</span></span>

<span data-ttu-id="1337c-182">Azure portal 内でグループ所有者 [の同意を直接](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 有効または無効にできます。</span><span class="sxs-lookup"><span data-stu-id="1337c-182">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

1. <span data-ttu-id="1337c-183">グローバル管理者または [会社管理者として Azure](https://portal.azure.com) portal [にサインインします](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="1337c-183">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator or Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>
1. <span data-ttu-id="1337c-184">[アプリケーション **Azure Active Directory Enterprise** とアクセス許可ユーザーの同意  >    >  **設定**  >  [**] を選択します**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)。</span><span class="sxs-lookup"><span data-stu-id="1337c-184">Select **Azure Active Directory** > **Enterprise applications** > **Consent and permissions** > [**User consent settings**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).</span></span>
1. <span data-ttu-id="1337c-185">データにアクセスするアプリに対するグループ所有者の同意というラベルが付いたコントロールを使用して、ユーザーの同意を有効 **、無効、または制限します**。</span><span class="sxs-lookup"><span data-stu-id="1337c-185">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data**.</span></span> <span data-ttu-id="1337c-186">既定値は[ **すべてのグループ所有者に対するグループ所有者の同意を許可する] です**。</span><span class="sxs-lookup"><span data-stu-id="1337c-186">The default is **Allow group owner consent for all group owners**.</span></span> <span data-ttu-id="1337c-187">チームの所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1337c-187">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

    ![Azure RSC チーム構成](../../assets/images/azure-rsc-team-configuration.png)

<span data-ttu-id="1337c-189">さらに、PowerShell を使用してグループ所有者の同意を有効または無効にできます。PowerShell を使用してグループ所有者の同意を構成するで説明されている手順 [に従います](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="1337c-189">In addition, you can enable or disable group owner consent using PowerShell, follow the steps outlined in [configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a><span data-ttu-id="1337c-190">チャットで RSC のユーザー同意設定を構成する</span><span class="sxs-lookup"><span data-stu-id="1337c-190">Configure user consent settings for RSC in a chat</span></span>

<span data-ttu-id="1337c-191">Azure portal 内でユーザーの [同意を直接](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) 有効または無効にできます。</span><span class="sxs-lookup"><span data-stu-id="1337c-191">You can enable or disable [user consent](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directly within the Azure portal:</span></span>

1. <span data-ttu-id="1337c-192">グローバル管理者または [会社管理者として Azure](https://portal.azure.com) portal [にサインインします](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="1337c-192">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator or Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>
1. <span data-ttu-id="1337c-193">[アプリケーション **Azure Active Directory Enterprise** とアクセス許可ユーザーの同意  >    >  **設定**  >  [**] を選択します**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)。</span><span class="sxs-lookup"><span data-stu-id="1337c-193">Select **Azure Active Directory** > **Enterprise applications** > **Consent and permissions** > [**User consent settings**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).</span></span>
1. <span data-ttu-id="1337c-194">[アプリケーションに対するユーザーの同意] というラベルの付いたコントロールを使用して、ユーザーの同意を有効 **、無効、または制限します**。</span><span class="sxs-lookup"><span data-stu-id="1337c-194">Enable, disable, or limit user consent with the control labeled **User consent for applications**.</span></span> <span data-ttu-id="1337c-195">既定値は [ **アプリに対するユーザーの同意を許可する] です**。</span><span class="sxs-lookup"><span data-stu-id="1337c-195">The default is **Allow user consent for apps**.</span></span> <span data-ttu-id="1337c-196">チャット メンバーが RSC を使用してアプリをインストールするには、そのユーザーに対してユーザーの同意を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1337c-196">For a chat member to install an app using RSC, user consent must be enabled for that user.</span></span>

    ![Azure RSC チャット構成](../../assets/images/azure-rsc-chat-configuration.png)

<span data-ttu-id="1337c-198">さらに、PowerShell を使用してユーザーの同意を有効または無効にしたり [、PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)を使用してユーザーの同意を構成するで説明されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="1337c-198">In addition, you can enable or disable user consent using PowerShell, follow the steps outlined in [configure user consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-using-the-aad-portal"></a><span data-ttu-id="1337c-199">AAD ポータルを使用Microsoft ID プラットフォームアプリをアプリに登録する</span><span class="sxs-lookup"><span data-stu-id="1337c-199">Register your app with Microsoft identity platform using the AAD portal</span></span>

<span data-ttu-id="1337c-200">AAD ポータルは、アプリを登録および構成する中央プラットフォームを提供します。</span><span class="sxs-lookup"><span data-stu-id="1337c-200">The AAD portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="1337c-201">ID プラットフォームと統合し、Microsoft のサービス API を呼び出すには、アプリを AAD ポータルGraph必要があります。</span><span class="sxs-lookup"><span data-stu-id="1337c-201">Your app must be registered in the AAD portal to integrate with the identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="1337c-202">詳細については、「アプリケーションを [ID プラットフォームに登録する」を参照してください](/graph/auth-register-app-v2)。</span><span class="sxs-lookup"><span data-stu-id="1337c-202">For more information, see [register an application with the identity platform](/graph/auth-register-app-v2).</span></span>

> [!WARNING]
> <span data-ttu-id="1337c-203">AAD アプリ ID を複数のアプリ間で共有Teams必要があります。</span><span class="sxs-lookup"><span data-stu-id="1337c-203">An AAD app ID must not be shared across multiple Teams apps.</span></span> <span data-ttu-id="1337c-204">1 つのアプリと AAD アプリの間に 1:1 Teamsが必要です。</span><span class="sxs-lookup"><span data-stu-id="1337c-204">There must be a 1:1 mapping between a Teams app and an AAD app.</span></span> <span data-ttu-id="1337c-205">同じ AAD アプリ ID にTeams複数のアプリをインストールしようとすると、インストールまたは実行時にエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="1337c-205">Attempts to install multiple Teams apps which are associated with the same AAD app ID will cause installation or runtime failures.</span></span>

## <a name="review-your-application-permissions-in-the-aad-portal"></a><span data-ttu-id="1337c-206">AAD ポータルでアプリケーションのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="1337c-206">Review your application permissions in the AAD portal</span></span>

1. <span data-ttu-id="1337c-207">[ホーム アプリの **登録**  >  **] ページに移動し**、RSC アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="1337c-207">Go to the **Home** > **App registrations** page and select your RSC app.</span></span>
1. <span data-ttu-id="1337c-208">左側 **のウィンドウから [API の** アクセス許可] を選択し、アプリの [構成済み **アクセス許可]** の一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="1337c-208">Choose **API permissions** from the left pane and go through the list of **Configured permissions** for your app.</span></span> <span data-ttu-id="1337c-209">アプリで RSC 呼び出しGraph場合は、そのページのすべてのアクセス許可を削除します。</span><span class="sxs-lookup"><span data-stu-id="1337c-209">If your app only makes RSC Graph API calls, delete all the permissions on that page.</span></span> <span data-ttu-id="1337c-210">アプリで RSC 以外の呼び出しを行う場合は、必要に応じてこれらのアクセス許可を保持します。</span><span class="sxs-lookup"><span data-stu-id="1337c-210">If your app also makes non-RSC calls, keep those permissions as required.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1337c-211">AAD ポータルを使用して RSC アクセス許可を要求することはできません。</span><span class="sxs-lookup"><span data-stu-id="1337c-211">The AAD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="1337c-212">RSC アクセス許可は現在、Teams クライアントにインストールされている Teams アプリケーション専用であり、Teams アプリ マニフェスト (JSON) ファイルで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="1337c-212">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the Teams app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="1337c-213">サーバーからアクセス トークンを取得Microsoft ID プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="1337c-213">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="1337c-214">API 呼びGraphするには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1337c-214">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="1337c-215">アプリが ID プラットフォームからトークンを取得するには、そのトークンを AAD ポータルに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1337c-215">Before your app can get a token from the identity platform, it must be registered in the AAD portal.</span></span> <span data-ttu-id="1337c-216">アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。</span><span class="sxs-lookup"><span data-stu-id="1337c-216">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="1337c-217">ID プラットフォームからアクセス トークンを取得するには、AAD 登録プロセスの次の値が必要です。</span><span class="sxs-lookup"><span data-stu-id="1337c-217">You must have the following values from the AAD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="1337c-218">アプリ **登録ポータルによって** 割り当てられたアプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="1337c-218">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="1337c-219">アプリがシングル サインオン (SSO) をサポートしている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1337c-219">If your app supports single sign-on (SSO) you must use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="1337c-220">クライアント **シークレット/パスワード、** または証明書である公開キーまたは秘密キー **のペア** です。</span><span class="sxs-lookup"><span data-stu-id="1337c-220">The **Client secret/password** or a public or private key pair that is **Certificate**.</span></span> <span data-ttu-id="1337c-221">ネイティブ アプリの場合、これは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="1337c-221">This is not required for native apps.</span></span>
- <span data-ttu-id="1337c-222">AAD **から応答** を受信するアプリのリダイレクト URI または返信 URL。</span><span class="sxs-lookup"><span data-stu-id="1337c-222">A **Redirect URI** or reply URL for your app to receive responses from AAD.</span></span>

<span data-ttu-id="1337c-223">詳細については、「ユーザーに [代わってアクセス権を取得](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) する」および「ユーザーなしで [アクセスを取得する」を参照してください](/graph/auth-v2-service)。</span><span class="sxs-lookup"><span data-stu-id="1337c-223">For more information, see [get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [get access without a user](/graph/auth-v2-service).</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="1337c-224">アプリ マニフェストTeams更新する</span><span class="sxs-lookup"><span data-stu-id="1337c-224">Update your Teams app manifest</span></span>

<span data-ttu-id="1337c-225">RSC アクセス許可は、アプリ マニフェスト JSON ファイルで宣言されます。</span><span class="sxs-lookup"><span data-stu-id="1337c-225">The RSC permissions are declared in your app manifest JSON file.</span></span> <span data-ttu-id="1337c-226">次の [値を使用して、WebApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="1337c-226">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

|<span data-ttu-id="1337c-227">名前</span><span class="sxs-lookup"><span data-stu-id="1337c-227">Name</span></span>| <span data-ttu-id="1337c-228">種類</span><span class="sxs-lookup"><span data-stu-id="1337c-228">Type</span></span> | <span data-ttu-id="1337c-229">説明</span><span class="sxs-lookup"><span data-stu-id="1337c-229">Description</span></span>|
|---|---|---|
|`id` |<span data-ttu-id="1337c-230">文字列</span><span class="sxs-lookup"><span data-stu-id="1337c-230">String</span></span> |<span data-ttu-id="1337c-231">AAD アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="1337c-231">Your AAD app ID.</span></span> <span data-ttu-id="1337c-232">詳細については [、「AAD ポータルにアプリを登録する」を参照してください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="1337c-232">For more information, see [register your app in the AAD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).</span></span>|
|`resource`|<span data-ttu-id="1337c-233">文字列</span><span class="sxs-lookup"><span data-stu-id="1337c-233">String</span></span>| <span data-ttu-id="1337c-234">このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加して値を指定する必要があります。任意の文字列が実行します。</span><span class="sxs-lookup"><span data-stu-id="1337c-234">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>|
|`applicationPermissions`|<span data-ttu-id="1337c-235">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="1337c-235">Array of strings</span></span>|<span data-ttu-id="1337c-236">アプリの RSC アクセス許可。</span><span class="sxs-lookup"><span data-stu-id="1337c-236">RSC permissions for  your app.</span></span> <span data-ttu-id="1337c-237">詳細については、「リソース固有 [のアクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="1337c-237">For more information, see [resource-specific permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>|

>
> [!IMPORTANT]
> <span data-ttu-id="1337c-238">RSC 以外のアクセス許可は Azure portal に格納されます。</span><span class="sxs-lookup"><span data-stu-id="1337c-238">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="1337c-239">アプリ マニフェストに追加しません。</span><span class="sxs-lookup"><span data-stu-id="1337c-239">Do not add them to the app manifest.</span></span>
>

### <a name="example-for-rsc-in-a-team"></a><span data-ttu-id="1337c-240">チームの RSC の例</span><span class="sxs-lookup"><span data-stu-id="1337c-240">Example for RSC in a team</span></span>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.ReadWrite.Group",
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

### <a name="example-for-rsc-in-a-chat"></a><span data-ttu-id="1337c-241">チャット内の RSC の例</span><span class="sxs-lookup"><span data-stu-id="1337c-241">Example for RSC in a chat</span></span>

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

> [!NOTE]
> <span data-ttu-id="1337c-242">アプリがチームスコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を同じマニフェストで指定できます `applicationPermissions` 。</span><span class="sxs-lookup"><span data-stu-id="1337c-242">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="1337c-243">アプリをサイドロードTeams</span><span class="sxs-lookup"><span data-stu-id="1337c-243">Sideload your app in Teams</span></span>

<span data-ttu-id="1337c-244">管理者がTeamsアプリのアップロードを許可している場合は、アプリを特定[](~/concepts/deploy-and-publish/apps-upload.md)のチームまたはチャットに直接サイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="1337c-244">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team or chat.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="1337c-245">アプリで追加された RSC アクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="1337c-245">Check your app for added RSC permissions</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1337c-246">RSC アクセス許可は、ユーザーに属性付けされません。</span><span class="sxs-lookup"><span data-stu-id="1337c-246">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="1337c-247">呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可を使用して行います。</span><span class="sxs-lookup"><span data-stu-id="1337c-247">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="1337c-248">アプリは、タブの削除など、ユーザーが実行できない操作を実行できます。RSC API 呼び出しを行う前に、チーム所有者またはチャット所有者の使用意図を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1337c-248">The app can be allowed to perform actions that the user cannot, such as deleting a tab. You must review the team owner's or chat owner's intent for your use before making RSC API calls.</span></span> <span data-ttu-id="1337c-249">詳細については、「API の概要[Microsoft Teamsを参照してください](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="1337c-249">For more information, see [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="1337c-250">アプリがリソースにインストールされた後、Graph[エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を使用して、リソース内のアプリに付与されたアクセス許可を表示できます。</span><span class="sxs-lookup"><span data-stu-id="1337c-250">After the app has been installed to a resource, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to view the permissions that have been granted to the app in the resource.</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a><span data-ttu-id="1337c-251">チームに追加された RSC アクセス許可をアプリで確認する</span><span class="sxs-lookup"><span data-stu-id="1337c-251">Check your app for added RSC permissions in a team</span></span>

1. <span data-ttu-id="1337c-252">チームの **groupId** を次のTeams。</span><span class="sxs-lookup"><span data-stu-id="1337c-252">Get the team's **groupId** from Teams.</span></span>
1. <span data-ttu-id="1337c-253">[Teams] で、左端 **Teams** ウィンドウから [プロパティ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1337c-253">In Teams, select **Teams** from the leftmost pane.</span></span>
1. <span data-ttu-id="1337c-254">アプリをインストールするチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="1337c-254">Select the team where the app is to be installed.</span></span>
1. <span data-ttu-id="1337c-255">そのチームの省略 &#x25CF;&#x25CF;&#x25CF; を選択します。</span><span class="sxs-lookup"><span data-stu-id="1337c-255">Select the ellipses &#x25CF;&#x25CF;&#x25CF; for that team.</span></span>
1. <span data-ttu-id="1337c-256">[ **チーム] ドロップダウン メニューから [チーム** へのリンクを取得する] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1337c-256">Select **Get link to team** from the team drop-down menu.</span></span>
1. <span data-ttu-id="1337c-257">[チームへのリンク **を取得する** ] ポップアップ ダイアログ ボックスから groupId **値をコピー** して保存します。</span><span class="sxs-lookup"><span data-stu-id="1337c-257">Copy and save the **groupId** value from the **Get a link to the team** pop-up dialog box.</span></span>
1. <span data-ttu-id="1337c-258">エクスプローラーにサインイン **Graphします**。</span><span class="sxs-lookup"><span data-stu-id="1337c-258">Sign in to **Graph Explorer**.</span></span>
1. <span data-ttu-id="1337c-259">このエンドポイント **に GET** 呼び出し `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` を行います。</span><span class="sxs-lookup"><span data-stu-id="1337c-259">Make a **GET** call to this endpoint: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="1337c-260">応答 `clientAppId` のフィールドは、アプリ マニフェスト `webApplicationInfo.id` で指定されたTeamsマップされます。</span><span class="sxs-lookup"><span data-stu-id="1337c-260">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>

    ![Graph RSC アクセス許可の GET 呼び出しに対するエクスプローラーの応答](../../assets/images/team-graph-permissions.png)

<span data-ttu-id="1337c-262">特定のチームにインストールされているアプリの詳細を取得する方法の詳細については、「指定したチームにインストールされているアプリの名前と他の詳細を取得する」 [を参照してください](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)。</span><span class="sxs-lookup"><span data-stu-id="1337c-262">For more information on how to get details of the apps installed in a specific team, see [get the names and other details of apps installed in the specified team](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a><span data-ttu-id="1337c-263">チャットで追加された RSC アクセス許可をアプリで確認する</span><span class="sxs-lookup"><span data-stu-id="1337c-263">Check your app for added RSC permissions in a chat</span></span>

1. <span data-ttu-id="1337c-264">Web クライアントからチャット スレッド ID を *Teamsします。*</span><span class="sxs-lookup"><span data-stu-id="1337c-264">Get the chat thread ID from the Teams *web* client.</span></span>
1. <span data-ttu-id="1337c-265">Web クライアントTeams、左端 **のウィンドウから**[チャット] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1337c-265">In the Teams web client, select **Chat** from the leftmost pane.</span></span>
1. <span data-ttu-id="1337c-266">アプリがインストールされているチャットをドロップダウン メニューから選択します。</span><span class="sxs-lookup"><span data-stu-id="1337c-266">Select the chat where the app is installed from the drop-down menu.</span></span>
1. <span data-ttu-id="1337c-267">Web URL をコピーし、文字列からチャット スレッド ID を保存します。</span><span class="sxs-lookup"><span data-stu-id="1337c-267">Copy the web URL and save the chat thread ID from the string.</span></span>

    ![Web URL からのチャット スレッド ID](../../assets/images/chat-thread-id.png)

1. <span data-ttu-id="1337c-269">エクスプローラーにサインイン **Graphします**。</span><span class="sxs-lookup"><span data-stu-id="1337c-269">Sign in to **Graph Explorer**.</span></span>
1. <span data-ttu-id="1337c-270">次の **エンドポイントに対** して GET 呼び出しを行います `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` 。</span><span class="sxs-lookup"><span data-stu-id="1337c-270">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`.</span></span> <span data-ttu-id="1337c-271">応答 `clientAppId` のフィールドは、アプリ マニフェスト `webApplicationInfo.id` で指定されたTeamsマップされます。</span><span class="sxs-lookup"><span data-stu-id="1337c-271">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>

    ![Graph RSC アクセス許可の GET 呼び出しに対するエクスプローラーの応答](../../assets/images/chat-graph-permissions.png)

<span data-ttu-id="1337c-273">特定のチャットにインストールされているアプリの詳細を取得する方法の詳細については、「指定したチャットにインストールされているアプリの名前と他の詳細を取得する」 [を参照してください](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)。</span><span class="sxs-lookup"><span data-stu-id="1337c-273">For more information on how to get details of apps installed in a specific chat, see [get the names and other details of apps installed in the specified chat](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat).</span></span>

## <a name="code-sample"></a><span data-ttu-id="1337c-274">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="1337c-274">Code sample</span></span>

| <span data-ttu-id="1337c-275">**サンプルの名前**</span><span class="sxs-lookup"><span data-stu-id="1337c-275">**Sample name**</span></span> | <span data-ttu-id="1337c-276">**説明**</span><span class="sxs-lookup"><span data-stu-id="1337c-276">**Description**</span></span> | <span data-ttu-id="1337c-277">**.NET**</span><span class="sxs-lookup"><span data-stu-id="1337c-277">**.NET**</span></span> |<span data-ttu-id="1337c-278">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="1337c-278">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="1337c-279">Resource-Specific同意 (RSC)</span><span class="sxs-lookup"><span data-stu-id="1337c-279">Resource-Specific Consent (RSC)</span></span> | <span data-ttu-id="1337c-280">RSC を使用して API Graph呼び出します。</span><span class="sxs-lookup"><span data-stu-id="1337c-280">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="1337c-281">表示</span><span class="sxs-lookup"><span data-stu-id="1337c-281">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="1337c-282">表示</span><span class="sxs-lookup"><span data-stu-id="1337c-282">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a><span data-ttu-id="1337c-283">関連項目</span><span class="sxs-lookup"><span data-stu-id="1337c-283">See also</span></span>
 
* [<span data-ttu-id="1337c-284">リソース固有の同意のアクセス許可をテストTeams</span><span class="sxs-lookup"><span data-stu-id="1337c-284">Test resource-specific consent permissions in Teams</span></span>](test-resource-specific-consent.md)
* [<span data-ttu-id="1337c-285">管理者向けリソース固有Microsoft Teams同意</span><span class="sxs-lookup"><span data-stu-id="1337c-285">Resource-specific consent in Microsoft Teams for admins</span></span>](/MicrosoftTeams/resource-specific-consent)
