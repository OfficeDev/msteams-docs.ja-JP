---
title: Teams 会議用のアプリを作成する
author: laujan
description: チーム会議用アプリの作成
ms.topic: conceptual
ms.author: lajanuar
keywords: Teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: e768c2dc6722d006c89927adfe60e03243a076d0
ms.sourcegitcommit: f0dfae429385ef02f61896ad49172c4803ef6622
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2020
ms.locfileid: "49740872"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="c2531-104">Teams 会議用のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="c2531-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="c2531-105">前提条件と考慮事項</span><span class="sxs-lookup"><span data-stu-id="c2531-105">Prerequisites and considerations</span></span>

1. <span data-ttu-id="c2531-106">会議のアプリには、Teams アプリ開発に関する基本的な [知識が必要です](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c2531-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="c2531-107">会議内のアプリは、タブ、[](../tabs/what-are-tabs.md)ボット、[](../bots/what-are-bots.md)メッセージング拡張機能の機能[](../messaging-extensions/what-are-messaging-extensions.md)で構成できます。また[、Teams](#update-your-app-manifest)アプリ マニフェストを更新して、アプリが会議で利用できる状態を示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="c2531-108">アプリをタブとして会議のライフサイクルで機能するには、グループチャット スコープで構成可能なタブをサポート [する必要があります](../resources/schema/manifest-schema.md#configurabletabs)。</span><span class="sxs-lookup"><span data-stu-id="c2531-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="c2531-109">*「Teams* [アプリをカスタム タブで拡張する」を参照してください](../tabs/how-to/add-tab.md)。スコープを `groupchat` サポートすると、会議前および [](teams-apps-in-meetings.md#pre-meeting-app-experience)会議後のチャット [でアプリを](teams-apps-in-meetings.md#post-meeting-app-experience)有効にできます。</span><span class="sxs-lookup"><span data-stu-id="c2531-109">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="c2531-110">会議 API URL パラメーターには、必要な場合があります。tenantId これらは、Teams クライアント SDK およびボット アクティビティの一 `meetingId` `userId` 部として利用できます。 [](/onedrive/find-your-office-365-tenant-id)</span><span class="sxs-lookup"><span data-stu-id="c2531-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="c2531-111">さらに、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼性の高い [情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="c2531-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="c2531-112">一部の会議 API では、認証トークンを生成するためにボット登録とボット アプリ `GetParticipant` [ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) が必要になります。</span><span class="sxs-lookup"><span data-stu-id="c2531-112">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="c2531-113">開発者は、会議前および会議後のシナリオに関する一般的な[Teams](../tabs/design/tabs.md)タブ設計ガイドライン、および Teams[](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)会議中にトリガーされる会議内ダイアログのガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-113">As a developer, you must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) for in-meeting dialog triggered during a Teams meeting.</span></span>

1. <span data-ttu-id="c2531-114">アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-114">Please note that in order for your app to be updated in real-time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="c2531-115">これらのイベントは、会議のライフサイクル全体にわたって、会議内ダイアログ (完了パラメーターを参照) 内に含め、その他 `bot Id` `Notification Signal API` のサーフェスにできます。</span><span class="sxs-lookup"><span data-stu-id="c2531-115">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="c2531-116">会議アプリ API リファレンス</span><span class="sxs-lookup"><span data-stu-id="c2531-116">Meeting apps API reference</span></span>

|<span data-ttu-id="c2531-117">API</span><span class="sxs-lookup"><span data-stu-id="c2531-117">API</span></span>|<span data-ttu-id="c2531-118">説明</span><span class="sxs-lookup"><span data-stu-id="c2531-118">Description</span></span>|<span data-ttu-id="c2531-119">要求</span><span class="sxs-lookup"><span data-stu-id="c2531-119">Request</span></span>|<span data-ttu-id="c2531-120">ソース</span><span class="sxs-lookup"><span data-stu-id="c2531-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="c2531-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="c2531-121">**GetUserContext**</span></span>| <span data-ttu-id="c2531-122">関連するコンテンツを Teams タブに表示するコンテキスト情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="c2531-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="c2531-123">_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="c2531-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="c2531-124">Microsoft Teams クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="c2531-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="c2531-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="c2531-125">**GetParticipant**</span></span>|<span data-ttu-id="c2531-126">この API を使用すると、ボットは会議 ID と参加者 ID で参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="c2531-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="c2531-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="c2531-128">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="c2531-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="c2531-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="c2531-129">**NotificationSignal**</span></span> |<span data-ttu-id="c2531-130">会議のシグナルは、次の既存の会話通知 API (ユーザーボット チャット用) を使用して配信されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="c2531-131">この API を使用すると、開発者はエンドユーザーのアクションに基づいてシグナルを送信し、会議中のダイアログ バブルを表示できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="c2531-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="c2531-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="c2531-133">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="c2531-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="c2531-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="c2531-134">GetUserContext</span></span>

<span data-ttu-id="c2531-135">タブ コンテンツのコンテキスト情報の特定と取得に関するガイダンスについては [、Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) タブのドキュメントのコンテキストの取得を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2531-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="c2531-136">会議の拡張性の一環として、応答ペイロードに新しい値が追加されました。</span><span class="sxs-lookup"><span data-stu-id="c2531-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="c2531-137">✔ **meetingId**: 会議コンテキストで実行するときにタブによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="c2531-138">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="c2531-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="c2531-139">会議の開催者は任意の時点で役割を変更できるので、参加者の役割をキャッシュに入らない。</span><span class="sxs-lookup"><span data-stu-id="c2531-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="c2531-140">Teams は現在、API の参加者が 350 人を超える大規模な配布リストや名簿サイズをサポート `GetParticipant` していない。</span><span class="sxs-lookup"><span data-stu-id="c2531-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="c2531-141">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="c2531-141">Query parameters</span></span>

|<span data-ttu-id="c2531-142">値</span><span class="sxs-lookup"><span data-stu-id="c2531-142">Value</span></span>|<span data-ttu-id="c2531-143">型</span><span class="sxs-lookup"><span data-stu-id="c2531-143">Type</span></span>|<span data-ttu-id="c2531-144">必須</span><span class="sxs-lookup"><span data-stu-id="c2531-144">Required</span></span>|<span data-ttu-id="c2531-145">説明</span><span class="sxs-lookup"><span data-stu-id="c2531-145">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="c2531-146">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="c2531-146">**meetingId**</span></span>| <span data-ttu-id="c2531-147">文字列</span><span class="sxs-lookup"><span data-stu-id="c2531-147">string</span></span> | <span data-ttu-id="c2531-148">はい</span><span class="sxs-lookup"><span data-stu-id="c2531-148">Yes</span></span> | <span data-ttu-id="c2531-149">会議識別子は、Bot Invoke と Teams クライアント SDK から利用できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-149">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="c2531-150">**participantId**</span><span class="sxs-lookup"><span data-stu-id="c2531-150">**participantId**</span></span>| <span data-ttu-id="c2531-151">文字列</span><span class="sxs-lookup"><span data-stu-id="c2531-151">string</span></span> | <span data-ttu-id="c2531-152">はい</span><span class="sxs-lookup"><span data-stu-id="c2531-152">Yes</span></span> | <span data-ttu-id="c2531-153">participantId はユーザー ID です。</span><span class="sxs-lookup"><span data-stu-id="c2531-153">The participantId is the user ID.</span></span> <span data-ttu-id="c2531-154">タブ SSO、ボット呼び出し、および Teams クライアント SDK で利用できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-154">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="c2531-155">Tab SSO から participantId を取得することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c2531-155">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="c2531-156">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="c2531-156">**tenantId**</span></span>| <span data-ttu-id="c2531-157">文字列</span><span class="sxs-lookup"><span data-stu-id="c2531-157">string</span></span> | <span data-ttu-id="c2531-158">はい</span><span class="sxs-lookup"><span data-stu-id="c2531-158">Yes</span></span> | <span data-ttu-id="c2531-159">テナント ユーザーには tenantId が必要です。</span><span class="sxs-lookup"><span data-stu-id="c2531-159">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="c2531-160">タブ SSO、ボット呼び出し、および Teams クライアント SDK で利用できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-160">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="c2531-161">Tab SSO から tenantId を取得することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c2531-161">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="c2531-162">例</span><span class="sxs-lookup"><span data-stu-id="c2531-162">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c2531-163">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c2531-163">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="c2531-164">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c2531-164">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="c2531-165">JSON</span><span class="sxs-lookup"><span data-stu-id="c2531-165">JSON</span></span>](#tab/json)

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="c2531-166">応答本文は次の場所に含されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-166">The response body is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="c2531-167">応答コード</span><span class="sxs-lookup"><span data-stu-id="c2531-167">Response codes</span></span>

* <span data-ttu-id="c2531-168">**403**: アプリは、参加者の情報を取得する許可されません。</span><span class="sxs-lookup"><span data-stu-id="c2531-168">**403**: The app is not allowed to get participant information.</span></span>  <span data-ttu-id="c2531-169">これは最も一般的なエラー応答であり、アプリが会議にインストールされていない場合にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="c2531-169">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="c2531-170">たとえば、テナント管理者によってアプリが無効になっている場合や、ライブ サイトの移行中にブロックされた場合です。</span><span class="sxs-lookup"><span data-stu-id="c2531-170">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>
* <span data-ttu-id="c2531-171">**200**: 参加者の情報が正常に取得されました。</span><span class="sxs-lookup"><span data-stu-id="c2531-171">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="c2531-172">**401**: 無効なトークンです。</span><span class="sxs-lookup"><span data-stu-id="c2531-172">**401**: Invalid token.</span></span>
* <span data-ttu-id="c2531-173">**404**: 参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="c2531-173">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="c2531-174">**500**: 会議の有効期限が切れているか (会議の終了から 60 日を超える) か、参加者の役割に基づいてアクセス許可を持っていません。</span><span class="sxs-lookup"><span data-stu-id="c2531-174">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="c2531-175">**近日公開**</span><span class="sxs-lookup"><span data-stu-id="c2531-175">**Coming Soon**</span></span>

* <span data-ttu-id="c2531-176">**404**: 会議の有効期限が切れているか、参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="c2531-176">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="c2531-177">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="c2531-177">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="c2531-178">会議中ダイアログが呼び出されると、同じコンテンツがチャット メッセージとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-178">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="c2531-179">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="c2531-179">Query parameters</span></span>

|<span data-ttu-id="c2531-180">値</span><span class="sxs-lookup"><span data-stu-id="c2531-180">Value</span></span>|<span data-ttu-id="c2531-181">型</span><span class="sxs-lookup"><span data-stu-id="c2531-181">Type</span></span>|<span data-ttu-id="c2531-182">必須</span><span class="sxs-lookup"><span data-stu-id="c2531-182">Required</span></span>|<span data-ttu-id="c2531-183">説明</span><span class="sxs-lookup"><span data-stu-id="c2531-183">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="c2531-184">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="c2531-184">**conversationId**</span></span>| <span data-ttu-id="c2531-185">文字列</span><span class="sxs-lookup"><span data-stu-id="c2531-185">string</span></span> | <span data-ttu-id="c2531-186">はい</span><span class="sxs-lookup"><span data-stu-id="c2531-186">Yes</span></span> | <span data-ttu-id="c2531-187">会話識別子はボット呼び出しの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-187">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="c2531-188">例</span><span class="sxs-lookup"><span data-stu-id="c2531-188">Example</span></span>

> [!NOTE]
>
<span data-ttu-id="c2531-189">要求 `completionBotId` されたペイロードの `externalResourceUrl` 例では、パラメーターは省略可能です。</span><span class="sxs-lookup"><span data-stu-id="c2531-189">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="c2531-190">`Bot ID` がマニフェストで宣言され、ボットが結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="c2531-190">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="c2531-191">externalResourceUrl の幅と高さのパラメーターはピクセル単位である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-191">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="c2531-192">サイズが [許容される制限](design/designing-apps-in-meetings.md) の範囲内にあるかについては、設計ガイドラインを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2531-192">Refer to the [design guidelines](design/designing-apps-in-meetings.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="c2531-193">URL は、会議中ダイアログで読 `<iframe>` み込まれたページです。</span><span class="sxs-lookup"><span data-stu-id="c2531-193">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="c2531-194">ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列に含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-194">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c2531-195">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c2531-195">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="c2531-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c2531-196">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="c2531-197">JSON</span><span class="sxs-lookup"><span data-stu-id="c2531-197">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="c2531-198">応答コード</span><span class="sxs-lookup"><span data-stu-id="c2531-198">Response Codes</span></span>

* <span data-ttu-id="c2531-199">**201**: シグナルを含むアクティビティが正常に送信される</span><span class="sxs-lookup"><span data-stu-id="c2531-199">**201**: activity with signal is successfully sent</span></span>  
* <span data-ttu-id="c2531-200">**401**: 無効なトークン</span><span class="sxs-lookup"><span data-stu-id="c2531-200">**401**: invalid token</span></span>  
* <span data-ttu-id="c2531-201">**201**: シグナルを含むアクティビティが正常に送信されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-201">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="c2531-202">**401**: 無効なトークンです。</span><span class="sxs-lookup"><span data-stu-id="c2531-202">**401**: Invalid token.</span></span>
* <span data-ttu-id="c2531-203">**403**: アプリは信号を送信できません。</span><span class="sxs-lookup"><span data-stu-id="c2531-203">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="c2531-204">これは、テナント管理者がアプリを無効にし、ライブ サイトの移行中にアプリがブロックされるなどのさまざまな理由で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-204">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="c2531-205">この場合、ペイロードには詳細なエラー メッセージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c2531-205">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="c2531-206">**404**: 会議チャットが存在しません。</span><span class="sxs-lookup"><span data-stu-id="c2531-206">**404**: Meeting chat doesn't exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="c2531-207">Teams 会議用にアプリを有効にする</span><span class="sxs-lookup"><span data-stu-id="c2531-207">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="c2531-208">アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="c2531-208">Update your app manifest</span></span>

<span data-ttu-id="c2531-209">会議アプリの機能は **、configurableTabs** スコープとコンテキスト配列を介してアプリ マニフェスト  ->  で **宣言** されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-209">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="c2531-210">*スコープ* は、アプリを利用できる場所 *を* 定義するユーザーとコンテキストを定義します。</span><span class="sxs-lookup"><span data-stu-id="c2531-210">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="c2531-211">アプリ マニフェスト [でDeveloper Previewマニフェスト](../resources/schema/manifest-schema-dev-preview.md) スキーマを使用して試してください。</span><span class="sxs-lookup"><span data-stu-id="c2531-211">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="c2531-212">Context プロパティ</span><span class="sxs-lookup"><span data-stu-id="c2531-212">Context property</span></span>

<span data-ttu-id="c2531-213">タブとプロパティは調和して機能し、アプリを表示する `context` `scopes` 場所を決定できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-213">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="c2531-214">スコープ内の `team` タブ `groupchat` は、複数のコンテキストを持つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-214">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="c2531-215">コンテキスト プロパティに使用できる値は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c2531-215">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="c2531-216">**channelTab**: チーム チャネルのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="c2531-216">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="c2531-217">**privateChatTab**: チームまたは会議のコンテキスト内に存在しない一連のユーザー間のグループ チャットのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="c2531-217">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="c2531-218">**meetingChatTab**: スケジュールされた会議のコンテキストで一連のユーザー間のグループ チャットのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="c2531-218">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="c2531-219">**meetingDetailsTab**: 予定表の会議詳細ビューのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="c2531-219">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="c2531-220">**meetingSidePanel**: 統合バー (u-bar) 経由で開いた会議内パネル。</span><span class="sxs-lookup"><span data-stu-id="c2531-220">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="c2531-221">"Context" プロパティは現在サポートされていないので、モバイル クライアントでは無視されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-221">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="c2531-222">会議シナリオ用にアプリを構成する</span><span class="sxs-lookup"><span data-stu-id="c2531-222">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="c2531-223">アプリをタブ ギャラリーに表示するには、構成可能なタブとグループ **チャットスコープ** をサポート **する必要があります**。</span><span class="sxs-lookup"><span data-stu-id="c2531-223">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="c2531-224">モバイル クライアントは、会議前サーフェスと会議後サーフェスでのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="c2531-224">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="c2531-225">モバイルでの会議中のエクスペリエンス (会議中のダイアログとタブ) は間もなく利用できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-225">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="c2531-226">モバイル用 [のタブを作成する場合は、モバイル](../tabs/design/tabs-mobile.md) のタブのガイダンスに従います。</span><span class="sxs-lookup"><span data-stu-id="c2531-226">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="c2531-227">会議の前に</span><span class="sxs-lookup"><span data-stu-id="c2531-227">Before a meeting</span></span>

<span data-ttu-id="c2531-228">開催者または発表者の役割を持つユーザーは、会議チャットおよび会議の詳細ページのプラス ➕ ボタンを使用して、会議に **タブを\*\*\*\*追加** します。</span><span class="sxs-lookup"><span data-stu-id="c2531-228">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="c2531-229">メッセージング拡張機能は、チャットのメッセージ作成領域 &#x25CF;&#x25CF;&#x25CF; 下にある省略記号/オーバーフロー メニューを介して追加されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-229">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="c2531-230">ボットは、"" キーを使用して [ボットの取得] を選択して会議 **@** チャット **に追加されます**。</span><span class="sxs-lookup"><span data-stu-id="c2531-230">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="c2531-231">✔は、Tabs SSO *を使用して* 確認 [する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="c2531-231">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="c2531-232">この認証の後、アプリは GetParticipant API を介してユーザー ロールを取得できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-232">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="c2531-233">✔ユーザー ロールに基づいて、アプリはロール固有のエクスペリエンスを表示する機能を備えています。</span><span class="sxs-lookup"><span data-stu-id="c2531-233">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="c2531-234">たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-234">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="c2531-235">**注**: 会議の進行中は、役割の割り当てを変更できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-235">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="c2531-236">*「Teams* [会議での役割」を参照してください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="c2531-236">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="c2531-237">会議中</span><span class="sxs-lookup"><span data-stu-id="c2531-237">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="c2531-238">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="c2531-238">**sidePanel**</span></span>

<span data-ttu-id="c2531-239">✔マニフェストで、上記のようにコンテキスト配列に **sidePanel** を追加します。</span><span class="sxs-lookup"><span data-stu-id="c2531-239">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="c2531-240">✔とすべてのシナリオで、アプリは幅 320 ピクセルの会議内タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-240">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="c2531-241">このためには、タブを最適化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-241">Your tab must be optimized for this.</span></span> <span data-ttu-id="c2531-242">*「FrameContext*[インターフェイス」を参照](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="c2531-242">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="c2531-243">✔に応じて[、userContext](../tabs/how-to/access-teams-context.md#user-context) API を使用して要求をルーティングするために Teams SDK に参照します。</span><span class="sxs-lookup"><span data-stu-id="c2531-243">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="c2531-244">✔タブの Teams 認証 [フローを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="c2531-244">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="c2531-245">タブの認証フローは、Web サイトの認証フローと非常に似ています。</span><span class="sxs-lookup"><span data-stu-id="c2531-245">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="c2531-246">したがって、タブは OAuth 2.0 を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="c2531-246">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="c2531-247">*「Microsoft* [ID プラットフォーム」および「OAuth 2.0 認証コード フロー」も参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。</span><span class="sxs-lookup"><span data-stu-id="c2531-247">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="c2531-248">✔は、ユーザーが会議中のビューで、作成メッセージの内線カードを投稿できる必要がある場合に、期待通り動作する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-248">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="c2531-249">✔ AppName in meeting - ツールヒントには、会議中の U バーにアプリ名が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c2531-249">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="c2531-250">**会議中ダイアログ**</span><span class="sxs-lookup"><span data-stu-id="c2531-250">**In-meeting dialog**</span></span>

<span data-ttu-id="c2531-251">✔、会議中のダイアログの [設計ガイドラインに従う必要があります](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="c2531-251">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="c2531-252">✔タブの Teams 認証 [フローを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="c2531-252">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="c2531-253">✔ API を [使用して](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) 、バブル通知をトリガーする必要がある場合に通知します。</span><span class="sxs-lookup"><span data-stu-id="c2531-253">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="c2531-254">✔要求ペイロードの一部として、紹介するコンテンツがホストされている URL を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-254">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="c2531-255">✔ダイアログでタスク モジュールを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="c2531-255">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="c2531-256">これらの通知は、実際には永続的です。</span><span class="sxs-lookup"><span data-stu-id="c2531-256">These notifications are persistent in nature.</span></span> <span data-ttu-id="c2531-257">ユーザーが Web ビューでアクションを実行した後 [**、submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出して自動終了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-257">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="c2531-258">これは、アプリの申請の要件です。</span><span class="sxs-lookup"><span data-stu-id="c2531-258">This is a requirement for app submission.</span></span> <span data-ttu-id="c2531-259">*「Teams* [SDK: タスク モジュール」も参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="c2531-259">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="c2531-260">アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、(ユーザーの Azure Active Directory ID) 要求メタデータではなく、オブジェクト内の `from.id` `from` (ユーザーの `from.aadObjectId` ID) 要求メタデータに依存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2531-260">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="c2531-261">*「タブ*[でのタスク モジュールの使用」と「](../task-modules-and-cards/task-modules/task-modules-tabs.md)タスク モジュールを作成 [して送信する」を参照してください](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。</span><span class="sxs-lookup"><span data-stu-id="c2531-261">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="c2531-262">会議後</span><span class="sxs-lookup"><span data-stu-id="c2531-262">After a meeting</span></span>

<span data-ttu-id="c2531-263">会議後と会議前の構成は同等です。</span><span class="sxs-lookup"><span data-stu-id="c2531-263">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="c2531-264">会議アプリのサンプル</span><span class="sxs-lookup"><span data-stu-id="c2531-264">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="c2531-265">会議トークンジェネレーター アプリ</span><span class="sxs-lookup"><span data-stu-id="c2531-265">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
