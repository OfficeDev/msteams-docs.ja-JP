---
title: Microsoft Graph を使用して、Teams でプロアクティブ ボット インストールとメッセージングを有効にする
description: Teams のプロアクティブ メッセージングと実装方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams プロアクティブなメッセージング チャットのインストール Graph
ms.openlocfilehash: b601c5858e5141ce81985dca62968b1713e1d2ba
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819162"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="2a07d-104">Microsoft Graph を使用して Teams のプロアクティブ ボットのインストールとプロアクティブなメッセージングを有効にする (パブリック プレビュー)</span><span class="sxs-lookup"><span data-stu-id="2a07d-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="2a07d-105">Microsoft Graph と Microsoft Teams のパブリック プレビューは、すでにアクセスしてフィードバックを行います。</span><span class="sxs-lookup"><span data-stu-id="2a07d-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="2a07d-106">このリリースは、拡張的なテストを受けてきてきてきませんが、運用環境での使用を意図したものではありません。</span><span class="sxs-lookup"><span data-stu-id="2a07d-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="2a07d-107">Teams でのプロアクティブ メッセージング</span><span class="sxs-lookup"><span data-stu-id="2a07d-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="2a07d-108">ユーザーとの会話を開始するために、プロアクティブ メッセージがボットによって開始されます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="2a07d-109">ウェルカム メッセージの送信、アンケートや投資の実行、組織全体の通知のブロードキャストなど、多くの目的に使用できます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="2a07d-110">Teams のプロアクティブ メッセージは、アドホックまたは**ダイアログ ベースの会話\*\*\*\*として配信**できます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="2a07d-111">メッセージ型</span><span class="sxs-lookup"><span data-stu-id="2a07d-111">Message Type</span></span> | <span data-ttu-id="2a07d-112">Description</span><span class="sxs-lookup"><span data-stu-id="2a07d-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="2a07d-113">アドホックのプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="2a07d-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="2a07d-114">ボットは会話フローを中断することなくメッセージを挿入します。</span><span class="sxs-lookup"><span data-stu-id="2a07d-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="2a07d-115">ダイアログベースのプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="2a07d-115">Dialog-based proactive message</span></span> | <span data-ttu-id="2a07d-116">ボットは新しいダイアログ スレッドを作成し、会話の制御を取得し、プロアクティブ メッセージを配信し、コントロールを閉じて前のダイアログに制御を返します。</span><span class="sxs-lookup"><span data-stu-id="2a07d-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="2a07d-117">*「ユーザー* [SDK v4 へのプロアクティブ通知の送信」をご覧ください。](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span><span class="sxs-lookup"><span data-stu-id="2a07d-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="2a07d-118">Teams でのアプリのプロアクティブなインストール</span><span class="sxs-lookup"><span data-stu-id="2a07d-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="2a07d-119">ボットがユーザーにプロアクティブにメッセージを送信するには、その前に、個人用アプリとして、またはユーザーがメンバーであるチームにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a07d-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="2a07d-120">場合によっては、インストールしていない、または以前にアプリを操作した _ユーザーにメッセージ_ を、表示しないように促す必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a07d-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="2a07d-121">たとえば、組織内のすべてのユーザーに対して、必要な情報をメッセージで送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a07d-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="2a07d-122">そのようなシナリオでは、Microsoft Graph API を使用して、ユーザー用にボットをプロアクティブにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="2a07d-123">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="2a07d-123">Permissions</span></span>

