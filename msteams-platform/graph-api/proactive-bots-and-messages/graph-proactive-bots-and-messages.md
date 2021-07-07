---
title: Microsoft Graphを使用して、アクティブボットのインストールとメッセージングを承認Teams
description: インプリTeamsプロアクティブ メッセージングについて説明します。
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: Teams プロアクティブ メッセージング チャットのインストール Graph
ms.openlocfilehash: 0f59a74cc24b7d80dd3afd4aa4369a47d56e4d59
ms.sourcegitcommit: a6253e89cb8c8c34d45b06e08c9668daeebc30a3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2021
ms.locfileid: "53300306"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a><span data-ttu-id="8489d-104">Graph API を使用してメッセージを送信するアプリの事前インストール</span><span class="sxs-lookup"><span data-stu-id="8489d-104">Proactive installation of apps using Graph API to send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="8489d-105">Microsoft GraphおよびMicrosoft Teamsパブリック プレビューは、早期アクセスとフィードバックのために利用できます。</span><span class="sxs-lookup"><span data-stu-id="8489d-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="8489d-106">このリリースでは広範なテストが実施されましたが、実稼働環境での使用を意図した製品ではありません。</span><span class="sxs-lookup"><span data-stu-id="8489d-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="8489d-107">プロアクティブ メッセージング (Teams</span><span class="sxs-lookup"><span data-stu-id="8489d-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="8489d-108">プロアクティブ メッセージはボットによって開始され、ユーザーとの会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="8489d-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="8489d-109">ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="8489d-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="8489d-110">インプロアクティブ メッセージTeams、アドホックまたはダイアログ ベース **の会話として配信** できます。</span><span class="sxs-lookup"><span data-stu-id="8489d-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="8489d-111">メッセージの種類</span><span class="sxs-lookup"><span data-stu-id="8489d-111">Message type</span></span> | <span data-ttu-id="8489d-112">説明</span><span class="sxs-lookup"><span data-stu-id="8489d-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="8489d-113">アドホックプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="8489d-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="8489d-114">ボットは、会話フローを中断せずにメッセージを対話します。</span><span class="sxs-lookup"><span data-stu-id="8489d-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="8489d-115">ダイアログ ベースのプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="8489d-115">Dialog-based proactive message</span></span> | <span data-ttu-id="8489d-116">ボットは新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じ、コントロールを前のダイアログに返します。</span><span class="sxs-lookup"><span data-stu-id="8489d-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="8489d-117">アプリのプロアクティブ インストールTeams</span><span class="sxs-lookup"><span data-stu-id="8489d-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="8489d-118">ボットがユーザーに事前にメッセージを送る前に、個人用アプリまたはユーザーがメンバーであるチームにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8489d-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="8489d-119">アプリをインストールしていない、または以前に操作したユーザーに事前にメッセージを送信する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="8489d-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="8489d-120">たとえば、組織内のすべてのユーザーに重要な情報をメッセージする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8489d-120">For example, the need to message important information to everyone in your organization.</span></span> <span data-ttu-id="8489d-121">このようなシナリオでは、Microsoft Graph API を使用して、ユーザー向けボットを事前にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="8489d-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="8489d-122">Permissions</span><span class="sxs-lookup"><span data-stu-id="8489d-122">Permissions</span></span>

<span data-ttu-id="8489d-123">Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true)リソースの種類のアクセス許可は、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) スコープまたはチーム (チャネル) スコープのアプリのインストール ライフサイクルを管理するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="8489d-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions help you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="8489d-124">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="8489d-124">Application permission</span></span> | <span data-ttu-id="8489d-125">説明</span><span class="sxs-lookup"><span data-stu-id="8489d-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="8489d-126">事前サインインTeams使用せずに、アプリがユーザーの読み取り、インストール、アップグレード、アンインストールを行えます。</span><span class="sxs-lookup"><span data-stu-id="8489d-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any *user*, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="8489d-127">事前サインインTeams使用せずに、アプリが任意のチームで自身を読み取り、インストール、アップグレード、アンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="8489d-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any *team*, without prior sign in or use.</span></span>|

