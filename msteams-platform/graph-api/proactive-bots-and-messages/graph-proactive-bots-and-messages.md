---
title: Microsoft Graphを使用して、アクティブボットのインストールとメッセージングを承認Teams
description: インプリTeamsプロアクティブ メッセージングについて説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams プロアクティブ メッセージング チャットのインストール Graph
ms.openlocfilehash: 06b50e5ab8594c257959430383bab5e355af4e06
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566153"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a><span data-ttu-id="adba0-104">Graph API を使用したアプリの事前インストールとメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="adba0-104">Proactive installation of apps using Graph API and send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="adba0-105">Microsoft GraphおよびMicrosoft Teamsパブリック プレビューは、早期アクセスとフィードバックのために利用できます。</span><span class="sxs-lookup"><span data-stu-id="adba0-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="adba0-106">このリリースでは広範なテストが実施されましたが、実稼働環境での使用を意図した製品ではありません。</span><span class="sxs-lookup"><span data-stu-id="adba0-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="adba0-107">プロアクティブ メッセージング (Teams</span><span class="sxs-lookup"><span data-stu-id="adba0-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="adba0-108">プロアクティブ メッセージはボットによって開始され、ユーザーとの会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="adba0-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="adba0-109">ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="adba0-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="adba0-110">インプロアクティブ メッセージTeams、アドホックまたはダイアログ ベース **の会話として配信** できます。</span><span class="sxs-lookup"><span data-stu-id="adba0-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="adba0-111">メッセージ型</span><span class="sxs-lookup"><span data-stu-id="adba0-111">Message Type</span></span> | <span data-ttu-id="adba0-112">説明</span><span class="sxs-lookup"><span data-stu-id="adba0-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="adba0-113">アドホックプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="adba0-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="adba0-114">ボットは、会話フローを中断せずにメッセージを対話します。</span><span class="sxs-lookup"><span data-stu-id="adba0-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="adba0-115">ダイアログ ベースのプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="adba0-115">Dialog-based proactive message</span></span> | <span data-ttu-id="adba0-116">ボットは新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じ、コントロールを前のダイアログに返します。</span><span class="sxs-lookup"><span data-stu-id="adba0-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="adba0-117">アプリのプロアクティブ インストールTeams</span><span class="sxs-lookup"><span data-stu-id="adba0-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="adba0-118">ボットがユーザーに事前にメッセージを送る前に、個人用アプリまたはユーザーがメンバーであるチームにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="adba0-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="adba0-119">アプリをインストールしていない、または以前に操作したユーザーに事前にメッセージを送信する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="adba0-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="adba0-120">たとえば、組織内のすべてのユーザーに重要な情報をメッセージする必要があります。</span><span class="sxs-lookup"><span data-stu-id="adba0-120">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="adba0-121">このようなシナリオでは、Microsoft Graph API を使用して、ユーザー向けボットを事前にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="adba0-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="adba0-122">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="adba0-122">Permissions</span></span>

