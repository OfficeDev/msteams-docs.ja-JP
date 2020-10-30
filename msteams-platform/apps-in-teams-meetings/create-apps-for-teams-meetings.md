---
title: Teams 会議用のアプリを作成する
author: laujan
description: teams 会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: cf42d660c9b4a82f8e28d4d4379194c1bcc681e1
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796170"
---
# <a name="create-apps-for-teams-meetings-developer-preview"></a><span data-ttu-id="39060-104">Teams 会議用のアプリを作成する (開発者プレビュー)</span><span class="sxs-lookup"><span data-stu-id="39060-104">Create apps for Teams meetings (Developer Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="39060-105">Microsoft Teams の開発者プレビューに含まれる機能は、すぐにアクセス、テスト、フィードバック目的のみに提供されています。</span><span class="sxs-lookup"><span data-stu-id="39060-105">Features included in Microsoft Teams Developer Preview are provided for early-access, testing, and feedback purposes only.</span></span> <span data-ttu-id="39060-106">公開リリースで利用できるようになる前に変更が行われ、運用アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="39060-106">They may undergo changes before becoming available in the public release and should not be used in production applications.</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="39060-107">前提条件と考慮事項</span><span class="sxs-lookup"><span data-stu-id="39060-107">Prerequisites and considerations</span></span>