<span data-ttu-id="8489d-128">これらのアクセス許可を使用するには、次の値で [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8489d-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

* <span data-ttu-id="8489d-129">**id**: Azure Active Directory (AAD) アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="8489d-129">**id**: Your Azure Active Directory (AAD) app ID.</span></span>
* <span data-ttu-id="8489d-130">**resource**: アプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="8489d-130">**resource**: The resource URL for the app.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="8489d-131">インストールは他のユーザー向けなので、ボットにはアプリケーションが必要であり、ユーザーが委任したアクセス許可は必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="8489d-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="8489d-132">AAD テナント管理者は、アプリケーション [に明示的にアクセス許可を付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="8489d-132">An AAD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="8489d-133">アプリケーションにアクセス許可が付与された後、AAD テナントのすべてのメンバーが付与されたアクセス許可を取得します。</span><span class="sxs-lookup"><span data-stu-id="8489d-133">After the application is granted permissions, all members of the AAD tenant get the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="8489d-134">プロアクティブ アプリのインストールとメッセージングを有効にする</span><span class="sxs-lookup"><span data-stu-id="8489d-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8489d-135">Microsoft Graphは、組織のアプリ ストアまたは組織のアプリ ストアに発行されたアプリTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="8489d-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="8489d-136">ユーザー向けプロアクティブ メッセージング ボットを作成してTeams</span><span class="sxs-lookup"><span data-stu-id="8489d-136">Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="8489d-137">開始するには、組織のアプリ ストア[または](../../bots/how-to/create-a-bot-for-teams.md)Teams ストアにある[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)プロアクティブ メッセージング機能を備えるボット[](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)がTeams[必要です](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)。</span><span class="sxs-lookup"><span data-stu-id="8489d-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that is in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

> [!TIP]
> <span data-ttu-id="8489d-138">実稼働対応の [*Company Communicator*](../..//samples/app-templates.md#company-communicator)アプリ テンプレートを使用すると、ブロードキャスト メッセージングが許可され、プロアクティブボット アプリケーションを構築できます。</span><span class="sxs-lookup"><span data-stu-id="8489d-138">The production-ready [*Company Communicator*](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good start to build your proactive bot application.</span></span>

### <a name="get-the-teamsappid-for-your-app"></a><span data-ttu-id="8489d-139">アプリの `teamsAppId` 取得</span><span class="sxs-lookup"><span data-stu-id="8489d-139">Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="8489d-140">次の方法 `teamsAppId` で取得できます。</span><span class="sxs-lookup"><span data-stu-id="8489d-140">You can retrieve the `teamsAppId` in the following ways:</span></span>

* <span data-ttu-id="8489d-141">組織のアプリ カタログから:</span><span class="sxs-lookup"><span data-stu-id="8489d-141">From your organization's app catalog:</span></span>

    <span data-ttu-id="8489d-142">**Microsoft Graph ページリファレンス:** [teamsApp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8489d-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

    <span data-ttu-id="8489d-143">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8489d-143">**HTTP GET** request:</span></span>

    ```http
        GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    <span data-ttu-id="8489d-144">要求は、アプリのカタログ生成アプリ ID であるオブジェクト `teamsApp` `id` を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="8489d-144">The request must return a `teamsApp` object `id`, which is the app's catalog generated app ID.</span></span> <span data-ttu-id="8489d-145">これは、アプリ マニフェストで指定した ID とはTeamsです。</span><span class="sxs-lookup"><span data-stu-id="8489d-145">This is different from the ID that you provided in your Teams app manifest:</span></span>

    ```json
    {
      "value": [
        {
          "id": "b1c5353a-7aca-41b3-830f-27d5218fe0e5",
          "externalId": "f31b1263-ba99-435a-a679-911d24850d7c",
          "name": "Test App",
          "version": "1.0.1",
          "distributionMethod": "Organization"
        }
      ]
    }
    ```

* <span data-ttu-id="8489d-146">個人用スコープ内のユーザーに対してアプリが既にアップロードまたはサイドロードされている場合:</span><span class="sxs-lookup"><span data-stu-id="8489d-146">If your app has already been uploaded or sideloaded for a user in personal scope:</span></span>

    <span data-ttu-id="8489d-147">**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8489d-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

    <span data-ttu-id="8489d-148">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8489d-148">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* <span data-ttu-id="8489d-149">チーム スコープ内のチャネルに対してアプリが既にアップロードまたはサイドロードされている場合:</span><span class="sxs-lookup"><span data-stu-id="8489d-149">If your app has already been uploaded or sideloaded for a channel in team scope:</span></span>

    <span data-ttu-id="8489d-150">**Microsoft Graph ページ リファレンス:** [チーム内のアプリの一覧](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8489d-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

    <span data-ttu-id="8489d-151">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8489d-151">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > <span data-ttu-id="8489d-152">結果の一覧を絞り込むには [**、teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) オブジェクトのフィールドをフィルター処理できます。</span><span class="sxs-lookup"><span data-stu-id="8489d-152">To narrow the list of results, you can filter any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="8489d-153">メッセージ受信者にボットが現在インストールされているかどうかを確認する</span><span class="sxs-lookup"><span data-stu-id="8489d-153">Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="8489d-154">メッセージ受信者に対してボットが現在インストールされているかどうかを確認するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="8489d-154">You can determine whether your bot is currently installed for a message recipient as follows:</span></span>

<span data-ttu-id="8489d-155">**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8489d-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="8489d-156">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8489d-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="8489d-157">要求は次の値を返します。</span><span class="sxs-lookup"><span data-stu-id="8489d-157">The request returns:</span></span>

* <span data-ttu-id="8489d-158">アプリがインストールされていない場合は空の配列。</span><span class="sxs-lookup"><span data-stu-id="8489d-158">An empty array if the app is not installed.</span></span>
* <span data-ttu-id="8489d-159">アプリがインストールされている場合 [、単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列。</span><span class="sxs-lookup"><span data-stu-id="8489d-159">An array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="install-your-app"></a><span data-ttu-id="8489d-160">アプリをインストールする</span><span class="sxs-lookup"><span data-stu-id="8489d-160">Install your app</span></span>

<span data-ttu-id="8489d-161">アプリは次のようにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="8489d-161">You can install your app as follows:</span></span>

<span data-ttu-id="8489d-162">**Microsoft Graph ページ リファレンス:** [ユーザー用アプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8489d-162">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="8489d-163">**HTTP POST** 要求:</span><span class="sxs-lookup"><span data-stu-id="8489d-163">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="8489d-164">ユーザーが実行中のMicrosoft Teams、アプリのインストールが直ちに行われます。</span><span class="sxs-lookup"><span data-stu-id="8489d-164">If the user has Microsoft Teams running, app installation occurs immediately.</span></span> <span data-ttu-id="8489d-165">インストールされているアプリを表示するには、再起動が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="8489d-165">A restart may be required to view the installed app.</span></span>

### <a name="retrieve-the-conversation-chatid"></a><span data-ttu-id="8489d-166">会話を取得する `chatId`</span><span class="sxs-lookup"><span data-stu-id="8489d-166">Retrieve the conversation `chatId`</span></span>

<span data-ttu-id="8489d-167">アプリがユーザー用にインストールされている場合、ボットは、プロアクティブ メッセージを送信するために必要な情報を含むイベント `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)通知を受信します。</span><span class="sxs-lookup"><span data-stu-id="8489d-167">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="8489d-168">**Microsoft Graph ページ リファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8489d-168">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

1. <span data-ttu-id="8489d-169">アプリが必要です `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="8489d-169">You must have your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="8489d-170">持ってない場合は、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="8489d-170">If you do not have it, use the following:</span></span>

    <span data-ttu-id="8489d-171">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8489d-171">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    <span data-ttu-id="8489d-172">応答 **の id** プロパティは、 `teamsAppInstallationId` です。</span><span class="sxs-lookup"><span data-stu-id="8489d-172">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

1. <span data-ttu-id="8489d-173">フェッチする次の要求を行います `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="8489d-173">Make the following request to fetch the `chatId`:</span></span>

    <span data-ttu-id="8489d-174">**HTTP GET 要求** (アクセス許可 — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="8489d-174">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    <span data-ttu-id="8489d-175">応答 **の id** プロパティは、 `chatId` です。</span><span class="sxs-lookup"><span data-stu-id="8489d-175">The **id** property of the response is the `chatId`.</span></span>

    <span data-ttu-id="8489d-176">次の要求を使用 `chatId` して取得できますが、より広範なアクセス許可が必要 `Chat.Read.All` です。</span><span class="sxs-lookup"><span data-stu-id="8489d-176">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

    <span data-ttu-id="8489d-177">**HTTP GET 要求** (アクセス許可 — `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="8489d-177">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a><span data-ttu-id="8489d-178">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="8489d-178">Send proactive messages</span></span>

<span data-ttu-id="8489d-179">ボットは、 [ユーザーまたはチーム](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) に対してボットが追加され、すべてのユーザー情報を受信した後に、プロアクティブ メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="8489d-179">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team, and has received all the user information.</span></span>

## <a name="code-sample"></a><span data-ttu-id="8489d-180">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="8489d-180">Code sample</span></span>

| <span data-ttu-id="8489d-181">**サンプルの名前**</span><span class="sxs-lookup"><span data-stu-id="8489d-181">**Sample Name**</span></span> | <span data-ttu-id="8489d-182">**説明**</span><span class="sxs-lookup"><span data-stu-id="8489d-182">**Description**</span></span> | <span data-ttu-id="8489d-183">**.NET**</span><span class="sxs-lookup"><span data-stu-id="8489d-183">**.NET**</span></span> | <span data-ttu-id="8489d-184">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="8489d-184">**Node.js**</span></span> |
|---------------|--------------|--------|-------------|--------|
| <span data-ttu-id="8489d-185">アプリのプロアクティブ インストールとプロアクティブ通知の送信</span><span class="sxs-lookup"><span data-stu-id="8489d-185">Proactive installation of app and sending proactive notifications</span></span> | <span data-ttu-id="8489d-186">このサンプルでは、ユーザーに対してアプリのプロアクティブ インストールを使用し、Microsoft の API を呼び出してプロアクティブ通知Graph示します。</span><span class="sxs-lookup"><span data-stu-id="8489d-186">This sample shows how you can use proactive installation of app for users and send proactive notifications by calling Microsoft Graph APIs.</span></span> | [<span data-ttu-id="8489d-187">View</span><span class="sxs-lookup"><span data-stu-id="8489d-187">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [<span data-ttu-id="8489d-188">View</span><span class="sxs-lookup"><span data-stu-id="8489d-188">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="see-also"></a><span data-ttu-id="8489d-189">関連項目</span><span class="sxs-lookup"><span data-stu-id="8489d-189">See also</span></span>

* [<span data-ttu-id="8489d-190">**アプリのセットアップ ポリシーを管理Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="8489d-190">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="8489d-191">ユーザーにプロアクティブ通知を送信する SDK v4</span><span class="sxs-lookup"><span data-stu-id="8489d-191">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="additional-code-samples"></a><span data-ttu-id="8489d-192">追加のコード サンプル</span><span class="sxs-lookup"><span data-stu-id="8489d-192">Additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8489d-193">**Teams のプロアクティブ メッセージング コード サンプル**</span><span class="sxs-lookup"><span data-stu-id="8489d-193">**Teams proactive messaging code samples**</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
