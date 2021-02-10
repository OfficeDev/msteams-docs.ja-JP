---
title: Microsoft Graph を使用して Teams で事前ボットのインストールとメッセージングを有効にする
description: Teams でのプロアクティブ メッセージングと実装方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams のプロアクティブ メッセージング チャットのインストールのグラフ
ms.openlocfilehash: 4f26b4d2f4e82fcf50b7a35c46bcd07e5afecf19
ms.sourcegitcommit: b99ed616db734371e4af4594b7e895c5b05737c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2021
ms.locfileid: "50162895"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="8ea8a-104">Microsoft Graph を使用して Teams でプロアクティブ ボットのインストールとプロアクティブ メッセージングを有効にする (パブリック プレビュー)</span><span class="sxs-lookup"><span data-stu-id="8ea8a-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="8ea8a-105">Microsoft Graph と Microsoft Teams のパブリック プレビューは、早期アクセスとフィードバックに利用できます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="8ea8a-106">このリリースでは広範なテストが実施されましたが、実稼働環境での使用を意図した方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="8ea8a-107">Teams でのプロアクティブ メッセージング</span><span class="sxs-lookup"><span data-stu-id="8ea8a-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="8ea8a-108">プロアクティブ メッセージは、ユーザーとの会話を開始するためにボットによって開始されます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="8ea8a-109">ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に対応します。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="8ea8a-110">Teams のプロアクティブ メッセージは、アドホックまたはダイアログ ベースの **会話として配信** できます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="8ea8a-111">メッセージ型</span><span class="sxs-lookup"><span data-stu-id="8ea8a-111">Message Type</span></span> | <span data-ttu-id="8ea8a-112">説明</span><span class="sxs-lookup"><span data-stu-id="8ea8a-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="8ea8a-113">臨時のプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="8ea8a-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="8ea8a-114">ボットは、会話フローを中断せずにメッセージを対話します。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="8ea8a-115">ダイアログ ベースのプロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="8ea8a-115">Dialog-based proactive message</span></span> | <span data-ttu-id="8ea8a-116">ボットは、新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じ、前のダイアログにコントロールを返します。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="8ea8a-117">*See* [,Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8ea8a-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="8ea8a-118">Teams でのアプリのプロアクティブ インストール</span><span class="sxs-lookup"><span data-stu-id="8ea8a-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="8ea8a-119">ボットが事前にユーザーにメッセージを送信するには、事前に個人用アプリとして、またはユーザーがメンバーであるチームにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="8ea8a-120">場合によっては、アプリをインストールしていないユーザーや以前にアプリとやり取りしていないユーザーに事前にメッセージを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="8ea8a-121">たとえば、組織内のすべてのユーザーに重要な情報をメッセージ送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="8ea8a-122">このようなシナリオでは、Microsoft Graph API を使用して、ユーザーのボットを事前にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="8ea8a-123">許可</span><span class="sxs-lookup"><span data-stu-id="8ea8a-123">Permissions</span></span>

<span data-ttu-id="8ea8a-124">Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) リソースの種類のアクセス許可を使用すると、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) スコープまたはチーム (チャネル) スコープに対するアプリのインストール ライフサイクルを管理できます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="8ea8a-125">アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="8ea8a-125">Application permission</span></span> | <span data-ttu-id="8ea8a-126">説明</span><span class="sxs-lookup"><span data-stu-id="8ea8a-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="8ea8a-127">Teams アプリは、事前サインインや使用なしで、任意のユーザーの読み取り、インストール、アップグレード、アンインストールを実行できます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="8ea8a-128">Teams アプリは、事前にサインインしたり使用したりすることなく、任意のチームで自身を読み取り、インストール、アップグレード、アンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="8ea8a-129">これらのアクセス許可を使用するには、次の値を使用して [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="8ea8a-130">**id**  — Azure ADアプリ ID。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="8ea8a-131">**resource** — アプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="8ea8a-132">ボットでは、 _アプリケーションは_ ユーザー _によって委任_ されたアクセス許可を必要とします。これは、インストールは自分用ではなく、他のユーザー向けのためです。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="8ea8a-133">Azure ADテナント管理者は、アプリケーションにアクセス [許可を明示的に付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="8ea8a-134">アプリケーションにアクセス許可が付与された後、Azure AD テナントのすべてのメンバーに付与されたアクセス許可が付与されます。 </span><span class="sxs-lookup"><span data-stu-id="8ea8a-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="8ea8a-135">予防的なアプリのインストールとメッセージングを有効にする</span><span class="sxs-lookup"><span data-stu-id="8ea8a-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="8ea8a-136">Microsoft Graph は、組織のアプリ カタログ内または AppSource 内で [公開されている](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) アプリのみを [インストールします](https://appsource.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="8ea8a-137">✔ Teams 用のプロアクティブ メッセージング ボットを作成して発行する</span><span class="sxs-lookup"><span data-stu-id="8ea8a-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="8ea8a-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with proactive [messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [in AppSource](https://appsource.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="8ea8a-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="8ea8a-139">実稼働対応の [**Company Communicator**](../..//samples/app-templates.md#company-communicator) アプリ テンプレートは、ブロードキャスト メッセージングを有効にし、プロアクティブ ボット アプリケーションを構築する良い基盤です。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="8ea8a-140">✔アプリを `teamsAppId` 取得する</span><span class="sxs-lookup"><span data-stu-id="8ea8a-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="8ea8a-141">**1.** 次の手順 `teamsAppId`  が必要です。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="8ea8a-142">組織 `teamsAppId` のアプリ カタログから取得できます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="8ea8a-143">**Microsoft Graph ページ リファレンス:** [teamsApp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8ea8a-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="8ea8a-144">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8ea8a-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="8ea8a-145">要求はオブジェクトを返 `teamsApp`  します。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="8ea8a-146">返されるオブジェクトは、アプリのカタログによって生成されたアプリ ID であり、Teams アプリ マニフェストで指定した `id`  "id:" とは異なります。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="8ea8a-147">**2.**  個人用スコープのユーザーに対してアプリが既にアップロードまたはサイドロードされている場合は、次の情報を `teamsAppId` 取得できます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-147">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="8ea8a-148">**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされたアプリを一覧表示する](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8ea8a-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="8ea8a-149">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8ea8a-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="8ea8a-150">**3.** チーム スコープのチャネルに対してアプリが既にアップロードまたはサイドロードされている場合は、次のように `teamsAppId` 取得できます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="8ea8a-151">**Microsoft Graph ページ リファレンス:** [チーム内のアプリを一覧表示する](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8ea8a-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="8ea8a-152">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8ea8a-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="8ea8a-153">[**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)オブジェクトの任意のフィールドにフィルターを適用して、結果の一覧を絞り込む。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="8ea8a-154">✔メッセージ受信者用にボットが現在インストールされているかどうかを確認する</span><span class="sxs-lookup"><span data-stu-id="8ea8a-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="8ea8a-155">**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされたアプリを一覧表示する](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8ea8a-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="8ea8a-156">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8ea8a-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="8ea8a-157">この要求は、アプリがインストールされていない場合は空の配列を返し、インストールされている場合は [単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列を返します。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="8ea8a-158">✔をインストールする</span><span class="sxs-lookup"><span data-stu-id="8ea8a-158">✔ Install your app</span></span>

<span data-ttu-id="8ea8a-159">**Microsoft Graph ページ リファレンス:** [ユーザー用アプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8ea8a-159">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="8ea8a-160">**HTTP POST** 要求:</span><span class="sxs-lookup"><span data-stu-id="8ea8a-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="8ea8a-161">ユーザーが Microsoft Teams を実行している場合、アプリがすぐにインストールされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="8ea8a-162">または、インストールされているアプリを表示するために再起動が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-162">Alternatively, a restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="8ea8a-163">✔ **chatId を取得する**</span><span class="sxs-lookup"><span data-stu-id="8ea8a-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="8ea8a-164">ユーザー用にアプリがインストールされている場合、ボットはプロアクティブ メッセージを送信するために必要な情報を含むイベント `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="8ea8a-165">次 `chatId` のように取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="8ea8a-166">**Microsoft Graph ページ リファレンス:** [チャットを取得する](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8ea8a-166">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="8ea8a-167">**1.** アプリが必要です `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="8ea8a-168">お持ちでない場合は、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="8ea8a-169">**HTTP GET** 要求:</span><span class="sxs-lookup"><span data-stu-id="8ea8a-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="8ea8a-170">応答 **の id** プロパティは次の値です `teamsAppInstallationId` 。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="8ea8a-171">**2. 次** の要求を行って、次の要求をフェッチします `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="8ea8a-172">**HTTP GET** 要求 (アクセス許可 — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):</span><span class="sxs-lookup"><span data-stu-id="8ea8a-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="8ea8a-173">応答 **の id** プロパティは次の値です `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="8ea8a-174">または、以下の要求を使用して取得できますが、 `chatId`  より広範なアクセス許可が必要 `Chat.Read.All` になります。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="8ea8a-175">**HTTP GET** 要求 (アクセス許可 — `Chat.Read.All` ):</span><span class="sxs-lookup"><span data-stu-id="8ea8a-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="8ea8a-176">✔メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="8ea8a-176">✔ Send proactive messages</span></span>

<span data-ttu-id="8ea8a-177">ボットがユーザーまたはチームに追加され、必要なユーザー情報を取得したら、プロアクティブ メッセージの送信 [を開始できます](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="8ea8a-178">C# / .NET</span><span class="sxs-lookup"><span data-stu-id="8ea8a-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="8ea8a-179">次のコード スニペットは [、C# 用 Microsoft Bot Framework サンプルの抜粋です。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="8ea8a-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="8ea8a-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8ea8a-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="8ea8a-181">次のコード スニペットは [、Microsoft Bot Framework Samples for JavaScript の抜粋です](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。</span><span class="sxs-lookup"><span data-stu-id="8ea8a-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

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

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="8ea8a-182">Teams 管理者向け関連トピック</span><span class="sxs-lookup"><span data-stu-id="8ea8a-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8ea8a-183">**Microsoft Teams のアプリのセットアップ ポリシーを管理する**</span><span class="sxs-lookup"><span data-stu-id="8ea8a-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="8ea8a-184">その他のコード サンプルを表示する</span><span class="sxs-lookup"><span data-stu-id="8ea8a-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8ea8a-185">**Teams プロアクティブ メッセージングのコード サンプル**</span><span class="sxs-lookup"><span data-stu-id="8ea8a-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
