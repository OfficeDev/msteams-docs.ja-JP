---
title: Teams 会議用のアプリを作成する
author: laujan
description: teams 会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: d7dc812f715b6a7edbcc706946b8d80dd692daee
ms.sourcegitcommit: 0aeb60027f423d8ceff3b377db8c3efbb6da4d17
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "48997973"
---
# <a name="create-apps-for-teams-meetings-developer-preview"></a><span data-ttu-id="2fc4c-104">Teams 会議用のアプリを作成する (開発者プレビュー)</span><span class="sxs-lookup"><span data-stu-id="2fc4c-104">Create apps for Teams meetings (Developer Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="2fc4c-105">Microsoft Teams の開発者プレビューに含まれる機能は、すぐにアクセス、テスト、フィードバック目的のみに提供されています。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-105">Features included in Microsoft Teams Developer Preview are provided for early-access, testing, and feedback purposes only.</span></span> <span data-ttu-id="2fc4c-106">公開リリースで利用できるようになる前に変更が行われ、運用アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-106">They may undergo changes before becoming available in the public release and should not be used in production applications.</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="2fc4c-107">前提条件と考慮事項</span><span class="sxs-lookup"><span data-stu-id="2fc4c-107">Prerequisites and considerations</span></span>

1. <span data-ttu-id="2fc4c-108">会議のアプリには、 [Teams アプリ開発](../overview.md)に関する基本的な知識が必要です。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-108">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="2fc4c-109">会議のアプリは、 [タブ](../tabs/what-are-tabs.md)、 [ボット](../bots/what-are-bots.md)、および [メッセージングの拡張](../messaging-extensions/what-are-messaging-extensions.md) 機能で構成され、Teams アプリの [マニフェスト](#update-your-app-manifest) を更新して、アプリが会議で利用できることを示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-109">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="2fc4c-110">アプリが会議のライフサイクルでタブとして機能するには、 [groupchat スコープ](../resources/schema/manifest-schema.md#configurabletabs)で構成可能なタブをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-110">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="2fc4c-111">*「* [カスタムタブを使用して Teams アプリを拡張する](../tabs/how-to/add-tab.md)」を参照してください。スコープをサポートすること `groupchat` で、 [プレミーティング](teams-apps-in-meetings.md#pre-meeting-app-experience) および [ミーティング後](teams-apps-in-meetings.md#post-meeting-app-experience) のチャットでアプリを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-111">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="2fc4c-112">ミーティング API URL パラメーターには、、が必要な場合があり `meetingId` `userId` ます。また、 [TenantId](/onedrive/find-your-office-365-tenant-id) は Teams クライアント SDK および bot アクティビティの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-112">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="2fc4c-113">さらに、 [TAB SSO 認証](../tabs/how-to/authentication/auth-aad-sso.md)を使用して、ユーザー id とテナント id の信頼できる情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-113">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="2fc4c-114">などの一部の会議 Api で `GetParticipant` は、 [ボット登録と BOT アプリ ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) が認証トークンを生成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-114">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="2fc4c-115">開発者は、teams の会議中にトリガー[される会議](design/designing-in-meeting-dialog.md)中のダイアログに加えて、会議前およびミーティング後のシナリオについて、teams の一般的な[タブデザインガイドライン](../tabs/design/tabs.md)に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-115">As a developer, you must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

1. <span data-ttu-id="2fc4c-116">アプリをリアルタイムで更新するためには、会議のイベントアクティビティに基づいて最新の状態になっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-116">Please note that in order for your app to be updated in real-time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="2fc4c-117">これらのイベントは、会議中のダイアログ (の「完了パラメーター」を参照してください `bot Id` `Notification Signal API` ) および会議ライフサイクル全体のその他のサーフェス内に存在することができます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-117">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="2fc4c-118">会議アプリ API リファレンス</span><span class="sxs-lookup"><span data-stu-id="2fc4c-118">Meeting apps API reference</span></span>

|<span data-ttu-id="2fc4c-119">API</span><span class="sxs-lookup"><span data-stu-id="2fc4c-119">API</span></span>|<span data-ttu-id="2fc4c-120">説明</span><span class="sxs-lookup"><span data-stu-id="2fc4c-120">Description</span></span>|<span data-ttu-id="2fc4c-121">要求</span><span class="sxs-lookup"><span data-stu-id="2fc4c-121">Request</span></span>|<span data-ttu-id="2fc4c-122">ソース</span><span class="sxs-lookup"><span data-stu-id="2fc4c-122">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="2fc4c-123">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-123">**GetUserContext**</span></span>| <span data-ttu-id="2fc4c-124">関連するコンテンツを Teams タブに表示するためのコンテキスト情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-124">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="2fc4c-125">_**getContext (() => {/ *...* / } )**_</span><span class="sxs-lookup"><span data-stu-id="2fc4c-125">_**microsoftTeams.getContext( ( ) => {  / *...* / } )**_</span></span>|<span data-ttu-id="2fc4c-126">Microsoft Teams クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="2fc4c-126">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="2fc4c-127">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-127">**GetParticipant**</span></span>|<span data-ttu-id="2fc4c-128">この API を使用すると、ボットはミーティング id と参加者 id で参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-128">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="2fc4c-129">/V1/meetings/{meetingId}/participants/{participantId} を **取得** する ( _**tenantid** )_</span><span class="sxs-lookup"><span data-stu-id="2fc4c-129">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="2fc4c-130">Microsoft Bot フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="2fc4c-130">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="2fc4c-131">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-131">**NotificationSignal**</span></span> |<span data-ttu-id="2fc4c-132">ミーティング信号は、次の既存の会話通知 API を使用して配信されます (ユーザーのためのチャット)。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-132">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="2fc4c-133">この API を使用すると、開発者はエンドユーザーのアクションに基づいて、会議中のダイアログで通知を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-133">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="2fc4c-134">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="2fc4c-134">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="2fc4c-135">Microsoft Bot フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="2fc4c-135">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="2fc4c-136">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="2fc4c-136">GetUserContext</span></span>

<span data-ttu-id="2fc4c-137">タブコンテンツのコンテキスト情報を識別して取得するためのガイダンスについては、「 [Teams のコンテキストの取得」タブ](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-137">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="2fc4c-138">会議機能拡張の一部として、応答ペイロードに新しい値が追加されました。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-138">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="2fc4c-139">✔の会議 **id** : 会議のコンテキストで実行している場合にタブで使用されます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-139">✔ **meetingId** : used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="2fc4c-140">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="2fc4c-140">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="2fc4c-141">会議の開催者はいつでも役割を変更できるため、参加者の役割をキャッシュしないでください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-141">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="2fc4c-142">現時点では、Teams は、API のために350以上の参加者の大きな配布リストまたは名簿サイズをサポートしていません `GetParticipant` 。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-142">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="2fc4c-143">Bot Framework SDK のサポートは近日に予定されています。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-143">Support for the Bot Framework SDK is coming soon.</span></span>


#### <a name="request"></a><span data-ttu-id="2fc4c-144">要求</span><span class="sxs-lookup"><span data-stu-id="2fc4c-144">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="2fc4c-145">[Bot フレームワーク API リファレンス](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)を *参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-145">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="2fc4c-146">**C# の例**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-146">**C# Example**</span></span>

```csharp
string meetingId = "meetingid?";
string participantId = "participantidhere";
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage();
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
request.Method = new HttpMethod("GET");
request.RequestUri = new System.Uri(Path.Combine(connectorClient.BaseUri.OriginalString, $"/meetings/{meetingId}/participants/{participantId}"));
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, cancellationToken).ConfigureAwait(false);
if (response.StatusCode == System.Net.HttpStatusCode.OK)
{
    var content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
    var theObject = Rest.Serialization.SafeJsonConvert.DeserializeObject<WhateverObjectIsReturned>(content, connectorClient.DeserializationSettings);
}
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a><span data-ttu-id="2fc4c-147">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="2fc4c-147">Query parameters</span></span>

|<span data-ttu-id="2fc4c-148">値</span><span class="sxs-lookup"><span data-stu-id="2fc4c-148">Value</span></span>|<span data-ttu-id="2fc4c-149">型</span><span class="sxs-lookup"><span data-stu-id="2fc4c-149">Type</span></span>|<span data-ttu-id="2fc4c-150">必須</span><span class="sxs-lookup"><span data-stu-id="2fc4c-150">Required</span></span>|<span data-ttu-id="2fc4c-151">説明</span><span class="sxs-lookup"><span data-stu-id="2fc4c-151">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="2fc4c-152">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-152">**meetingId**</span></span>| <span data-ttu-id="2fc4c-153">文字列</span><span class="sxs-lookup"><span data-stu-id="2fc4c-153">string</span></span> | <span data-ttu-id="2fc4c-154">はい</span><span class="sxs-lookup"><span data-stu-id="2fc4c-154">Yes</span></span> | <span data-ttu-id="2fc4c-155">会議識別子は、ボット Invoke および Teams クライアント SDK を介して利用できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-155">The meeting identifier is available via Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="2fc4c-156">**participantId**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-156">**participantId**</span></span>| <span data-ttu-id="2fc4c-157">文字列</span><span class="sxs-lookup"><span data-stu-id="2fc4c-157">string</span></span> | <span data-ttu-id="2fc4c-158">はい</span><span class="sxs-lookup"><span data-stu-id="2fc4c-158">Yes</span></span> | <span data-ttu-id="2fc4c-159">このフィールドはユーザー ID であり、タブ SSO、Bot 呼び出し、Teams クライアント SDK で使用できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-159">This field is the User ID and it is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="2fc4c-160">タブ SSO を強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-160">Tab SSO is highly recommended</span></span>|
|<span data-ttu-id="2fc4c-161">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-161">**tenantId**</span></span>| <span data-ttu-id="2fc4c-162">文字列</span><span class="sxs-lookup"><span data-stu-id="2fc4c-162">string</span></span> | <span data-ttu-id="2fc4c-163">はい</span><span class="sxs-lookup"><span data-stu-id="2fc4c-163">Yes</span></span> | <span data-ttu-id="2fc4c-164">これは、テナントのユーザーに必要です。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-164">This required for tenant users.</span></span> <span data-ttu-id="2fc4c-165">これは、タブ SSO、Bot 呼び出し、Teams クライアント SDK で利用できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-165">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="2fc4c-166">タブ SSO を強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-166">Tab SSO is highly recommended</span></span>|

#### <a name="response-payload"></a><span data-ttu-id="2fc4c-167">応答ペイロード</span><span class="sxs-lookup"><span data-stu-id="2fc4c-167">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="2fc4c-168">[ミーティング] の下の **役割** は、 *開催者* 、 *発表者* 、または *出席* 者になることができます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-168">**role** under "meeting" can be *Organizer* , *Presenter* , or *Attendee*.</span></span>

<span data-ttu-id="2fc4c-169">**例 1**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-169">**Example 1**</span></span>

```json
{
  "user":
  {
      "id": "29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId": "6aebbad0-e5a5-424a-834a-20fb051f3c1a",
      "name": "Allan Deyoung",
      "givenName": "Allan",
      "surname": "Deyoung",
      "email": "Allan.Deyoung@microsoft.com",
      "userPrincipalName": "Allan.Deyoung@microsoft.com",
      "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
      "userRole": "user"
  },
  "meeting":
  {
      "role ": "Presenter",
      "inMeeting":true
  },
  "conversation":
  {
      "id": "<conversation id>"
  }
}
```
#### <a name="response-codes"></a><span data-ttu-id="2fc4c-170">応答コード</span><span class="sxs-lookup"><span data-stu-id="2fc4c-170">Response Codes</span></span>

<span data-ttu-id="2fc4c-171">**403** : アプリは、参加者情報を取得することを許可されていません。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-171">**403** : The app is not allowed to get participant information.</span></span> <span data-ttu-id="2fc4c-172">これは、最も一般的なエラー応答であり、アプリがテナント管理者によって無効にされた場合や、ライブサイトの移行中にブロックされた場合など、会議にインストールされていない場合にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-172">This will be the most common error response and is triggered when the app is not installed in the meeting such as when it is disabled by tenant admin or blocked during live site migration.</span></span>  
<span data-ttu-id="2fc4c-173">**200** : 参加者情報が正常に取得されました。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-173">**200** : Participant information successfully retrieved.</span></span>  
<span data-ttu-id="2fc4c-174">**401** : 無効なトークンです。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-174">**401** : Invalid token.</span></span>  
<span data-ttu-id="2fc4c-175">**404** : 参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-175">**404** : Participant cannot be found.</span></span> 
<span data-ttu-id="2fc4c-176">**500** : 会議は有効期限が切れています (会議が終了してからの経過期間は60日を超えています)。または、参加者が役割に基づいてアクセス許可を持っていません。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-176">**500** : The meeting is either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>

<span data-ttu-id="2fc4c-177">**近日公開**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-177">**Coming Soon**</span></span>

<span data-ttu-id="2fc4c-178">**404** : 会議の有効期限が切れているか、参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-178">**404** : the meeting has either expired or participant cannot be found.</span></span> 

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="2fc4c-179">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="2fc4c-179">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="2fc4c-180">会議中のダイアログが呼び出されると、同じコンテンツがチャットメッセージとして表示されることもあります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-180">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="2fc4c-181">要求</span><span class="sxs-lookup"><span data-stu-id="2fc4c-181">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="2fc4c-182">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="2fc4c-182">Query parameters</span></span>

|<span data-ttu-id="2fc4c-183">値</span><span class="sxs-lookup"><span data-stu-id="2fc4c-183">Value</span></span>|<span data-ttu-id="2fc4c-184">型</span><span class="sxs-lookup"><span data-stu-id="2fc4c-184">Type</span></span>|<span data-ttu-id="2fc4c-185">必須</span><span class="sxs-lookup"><span data-stu-id="2fc4c-185">Required</span></span>|<span data-ttu-id="2fc4c-186">説明</span><span class="sxs-lookup"><span data-stu-id="2fc4c-186">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="2fc4c-187">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-187">**conversationId**</span></span>| <span data-ttu-id="2fc4c-188">文字列</span><span class="sxs-lookup"><span data-stu-id="2fc4c-188">string</span></span> | <span data-ttu-id="2fc4c-189">はい</span><span class="sxs-lookup"><span data-stu-id="2fc4c-189">Yes</span></span> | <span data-ttu-id="2fc4c-190">会話 id は bot 呼び出しの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-190">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="request-payload"></a><span data-ttu-id="2fc4c-191">要求のペイロード</span><span class="sxs-lookup"><span data-stu-id="2fc4c-191">Request Payload</span></span>

> [!NOTE]
>
> *  <span data-ttu-id="2fc4c-192">次に示す要求されたペイロードで `completionBotId` は、のパラメーター `externalResourceUrl` は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-192">In the requested payload below, the `completionBotId` parameter of the `externalResourceUrl`is an optional.</span></span> <span data-ttu-id="2fc4c-193">これは、 `Bot ID` マニフェストで宣言されているです。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-193">It is the `Bot ID` that is declared in the manifest.</span></span> <span data-ttu-id="2fc4c-194">Bot は result オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-194">The bot will receive a result object.</span></span>
> * <span data-ttu-id="2fc4c-195">ExternalResourceUrl の幅と高さのパラメーターは、ピクセル単位でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-195">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="2fc4c-196">ディメンションが許容範囲内にあることを確認するには、 [設計ガイドライン](design/designing-in-meeting-dialog.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-196">Refer to the [design guidelines](design/designing-in-meeting-dialog.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="2fc4c-197">URL は、 `<iframe>` [会議中] ダイアログボックスの内側に読み込まれるページです。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-197">The URL is the page loaded as an `<iframe>` inside the in-meeting dialog.</span></span> <span data-ttu-id="2fc4c-198">URL のドメインは、アプリのマニフェストのアプリの配列に含まれている必要があり `validDomains` ます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-198">The URL's domain must be in the app's `validDomains` array in your app manifest.</span></span>


# <a name="json"></a>[<span data-ttu-id="2fc4c-199">JSON</span><span class="sxs-lookup"><span data-stu-id="2fc4c-199">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

# <a name="cnet"></a>[<span data-ttu-id="2fc4c-200">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2fc4c-200">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
  {
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
  };
activity.ChannelData = new TeamsChannelData
  {
    Notification = notification
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="2fc4c-201">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2fc4c-201">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> <span data-ttu-id="2fc4c-202">コンテンツバブル (taskInfo URL) 内の URL は、Teams アプリマニフェストに含まれている [有効なドメイン](../resources/schema/manifest-schema.md#validdomains) の一覧に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-202">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="2fc4c-203">応答コード</span><span class="sxs-lookup"><span data-stu-id="2fc4c-203">Response Codes</span></span>

<span data-ttu-id="2fc4c-204">**201** : シグナルが正常に送信されたアクティビティ</span><span class="sxs-lookup"><span data-stu-id="2fc4c-204">**201** : activity with signal is successfully sent</span></span>  
<span data-ttu-id="2fc4c-205">**401** : 無効なトークン</span><span class="sxs-lookup"><span data-stu-id="2fc4c-205">**401** : invalid token</span></span>  
<span data-ttu-id="2fc4c-206">**403** : アプリは、シグナルを送信することを許可されていません。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-206">**403** : the app is not allowed to send the signal.</span></span> <span data-ttu-id="2fc4c-207">この場合、ペイロードに詳細なエラーメッセージが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-207">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="2fc4c-208">多くの理由が考えられます。これは、テナント管理者によって無効にされたアプリ、運用サイトの移行中にブロックされたなどです。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-208">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="2fc4c-209">**404** : 会議チャットが存在しません</span><span class="sxs-lookup"><span data-stu-id="2fc4c-209">**404** : meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="2fc4c-210">Teams 会議でアプリを有効にする</span><span class="sxs-lookup"><span data-stu-id="2fc4c-210">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="2fc4c-211">アプリのマニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="2fc4c-211">Update your app manifest</span></span>

<span data-ttu-id="2fc4c-212">ミーティングアプリの機能は、[アプリケーションマニフェスト] の [セキュリティの定義] **タブ**  ->  **スコープ** と **コンテキスト** 配列を使用して宣言されています。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-212">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="2fc4c-213">*スコープ* は、アプリが使用可能になる場所と *コンテキスト* を定義します。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-213">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> * <span data-ttu-id="2fc4c-214">[開発者プレビューマニフェストスキーマ](../resources/schema/manifest-schema-dev-preview.md)を使用して、アプリマニフェストでこれを試してください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-214">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

```json
"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel"
     ]
    }
  ]
