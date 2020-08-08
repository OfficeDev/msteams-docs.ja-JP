---
title: Microsoft Graph を使用して Teams での積極的なボットのインストールとメッセージングを有効にする
description: Teams における予防的なメッセージングと実装方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams の予防的なメッセージングチャットインストールグラフ
ms.openlocfilehash: f1d2c51957eefbc548918210b843e408eb1107c8
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587742"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="dd996-104">Microsoft Graph を使用した Teams での予防的なインストールと予防的なメッセージングを有効にする (パブリックプレビュー)</span><span class="sxs-lookup"><span data-stu-id="dd996-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="dd996-105">Microsoft Graph のパブリックプレビューは、初めてアクセスしてフィードバックする際に使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd996-105">Microsoft Graph public previews are available for early-access and feedback.</span></span> <span data-ttu-id="dd996-106">このリリースは広範なテストを経ていますが、運用環境での使用は想定されていません。</span><span class="sxs-lookup"><span data-stu-id="dd996-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="dd996-107">Teams での事前のメッセージング</span><span class="sxs-lookup"><span data-stu-id="dd996-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="dd996-108">事前メッセージは、ユーザーとの会話を開始する bot によって開始されます。</span><span class="sxs-lookup"><span data-stu-id="dd996-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="dd996-109">開始メッセージの送信、調査または投票の実行、組織全体にわたる通知の配信など、さまざまな目的に対応しています。</span><span class="sxs-lookup"><span data-stu-id="dd996-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="dd996-110">Teams の事前メッセージ**は、アドホックまたは\*\*\*\*ダイアログベース**の会話として配信できます。</span><span class="sxs-lookup"><span data-stu-id="dd996-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="dd996-111">メッセージ型</span><span class="sxs-lookup"><span data-stu-id="dd996-111">Message Type</span></span> | <span data-ttu-id="dd996-112">説明</span><span class="sxs-lookup"><span data-stu-id="dd996-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="dd996-113">アドホックの事前メッセージ</span><span class="sxs-lookup"><span data-stu-id="dd996-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="dd996-114">Bot は、会話フローを中断することなくメッセージを interjects します。</span><span class="sxs-lookup"><span data-stu-id="dd996-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="dd996-115">ダイアログベースの事前メッセージ</span><span class="sxs-lookup"><span data-stu-id="dd996-115">Dialog-based proactive message</span></span> | <span data-ttu-id="dd996-116">Bot は、新しいダイアログスレッドを作成し、会話の制御を取得し、事前メッセージを配信し、前のダイアログに制御を戻します。</span><span class="sxs-lookup"><span data-stu-id="dd996-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="dd996-117">「[ユーザーに事前通知を送信する SDK V4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp) *」を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="dd996-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="dd996-118">Teams での事前にアプリをインストールする</span><span class="sxs-lookup"><span data-stu-id="dd996-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="dd996-119">Bot がユーザーに対して予防的なメッセージを実行できるようにするには、ユーザーを個人のアプリとしてインストールするか、またはユーザーがメンバーになっているチームにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd996-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="dd996-120">インストールさ_れていない_、またはアプリに以前対話したことがない場合は、事前にメッセージを事前に作成しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd996-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="dd996-121">たとえば、組織内のすべてのユーザーにとって重要な情報をメッセージにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd996-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="dd996-122">このようなシナリオでは、Microsoft Graph API を使用して、ユーザー向けに bot を事前にインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="dd996-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="dd996-123">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="dd996-123">Permissions</span></span>