<span data-ttu-id="2a07d-124">Microsoft Graph [teamsAppInstallation リソースの種類の](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) アクセス許可を使用すると、Microsoft Teams プラットフォーム内のすべてのユーザー (個人) またはチーム (チャネル) スコープに対するアプリのインストール ライフサイクルを管理できます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="2a07d-125">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="2a07d-125">Application permission</span></span> | <span data-ttu-id="2a07d-126">Description</span><span class="sxs-lookup"><span data-stu-id="2a07d-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="2a07d-127">以前のサインインや使用をすることなく、Teams アプリで、すべてのユーザーに対してそれ **自体の**読み取り、インストール、アップグレード、アンインストールを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="2a07d-128">Teams アプリで、以前のサインインや使用をせずに、任意のチームでそれ自体の読み **取**り、インストール、アップグレード、アンインストールを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="2a07d-129">これらのアクセス許可を使用するには、次の値 [を使用して、アプリ](../../resources/schema/manifest-schema.md#webapplicationinfo) マニフェストに webApplicationInfo キーを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a07d-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="2a07d-130">**id**  — Azure AD アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="2a07d-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="2a07d-131">**resource** — アプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="2a07d-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="2a07d-132">ボットのインストール_は、ユーザー__に代用するもの_ではありませんが、他のユーザーに対してはインストールされないため、アプリケーションには、ユーザーに委任されたアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="2a07d-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="2a07d-133">テナント管理者が Azure ADは、アプリケーション [にアクセス許可を明示的に付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="2a07d-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="2a07d-134">アプリケーションにアクセス許可が付与されると _、テナント_ テナントのすべてのメンバーにADアクセス許可が付与されます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="2a07d-135">プロアクティブ アプリのインストールとメッセージングを有効にする</span><span class="sxs-lookup"><span data-stu-id="2a07d-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="2a07d-136">Microsoft Graph は、組織のアプリ カタログ内または AppSource 内に [公開された](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) アプリのみを [インストールします](https://appsource.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="2a07d-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="2a07d-137">✔ Teams のプロアクティブ メッセージング ボットを作成して公開する</span><span class="sxs-lookup"><span data-stu-id="2a07d-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="2a07d-138">開始するには、プロアクティブ メッセージング機能を使用し、[proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md)組織のアプリ カタログまたは[published](../../concepts/deploy-and-publish/overview.md)AppSource で公開[される Teams](../../bots/how-to/create-a-bot-for-teams.md) [用ボ](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)ットが[必要です](https://appsource.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="2a07d-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="2a07d-139">運用環境に適した [**会社のCommunicator、**](../..//samples/app-templates.md#company-communicator) ブロードキャスト メッセージングを有効にして、プロアクティブなボット アプリケーションを構築するための基盤になります。</span><span class="sxs-lookup"><span data-stu-id="2a07d-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="2a07d-140">✔アプリを `teamsAppId` 取得する</span><span class="sxs-lookup"><span data-stu-id="2a07d-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="2a07d-141">**1.** 次の `teamsAppId`  手順に進んでください。</span><span class="sxs-lookup"><span data-stu-id="2a07d-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="2a07d-142">組織 `teamsAppId` のアプリ カタログから取得できます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="2a07d-143">**Microsoft Graph ページ リファレンス:** [teamsApp リソース タイプ](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span><span class="sxs-lookup"><span data-stu-id="2a07d-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span></span>

<span data-ttu-id="2a07d-144">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="2a07d-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="2a07d-145">要求はオブジェクトを返 `teamsApp`  します。</span><span class="sxs-lookup"><span data-stu-id="2a07d-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="2a07d-146">返されたオブジェクトのカタログ `id`  は、アプリのカタログに生成されたアプリ ID で、Teams アプリ マニフェストに指定した "id:" とは異なります。</span><span class="sxs-lookup"><span data-stu-id="2a07d-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="2a07d-147">**2.**  個人用スコープでユーザーのアプリが既にアップロードまたはサイドローディングされている場合は、次のように `teamsAppId` して取得できます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-147">**2.**  If your app has already been uploaded/sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="2a07d-148">**Microsoft Graph ページ リファレンス: ユーザーにインストール**[されたアプリを一覧表示する](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="2a07d-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="2a07d-149">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="2a07d-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="2a07d-150">**3.** チームのスコープでチャネル用にアプリが既にアップロードまたはサイドロードされている場合は、次のように `teamsAppId` して取得できます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="2a07d-151">**Microsoft Graph ページ リファレンス:** [チーム内のアプリを一覧表示する](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="2a07d-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="2a07d-152">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="2a07d-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="2a07d-153">[**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0)オブジェクトのいずれかのフィールドでフィルター処理して結果リストを絞り込むことができます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="2a07d-154">✔メッセージ受信者にボットが現在インストールされているかどうかを確認する</span><span class="sxs-lookup"><span data-stu-id="2a07d-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="2a07d-155">**Microsoft Graph ページ リファレンス: ユーザーにインストール**[されたアプリを一覧表示する](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="2a07d-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="2a07d-156">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="2a07d-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="2a07d-157">この要求は、アプリがインストールされていない場合は空の配列を返し、インストールされている [場合は、単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) オブジェクトの配列を返します。</span><span class="sxs-lookup"><span data-stu-id="2a07d-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="2a07d-158">✔をインストールする</span><span class="sxs-lookup"><span data-stu-id="2a07d-158">✔ Install your app</span></span>

<span data-ttu-id="2a07d-159">**Microsoft Graph リファレンス: ユーザー**[用アプリをインストールする](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="2a07d-159">**Microsoft Graph reference:** [Install app for user](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="2a07d-160">**HTTP POST** 要求:</span><span class="sxs-lookup"><span data-stu-id="2a07d-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="2a07d-161">ユーザーが Microsoft Teams を実行している場合は、アプリのインストールがすぐに表示される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2a07d-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="2a07d-162">または、インストール済みアプリを表示するには、再起動が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="2a07d-162">Alternatively,  a  restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="2a07d-163">✔ **chatId を取得する**</span><span class="sxs-lookup"><span data-stu-id="2a07d-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="2a07d-164">アプリがユーザー用にインストールされると、ボットはイベント通知を受け取り、プロアクティブ メッセージを `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)送信するために必要な情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2a07d-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="2a07d-165">`chatId`次のように取得できる。</span><span class="sxs-lookup"><span data-stu-id="2a07d-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="2a07d-166">**Microsoft Graph リファレンス:** [チャットを取得する](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="2a07d-166">**Microsoft Graph reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="2a07d-167">**1.** アプリが必要になります `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="2a07d-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="2a07d-168">使用しない場合は、以下を使用します。</span><span class="sxs-lookup"><span data-stu-id="2a07d-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="2a07d-169">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="2a07d-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="2a07d-170">応答 **の id** プロパティは次の場所です `teamsAppInstallationId` 。</span><span class="sxs-lookup"><span data-stu-id="2a07d-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="2a07d-171">**2. 次** のような要求を行ってフェッチします `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="2a07d-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="2a07d-172">**HTTP GET 要求** (アクセス許可 `TeamsAppInstallation.ReadWriteSelfForUser.All` —</span><span class="sxs-lookup"><span data-stu-id="2a07d-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="2a07d-173">応答 **の id** プロパティは次の場所です `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="2a07d-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="2a07d-174">または、次の要求で `chatId`  取得できますが、より広範なアクセス許可が必要 `Chat.Read.All` になります。</span><span class="sxs-lookup"><span data-stu-id="2a07d-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="2a07d-175">**HTTP GET 要求** (アクセス許可 `Chat.Read.All` —</span><span class="sxs-lookup"><span data-stu-id="2a07d-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="2a07d-176">✔アクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="2a07d-176">✔ Send proactive messages</span></span>

<span data-ttu-id="2a07d-177">ユーザーまたはチームにボットが追加され、必要なユーザー情報を取得したら、プロアクティブ メッセージ [を送信できるようになります](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)。</span><span class="sxs-lookup"><span data-stu-id="2a07d-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="2a07d-178">C# / .NET</span><span class="sxs-lookup"><span data-stu-id="2a07d-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="2a07d-179">次のコード スニペットは [、Microsoft Bot Framework Samples for C# のサンプルのスニペットです。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="2a07d-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

```csharp
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Bot.Builder;
using Microsoft.Bot.Schema;

namespace Microsoft.BotBuilderSamples
{
    public class ProactiveBot : ActivityHandler
    {
        // Message to send to users when the bot receives a Conversation Update event
        private const string WelcomeMessage = "Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.";

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

        public ProactiveBot(ConcurrentDictionary<string, ConversationReference> conversationReferences)
        {
            _conversationReferences = conversationReferences;
        }

        private void AddConversationReference(Activity activity)
        {
            var conversationReference = activity.GetConversationReference();
            _conversationReferences.AddOrUpdate(conversationReference.User.Id, conversationReference, (key, newValue) => conversationReference);
        }

        protected override Task OnConversationUpdateActivityAsync(ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            return base.OnConversationUpdateActivityAsync(turnContext, cancellationToken);
        }

        protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            foreach (var member in membersAdded)
            {
                // Greet anyone that was not the target (recipient) of this message.
                if (member.Id != turnContext.Activity.Recipient.Id)
                {
                    await turnContext.SendActivityAsync(MessageFactory.Text(WelcomeMessage), cancellationToken);
                }
            }
        }

        protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            // Echo back what the user said
            await turnContext.SendActivityAsync(MessageFactory.Text($"You sent '{turnContext.Activity.Text}'"), cancellationToken);
        }
    }
}
```

# <a name="javascript"></a>[<span data-ttu-id="2a07d-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2a07d-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="2a07d-181">次のコード スニペットは [、JavaScript 用 Microsoft Bot Framework サンプルのものです](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。</span><span class="sxs-lookup"><span data-stu-id="2a07d-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

```javascript
const { ActivityHandler, TurnContext } = require('botbuilder');

class ProactiveBot extends ActivityHandler {
    constructor(conversationReferences) {
        super();

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        this.conversationReferences = conversationReferences;

        this.onConversationUpdate(async (context, next) => {
            this.addConversationReference(context.activity);

            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (let cnt = 0; cnt < membersAdded.length; cnt++) {
                if (membersAdded[cnt].id !== context.activity.recipient.id) {
                    const welcomeMessage = 'Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.';
                    await context.sendActivity(welcomeMessage);
                }
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });

        this.onMessage(async (context, next) => {
            this.addConversationReference(context.activity);

            // Echo back what the user said
            await context.sendActivity(`You sent '${ context.activity.text }'`);
            await next();
        });
    }

    addConversationReference(activity) {
        const conversationReference = TurnContext.getConversationReference(activity);
        this.conversationReferences[conversationReference.conversation.id] = conversationReference;
    }
}

module.exports.ProactiveBot = ProactiveBot;

```
---

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="2a07d-182">Teams 管理者向けの関連トピック</span><span class="sxs-lookup"><span data-stu-id="2a07d-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2a07d-183">**Microsoft Teams でアプリのセットアップ ポリシーを管理する**</span><span class="sxs-lookup"><span data-stu-id="2a07d-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="2a07d-184">その他のコード サンプルを表示する</span><span class="sxs-lookup"><span data-stu-id="2a07d-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2a07d-185">**Teams のプロアクティブなメッセージング コード サンプル**</span><span class="sxs-lookup"><span data-stu-id="2a07d-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