```

### <a name="context-property"></a><span data-ttu-id="2fc4c-215">Context プロパティ</span><span class="sxs-lookup"><span data-stu-id="2fc4c-215">Context property</span></span>

<span data-ttu-id="2fc4c-216">Tab `context` およびプロパティは、 `scopes` アプリを表示する場所を決定できるようにするために、ハーモニーで機能します。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-216">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="2fc4c-217">またはの範囲内のタブに `team` は、 `groupchat` 複数のコンテキストを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-217">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="2fc4c-218">Context プロパティに指定できる値は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-218">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="2fc4c-219">[ **Channeltab タブ** : チームチャネルのヘッダーのタブ。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-219">**channelTab** : a tab in the header of a team channel.</span></span>
* <span data-ttu-id="2fc4c-220">**privateChatTab** : チームまたは会議のコンテキストではないユーザーのセット間のグループチャットのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-220">**privateChatTab** : a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="2fc4c-221">**meetingChatTab** : 予約された会議のコンテキスト内のユーザーのセット間のグループチャットのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-221">**meetingChatTab** : a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="2fc4c-222">[会議詳細] **タブ: 予定** 表の会議の詳細ビューのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-222">**meetingDetailsTab** : a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="2fc4c-223">会議の **sidepanel** : 統合バー (u バー) によって開かれた会議中のパネル。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-223">**meetingSidePanel** : an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="2fc4c-224">"Context" プロパティは現在サポートされていないため、モバイルクライアントでは無視されます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-224">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="2fc4c-225">アプリを構成してシナリオをミーティングする</span><span class="sxs-lookup"><span data-stu-id="2fc4c-225">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="2fc4c-226">アプリケーションがタブギャラリーに表示されるようにするには、 **構成可能なタブ** と **グループチャットスコープ** をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-226">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="2fc4c-227">モバイルクライアントは、会議のプレおよびポストの表面でのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-227">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="2fc4c-228">モバイルの会議中のエクスペリエンス (会議中のダイアログとパネル) は近日中に利用可能になります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-228">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon.</span></span> <span data-ttu-id="2fc4c-229">モバイル用のタブを作成するときに、 [[モバイル] のタブのガイダンス](../tabs/design/tabs-mobile.md) に従ってください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-229">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span> 

### <a name="pre-meeting"></a><span data-ttu-id="2fc4c-230">プレミーティング</span><span class="sxs-lookup"><span data-stu-id="2fc4c-230">Pre-meeting</span></span>

<span data-ttu-id="2fc4c-231">開催者または発表者の役割を持つユーザーは、会議 **チャット** および会議の **詳細** ページのプラス➕ボタンを使用して、会議にタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-231">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="2fc4c-232">メッセージング拡張機能は、[会話の作成メッセージ] 領域の下にある [楕円/オーバーフロー] メニュー &#x25CF;&#x25CF;&#x25CF; 経由で追加されます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-232">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="2fc4c-233">Bot は、"" キーを使用して会議チャットに追加され、[ **@** **ボットを取得** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-233">Bots are added to a meeting chat using the " **@** " key and selecting **Get bots**.</span></span>

<span data-ttu-id="2fc4c-234">ユーザー id は、 [タブ SSO](../tabs/how-to/authentication/auth-aad-sso.md)を使用して確認する *必要があり* ✔。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-234">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="2fc4c-235">この認証の後、アプリは GetParticipant API を使用してユーザーロールを取得できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-235">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="2fc4c-236">✔ユーザーの役割に基づいて、アプリに役割固有のエクスペリエンスを提供する機能が用意されました。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-236">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="2fc4c-237">たとえば、投票アプリでは、開催者と発表者のみが新しい投票を作成できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-237">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="2fc4c-238">**注** : 役割の割り当ては、会議の進行中に変更できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-238">**NOTE** : Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="2fc4c-239">*「* [Teams Meeting の役割](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-239">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="2fc4c-240">会議中</span><span class="sxs-lookup"><span data-stu-id="2fc4c-240">In-meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="2fc4c-241">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-241">**sidePanel**</span></span>

<span data-ttu-id="2fc4c-242">アプリマニフェスト内の✔前述のように、 **コンテキスト** 配列に **sidepanel** を追加します。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-242">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="2fc4c-243">会議の✔とすべてのシナリオにおいて、アプリは、ため320px ですの幅で表示される [会議中] タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-243">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="2fc4c-244">このためにタブを最適化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-244">Your tab must be optimized for this.</span></span> <span data-ttu-id="2fc4c-245">*参照* 、 [framecontext インターフェイス](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2fc4c-245">*See* , [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span></span>

<span data-ttu-id="2fc4c-246">**UserContext** API を使用して要求を適切にルーティングするには、 [Teams SDK](../tabs/how-to/access-teams-context.md#user-context)を参照してください✔。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-246">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="2fc4c-247">✔ [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-247">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="2fc4c-248">タブの認証フローは、web サイトの認証フローとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-248">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="2fc4c-249">そのため、タブは OAuth 2.0 を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-249">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="2fc4c-250">「 [Microsoft identity platform And OAuth 2.0 認証コードフロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow) *」も参照して* ください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-250">*See also* , [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="2fc4c-251">**会議中のダイアログ**</span><span class="sxs-lookup"><span data-stu-id="2fc4c-251">**in-meeting dialog**</span></span>

<span data-ttu-id="2fc4c-252">✔ [会議中のダイアログの設計ガイドライン](design/designing-in-meeting-dialog.md)に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="2fc4c-253">✔ [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="2fc4c-254">✔ [通知](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API を使用して、バブル通知がトリガーされる必要があることを通知します。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-254">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="2fc4c-255">✔通知要求のペイロードの一部として、紹介するコンテンツがホストされる URL を含めます。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="2fc4c-256">これらの通知は、本質的に永続的なものです。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-256">These notifications are persistent in nature.</span></span> <span data-ttu-id="2fc4c-257">ユーザーが web ビューでアクションを実行した後に、 [**Submittask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出して自動消去する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-257">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="2fc4c-258">これは、アプリを送信するための要件です。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-258">This is a requirement for app submission.</span></span> <span data-ttu-id="2fc4c-259">「 [TEAMS SDK: タスクモジュール](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true) *」も参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-259">*See also* , [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="2fc4c-260">アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求のペイロードは、( `from.id` `from` `from.aadObjectId` ユーザーの AZURE Active Directory ID) 要求メタデータではなく、オブジェクト内の (ユーザーの ID) 要求メタデータに依存している必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-260">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="2fc4c-261">*「* [タスクモジュールを使用して](../task-modules-and-cards/task-modules/task-modules-tabs.md) タスク [モジュールを作成し、送信](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-261">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="2fc4c-262">会議後</span><span class="sxs-lookup"><span data-stu-id="2fc4c-262">Post-meeting</span></span>

<span data-ttu-id="2fc4c-263">ポストミーティングと事前会議の構成は同等です。</span><span class="sxs-lookup"><span data-stu-id="2fc4c-263">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="2fc4c-264">会議アプリのサンプル</span><span class="sxs-lookup"><span data-stu-id="2fc4c-264">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="2fc4c-265">会議トークン生成アプリ</span><span class="sxs-lookup"><span data-stu-id="2fc4c-265">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