<span data-ttu-id="dd996-124">Microsoft Graph [teamsAppInstallation リソースの種類](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0)のアクセス許可を使用すると、microsoft Teams プラットフォーム内のすべてのユーザー (個人) スコープまたはチーム (チャネル) スコープのアプリのインストールライフサイクルを管理できます。</span><span class="sxs-lookup"><span data-stu-id="dd996-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="dd996-125">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="dd996-125">Application permission</span></span> | <span data-ttu-id="dd996-126">説明</span><span class="sxs-lookup"><span data-stu-id="dd996-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="dd996-127">Teams アプリは、サインインまたは使用前に、**ユーザー**の読み取り、インストール、アップグレード、およびアンインストールを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="dd996-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="dd996-128">Teams アプリは、サインインまたは使用前に、任意の**チーム**で自分自身を読み取り、インストール、アップグレード、およびアンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="dd996-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="dd996-129">これらのアクセス許可を使用するには、次の値を使用して、 [Webapplicationinfo](../../resources/schema/manifest-schema.md#webapplicationinfo)キーをアプリのマニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd996-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="dd996-130">**id** : Azure AD アプリ id。</span><span class="sxs-lookup"><span data-stu-id="dd996-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="dd996-131">**resource** —アプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="dd996-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="dd996-132">Bot には、ユーザーにはインストールされませんが、それ以外の場合は、_アプリケーション_による_委任_されたアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="dd996-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="dd996-133">Azure AD テナント管理者は、[アプリケーションに対するアクセス許可を明示的に付与](/graph/security-authorization#grant-permissions-to-an-application)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd996-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="dd996-134">アプリケーションにアクセス許可が付与されると、Azure AD テナントの_すべて_のメンバーが付与されたアクセス許可を取得します。</span><span class="sxs-lookup"><span data-stu-id="dd996-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="dd996-135">事前にアプリのインストールとメッセージングを有効にする</span><span class="sxs-lookup"><span data-stu-id="dd996-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="dd996-136">Microsoft Graph では、組織の[アプリカタログ](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)または[appsource](https://appsource.microsoft.com/)に発行されたアプリのみがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="dd996-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="dd996-137">チームのために予防的なメッセージングボットを作成して発行する✔</span><span class="sxs-lookup"><span data-stu-id="dd996-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="dd996-138">作業を開始するには、[積極的なメッセージング](../../concepts/bots/bot-conversations/bots-conv-proactive.md)機能を備え、組織の[アプリカタログ](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)または[appsource](https://appsource.microsoft.com/)に[公開](../../concepts/deploy-and-publish/overview.md)されている[Teams 用の bot](../../bots/how-to/create-a-bot-for-teams.md)が必要です。</span><span class="sxs-lookup"><span data-stu-id="dd996-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="dd996-139">運用に対応した[**会社の Communicator**](../..//samples/app-templates.md#company-communicator)アプリテンプレートでは、ブロードキャストメッセージングが有効になり、予防的な bot アプリケーションを構築するための基礎となります。</span><span class="sxs-lookup"><span data-stu-id="dd996-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="dd996-140">`teamsAppId`アプリのを取得✔</span><span class="sxs-lookup"><span data-stu-id="dd996-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="dd996-141">**1.** 次の手順では、が必要になります。 `teamsAppId`</span><span class="sxs-lookup"><span data-stu-id="dd996-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="dd996-142">は、 `teamsAppId` 組織のアプリカタログから取得できます。</span><span class="sxs-lookup"><span data-stu-id="dd996-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="dd996-143">**Microsoft Graph ページリファレンス:** [teamsapp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span><span class="sxs-lookup"><span data-stu-id="dd996-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span></span>

<span data-ttu-id="dd996-144">**HTTP GET**要求:</span><span class="sxs-lookup"><span data-stu-id="dd996-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="dd996-145">要求はオブジェクトを返し `teamsApp` ます。</span><span class="sxs-lookup"><span data-stu-id="dd996-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="dd996-146">返されるオブジェクトは、アプリのカタログ生成されたアプリ id であり、 `id` Teams アプリマニフェストで指定した "id:" とは異なります。</span><span class="sxs-lookup"><span data-stu-id="dd996-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="dd996-147">**2.** 個人スコープ内のユーザーに対してアプリが既にアップロードされている場合は、次のようにサイドロードを取得できます。 `teamsAppId`</span><span class="sxs-lookup"><span data-stu-id="dd996-147">**2.**  If your app has already been uploaded/sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="dd996-148">**Microsoft Graph ページリファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="dd996-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="dd996-149">**HTTP GET**要求:</span><span class="sxs-lookup"><span data-stu-id="dd996-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="dd996-150">**3.** アプリがチームスコープ内のチャネルに対して既にアップロードまたはサイドロードされている場合は、次のようにを取得できます `teamsAppId` 。</span><span class="sxs-lookup"><span data-stu-id="dd996-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="dd996-151">**Microsoft Graph ページリファレンス:** teams[のアプリの一覧](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="dd996-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="dd996-152">**HTTP GET**要求:</span><span class="sxs-lookup"><span data-stu-id="dd996-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{manifestId}'
```

>[!TIP]
> <span data-ttu-id="dd996-153">[**Teamsapp**](/graph/api/resources/teamsapp?view=graph-rest-1.0)オブジェクトの任意のフィールドをフィルター処理して、結果の一覧を絞り込むことができます。</span><span class="sxs-lookup"><span data-stu-id="dd996-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="dd996-154">✔ Bot がメッセージの受信者に現在インストールされているかどうかを判断するには</span><span class="sxs-lookup"><span data-stu-id="dd996-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="dd996-155">**Microsoft Graph ページリファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="dd996-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="dd996-156">**HTTP GET**要求:</span><span class="sxs-lookup"><span data-stu-id="dd996-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="dd996-157">この要求は、アプリがインストールされていない場合は空の配列を返し、インストールされている場合は1つの[teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta)オブジェクトを持つ配列を返します。</span><span class="sxs-lookup"><span data-stu-id="dd996-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="dd996-158">アプリをインストール✔には</span><span class="sxs-lookup"><span data-stu-id="dd996-158">✔ Install your app</span></span>

<span data-ttu-id="dd996-159">**Microsoft Graph リファレンス:** [ユーザーのアプリをインストールする](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="dd996-159">**Microsoft Graph reference:** [Install app for user](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="dd996-160">**HTTP POST**要求:</span><span class="sxs-lookup"><span data-stu-id="dd996-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="dd996-161">ユーザーが Microsoft Teams を実行している場合は、直ちにアプリのインストールが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="dd996-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="dd996-162">または、インストールされているアプリを表示するために再起動が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="dd996-162">Alternatively,  a  restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="dd996-163">会話**chatId**を取得✔には</span><span class="sxs-lookup"><span data-stu-id="dd996-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="dd996-164">アプリがユーザー用にインストールされている場合、bot は、 `conversationUpdate` 事前メッセージを送信するために必要な情報が含まれた[イベント通知](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="dd996-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="dd996-165">は、次のように `chatId` 取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="dd996-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="dd996-166">**Microsoft Graph リファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="dd996-166">**Microsoft Graph reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="dd996-167">**1.** アプリは必要になります `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="dd996-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="dd996-168">使用していない場合は、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="dd996-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="dd996-169">**HTTP GET**要求:</span><span class="sxs-lookup"><span data-stu-id="dd996-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="dd996-170">応答の**id**プロパティは、 `teamsAppInstallationId` です。</span><span class="sxs-lookup"><span data-stu-id="dd996-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="dd996-171">**2.** 次のものをフェッチするための要求を行います。 `chatId`</span><span class="sxs-lookup"><span data-stu-id="dd996-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="dd996-172">**HTTP GET**要求 (アクセス許可— `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="dd996-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="dd996-173">応答の**id**プロパティは、 `chatId` です。</span><span class="sxs-lookup"><span data-stu-id="dd996-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="dd996-174">または、以下の要求でを取得することもでき `chatId` ますが、より広範なアクセス許可が必要になり `Chat.Read.All` ます。</span><span class="sxs-lookup"><span data-stu-id="dd996-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="dd996-175">**HTTP GET**要求 (アクセス許可— `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="dd996-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="dd996-176">積極的なメッセージを送信✔には</span><span class="sxs-lookup"><span data-stu-id="dd996-176">✔ Send proactive messages</span></span>

<span data-ttu-id="dd996-177">ユーザーまたはチームに bot が追加され、必要なユーザー情報を取得している場合は、[事前メッセージの送信](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)を開始できます。</span><span class="sxs-lookup"><span data-stu-id="dd996-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="dd996-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="dd996-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="dd996-179">次のコードスニペットは、 [C# の Microsoft Bot フレームワークサンプル](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)からのものです。</span><span class="sxs-lookup"><span data-stu-id="dd996-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="dd996-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="dd996-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="dd996-181">次のコードスニペットは、 [JavaScript の Microsoft Bot フレームワークサンプル](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)からのものです。</span><span class="sxs-lookup"><span data-stu-id="dd996-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

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

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="dd996-182">Teams 管理者向けの関連トピック</span><span class="sxs-lookup"><span data-stu-id="dd996-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="dd996-183">**Microsoft Teams でアプリのセットアップポリシーを管理する**</span><span class="sxs-lookup"><span data-stu-id="dd996-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="dd996-184">追加のコードサンプルを表示する</span><span class="sxs-lookup"><span data-stu-id="dd996-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="dd996-185">**Teams の予防的なメッセージングコードサンプル**</span><span class="sxs-lookup"><span data-stu-id="dd996-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
