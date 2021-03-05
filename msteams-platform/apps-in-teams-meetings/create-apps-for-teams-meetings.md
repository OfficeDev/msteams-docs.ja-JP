---
title: Teams 会議用のアプリを作成する
author: laujan
description: チーム会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: bd0f53ae34a23bdbbdc2e6f3992c7dd0836e9f28
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449494"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="d95ef-104">Teams 会議用のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="d95ef-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="d95ef-105">前提条件と考慮事項</span><span class="sxs-lookup"><span data-stu-id="d95ef-105">Prerequisites and considerations</span></span>

* <span data-ttu-id="d95ef-106">会議のアプリには、Teams アプリ開発に関する基本的 [な知識が必要です](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="d95ef-107">会議内のアプリは、タブ、[](../tabs/what-are-tabs.md)ボット、[](../bots/what-are-bots.md)メッセージング拡張機能の機能[](../messaging-extensions/what-are-messaging-extensions.md)で構成され、アプリが会議で使用できるかどうかを示すために[Teams](#update-your-app-manifest)アプリ マニフェストの更新が必要になります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

* <span data-ttu-id="d95ef-108">アプリが会議のライフサイクルでタブとして機能するには [、groupchat](../resources/schema/manifest-schema.md#configurabletabs) スコープで構成可能なタブをサポートする必要があります (「グループ タブを作成する方法」 [を参照](../build-your-first-app/build-channel-tab.md))。</span><span class="sxs-lookup"><span data-stu-id="d95ef-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) (see how to [build a group tab](../build-your-first-app/build-channel-tab.md)).</span></span> <span data-ttu-id="d95ef-109">スコープを `groupchat` サポートすると、会議前および[](teams-apps-in-meetings.md#pre-meeting-app-experience)会議後のチャットで[アプリを](teams-apps-in-meetings.md#post-meeting-app-experience)有効にできます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-109">Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

* <span data-ttu-id="d95ef-110">会議 API の URL パラメーターには、Teams クライアント SDK とボット アクティビティの一部として使用できる 、、 `meetingId` `userId` および [tenantId](/onedrive/find-your-office-365-tenant-id) が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="d95ef-111">さらに、ユーザー ID とテナント ID の信頼できる情報は、Tab SSO 認証を使用 [して取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="d95ef-112">会議 API の中には、認証トークンを生成するためにボット登録と `GetParticipant` [ID](../build-your-first-app/build-bot.md) が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-112">Some meeting APIs, such as `GetParticipant`, require a [bot registration and ID](../build-your-first-app/build-bot.md) to generate auth tokens.</span></span>

* <span data-ttu-id="d95ef-113">会議前および会議後のシナリオでは、一般的な [Teams](../tabs/design/tabs.md) タブ設計ガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-113">You must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="d95ef-114">会議中のエクスペリエンスについては、「会議内タブ」と [「](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) 会議内ダイアログ [の設計ガイドライン」を](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) 参照してください。</span><span class="sxs-lookup"><span data-stu-id="d95ef-114">For experiences during meetings, refer to the [in-meeting tab](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) design guidelines.</span></span>

* <span data-ttu-id="d95ef-115">アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-115">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="d95ef-116">これらのイベントは、会議中のダイアログ (完了パラメーターを参照) 内に含め、会議のライフサイクル全体にわたって他 `bot Id` `Notification Signal API` のサーフェスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-116">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="d95ef-117">会議アプリ API リファレンス</span><span class="sxs-lookup"><span data-stu-id="d95ef-117">Meeting apps API reference</span></span>

|<span data-ttu-id="d95ef-118">API</span><span class="sxs-lookup"><span data-stu-id="d95ef-118">API</span></span>|<span data-ttu-id="d95ef-119">説明</span><span class="sxs-lookup"><span data-stu-id="d95ef-119">Description</span></span>|<span data-ttu-id="d95ef-120">要求</span><span class="sxs-lookup"><span data-stu-id="d95ef-120">Request</span></span>|<span data-ttu-id="d95ef-121">ソース</span><span class="sxs-lookup"><span data-stu-id="d95ef-121">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="d95ef-122">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="d95ef-122">**GetUserContext**</span></span>| <span data-ttu-id="d95ef-123">関連するコンテンツを Teams タブに表示するコンテキスト情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="d95ef-123">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="d95ef-124">_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="d95ef-124">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="d95ef-125">Microsoft Teams クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="d95ef-125">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="d95ef-126">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="d95ef-126">**GetParticipant**</span></span>|<span data-ttu-id="d95ef-127">この API を使用すると、ボットは会議 ID と参加者 ID によって参加者情報をフェッチできます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-127">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="d95ef-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="d95ef-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="d95ef-129">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="d95ef-129">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="d95ef-130">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="d95ef-130">**NotificationSignal**</span></span> |<span data-ttu-id="d95ef-131">会議シグナルは、次の既存の会話通知 API (ユーザー ボット チャット用) を使用して配信されます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-131">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="d95ef-132">この API を使用すると、開発者はエンド ユーザー のアクションに基づいて、会議中のダイアログ バブルを表示できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-132">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="d95ef-133">**POST** _**/v3/conversation/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="d95ef-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="d95ef-134">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="d95ef-134">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="d95ef-135">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="d95ef-135">GetUserContext</span></span>

<span data-ttu-id="d95ef-136">タブ コンテンツのコンテキスト情報の特定と取得に関するガイダンスについては [、Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) タブドキュメントのコンテキストの取得を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d95ef-136">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="d95ef-137">会議の機能拡張の一環として、応答ペイロードに新しい値が追加されました。</span><span class="sxs-lookup"><span data-stu-id="d95ef-137">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="d95ef-138">✔ **meetingId**: 会議コンテキストで実行するときにタブによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-138">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="d95ef-139">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="d95ef-139">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="d95ef-140">会議開催者は任意の時点で役割を変更できるので、参加者の役割をキャッシュしない。</span><span class="sxs-lookup"><span data-stu-id="d95ef-140">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="d95ef-141">Teams は現在、API の大きな配布リストや 350 人を超える参加者の名簿サイズをサポート `GetParticipant` していない。</span><span class="sxs-lookup"><span data-stu-id="d95ef-141">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="d95ef-142">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="d95ef-142">Query parameters</span></span>

|<span data-ttu-id="d95ef-143">値</span><span class="sxs-lookup"><span data-stu-id="d95ef-143">Value</span></span>|<span data-ttu-id="d95ef-144">型</span><span class="sxs-lookup"><span data-stu-id="d95ef-144">Type</span></span>|<span data-ttu-id="d95ef-145">必須</span><span class="sxs-lookup"><span data-stu-id="d95ef-145">Required</span></span>|<span data-ttu-id="d95ef-146">説明</span><span class="sxs-lookup"><span data-stu-id="d95ef-146">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="d95ef-147">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="d95ef-147">**meetingId**</span></span>| <span data-ttu-id="d95ef-148">文字列</span><span class="sxs-lookup"><span data-stu-id="d95ef-148">string</span></span> | <span data-ttu-id="d95ef-149">はい</span><span class="sxs-lookup"><span data-stu-id="d95ef-149">Yes</span></span> | <span data-ttu-id="d95ef-150">会議識別子は、ボットの呼び出しと Teams クライアント SDK を使用して使用できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-150">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="d95ef-151">**participantId**</span><span class="sxs-lookup"><span data-stu-id="d95ef-151">**participantId**</span></span>| <span data-ttu-id="d95ef-152">文字列</span><span class="sxs-lookup"><span data-stu-id="d95ef-152">string</span></span> | <span data-ttu-id="d95ef-153">はい</span><span class="sxs-lookup"><span data-stu-id="d95ef-153">Yes</span></span> | <span data-ttu-id="d95ef-154">participantId はユーザー ID です。</span><span class="sxs-lookup"><span data-stu-id="d95ef-154">The participantId is the user ID.</span></span> <span data-ttu-id="d95ef-155">これは、Tab SSO、Bot Invoke、Teams クライアント SDK で使用できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-155">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="d95ef-156">Tab SSO から参加者 Id を取得することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d95ef-156">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="d95ef-157">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="d95ef-157">**tenantId**</span></span>| <span data-ttu-id="d95ef-158">文字列</span><span class="sxs-lookup"><span data-stu-id="d95ef-158">string</span></span> | <span data-ttu-id="d95ef-159">はい</span><span class="sxs-lookup"><span data-stu-id="d95ef-159">Yes</span></span> | <span data-ttu-id="d95ef-160">テナント ユーザーには tenantId が必要です。</span><span class="sxs-lookup"><span data-stu-id="d95ef-160">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="d95ef-161">これは、Tab SSO、Bot Invoke、Teams クライアント SDK で使用できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-161">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="d95ef-162">Tab SSO から tenantId を取得することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d95ef-162">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="d95ef-163">例</span><span class="sxs-lookup"><span data-stu-id="d95ef-163">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="d95ef-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d95ef-164">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}

```

# <a name="javascript"></a>[<span data-ttu-id="d95ef-165">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d95ef-165">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="d95ef-166">JSON</span><span class="sxs-lookup"><span data-stu-id="d95ef-166">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="d95ef-167">応答本文は次の場合です。</span><span class="sxs-lookup"><span data-stu-id="d95ef-167">The response body is:</span></span>

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "isGroup":true
   }
}
```

* * *

#### <a name="response-codes"></a><span data-ttu-id="d95ef-168">応答コード</span><span class="sxs-lookup"><span data-stu-id="d95ef-168">Response codes</span></span>

* <span data-ttu-id="d95ef-169">**403**: アプリで参加者情報を取得できない。</span><span class="sxs-lookup"><span data-stu-id="d95ef-169">**403**: The app is not allowed to get participant information.</span></span> <span data-ttu-id="d95ef-170">これは最も一般的なエラー応答であり、アプリが会議にインストールされていない場合にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-170">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="d95ef-171">たとえば、テナント管理者がアプリを無効にした場合や、生活者の軽減中にブロックされている場合などです。</span><span class="sxs-lookup"><span data-stu-id="d95ef-171">For example, if the app is disabled by tenant admin or blocked during livesite mitigation.</span></span>
* <span data-ttu-id="d95ef-172">**200**: 参加者情報が正常に取得されました。</span><span class="sxs-lookup"><span data-stu-id="d95ef-172">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="d95ef-173">**401**: トークンが無効です。</span><span class="sxs-lookup"><span data-stu-id="d95ef-173">**401**: Invalid token.</span></span>
* <span data-ttu-id="d95ef-174">**404**: 参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="d95ef-174">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="d95ef-175">**500**: 会議の有効期限が切れているか (会議が終了して 60 日を超える) か、参加者が自分の役割に基づいてアクセス許可を持っていません。</span><span class="sxs-lookup"><span data-stu-id="d95ef-175">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="d95ef-176">**近日公開**</span><span class="sxs-lookup"><span data-stu-id="d95ef-176">**Coming Soon**</span></span>

* <span data-ttu-id="d95ef-177">**404**: 会議の有効期限が切れているか、参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="d95ef-177">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="d95ef-178">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="d95ef-178">NotificationSignal API</span></span>

<span data-ttu-id="d95ef-179">会議のすべてのユーザーは、NotificationSignal API を介して送信された通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-179">All users in a meeting receive the notifications sent through the NotificationSignal API.</span></span>

> [!NOTE]
> <span data-ttu-id="d95ef-180">現在、ターゲット通知の送信はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d95ef-180">Currently, sending targetted notifications is not supported.</span></span>
> <span data-ttu-id="d95ef-181">会議中のダイアログが呼び出されると、同じコンテンツもチャット メッセージとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-181">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="d95ef-182">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="d95ef-182">Query parameters</span></span>

|<span data-ttu-id="d95ef-183">値</span><span class="sxs-lookup"><span data-stu-id="d95ef-183">Value</span></span>|<span data-ttu-id="d95ef-184">型</span><span class="sxs-lookup"><span data-stu-id="d95ef-184">Type</span></span>|<span data-ttu-id="d95ef-185">必須</span><span class="sxs-lookup"><span data-stu-id="d95ef-185">Required</span></span>|<span data-ttu-id="d95ef-186">説明</span><span class="sxs-lookup"><span data-stu-id="d95ef-186">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="d95ef-187">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="d95ef-187">**conversationId**</span></span>| <span data-ttu-id="d95ef-188">文字列</span><span class="sxs-lookup"><span data-stu-id="d95ef-188">string</span></span> | <span data-ttu-id="d95ef-189">はい</span><span class="sxs-lookup"><span data-stu-id="d95ef-189">Yes</span></span> | <span data-ttu-id="d95ef-190">会話識別子は、ボットの呼び出しの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-190">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="d95ef-191">例</span><span class="sxs-lookup"><span data-stu-id="d95ef-191">Example</span></span>

<span data-ttu-id="d95ef-192">は `Bot ID` マニフェストで宣言され、ボットは結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-192">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span> <span data-ttu-id="d95ef-193">次の例では、要求 `completionBotId` されたペイロードのパラメーター `externalResourceUrl` は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="d95ef-193">In the following example, the `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload:</span></span>

> [!NOTE]
> * <span data-ttu-id="d95ef-194">幅 `externalResourceUrl` と高さのパラメーターはピクセル単位である必要があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-194">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="d95ef-195">寸法が許容される制限内にあるか確認するには、「設計ガイドライン [」を参照してください](design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-195">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="d95ef-196">URL は、会議内ダイアログに表示 `<iframe>` されるページです。</span><span class="sxs-lookup"><span data-stu-id="d95ef-196">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="d95ef-197">ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-197">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="d95ef-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d95ef-198">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");

activity.ChannelData = new TeamsChannelData
  {
    Notification = new NotificationInfo()
                    {
                        AlertInMeeting = true,
                        ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
                    }
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="d95ef-199">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d95ef-199">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="d95ef-200">JSON</span><span class="sxs-lookup"><span data-stu-id="d95ef-200">JSON</span></span>](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities

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

* * *

#### <a name="response-codes"></a><span data-ttu-id="d95ef-201">応答コード</span><span class="sxs-lookup"><span data-stu-id="d95ef-201">Response Codes</span></span>

* <span data-ttu-id="d95ef-202">**201**: シグナルを含むアクティビティが正常に送信されます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-202">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="d95ef-203">**401**: トークンが無効です。</span><span class="sxs-lookup"><span data-stu-id="d95ef-203">**401**: Invalid token.</span></span>
* <span data-ttu-id="d95ef-204">**403**: アプリが信号を送信できません。</span><span class="sxs-lookup"><span data-stu-id="d95ef-204">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="d95ef-205">これは、テナント管理者がアプリを無効にし、アプリがライブ サイトの移行中にブロックされるなど、さまざまな理由で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-205">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="d95ef-206">この場合、ペイロードには詳細なエラー メッセージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d95ef-206">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="d95ef-207">**404**: 会議チャットが存在しません。</span><span class="sxs-lookup"><span data-stu-id="d95ef-207">**404**: Meeting chat does not exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="d95ef-208">Teams 会議でアプリを有効にする</span><span class="sxs-lookup"><span data-stu-id="d95ef-208">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="d95ef-209">アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="d95ef-209">Update your app manifest</span></span>

<span data-ttu-id="d95ef-210">会議アプリの機能は、構成可能な **Tabs** スコープとコンテキスト配列を使用してアプリ マニフェスト  ->  **で\*\*\*\*宣言** されます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-210">The meetings app capabilities are declared in your app manifest through the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="d95ef-211">*スコープ* は、アプリ *を使用できる* 場所を定義するユーザーとコンテキストを定義します。</span><span class="sxs-lookup"><span data-stu-id="d95ef-211">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="d95ef-212">アプリ マニフェストで [Developer Previewマニフェスト スキーマ](../resources/schema/manifest-schema-dev-preview.md) を使用してください。</span><span class="sxs-lookup"><span data-stu-id="d95ef-212">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="d95ef-213">Context プロパティ</span><span class="sxs-lookup"><span data-stu-id="d95ef-213">Context property</span></span>

<span data-ttu-id="d95ef-214">タブと `context` プロパティ `scopes` は調和して機能し、アプリを表示する場所を決定できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-214">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="d95ef-215">またはスコープ内 `team` のタブ `groupchat` には、複数のコンテキストを指定できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-215">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="d95ef-216">context プロパティで使用できる値は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d95ef-216">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="d95ef-217">**channelTab**: チーム チャネルのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="d95ef-217">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="d95ef-218">**privateChatTab**: チームや会議のコンテキストではない一連のユーザー間のグループ チャットのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="d95ef-218">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="d95ef-219">**meetingChatTab**: スケジュールされた会議のコンテキスト内の一連のユーザー間のグループ チャットのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="d95ef-219">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="d95ef-220">**meetingDetailsTab:** 予定表の会議の詳細ビューのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="d95ef-220">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="d95ef-221">**meetingSidePanel**: 統合バー (u-bar) を介して開いた会議内パネル。</span><span class="sxs-lookup"><span data-stu-id="d95ef-221">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="d95ef-222">"Context" プロパティは現在サポートされていないので、モバイル クライアントでは無視されます</span><span class="sxs-lookup"><span data-stu-id="d95ef-222">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="d95ef-223">会議シナリオ用にアプリを構成する</span><span class="sxs-lookup"><span data-stu-id="d95ef-223">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="d95ef-224">タブ ギャラリーにアプリを表示するには、構成可能なタブとグループ チャット **スコープをサポート\*\*\*\*する必要があります**。</span><span class="sxs-lookup"><span data-stu-id="d95ef-224">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="d95ef-225">モバイル クライアントは、会議表面の事前および投稿でのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="d95ef-225">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="d95ef-226">モバイルでの会議中のエクスペリエンス (会議中のダイアログとタブ) は近日公開されます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-226">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="d95ef-227">モバイル用 [のタブを作成する場合は、モバイル](../tabs/design/tabs-mobile.md) 上のタブのガイダンスに従います。</span><span class="sxs-lookup"><span data-stu-id="d95ef-227">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="d95ef-228">会議の前に</span><span class="sxs-lookup"><span data-stu-id="d95ef-228">Before a meeting</span></span>

<span data-ttu-id="d95ef-229">開催者または発表者の役割を持つユーザーは、会議チャットと会議の詳細ページのプラス ➕ボタンを使用して、会議にタブ **を追加** します。</span><span class="sxs-lookup"><span data-stu-id="d95ef-229">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="d95ef-230">メッセージング拡張機能は、チャット内のメッセージの作成領域 &#x25CF;&#x25CF;&#x25CF; 下にある省略記号/オーバーフロー メニューを介して追加されます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-230">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="d95ef-231">"" キーを使用して [ボットの取得] を選択すると、ボット **@** が会議チャット **に追加されます**。</span><span class="sxs-lookup"><span data-stu-id="d95ef-231">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="d95ef-232">✔ユーザー ID は *、Tabs* SSO を介して [確認する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-232">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="d95ef-233">この認証の後、アプリは GetParticipant API を介してユーザー ロールを取得できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-233">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="d95ef-234">✔ユーザー ロールに基づいて、アプリはロール固有のエクスペリエンスを表示する機能を持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-234">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="d95ef-235">たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-235">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="d95ef-236">**メモ**: 役割の割り当ては、会議の進行中に変更できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-236">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="d95ef-237">*「Teams* [会議での役割」を参照してください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-237">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="d95ef-238">会議中</span><span class="sxs-lookup"><span data-stu-id="d95ef-238">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="d95ef-239">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="d95ef-239">**sidePanel**</span></span>

<span data-ttu-id="d95ef-240">✔ アプリ マニフェストで、前述のようにコンテキスト配列に **sidePanel** を追加します。 </span><span class="sxs-lookup"><span data-stu-id="d95ef-240">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="d95ef-241">✔ 会議だけでなく、すべてのシナリオで、アプリは幅が 320px の会議内タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-241">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="d95ef-242">このためにタブを最適化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-242">Your tab must be optimized for this.</span></span> <span data-ttu-id="d95ef-243">*「FrameContext*[インターフェイス」を参照してください。](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="d95ef-243">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="d95ef-244">✔に応じて要求をルーティングするために **userContext** API を使用するために [Teams SDK](../tabs/how-to/access-teams-context.md#user-context)に参照します。</span><span class="sxs-lookup"><span data-stu-id="d95ef-244">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="d95ef-245">✔タブについては [、「Teams 認証フロー」を参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="d95ef-246">タブの認証フローは、Web サイトの認証フローと非常に似ています。</span><span class="sxs-lookup"><span data-stu-id="d95ef-246">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="d95ef-247">したがって、タブは OAuth 2.0 を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-247">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="d95ef-248">*「Microsoft* [IDENTITY プラットフォーム」および「OAuth 2.0 承認コード フロー」も参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-248">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="d95ef-249">✔メッセージ拡張機能は、ユーザーが会議内ビューに表示され、メッセージ内線カードの作成を投稿できる場合に期待通り機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-249">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="d95ef-250">✔ AppName の会議中 - ツールヒントに、会議内のアプリ名の U バーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d95ef-250">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="d95ef-251">**会議中ダイアログ**</span><span class="sxs-lookup"><span data-stu-id="d95ef-251">**In-meeting dialog**</span></span>

<span data-ttu-id="d95ef-252">✔会議中のダイアログデザインガイドライン [に従う必要があります](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="d95ef-253">✔タブについては [、「Teams 認証フロー」を参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="d95ef-254">✔ [NotificationSignal API を](create-apps-for-teams-meetings.md#notificationsignal-api) 使用して、バブル通知をトリガーする必要があるという通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="d95ef-254">✔ Use the [NotificationSignal API](create-apps-for-teams-meetings.md#notificationsignal-api) to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="d95ef-255">✔通知要求ペイロードの一部として、紹介するコンテンツがホストされている URL を含める。</span><span class="sxs-lookup"><span data-stu-id="d95ef-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="d95ef-256">✔会議中のダイアログでは、タスク モジュールを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="d95ef-256">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="d95ef-257">これらの通知は、自然の中で永続的です。</span><span class="sxs-lookup"><span data-stu-id="d95ef-257">These notifications are persistent in nature.</span></span> <span data-ttu-id="d95ef-258">ユーザーが Web ビューでアクションを実行した後 [**、submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出して自動終了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-258">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="d95ef-259">これは、アプリの申請に必要な要件です。</span><span class="sxs-lookup"><span data-stu-id="d95ef-259">This is a requirement for app submission.</span></span> <span data-ttu-id="d95ef-260">*「Teams* [SDK: タスク モジュール」も参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-260">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="d95ef-261">アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、オブジェクト内の (ユーザーの ID) 要求メタデータに依存する必要があります。(ユーザーの `from.id` `from` Azure Active Directory `from.aadObjectId` ID) 要求メタデータは使用しない必要があります。</span><span class="sxs-lookup"><span data-stu-id="d95ef-261">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="d95ef-262">*「タブ*[でのタスク モジュールの使用」および「](../task-modules-and-cards/task-modules/task-modules-tabs.md)[タスク モジュールの作成と送信」を参照してください](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。</span><span class="sxs-lookup"><span data-stu-id="d95ef-262">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="d95ef-263">会議の後</span><span class="sxs-lookup"><span data-stu-id="d95ef-263">After a meeting</span></span>

<span data-ttu-id="d95ef-264">会議後と会議前の構成は同等です。</span><span class="sxs-lookup"><span data-stu-id="d95ef-264">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="d95ef-265">会議アプリのサンプル</span><span class="sxs-lookup"><span data-stu-id="d95ef-265">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="d95ef-266">会議トークンジェネレーター アプリ</span><span class="sxs-lookup"><span data-stu-id="d95ef-266">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
