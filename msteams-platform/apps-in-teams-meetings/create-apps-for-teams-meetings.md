---
title: Teams 会議用のアプリを作成する
author: laujan
description: teams 会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: 847e79d188a52892cda8732a2b58cee068cb5e95
ms.sourcegitcommit: e92408e751a8f51028908ab7e2415a8051a536c0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2020
ms.locfileid: "48326306"
---
# <a name="create-apps-for-teams-meetings-release-preview"></a><span data-ttu-id="b275b-104">Teams 会議用のアプリを作成する (リリースプレビュー)</span><span class="sxs-lookup"><span data-stu-id="b275b-104">Create apps for Teams meetings (Release Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="b275b-105">Microsoft Teams のリリースプレビューで強調表示されている機能は、初期の洞察とフィードバックのみを目的として提供されています。</span><span class="sxs-lookup"><span data-stu-id="b275b-105">Features highlighted in Microsoft Teams Release Preview are provided for early insight and feedback purposes only.</span></span> <span data-ttu-id="b275b-106">これらは、有効になる前に変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-106">They may undergo changes before they can be enabled.</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="b275b-107">前提条件と考慮事項</span><span class="sxs-lookup"><span data-stu-id="b275b-107">Prerequisites and considerations</span></span>

1. <span data-ttu-id="b275b-108">会議のアプリには、 [Teams アプリ開発](../overview.md)に関する基本的な知識が必要です。</span><span class="sxs-lookup"><span data-stu-id="b275b-108">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="b275b-109">会議のアプリは、 [タブ](../tabs/what-are-tabs.md)、 [ボット](../bots/what-are-bots.md)、および [メッセージングの拡張](../messaging-extensions/what-are-messaging-extensions.md) 機能で構成され、Teams アプリの [マニフェスト](#update-your-app-manifest) を更新して、アプリが会議で利用できることを示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-109">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="b275b-110">アプリが会議のライフサイクルでタブとして機能するには、 [groupchat スコープ](../resources/schema/manifest-schema.md#configurabletabs)で構成可能なタブをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-110">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="b275b-111">*「* [カスタムタブを使用して Teams アプリを拡張する](../tabs/how-to/add-tab.md)」を参照してください。スコープをサポートすること `groupchat` で、 [プレミーティング](teams-apps-in-meetings.md#pre-meeting-app-experience) および [ミーティング後](teams-apps-in-meetings.md#post-meeting-app-experience) のチャットでアプリを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="b275b-111">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="b275b-112">ミーティング API URL パラメーターには、、が必要な場合があり `meetingId` `userId` ます。また、 [TenantId](/onedrive/find-your-office-365-tenant-id) は Teams クライアント SDK および bot アクティビティの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="b275b-112">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="b275b-113">さらに、 [TAB SSO 認証](../tabs/how-to/authentication/auth-aad-sso.md)を使用して、ユーザー id とテナント id の信頼できる情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="b275b-113">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="b275b-114">などの一部の会議 Api で `GetParticipant` は、 [ボット登録と BOT アプリ ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) が認証トークンを生成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-114">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="b275b-115">開発者は、チームの会議中にトリガー[される会議](design/designing-in-meeting-dialog.md)中のダイアログのための、会議前およびミーティング後のシナリオのための [teams][タブデザインのガイドライン](../tabs/design/tabs.md)に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-115">Developers must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="b275b-116">会議アプリ API リファレンス</span><span class="sxs-lookup"><span data-stu-id="b275b-116">Meeting apps API reference</span></span>

|<span data-ttu-id="b275b-117">API</span><span class="sxs-lookup"><span data-stu-id="b275b-117">API</span></span>|<span data-ttu-id="b275b-118">説明</span><span class="sxs-lookup"><span data-stu-id="b275b-118">Description</span></span>|<span data-ttu-id="b275b-119">要求</span><span class="sxs-lookup"><span data-stu-id="b275b-119">Request</span></span>|<span data-ttu-id="b275b-120">ソース</span><span class="sxs-lookup"><span data-stu-id="b275b-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="b275b-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="b275b-121">**GetUserContext**</span></span>| <span data-ttu-id="b275b-122">関連するコンテンツを Teams タブに表示するためのコンテキスト情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="b275b-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="b275b-123">_**getContext (() => {/*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="b275b-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="b275b-124">Microsoft Teams クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="b275b-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="b275b-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="b275b-125">**GetParticipant**</span></span>|<span data-ttu-id="b275b-126">この API を使用すると、ボットはミーティング id と参加者 id で参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="b275b-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="b275b-127">/V1/meetings/{meetingId}/participants/{participantId} を**取得**する ( _ **tenantid** )_</span><span class="sxs-lookup"><span data-stu-id="b275b-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="b275b-128">Microsoft Bot フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="b275b-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="b275b-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="b275b-129">**NotificationSignal**</span></span> |<span data-ttu-id="b275b-130">ミーティング信号は、次の既存の会話通知 API を使用して配信されます (ユーザーのためのチャット)。</span><span class="sxs-lookup"><span data-stu-id="b275b-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="b275b-131">この API を使用すると、開発者はエンドユーザーのアクションに基づいて、会議中のダイアログで通知を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="b275b-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="b275b-132">**POST** _ **/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="b275b-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="b275b-133">Microsoft Bot フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="b275b-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="b275b-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="b275b-134">GetUserContext</span></span>

<span data-ttu-id="b275b-135">タブコンテンツのコンテキスト情報を識別して取得するためのガイダンスについては、「 [Teams のコンテキストの取得」タブ](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b275b-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="b275b-136">会議機能拡張の一部として、応答ペイロードに新しい値が追加されました。</span><span class="sxs-lookup"><span data-stu-id="b275b-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="b275b-137">✔の会議 **id**: 会議のコンテキストで実行している場合にタブで使用されます。</span><span class="sxs-lookup"><span data-stu-id="b275b-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="b275b-138">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="b275b-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="b275b-139">会議の開催者はいつでも役割を変更できるため、参加者の役割をキャッシュしないでください。</span><span class="sxs-lookup"><span data-stu-id="b275b-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="b275b-140">現時点では、Teams は、API のために350以上の参加者の大きな配布リストまたは名簿サイズをサポートしていません `GetParticipant` 。</span><span class="sxs-lookup"><span data-stu-id="b275b-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="b275b-141">Bot Framework SDK のサポートは近日に予定されています。</span><span class="sxs-lookup"><span data-stu-id="b275b-141">Support for the Bot Framework SDK is coming soon.</span></span>

#### <a name="request"></a><span data-ttu-id="b275b-142">要求</span><span class="sxs-lookup"><span data-stu-id="b275b-142">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="b275b-143">[Bot フレームワーク API リファレンス](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="b275b-143">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="b275b-144">**C# の例**</span><span class="sxs-lookup"><span data-stu-id="b275b-144">**C# Example**</span></span>

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
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a><span data-ttu-id="b275b-145">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="b275b-145">Query parameters</span></span>

<span data-ttu-id="b275b-146">**会議 id**。</span><span class="sxs-lookup"><span data-stu-id="b275b-146">**meetingId**.</span></span> <span data-ttu-id="b275b-147">会議識別子が必要です。</span><span class="sxs-lookup"><span data-stu-id="b275b-147">The meeting identifier is required.</span></span>  
<span data-ttu-id="b275b-148">**participantId**。</span><span class="sxs-lookup"><span data-stu-id="b275b-148">**participantId**.</span></span> <span data-ttu-id="b275b-149">参加者識別子が必要です。</span><span class="sxs-lookup"><span data-stu-id="b275b-149">The participant identifier is required.</span></span>  
<span data-ttu-id="b275b-150">**tenantId**。</span><span class="sxs-lookup"><span data-stu-id="b275b-150">**tenantId**.</span></span> <span data-ttu-id="b275b-151">参加者の[テナント id](/onedrive/find-your-office-365-tenant-id) 。</span><span class="sxs-lookup"><span data-stu-id="b275b-151">[Tenant id](/onedrive/find-your-office-365-tenant-id) of the participant.</span></span> <span data-ttu-id="b275b-152">テナントユーザーにとって必須です。</span><span class="sxs-lookup"><span data-stu-id="b275b-152">Required for tenant user.</span></span>

#### <a name="response-payload"></a><span data-ttu-id="b275b-153">応答ペイロード</span><span class="sxs-lookup"><span data-stu-id="b275b-153">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="b275b-154">**例 1**</span><span class="sxs-lookup"><span data-stu-id="b275b-154">**Example 1**</span></span>

```json
{
    "meetingRole":"Presenter",
    "conversation":{
            "isGroup": true,
            "id": "19:meeting_NDQxMzg1YjUtMGIzNC00Yjc1LWFmYWYtYzk1MGY2MTMwNjE0@thread.v2"
        }
}
```

<span data-ttu-id="b275b-155">**会議の役割** は、 *開催者*、 *発表者*、または *出席*者になることができます。</span><span class="sxs-lookup"><span data-stu-id="b275b-155">**meetingRole** can be *Organizer*, *Presenter*, or *Attendee*.</span></span>

<span data-ttu-id="b275b-156">**例 2**</span><span class="sxs-lookup"><span data-stu-id="b275b-156">**Example 2**</span></span>

```json
{
   "meetingRole":"Presenter",
   "conversation":{
      "isGroup":true,
      "id":"19:meeting_NDQxMzg1YjUtMGIzNC00Yjc1LWFmYWYtYzk1MGY2MTMwNjE0@thread.v2"
   }
}
```

#### <a name="response-codes"></a><span data-ttu-id="b275b-157">応答コード</span><span class="sxs-lookup"><span data-stu-id="b275b-157">Response Codes</span></span>

<span data-ttu-id="b275b-158">**403**: アプリは、参加者情報を取得することを許可されていません。</span><span class="sxs-lookup"><span data-stu-id="b275b-158">**403**: the app is not allowed to get participant information.</span></span> <span data-ttu-id="b275b-159">これは、最も一般的なエラー応答であり、アプリがテナント管理者によって無効にされた場合や、ライブサイトの緩和時にブロックされた場合など、アプリがインストールされていない場合にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="b275b-159">This will be the most common error response and is triggered when the app is not installed in the meeting such as when the app is disabled by tenant admin or blocked during live site mitigation.</span></span>  
<span data-ttu-id="b275b-160">**200**: 参加者情報が正常に取得されました</span><span class="sxs-lookup"><span data-stu-id="b275b-160">**200**: participant information successfully retrieved</span></span>  
<span data-ttu-id="b275b-161">**401**: 無効なトークン</span><span class="sxs-lookup"><span data-stu-id="b275b-161">**401**: invalid token</span></span>  
<span data-ttu-id="b275b-162">**404**: 会議が存在しないか、参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="b275b-162">**404**: the meeting doesn't exist or participant can’t be found.</span></span>

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="b275b-163">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="b275b-163">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="b275b-164">会議中のダイアログが呼び出されると、同じコンテンツがチャットメッセージとして表示されることもあります。</span><span class="sxs-lookup"><span data-stu-id="b275b-164">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="b275b-165">要求</span><span class="sxs-lookup"><span data-stu-id="b275b-165">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="b275b-166">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="b275b-166">Query parameters</span></span>

<span data-ttu-id="b275b-167">**conversationId**: 会話 id。</span><span class="sxs-lookup"><span data-stu-id="b275b-167">**conversationId**: The conversation identifier.</span></span> <span data-ttu-id="b275b-168">必須</span><span class="sxs-lookup"><span data-stu-id="b275b-168">Required</span></span>

#### <a name="request-payload"></a><span data-ttu-id="b275b-169">要求のペイロード</span><span class="sxs-lookup"><span data-stu-id="b275b-169">Request Payload</span></span>

# <a name="json"></a>[<span data-ttu-id="b275b-170">JSON</span><span class="sxs-lookup"><span data-stu-id="b275b-170">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
    "notification": {
    "alertInMeeting": true,
    "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
    }
},
    "replyToId": "1493070356924"
    }