<span data-ttu-id="adba0-123">Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true)リソースの種類のアクセス許可は、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) スコープまたはチーム (チャネル) スコープのアプリのインストール ライフサイクルを管理するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="adba0-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="adba0-124">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="adba0-124">Application permission</span></span> | <span data-ttu-id="adba0-125">説明</span><span class="sxs-lookup"><span data-stu-id="adba0-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="adba0-126">事前サインインTeams使用せずに、アプリがユーザーの読み取り、インストール、アップグレード、アンインストールを行えます。</span><span class="sxs-lookup"><span data-stu-id="adba0-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="adba0-127">事前サインインTeams使用せずに、アプリが任意のチームで自身を読み取り、インストール、アップグレード、アンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="adba0-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="adba0-128">これらのアクセス許可を使用するには、次の値で [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="adba0-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="adba0-129">**id** — Azure ADアプリ ID。</span><span class="sxs-lookup"><span data-stu-id="adba0-129">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="adba0-130">**resource** — アプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="adba0-130">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="adba0-131">インストールは他のユーザー向けなので、ボットにはアプリケーションが必要であり、ユーザーが委任したアクセス許可は必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="adba0-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="adba0-132">Azure テナントADは、アプリケーションに明示的に [アクセス許可を付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="adba0-132">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="adba0-133">アプリケーションにアクセス許可が付与された後、Azure テナントのすべてのADアクセス許可を取得します。</span><span class="sxs-lookup"><span data-stu-id="adba0-133">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="adba0-134">プロアクティブ アプリのインストールとメッセージングを有効にする</span><span class="sxs-lookup"><span data-stu-id="adba0-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
><span data-ttu-id="adba0-135">Microsoft Graphは、組織のアプリ ストアまたは組織のアプリ ストアに発行されたアプリTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="adba0-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="adba0-136">✔ プロアクティブ メッセージング ボットを作成して発行Teams</span><span class="sxs-lookup"><span data-stu-id="adba0-136">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="adba0-137">開始するには、組織のアプリ ストア[または](../../bots/how-to/create-a-bot-for-teams.md)Teams ストアにある[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)プロアクティブ メッセージング機能を備えるボットが[](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)Teams[必要です](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)。</span><span class="sxs-lookup"><span data-stu-id="adba0-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

>[!TIP]
> <span data-ttu-id="adba0-138">実稼働対応の [**Company Communicator**](../..//samples/app-templates.md#company-communicator)アプリ テンプレートはブロードキャスト メッセージングを許可し、プロアクティブボット アプリケーションを構築する良い基盤です。</span><span class="sxs-lookup"><span data-stu-id="adba0-138">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="adba0-139">✔アプリを `teamsAppId` 取得する</span><span class="sxs-lookup"><span data-stu-id="adba0-139">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="adba0-140">**1.** 次の手順 `teamsAppId` が必要です。</span><span class="sxs-lookup"><span data-stu-id="adba0-140">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="adba0-141">組織 `teamsAppId` のアプリ カタログから取得できます。</span><span class="sxs-lookup"><span data-stu-id="adba0-141">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="adba0-142">**Microsoft Graph ページリファレンス:** [teamsApp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="adba0-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="adba0-143">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="adba0-143">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="adba0-144">要求はオブジェクトを返す必要 `teamsApp` があります。</span><span class="sxs-lookup"><span data-stu-id="adba0-144">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="adba0-145">返されるオブジェクトは、アプリのカタログによって生成されるアプリ ID であり、アプリ マニフェストで指定した ID とは `id` Teams異なります。</span><span class="sxs-lookup"><span data-stu-id="adba0-145">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="adba0-146">**2.**  個人用スコープ内のユーザーに対してアプリが既にアップロードまたはサイドロードされている場合は、次のように `teamsAppId` 取得できます。</span><span class="sxs-lookup"><span data-stu-id="adba0-146">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="adba0-147">**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="adba0-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="adba0-148">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="adba0-148">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="adba0-149">**3.** チーム スコープ内のチャネルに対してアプリがアップロードまたはサイドロードされている場合は、次のように `teamsAppId` 取得できます。</span><span class="sxs-lookup"><span data-stu-id="adba0-149">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="adba0-150">**Microsoft Graph ページ リファレンス:** [チーム内のアプリの一覧](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="adba0-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="adba0-151">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="adba0-151">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="adba0-152">結果の一覧を絞り込むには [**、teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) オブジェクトのフィールドをフィルター処理できます。</span><span class="sxs-lookup"><span data-stu-id="adba0-152">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="adba0-153">✔ メッセージ受信者にボットが現在インストールされているかどうかを確認する</span><span class="sxs-lookup"><span data-stu-id="adba0-153">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="adba0-154">**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="adba0-154">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="adba0-155">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="adba0-155">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="adba0-156">この要求は、アプリがインストールされていない場合は空の配列、アプリがインストールされている場合は [単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列を返します。</span><span class="sxs-lookup"><span data-stu-id="adba0-156">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="adba0-157">✔ アプリをインストールする</span><span class="sxs-lookup"><span data-stu-id="adba0-157">✔ Install your app</span></span>

<span data-ttu-id="adba0-158">**Microsoft Graph ページ リファレンス:** [ユーザー用アプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="adba0-158">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="adba0-159">**HTTP POST** 要求:</span><span class="sxs-lookup"><span data-stu-id="adba0-159">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="adba0-160">ユーザーが実行中のMicrosoft Teams、アプリのインストールがすぐに表示されます。</span><span class="sxs-lookup"><span data-stu-id="adba0-160">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="adba0-161">インストールされているアプリを表示するには、再起動が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="adba0-161">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="adba0-162">✔ 会話の **chatId を取得する**</span><span class="sxs-lookup"><span data-stu-id="adba0-162">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="adba0-163">アプリがユーザー用にインストールされている場合、ボットは、プロアクティブ メッセージを送信するために必要な情報を含むイベント `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)通知を受信します。</span><span class="sxs-lookup"><span data-stu-id="adba0-163">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="adba0-164">また `chatId` 、次のように取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="adba0-164">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="adba0-165">**Microsoft Graph ページ リファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="adba0-165">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="adba0-166">**1.** アプリが必要です `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="adba0-166">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="adba0-167">持ってない場合は、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="adba0-167">If you don't have it, use the following:</span></span>

<span data-ttu-id="adba0-168">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="adba0-168">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="adba0-169">応答 **の id** プロパティは、 `teamsAppInstallationId` です。</span><span class="sxs-lookup"><span data-stu-id="adba0-169">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="adba0-170">**2. 次** の要求を行って、 をフェッチします `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="adba0-170">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="adba0-171">**HTTP GET 要求** (アクセス許可 — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="adba0-171">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="adba0-172">応答 **の id** プロパティは、 `chatId` です。</span><span class="sxs-lookup"><span data-stu-id="adba0-172">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="adba0-173">次の要求を使用 `chatId` して取得できますが、より広範なアクセス許可が必要 `Chat.Read.All` です。</span><span class="sxs-lookup"><span data-stu-id="adba0-173">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="adba0-174">**HTTP GET 要求** (アクセス許可 — `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="adba0-174">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="adba0-175">✔プロアクティブ メッセージの送信</span><span class="sxs-lookup"><span data-stu-id="adba0-175">✔ Send proactive messages</span></span>

<span data-ttu-id="adba0-176">ボットは、 [ユーザーまたはチーム](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) に対してボットが追加され、すべてのユーザー情報を受信した後に、プロアクティブ メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="adba0-176">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="see-also"></a><span data-ttu-id="adba0-177">関連項目</span><span class="sxs-lookup"><span data-stu-id="adba0-177">See also</span></span>

* [<span data-ttu-id="adba0-178">**Microsoft Teams のアプリのセットアップ ポリシーを管理する**</span><span class="sxs-lookup"><span data-stu-id="adba0-178">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="adba0-179">ユーザーにプロアクティブ通知を送信する SDK v4</span><span class="sxs-lookup"><span data-stu-id="adba0-179">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a><span data-ttu-id="adba0-180">その他のコード サンプルを見る</span><span class="sxs-lookup"><span data-stu-id="adba0-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="adba0-181">**Teams のプロアクティブ メッセージング コード サンプル**</span><span class="sxs-lookup"><span data-stu-id="adba0-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)