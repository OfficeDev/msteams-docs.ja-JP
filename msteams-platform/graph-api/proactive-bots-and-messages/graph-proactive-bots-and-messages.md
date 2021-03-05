---
title: Microsoft Graph を使用して Teams でのプロアクティブ ボットのインストールとメッセージングを承認する
description: Teams でのプロアクティブ メッセージングと実装方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams プロアクティブ メッセージング チャットのインストール Graph
ms.openlocfilehash: ac59f3408096993379cae490cd555d3b913cc827
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449403"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a><span data-ttu-id="22e58-104">Graph API を使用してアプリをプロアクティブにインストールし、メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="22e58-104">Proactive installation of apps using Graph API and send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="22e58-105">Microsoft Graph と Microsoft Teams のパブリック プレビューは、早期アクセスとフィードバックに利用できます。</span><span class="sxs-lookup"><span data-stu-id="22e58-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="22e58-106">このリリースでは広範なテストが実施されましたが、実稼働環境での使用を意図した製品ではありません。</span><span class="sxs-lookup"><span data-stu-id="22e58-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="22e58-107">Teams でのプロアクティブ メッセージング</span><span class="sxs-lookup"><span data-stu-id="22e58-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="22e58-108">プロアクティブ メッセージはボットによって開始され、ユーザーとの会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="22e58-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="22e58-109">ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="22e58-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="22e58-110">Teams のプロアクティブ メッセージは、アドホックまたは **ダイアログ** ベース **の会話として配信** できます。</span><span class="sxs-lookup"><span data-stu-id="22e58-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="22e58-111">メッセージ型</span><span class="sxs-lookup"><span data-stu-id="22e58-111">Message Type</span></span> | <span data-ttu-id="22e58-112">説明</span><span class="sxs-lookup"><span data-stu-id="22e58-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="22e58-113">アドホックプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="22e58-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="22e58-114">ボットは、会話フローを中断せずにメッセージを対話します。</span><span class="sxs-lookup"><span data-stu-id="22e58-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="22e58-115">ダイアログ ベースのプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="22e58-115">Dialog-based proactive message</span></span> | <span data-ttu-id="22e58-116">ボットは新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じ、コントロールを前のダイアログに返します。</span><span class="sxs-lookup"><span data-stu-id="22e58-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="22e58-117">「ユーザー [にプロアクティブ通知を送信する SDK v4」を参照してください](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="22e58-117">See, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="22e58-118">Teams でのプロアクティブ アプリのインストール</span><span class="sxs-lookup"><span data-stu-id="22e58-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="22e58-119">ボットがユーザーに事前にメッセージを送る前に、個人用アプリまたはユーザーがメンバーであるチームにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="22e58-119">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="22e58-120">アプリをインストールしていない、または以前に操作したユーザーに事前にメッセージを送信する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="22e58-120">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="22e58-121">たとえば、組織内のすべてのユーザーに重要な情報をメッセージする必要があります。</span><span class="sxs-lookup"><span data-stu-id="22e58-121">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="22e58-122">このようなシナリオでは、Microsoft Graph API を使用して、ユーザー向けボットを事前にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="22e58-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="22e58-123">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="22e58-123">Permissions</span></span>