```

# <a name="cnet"></a>[<span data-ttu-id="b275b-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b275b-171">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
{
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
};
activity.ChannelData = new TeamsChannelData
{
    Notification = notification
};
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="b275b-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b275b-172">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
        replyActivity.channelData = {
            notification: {
                alertInMeeting: true,
                externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>’
            }
        };
        await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> <span data-ttu-id="b275b-173">コンテンツバブル (taskInfo URL) 内の URL は、Teams アプリマニフェストに含まれている [有効なドメイン](../resources/schema/manifest-schema.md#validdomains) の一覧に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-173">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="b275b-174">応答コード</span><span class="sxs-lookup"><span data-stu-id="b275b-174">Response Codes</span></span>

<span data-ttu-id="b275b-175">**201**: シグナルが正常に送信されたアクティビティ</span><span class="sxs-lookup"><span data-stu-id="b275b-175">**201**: activity with signal is successfully sent</span></span>  
<span data-ttu-id="b275b-176">**401**: 無効なトークン</span><span class="sxs-lookup"><span data-stu-id="b275b-176">**401**: invalid token</span></span>  
<span data-ttu-id="b275b-177">**403**: アプリは、シグナルを送信することを許可されていません。</span><span class="sxs-lookup"><span data-stu-id="b275b-177">**403**: the app is not allowed to send the signal.</span></span> <span data-ttu-id="b275b-178">この場合、ペイロードに詳細なエラーメッセージが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-178">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="b275b-179">多くの理由が考えられます。これは、テナント管理者によって無効にされたアプリ、運用サイトの移行中にブロックされたなどです。</span><span class="sxs-lookup"><span data-stu-id="b275b-179">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="b275b-180">**404**: 会議チャットが存在しません</span><span class="sxs-lookup"><span data-stu-id="b275b-180">**404**: meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="b275b-181">Teams 会議でアプリを有効にする</span><span class="sxs-lookup"><span data-stu-id="b275b-181">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="b275b-182">アプリのマニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="b275b-182">Update your app manifest</span></span>

<span data-ttu-id="b275b-183">ミーティングアプリの機能は、[アプリケーションマニフェスト] の [セキュリティの定義]**タブ**  ->  **スコープ**と**コンテキスト**配列を使用して宣言されています。</span><span class="sxs-lookup"><span data-stu-id="b275b-183">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="b275b-184">*スコープ* は、アプリが使用可能になる場所と *コンテキスト* を定義します。</span><span class="sxs-lookup"><span data-stu-id="b275b-184">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="b275b-185">[開発者プレビューマニフェストスキーマ](../resources/schema/manifest-schema-dev-preview.md)を使用して、アプリマニフェストでこれを試してください。</span><span class="sxs-lookup"><span data-stu-id="b275b-185">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="b275b-186">Context プロパティ</span><span class="sxs-lookup"><span data-stu-id="b275b-186">Context property</span></span>

<span data-ttu-id="b275b-187">Tab `context` およびプロパティは、 `scopes` アプリを表示する場所を決定できるようにするために、ハーモニーで機能します。</span><span class="sxs-lookup"><span data-stu-id="b275b-187">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="b275b-188">またはの範囲内のタブに `team` は、 `groupchat` 複数のコンテキストを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="b275b-188">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="b275b-189">Context プロパティに指定できる値は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b275b-189">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="b275b-190">[ **Channeltab タブ**: チームチャネルのヘッダーのタブ。</span><span class="sxs-lookup"><span data-stu-id="b275b-190">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="b275b-191">**privateChatTab**: チームまたは会議のコンテキストではないユーザーのセット間のグループチャットのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="b275b-191">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="b275b-192">**meetingChatTab**: 予約された会議のコンテキスト内のユーザーのセット間のグループチャットのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="b275b-192">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="b275b-193">[会議詳細]**タブ: 予定**表の会議の詳細ビューのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="b275b-193">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="b275b-194">会議の**sidepanel**: 統合バー (u バー) によって開かれた会議中のパネル。</span><span class="sxs-lookup"><span data-stu-id="b275b-194">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="b275b-195">アプリを構成してシナリオをミーティングする</span><span class="sxs-lookup"><span data-stu-id="b275b-195">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> <span data-ttu-id="b275b-196">アプリケーションがタブギャラリーに表示されるようにするには、 **構成可能なタブ** と **グループチャットスコープ**をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-196">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>

### <a name="pre-meeting"></a><span data-ttu-id="b275b-197">プレミーティング</span><span class="sxs-lookup"><span data-stu-id="b275b-197">Pre-meeting</span></span>

<span data-ttu-id="b275b-198">開催者または発表者の役割を持つユーザーは、会議 **チャット** および会議の **詳細** ページのプラス➕ボタンを使用して、会議にタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="b275b-198">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="b275b-199">メッセージング拡張機能は、[会話の作成メッセージ] 領域の下にある [楕円/オーバーフロー] メニュー &#x25CF;&#x25CF;&#x25CF; 経由で追加されます。</span><span class="sxs-lookup"><span data-stu-id="b275b-199">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="b275b-200">Bot は、"" キーを使用して会議チャットに追加され、[ **@** **ボットを取得**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b275b-200">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="b275b-201">ユーザー id は、[タブ SSO](../tabs/how-to/authentication/auth-aad-sso.md)を使用して確認する*必要があり*✔。</span><span class="sxs-lookup"><span data-stu-id="b275b-201">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="b275b-202">この認証の後、アプリは GetParticipant API を使用してユーザーロールを取得できます。</span><span class="sxs-lookup"><span data-stu-id="b275b-202">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="b275b-203">✔ユーザーの役割に基づいて、アプリに役割固有のエクスペリエンスを提供する機能が用意されました。</span><span class="sxs-lookup"><span data-stu-id="b275b-203">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="b275b-204">たとえば、投票アプリでは、開催者と発表者のみが新しい投票を作成できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="b275b-204">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="b275b-205">**注**: 役割の割り当ては、会議の進行中に変更できます。</span><span class="sxs-lookup"><span data-stu-id="b275b-205">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="b275b-206">*「* [Teams Meeting の役割](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b275b-206">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="b275b-207">会議中</span><span class="sxs-lookup"><span data-stu-id="b275b-207">In-meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="b275b-208">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="b275b-208">**sidePanel**</span></span>

<span data-ttu-id="b275b-209">アプリマニフェスト内の✔前述のように、**コンテキスト**配列に**sidepanel**を追加します。</span><span class="sxs-lookup"><span data-stu-id="b275b-209">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="b275b-210">会議の✔とすべてのシナリオにおいて、アプリは、ため320px ですの幅で表示される [会議中] タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="b275b-210">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="b275b-211">このためにタブを最適化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-211">Your tab must be optimized for this.</span></span> <span data-ttu-id="b275b-212">*参照*、 [framecontext インターフェイス](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="b275b-212">*See*, [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span></span>

<span data-ttu-id="b275b-213">**UserContext** API を使用して要求を適切にルーティングするには、 [Teams SDK](../tabs/how-to/access-teams-context.md#user-context)を参照してください✔。</span><span class="sxs-lookup"><span data-stu-id="b275b-213">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="b275b-214">✔ [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b275b-214">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="b275b-215">タブの認証フローは、web サイトの認証フローとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="b275b-215">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="b275b-216">そのため、タブは OAuth 2.0 を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="b275b-216">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="b275b-217">「 [Microsoft identity platform And OAuth 2.0 認証コードフロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow) *」も参照して*ください。</span><span class="sxs-lookup"><span data-stu-id="b275b-217">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="b275b-218">**会議中のダイアログ**</span><span class="sxs-lookup"><span data-stu-id="b275b-218">**in-meeting dialog**</span></span>

<span data-ttu-id="b275b-219">✔ [会議中のダイアログの設計ガイドライン](design/designing-in-meeting-dialog.md)に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-219">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="b275b-220">✔ [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b275b-220">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="b275b-221">✔ [通知](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API を使用して、バブル通知がトリガーされる必要があることを通知します。</span><span class="sxs-lookup"><span data-stu-id="b275b-221">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="b275b-222">✔通知要求のペイロードの一部として、紹介するコンテンツがホストされる URL を含めます。</span><span class="sxs-lookup"><span data-stu-id="b275b-222">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="b275b-223">これらの通知は、本質的に永続的なものです。</span><span class="sxs-lookup"><span data-stu-id="b275b-223">These notifications are persistent in nature.</span></span> <span data-ttu-id="b275b-224">ユーザーが web ビューでアクションを実行した後に、 [**Submittask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出して自動消去する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-224">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="b275b-225">これは、アプリを送信するための要件です。</span><span class="sxs-lookup"><span data-stu-id="b275b-225">This is a requirement for app submission.</span></span> <span data-ttu-id="b275b-226">「 [TEAMS SDK: タスクモジュール](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true) *」も参照してください*。</span><span class="sxs-lookup"><span data-stu-id="b275b-226">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="b275b-227">アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求のペイロードは、( `from.id` `from` `from.aadObjectId` ユーザーの AZURE Active Directory ID) 要求メタデータではなく、オブジェクト内の (ユーザーの ID) 要求メタデータに依存している必要があります。</span><span class="sxs-lookup"><span data-stu-id="b275b-227">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="b275b-228">*「* [タスクモジュールを使用して](../task-modules-and-cards/task-modules/task-modules-tabs.md) タスク [モジュールを作成し、送信](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b275b-228">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="b275b-229">会議後</span><span class="sxs-lookup"><span data-stu-id="b275b-229">Post-meeting</span></span>

<span data-ttu-id="b275b-230">ポストミーティングと事前会議の構成は同等です。</span><span class="sxs-lookup"><span data-stu-id="b275b-230">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="b275b-231">会議アプリのサンプル</span><span class="sxs-lookup"><span data-stu-id="b275b-231">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="b275b-232">会議トークン生成アプリ</span><span class="sxs-lookup"><span data-stu-id="b275b-232">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