1. <span data-ttu-id="39060-108">会議のアプリには、 [Teams アプリ開発](../overview.md)に関する基本的な知識が必要です。</span><span class="sxs-lookup"><span data-stu-id="39060-108">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="39060-109">会議のアプリは、 [タブ](../tabs/what-are-tabs.md)、 [ボット](../bots/what-are-bots.md)、および [メッセージングの拡張](../messaging-extensions/what-are-messaging-extensions.md) 機能で構成され、Teams アプリの [マニフェスト](#update-your-app-manifest) を更新して、アプリが会議で利用できることを示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-109">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="39060-110">アプリが会議のライフサイクルでタブとして機能するには、 [groupchat スコープ](../resources/schema/manifest-schema.md#configurabletabs)で構成可能なタブをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-110">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="39060-111">*「* [カスタムタブを使用して Teams アプリを拡張する](../tabs/how-to/add-tab.md)」を参照してください。スコープをサポートすること `groupchat` で、 [プレミーティング](teams-apps-in-meetings.md#pre-meeting-app-experience) および [ミーティング後](teams-apps-in-meetings.md#post-meeting-app-experience) のチャットでアプリを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="39060-111">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="39060-112">ミーティング API URL パラメーターには、、が必要な場合があり `meetingId` `userId` ます。また、 [TenantId](/onedrive/find-your-office-365-tenant-id) は Teams クライアント SDK および bot アクティビティの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="39060-112">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="39060-113">さらに、 [TAB SSO 認証](../tabs/how-to/authentication/auth-aad-sso.md)を使用して、ユーザー id とテナント id の信頼できる情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="39060-113">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="39060-114">などの一部の会議 Api で `GetParticipant` は、 [ボット登録と BOT アプリ ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) が認証トークンを生成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-114">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="39060-115">開発者は、チームの会議中にトリガー[される会議](design/designing-in-meeting-dialog.md)中のダイアログのための、会議前およびミーティング後のシナリオのための [teams][タブデザインのガイドライン](../tabs/design/tabs.md)に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-115">Developers must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="39060-116">会議アプリ API リファレンス</span><span class="sxs-lookup"><span data-stu-id="39060-116">Meeting apps API reference</span></span>

|<span data-ttu-id="39060-117">API</span><span class="sxs-lookup"><span data-stu-id="39060-117">API</span></span>|<span data-ttu-id="39060-118">説明</span><span class="sxs-lookup"><span data-stu-id="39060-118">Description</span></span>|<span data-ttu-id="39060-119">要求</span><span class="sxs-lookup"><span data-stu-id="39060-119">Request</span></span>|<span data-ttu-id="39060-120">ソース</span><span class="sxs-lookup"><span data-stu-id="39060-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="39060-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="39060-121">**GetUserContext**</span></span>| <span data-ttu-id="39060-122">関連するコンテンツを Teams タブに表示するためのコンテキスト情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="39060-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="39060-123">_**getContext (() => {/ *...* / } )**_</span><span class="sxs-lookup"><span data-stu-id="39060-123">_**microsoftTeams.getContext( ( ) => {  / *...* / } )**_</span></span>|<span data-ttu-id="39060-124">Microsoft Teams クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="39060-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="39060-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="39060-125">**GetParticipant**</span></span>|<span data-ttu-id="39060-126">この API を使用すると、ボットはミーティング id と参加者 id で参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="39060-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="39060-127">/V1/meetings/{meetingId}/participants/{participantId} を **取得** する ( _**tenantid** )_</span><span class="sxs-lookup"><span data-stu-id="39060-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="39060-128">Microsoft Bot フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="39060-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="39060-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="39060-129">**NotificationSignal**</span></span> |<span data-ttu-id="39060-130">ミーティング信号は、次の既存の会話通知 API を使用して配信されます (ユーザーのためのチャット)。</span><span class="sxs-lookup"><span data-stu-id="39060-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="39060-131">この API を使用すると、開発者はエンドユーザーのアクションに基づいて、会議中のダイアログで通知を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="39060-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="39060-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="39060-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="39060-133">Microsoft Bot フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="39060-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="39060-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="39060-134">GetUserContext</span></span>

<span data-ttu-id="39060-135">タブコンテンツのコンテキスト情報を識別して取得するためのガイダンスについては、「 [Teams のコンテキストの取得」タブ](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="39060-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="39060-136">会議機能拡張の一部として、応答ペイロードに新しい値が追加されました。</span><span class="sxs-lookup"><span data-stu-id="39060-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="39060-137">✔の会議 **id** : 会議のコンテキストで実行している場合にタブで使用されます。</span><span class="sxs-lookup"><span data-stu-id="39060-137">✔ **meetingId** : used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="39060-138">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="39060-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="39060-139">会議の開催者はいつでも役割を変更できるため、参加者の役割をキャッシュしないでください。</span><span class="sxs-lookup"><span data-stu-id="39060-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="39060-140">現時点では、Teams は、API のために350以上の参加者の大きな配布リストまたは名簿サイズをサポートしていません `GetParticipant` 。</span><span class="sxs-lookup"><span data-stu-id="39060-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="39060-141">Bot Framework SDK のサポートは近日に予定されています。</span><span class="sxs-lookup"><span data-stu-id="39060-141">Support for the Bot Framework SDK is coming soon.</span></span>

#### <a name="request"></a><span data-ttu-id="39060-142">要求</span><span class="sxs-lookup"><span data-stu-id="39060-142">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="39060-143">[Bot フレームワーク API リファレンス](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)を *参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="39060-143">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="39060-144">**C# の例**</span><span class="sxs-lookup"><span data-stu-id="39060-144">**C# Example**</span></span>

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

#### <a name="query-parameters"></a><span data-ttu-id="39060-145">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="39060-145">Query parameters</span></span>

|<span data-ttu-id="39060-146">値</span><span class="sxs-lookup"><span data-stu-id="39060-146">Value</span></span>|<span data-ttu-id="39060-147">型</span><span class="sxs-lookup"><span data-stu-id="39060-147">Type</span></span>|<span data-ttu-id="39060-148">必須</span><span class="sxs-lookup"><span data-stu-id="39060-148">Required</span></span>|<span data-ttu-id="39060-149">説明</span><span class="sxs-lookup"><span data-stu-id="39060-149">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="39060-150">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="39060-150">**meetingId**</span></span>| <span data-ttu-id="39060-151">文字列</span><span class="sxs-lookup"><span data-stu-id="39060-151">string</span></span> | <span data-ttu-id="39060-152">はい</span><span class="sxs-lookup"><span data-stu-id="39060-152">Yes</span></span> | <span data-ttu-id="39060-153">会議識別子は、ボット Invoke および Teams クライアント SDK を介して利用できます。</span><span class="sxs-lookup"><span data-stu-id="39060-153">The meeting identifier is available via Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="39060-154">**participantId**</span><span class="sxs-lookup"><span data-stu-id="39060-154">**participantId**</span></span>| <span data-ttu-id="39060-155">文字列</span><span class="sxs-lookup"><span data-stu-id="39060-155">string</span></span> | <span data-ttu-id="39060-156">はい</span><span class="sxs-lookup"><span data-stu-id="39060-156">Yes</span></span> | <span data-ttu-id="39060-157">このフィールドはユーザー ID であり、タブ SSO、Bot 呼び出し、Teams クライアント SDK で使用できます。</span><span class="sxs-lookup"><span data-stu-id="39060-157">This field is the User ID and it is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="39060-158">タブ SSO を強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="39060-158">Tab SSO is highly recommended</span></span>|
|<span data-ttu-id="39060-159">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="39060-159">**tenantId**</span></span>| <span data-ttu-id="39060-160">文字列</span><span class="sxs-lookup"><span data-stu-id="39060-160">string</span></span> | <span data-ttu-id="39060-161">はい</span><span class="sxs-lookup"><span data-stu-id="39060-161">Yes</span></span> | <span data-ttu-id="39060-162">これは、テナントのユーザーに必要です。</span><span class="sxs-lookup"><span data-stu-id="39060-162">This required for tenant users.</span></span> <span data-ttu-id="39060-163">これは、タブ SSO、Bot 呼び出し、Teams クライアント SDK で利用できます。</span><span class="sxs-lookup"><span data-stu-id="39060-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="39060-164">タブ SSO を強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="39060-164">Tab SSO is highly recommended</span></span>|

#### <a name="response-payload"></a><span data-ttu-id="39060-165">応答ペイロード</span><span class="sxs-lookup"><span data-stu-id="39060-165">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="39060-166">[ミーティング] の下の **役割** は、 *開催者* 、 *発表者* 、または *出席* 者になることができます。</span><span class="sxs-lookup"><span data-stu-id="39060-166">**role** under "meeting" can be *Organizer* , *Presenter* , or *Attendee* .</span></span>

<span data-ttu-id="39060-167">**例 1**</span><span class="sxs-lookup"><span data-stu-id="39060-167">**Example 1**</span></span>

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
#### <a name="response-codes"></a><span data-ttu-id="39060-168">応答コード</span><span class="sxs-lookup"><span data-stu-id="39060-168">Response Codes</span></span>

<span data-ttu-id="39060-169">**403** : アプリは、参加者情報を取得することを許可されていません。</span><span class="sxs-lookup"><span data-stu-id="39060-169">**403** : the app is not allowed to get participant information.</span></span> <span data-ttu-id="39060-170">これは、最も一般的なエラー応答であり、アプリがテナント管理者によって無効にされた場合や、ライブサイトの緩和時にブロックされた場合など、アプリがインストールされていない場合にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="39060-170">This will be the most common error response and is triggered when the app is not installed in the meeting such as when the app is disabled by tenant admin or blocked during live site mitigation.</span></span>  
<span data-ttu-id="39060-171">**200** : 参加者情報が正常に取得されました</span><span class="sxs-lookup"><span data-stu-id="39060-171">**200** : participant information successfully retrieved</span></span>  
<span data-ttu-id="39060-172">**401** : 無効なトークン</span><span class="sxs-lookup"><span data-stu-id="39060-172">**401** : invalid token</span></span>  
<span data-ttu-id="39060-173">**404** : 会議が存在しないか、参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="39060-173">**404** : the meeting doesn't exist or participant can’t be found.</span></span>

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="39060-174">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="39060-174">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="39060-175">会議中のダイアログが呼び出されると、同じコンテンツがチャットメッセージとして表示されることもあります。</span><span class="sxs-lookup"><span data-stu-id="39060-175">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="39060-176">要求</span><span class="sxs-lookup"><span data-stu-id="39060-176">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="39060-177">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="39060-177">Query parameters</span></span>

|<span data-ttu-id="39060-178">値</span><span class="sxs-lookup"><span data-stu-id="39060-178">Value</span></span>|<span data-ttu-id="39060-179">型</span><span class="sxs-lookup"><span data-stu-id="39060-179">Type</span></span>|<span data-ttu-id="39060-180">必須</span><span class="sxs-lookup"><span data-stu-id="39060-180">Required</span></span>|<span data-ttu-id="39060-181">説明</span><span class="sxs-lookup"><span data-stu-id="39060-181">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="39060-182">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="39060-182">**conversationId**</span></span>| <span data-ttu-id="39060-183">文字列</span><span class="sxs-lookup"><span data-stu-id="39060-183">string</span></span> | <span data-ttu-id="39060-184">はい</span><span class="sxs-lookup"><span data-stu-id="39060-184">Yes</span></span> | <span data-ttu-id="39060-185">会話 id は bot 呼び出しの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="39060-185">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="request-payload"></a><span data-ttu-id="39060-186">要求のペイロード</span><span class="sxs-lookup"><span data-stu-id="39060-186">Request Payload</span></span>

> [!NOTE]
>
> <span data-ttu-id="39060-187">以下の requeste ペイロードの externalResourceUrl に含まれる [参照入力 Tid はオプションのパラメーターです。</span><span class="sxs-lookup"><span data-stu-id="39060-187">The completionBotId in the externalResourceUrl in the requeste payload below is an optional parameter.</span></span> <span data-ttu-id="39060-188">マニフェストで宣言されている Bot ID です。</span><span class="sxs-lookup"><span data-stu-id="39060-188">It is the Bot ID that is declared in the manifest.</span></span> <span data-ttu-id="39060-189">Bot は result オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="39060-189">The bot will receive a result object.</span></span>

# <a name="json"></a>[<span data-ttu-id="39060-190">JSON</span><span class="sxs-lookup"><span data-stu-id="39060-190">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

# <a name="cnet"></a>[<span data-ttu-id="39060-191">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="39060-191">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
  {
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID"
  };
activity.ChannelData = new TeamsChannelData
  {
    Notification = notification
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="39060-192">JavaScript</span><span class="sxs-lookup"><span data-stu-id="39060-192">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> <span data-ttu-id="39060-193">コンテンツバブル (taskInfo URL) 内の URL は、Teams アプリマニフェストに含まれている [有効なドメイン](../resources/schema/manifest-schema.md#validdomains) の一覧に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-193">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="39060-194">応答コード</span><span class="sxs-lookup"><span data-stu-id="39060-194">Response Codes</span></span>

<span data-ttu-id="39060-195">**201** : シグナルが正常に送信されたアクティビティ</span><span class="sxs-lookup"><span data-stu-id="39060-195">**201** : activity with signal is successfully sent</span></span>  
<span data-ttu-id="39060-196">**401** : 無効なトークン</span><span class="sxs-lookup"><span data-stu-id="39060-196">**401** : invalid token</span></span>  
<span data-ttu-id="39060-197">**403** : アプリは、シグナルを送信することを許可されていません。</span><span class="sxs-lookup"><span data-stu-id="39060-197">**403** : the app is not allowed to send the signal.</span></span> <span data-ttu-id="39060-198">この場合、ペイロードに詳細なエラーメッセージが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-198">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="39060-199">多くの理由が考えられます。これは、テナント管理者によって無効にされたアプリ、運用サイトの移行中にブロックされたなどです。</span><span class="sxs-lookup"><span data-stu-id="39060-199">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="39060-200">**404** : 会議チャットが存在しません</span><span class="sxs-lookup"><span data-stu-id="39060-200">**404** : meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="39060-201">Teams 会議でアプリを有効にする</span><span class="sxs-lookup"><span data-stu-id="39060-201">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="39060-202">アプリのマニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="39060-202">Update your app manifest</span></span>

<span data-ttu-id="39060-203">ミーティングアプリの機能は、[アプリケーションマニフェスト] の [セキュリティの定義] **タブ**  ->  **スコープ** と **コンテキスト** 配列を使用して宣言されています。</span><span class="sxs-lookup"><span data-stu-id="39060-203">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="39060-204">*スコープ* は、アプリが使用可能になる場所と *コンテキスト* を定義します。</span><span class="sxs-lookup"><span data-stu-id="39060-204">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> * <span data-ttu-id="39060-205">[開発者プレビューマニフェストスキーマ](../resources/schema/manifest-schema-dev-preview.md)を使用して、アプリマニフェストでこれを試してください。</span><span class="sxs-lookup"><span data-stu-id="39060-205">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="39060-206">Context プロパティ</span><span class="sxs-lookup"><span data-stu-id="39060-206">Context property</span></span>

<span data-ttu-id="39060-207">Tab `context` およびプロパティは、 `scopes` アプリを表示する場所を決定できるようにするために、ハーモニーで機能します。</span><span class="sxs-lookup"><span data-stu-id="39060-207">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="39060-208">またはの範囲内のタブに `team` は、 `groupchat` 複数のコンテキストを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="39060-208">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="39060-209">Context プロパティに指定できる値は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="39060-209">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="39060-210">[ **Channeltab タブ** : チームチャネルのヘッダーのタブ。</span><span class="sxs-lookup"><span data-stu-id="39060-210">**channelTab** : a tab in the header of a team channel.</span></span>
* <span data-ttu-id="39060-211">**privateChatTab** : チームまたは会議のコンテキストではないユーザーのセット間のグループチャットのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="39060-211">**privateChatTab** : a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="39060-212">**meetingChatTab** : 予約された会議のコンテキスト内のユーザーのセット間のグループチャットのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="39060-212">**meetingChatTab** : a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="39060-213">[会議詳細] **タブ: 予定** 表の会議の詳細ビューのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="39060-213">**meetingDetailsTab** : a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="39060-214">会議の **sidepanel** : 統合バー (u バー) によって開かれた会議中のパネル。</span><span class="sxs-lookup"><span data-stu-id="39060-214">**meetingSidePanel** : an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="39060-215">"Context" プロパティは現在サポートされていないため、モバイルクライアントでは無視されます。</span><span class="sxs-lookup"><span data-stu-id="39060-215">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="39060-216">アプリを構成してシナリオをミーティングする</span><span class="sxs-lookup"><span data-stu-id="39060-216">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="39060-217">アプリケーションがタブギャラリーに表示されるようにするには、 **構成可能なタブ** と **グループチャットスコープ** をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-217">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope** .</span></span>
>
> * <span data-ttu-id="39060-218">モバイルクライアントは、会議のプレおよびポストの表面でのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="39060-218">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="39060-219">モバイルの会議中のエクスペリエンス (会議中のダイアログとパネル) は近日中に利用可能になります。</span><span class="sxs-lookup"><span data-stu-id="39060-219">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon.</span></span> <span data-ttu-id="39060-220">モバイル用のタブを作成するときに、 [[モバイル] のタブのガイダンス](../tabs/design/tabs-mobile.md) に従ってください。</span><span class="sxs-lookup"><span data-stu-id="39060-220">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span> 

### <a name="pre-meeting"></a><span data-ttu-id="39060-221">プレミーティング</span><span class="sxs-lookup"><span data-stu-id="39060-221">Pre-meeting</span></span>

<span data-ttu-id="39060-222">開催者または発表者の役割を持つユーザーは、会議 **チャット** および会議の **詳細** ページのプラス➕ボタンを使用して、会議にタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="39060-222">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="39060-223">メッセージング拡張機能は、[会話の作成メッセージ] 領域の下にある [楕円/オーバーフロー] メニュー &#x25CF;&#x25CF;&#x25CF; 経由で追加されます。</span><span class="sxs-lookup"><span data-stu-id="39060-223">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="39060-224">Bot は、"" キーを使用して会議チャットに追加され、[ **@** **ボットを取得** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="39060-224">Bots are added to a meeting chat using the " **@** " key and selecting **Get bots** .</span></span>

<span data-ttu-id="39060-225">ユーザー id は、 [タブ SSO](../tabs/how-to/authentication/auth-aad-sso.md)を使用して確認する *必要があり* ✔。</span><span class="sxs-lookup"><span data-stu-id="39060-225">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="39060-226">この認証の後、アプリは GetParticipant API を使用してユーザーロールを取得できます。</span><span class="sxs-lookup"><span data-stu-id="39060-226">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="39060-227">✔ユーザーの役割に基づいて、アプリに役割固有のエクスペリエンスを提供する機能が用意されました。</span><span class="sxs-lookup"><span data-stu-id="39060-227">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="39060-228">たとえば、投票アプリでは、開催者と発表者のみが新しい投票を作成できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="39060-228">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="39060-229">**注** : 役割の割り当ては、会議の進行中に変更できます。</span><span class="sxs-lookup"><span data-stu-id="39060-229">**NOTE** : Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="39060-230">*「* [Teams Meeting の役割](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39060-230">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="39060-231">会議中</span><span class="sxs-lookup"><span data-stu-id="39060-231">In-meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="39060-232">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="39060-232">**sidePanel**</span></span>

<span data-ttu-id="39060-233">アプリマニフェスト内の✔前述のように、 **コンテキスト** 配列に **sidepanel** を追加します。</span><span class="sxs-lookup"><span data-stu-id="39060-233">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="39060-234">会議の✔とすべてのシナリオにおいて、アプリは、ため320px ですの幅で表示される [会議中] タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="39060-234">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="39060-235">このためにタブを最適化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-235">Your tab must be optimized for this.</span></span> <span data-ttu-id="39060-236">*参照* 、 [framecontext インターフェイス](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="39060-236">*See* , [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span></span>

<span data-ttu-id="39060-237">**UserContext** API を使用して要求を適切にルーティングするには、 [Teams SDK](../tabs/how-to/access-teams-context.md#user-context)を参照してください✔。</span><span class="sxs-lookup"><span data-stu-id="39060-237">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="39060-238">✔ [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39060-238">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="39060-239">タブの認証フローは、web サイトの認証フローとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="39060-239">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="39060-240">そのため、タブは OAuth 2.0 を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="39060-240">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="39060-241">「 [Microsoft identity platform And OAuth 2.0 認証コードフロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow) *」も参照して* ください。</span><span class="sxs-lookup"><span data-stu-id="39060-241">*See also* , [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="39060-242">**会議中のダイアログ**</span><span class="sxs-lookup"><span data-stu-id="39060-242">**in-meeting dialog**</span></span>

<span data-ttu-id="39060-243">✔ [会議中のダイアログの設計ガイドライン](design/designing-in-meeting-dialog.md)に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-243">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="39060-244">✔ [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39060-244">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="39060-245">✔ [通知](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API を使用して、バブル通知がトリガーされる必要があることを通知します。</span><span class="sxs-lookup"><span data-stu-id="39060-245">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="39060-246">✔通知要求のペイロードの一部として、紹介するコンテンツがホストされる URL を含めます。</span><span class="sxs-lookup"><span data-stu-id="39060-246">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="39060-247">これらの通知は、本質的に永続的なものです。</span><span class="sxs-lookup"><span data-stu-id="39060-247">These notifications are persistent in nature.</span></span> <span data-ttu-id="39060-248">ユーザーが web ビューでアクションを実行した後に、 [**Submittask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出して自動消去する必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-248">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="39060-249">これは、アプリを送信するための要件です。</span><span class="sxs-lookup"><span data-stu-id="39060-249">This is a requirement for app submission.</span></span> <span data-ttu-id="39060-250">「 [TEAMS SDK: タスクモジュール](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true) *」も参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="39060-250">*See also* , [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="39060-251">アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求のペイロードは、( `from.id` `from` `from.aadObjectId` ユーザーの AZURE Active Directory ID) 要求メタデータではなく、オブジェクト内の (ユーザーの ID) 要求メタデータに依存している必要があります。</span><span class="sxs-lookup"><span data-stu-id="39060-251">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="39060-252">*「* [タスクモジュールを使用して](../task-modules-and-cards/task-modules/task-modules-tabs.md) タスク [モジュールを作成し、送信](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="39060-252">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="39060-253">会議後</span><span class="sxs-lookup"><span data-stu-id="39060-253">Post-meeting</span></span>

<span data-ttu-id="39060-254">ポストミーティングと事前会議の構成は同等です。</span><span class="sxs-lookup"><span data-stu-id="39060-254">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="39060-255">会議アプリのサンプル</span><span class="sxs-lookup"><span data-stu-id="39060-255">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="39060-256">会議トークン生成アプリ</span><span class="sxs-lookup"><span data-stu-id="39060-256">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