<span data-ttu-id="22e58-124">Microsoft Graph [teamsAppInstallation リソース](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) の種類のアクセス許可は、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) スコープまたはチーム (チャネル) スコープのアプリのインストール ライフサイクルを管理するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="22e58-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="22e58-125">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="22e58-125">Application permission</span></span> | <span data-ttu-id="22e58-126">説明</span><span class="sxs-lookup"><span data-stu-id="22e58-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="22e58-127">Teams アプリは、事前にサインインまたは使用することなく、ユーザーの読み取り、インストール、アップグレード、アンインストールを行えます。</span><span class="sxs-lookup"><span data-stu-id="22e58-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="22e58-128">Teams アプリは、事前サインインや使用を行わずに、任意のチームで自身を読み取り、インストール、アップグレード、アンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="22e58-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="22e58-129">これらのアクセス許可を使用するには、次の値で [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="22e58-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="22e58-130">**id** — Azure ADアプリ ID。</span><span class="sxs-lookup"><span data-stu-id="22e58-130">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="22e58-131">**resource** — アプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="22e58-131">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="22e58-132">インストールは他のユーザー向けなので、ボットにはアプリケーションが必要であり、ユーザーが委任したアクセス許可は必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="22e58-132">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="22e58-133">Azure テナントADは、アプリケーションに明示的に [アクセス許可を付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="22e58-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="22e58-134">アプリケーションにアクセス許可が付与された後、Azure テナントのすべてのADアクセス許可を取得します。</span><span class="sxs-lookup"><span data-stu-id="22e58-134">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="22e58-135">プロアクティブ アプリのインストールとメッセージングを有効にする</span><span class="sxs-lookup"><span data-stu-id="22e58-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="22e58-136">Microsoft Graph は、組織のアプリ カタログ内または AppSource で発行 [された](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) アプリのみを [インストールできます](https://appsource.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="22e58-136">Microsoft Graph can only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="22e58-137">✔ Teams 用のプロアクティブ メッセージング ボットを作成して発行する</span><span class="sxs-lookup"><span data-stu-id="22e58-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="22e58-138">開始するには、組織のアプリ カタログまたは[AppSource](../../bots/how-to/create-a-bot-for-teams.md)で公開されているプロアクティブ[](../../concepts/deploy-and-publish/overview.md)メッセージング機能を備える[](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)Teams 用ボットが[必要です](https://appsource.microsoft.com/)。 [](../../concepts/bots/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="22e58-138">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that is [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="22e58-139">実稼働対応の [**Company Communicator**](../..//samples/app-templates.md#company-communicator) アプリ テンプレートはブロードキャスト メッセージングを許可し、プロアクティブボット アプリケーションを構築する良い基盤です。</span><span class="sxs-lookup"><span data-stu-id="22e58-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="22e58-140">✔アプリを `teamsAppId` 取得する</span><span class="sxs-lookup"><span data-stu-id="22e58-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="22e58-141">**1.** 次の手順 `teamsAppId` が必要です。</span><span class="sxs-lookup"><span data-stu-id="22e58-141">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="22e58-142">組織 `teamsAppId` のアプリ カタログから取得できます。</span><span class="sxs-lookup"><span data-stu-id="22e58-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="22e58-143">**Microsoft Graph ページリファレンス:** [teamsApp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="22e58-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="22e58-144">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="22e58-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="22e58-145">要求はオブジェクトを返す必要 `teamsApp` があります。</span><span class="sxs-lookup"><span data-stu-id="22e58-145">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="22e58-146">返されるオブジェクトは、アプリのカタログによって生成されるアプリ ID であり、Teams アプリ マニフェストで指定した `id` ID とは異なります。</span><span class="sxs-lookup"><span data-stu-id="22e58-146">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="22e58-147">**2.**  個人用スコープ内のユーザーに対してアプリが既にアップロードまたはサイドロードされている場合は、次のように `teamsAppId` 取得できます。</span><span class="sxs-lookup"><span data-stu-id="22e58-147">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="22e58-148">**Microsoft Graph ページリファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="22e58-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="22e58-149">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="22e58-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="22e58-150">**3.** チーム スコープ内のチャネルに対してアプリがアップロードまたはサイドロードされている場合は、次のように `teamsAppId` 取得できます。</span><span class="sxs-lookup"><span data-stu-id="22e58-150">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="22e58-151">**Microsoft Graph ページリファレンス:** [チーム内のアプリを一覧表示する](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="22e58-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="22e58-152">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="22e58-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="22e58-153">結果の一覧を絞り込むには [**、teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) オブジェクトのフィールドをフィルター処理できます。</span><span class="sxs-lookup"><span data-stu-id="22e58-153">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="22e58-154">✔ メッセージ受信者にボットが現在インストールされているかどうかを確認する</span><span class="sxs-lookup"><span data-stu-id="22e58-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="22e58-155">**Microsoft Graph ページリファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="22e58-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="22e58-156">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="22e58-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="22e58-157">この要求は、アプリがインストールされていない場合は空の配列、アプリがインストールされている場合は [単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列を返します。</span><span class="sxs-lookup"><span data-stu-id="22e58-157">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="22e58-158">✔ アプリをインストールする</span><span class="sxs-lookup"><span data-stu-id="22e58-158">✔ Install your app</span></span>

<span data-ttu-id="22e58-159">**Microsoft Graph ページリファレンス:** [ユーザー用アプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="22e58-159">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="22e58-160">**HTTP POST** 要求:</span><span class="sxs-lookup"><span data-stu-id="22e58-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="22e58-161">ユーザーが Microsoft Teams を実行している場合、アプリのインストールはすぐに表示されます。</span><span class="sxs-lookup"><span data-stu-id="22e58-161">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="22e58-162">インストールされているアプリを表示するには、再起動が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="22e58-162">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="22e58-163">✔ 会話の **chatId を取得する**</span><span class="sxs-lookup"><span data-stu-id="22e58-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="22e58-164">アプリがユーザー用にインストールされている場合、ボットは、プロアクティブ メッセージを送信するために必要な情報を含むイベント `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)通知を受信します。</span><span class="sxs-lookup"><span data-stu-id="22e58-164">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="22e58-165">また `chatId` 、次のように取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="22e58-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="22e58-166">**Microsoft Graph ページリファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="22e58-166">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="22e58-167">**1.** アプリが必要です `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="22e58-167">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="22e58-168">持ってない場合は、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="22e58-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="22e58-169">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="22e58-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="22e58-170">応答 **の id** プロパティは、 `teamsAppInstallationId` です。</span><span class="sxs-lookup"><span data-stu-id="22e58-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="22e58-171">**2. 次** の要求を行って、 をフェッチします `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="22e58-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="22e58-172">**HTTP GET 要求** (アクセス許可 — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="22e58-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="22e58-173">応答 **の id** プロパティは、 `chatId` です。</span><span class="sxs-lookup"><span data-stu-id="22e58-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="22e58-174">次の要求を使用 `chatId` して取得できますが、より広範なアクセス許可が必要 `Chat.Read.All` です。</span><span class="sxs-lookup"><span data-stu-id="22e58-174">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="22e58-175">**HTTP GET 要求** (アクセス許可 — `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="22e58-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="22e58-176">✔プロアクティブ メッセージの送信</span><span class="sxs-lookup"><span data-stu-id="22e58-176">✔ Send proactive messages</span></span>

<span data-ttu-id="22e58-177">ボットは、 [ユーザーまたはチーム](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) に対してボットが追加され、すべてのユーザー情報を受信した後に、プロアクティブ メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="22e58-177">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="22e58-178">Teams 管理者向け関連トピック</span><span class="sxs-lookup"><span data-stu-id="22e58-178">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="22e58-179">**Microsoft Teams のアプリのセットアップ ポリシーを管理する**</span><span class="sxs-lookup"><span data-stu-id="22e58-179">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="22e58-180">その他のコード サンプルを見る</span><span class="sxs-lookup"><span data-stu-id="22e58-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="22e58-181">**Teams のプロアクティブ メッセージング コード サンプル**</span><span class="sxs-lookup"><span data-stu-id="22e58-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
